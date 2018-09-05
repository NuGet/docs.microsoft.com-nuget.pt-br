---
title: Índice de serviço, API do NuGet
description: O índice de serviço é o ponto de entrada da API de HTTP do NuGet e enumera os recursos do servidor.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 478b74f98caafdc7c6b69423b9f9d72890c8d7cb
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545251"
---
# <a name="service-index"></a>Índice de serviço

O índice de serviço é um documento JSON que é o ponto de entrada para uma origem de pacote do NuGet e permite que uma implementação de cliente descobrir os recursos da fonte de pacote. O índice de serviço é um objeto JSON com duas propriedades obrigatórias: `version` (a versão do esquema do índice de serviço) e `resources` (pontos de extremidade ou recursos da origem do pacote).

índice de serviço do NuGet.org está localizado em `https://api.nuget.org/v3/index.json`.

## <a name="versioning"></a>Controle de versão

O `version` valor é uma cadeia de caracteres de versão pode ser analisado SemVer 2.0.0 que indica a versão do esquema do índice de serviço. A API exige que a cadeia de caracteres de versão tem um número de versão principal `3`. Como o esquema de índice de serviço forem feitas alterações sem interrupções, versão secundária da cadeia de caracteres de versão será aumentado.

Cada recurso no índice de serviço tem controle de versão independentemente do serviço de versão de esquema de índice.

A versão atual do esquema é `3.0.0`. O `3.0.0` versão é funcionalmente equivalente à antiga `3.0.0-beta.1` versão, mas deve ser preferencial, pois ele se comunica mais claramente o esquema estável, definido.

## <a name="http-methods"></a>Métodos HTTP

O índice de serviço é acessível por meio de métodos HTTP `GET` e `HEAD`.

## <a name="resources"></a>Recursos

O `resources` propriedade contém uma matriz de recursos com suporte desta origem do pacote.

### <a name="resource"></a>Recurso

Um recurso é um objeto no `resources` matriz. Representa um recurso de controle de versão de uma origem de pacote. Um recurso tem as seguintes propriedades:

Nome          | Tipo   | Necessária | Observações
------------- | ------ | -------- | -----
@id           | cadeia de caracteres | sim      | A URL para o recurso
@type         | cadeia de caracteres | sim      | Uma constante de cadeia de caracteres que representa o tipo de recurso
comment       | cadeia de caracteres | no       | Uma descrição legível do recurso

O `@id` é uma URL que deve ser absoluto e deve ter o esquema HTTP ou HTTPS.

O `@type` é usado para identificar o protocolo específico a ser usado ao interagir com o recurso. O tipo do recurso é uma cadeia de caracteres opaca, mas geralmente tem o formato:

    {RESOURCE_NAME}/{RESOURCE_VERSION}

Os clientes devem codificar o `@type` valores que compreendem e pesquisar no índice de serviço da origem do pacote. Exatamente `@type` valores em uso atualmente são enumerados sobre os documentos de referência de recursos individuais listados na [visão geral da API](overview.md#resources-and-schema).

Para fins desta documentação, a documentação sobre recursos diferentes, essencialmente, será agrupada pelo `{RESOURCE_NAME}` encontrado no índice de serviço que é análogo ao agrupamento por cenário. 

Não há nenhum requisito de que cada recurso tem um único `@id` ou `@type`. Cabe a implementação do cliente para determinar qual recurso para dar preferência em relação a outra. Uma possível implementação é que os recursos da mesma ou compatível `@type` podem ser usados em um estilo round-robin em caso de erro de servidor ou de falha de conexão.

### <a name="sample-request"></a>Exemplo de solicitação

OBTER https://api.nuget.org/v3/index.json

### <a name="sample-response"></a>Resposta de exemplo

[!code-JSON [service-index.json](./_data/service-index.json)]
