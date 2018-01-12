---
title: "Restauração do pacote do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Uma descrição de como o NuGet restaura os pacotes dos quais um projeto depende, incluindo como desabilitar a restauração e restringir as versões."
keywords: "Restauração de pacote do NuGet, instalação de pacote do NuGet, instalar o pacote, restaurando pacotes, versões de dependência, desabilitar a restauração automática, restringindo as versões do pacote"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4e819a2bb34bbe70f0f11d5adeed82b976a8cb65
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="package-restore"></a>Restauração de pacote

Para promover um ambiente de desenvolvimento mais limpo e reduzir o tamanho do repositório, a **Restauração de pacote** do NuGet instala todos os pacotes referenciados antes de um projeto ser compilado. Esse recurso amplamente utilizado garante que todas as dependências estejam disponíveis em um projeto sem precisar armazenar tais pacotes no controle do código-fonte (consulte [Pacotes e controle do código-fonte](../consume-packages/packages-and-source-control.md) para ver como configurar seu repositório para excluir binários de pacote).

Neste tópico:
- [Guia rápido de restauração de pacote](#quick-guide-to-package-restore)
- [Visão geral de restauração de pacote](#package-restore-overview)
- [Habilitar e desabilitar a restauração do pacote](#enabling-and-disabling-package-restore)
- [Restrições de versões de pacote com restauração](#constraining-package-versions-with-restore)
- [Restauração de linha de comando](#command-line-restore) para todas as versões do NuGet
- [Restauração automática no Visual Studio](#automatic-restore-in-visual-studio) para o NuGet 2.7 e posterior.
- [Restauração integrada do MSBuild no Visual Studio](#msbuild-integrated-restore) para o NuGet 2.6 e versões anteriores.
- [Restauração de pacote com o Team Foundation Build](#package-restore-with-team-foundation-build)

O comportamento de restauração varia de acordo com a versão; para verificar a versão do NuGet, basta executar `nuget.exe` na linha de comando e examinar a primeira linha de saída.

Para ver detalhes adicionais sobre a restauração de pacote nos servidores de build, consulte [Restauração de pacote com TFBuild](../consume-packages/team-foundation-build.md).

> [!Note]
> Projetos configurados para restauração de pacote também funcionam com xbuild no Mono.

## <a name="quick-guide-to-package-restore"></a>Guia rápido de restauração de pacote

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> Se você encontrar o erro “Este projeto faz referência a pacotes do NuGet que estão ausentes neste computador” ou “Um ou mais pacotes do NuGet precisam ser restaurados, mas não foi possível fazer isso, pois o consentimento não foi concedido”, ative a restauração automática seguindo as instruções em [Habilitando e desabilitando a restauração do pacote](#enabling-and-disabling-package-restore).

## <a name="package-restore-overview"></a>Visão geral de restauração de pacote

Primeiro, as referências de pacote são mantidas em um dos seguintes formatos de gerenciamento de pacotes, dependendo do tipo de projeto e a versão do NuGet. (Observe que o NuGet 4 e o MSBuild 15.1 são instalados com o Visual Studio 2017.)

| Método | Versão do NuGet | Descrição | 
| --- | --- | --- |
| `packages.config` | 2.x ou superior | Lista o conjunto aprofundado completo de dependências. Pacotes adicionados ao `packages.config` também precisam ser adicionados ao arquivo de projeto, assim como os Destinos e Objetos. Esse é o método de linha de base para todas as versões do NuGet, mas tem um desempenho mais lento comparado com as outras opções. (Consulte [Esquema packages.config](../schema/packages-config.md).) | 
| `project.json` | 3.x ou superior | Usado somente por padrão com os projetos UWP, mas projetos podem ser convertidos de `packages.config`. `project.json` lista somente as dependências de nível superior. Referências, Destinos e Objetos são adicionados dinamicamente ao projeto durante o build, resultando em um melhor desempenho em comparação com `packages.config`. (Consulte [Esquema project.json](../schema/project-json.md).)|
| PackageReference | 4.x ou superior | Lista as dependências diretamente no arquivo de projeto no nó `<PackageReference>`, junto com `<Reference>` e `<ProjectReference>`. Funciona de forma semelhante com o `project.json`; consulte [Referências de pacote em arquivos de projeto](../Consume-Packages/Package-References-in-Project-Files.md). |

Em segundo, você iniciará uma restauração usando a lista de referência de várias maneiras:

Na linha de comando ou no [Console de Gerenciador de Pacotes](../tools/Package-Manager-Console.md):

| Comando | Cenários aplicáveis |
| --- | --- | 
| `nuget restore` | Todas as versões do NuGet e todos os tipos de referência. Consulte [Restauração da linha de comando](#command-line-restore) abaixo. | 
| `dotnet restore` | O mesmo que `nuget restore` para projetos .NET Core. Consulte [dotnet restore](/dotnet/articles/core/tools/dotnet-restore). |
| `msbuild /t:restore` | Nuget 4.x e superior e MSBuild 15.1 e superior somente com [referências de pacote em arquivos de projeto](../Consume-Packages/Package-References-in-Project-Files.md). `nuget restore` e `dotnet restore` usam esse comando para projetos aplicável. Consulte [Empacotamento e restauração do NuGet como destinos do MSBuild- restore target](../schema/msbuild-targets.md#restore-target).|

O próprio Visual Studio também restaura pacotes em momentos diferentes:

| Tipo | Quando ocorre a restauração |
| --- | --- |
| Restauração de modelo | Durante a criação de um novo projeto, visto que alguns modelos dependem de pacotes externos. |
| Restauração de build | Como a primeira etapa de um build. |
| Restauração de solução | Quando o usuário clica com o botão direito do mouse em uma solução e seleciona **Restaurar pacotes do NuGet**. |
| Restaurar na alteração do projeto | *(Somente NuGet 4.x)* Quando um projeto baseado no SDK do .NET Core é usado, incluindo quando as alterações de estado do projeto. |

## <a name="enabling-and-disabling-package-restore"></a>Habilitar e desabilitar a restauração do pacote

A restauração do pacote é habilitada primariamente por meio de **Ferramentas > Opções > Gerenciador de Pacotes do NuGet** no Visual Studio:

![Controlar comportamentos de restauração do pacote por meio de opções do Gerenciador de Pacotes do NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Permitir que o NuGet baixe pacotes ausentes**: controla todas as formas de restauração de pacotes alterando a configuração `packageRestore/enabled` no arquivo `%AppData%\NuGet\NuGet.Config` conforme mostrado abaixo.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  A configuração `packageRestore/enabled` pode ser substituída globalmente definindo uma variável de ambiente chamada **EnableNuGetPackageRestore** com um valor de TRUE ou FALSE antes de abrir o Visual Studio ou iniciar um build.
    

- **Verificar automaticamente os pacotes ausentes durante o build no Visual Studio**: controla a restauração automática para NuGet 2.7 e posterior, alterando a configuração `packageRestore/automatic` no arquivo `%AppData%\NuGet\NuGet.Config` conforme mostrado abaixo.
            
    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

Para referência, consulte o [Arquivo de configuração do NuGet – Seção packageRestore](../Schema/nuget-config-file.md#packagerestore-section).

Em alguns casos, um desenvolvedor ou empresa podem optar por habilitar ou desabilitar a restauração de pacotes em um computador por padrão para todos os usuários. Isso pode ser feito adicionando as mesmas configurações acima ao arquivo de configuração global do NuGet localizado em `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`. Usuários individuais poderão, então, habilitar seletivamente a restauração conforme necessário no nível do projeto. Consulte [Configurando o comportamento do NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) para ver os detalhes sobre como o NuGet prioriza vários arquivos de configuração.

## <a name="constraining-package-versions-with-restore"></a>Restrições de versões de pacote com restauração

Quando o NuGet restaura pacotes por meio de qualquer método, ele aceitará quaisquer restrições especificadas no `packages.config`, `project.json` ou no arquivo de projeto:

- `packages.config`: especifique um intervalo de versão na propriedade `allowedVersion` da dependência. Consulte [Reinstalando e atualizando pacotes](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Por exemplo:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- `project.json`: especifique um intervalo de versão diretamente com o número de versão da dependência. Por exemplo:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- Referências de pacote nos arquivos de projeto: especifique um intervalo de versão diretamente com o número de versão da dependência. Por exemplo:
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

Em todo os casos, use a notação descrita em [Controle de versão do pacote](../reference/package-versioning.md).

## <a name="command-line-restore"></a>Restauração da linha de comando

Para NuGet 2.7 e posterior, use o [restaurar](../tools/cli-ref-restore.md) comando para restaurar todos os pacotes em uma solução (independente de se ele usa `packages.config`, `project.json` ou as referências de pacote em arquivos de projeto). Para determinada pasta de projeto como `c:\proj\app`, as variações comuns abaixo restauram os pacotes:

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

Para NuGet 4.0 ou superior e MSBuild 15.1 ou superior, também é possível usar `MSBuild /t:restore` conforme descrito em [Empacotamento e restauração do NuGet como destinos do MSBuild](../schema/msbuild-targets.md).

## <a name="build-time-restore-in-visual-studio"></a>Restauração de tempo de build no Visual Studio

O Visual Studio restaura automaticamente os pacotes ausentes por padrão no início de um build. Esse comportamento pode ser alterado desmarcando **Ferramentas > Opções > Gerenciador do Pacote do NuGet > Geral > Verificar automaticamente os pacotes ausentes durante o build no Visual Studio**.

Quando habilitada, a restauração automática funciona da seguinte maneira:

1. Quando um build é iniciado, o Visual Studio instrui o NuGet a restaurar os pacotes.
1. O NuGet busca recursivamente todos os arquivos `packages.config` na solução, busca por `project.json` ou procura no arquivo de projeto.
1. Para cada pacote listados nos arquivos de referência, o NuGet verifica se ele já existe na solução (o pasta `packages`, `project.lock.json` ou `project.assets.json`, dependendo se o projeto está usando `packages.config`, `project.json` ou referências de pacote nos arquivos do projeto).
1. Se o pacote não for encontrado, o NuGet tentará recuperá-lo do seu cache primeiro (consulte [Gerenciamento do cache do NuGet](../consume-packages/managing-the-nuget-cache.md). Se o pacote não estiver no cache, o NuGet tentará baixá-lo das origens habilitadas, conforme listado em **Ferramentas > Opções > Gerenciador de Pacotes do NuGet > Origens de Pacote**, na ordem em que elas aparecem. Nesse caso, o NuGet não indica uma falha ao localizar o pacote até que todas as origens tenham sido verificadas, quando então ele relata a falha somente para a última origem na lista. Implicitamente, esse erro também significa que o pacote não estava presente em nenhuma das outras fontes, mesmo que os erros não tenham sido mostrados para as fontes individualmente.
1. Se o download for bem-sucedido, o NuGet armazena o pacote em cache e o instala na solução (novamente, na pasta `packages`, `project.lock.json` ou `project.assets.json`); caso contrário o NuGet falhará e o build falhará.

Durante esse processo, você verá uma caixa de diálogo de andamento com a opção para cancelar a restauração do pacote.

## <a name="package-restore-with-team-foundation-build"></a>Restauração de Pacote com o Team Foundation Build

A restauração do pacote normalmente é usada ao criar projetos em servidores de build, assim como acontece com o TFS (Team Foundation Server) e o Visual Studio Team Services (bem como outros sistemas de build, que não são abordados aqui).

### <a name="visual-studio-team-services"></a>Visual Studio Team Services

Ao criar uma definição de build do Team Services, basta incluir a tarefa Restaurar pacotes do NuGet na definição do antes de qualquer tarefa de build. Essa tarefa é incluída por padrão em diversos modelos de build.

![Tarefa de restauração de pacote do NuGet em uma definição de build do Visual Studio Team Service](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a>Team Foundation Server

Com o TFS 2013 e posterior, os pacotes são automaticamente restaurados por padrão durante o build, desde que você esteja usando um modelo do Team Build para Team Foundation Server 2013 ou posterior.

Se estiver usando uma versão anterior dos modelos de build (como em um projeto que foi migrado de versões anteriores do TFS), você também precisará migrar esses modelos de build para o TFS 2013. Isso significa basicamente recriar as partes personalizadas dos Modelos de build usando o modelo apropriado para o controle do código-fonte (TFVC ou Git).

Para obter uma versão anterior do TFS, você pode simplesmente incluir uma etapa de build para invocar [restauração de linha de comando](#command-line-restore) conforme descrito anteriormente.

Para obter mais detalhes, consulte [Explicação passo a passo da restauração de pacotes com o Team Foundation Build](../consume-packages/team-foundation-build.md).    
