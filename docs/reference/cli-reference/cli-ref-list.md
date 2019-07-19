---
title: Comando de lista da CLI do NuGet
description: Referência para o comando de lista NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327733"
---
# <a name="list-command-nuget-cli"></a>comando List (NuGet CLI)

**Aplica-se a:** consumo de &bullet; pacote, **versões com suporte para publicação:** todos

Exibe uma lista de pacotes de uma determinada origem. Se nenhuma fonte for especificada, todas as fontes definidas no arquivo de configuração global `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config`ou, serão usadas. Se `NuGet.Config` não especificar nenhuma fonte `list` , o usará o feed padrão (NuGet.org).

## <a name="usage"></a>Uso

```cli
nuget list [search terms] [options]
```

onde os termos de pesquisa opcionais filtrarão a lista exibida. Os termos de pesquisa são aplicados aos nomes de pacotes, marcas e descrições de pacote da mesma forma que quando estão usando-os no nuget.org.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| AllVersions | Listar todas as versões de um pacote. Por padrão, somente a versão mais recente do pacote é exibida. |
| ConfigFile | O arquivo de configuração do NuGet a ser aplicado. Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.|
| ForceEnglishOutput | *(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês. |
| Help | Exibe informações de ajuda para o comando. |
| IncludeDelisted | *(3,2 +)* Exibir pacotes não listados. |
| NonInteractive | Suprime prompts de entrada ou confirmações do usuário. |
| Pré-lançamento | Inclui pacotes de pré-lançamento na lista. |
| Origem | Especifica uma lista de fontes de pacotes a serem pesquisadas. |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
