---
title: Comando de atualização da CLI do NuGet
description: Referência para o comando de atualização NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327503"
---
# <a name="update-command-nuget-cli"></a>Commando update (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** do consumo do pacote: todas

Atualiza todos os pacotes de um projeto (usando `packages.config`) para as últimas versões disponíveis. É recomendável executar [' Restore '](cli-ref-restore.md) antes de executar `update`o. (Para atualizar um pacote individual, use [`nuget install`](cli-ref-install.md) sem especificar um número de versão, caso em que o NuGet instala a versão mais recente.)

Observação: `update` o não funciona com a CLI em execução em mono (Mac OSX ou Linux) ou ao usar o formato PackageReference.

O `update` comando também atualiza referências de assembly no arquivo de projeto, desde que essas referências já existam. Se um pacote atualizado tiver um assembly adicionado, uma nova referência *não* será adicionada. Novas dependências de pacote também não têm suas referências de assembly adicionadas. Para incluir essas operações como parte de uma atualização, atualize o pacote no Visual Studio usando a interface do usuário do Gerenciador de pacotes ou o console do Gerenciador de pacotes.

Esse comando também pode ser usado para atualizar o NuGet. exe usando o sinalizador *-Self* .

## <a name="usage"></a>Uso

```cli
nuget update <configPath> [options]
```

onde `<configPath>` o identifica um `packages.config` arquivo de solução ou que lista as dependências do projeto.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet a ser aplicado. Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.|
| FileConflictAction | Especifica a ação a ser tomada quando solicitado a substituir ou ignorar os arquivos existentes referenciados pelo projeto. Os valores são *substituir, ignorar, nenhum*. |
| ForceEnglishOutput | *(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês. |
| Help | Exibe informações de ajuda para o comando. |
| Id | Especifica uma lista de IDs de pacote a serem atualizadas. |
| MSBuildPath | *(4.0 +)* Especifica o caminho do MSBuild a ser usado com o comando, tendo precedência sobre `-MSBuildVersion`. |
| MSBuildVersion | *(3,2 +)* Especifica a versão do MSBuild a ser usada com este comando. Os valores com suporte são 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Por padrão, o MSBuild em seu caminho é escolhido; caso contrário, ele usa a versão mais recente instalada do MSBuild. |
| NonInteractive | Suprime prompts de entrada ou confirmações do usuário. |
| Pré-lançamento | Permite atualizar para versões de pré-lançamento. Esse sinalizador não é necessário ao atualizar pacotes de pré-lançamento que já estão instalados. |
| RepositoryPath | Especifica a pasta local onde os pacotes são instalados. |
| Removidos | Especifica que somente as atualizações com a versão mais recente disponível na mesma versão principal e secundária do pacote instalado serão instaladas. |
| Auto-restauração | Atualiza o NuGet. exe para a versão mais recente; todos os outros argumentos são ignorados. |
| Origem | Especifica a lista de origens do pacote (como URLs) a serem usadas para as atualizações. Se omitido, o comando usará as fontes fornecidas em arquivos de configuração, consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |
| Versão | Quando usado com uma ID de pacote, especifica a versão do pacote a ser atualizada. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
