---
title: Restauração de pacote do NuGet
description: Uma visão geral de como o NuGet restaura os pacotes dos quais um projeto depende, incluindo como desabilitar a restauração e restringir as versões.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: e85d8cc3fd9492118bd8f34cfd05f20a9724c281
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842349"
---
# <a name="package-restore-options"></a>Opções de restauração de pacote

Para promover um ambiente de desenvolvimento mais limpo e reduzir o tamanho do repositório, a **Restauração de Pacote** do NuGet instala todas as dependências de um projeto listadas no arquivo de projeto ou em `packages.config`. Os comandos `dotnet build` e `dotnet run` do .NET Core 2.0 e posterior fazem uma restauração de pacote automática. O Visual Studio pode restaurar pacotes automaticamente quando ele cria um projeto, e você pode restaurar pacotes a qualquer momento por meio do Visual Studio, de `nuget restore`, de `dotnet restore` e do xbuild no Mono.

A Restauração de Pacote garante que todas as dependências de um projeto estejam disponíveis, sem a necessidade de armazená-las no controle do código-fonte. Para configurar o repositório do controle do código-fonte para excluir os binários do pacote, confira [Pacotes e controle do código-fonte](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Visão geral da Restauração de Pacote

Primeiro, a Restauração de Pacote instala as dependências diretas de um projeto, conforme necessário, e, em seguida, instala as dependências desses pacotes em todo o grafo de dependência.

Se um pacote ainda não estiver instalado, primeiro, o NuGet tentará recuperá-lo do [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). Se o pacote não estiver no cache, o NuGet tentará baixar o pacote de todas as origens habilitadas na lista em **Ferramentas** > **Opções** > **Gerenciador de Pacotes NuGet** > **Origens do Pacote** no Visual Studio. Durante a restauração, o NuGet ignora a ordem das origens do pacote e usa o pacote de qualquer origem que responder às solicitações primeiro. Para obter mais informações sobre como o NuGet se comporta, confira [Configurações comuns do NuGet](Configuring-NuGet-Behavior.md). 

> [!Note]
> O NuGet não indicará uma falha na restauração de um pacote enquanto todas as origens não forem verificadas. Nesse momento, o NuGet relatará uma falha somente para a última origem na lista. O erro indica que o pacote não estava presente em *nenhuma* das outras origens, mesmo que os erros não sejam mostrados para cada uma dessas fontes individualmente.

## <a name="restore-packages"></a>Restaurar pacotes

Dispare a Restauração de Pacote usando uma das seguintes maneiras:

- **Visual Studio**: No Visual Studio no Windows, use um dos métodos a seguir.

    - Restaurar os pacotes automaticamente. A Restauração de Pacote ocorre automaticamente quando você cria um projeto com base em um modelo ou compila um projeto, sujeito às opções em [Habilitar e desabilitar a restauração de pacote](#enable-and-disable-package-restore-visual-studio). No NuGet 4.0 e posterior, a restauração também ocorre automaticamente quando você faz alterações em um projeto do estilo SDK (normalmente um projeto do .NET Core ou .NET Standard).

    - Restaurar os pacotes manualmente. Para restaurar manualmente, clique com o botão direito na solução no **Gerenciador de Soluções** e selecione **Restaurar Pacotes NuGet**. Se um ou mais pacotes individuais ainda não estiverem instalados corretamente, o **Gerenciador de Soluções** mostrará um ícone de erro. Clique com o botão direito do mouse e selecione **Gerenciar Pacotes NuGet** e use o **Gerenciador de Pacotes** para desinstalar e reinstalar os pacotes afetados. Para obter mais informações, confira [Reinstalar e atualizar pacotes](../consume-packages/reinstalling-and-updating-packages.md)

    Se você receber o erro "Este projeto referencia pacotes NuGet que estão ausentes deste computador" ou "Um ou mais pacotes NuGet precisam ser restaurados, mas não foi possível fazer isso, pois o consentimento não foi dado", [habilite a restauração automática](#enable-and-disable-package-restore-visual-studio). Além disso, confira [Migrar para restauração automática de pacote](#migrate-to-automatic-package-restore-visual-studio) e [Solução de problemas de restauração de pacote](Package-restore-troubleshooting.md).

- **CLI do dotnet**: Na linha de comando, alterne para a pasta que contém o projeto e use o comando [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) para restaurar os pacotes listados no arquivo de projeto com [PackageReference](../consume-packages/package-references-in-project-files.md). Com o .NET Core 2.0 e posterior, a restauração ocorre automaticamente com os comandos `dotnet build` e `dotnet run`.  

- **CLI do nuget.exe**: Na linha de comando, alterne para a pasta que contém o projeto e use o comando [nuget restore](../tools/cli-ref-restore.md) para restaurar os pacotes listados em um arquivo de projeto ou solução ou no `packages.config`. 

- **MSBuild**: Use o comando [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) para restaurar os pacotes listados no arquivo de projeto com PackageReference. Esse comando só está disponível no NuGet 4.x e posterior e no MSBuild 15.1 e posterior, que estão incluídos no Visual Studio 2017 e em versões superiores. `nuget restore` e `dotnet restore` usam esse comando para projetos aplicáveis.

- **Azure Pipelines**: Ao criar uma definição de build no Azure Pipelines, inclua a tarefa [restore](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) do NuGet ou a tarefa [restore](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) do .NET Core na definição antes de qualquer tarefa de build. Alguns modelos de build incluem a tarefa de restauração por padrão.

- **Azure DevOps Server**: O Azure DevOps Server e o TFS 2013 e posterior restaurarão pacotes automaticamente durante o build se você estiver usando um modelo do Team Build do TFS 2013 ou posterior. Para versões anteriores do TFS, você pode incluir uma etapa de build para executar uma opção de restauração de linha de comando ou, opcionalmente, migrar o modelo de build para uma versão posterior. Para obter mais informações, confira [Configurar a restauração de pacote com o Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="enable-and-disable-package-restore-visual-studio"></a>Habilitar e desabilitar a restauração de pacote (Visual Studio)

No Visual Studio, você controla a Restauração de Pacote principalmente por meio de **Ferramentas** > **Opções** > **Gerenciador de Pacotes NuGet**:

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

Em todo os casos, use a notação descrita em [Controle de versão do pacote](../reference/package-versioning.md).

## <a name="force-restore-from-package-sources"></a>Forçar a restauração em origens do pacote

Por padrão, as operações de restauração do NuGet usam pacotes das pastas *global-packages* e *http-cache*, que são descritas em [Gerenciar os pacotes globais e as pastas de cache](managing-the-global-packages-and-cache-folders.md).

Para evitar o uso da pasta *global-packages*, siga um destes procedimentos:

- Limpe a pasta usando `nuget locals global-packages -clear` ou `dotnet nuget locals global-packages --clear`.
- Altere temporariamente a localização da pasta *global-packages* antes da operação de restauração usando um dos seguintes métodos:
  - Defina a variável de ambiente NUGET_PACKAGES para uma pasta diferente.
  - Crie um arquivo `NuGet.Config` que define `globalPackagesFolder` (se você estiver usando PackageReference) ou `repositoryPath` (se você estiver usando `packages.config`) em outra pasta. Para obter mais informações, confira [Definições de configuração](../reference/nuget-config-file.md#config-section).
  - Somente no MSBuild: Especifique outra pasta com a propriedade `RestorePackagesPath`.

Para evitar o uso do cache para origens HTTP, siga um destes procedimentos:

- Use a opção `-NoCache` com `nuget restore` ou a opção `--no-cache` com `dotnet restore`. Essas opções não afetam as operações de restauração por meio do console ou do Gerenciador de Pacotes do Visual Studio.
- Limpe o cache usando `nuget locals http-cache -clear` ou `dotnet nuget locals http-cache --clear`.
- Defina temporariamente a variável de ambiente NUGET_HTTP_CACHE_PATH como outra pasta.

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>Migrar para restauração automática de pacote (Visual Studio)

Para o NuGet 2.6 e anterior, havia suporte para uma restauração de pacote integrada ao MSBuild, mas isso não é mais verdade. Normalmente, ele era habilitado clicando com o botão direito do mouse em uma solução no Visual Studio e selecionando **Habilitar restauração de pacote do NuGet**. Se o seu projeto usa a restauração de pacote integrada do MSBuild preterida, migre para a restauração automática de pacote.

Os projetos que usam a restauração de pacote integrada do MSBuild normalmente contêm uma pasta *.nuget* com três arquivos: *NuGet.config*, *nuget.exe* e *NuGet.targets*. A presença de um *NuGet.targets* determina se o NuGet continuará a usar a abordagem integrada do MSBuild, de modo que esse arquivo deve ser removido durante a migração.

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
