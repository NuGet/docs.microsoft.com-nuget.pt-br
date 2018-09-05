---
title: Comando de lista de CLI do NuGet
description: Referência do comando de lista nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549795"
---
# <a name="list-command-nuget-cli"></a>comando List (CLI do NuGet)

**Aplica-se a:** consumo de pacote, publicando &bullet; **versões com suporte:** todos os

Exibe uma lista de pacotes de uma origem específica. Se nenhuma fonte forem especificado, todas as fontes definidas no arquivo de configuração global, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config`, são usados. Se `NuGet.Config` não especifica nenhuma fonte, em seguida, `list` usa o feed padrão (nuget.org).

## <a name="usage"></a>Uso

```cli
nuget list [search terms] [options]
```

em que os termos de pesquisa opcional filtrará a lista exibida. Termos de pesquisa são aplicados aos nomes dos pacotes, marcas e descrições de pacote como elas são quando usá-los em nuget.org.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| AllVersions | Liste todas as versões de um pacote. Por padrão, somente a versão mais recente do pacote é exibida. |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| ForceEnglishOutput | *(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| IncludeDelisted | *(3.2 e superior)*  Exibir os pacotes não listados. |
| NonInteractive | Suprime a solicitações de entrada do usuário ou confirmações. |
| Versão de pré-lançamento | Inclui pacotes pré-lançados na lista. |
| Origem | Especifica uma lista de origens de pacotes para pesquisar. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
