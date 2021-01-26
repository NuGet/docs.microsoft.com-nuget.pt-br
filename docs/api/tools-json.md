---
title: tools.json para descobrir nuget.exe versões
description: O ponto de extremidade para
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773816"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>tools.json para descobrir nuget.exe versões

Hoje, há algumas maneiras de obter a versão mais recente do nuget.exe em seu computador de maneira programável. Por exemplo, você pode baixar e extrair o [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) pacote do NuGet.org. Isso tem alguma complexidade, pois ela requer que você já tenha nuget.exe (para `nuget.exe install` ) ou precise descompactar o. nupkg usando uma ferramenta de descompactação básica e encontrar o binário interno.

Se você já tiver nuget.exe, também poderá usar `nuget.exe update -self` , mas isso também requer uma cópia existente do nuget.exe. Essa abordagem também o atualiza para a versão mais recente. Ele não permite o uso de uma versão específica.

O `tools.json` ponto de extremidade está disponível para resolver o problema de inicialização e para dar o controle da versão do nuget.exe que você baixa. Isso pode ser usado em ambientes de CI/CD ou em scripts personalizados para descobrir e baixar qualquer versão de lançamento do nuget.exe.

O `tools.json` ponto de extremidade pode ser obtido usando uma solicitação HTTP não autenticada (por exemplo, `Invoke-WebRequest` no PowerShell ou `wget` ). Ele pode ser analisado usando um desserializador JSON e subseqüentes nuget.exe as URLs de download também podem ser buscadas usando solicitações HTTP não autenticadas.

O ponto de extremidade pode ser buscado usando o `GET` método:

```
GET https://dist.nuget.org/tools.json
```

O [esquema JSON](https://json-schema.org/) para o ponto de extremidade está disponível aqui:

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a>Resposta

A resposta é um documento JSON que contém todas as versões disponíveis do nuget.exe.

O objeto JSON raiz tem a seguinte propriedade:

Nome      | Type             | Necessária
--------- | ---------------- | --------
nuget.exe | matriz de objetos | sim

Cada objeto na `nuget.exe` matriz tem as seguintes propriedades:

Nome     | Type   | Necessária | Observações
-------- | ------ | -------- | -----
version  | string | sim      | Uma cadeia de caracteres SemVer 2.0.0
url      | string | sim      | Uma URL absoluta para baixar esta versão do nuget.exe
preparar    | string | sim      | Uma cadeia de caracteres de enumeração
atualizada | string | sim      | Um carimbo de data/hora ISO 8601 aproximado de quando a versão foi disponibilizada

Os itens na matriz serão classificados em ordem decrescente, SemVer 2.0.0 Order. Essa garantia destina-se a reduzir a carga de um cliente que está interessado no número de versão mais alto. No entanto, isso significa que a lista não está classificada em ordem cronológica. Por exemplo, se uma versão principal inferior for atendida em uma data posterior à versão principal mais alta, essa versão de serviço não aparecerá na parte superior da lista. Se você quiser que a versão mais recente seja liberada pelo *carimbo de data/hora*, basta classificar a matriz pela `uploaded` cadeia de caracteres. Isso funciona porque o `uploaded` carimbo de data/hora está no formato [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) , que pode ser classificado cronologicamente usando uma classificação lexicográfica (ou seja, uma classificação de cadeia de caracteres simples).

A `stage` propriedade indica como verificados esta versão da ferramenta é. 

Estágio              | Significado
------------------ | ------
EarlyAccessPreview | Ainda não está visível na [página de download da Web](https://www.nuget.org/downloads) e deve ser validada pelos parceiros
Liberado           | Disponível no site de download, mas ainda não é recomendado para consumo de larga propagação
ReleasedAndBlessed | Disponível no site de download e é recomendado para consumo

Uma abordagem simples para ter a versão mais recente e recomendada é usar a primeira versão na lista com o `stage` valor de `ReleasedAndBlessed` . Isso funciona porque as versões são classificadas em SemVer 2.0.0 Order.

O `NuGet.CommandLine` pacote em NuGet.org normalmente é atualizado apenas com `ReleasedAndBlessed` versões.

### <a name="sample-request"></a>Solicitação de exemplo

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [tools-json.json](./_data/tools-json.json)]
