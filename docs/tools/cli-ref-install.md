---
title: Comando de instalação da CLI do NuGet
description: Referência para o comando de instalação nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 8088c6dcb7d453650950c219e1cc4dd047a64417
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425988"
---
# <a name="install-command-nuget-cli"></a>Commando install (NuGet CLI)

**Aplica-se a:** consumo do pacote &bullet; **versões com suporte:** todos os

Baixa e instala um pacote em um projeto, padronizando para a pasta atual, usando fontes de pacote especificado.

> [!Tip]
> Para baixar o pacote diretamente fora do contexto de um projeto, visite a página do pacote no [nuget.org](https://www.nuget.org) e selecione o **baixar** link.

Se nenhuma fonte forem especificado, aqueles listados no arquivo de configuração global, `%appdata%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), são usados. Ver [configurações de NuGet comuns](../consume-packages/configuring-nuget-behavior.md) para obter mais detalhes.

Se nenhum pacote específico for especificado, `install` instala todos os pacotes listados no projeto do `packages.config` arquivo, tornando-a semelhante ao [ `restore` ](cli-ref-restore.md).

O `install` comando não modifica um arquivo de projeto ou `packages.config`; dessa forma é semelhante ao `restore` em que ele apenas adiciona pacotes para o disco, mas não altera as dependências do projeto.

Para adicionar uma dependência, adicionar um pacote por meio do Gerenciador de pacotes da interface do usuário ou o Console no Visual Studio, ou modifique `packages.config` e, em seguida, execute o `install` ou `restore`.

## <a name="usage"></a>Uso

```cli
nuget install <packageID | configFilePath> [options]
```

em que `<packageID>` nomeia o pacote de instalação (usando a versão mais recente), ou `<configFilePath>` identifica o `packages.config` arquivo que lista os pacotes sejam instalados. Você pode indicar uma versão específica com o `-Version` opção.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| DependencyVersion | *(4.4 ou superior)*  a versão dos pacotes de dependência a ser usado, que pode ser um dos seguintes:<br/><ul><li>*Mais baixo* (padrão): a versão mais antiga</li><li>*HighestPatch*: a versão com o patch mais baixa principal, secundária menor, mais alto</li><li>*HighestMinor*: a versão com menor principais, o patch mais alto de pequena, mais alto</li><li>*Mais alto*: a versão mais recente</li></ul> |
| DisableParallelProcessing | Desativa a instalação de vários pacotes em paralelo. |
| ExcludeVersion | Instala o pacote para uma pasta chamada com apenas o nome do pacote e não o número de versão. |
| FallbackSource | *(3.2 e superior)*  Uma lista de origens de pacote a ser usado como fallbacks no caso do pacote não for encontrado no primário ou a fonte padrão. |
| ForceEnglishOutput | *(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Framework | *(4.4 ou superior)*  Usada para selecionar as dependências de estrutura de destino. O padrão é 'Any' se não for especificado. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NoCache | Impede que o NuGet usando pacotes armazenados em cache. Ver [gerenciar as pastas de cache e de pacotes globais](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Suprime a solicitações de entrada do usuário ou confirmações. |
| OutputDirectory | Especifica a pasta na qual os pacotes são instalados. Se nenhuma pasta for especificada, a pasta atual será usada. |
| PackageSaveMode | Especifica os tipos de arquivos a serem salvos após a instalação do pacote: um dos `nuspec`, `nupkg`, ou `nuspec;nupkg`. |
| Versão de pré-lançamento | Permite que os pacotes de pré-lançamento a serem instalados. Este sinalizador não é necessário ao restaurar os pacotes com `packages.config`. |
| RequireConsent | Verifica se a restauração de pacotes está habilitado antes de baixar e instalar os pacotes. Para obter detalhes, consulte [restauração de pacote](../consume-packages/package-restore.md). |
| SolutionDirectory | Especifica a pasta raiz da solução para o qual restaurar os pacotes. |
| Origem | Especifica a lista de origens de pacote (como URLs) para usar. Se omitido, o comando usa as fontes fornecidas em arquivos de configuração, consulte [configurações de NuGet comuns](../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |
| Versão | Especifica a versão do pacote a instalar. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
