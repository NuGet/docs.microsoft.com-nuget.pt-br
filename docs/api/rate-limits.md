---
title: API do NuGet, os limites de taxa
description: As APIs do NuGet será impuseram limites de taxa para evitar abusos.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: a55eb49318b766028d1579a4d33618617bbd8801
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508121"
---
# <a name="rate-limits"></a>Limites de taxa

A API de NuGet.org impõe a limitação de taxa para evitar abusos. Solicitações que excedem o limite de taxa retornarão o seguinte erro: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Usando limites de taxa de limitação da solicitação, além de algumas APIs também impõem a cota. As solicitações que excedem a cota de retornar o seguinte erro:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

As tabelas a seguir listam os limites de taxa para a API do NuGet.org.

## <a name="package-search"></a>Pesquisa de pacote

> [!Note]
> Recomendamos o uso do NuGet.org [APIs V3](https://docs.microsoft.com/nuget/api/search-query-service-resource) para pesquisa de alto desempenho e não têm nenhum limite no momento. APIs de pesquisa V1 e V2, os limites de followins se aplicam:


| API | Tipo de limite | Valor de limite | API usecase |
|:---|:---|:---|:---|
**OBTER** `/api/v1/Packages` | PI | 1000 / minuto | Consultar metadados de pacote do NuGet por meio do OData v1 `Packages` coleção |
**OBTER** `/api/v1/Search()` | PI | 3000 / minuto | Procurar pacotes do NuGet por meio do ponto de extremidade v1 Search | 
**OBTER** `/api/v2/Packages` | PI | 20000 / minuto | Consultar metadados de pacote do NuGet por meio do OData v2 `Packages` coleção | 
**OBTER** `/api/v2/Packages/$count` | PI | 100 / minuto | Consultar a contagem de pacotes do NuGet por meio do OData v2 `Packages` coleção | 

## <a name="package-push-and-unlist"></a>Pacote de Push e remover da lista

| API | Tipo de limite | Valor de limite | API usecase | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | Chave de API | 250 / hora | Carregar um novo pacote de NuGet (versão) por meio do ponto de extremidade de envio por push v2 
**EXCLUIR** `/api/v2/package/{id}/{version}` | Chave de API | 250 / hora | Remover da lista um pacote do NuGet por meio do ponto de extremidade v2 (versão) 
