---
title: Limites de taxa | Microsoft Docs
author:
- cmanu
- anangaur
ms.author:
- cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: As APIs do NuGet serão ter impostas limites de taxa para evitar o abuso.
keywords: Limitação de taxa de API, o NuGet
ms.reviewer:
- skofman
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f7891d5e4c008219d9f4808f223f3e5e7ae06ced
ms.sourcegitcommit: fa40be739d093a37d5f7072b62ebdb4f595f4110
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2018
---
# <a name="rate-limits"></a>Limites de taxa

A API do NuGet.org impõe a limitação de taxa para evitar o abuso. Solicitações que excedem o limite de taxa retornam o erro a seguir: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

As tabelas a seguir listam os limites de taxa para a API do NuGet.org.

## <a name="package-search"></a>Pesquisa de pacote

> [!Note]
> Recomendamos o uso do NuGet.org [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) para pesquisa de alto desempenho e não têm nenhum limite no momento. APIs de pesquisa V1 e V2, os limites de followins se aplicam:


| API | Tipo de limite | Valor do limite | API usecase |
|:---|:---|:---|:---|
**OBTER** `/api/v1/Packages` | PI | 1000 / minuto | Consultar metadados de pacote do NuGet via OData v1 `Packages` coleção |
**OBTER** `/api/v1/Search()` | PI | 3000 / minuto | Procurar pacotes do NuGet via ponto de extremidade de pesquisa v1 | 
**OBTER** `/api/v2/Packages` | PI | 20000 / minuto | Consultar metadados de pacote do NuGet via OData v2 `Packages` coleção | 
**OBTER** `/api/v2/Packages/$count` | PI | 100 / minuto | Consulta de contagem de pacotes do NuGet via OData v2 `Packages` coleção | 

## <a name="package-push-and-unlist"></a>Pacote de Push e remover da lista

| API | Tipo de limite | Valor do limite | APU usecase | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | Chave de API | 100 / minuto | Carregue um novo pacote de NuGet (versão) por meio do ponto de extremidade de envio por push v2 
**EXCLUIR** `/api/v2/package/{id}/{version}` | Chave de API | 100 / minuto | Remover da lista um pacote do NuGet via ponto de extremidade v2 (versão) 
