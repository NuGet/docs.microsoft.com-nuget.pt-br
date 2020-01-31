---
title: Limites de taxa, API do NuGet
description: As APIs do NuGet terão limites de taxa impostos para evitar abusos.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813189"
---
# <a name="rate-limits"></a>Limites de taxa

A API NuGet.org impõe a limitação de taxa para evitar abuso. As solicitações que excedem o limite de taxa retornam o seguinte erro: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Além da limitação de solicitação usando limites de taxa, algumas APIs também impõem cotas. As solicitações que excedem a cota retornam o seguinte erro:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

As tabelas a seguir listam os limites de taxa para a API NuGet.org.

## <a name="package-search"></a>Pesquisa de pacote

> [!Note]
> É recomendável usar as APIs de [pesquisa v3](search-query-service-resource.md) do NuGet. org, pois a taxa não é limitada no momento. Para APIs de pesquisa v1 e v2, os seguintes limites se aplicam:

| API | Tipo de limite | Valor de limite | UseCase de API |
|:---|:---|:---|:---|
**Obter** `/api/v1/Packages` | PI | 1000/minuto | Consultar metadados do pacote NuGet via coleção de `Packages` do OData v1 |
**Obter** `/api/v1/Search()` | PI | 3000/minuto | Pesquisar pacotes NuGet por meio do ponto de extremidade de pesquisa v1 | 
**Obter** `/api/v2/Packages` | PI | 20000/minuto | Consultar metadados do pacote NuGet por meio da coleção de `Packages` OData do v2 | 
**Obter** `/api/v2/Packages/$count` | PI | 100/minuto | Consultar a contagem de pacotes NuGet por meio da coleção de `Packages` do OData do v2 | 

## <a name="package-push-and-unlist"></a>Enviar por push de pacote e não listar

| API | Tipo de limite | Valor de limite | UseCase de API | 
|:---|:---|:---|:--- |
**Colocar** `/api/v2/package` | Chave de API | 350/hora | Carregar um novo pacote NuGet (versão) por meio do ponto de extremidade de push v2 
**Excluir** `/api/v2/package/{id}/{version}` | Chave de API | 250/hora | Deslistar um pacote NuGet (versão) via ponto de extremidade v2 
