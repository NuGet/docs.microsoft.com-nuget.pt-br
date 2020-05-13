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
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367928"
---
# <a name="rate-limits"></a><span data-ttu-id="2c81f-103">Limites de taxa</span><span class="sxs-lookup"><span data-stu-id="2c81f-103">Rate Limits</span></span>

<span data-ttu-id="2c81f-104">A API NuGet.org impõe a limitação de taxa para evitar abuso.</span><span class="sxs-lookup"><span data-stu-id="2c81f-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="2c81f-105">As solicitações que excedem o limite de taxa retornam o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="2c81f-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="2c81f-106">Além da limitação de solicitação usando limites de taxa, algumas APIs também impõem cotas.</span><span class="sxs-lookup"><span data-stu-id="2c81f-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="2c81f-107">As solicitações que excedem a cota retornam o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="2c81f-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="2c81f-108">As tabelas a seguir listam os limites de taxa para a API NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="2c81f-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="2c81f-109">Pesquisa de pacote</span><span class="sxs-lookup"><span data-stu-id="2c81f-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="2c81f-110">É recomendável usar as APIs de [pesquisa v3](search-query-service-resource.md) do NuGet. org, pois a taxa não é limitada no momento.</span><span class="sxs-lookup"><span data-stu-id="2c81f-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="2c81f-111">Para APIs de pesquisa v1 e v2, os seguintes limites se aplicam:</span><span class="sxs-lookup"><span data-stu-id="2c81f-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="2c81f-112">API</span><span class="sxs-lookup"><span data-stu-id="2c81f-112">API</span></span> | <span data-ttu-id="2c81f-113">Tipo de limite</span><span class="sxs-lookup"><span data-stu-id="2c81f-113">Limit Type</span></span> | <span data-ttu-id="2c81f-114">Valor de limite</span><span class="sxs-lookup"><span data-stu-id="2c81f-114">Limit Value</span></span> | <span data-ttu-id="2c81f-115">Caso de uso da API</span><span class="sxs-lookup"><span data-stu-id="2c81f-115">API Use Case</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="2c81f-116">**Obter**`/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="2c81f-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="2c81f-117">IP</span><span class="sxs-lookup"><span data-stu-id="2c81f-117">IP</span></span> | <span data-ttu-id="2c81f-118">1000/minuto</span><span class="sxs-lookup"><span data-stu-id="2c81f-118">1000 / minute</span></span> | <span data-ttu-id="2c81f-119">Consultar metadados do pacote NuGet via coleção de OData v1 `Packages`</span><span class="sxs-lookup"><span data-stu-id="2c81f-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="2c81f-120">**Obter**`/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="2c81f-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="2c81f-121">IP</span><span class="sxs-lookup"><span data-stu-id="2c81f-121">IP</span></span> | <span data-ttu-id="2c81f-122">3000/minuto</span><span class="sxs-lookup"><span data-stu-id="2c81f-122">3000 / minute</span></span> | <span data-ttu-id="2c81f-123">Pesquisar pacotes NuGet por meio do ponto de extremidade de pesquisa v1</span><span class="sxs-lookup"><span data-stu-id="2c81f-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="2c81f-124">**Obter**`/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="2c81f-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="2c81f-125">IP</span><span class="sxs-lookup"><span data-stu-id="2c81f-125">IP</span></span> | <span data-ttu-id="2c81f-126">20000/minuto</span><span class="sxs-lookup"><span data-stu-id="2c81f-126">20000 / minute</span></span> | <span data-ttu-id="2c81f-127">Consultar metadados do pacote NuGet por meio da coleção do OData v2 `Packages`</span><span class="sxs-lookup"><span data-stu-id="2c81f-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="2c81f-128">**Obter**`/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="2c81f-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="2c81f-129">IP</span><span class="sxs-lookup"><span data-stu-id="2c81f-129">IP</span></span> | <span data-ttu-id="2c81f-130">100/minuto</span><span class="sxs-lookup"><span data-stu-id="2c81f-130">100 / minute</span></span> | <span data-ttu-id="2c81f-131">Consultar contagem de pacotes NuGet por meio da coleção de OData do v2 `Packages`</span><span class="sxs-lookup"><span data-stu-id="2c81f-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="2c81f-132">Enviar por push de pacote e não listar</span><span class="sxs-lookup"><span data-stu-id="2c81f-132">Package Push and Unlist</span></span>

