---
title: Índice de serviço, o NuGet API
description: O índice de serviço é o ponto de entrada da API de HTTP do NuGet e enumera os recursos do servidor.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 84e623e8480e4d17edad2ec3b2da6dcb6e53d21b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822088"
---
# <a name="service-index"></a><span data-ttu-id="0f952-103">Índice de serviço</span><span class="sxs-lookup"><span data-stu-id="0f952-103">Service index</span></span>

<span data-ttu-id="0f952-104">O índice de serviço é um documento JSON que é o ponto de entrada para uma origem de pacote do NuGet e permite uma implementação de cliente descobrir os recursos da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="0f952-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="0f952-105">O índice de serviço é um objeto JSON com duas propriedades obrigatórias: `version` (a versão do esquema do índice de serviço) e `resources` (pontos de extremidade ou recursos da origem do pacote).</span><span class="sxs-lookup"><span data-stu-id="0f952-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="0f952-106">índice de serviço do NuGet.org está localizado em `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="0f952-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="0f952-107">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="0f952-107">Versioning</span></span>

<span data-ttu-id="0f952-108">O `version` valor é uma cadeia de caracteres de versão pode ser analisado SemVer 2.0.0 que indica a versão do esquema do índice de serviço.</span><span class="sxs-lookup"><span data-stu-id="0f952-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="0f952-109">A API exige que a cadeia de caracteres de versão tem um número de versão principal do `3`.</span><span class="sxs-lookup"><span data-stu-id="0f952-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="0f952-110">Como as alterações recentes não são feitas para o esquema de índice de serviço, versão secundária da cadeia de caracteres de versão será aumentado.</span><span class="sxs-lookup"><span data-stu-id="0f952-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="0f952-111">Cada recurso no índice de serviço é com controle de versão independentemente do serviço de versão de esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="0f952-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="0f952-112">A versão atual do esquema é `3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="0f952-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="0f952-113">O `3.0.0` versão é funcionalmente equivalente à antigos `3.0.0-beta.1` versão mas deve ser preferencial porque ele se comunica mais claramente o esquema estável, definido.</span><span class="sxs-lookup"><span data-stu-id="0f952-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="0f952-114">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="0f952-114">HTTP methods</span></span>

<span data-ttu-id="0f952-115">O índice de serviço está acessível por meio de métodos HTTP `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="0f952-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="0f952-116">Recursos</span><span class="sxs-lookup"><span data-stu-id="0f952-116">Resources</span></span>

<span data-ttu-id="0f952-117">O `resources` propriedade contém uma matriz de recursos com suporte por essa origem de pacote.</span><span class="sxs-lookup"><span data-stu-id="0f952-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="0f952-118">Recurso</span><span class="sxs-lookup"><span data-stu-id="0f952-118">Resource</span></span>

<span data-ttu-id="0f952-119">Um recurso é um objeto na `resources` matriz.</span><span class="sxs-lookup"><span data-stu-id="0f952-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="0f952-120">Representa um recurso com versão de uma origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="0f952-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="0f952-121">Um recurso tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="0f952-121">A resource has the following properties:</span></span>

<span data-ttu-id="0f952-122">Nome</span><span class="sxs-lookup"><span data-stu-id="0f952-122">Name</span></span>          | <span data-ttu-id="0f952-123">Tipo</span><span class="sxs-lookup"><span data-stu-id="0f952-123">Type</span></span>   | <span data-ttu-id="0f952-124">Necessária</span><span class="sxs-lookup"><span data-stu-id="0f952-124">Required</span></span> | <span data-ttu-id="0f952-125">Observações</span><span class="sxs-lookup"><span data-stu-id="0f952-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="0f952-126">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0f952-126">string</span></span> | <span data-ttu-id="0f952-127">sim</span><span class="sxs-lookup"><span data-stu-id="0f952-127">yes</span></span>      | <span data-ttu-id="0f952-128">A URL para o recurso</span><span class="sxs-lookup"><span data-stu-id="0f952-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="0f952-129">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0f952-129">string</span></span> | <span data-ttu-id="0f952-130">sim</span><span class="sxs-lookup"><span data-stu-id="0f952-130">yes</span></span>      | <span data-ttu-id="0f952-131">Uma constante de cadeia de caracteres que representa o tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="0f952-131">A string constant representing the resource type</span></span>
<span data-ttu-id="0f952-132">comment</span><span class="sxs-lookup"><span data-stu-id="0f952-132">comment</span></span>       | <span data-ttu-id="0f952-133">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0f952-133">string</span></span> | <span data-ttu-id="0f952-134">no</span><span class="sxs-lookup"><span data-stu-id="0f952-134">no</span></span>       | <span data-ttu-id="0f952-135">Uma descrição legível do recurso</span><span class="sxs-lookup"><span data-stu-id="0f952-135">A human readable description of the resource</span></span>

<span data-ttu-id="0f952-136">O `@id` é uma URL que deve ser absoluto e deve ter o esquema HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0f952-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="0f952-137">O `@type` é usado para identificar o protocolo específico a ser usado ao interagir com o recurso.</span><span class="sxs-lookup"><span data-stu-id="0f952-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="0f952-138">O tipo do recurso é uma cadeia de caracteres opaca mas geralmente tem o formato:</span><span class="sxs-lookup"><span data-stu-id="0f952-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="0f952-139">Os clientes devem codificar o `@type` valores que compreendem e observá-los no índice de serviço da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="0f952-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="0f952-140">Exato `@type` valores em uso hoje em dia são enumerados nos documentos de referência de recursos individuais listados no [visão geral da API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="0f952-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="0f952-141">Para manter esta documentação, a documentação sobre recursos diferentes essencialmente será agrupada pelo `{RESOURCE_NAME}` encontrado no índice de serviço que é análogo à agrupamento por cenário.</span><span class="sxs-lookup"><span data-stu-id="0f952-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="0f952-142">Não há nenhum requisito de que cada recurso tem uma única `@id` ou `@type`.</span><span class="sxs-lookup"><span data-stu-id="0f952-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="0f952-143">Cabe a implementação do cliente para determinar qual recurso preferir em detrimento de outro.</span><span class="sxs-lookup"><span data-stu-id="0f952-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="0f952-144">Uma possível implementação é que recursos de idênticos ou compatíveis `@type` pode ser usado em um modo round robin no caso de erro de servidor ou de falha de conexão.</span><span class="sxs-lookup"><span data-stu-id="0f952-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="0f952-145">Solicitação de amostra</span><span class="sxs-lookup"><span data-stu-id="0f952-145">Sample request</span></span>

<span data-ttu-id="0f952-146">OBTER https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="0f952-146">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="0f952-147">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="0f952-147">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
