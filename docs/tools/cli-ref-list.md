---
title: Comando de lista de CLI do NuGet
description: Referência para o comando de lista de nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b0f144d8abbba7388fe39cd113e4eeddccbca2c6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818432"
---
# <a name="list-command-nuget-cli"></a>comando Listar (NuGet CLI)

**Aplica-se a:** consumo de pacote, a publicação &bullet; **versões com suporte:** todos

Exibe uma lista de pacotes de uma origem específica. Se nenhuma fonte for especificada, todas as fontes definidas no arquivo de configuração global, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config`, são usados. Se `NuGet.Config` não especifica nenhuma fonte, em seguida, `list` usa o feed padrão (nuget.org).

## <a name="usage"></a>Uso

```cli
nuget list [search terms] [options]
```

onde os termos de pesquisa opcional filtra a lista exibida. Termos de pesquisa são aplicados para os nomes dos pacotes, marcas e descrições de pacote como elas são quando usá-los em nuget.org.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| Todasas versões | Lista todas as versões de um pacote. Por padrão, somente a versão mais recente do pacote é exibida. |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| IncludeDelisted | *(3.2 +)*  Exibir pacotes não listados. |
| NonInteractive | Suprime avisos para a entrada do usuário ou confirmações. |
| Versão de pré-lançamento | Inclui pacotes pré-lançados na lista. |
| Origem | Especifica uma lista de fontes de pacotes para pesquisar. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```