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
# <a name="rate-limits"></a><span data-ttu-id="b3169-104">Limites de taxa</span><span class="sxs-lookup"><span data-stu-id="b3169-104">Rate Limits</span></span>

<span data-ttu-id="b3169-105">A API do NuGet.org impõe a limitação de taxa para evitar o abuso.</span><span class="sxs-lookup"><span data-stu-id="b3169-105">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="b3169-106">Solicitações que excedem o limite de taxa retornam o erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3169-106">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="b3169-107">As tabelas a seguir listam os limites de taxa para a API do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="b3169-107">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="b3169-108">Pesquisa de pacote</span><span class="sxs-lookup"><span data-stu-id="b3169-108">Package search</span></span>

> [!Note]
> <span data-ttu-id="b3169-109">Recomendamos o uso do NuGet.org [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) para pesquisa de alto desempenho e não têm nenhum limite no momento.</span><span class="sxs-lookup"><span data-stu-id="b3169-109">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="b3169-110">APIs de pesquisa V1 e V2, os limites de followins se aplicam:</span><span class="sxs-lookup"><span data-stu-id="b3169-110">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="b3169-111">API</span><span class="sxs-lookup"><span data-stu-id="b3169-111">API</span></span> | <span data-ttu-id="b3169-112">Tipo de limite</span><span class="sxs-lookup"><span data-stu-id="b3169-112">Limit Type</span></span> | <span data-ttu-id="b3169-113">Valor do limite</span><span class="sxs-lookup"><span data-stu-id="b3169-113">Limit Value</span></span> | <span data-ttu-id="b3169-114">API usecase</span><span class="sxs-lookup"><span data-stu-id="b3169-114">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="b3169-115">**OBTER** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="b3169-115">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="b3169-116">PI</span><span class="sxs-lookup"><span data-stu-id="b3169-116">IP</span></span> | <span data-ttu-id="b3169-117">1000 / minuto</span><span class="sxs-lookup"><span data-stu-id="b3169-117">1000 / minute</span></span> | <span data-ttu-id="b3169-118">Consultar metadados de pacote do NuGet via OData v1 `Packages` coleção</span><span class="sxs-lookup"><span data-stu-id="b3169-118">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="b3169-119">**OBTER** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="b3169-119">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="b3169-120">PI</span><span class="sxs-lookup"><span data-stu-id="b3169-120">IP</span></span> | <span data-ttu-id="b3169-121">3000 / minuto</span><span class="sxs-lookup"><span data-stu-id="b3169-121">3000 / minute</span></span> | <span data-ttu-id="b3169-122">Procurar pacotes do NuGet via ponto de extremidade de pesquisa v1</span><span class="sxs-lookup"><span data-stu-id="b3169-122">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="b3169-123">**OBTER** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="b3169-123">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="b3169-124">PI</span><span class="sxs-lookup"><span data-stu-id="b3169-124">IP</span></span> | <span data-ttu-id="b3169-125">20000 / minuto</span><span class="sxs-lookup"><span data-stu-id="b3169-125">20000 / minute</span></span> | <span data-ttu-id="b3169-126">Consultar metadados de pacote do NuGet via OData v2 `Packages` coleção</span><span class="sxs-lookup"><span data-stu-id="b3169-126">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="b3169-127">**OBTER** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="b3169-127">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="b3169-128">PI</span><span class="sxs-lookup"><span data-stu-id="b3169-128">IP</span></span> | <span data-ttu-id="b3169-129">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="b3169-129">100 / minute</span></span> | <span data-ttu-id="b3169-130">Consulta de contagem de pacotes do NuGet via OData v2 `Packages` coleção</span><span class="sxs-lookup"><span data-stu-id="b3169-130">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="b3169-131">Pacote de Push e remover da lista</span><span class="sxs-lookup"><span data-stu-id="b3169-131">Package Push and Unlist</span></span>

| <span data-ttu-id="b3169-132">API</span><span class="sxs-lookup"><span data-stu-id="b3169-132">API</span></span> | <span data-ttu-id="b3169-133">Tipo de limite</span><span class="sxs-lookup"><span data-stu-id="b3169-133">Limit Type</span></span> | <span data-ttu-id="b3169-134">Valor do limite</span><span class="sxs-lookup"><span data-stu-id="b3169-134">Limit Value</span></span> | <span data-ttu-id="b3169-135">APU usecase</span><span class="sxs-lookup"><span data-stu-id="b3169-135">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="b3169-136">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="b3169-136">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="b3169-137">Chave de API</span><span class="sxs-lookup"><span data-stu-id="b3169-137">API Key</span></span> | <span data-ttu-id="b3169-138">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="b3169-138">100 / minute</span></span> | <span data-ttu-id="b3169-139">Carregue um novo pacote de NuGet (versão) por meio do ponto de extremidade de envio por push v2</span><span class="sxs-lookup"><span data-stu-id="b3169-139">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="b3169-140">**EXCLUIR** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="b3169-140">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="b3169-141">Chave de API</span><span class="sxs-lookup"><span data-stu-id="b3169-141">API Key</span></span> | <span data-ttu-id="b3169-142">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="b3169-142">100 / minute</span></span> | <span data-ttu-id="b3169-143">Remover da lista um pacote do NuGet via ponto de extremidade v2 (versão)</span><span class="sxs-lookup"><span data-stu-id="b3169-143">Unlist a NuGet package (version) via v2 endpoint</span></span> 
