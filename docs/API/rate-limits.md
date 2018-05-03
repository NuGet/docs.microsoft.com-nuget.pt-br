---
title: Limites, o NuGet API de taxa
description: As APIs do NuGet serão ter impostas limites de taxa para evitar o abuso.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 3aaebef8fff670759c6484a5a8f90a2f4dd58c66
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="rate-limits"></a><span data-ttu-id="c4e07-103">Limites de taxa</span><span class="sxs-lookup"><span data-stu-id="c4e07-103">Rate Limits</span></span>

<span data-ttu-id="c4e07-104">A API do NuGet.org impõe a limitação de taxa para evitar o abuso.</span><span class="sxs-lookup"><span data-stu-id="c4e07-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="c4e07-105">Solicitações que excedem o limite de taxa retornam o erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4e07-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="c4e07-106">As tabelas a seguir listam os limites de taxa para a API do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c4e07-106">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="c4e07-107">Pesquisa de pacote</span><span class="sxs-lookup"><span data-stu-id="c4e07-107">Package search</span></span>

> [!Note]
> <span data-ttu-id="c4e07-108">Recomendamos o uso do NuGet.org [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) para pesquisa de alto desempenho e não têm nenhum limite no momento.</span><span class="sxs-lookup"><span data-stu-id="c4e07-108">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="c4e07-109">APIs de pesquisa V1 e V2, os limites de followins se aplicam:</span><span class="sxs-lookup"><span data-stu-id="c4e07-109">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="c4e07-110">API</span><span class="sxs-lookup"><span data-stu-id="c4e07-110">API</span></span> | <span data-ttu-id="c4e07-111">Tipo de limite</span><span class="sxs-lookup"><span data-stu-id="c4e07-111">Limit Type</span></span> | <span data-ttu-id="c4e07-112">Valor do limite</span><span class="sxs-lookup"><span data-stu-id="c4e07-112">Limit Value</span></span> | <span data-ttu-id="c4e07-113">API usecase</span><span class="sxs-lookup"><span data-stu-id="c4e07-113">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="c4e07-114">**OBTER** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="c4e07-114">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="c4e07-115">PI</span><span class="sxs-lookup"><span data-stu-id="c4e07-115">IP</span></span> | <span data-ttu-id="c4e07-116">1000 / minuto</span><span class="sxs-lookup"><span data-stu-id="c4e07-116">1000 / minute</span></span> | <span data-ttu-id="c4e07-117">Consultar metadados de pacote do NuGet via OData v1 `Packages` coleção</span><span class="sxs-lookup"><span data-stu-id="c4e07-117">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="c4e07-118">**OBTER** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="c4e07-118">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="c4e07-119">PI</span><span class="sxs-lookup"><span data-stu-id="c4e07-119">IP</span></span> | <span data-ttu-id="c4e07-120">3000 / minuto</span><span class="sxs-lookup"><span data-stu-id="c4e07-120">3000 / minute</span></span> | <span data-ttu-id="c4e07-121">Procurar pacotes do NuGet via ponto de extremidade de pesquisa v1</span><span class="sxs-lookup"><span data-stu-id="c4e07-121">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="c4e07-122">**OBTER** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="c4e07-122">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="c4e07-123">PI</span><span class="sxs-lookup"><span data-stu-id="c4e07-123">IP</span></span> | <span data-ttu-id="c4e07-124">20000 / minuto</span><span class="sxs-lookup"><span data-stu-id="c4e07-124">20000 / minute</span></span> | <span data-ttu-id="c4e07-125">Consultar metadados de pacote do NuGet via OData v2 `Packages` coleção</span><span class="sxs-lookup"><span data-stu-id="c4e07-125">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="c4e07-126">**OBTER** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="c4e07-126">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="c4e07-127">PI</span><span class="sxs-lookup"><span data-stu-id="c4e07-127">IP</span></span> | <span data-ttu-id="c4e07-128">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="c4e07-128">100 / minute</span></span> | <span data-ttu-id="c4e07-129">Consulta de contagem de pacotes do NuGet via OData v2 `Packages` coleção</span><span class="sxs-lookup"><span data-stu-id="c4e07-129">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="c4e07-130">Pacote de Push e remover da lista</span><span class="sxs-lookup"><span data-stu-id="c4e07-130">Package Push and Unlist</span></span>

| <span data-ttu-id="c4e07-131">API</span><span class="sxs-lookup"><span data-stu-id="c4e07-131">API</span></span> | <span data-ttu-id="c4e07-132">Tipo de limite</span><span class="sxs-lookup"><span data-stu-id="c4e07-132">Limit Type</span></span> | <span data-ttu-id="c4e07-133">Valor do limite</span><span class="sxs-lookup"><span data-stu-id="c4e07-133">Limit Value</span></span> | <span data-ttu-id="c4e07-134">APU usecase</span><span class="sxs-lookup"><span data-stu-id="c4e07-134">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="c4e07-135">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="c4e07-135">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="c4e07-136">Chave de API</span><span class="sxs-lookup"><span data-stu-id="c4e07-136">API Key</span></span> | <span data-ttu-id="c4e07-137">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="c4e07-137">100 / minute</span></span> | <span data-ttu-id="c4e07-138">Carregue um novo pacote de NuGet (versão) por meio do ponto de extremidade de envio por push v2</span><span class="sxs-lookup"><span data-stu-id="c4e07-138">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="c4e07-139">**EXCLUIR** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="c4e07-139">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="c4e07-140">Chave de API</span><span class="sxs-lookup"><span data-stu-id="c4e07-140">API Key</span></span> | <span data-ttu-id="c4e07-141">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="c4e07-141">100 / minute</span></span> | <span data-ttu-id="c4e07-142">Remover da lista um pacote do NuGet via ponto de extremidade v2 (versão)</span><span class="sxs-lookup"><span data-stu-id="c4e07-142">Unlist a NuGet package (version) via v2 endpoint</span></span> 
