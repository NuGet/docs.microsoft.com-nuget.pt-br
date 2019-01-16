---
title: Índice de serviço, API do NuGet
description: O índice de serviço é o ponto de entrada da API de HTTP do NuGet e enumera os recursos do servidor.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1dcfb87690b728280b494d4434f9c1d7ee7a7e74
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324715"
---
# <a name="service-index"></a><span data-ttu-id="f1b54-103">Índice de serviço</span><span class="sxs-lookup"><span data-stu-id="f1b54-103">Service index</span></span>

<span data-ttu-id="f1b54-104">O índice de serviço é um documento JSON que é o ponto de entrada para uma origem de pacote do NuGet e permite que uma implementação de cliente descobrir os recursos da fonte de pacote.</span><span class="sxs-lookup"><span data-stu-id="f1b54-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="f1b54-105">O índice de serviço é um objeto JSON com duas propriedades obrigatórias: `version` (a versão do esquema do índice de serviço) e `resources` (pontos de extremidade ou recursos da origem do pacote).</span><span class="sxs-lookup"><span data-stu-id="f1b54-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="f1b54-106">índice de serviço do NuGet.org está localizado em `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="f1b54-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="f1b54-107">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="f1b54-107">Versioning</span></span>

<span data-ttu-id="f1b54-108">O `version` valor é uma cadeia de caracteres de versão pode ser analisado SemVer 2.0.0 que indica a versão do esquema do índice de serviço.</span><span class="sxs-lookup"><span data-stu-id="f1b54-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="f1b54-109">A API exige que a cadeia de caracteres de versão tem um número de versão principal `3`.</span><span class="sxs-lookup"><span data-stu-id="f1b54-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="f1b54-110">Como o esquema de índice de serviço forem feitas alterações sem interrupções, versão secundária da cadeia de caracteres de versão será aumentado.</span><span class="sxs-lookup"><span data-stu-id="f1b54-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="f1b54-111">Cada recurso no índice de serviço tem controle de versão independentemente do serviço de versão de esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="f1b54-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="f1b54-112">A versão atual do esquema é `3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="f1b54-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="f1b54-113">O `3.0.0` versão é funcionalmente equivalente à antiga `3.0.0-beta.1` versão, mas deve ser preferencial, pois ele se comunica mais claramente o esquema estável, definido.</span><span class="sxs-lookup"><span data-stu-id="f1b54-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="f1b54-114">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="f1b54-114">HTTP methods</span></span>

<span data-ttu-id="f1b54-115">O índice de serviço é acessível por meio de métodos HTTP `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="f1b54-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="f1b54-116">Recursos</span><span class="sxs-lookup"><span data-stu-id="f1b54-116">Resources</span></span>

<span data-ttu-id="f1b54-117">O `resources` propriedade contém uma matriz de recursos com suporte desta origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="f1b54-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="f1b54-118">Recurso</span><span class="sxs-lookup"><span data-stu-id="f1b54-118">Resource</span></span>

<span data-ttu-id="f1b54-119">Um recurso é um objeto no `resources` matriz.</span><span class="sxs-lookup"><span data-stu-id="f1b54-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="f1b54-120">Representa um recurso de controle de versão de uma origem de pacote.</span><span class="sxs-lookup"><span data-stu-id="f1b54-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="f1b54-121">Um recurso tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="f1b54-121">A resource has the following properties:</span></span>

<span data-ttu-id="f1b54-122">Nome</span><span class="sxs-lookup"><span data-stu-id="f1b54-122">Name</span></span>          | <span data-ttu-id="f1b54-123">Tipo</span><span class="sxs-lookup"><span data-stu-id="f1b54-123">Type</span></span>   | <span data-ttu-id="f1b54-124">Necessária</span><span class="sxs-lookup"><span data-stu-id="f1b54-124">Required</span></span> | <span data-ttu-id="f1b54-125">Observações</span><span class="sxs-lookup"><span data-stu-id="f1b54-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="f1b54-126">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f1b54-126">string</span></span> | <span data-ttu-id="f1b54-127">sim</span><span class="sxs-lookup"><span data-stu-id="f1b54-127">yes</span></span>      | <span data-ttu-id="f1b54-128">A URL para o recurso</span><span class="sxs-lookup"><span data-stu-id="f1b54-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="f1b54-129">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f1b54-129">string</span></span> | <span data-ttu-id="f1b54-130">sim</span><span class="sxs-lookup"><span data-stu-id="f1b54-130">yes</span></span>      | <span data-ttu-id="f1b54-131">Uma constante de cadeia de caracteres que representa o tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="f1b54-131">A string constant representing the resource type</span></span>
<span data-ttu-id="f1b54-132">comment</span><span class="sxs-lookup"><span data-stu-id="f1b54-132">comment</span></span>       | <span data-ttu-id="f1b54-133">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f1b54-133">string</span></span> | <span data-ttu-id="f1b54-134">no</span><span class="sxs-lookup"><span data-stu-id="f1b54-134">no</span></span>       | <span data-ttu-id="f1b54-135">Uma descrição legível do recurso</span><span class="sxs-lookup"><span data-stu-id="f1b54-135">A human readable description of the resource</span></span>

<span data-ttu-id="f1b54-136">O `@id` é uma URL que deve ser absoluto e deve ter o esquema HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f1b54-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="f1b54-137">O `@type` é usado para identificar o protocolo específico a ser usado ao interagir com o recurso.</span><span class="sxs-lookup"><span data-stu-id="f1b54-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="f1b54-138">O tipo do recurso é uma cadeia de caracteres opaca, mas geralmente tem o formato:</span><span class="sxs-lookup"><span data-stu-id="f1b54-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="f1b54-139">Os clientes devem codificar o `@type` valores que compreendem e pesquisar no índice de serviço da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="f1b54-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="f1b54-140">Exatamente `@type` valores em uso atualmente são enumerados sobre os documentos de referência de recursos individuais listados na [visão geral da API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="f1b54-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="f1b54-141">Para fins desta documentação, a documentação sobre recursos diferentes, essencialmente, será agrupada pelo `{RESOURCE_NAME}` encontrado no índice de serviço que é análogo ao agrupamento por cenário.</span><span class="sxs-lookup"><span data-stu-id="f1b54-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="f1b54-142">Não há nenhum requisito de que cada recurso tem um único `@id` ou `@type`.</span><span class="sxs-lookup"><span data-stu-id="f1b54-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="f1b54-143">Cabe a implementação do cliente para determinar qual recurso para dar preferência em relação a outra.</span><span class="sxs-lookup"><span data-stu-id="f1b54-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="f1b54-144">Uma possível implementação é que os recursos da mesma ou compatível `@type` podem ser usados em um estilo round-robin em caso de erro de servidor ou de falha de conexão.</span><span class="sxs-lookup"><span data-stu-id="f1b54-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="f1b54-145">Exemplo de solicitação</span><span class="sxs-lookup"><span data-stu-id="f1b54-145">Sample request</span></span>

    GET https://api.nuget.org/v3/index.json

### <a name="sample-response"></a><span data-ttu-id="f1b54-146">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="f1b54-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
