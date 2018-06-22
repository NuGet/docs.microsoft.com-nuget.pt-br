---
title: Conteúdo do pacote, o NuGet API
description: O endereço base do pacote é uma interface simples para buscar o pacote propriamente dito.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a6ac40368f30d33f35d4ca0b6cc18ce4bd6efee5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819171"
---
# <a name="package-content"></a><span data-ttu-id="59f70-103">Conteúdo do pacote</span><span class="sxs-lookup"><span data-stu-id="59f70-103">Package Content</span></span>

<span data-ttu-id="59f70-104">É possível gerar uma URL para buscar o conteúdo de um pacote arbitrário (o arquivo. nupkg) usando a API V3.</span><span class="sxs-lookup"><span data-stu-id="59f70-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="59f70-105">O recurso usado para buscar o conteúdo do pacote é o `PackageBaseAddress` recurso encontrado na [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="59f70-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="59f70-106">Esse recurso também permite a descoberta de todas as versões de um pacote, listados ou não listadas.</span><span class="sxs-lookup"><span data-stu-id="59f70-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="59f70-107">Este recurso é conhecido como um "pacote base endereço" ou "contêiner simples".</span><span class="sxs-lookup"><span data-stu-id="59f70-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="59f70-108">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="59f70-108">Versioning</span></span>

<span data-ttu-id="59f70-109">O seguinte `@type` valor é usado:</span><span class="sxs-lookup"><span data-stu-id="59f70-109">The following `@type` value is used:</span></span>

<span data-ttu-id="59f70-110">Valor @type</span><span class="sxs-lookup"><span data-stu-id="59f70-110">@type value</span></span>              | <span data-ttu-id="59f70-111">Observações</span><span class="sxs-lookup"><span data-stu-id="59f70-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="59f70-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="59f70-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="59f70-113">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="59f70-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="59f70-114">URL Base</span><span class="sxs-lookup"><span data-stu-id="59f70-114">Base URL</span></span>

<span data-ttu-id="59f70-115">A URL base para as seguintes APIs é o valor da `@id` propriedade associada com o recurso mencionados acima `@type` valor.</span><span class="sxs-lookup"><span data-stu-id="59f70-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="59f70-116">No documento a seguir, a URL base do espaço reservado `{@id}` será usado.</span><span class="sxs-lookup"><span data-stu-id="59f70-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="59f70-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="59f70-117">HTTP methods</span></span>

