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
ms.openlocfilehash: c5d3cf68ac6a96a6c14eb5e652bcf72698b6a8e8
ms.sourcegitcommit: 8f0bb8bb9cb91d27d660963ed9b0f32642f420fe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34225938"
---
# <a name="rate-limits"></a><span data-ttu-id="57b45-103">Limites de taxa</span><span class="sxs-lookup"><span data-stu-id="57b45-103">Rate Limits</span></span>

<span data-ttu-id="57b45-104">A API do NuGet.org impõe a limitação de taxa para evitar o abuso.</span><span class="sxs-lookup"><span data-stu-id="57b45-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="57b45-105">Solicitações que excedem o limite de taxa retornam o erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="57b45-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="57b45-106">As tabelas a seguir listam os limites de taxa para a API do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="57b45-106">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="57b45-107">Pesquisa de pacote</span><span class="sxs-lookup"><span data-stu-id="57b45-107">Package search</span></span>

> [!Note]
> <span data-ttu-id="57b45-108">Recomendamos o uso do NuGet.org [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) para pesquisa de alto desempenho e não têm nenhum limite no momento.</span><span class="sxs-lookup"><span data-stu-id="57b45-108">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="57b45-109">APIs de pesquisa V1 e V2, os limites de followins se aplicam:</span><span class="sxs-lookup"><span data-stu-id="57b45-109">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="57b45-110">API</span><span class="sxs-lookup"><span data-stu-id="57b45-110">API</span></span> | <span data-ttu-id="57b45-111">Tipo de limite</span><span class="sxs-lookup"><span data-stu-id="57b45-111">Limit Type</span></span> | <span data-ttu-id="57b45-112">Valor do limite</span><span class="sxs-lookup"><span data-stu-id="57b45-112">Limit Value</span></span> | <span data-ttu-id="57b45-113">API usecase</span><span class="sxs-lookup"><span data-stu-id="57b45-113">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="57b45-114">**OBTER** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="57b45-114">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="57b45-115">PI</span><span class="sxs-lookup"><span data-stu-id="57b45-115">IP</span></span> | <span data-ttu-id="57b45-116">1000 / minuto</span><span class="sxs-lookup"><span data-stu-id="57b45-116">1000 / minute</span></span> | <span data-ttu-id="57b45-117">Consultar metadados de pacote do NuGet via OData v1 `Packages` coleção</span><span class="sxs-lookup"><span data-stu-id="57b45-117">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="57b45-118">**OBTER** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="57b45-118">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="57b45-119">PI</span><span class="sxs-lookup"><span data-stu-id="57b45-119">IP</span></span> | <span data-ttu-id="57b45-120">3000 / minuto</span><span class="sxs-lookup"><span data-stu-id="57b45-120">3000 / minute</span></span> | <span data-ttu-id="57b45-121">Procurar pacotes do NuGet via ponto de extremidade de pesquisa v1</span><span class="sxs-lookup"><span data-stu-id="57b45-121">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="57b45-122">**OBTER** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="57b45-122">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="57b45-123">PI</span><span class="sxs-lookup"><span data-stu-id="57b45-123">IP</span></span> | <span data-ttu-id="57b45-124">20000 / minuto</span><span class="sxs-lookup"><span data-stu-id="57b45-124">20000 / minute</span></span> | <span data-ttu-id="57b45-125">Consultar metadados de pacote do NuGet via OData v2 `Packages` coleção</span><span class="sxs-lookup"><span data-stu-id="57b45-125">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="57b45-126">**OBTER** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="57b45-126">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="57b45-127">PI</span><span class="sxs-lookup"><span data-stu-id="57b45-127">IP</span></span> | <span data-ttu-id="57b45-128">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="57b45-128">100 / minute</span></span> | <span data-ttu-id="57b45-129">Consulta de contagem de pacotes do NuGet via OData v2 `Packages` coleção</span><span class="sxs-lookup"><span data-stu-id="57b45-129">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="57b45-130">Pacote de Push e remover da lista</span><span class="sxs-lookup"><span data-stu-id="57b45-130">Package Push and Unlist</span></span>

| <span data-ttu-id="57b45-131">API</span><span class="sxs-lookup"><span data-stu-id="57b45-131">API</span></span> | <span data-ttu-id="57b45-132">Tipo de limite</span><span class="sxs-lookup"><span data-stu-id="57b45-132">Limit Type</span></span> | <span data-ttu-id="57b45-133">Valor do limite</span><span class="sxs-lookup"><span data-stu-id="57b45-133">Limit Value</span></span> | <span data-ttu-id="57b45-134">API usecase</span><span class="sxs-lookup"><span data-stu-id="57b45-134">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="57b45-135">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="57b45-135">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="57b45-136">Chave de API</span><span class="sxs-lookup"><span data-stu-id="57b45-136">API Key</span></span> | <span data-ttu-id="57b45-137">250 / hora</span><span class="sxs-lookup"><span data-stu-id="57b45-137">250 / hour</span></span> | <span data-ttu-id="57b45-138">Carregue um novo pacote de NuGet (versão) por meio do ponto de extremidade de envio por push v2</span><span class="sxs-lookup"><span data-stu-id="57b45-138">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="57b45-139">**EXCLUIR** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="57b45-139">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="57b45-140">Chave de API</span><span class="sxs-lookup"><span data-stu-id="57b45-140">API Key</span></span> | <span data-ttu-id="57b45-141">250 / hora</span><span class="sxs-lookup"><span data-stu-id="57b45-141">250 / hour</span></span> | <span data-ttu-id="57b45-142">Remover da lista um pacote do NuGet via ponto de extremidade v2 (versão)</span><span class="sxs-lookup"><span data-stu-id="57b45-142">Unlist a NuGet package (version) via v2 endpoint</span></span> 
