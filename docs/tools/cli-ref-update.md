---
title: Comando de atualização de CLI do NuGet
description: Referência do comando de atualização nuget.exe
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a242d02a54fd86899cbe274ab63538b53307c1bb
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425913"
---
# <a name="update-command-nuget-cli"></a>Commando update (NuGet CLI)

**Aplica-se a:** consumo do pacote &bullet; **versões com suporte:** todos os

Atualiza todos os pacotes em um projeto (usando `packages.config`) para suas versões mais recentes disponíveis. É recomendável executar ['restore'](cli-ref-restore.md) antes de executar o `update`. (Para atualizar um pacote individual, use [ `nuget install` ](cli-ref-install.md) sem especificar um número de versão, em que o NuGet caso instala a versão mais recente.)

Observação: `update` não funciona com a CLI executando em Mono (Mac OSX ou Linux) ou ao usar o formato PackageReference.

O `update` comando também atualiza as referências de assembly no arquivo de projeto, desde aqueles faz referência já existir. Se um pacote atualizado tiver um assembly adicionado, uma nova referência será *não* adicionado. Novas dependências do pacote também não têm suas referências de assembly adicionadas. Para incluir essas operações como parte de uma atualização, atualize o pacote no Visual Studio usando a UI do Gerenciador de pacotes ou o Console do Gerenciador de pacotes.

Esse comando também pode ser usado para atualizar nuget.exe em si usando o *-self* sinalizador.

## <a name="usage"></a>Uso

```cli
nuget update <configPath> [options]
```

em que `<configPath>` identifica um uma `packages.config` ou arquivo de solução que lista as dependências do projeto.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| FileConflictAction | Especifica a ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes, referenciados pelo projeto. Os valores são *substituir, ignorar, nenhum*. |
| ForceEnglishOutput | *(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Help | Exibe informações de ajuda para o comando. |
| Id | Especifica uma lista de IDs de atualização de pacote. |
| MSBuildPath | *(4.0 e posteriores)*  Especifica o caminho do MSBuild a usar com o comando, tendo precedência sobre `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 e superior)*  Especifica a versão do MSBuild a ser usado com este comando. Valores com suporte são 4, 12, 14, 15.1, 15.3, 15.4, 15,5, 15.6, 15.7, 15,8, 15,9. Por padrão que o MSBuild em seu caminho é escolhido, caso contrário, o padrão é a versão mais recente instalada do MSBuild. |
| NonInteractive | Suprime a solicitações de entrada do usuário ou confirmações. |
| Versão de pré-lançamento | Permite a atualização para versões de pré-lançamento. Este sinalizador não é necessário ao atualizar os pacotes de pré-lançamento que já estão instalados. |
| RepositoryPath | Especifica a pasta local onde os pacotes são instalados. |
| Safe | Especifica que atualiza apenas com a versão mais recente disponível dentro da mesma versão principal e secundária como o pacote instalado será instalado. |
| Self | Nuget.exe atualizações para a versão mais recente; todos os outros argumentos são ignorados. |
| Origem | Especifica a lista de origens de pacote (como URLs) para usar as atualizações. Se omitido, o comando usa as fontes fornecidas em arquivos de configuração, consulte [configurações de NuGet comuns](../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |
| Versão | Quando usado com uma ID de pacote, especifica a versão do pacote a atualizar. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
