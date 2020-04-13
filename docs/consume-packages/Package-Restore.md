---
title: Restauração de pacote do NuGet
description: Uma visão geral de como o NuGet restaura os pacotes dos quais um projeto depende, incluindo como desabilitar a restauração e restringir as versões.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: c1f1957c58839ac763238938b476eb0882c56a59
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428740"
---
# <a name="restore-packages-using-package-restore"></a>Restaurar pacotes usando a Restauração de Pacote

Para promover um ambiente de desenvolvimento mais limpo e reduzir o tamanho do repositório, a **Restauração de Pacote** do NuGet instala todas as dependências de um projeto listadas no arquivo de projeto ou em `packages.config`. Os comandos `dotnet build` e `dotnet run` do .NET Core 2.0 e posterior fazem uma restauração de pacote automática. O Visual Studio pode restaurar pacotes automaticamente quando ele cria um projeto, e você pode restaurar pacotes a qualquer momento por meio do Visual Studio, de `nuget restore`, de `dotnet restore` e do xbuild no Mono.

A Restauração de Pacote garante que todas as dependências de um projeto estejam disponíveis, sem a necessidade de armazená-las no controle do código-fonte. Para configurar o repositório do controle do código-fonte para excluir os binários do pacote, confira [Pacotes e controle do código-fonte](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Visão geral da Restauração de Pacote

Primeiro, a Restauração de Pacote instala as dependências diretas de um projeto, conforme necessário, e, em seguida, instala as dependências desses pacotes em todo o grafo de dependência.

Se um pacote ainda não estiver instalado, primeiro, o NuGet tentará recuperá-lo do [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). Se o pacote não estiver no cache, o NuGet tentará baixar o pacote de todas as fontes habilitadas na lista no **Tools** > **Options** > **NuGet Package Manager** > **Package Sources** no Visual Studio. Durante a restauração, o NuGet ignora a ordem das origens do pacote e usa o pacote de qualquer origem que responder às solicitações primeiro. Para obter mais informações sobre como o NuGet se comporta, confira [Configurações comuns do NuGet](Configuring-NuGet-Behavior.md). 

> [!Note]
> O NuGet não indicará uma falha na restauração de um pacote enquanto todas as origens não forem verificadas. Nesse momento, o NuGet relatará uma falha somente para a última origem na lista. O erro indica que o pacote não estava presente em *nenhuma* das outras origens, mesmo que os erros não sejam mostrados para cada uma dessas fontes individualmente.

## <a name="restore-packages"></a>Restaurar pacotes

A Restauração de Pacote tenta instalar todas as dependências de pacotes no estado correto correspondente às referências de pacote do arquivo de projeto (*.csproj*) ou do arquivo *packages.config*. No Visual Studio, as referências aparecem no Gerenciador de Soluções em **Dependências \ NuGet ** ou no nó **Referências**.

1. Se as referências de pacote no arquivo de projeto estiverem corretas, use sua ferramenta preferida para restaurar os pacotes.

   - [Visual Studio](#restore-using-visual-studio) ([restauração automática](#restore-packages-automatically-using-visual-studio) ou [restauração manual](#restore-packages-manually-using-visual-studio))
   - [CLI do dotnet](#restore-using-the-dotnet-cli)
   - [CLI do nuget.exe](#restore-using-the-nugetexe-cli)
   - [MSBuild](#restore-using-msbuild)
   - [Azure Pipelines](#restore-using-azure-pipelines)
   - [Servidor Azure DevOps](#restore-using-azure-devops-server)

   Se as referências de pacote no arquivo de projeto (*.csproj*) ou no arquivo *packages.config* estiverem incorretas (não corresponderem ao estado desejado após a Restauração de Pacote), instale ou atualize os pacotes.

   Para projetos que usam PackageReference, após uma restauração bem-sucedida, o pacote deve estar presente na pasta *global-packages* e o arquivo `obj/project.assets.json` é recriado. Para projetos que usam `packages.config`, o pacote deve aparecer na pasta `packages` do projeto. Nesse momento, o projeto deverá ser compilado com êxito. 

2. Depois de executar a Restauração de Pacote, se ainda houver pacotes ausentes ou erros relacionados a pacotes (como ícones de erro no Gerenciador de Soluções do Visual Studio), poderá ser necessário seguir as instruções descritas em [Solução de problemas de restauração de pacote](package-restore-troubleshooting.md) ou, como alternativa, [Reinstalar e atualizar os pacotes](../consume-packages/reinstalling-and-updating-packages.md).

   No Visual Studio, o Console do Gerenciador de Pacotes fornece várias opções flexíveis para reinstalar os pacotes. Confira [Usar Update-Package](reinstalling-and-updating-packages.md#using-update-package).

## <a name="restore-using-visual-studio"></a>Restaurar usando o Visual Studio

No Visual Studio no Windows, siga um destes procedimentos:

- Restaurar pacotes automaticamente ou

- Restaurar pacotes manualmente

### <a name="restore-packages-automatically-using-visual-studio"></a>Restaurar pacotes automaticamente usando o Visual Studio

A Restauração de Pacote ocorre automaticamente quando você cria um projeto com base em um modelo ou compila um projeto, sujeito às opções em [Habilitar e desabilitar a restauração de pacote](#enable-and-disable-package-restore-in-visual-studio). No NuGet 4.0 e posterior, a restauração também ocorre automaticamente quando você faz alterações em um projeto do estilo SDK (normalmente um projeto do .NET Core ou .NET Standard).

1. Habilite a restauração automática do pacote escolhendo O Gerenciador**de Pacotes** >  **NuGet** > e, em seguida, selecionando **verificar automaticamente se faltam pacotes durante a compilação no Visual Studio** em **Restauração de pacotes**.**NuGet Package Manager**

   Para projetos com estilo diferente do SDK, selecione primeiro **Permitir que o NuGet baixe os pacotes ausentes** para habilitar a opção de restauração automática.

1. Compile o projeto.

   Se um ou mais pacotes individuais ainda não estiverem instalados corretamente, o **Gerenciador de Soluções** mostrará um ícone de erro. Clique com o botão direito do mouse e selecione **Gerenciar Pacotes NuGet** e use o **Gerenciador de Pacotes** para desinstalar e reinstalar os pacotes afetados. Para obter mais informações, confira [Reinstalar e atualizar pacotes](../consume-packages/reinstalling-and-updating-packages.md)

   Se você receber o erro "Este projeto referencia pacotes NuGet que estão ausentes deste computador" ou "Um ou mais pacotes NuGet precisam ser restaurados, mas não foi possível fazer isso, pois o consentimento não foi dado", [habilite a restauração automática](#enable-and-disable-package-restore-in-visual-studio). Para projetos mais antigos, confira também [Migrar para a restauração de pacote automática](#migrate-to-automatic-package-restore-visual-studio). Consulte também a [solução de problemas do Package Restore](Package-restore-troubleshooting.md).

### <a name="restore-packages-manually-using-visual-studio"></a>Restaurar pacotes manualmente usando o Visual Studio

1. Habilite a restauração do pacote escolhendo**opções de** >  **ferramentas** > **NuGet Package Manager**. Nas opções de **Restauração de Pacote**, selecione **Permitir que o NuGet baixe os pacotes ausentes**.

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse na solução e selecione **Restaurar Pacotes NuGet**.

   Se um ou mais pacotes individuais ainda não estiverem instalados corretamente, o **Gerenciador de Soluções** mostrará um ícone de erro. Clique com o botão direito do mouse e selecione **Gerenciar Pacotes NuGet** e use o **Gerenciador de Pacotes** para desinstalar e reinstalar os pacotes afetados. Para obter mais informações, confira [Reinstalar e atualizar pacotes](../consume-packages/reinstalling-and-updating-packages.md)

   Se você receber o erro "Este projeto referencia pacotes NuGet que estão ausentes deste computador" ou "Um ou mais pacotes NuGet precisam ser restaurados, mas não foi possível fazer isso, pois o consentimento não foi dado", [habilite a restauração automática](#enable-and-disable-package-restore-in-visual-studio). Para projetos mais antigos, confira também [Migrar para a restauração de pacote automática](#migrate-to-automatic-package-restore-visual-studio). Consulte também a [solução de problemas do Package Restore](Package-restore-troubleshooting.md).

### <a name="enable-and-disable-package-restore-in-visual-studio"></a>Habilitar e desabilitar a restauração de pacote no Visual Studio

No Visual Studio, você controla a restauração de pacotes principalmente através do **Tools** > **Options** > **NuGet Package Manager**:

![Controlar a Restauração de Pacote por meio das opções do Gerenciador de Pacotes NuGet](media/Restore-01-AutoRestoreOptions.png)

- A configuração **Permitir que o NuGet baixe os pacotes ausentes** controla todas as formas de restauração de pacote alterando a configuração `packageRestore/enabled` na [seção packageRestore](../reference/nuget-config-file.md#packagerestore-section) do arquivo `NuGet.Config`, em `%AppData%\NuGet\` no Windows ou `~/.nuget/NuGet/` no Mac/Linux. Essa configuração também habilita o comando **Restaurar Pacotes NuGet** no menu de contexto da solução no Visual Studio.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    
  > [!Note]
  > Para substituir globalmente a configuração `packageRestore/enabled`, defina a variável de ambiente **EnableNuGetPackageRestore** com um valor igual a True ou False antes de iniciar o Visual Studio ou um build.

- A configuração **Verificar automaticamente os pacotes ausentes durante o build no Visual Studio** controla a restauração automática alterando a configuração `packageRestore/automatic` na [seção packageRestore](../reference/nuget-config-file.md#packagerestore-section) do arquivo `NuGet.Config`. Quando essa opção é definida como True, a execução de um build no Visual Studio restaura automaticamente todos os pacotes ausentes. Essa configuração não afeta os builds executados na linha de comando do MSBuild.

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

Para habilitar ou desabilitar a Restauração de Pacote para todos os usuários em um computador, um desenvolvedor ou uma empresa pode adicionar as definições de configuração ao arquivo `nuget.config` global. O `nuget.config` global está no Windows em `%ProgramData%\NuGet\Config`, às vezes, em uma pasta `\{IDE}\{Version}\{SKU}\` específica do Visual Studio ou no Mac/Linux em `~/.local/share`. Usuários individuais poderão, então, habilitar seletivamente a restauração conforme necessário no nível do projeto. Para obter mais detalhes sobre como o NuGet prioriza vários arquivos de configuração, confira [Configurações comuns do NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> Se você editar as configurações de `packageRestore` diretamente em `nuget.config`, reinicie o Visual Studio para que a caixa de diálogo **Opções** mostre os valores atuais.

### <a name="choose-default-package-management-format"></a>Escolha o formato padrão de gerenciamento de pacotes

![Controle o formato padrão de gerenciamento de pacotes embora as opções do NuGet Package Manager](media/Restore-02-PackageFormatOptions.png)

NuGet tem dois formatos nos quais um [`PackageReference`](package-references-in-project-files.md) [`packages.config`](../reference/packages-config.md)projeto pode usar pacotes: e . O formato padrão pode ser selecionado a partir da lista de paradas no título **'Gerenciamento de** pacotes'. Uma opção a ser solicitada quando o primeiro pacote é instalado em um projeto também está disponível.

> [!Note]
> Se um projeto não suportar ambos os formatos de gerenciamento de pacotes, o formato de gerenciamento de pacotes usado será o que é compatível com o projeto e, portanto, pode não ser o padrão definido nas opções. Além disso, o NuGet não solicitará a seleção na primeira instalação do pacote, mesmo que a opção esteja selecionada na janela de opções.
>
> Se o Console do Gerenciador de Pacotes for usado para instalar o primeiro pacote em um projeto, o NuGet não solicitará a seleção do formato, mesmo que a opção esteja selecionada na janela de opções.

## <a name="restore-using-the-dotnet-cli"></a>Restaurar usando a CLI do dotnet

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> Para adicionar uma referência de pacote ausente ao arquivo de projeto, use [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x), que também executa o comando `restore`.

## <a name="restore-using-the-nugetexe-cli"></a>Restaurar usando a CLI nuget.exe

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> O `restore`comando não modifica um arquivo de projeto ou *pacotes.config*. Para adicionar uma dependência, adicione um pacote através da IA do Gerenciador de Pacotes ou `install` `restore`console no Visual Studio, ou modifique *pacotes.config* e execute ou .

## <a name="restore-using-msbuild"></a>Restaurar usando o MSBuild

Para restaurar os pacotes listados no arquivo de projeto com PackageReference, use o comando [msbuild -t:restore](../reference/msbuild-targets.md#restore-target). Esse comando só está disponível no NuGet 4.x e posterior e no MSBuild 15.1 e posterior, que estão incluídos no Visual Studio 2017 e em versões superiores. `nuget restore` e `dotnet restore` usam esse comando para projetos aplicáveis.

1. Abra um prompt de comando do Desenvolvedor (na caixa **Pesquisar**, digite **Prompt de Comando do Desenvolvedor**).

   Você normalmente deseja iniciar o Prompt de Comando do Desenvolvedor para Visual Studio usando o menu **Iniciar**, pois ele estará configurado com todos os caminhos necessários para o MSBuild.

2. Alterne para a pasta que contém o arquivo de projeto e digite o comando a seguir.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

3. Digite o comando a seguir para recompilar o projeto.

   ```cmd
   msbuild
   ```

   Verifique se a saída de MSBuild indica que a compilação foi concluída com êxito.

## <a name="restore-using-azure-pipelines"></a>Restaurar usando o Azure Pipelines

Ao criar uma definição de build no Azure Pipelines, inclua a tarefa [restore](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) do NuGet ou a tarefa [restore](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) do .NET Core na definição antes de qualquer tarefa de build. Alguns modelos de build incluem a tarefa de restauração por padrão.

## <a name="restore-using-azure-devops-server"></a>Restaurar usando o Azure DevOps Server

O Azure DevOps Server e o TFS 2013 e posterior restaurarão pacotes automaticamente durante o build se você estiver usando um modelo do Team Build do TFS 2013 ou posterior. Para versões anteriores do TFS, você pode incluir uma etapa de build para executar uma opção de restauração de linha de comando ou, opcionalmente, migrar o modelo de build para uma versão posterior. Para obter mais informações, confira [Configurar a restauração de pacote com o Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="constrain-package-versions-with-restore"></a>Restringir as versões do pacote com a restauração

Quando o NuGet restaura pacotes por meio de qualquer método, ele respeita todas as restrições especificadas em `packages.config` ou no arquivo de projeto:

- Em `packages.config`, você pode especificar um intervalo de versão na propriedade `allowedVersion` da dependência. Confira [Restringir as versões de atualização](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) para obter mais informações. Por exemplo:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Em um arquivo de projeto, você pode usar PackageReference para especificar o intervalo de uma dependência diretamente. Por exemplo:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Em todo os casos, use a notação descrita em [Controle de versão do pacote](../concepts/package-versioning.md).

## <a name="force-restore-from-package-sources"></a>Forçar a restauração em origens do pacote

Por padrão, as operações de restauração do NuGet usam pacotes das pastas *global-packages* e *http-cache*, que são descritas em [Gerenciar os pacotes globais e as pastas de cache](managing-the-global-packages-and-cache-folders.md).

Para evitar o uso da pasta *global-packages*, siga um destes procedimentos:

- Limpe a pasta usando `nuget locals global-packages -clear` ou `dotnet nuget locals global-packages --clear`.
- Altere temporariamente a localização da pasta *de pacotes globais* antes da operação de restauração, usando um dos seguintes métodos:
  - Defina a variável de ambiente NUGET_PACKAGES para uma pasta diferente.
  - Crie um arquivo `NuGet.Config` que define `globalPackagesFolder` (se você estiver usando PackageReference) ou `repositoryPath` (se você estiver usando `packages.config`) em outra pasta. Para obter mais informações, confira [Definições de configuração](../reference/nuget-config-file.md#config-section).
  - Somente MSBuild: Especifique `RestorePackagesPath` uma pasta diferente com a propriedade.

Para evitar o uso do cache para origens HTTP, siga um destes procedimentos:

- Use a opção `-NoCache` com `nuget restore` ou a opção `--no-cache` com `dotnet restore`. Essas opções não afetam as operações de restauração por meio do console ou do Gerenciador de Pacotes do Visual Studio.
- Limpe o cache usando `nuget locals http-cache -clear` ou `dotnet nuget locals http-cache --clear`.
- Defina temporariamente a variável de ambiente NUGET_HTTP_CACHE_PATH como outra pasta.

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>Migrar para restauração automática de pacote (Visual Studio)

Para o NuGet 2.6 e anterior, havia suporte para uma restauração de pacote integrada ao MSBuild, mas isso não é mais verdade. Normalmente, ele era habilitado clicando com o botão direito do mouse em uma solução no Visual Studio e selecionando **Habilitar restauração de pacote do NuGet**. Se o seu projeto usa a restauração de pacote integrada do MSBuild preterida, migre para a restauração automática de pacote.

Projetos que usam restauração de pacote supérdia integrada do MSBuild normalmente contêm uma pasta *.nuget* com três arquivos: *NuGet.config*, *nuget.exe*e *NuGet.targets*. A presença de um *NuGet.targets* determina se o NuGet continuará a usar a abordagem integrada do MSBuild, de modo que esse arquivo deve ser removido durante a migração.

Para migrar para restauração automática de pacote:

1. Feche o Visual Studio.
2. Exclua *.nuget/nuget.exe* e *.nuget/NuGet.targets*.
3. Para cada arquivo de projeto, remova o elemento `<RestorePackages>` e qualquer referência a *NuGet.targets*.

Para testar a restauração automática de pacote:

1. Remova a pasta *packages* da solução.
2. Abra a solução no Visual Studio e inicie uma compilação.

   A restauração automática de pacote deve baixar e instalar cada pacote de dependência, sem adicioná-los ao controle do código-fonte.

## <a name="troubleshooting"></a>Solução de problemas

Confira [Solução de problemas de erros de restauração de pacote](package-restore-troubleshooting.md).
