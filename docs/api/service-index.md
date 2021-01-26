---
title: Índice de serviço, API do NuGet
description: O índice de serviço é o ponto de entrada da API HTTP do NuGet e enumera os recursos do servidor.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775355"
---
# <a name="service-index"></a>Índice de serviço

O índice de serviço é um documento JSON que é o ponto de entrada para uma origem de pacote NuGet e permite que uma implementação de cliente descubra os recursos da origem do pacote. O índice de serviço é um objeto JSON com duas propriedades obrigatórias: `version` (a versão do esquema do índice de serviço) e `resources`  (os pontos de extremidade ou as funcionalidades da origem do pacote).

o índice de serviço do NuGet. org está localizado em `https://api.nuget.org/v3/index.json` .

## <a name="versioning"></a>Controle de versão

O `version` valor é uma cadeia de caracteres de versão analisável SemVer 2.0.0 que indica a versão do esquema do índice de serviço. A API determina que a cadeia de caracteres de versão tem um número de versão principal de `3` . Como alterações não significativas são feitas no esquema de índice de serviço, a versão secundária da cadeia de caracteres de versão será aumentada.

Cada recurso no índice de serviço tem controle de versão independentemente da versão do esquema do índice de serviço.

A versão atual do esquema é `3.0.0` . A `3.0.0` versão é funcionalmente equivalente à versão mais antiga `3.0.0-beta.1` , mas deve ser preferida, pois ela comunica mais claramente o esquema estável e definido.

## <a name="http-methods"></a>Métodos HTTP

O índice de serviço pode ser acessado usando métodos HTTP `GET` e `HEAD` .

## <a name="resources"></a>Recursos

A `resources` propriedade contém uma matriz de recursos com suporte nesta origem do pacote.

### <a name="resource"></a>Recurso

Um recurso é um objeto na `resources` matriz. Ele representa um recurso com versão de uma origem de pacote. Um recurso tem as seguintes propriedades:

Nome          | Type   | Necessária | Observações
------------- | ------ | -------- | -----
@id           | string | sim      | A URL para o recurso
@type         | string | sim      | Uma constante de cadeia de caracteres que representa o tipo de recurso
comentário       | string | não       | Uma descrição legível humana do recurso

O `@id` é uma URL que deve ser absoluta e deve ter o esquema http ou HTTPS.

O `@type` é usado para identificar o protocolo específico a ser usado ao interagir com o recurso. O tipo do recurso é uma cadeia de caracteres opaca, mas geralmente tem o formato:

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

Os clientes devem embutir em código os `@type` valores que eles entendem e procurar em um índice de serviço da origem do pacote. Os valores exatos `@type` em uso hoje são enumerados nos documentos de referência de recursos individuais listados na [visão geral da API](overview.md#resources-and-schema).

Para fins desta documentação, a documentação sobre diferentes recursos será basicamente agrupada pelo `{RESOURCE_NAME}` encontrado no índice de serviço, que é análogo ao agrupamento por cenário. 

Não há nenhum requisito para que cada recurso tenha um único `@id` ou `@type` . Cabe à implementação do cliente determinar qual recurso você prefere sobre outro. Uma implementação possível é que os recursos do mesmo ou compatíveis `@type` podem ser usados em um modo Round Robin em caso de falha de conexão ou erro de servidor.

### <a name="sample-request"></a>Solicitação de exemplo

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [service-index.json](./_data/service-index.json)]
