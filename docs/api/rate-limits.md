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
# <a name="rate-limits"></a><span data-ttu-id="3e77b-103">Limites de taxa</span><span class="sxs-lookup"><span data-stu-id="3e77b-103">Rate Limits</span></span>

<span data-ttu-id="3e77b-104">A API NuGet.org impõe a limitação de taxa para evitar abuso.</span><span class="sxs-lookup"><span data-stu-id="3e77b-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="3e77b-105">As solicitações que excedem o limite de taxa retornam o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="3e77b-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="3e77b-106">Além da limitação de solicitação usando limites de taxa, algumas APIs também impõem cotas.</span><span class="sxs-lookup"><span data-stu-id="3e77b-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="3e77b-107">As solicitações que excedem a cota retornam o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="3e77b-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="3e77b-108">As tabelas a seguir listam os limites de taxa para a API NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="3e77b-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="3e77b-109">Pesquisa de pacote</span><span class="sxs-lookup"><span data-stu-id="3e77b-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="3e77b-110">É recomendável usar as APIs de [pesquisa v3](search-query-service-resource.md) do NuGet. org, pois a taxa não é limitada no momento.</span><span class="sxs-lookup"><span data-stu-id="3e77b-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="3e77b-111">Para APIs de pesquisa v1 e v2, os seguintes limites se aplicam:</span><span class="sxs-lookup"><span data-stu-id="3e77b-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="3e77b-112">API</span><span class="sxs-lookup"><span data-stu-id="3e77b-112">API</span></span> | <span data-ttu-id="3e77b-113">Tipo de limite</span><span class="sxs-lookup"><span data-stu-id="3e77b-113">Limit Type</span></span> | <span data-ttu-id="3e77b-114">Valor de limite</span><span class="sxs-lookup"><span data-stu-id="3e77b-114">Limit Value</span></span> | <span data-ttu-id="3e77b-115">UseCase de API</span><span class="sxs-lookup"><span data-stu-id="3e77b-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="3e77b-116">**Obter** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="3e77b-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="3e77b-117">PI</span><span class="sxs-lookup"><span data-stu-id="3e77b-117">IP</span></span> | <span data-ttu-id="3e77b-118">1000/minuto</span><span class="sxs-lookup"><span data-stu-id="3e77b-118">1000 / minute</span></span> | <span data-ttu-id="3e77b-119">Consultar metadados do pacote NuGet via coleção de `Packages` do OData v1</span><span class="sxs-lookup"><span data-stu-id="3e77b-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="3e77b-120">**Obter** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="3e77b-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="3e77b-121">PI</span><span class="sxs-lookup"><span data-stu-id="3e77b-121">IP</span></span> | <span data-ttu-id="3e77b-122">3000/minuto</span><span class="sxs-lookup"><span data-stu-id="3e77b-122">3000 / minute</span></span> | <span data-ttu-id="3e77b-123">Pesquisar pacotes NuGet por meio do ponto de extremidade de pesquisa v1</span><span class="sxs-lookup"><span data-stu-id="3e77b-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="3e77b-124">**Obter** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="3e77b-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="3e77b-125">PI</span><span class="sxs-lookup"><span data-stu-id="3e77b-125">IP</span></span> | <span data-ttu-id="3e77b-126">20000/minuto</span><span class="sxs-lookup"><span data-stu-id="3e77b-126">20000 / minute</span></span> | <span data-ttu-id="3e77b-127">Consultar metadados do pacote NuGet por meio da coleção de `Packages` OData do v2</span><span class="sxs-lookup"><span data-stu-id="3e77b-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="3e77b-128">**Obter** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="3e77b-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="3e77b-129">PI</span><span class="sxs-lookup"><span data-stu-id="3e77b-129">IP</span></span> | <span data-ttu-id="3e77b-130">100/minuto</span><span class="sxs-lookup"><span data-stu-id="3e77b-130">100 / minute</span></span> | <span data-ttu-id="3e77b-131">Consultar a contagem de pacotes NuGet por meio da coleção de `Packages` do OData do v2</span><span class="sxs-lookup"><span data-stu-id="3e77b-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="3e77b-132">Enviar por push de pacote e não listar</span><span class="sxs-lookup"><span data-stu-id="3e77b-132">Package Push and Unlist</span></span>

| <span data-ttu-id="3e77b-133">API</span><span class="sxs-lookup"><span data-stu-id="3e77b-133">API</span></span> | <span data-ttu-id="3e77b-134">Tipo de limite</span><span class="sxs-lookup"><span data-stu-id="3e77b-134">Limit Type</span></span> | <span data-ttu-id="3e77b-135">Valor de limite</span><span class="sxs-lookup"><span data-stu-id="3e77b-135">Limit Value</span></span> | <span data-ttu-id="3e77b-136">UseCase de API</span><span class="sxs-lookup"><span data-stu-id="3e77b-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="3e77b-137">**Colocar** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="3e77b-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="3e77b-138">Chave de API</span><span class="sxs-lookup"><span data-stu-id="3e77b-138">API Key</span></span> | <span data-ttu-id="3e77b-139">350/hora</span><span class="sxs-lookup"><span data-stu-id="3e77b-139">350 / hour</span></span> | <span data-ttu-id="3e77b-140">Carregar um novo pacote NuGet (versão) por meio do ponto de extremidade de push v2</span><span class="sxs-lookup"><span data-stu-id="3e77b-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="3e77b-141">**Excluir** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="3e77b-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="3e77b-142">Chave de API</span><span class="sxs-lookup"><span data-stu-id="3e77b-142">API Key</span></span> | <span data-ttu-id="3e77b-143">250/hora</span><span class="sxs-lookup"><span data-stu-id="3e77b-143">250 / hour</span></span> | <span data-ttu-id="3e77b-144">Deslistar um pacote NuGet (versão) via ponto de extremidade v2</span><span class="sxs-lookup"><span data-stu-id="3e77b-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
