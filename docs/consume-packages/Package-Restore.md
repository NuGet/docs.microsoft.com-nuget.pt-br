---
title: Restauração de pacote do NuGet
description: Uma visão geral de como o NuGet restaura os pacotes dos quais um projeto depende, incluindo como desabilitar a restauração e restringir as versões.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9acb87a5f5731fb33c91a1ae9b106c6df492ddcd
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453527"
---
# <a name="package-restore"></a>Restauração de pacote

Para promover um ambiente de desenvolvimento mais limpo e reduzir o tamanho do repositório, a **Restauração de pacote** do NuGet instala todas as dependências de um projeto conforme listado no arquivo de projeto ou em `packages.config`. O Visual Studio pode restaurar pacotes automaticamente quando um projeto é compilado. Os comandos `dotnet build` e `dotnet run` (.NET Core 2.0 ou posterior) também executam uma restauração automática. Também é possível restaurar pacotes a qualquer momento por meio do Visual Studio, `nuget restore`, `dotnet restore` e xbuild no Mono.

A restauração de pacote garante que todas as dependências de um projeto estejam disponíveis sem armazenar esses pacotes no controle do código-fonte. Confira [Pacotes e controle do código-fonte](../consume-packages/packages-and-source-control.md) para ver como configurar seu repositório para excluir os binários do pacote.

## <a name="package-restore-overview"></a>Visão geral de restauração de pacote

Primeiro, a restauração de pacotes instala as dependências diretas de um projeto conforme o necessário, depois instala todas as dependências desses pacotes em todo o grafo de dependência.

Se um pacote ainda não estiver instalado, primeiro o NuGet tentará recuperá-lo do [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). Se o pacote não estiver no cache, o NuGet tentará baixar o pacote de todas as origens habilitadas (confira [Como configurar o comportamento do NuGet](Configuring-NuGet-Behavior.md)); as origens também aparecem na lista **Ferramentas > Opções > Gerenciador de Pacotes do NuGet > Origens de Pacotes** no Visual Studio). Durante a restauração, o NuGet ignora a ordem das origens de pacotes usando o pacote de qualquer origem que responder às solicitações primeiro.

> [!Note]
> O NuGet não indicará a falha na restauração de um pacote até que todas as origens sejam verificadas. Nesse momento, o NuGet relatará uma falha somente para a última origem na lista. O erro indica que o pacote não estava presente em *nenhuma* das outras origens, mesmo que os erros não sejam mostrados para cada um dessas fontes individualmente.

A restauração do pacote é disparada das seguintes maneiras:

- **CLI do dotnet**: use o comando [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), que restaura os pacotes listados no arquivo do projeto (veja [PackageReference](../consume-packages/package-references-in-project-files.md)). Com o .NET Core 2.0 e posterior, a restauração é feita automaticamente com `dotnet build` e `dotnet run`.

