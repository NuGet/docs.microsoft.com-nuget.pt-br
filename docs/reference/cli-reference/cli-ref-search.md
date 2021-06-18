---
title: Comando de pesquisa da CLI do NuGet
description: Referência para o comando nuget.exe search
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323655"
---
# <a name="search-command-nuget-cli"></a>comando search (CLI do NuGet)

**Aplica-se a:** consumo de pacote &bullet; **Versões com suporte:** 5.8+

Pesquisa uma determinada fonte usando a cadeia de caracteres de consulta fornecida. Se nenhuma fonte for especificada, todas as fontes definidas em %AppData%\NuGet\NuGet.Config serão usadas.

## <a name="usage"></a>Uso

```cli
nuget search [search terms] [options]
```

em que os termos de pesquisa são aplicados aos nomes de pacotes, marcas e descrições do pacote, assim como são ao usá-los no nuget.org.

## <a name="options"></a>Opções

| Nome | Descrição | Uso |
| ---  |     ---     |  :-:  |
| Pré-lançamento | Os pacotes de pré-lançamento não são incluídos por padrão, mas podem ser incluídos usando esse argumento | -PreRelease |
| Fonte | Origem(s) de pacote específica a ser pesquisada em vez de consultar as fontes padrão no __nuget.config__ | -Source `<Source URL>`|
| Take | O número de resultados a retornar. O valor padrão é 20. | -Take `<positive integer>` |
| Detalhamento | O nível de detalhes a ser exibido na saída. O padrão é _normal._ (Veja a observação abaixo)  | -Verbosity `<quiet|normal|detailed>` |
| Ajuda | Exibe informações de ajuda para o comando | -Help |

Consulte também [Variáveis de ambiente](cli-ref-environment-variables.md)

> [!NOTE] 
> Níveis de detalhes:
> * _quiet_ – ID do pacote, versão
> * _normal_ – ID do pacote, versão, downloads, visualização da descrição
> * _detalhado –_ ID do pacote, versão, downloads, descrição completa, outras informações, como a URL da consulta

## <a name="examples"></a>Exemplos

Pesquise *pacotes* relacionados ao registro em log de fontes padrão:
```
nuget search logging
```
*Pesquise pacotes* relacionados ao registro em log com detalhamento detalhado:
```
nuget search logging -Verbosity detailed
```
*Pesquise pacotes* relacionados ao registro em log e mostre apenas os cinco principais resultados:
```
nuget search logging -Take 5
```
Pesquise pacotes relacionados a *JSON,* incluindo versões de pré-lançamento, do feed/origem especificado:
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
Pesquise pacotes relacionados a *JSON* de várias fontes/feeds:
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
