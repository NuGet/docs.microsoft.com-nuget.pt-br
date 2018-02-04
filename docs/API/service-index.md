---
title: "Índice de serviço, o NuGet API | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "O índice de serviço é o ponto de entrada da API de HTTP do NuGet e enumera os recursos do servidor."
keywords: Ponto de entrada de API do NuGet, descoberta de ponto de extremidade NuGetA PI
ms.reviewer:
- karann
- unnir
ms.openlocfilehash: 9d0bb421c163520df4a1f0e9f3f71aab823aace3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="service-index"></a><span data-ttu-id="f6bfd-104">Índice de serviço</span><span class="sxs-lookup"><span data-stu-id="f6bfd-104">Service index</span></span>

<span data-ttu-id="f6bfd-105">O índice de serviço é um documento JSON que é o ponto de entrada para uma origem de pacote do NuGet e permite uma implementação de cliente descobrir os recursos da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="f6bfd-105">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="f6bfd-106">O índice de serviço é um objeto JSON com duas propriedades obrigatórias: `version` (a versão do esquema do índice de serviço) e `resources` (pontos de extremidade ou recursos da origem do pacote).</span><span class="sxs-lookup"><span data-stu-id="f6bfd-106">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="f6bfd-107">índice de serviço do NuGet.org está localizado em `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="f6bfd-107">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="f6bfd-108">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="f6bfd-108">Versioning</span></span>

<span data-ttu-id="f6bfd-109">O `version` valor é uma cadeia de caracteres de versão pode ser analisado SemVer 2.0.0 que indica a versão do esquema do índice de serviço.</span><span class="sxs-lookup"><span data-stu-id="f6bfd-109">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span>
<span data-ttu-id="f6bfd-110">A API exige que a cadeia de caracteres de versão tem um número de versão principal do `3`.</span><span class="sxs-lookup"><span data-stu-id="f6bfd-110">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="f6bfd-111">Como as alterações recentes não são feitas para o esquema de índice de serviço, versão secundária da cadeia de caracteres de versão será aumentado.</span><span class="sxs-lookup"><span data-stu-id="f6bfd-111">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="f6bfd-112">Cada recurso no índice de serviço é com controle de versão independentemente do serviço de versão de esquema de índice.</span><span class="sxs-lookup"><span data-stu-id="f6bfd-112">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="f6bfd-113">A versão atual do esquema é `3.0.0-beta.1`.</span><span class="sxs-lookup"><span data-stu-id="f6bfd-113">The current schema version is `3.0.0-beta.1`.</span></span>

## <a name="http-methods"></a><span data-ttu-id="f6bfd-114">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="f6bfd-114">HTTP methods</span></span>

<span data-ttu-id="f6bfd-115">O índice de serviço está acessível por meio de métodos HTTP `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="f6bfd-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="f6bfd-116">Recursos</span><span class="sxs-lookup"><span data-stu-id="f6bfd-116">Resources</span></span>

<span data-ttu-id="f6bfd-117">O `resources` propriedade contém uma matriz de recursos com suporte por essa origem de pacote.</span><span class="sxs-lookup"><span data-stu-id="f6bfd-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="f6bfd-118">Recurso</span><span class="sxs-lookup"><span data-stu-id="f6bfd-118">Resource</span></span>

<span data-ttu-id="f6bfd-119">Um recurso é um objeto na `resources` matriz.</span><span class="sxs-lookup"><span data-stu-id="f6bfd-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="f6bfd-120">Representa um recurso com versão de uma origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="f6bfd-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="f6bfd-121">Um recurso tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="f6bfd-121">A resource has the following properties:</span></span>

<span data-ttu-id="f6bfd-122">Nome</span><span class="sxs-lookup"><span data-stu-id="f6bfd-122">Name</span></span>          | <span data-ttu-id="f6bfd-123">Tipo</span><span class="sxs-lookup"><span data-stu-id="f6bfd-123">Type</span></span>   | <span data-ttu-id="f6bfd-124">Necessária</span><span class="sxs-lookup"><span data-stu-id="f6bfd-124">Required</span></span> | <span data-ttu-id="f6bfd-125">Observações</span><span class="sxs-lookup"><span data-stu-id="f6bfd-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="f6bfd-126">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f6bfd-126">string</span></span> | <span data-ttu-id="f6bfd-127">sim</span><span class="sxs-lookup"><span data-stu-id="f6bfd-127">yes</span></span>      | <span data-ttu-id="f6bfd-128">A URL para o recurso</span><span class="sxs-lookup"><span data-stu-id="f6bfd-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="f6bfd-129">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f6bfd-129">string</span></span> | <span data-ttu-id="f6bfd-130">sim</span><span class="sxs-lookup"><span data-stu-id="f6bfd-130">yes</span></span>      | <span data-ttu-id="f6bfd-131">Uma constante de cadeia de caracteres que representa o tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="f6bfd-131">A string constant representing the resource type</span></span>
<span data-ttu-id="f6bfd-132">comment</span><span class="sxs-lookup"><span data-stu-id="f6bfd-132">comment</span></span>       | <span data-ttu-id="f6bfd-133">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f6bfd-133">string</span></span> | <span data-ttu-id="f6bfd-134">no</span><span class="sxs-lookup"><span data-stu-id="f6bfd-134">no</span></span>       | <span data-ttu-id="f6bfd-135">Uma descrição legível do recurso</span><span class="sxs-lookup"><span data-stu-id="f6bfd-135">A human readable description of the resource</span></span>

<span data-ttu-id="f6bfd-136">O `@id` é uma URL que deve ser absoluto e deve ter o esquema HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f6bfd-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="f6bfd-137">O `@type` é usado para identificar o protocolo específico a ser usado ao interagir com o recurso.</span><span class="sxs-lookup"><span data-stu-id="f6bfd-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="f6bfd-138">O tipo do recurso é uma cadeia de caracteres opaca mas geralmente tem o formato:</span><span class="sxs-lookup"><span data-stu-id="f6bfd-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="f6bfd-139">Os clientes devem codificar o `@type` valores que compreendem e observá-los no índice de serviço da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="f6bfd-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="f6bfd-140">Exato `@type` valores em uso hoje em dia são enumerados nos documentos de referência de recursos individuais listados no [visão geral da API](overview.md#resources-and-schema).</span><span class="sxs-lookup"><span data-stu-id="f6bfd-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="f6bfd-141">Para manter esta documentação, a documentação sobre recursos diferentes essencialmente será agrupada pelo `{RESOURCE_NAME}` encontrado no índice de serviço que é análogo à agrupamento por cenário.</span><span class="sxs-lookup"><span data-stu-id="f6bfd-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="f6bfd-142">Não há nenhum requisito de que cada recurso tem uma única `@id` ou `@type`.</span><span class="sxs-lookup"><span data-stu-id="f6bfd-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="f6bfd-143">Cabe a implementação do cliente para determinar qual recurso preferir em detrimento de outro.</span><span class="sxs-lookup"><span data-stu-id="f6bfd-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="f6bfd-144">Uma possível implementação é que recursos de idênticos ou compatíveis `@type` pode ser usado em um modo round robin no caso de erro de servidor ou de falha de conexão.</span><span class="sxs-lookup"><span data-stu-id="f6bfd-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="f6bfd-145">Solicitação de amostra</span><span class="sxs-lookup"><span data-stu-id="f6bfd-145">Sample request</span></span>

<span data-ttu-id="f6bfd-146">OBTER https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="f6bfd-146">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="f6bfd-147">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="f6bfd-147">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