- **IU do Gerenciador de pacote (Visual Studio no Windows)**: os pacotes são restaurados automaticamente ao criar um projeto de um modelo e ao compilar um projeto (sujeito à opção descrita em [Habilitar e desabilitar a restauração do pacote](#enabling-and-disabling-package-restore)). No NuGet 4.0 +, a restauração também ocorre automaticamente quando as alterações são feitas em um projeto baseado no SDK do .NET Core.

    Para restaurar manualmente, clique com o botão direito na solução no Gerenciador de Soluções e selecione **Restaurar Pacotes NuGet**. Se um ou mais pacotes individuais ainda não tiverem sido instalados corretamente (o que significa que o Gerenciador de Soluções mostra um ícone de erro), use a interface do usuário do Gerenciador de Pacotes para desinstalar e reinstalar os pacotes afetados. Consulte [Reinstalando e atualizando pacotes](../consume-packages/reinstalling-and-updating-packages.md)

    Se você encontrar o erro “Este projeto faz referência a pacotes do NuGet que estão ausentes neste computador” ou “Um ou mais pacotes do NuGet precisam ser restaurados, mas não foi possível fazer isso, pois o consentimento não foi concedido”, ative a restauração automática seguindo as instruções em [Habilitando e desabilitando a restauração do pacote](#enabling-and-disabling-package-restore). Confira também [Solucionar problemas de restauração de pacotes](Package-restore-troubleshooting.md).

- **CLI do NuGet**: use o comando [nuget restore](../tools/cli-ref-restore.md), que restaura os pacotes listados no arquivo de projeto ou no `packages.config`. Você também pode especificar um arquivo de solução.

- **MSBuild**: use o comando [msbuild /t:restore](../reference/msbuild-targets.md#restore-target), que restaura os pacotes listados no arquivo de projeto (apenas PackageReference). Disponível apenas no NuGet 4.x e posterior e no MSBuild 15.1 e posterior, que são incluídos no Visual Studio 2017. `nuget restore` e `dotnet restore` usam esse comando para projetos aplicável.

- **Visual Studio Team Services**: ao criar uma definição de compilação no Team Services, inclua a tarefa [Restaurar NuGet](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) ou [Restaurar .NET Core](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) na definição do antes de qualquer tarefa de compilação. Essa tarefa é incluída por padrão em diversos modelos de build.

- **Team Foundation Server**: o TFS 2013 e posterior restaura automaticamente os pacotes durante a compilação, desde que você esteja usando um modelo do Team Build para TFS 2013 ou posterior. Para obter uma versão anterior do TFS, você pode incluir uma etapa de compilação para invocar uma das opções de restauração de linha de comando descritas anteriormente. Opcionalmente, você pode migrar o modelo de compilação para o TFS 2013. Para saber mais, veja o [Passo a passo da restauração de pacotes com o Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="enabling-and-disabling-package-restore"></a>Habilitar e desabilitar a restauração do pacote

A restauração do pacote é habilitada primariamente por meio de **Ferramentas > Opções > Gerenciador de Pacotes do NuGet** no Visual Studio:

![Controlar comportamentos de restauração do pacote por meio de opções do Gerenciador de Pacotes do NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Permitir que o NuGet baixe pacotes ausentes**: controla todas as formas de restauração de pacote alterando a configuração `packageRestore/enabled` no arquivo `NuGet.Config`, conforme mostrado abaixo (`%AppData%\NuGet\NuGet.Config` no Windows e `~/.nuget/NuGet/NuGet.Config` no Mac/Linux). No Visual Studio, essa configuração permite que o comando **Restaurar Pacotes NuGet** no menu de contexto da solução funcione.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```

> [!Note]
>  A configuração `packageRestore/enabled` pode ser substituída globalmente definindo uma variável de ambiente chamada **EnableNuGetPackageRestore** com um valor de TRUE ou FALSE antes de abrir o Visual Studio ou iniciar um build.

- **Verificar automaticamente os pacotes ausentes durante o build no Visual Studio**: controla a restauração automática alterando a configuração `packageRestore/automatic` no arquivo `NuGet.Config`, conforme mostrado abaixo (`%AppData%\NuGet\NuGet.Config` no Windows e `~/.nuget/NuGet/NuGet.Config` no Mac/Linux). Quando essa opção for definida, executar um build no Visual Studio automaticamente restaurará todos os pacotes ausentes. A opção não afetará os builds executados na linha de comando usando o MSBuild.

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

Para referência, consulte o [Arquivo de configuração do NuGet – Seção packageRestore](../reference/nuget-config-file.md#packagerestore-section).

Em alguns casos, um desenvolvedor ou empresa podem optar por habilitar ou desabilitar a restauração de pacotes para todos os usuários em um computador. Para isso, adicione as mesmas configurações acima ao arquivo de configuração global do NuGet localizado em `%ProgramData%\NuGet\Config` (Windows, possivelmente em uma pasta `\{IDE}\{Version}\{SKU}\` específica do Visual Studio) ou `~/.local/share` (Mac/Linux). Usuários individuais poderão, então, habilitar seletivamente a restauração conforme necessário no nível do projeto. Confira [Configurando o comportamento do NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) para ver os detalhes sobre como o NuGet prioriza vários arquivos de configuração.

> [!Important]
> Se você editar as configurações de `packageRestore` diretamente em `nuget.config`, reinicie o Visual Studio para que a caixa de diálogo de opções mostre os valores atuais.

## <a name="constraining-package-versions-with-restore"></a>Restrições de versões de pacote com restauração

Ao restaurar pacotes por meio de qualquer método, o NuGet aceita quaisquer restrições especificadas no `packages.config` ou no arquivo de projeto:

- `packages.config`: especifique um intervalo de versão na propriedade `allowedVersion` da dependência. Confira [Reinstalando e atualizando pacotes](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Por exemplo:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Arquivo de projeto (PackageReference): especifique um intervalo de versão diretamente com o número de versão da dependência. Por exemplo:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Em todo os casos, use a notação descrita em [Controle de versão do pacote](../reference/package-versioning.md).

## <a name="forcing-restore-from-package-sources"></a>Forçar a restauração a partir de origens do pacote

Por padrão, as operações de restauração do NuGet usam pacotes das pastas *global-packages* e *http-cache*, que são descritas em [Como gerenciar as pastas de pacotes globais e de cache](managing-the-global-packages-and-cache-folders.md).

Para evitar o uso da pasta *global-packages*, siga um destes procedimentos:

- Limpe a pasta usando `nuget locals global-packages -clear` ou `dotnet nuget locals global-packages --clear`
- Altere temporariamente a localização da pasta *global-packages* antes da operação de restauração usando um dos seguintes métodos:
  - Defina a variável de ambiente NUGET_PACKAGES para uma pasta diferente.
  - Crie um arquivo `NuGet.Config` que defina `globalPackagesFolder` (se estiver usando PackageReference) ou `repositoryPath` (se estiver usando `packages.config`) para uma pasta diferente (consulte [definições de configuração](../reference/nuget-config-file.md#config-section)
  - Somente MSBuild: especifique uma pasta diferente com a propriedade `RestorePackagesPath`.

Para evitar o uso do cache para origens HTTP, siga um destes procedimentos:

- Use a opção `-NoCache` com `nuget restore` ou a opção `--no-cache` com `dotnet restore`. Essas opções não afetam as operações de restauração por meio da interface do usuário ou do Console do Gerenciador de Pacotes do Visual Studio.
- Limpe o cache usando `nuget locals http-cache -clear` ou `dotnet nuget locals http-cache --clear`.
- Defina temporariamente a variável de ambiente NUGET_HTTP_CACHE_PATH para uma pasta diferente.

## <a name="troubleshooting"></a>Solução de problemas

Confira [Solucionar problemas de restauração de pacotes](package-restore-troubleshooting.md).
