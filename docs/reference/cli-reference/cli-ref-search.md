---
title: Comando de pesquisa da CLI do NuGet
description: Referência para o comando nuget.exe Search
author: advay26
ms.author: t-adtand
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 35e4906960534299418cb2a17c190476708b2634
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623262"
---
# <a name="search-command-nuget-cli"></a>comando Search (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** do consumo de pacotes: 5.8 +

Pesquisa uma determinada fonte usando a cadeia de caracteres de consulta fornecida. Se nenhuma fonte for especificada, todas as fontes definidas em% AppData% \NuGet\NuGet.config serão usadas.

## <a name="usage"></a>Uso

```cli
nuget search [search terms] [options]
```

onde os termos de pesquisa são aplicados aos nomes de pacotes, marcas e descrições de pacote, assim como são quando eles são usado em nuget.org.

## <a name="options"></a>Opções

| Nome | Descrição | Uso |
| ---  |     ---     |  :-:  |
| Pré-lançamento | Os pacotes de pré-lançamento não são incluídos por padrão, mas podem ser incluídos usando esse argumento | -Pré-lançamento |
| Fonte | Origem (s) de pacote específico para pesquisar em vez de consultar as fontes padrão no __nuget.config__ | -Origem `<Source URL>`|
| Take | O número de resultados a serem retornados. O valor padrão é 20. | -Take `<positive integer>` |
| Detalhamento | O nível de detalhe a ser exibido na saída. O padrão é _normal_. (Consulte a observação abaixo)  | -Detalhes `<quiet\|normal\|detailed>` |
| Ajuda | Exibe informações de ajuda para o comando | -Ajuda |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

__OBSERVAÇÃO__

Níveis de detalhamento:

* _Quiet_ -ID do pacote, versão
* _normal_ -ID do pacote, versão, downloads, visualização da descrição
* _detalhado_ -ID do pacote, versão, downloads, descrição completa, outras informações, como a URL de consulta

## <a name="examples"></a>Exemplos

Pesquisar pacotes relacionados ao *log*de fontes padrão:
```
nuget search logging
```
Pesquise pacotes relacionados ao *registro em log*com detalhes detalhados:
```
nuget search logging -Verbosity detailed
```
Pesquise pacotes relacionados ao *registro em log*e mostre apenas os 5 principais resultados:
```
nuget search logging -Take 5
```
Pesquisar pacotes relacionados a *JSON*, incluindo versões de pré-lançamento, de origem/feed especificado:
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
Pesquisar pacotes relacionados a *JSON*de várias fontes/feeds:
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