<span data-ttu-id="59f70-118">Todas as URLs encontradas no suporte a recurso de registro os métodos HTTP `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="59f70-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="59f70-119">Enumerar as versões do pacote</span><span class="sxs-lookup"><span data-stu-id="59f70-119">Enumerate package versions</span></span>

<span data-ttu-id="59f70-120">Se o cliente sabe uma ID de pacote e quer descobrir quais versões do pacote do pacote de origem tem disponível, o cliente pode construir uma URL previsível para enumerar todas as versões do pacote.</span><span class="sxs-lookup"><span data-stu-id="59f70-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="59f70-121">Essa lista deve ser uma "listagem de diretório" para a API de conteúdo do pacote mencionada abaixo.</span><span class="sxs-lookup"><span data-stu-id="59f70-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="59f70-122">Essa lista contém as duas versões do pacote listados e não listados.</span><span class="sxs-lookup"><span data-stu-id="59f70-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="59f70-123">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="59f70-123">Request parameters</span></span>

<span data-ttu-id="59f70-124">Nome</span><span class="sxs-lookup"><span data-stu-id="59f70-124">Name</span></span>     | <span data-ttu-id="59f70-125">No</span><span class="sxs-lookup"><span data-stu-id="59f70-125">In</span></span>     | <span data-ttu-id="59f70-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="59f70-126">Type</span></span>    | <span data-ttu-id="59f70-127">Necessária</span><span class="sxs-lookup"><span data-stu-id="59f70-127">Required</span></span> | <span data-ttu-id="59f70-128">Observações</span><span class="sxs-lookup"><span data-stu-id="59f70-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="59f70-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="59f70-129">LOWER_ID</span></span> | <span data-ttu-id="59f70-130">URL</span><span class="sxs-lookup"><span data-stu-id="59f70-130">URL</span></span>    | <span data-ttu-id="59f70-131">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="59f70-131">string</span></span>  | <span data-ttu-id="59f70-132">sim</span><span class="sxs-lookup"><span data-stu-id="59f70-132">yes</span></span>      | <span data-ttu-id="59f70-133">A ID do pacote, letras minúsculas</span><span class="sxs-lookup"><span data-stu-id="59f70-133">The package ID, lowercase</span></span>

<span data-ttu-id="59f70-134">O `LOWER_ID` valor é a ID do pacote desejado em minúscula usando as regras implementadas pelo. Do NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.</span><span class="sxs-lookup"><span data-stu-id="59f70-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="59f70-135">Resposta</span><span class="sxs-lookup"><span data-stu-id="59f70-135">Response</span></span>

<span data-ttu-id="59f70-136">Se a origem do pacote não tem nenhuma versão da ID do pacote fornecido, um código de 404 status será retornado.</span><span class="sxs-lookup"><span data-stu-id="59f70-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="59f70-137">Se a origem do pacote tem uma ou mais versões, um código de 200 status será retornado.</span><span class="sxs-lookup"><span data-stu-id="59f70-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="59f70-138">O corpo da resposta é um objeto JSON com a seguinte propriedade:</span><span class="sxs-lookup"><span data-stu-id="59f70-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="59f70-139">Nome</span><span class="sxs-lookup"><span data-stu-id="59f70-139">Name</span></span>     | <span data-ttu-id="59f70-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="59f70-140">Type</span></span>             | <span data-ttu-id="59f70-141">Necessária</span><span class="sxs-lookup"><span data-stu-id="59f70-141">Required</span></span> | <span data-ttu-id="59f70-142">Observações</span><span class="sxs-lookup"><span data-stu-id="59f70-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="59f70-143">versões</span><span class="sxs-lookup"><span data-stu-id="59f70-143">versions</span></span> | <span data-ttu-id="59f70-144">Matriz de cadeias de caracteres</span><span class="sxs-lookup"><span data-stu-id="59f70-144">array of strings</span></span> | <span data-ttu-id="59f70-145">sim</span><span class="sxs-lookup"><span data-stu-id="59f70-145">yes</span></span>      | <span data-ttu-id="59f70-146">O pacote IDs disponíveis</span><span class="sxs-lookup"><span data-stu-id="59f70-146">The package IDs available</span></span>

<span data-ttu-id="59f70-147">As cadeias de caracteres no `versions` matriz estão todos em minúscula, [normalizado cadeias de caracteres de versão NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="59f70-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="59f70-148">As cadeias de caracteres de versão não contém metadados de compilação SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="59f70-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="59f70-149">A intenção é que as cadeias de caracteres de versão encontradas nesta matriz podem ser usadas textualmente para o `LOWER_VERSION` tokens encontrado nos seguintes pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="59f70-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="59f70-150">Solicitação de amostra</span><span class="sxs-lookup"><span data-stu-id="59f70-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="59f70-151">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="59f70-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="59f70-152">Baixar o conteúdo do pacote (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="59f70-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="59f70-153">Se o cliente sabe um ID de pacote e a versão e deseja baixar o conteúdo do pacote, eles só precisam construir a URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="59f70-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="59f70-154">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="59f70-154">Request parameters</span></span>

<span data-ttu-id="59f70-155">Nome</span><span class="sxs-lookup"><span data-stu-id="59f70-155">Name</span></span>          | <span data-ttu-id="59f70-156">No</span><span class="sxs-lookup"><span data-stu-id="59f70-156">In</span></span>     | <span data-ttu-id="59f70-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="59f70-157">Type</span></span>   | <span data-ttu-id="59f70-158">Necessária</span><span class="sxs-lookup"><span data-stu-id="59f70-158">Required</span></span> | <span data-ttu-id="59f70-159">Observações</span><span class="sxs-lookup"><span data-stu-id="59f70-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="59f70-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="59f70-160">LOWER_ID</span></span>      | <span data-ttu-id="59f70-161">URL</span><span class="sxs-lookup"><span data-stu-id="59f70-161">URL</span></span>    | <span data-ttu-id="59f70-162">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="59f70-162">string</span></span> | <span data-ttu-id="59f70-163">sim</span><span class="sxs-lookup"><span data-stu-id="59f70-163">yes</span></span>      | <span data-ttu-id="59f70-164">A ID do pacote, letras minúsculas</span><span class="sxs-lookup"><span data-stu-id="59f70-164">The package ID, lowercase</span></span>
<span data-ttu-id="59f70-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="59f70-165">LOWER_VERSION</span></span> | <span data-ttu-id="59f70-166">URL</span><span class="sxs-lookup"><span data-stu-id="59f70-166">URL</span></span>    | <span data-ttu-id="59f70-167">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="59f70-167">string</span></span> | <span data-ttu-id="59f70-168">sim</span><span class="sxs-lookup"><span data-stu-id="59f70-168">yes</span></span>      | <span data-ttu-id="59f70-169">A versão do pacote, padronizado e minúscula</span><span class="sxs-lookup"><span data-stu-id="59f70-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="59f70-170">Ambos `LOWER_ID` e `LOWER_VERSION` em minúscula usando as regras implementadas pelo. Do NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.</span><span class="sxs-lookup"><span data-stu-id="59f70-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="59f70-171">O `LOWER_VERSION` é a versão do pacote desejado normalizado de acordo com a versão do NuGet [as regras de normalização](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="59f70-171">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="59f70-172">Isso significa que os metadados de compilação que é permitido pela especificação SemVer 2.0.0 devem ser excluídos nesse caso.</span><span class="sxs-lookup"><span data-stu-id="59f70-172">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="59f70-173">Corpo da resposta</span><span class="sxs-lookup"><span data-stu-id="59f70-173">Response body</span></span>

<span data-ttu-id="59f70-174">Se o pacote existe na origem do pacote, um código de 200 status será retornado.</span><span class="sxs-lookup"><span data-stu-id="59f70-174">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="59f70-175">O corpo da resposta será o conteúdo do pacote.</span><span class="sxs-lookup"><span data-stu-id="59f70-175">The response body will be the package content itself.</span></span>

<span data-ttu-id="59f70-176">Se o pacote não existe na origem do pacote, um código de 404 status será retornado.</span><span class="sxs-lookup"><span data-stu-id="59f70-176">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="59f70-177">Solicitação de amostra</span><span class="sxs-lookup"><span data-stu-id="59f70-177">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="59f70-178">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="59f70-178">Sample response</span></span>

<span data-ttu-id="59f70-179">O fluxo binário é nupkg para newtonsoft 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="59f70-179">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="59f70-180">Baixe o manifesto de pacote (. NuSpec)</span><span class="sxs-lookup"><span data-stu-id="59f70-180">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="59f70-181">Se o cliente sabe um ID de pacote e a versão e deseja baixar o manifesto de pacote, eles só precisam construir a URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="59f70-181">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="59f70-182">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="59f70-182">Request parameters</span></span>

<span data-ttu-id="59f70-183">Nome</span><span class="sxs-lookup"><span data-stu-id="59f70-183">Name</span></span>          | <span data-ttu-id="59f70-184">No</span><span class="sxs-lookup"><span data-stu-id="59f70-184">In</span></span>     | <span data-ttu-id="59f70-185">Tipo</span><span class="sxs-lookup"><span data-stu-id="59f70-185">Type</span></span>    | <span data-ttu-id="59f70-186">Necessária</span><span class="sxs-lookup"><span data-stu-id="59f70-186">Required</span></span> | <span data-ttu-id="59f70-187">Observações</span><span class="sxs-lookup"><span data-stu-id="59f70-187">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="59f70-188">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="59f70-188">LOWER_ID</span></span>      | <span data-ttu-id="59f70-189">URL</span><span class="sxs-lookup"><span data-stu-id="59f70-189">URL</span></span>    | <span data-ttu-id="59f70-190">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="59f70-190">string</span></span>  | <span data-ttu-id="59f70-191">sim</span><span class="sxs-lookup"><span data-stu-id="59f70-191">yes</span></span>      | <span data-ttu-id="59f70-192">A ID do pacote, letras minúsculas</span><span class="sxs-lookup"><span data-stu-id="59f70-192">The package ID, lowercase</span></span>
<span data-ttu-id="59f70-193">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="59f70-193">LOWER_VERSION</span></span> | <span data-ttu-id="59f70-194">URL</span><span class="sxs-lookup"><span data-stu-id="59f70-194">URL</span></span>    | <span data-ttu-id="59f70-195">inteiro</span><span class="sxs-lookup"><span data-stu-id="59f70-195">integer</span></span> | <span data-ttu-id="59f70-196">sim</span><span class="sxs-lookup"><span data-stu-id="59f70-196">yes</span></span>      | <span data-ttu-id="59f70-197">A versão do pacote, padronizado e minúscula</span><span class="sxs-lookup"><span data-stu-id="59f70-197">The package version, normalized and lowercased</span></span>

<span data-ttu-id="59f70-198">Ambos `LOWER_ID` e `LOWER_VERSION` em minúscula usando as regras implementadas pelo. Do NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.</span><span class="sxs-lookup"><span data-stu-id="59f70-198">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="59f70-199">O `LOWER_VERSION` é a versão do pacote desejado normalizado de acordo com a versão do NuGet [as regras de normalização](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="59f70-199">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="59f70-200">Isso significa que os metadados de compilação que é permitido pela especificação SemVer 2.0.0 devem ser excluídos nesse caso.</span><span class="sxs-lookup"><span data-stu-id="59f70-200">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="59f70-201">Corpo da resposta</span><span class="sxs-lookup"><span data-stu-id="59f70-201">Response body</span></span>

<span data-ttu-id="59f70-202">Se o pacote existe na origem do pacote, um código de 200 status será retornado.</span><span class="sxs-lookup"><span data-stu-id="59f70-202">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="59f70-203">O corpo da resposta será o manifesto de pacote, que é o. NuSpec contidas o nupkg correspondente.</span><span class="sxs-lookup"><span data-stu-id="59f70-203">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="59f70-204">A. NuSpec é um documento XML.</span><span class="sxs-lookup"><span data-stu-id="59f70-204">The .nuspec is an XML document.</span></span>

<span data-ttu-id="59f70-205">Se o pacote não existe na origem do pacote, um código de 404 status será retornado.</span><span class="sxs-lookup"><span data-stu-id="59f70-205">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="59f70-206">Solicitação de amostra</span><span class="sxs-lookup"><span data-stu-id="59f70-206">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="59f70-207">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="59f70-207">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
