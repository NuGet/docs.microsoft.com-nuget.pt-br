---
title: Comando de lista da CLI do NuGet
description: Referência para o comando de lista NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813332"
---
# <a name="list-command-nuget-cli"></a>comando List (NuGet CLI)

**Aplica-se a:** consumo de pacote, publicação &bullet; **versões com suporte:** todos

Exibe uma lista de pacotes de uma determinada origem. Se nenhuma fonte for especificada, todas as fontes definidas no arquivo de configuração global, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config`, serão usadas. Se `NuGet.Config` não especificar nenhuma fonte, `list` usará o feed padrão (nuget.org).

## <a name="usage"></a>Medição de

```cli
nuget list [search terms] [options]
```

onde os termos de pesquisa opcionais filtrarão a lista exibida. Os termos de pesquisa são aplicados aos nomes de pacotes, marcas e descrições de pacote da mesma forma que quando estão usando-os no nuget.org.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| AllVersions | Listar todas as versões de um pacote. Por padrão, somente a versão mais recente do pacote é exibida. |
| ConfigFile | O arquivo de configuração do NuGet a ser aplicado. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) será usado.|
| ForceEnglishOutput | *(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| IncludeDelisted | *(3,2 +)* Exibir pacotes não listados. |
| NonInteractive | Suprime prompts de entrada ou confirmações do usuário. |
| PreRelease | Inclui pacotes de pré-lançamento na lista. |
| Source | Especifica uma lista de fontes de pacotes a serem pesquisadas. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

Listar todos os pacotes de feeds configurados:
```
nuget list
```
Listar pacotes relacionados ao Azure com detalhes detalhados:
```
nuget list Azure -Verbosity detailed
```
Listar todas as versões de pacotes relacionados ao Azure de feeds configurados:
```
nuget list Azure -AllVersions
```
Listar todas as versões de pacotes relacionados ao JSON de origem/feed especificado:
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
Listar pacotes relacionados a JSON de várias fontes/feeds:
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

