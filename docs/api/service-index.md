---
title: Índice de serviço, API do NuGet
description: O índice de serviço é o ponto de entrada da API HTTP do NuGet e enumera os recursos do servidor.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775355"
---
# <a name="service-index"></a><span data-ttu-id="0e05e-103">Índice de serviço</span><span class="sxs-lookup"><span data-stu-id="0e05e-103">Service index</span></span>

<span data-ttu-id="0e05e-104">O índice de serviço é um documento JSON que é o ponto de entrada para uma origem de pacote NuGet e permite que uma implementação de cliente descubra os recursos da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="0e05e-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="0e05e-105">O índice de serviço é um objeto JSON com duas propriedades obrigatórias: `version` (a versão do esquema do índice de serviço) e `resources`  (os pontos de extremidade ou as funcionalidades da origem do pacote).</span><span class="sxs-lookup"><span data-stu-id="0e05e-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="0e05e-106">o índice de serviço do NuGet. org está localizado em `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="0e05e-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="0e05e-107">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="0e05e-107">Versioning</span></span>

<span data-ttu-id="0e05e-108">O `version` valor é uma cadeia de caracteres de versão analisável SemVer 2.0.0 que indica a versão do esquema do índice de serviço.</span><span class="sxs-lookup"><span data-stu-id="0e05e-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="0e05e-109">A API determina que a cadeia de caracteres de versão tem um número de versão principal de `3` .</span><span class="sxs-lookup"><span data-stu-id="0e05e-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="0e05e-110">Como alterações não significativas são feitas no esquema de índice de serviço, a versão secundária da cadeia de caracteres de versão será aumentada.</span><span class="sxs-lookup"><span data-stu-id="0e05e-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="0e05e-111">Cada recurso no índice de serviço tem controle de versão independentemente da versão do esquema do índice de serviço.</span><span class="sxs-lookup"><span data-stu-id="0e05e-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="0e05e-112">A versão atual do esquema é `3.0.0` .</span><span class="sxs-lookup"><span data-stu-id="0e05e-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="0e05e-113">A `3.0.0` versão é funcionalmente equivalente à versão mais antiga `3.0.0-beta.1` , mas deve ser preferida, pois ela comunica mais claramente o esquema estável e definido.</span><span class="sxs-lookup"><span data-stu-id="0e05e-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="0e05e-114">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="0e05e-114">HTTP methods</span></span>

<span data-ttu-id="0e05e-115">O índice de serviço pode ser acessado usando métodos HTTP `GET` e `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="0e05e-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="0e05e-116">Recursos</span><span class="sxs-lookup"><span data-stu-id="0e05e-116">Resources</span></span>

<span data-ttu-id="0e05e-117">A `resources` propriedade contém uma matriz de recursos com suporte nesta origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="0e05e-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="0e05e-118">Recurso</span><span class="sxs-lookup"><span data-stu-id="0e05e-118">Resource</span></span>

<span data-ttu-id="0e05e-119">Um recurso é um objeto na `resources` matriz.</span><span class="sxs-lookup"><span data-stu-id="0e05e-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="0e05e-120">Ele representa um recurso com versão de uma origem de pacote.</span><span class="sxs-lookup"><span data-stu-id="0e05e-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="0e05e-121">Um recurso tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="0e05e-121">A resource has the following properties:</span></span>

<span data-ttu-id="0e05e-122">Nome</span><span class="sxs-lookup"><span data-stu-id="0e05e-122">Name</span></span>          | <span data-ttu-id="0e05e-123">Type</span><span class="sxs-lookup"><span data-stu-id="0e05e-123">Type</span></span>   | <span data-ttu-id="0e05e-124">Necessária</span><span class="sxs-lookup"><span data-stu-id="0e05e-124">Required</span></span> | <span data-ttu-id="0e05e-125">Observações</span><span class="sxs-lookup"><span data-stu-id="0e05e-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="0e05e-126">string</span><span class="sxs-lookup"><span data-stu-id="0e05e-126">string</span></span> | <span data-ttu-id="0e05e-127">sim</span><span class="sxs-lookup"><span data-stu-id="0e05e-127">yes</span></span>      | <span data-ttu-id="0e05e-128">A URL para o recurso</span><span class="sxs-lookup"><span data-stu-id="0e05e-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="0e05e-129">string</span><span class="sxs-lookup"><span data-stu-id="0e05e-129">string</span></span> | <span data-ttu-id="0e05e-130">sim</span><span class="sxs-lookup"><span data-stu-id="0e05e-130">yes</span></span>      | <span data-ttu-id="0e05e-131">Uma constante de cadeia de caracteres que representa o tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="0e05e-131">A string constant representing the resource type</span></span>
<span data-ttu-id="0e05e-132">comentário</span><span class="sxs-lookup"><span data-stu-id="0e05e-132">comment</span></span>       | <span data-ttu-id="0e05e-133">string</span><span class="sxs-lookup"><span data-stu-id="0e05e-133">string</span></span> | <span data-ttu-id="0e05e-134">não</span><span class="sxs-lookup"><span data-stu-id="0e05e-134">no</span></span>       | <span data-ttu-id="0e05e-135">Uma descrição legível humana do recurso</span><span class="sxs-lookup"><span data-stu-id="0e05e-135">A human readable description of the resource</span></span>

<span data-ttu-id="0e05e-136">O `@id` é uma URL que deve ser absoluta e deve ter o esquema http ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0e05e-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="0e05e-137">O `@type` é usado para identificar o protocolo específico a ser usado ao interagir com o recurso.</span><span class="sxs-lookup"><span data-stu-id="0e05e-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="0e05e-138">O tipo do recurso é uma cadeia de caracteres opaca, mas geralmente tem o formato:</span><span class="sxs-lookup"><span data-stu-id="0e05e-138">The type of the resource is an opaque string but generally has the format:</span></span>

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

<span data-ttu-id="0e05e-139">Os clientes devem embutir em código os `@type` valores que eles entendem e procurar em um índice de serviço da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="0e05e-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="0e05e-140">Os valores exatos `@type` em uso hoje são enumerados nos documentos de referência de recursos individuais listados na [visão geral da API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="0e05e-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="0e05e-141">Para fins desta documentação, a documentação sobre diferentes recursos será basicamente agrupada pelo `{RESOURCE_NAME}` encontrado no índice de serviço, que é análogo ao agrupamento por cenário.</span><span class="sxs-lookup"><span data-stu-id="0e05e-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="0e05e-142">Não há nenhum requisito para que cada recurso tenha um único `@id` ou `@type` .</span><span class="sxs-lookup"><span data-stu-id="0e05e-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="0e05e-143">Cabe à implementação do cliente determinar qual recurso você prefere sobre outro.</span><span class="sxs-lookup"><span data-stu-id="0e05e-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="0e05e-144">Uma implementação possível é que os recursos do mesmo ou compatíveis `@type` podem ser usados em um modo Round Robin em caso de falha de conexão ou erro de servidor.</span><span class="sxs-lookup"><span data-stu-id="0e05e-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="0e05e-145">Solicitação de exemplo</span><span class="sxs-lookup"><span data-stu-id="0e05e-145">Sample request</span></span>

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a><span data-ttu-id="0e05e-146">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="0e05e-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
