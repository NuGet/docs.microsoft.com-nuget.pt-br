---
title: API do NuGet, os limites de taxa
description: As APIs do NuGet será impuseram limites de taxa para evitar abusos.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548671"
---
# <a name="rate-limits"></a><span data-ttu-id="1834c-103">Limites de taxa</span><span class="sxs-lookup"><span data-stu-id="1834c-103">Rate Limits</span></span>

<span data-ttu-id="1834c-104">A API de NuGet.org impõe a limitação de taxa para evitar abusos.</span><span class="sxs-lookup"><span data-stu-id="1834c-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="1834c-105">Solicitações que excedem o limite de taxa retornarão o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="1834c-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="1834c-106">Usando limites de taxa de limitação da solicitação, além de algumas APIs também impõem a cota.</span><span class="sxs-lookup"><span data-stu-id="1834c-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="1834c-107">As solicitações que excedem a cota de retornar o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="1834c-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="1834c-108">As tabelas a seguir listam os limites de taxa para a API do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="1834c-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="1834c-109">Pesquisa de pacote</span><span class="sxs-lookup"><span data-stu-id="1834c-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="1834c-110">Recomendamos o uso do NuGet.org [APIs V3](https://docs.microsoft.com/nuget/api/search-query-service-resource) para pesquisa de alto desempenho e não têm nenhum limite no momento.</span><span class="sxs-lookup"><span data-stu-id="1834c-110">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="1834c-111">APIs de pesquisa V1 e V2, os limites de followins se aplicam:</span><span class="sxs-lookup"><span data-stu-id="1834c-111">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="1834c-112">API</span><span class="sxs-lookup"><span data-stu-id="1834c-112">API</span></span> | <span data-ttu-id="1834c-113">Tipo de limite</span><span class="sxs-lookup"><span data-stu-id="1834c-113">Limit Type</span></span> | <span data-ttu-id="1834c-114">Valor de limite</span><span class="sxs-lookup"><span data-stu-id="1834c-114">Limit Value</span></span> | <span data-ttu-id="1834c-115">API usecase</span><span class="sxs-lookup"><span data-stu-id="1834c-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="1834c-116">**OBTER** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="1834c-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="1834c-117">PI</span><span class="sxs-lookup"><span data-stu-id="1834c-117">IP</span></span> | <span data-ttu-id="1834c-118">1000 / minuto</span><span class="sxs-lookup"><span data-stu-id="1834c-118">1000 / minute</span></span> | <span data-ttu-id="1834c-119">Consultar metadados de pacote do NuGet por meio do OData v1 `Packages` coleção</span><span class="sxs-lookup"><span data-stu-id="1834c-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="1834c-120">**OBTER** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="1834c-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="1834c-121">PI</span><span class="sxs-lookup"><span data-stu-id="1834c-121">IP</span></span> | <span data-ttu-id="1834c-122">3000 / minuto</span><span class="sxs-lookup"><span data-stu-id="1834c-122">3000 / minute</span></span> | <span data-ttu-id="1834c-123">Procurar pacotes do NuGet por meio do ponto de extremidade v1 Search</span><span class="sxs-lookup"><span data-stu-id="1834c-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="1834c-124">**OBTER** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="1834c-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="1834c-125">PI</span><span class="sxs-lookup"><span data-stu-id="1834c-125">IP</span></span> | <span data-ttu-id="1834c-126">20000 / minuto</span><span class="sxs-lookup"><span data-stu-id="1834c-126">20000 / minute</span></span> | <span data-ttu-id="1834c-127">Consultar metadados de pacote do NuGet por meio do OData v2 `Packages` coleção</span><span class="sxs-lookup"><span data-stu-id="1834c-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="1834c-128">**OBTER** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="1834c-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="1834c-129">PI</span><span class="sxs-lookup"><span data-stu-id="1834c-129">IP</span></span> | <span data-ttu-id="1834c-130">100 / minuto</span><span class="sxs-lookup"><span data-stu-id="1834c-130">100 / minute</span></span> | <span data-ttu-id="1834c-131">Consultar a contagem de pacotes do NuGet por meio do OData v2 `Packages` coleção</span><span class="sxs-lookup"><span data-stu-id="1834c-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="1834c-132">Pacote de Push e remover da lista</span><span class="sxs-lookup"><span data-stu-id="1834c-132">Package Push and Unlist</span></span>

| <span data-ttu-id="1834c-133">API</span><span class="sxs-lookup"><span data-stu-id="1834c-133">API</span></span> | <span data-ttu-id="1834c-134">Tipo de limite</span><span class="sxs-lookup"><span data-stu-id="1834c-134">Limit Type</span></span> | <span data-ttu-id="1834c-135">Valor de limite</span><span class="sxs-lookup"><span data-stu-id="1834c-135">Limit Value</span></span> | <span data-ttu-id="1834c-136">API usecase</span><span class="sxs-lookup"><span data-stu-id="1834c-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="1834c-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="1834c-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="1834c-138">Chave de API</span><span class="sxs-lookup"><span data-stu-id="1834c-138">API Key</span></span> | <span data-ttu-id="1834c-139">250 / hora</span><span class="sxs-lookup"><span data-stu-id="1834c-139">250 / hour</span></span> | <span data-ttu-id="1834c-140">Carregar um novo pacote de NuGet (versão) por meio do ponto de extremidade de envio por push v2</span><span class="sxs-lookup"><span data-stu-id="1834c-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="1834c-141">**EXCLUIR** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="1834c-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="1834c-142">Chave de API</span><span class="sxs-lookup"><span data-stu-id="1834c-142">API Key</span></span> | <span data-ttu-id="1834c-143">250 / hora</span><span class="sxs-lookup"><span data-stu-id="1834c-143">250 / hour</span></span> | <span data-ttu-id="1834c-144">Remover da lista um pacote do NuGet por meio do ponto de extremidade v2 (versão)</span><span class="sxs-lookup"><span data-stu-id="1834c-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