| <span data-ttu-id="2c81f-133">API</span><span class="sxs-lookup"><span data-stu-id="2c81f-133">API</span></span> | <span data-ttu-id="2c81f-134">Tipo de limite</span><span class="sxs-lookup"><span data-stu-id="2c81f-134">Limit Type</span></span> | <span data-ttu-id="2c81f-135">Valor de limite</span><span class="sxs-lookup"><span data-stu-id="2c81f-135">Limit Value</span></span> | <span data-ttu-id="2c81f-136">Caso de uso da API</span><span class="sxs-lookup"><span data-stu-id="2c81f-136">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="2c81f-137">**Put**`/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="2c81f-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="2c81f-138">Chave de API</span><span class="sxs-lookup"><span data-stu-id="2c81f-138">API Key</span></span> | <span data-ttu-id="2c81f-139">350/hora</span><span class="sxs-lookup"><span data-stu-id="2c81f-139">350 / hour</span></span> | <span data-ttu-id="2c81f-140">Carregar um novo pacote NuGet (versão) por meio do ponto de extremidade de push v2</span><span class="sxs-lookup"><span data-stu-id="2c81f-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="2c81f-141">**Excluir**`/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="2c81f-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="2c81f-142">Chave de API</span><span class="sxs-lookup"><span data-stu-id="2c81f-142">API Key</span></span> | <span data-ttu-id="2c81f-143">250/hora</span><span class="sxs-lookup"><span data-stu-id="2c81f-143">250 / hour</span></span> | <span data-ttu-id="2c81f-144">Deslistar um pacote NuGet (versão) via ponto de extremidade v2</span><span class="sxs-lookup"><span data-stu-id="2c81f-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 

## <a name="nugetorg-website-page-views"></a><span data-ttu-id="2c81f-145">exibições de página do site nuget.org</span><span class="sxs-lookup"><span data-stu-id="2c81f-145">nuget.org website page views</span></span>

<span data-ttu-id="2c81f-146">Se você estiver acessando as páginas da Web do nuget.org programaticamente, considere a investigação de nossas [APIs v3](overview.md)documentadas.</span><span class="sxs-lookup"><span data-stu-id="2c81f-146">If you are accessing the nuget.org web pages programmatically, consider investigating our documented [V3 APIs](overview.md).</span></span> <span data-ttu-id="2c81f-147">Esses pontos de extremidade permitem um acesso mais simples aos metadados e ao conteúdo do pacote.</span><span class="sxs-lookup"><span data-stu-id="2c81f-147">These endpoints allow for simpler access to package metadata and content.</span></span> <span data-ttu-id="2c81f-148">A API v3 tem melhor disponibilidade e tem um desempenho maior do que acessar as páginas da Web da galeria do NuGet, que são projetadas para interação com o navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="2c81f-148">The V3 API has better availability and has higher performance than accessing the NuGet Gallery web pages, which are designed for web browser interaction.</span></span>

| <span data-ttu-id="2c81f-149">API</span><span class="sxs-lookup"><span data-stu-id="2c81f-149">API</span></span> | <span data-ttu-id="2c81f-150">Tipo de limite</span><span class="sxs-lookup"><span data-stu-id="2c81f-150">Limit Type</span></span> | <span data-ttu-id="2c81f-151">Valor de limite</span><span class="sxs-lookup"><span data-stu-id="2c81f-151">Limit Value</span></span> | <span data-ttu-id="2c81f-152">Caso de uso da API</span><span class="sxs-lookup"><span data-stu-id="2c81f-152">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="2c81f-153">**Obter**`/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="2c81f-153">**GET** `/package/{id}/{version}`</span></span> | <span data-ttu-id="2c81f-154">IP</span><span class="sxs-lookup"><span data-stu-id="2c81f-154">IP</span></span> | <span data-ttu-id="2c81f-155">50/minuto</span><span class="sxs-lookup"><span data-stu-id="2c81f-155">50 / minute</span></span> | <span data-ttu-id="2c81f-156">Página de detalhes do pacote de exibição (versão).</span><span class="sxs-lookup"><span data-stu-id="2c81f-156">Display package (version) details page.</span></span> 
