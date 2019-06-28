---
title: Conteúdo do pacote, API do NuGet
description: O endereço base do pacote é uma interface simple para buscar o pacote propriamente dito.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2f0f93e0cee78ea03cbd53194cdc2a10871fd7e1
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426759"
---
# <a name="package-content"></a><span data-ttu-id="11ab9-103">Conteúdo do pacote</span><span class="sxs-lookup"><span data-stu-id="11ab9-103">Package Content</span></span>

<span data-ttu-id="11ab9-104">É possível gerar uma URL para buscar o conteúdo de um pacote arbitrários (o arquivo. nupkg) usando a API V3.</span><span class="sxs-lookup"><span data-stu-id="11ab9-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="11ab9-105">O recurso usado para buscar o conteúdo do pacote é o `PackageBaseAddress` recurso encontrado na [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="11ab9-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="11ab9-106">Esse recurso também permite a descoberta de todas as versões de um pacote, listados ou não listado.</span><span class="sxs-lookup"><span data-stu-id="11ab9-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="11ab9-107">Esse recurso é conhecido como o o "pacote endereço básico" ou "contêiner simples".</span><span class="sxs-lookup"><span data-stu-id="11ab9-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="11ab9-108">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="11ab9-108">Versioning</span></span>

<span data-ttu-id="11ab9-109">O seguinte `@type` valor é usado:</span><span class="sxs-lookup"><span data-stu-id="11ab9-109">The following `@type` value is used:</span></span>

<span data-ttu-id="11ab9-110">Valor @type</span><span class="sxs-lookup"><span data-stu-id="11ab9-110">@type value</span></span>              | <span data-ttu-id="11ab9-111">Observações</span><span class="sxs-lookup"><span data-stu-id="11ab9-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="11ab9-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="11ab9-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="11ab9-113">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="11ab9-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="11ab9-114">URL Base</span><span class="sxs-lookup"><span data-stu-id="11ab9-114">Base URL</span></span>

<span data-ttu-id="11ab9-115">A URL base para as APIs a seguir é o valor da `@id` propriedade associada ao recurso mencionados anteriormente `@type` valor.</span><span class="sxs-lookup"><span data-stu-id="11ab9-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="11ab9-116">O seguinte documento, o espaço reservado de URL de base `{@id}` será usado.</span><span class="sxs-lookup"><span data-stu-id="11ab9-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="11ab9-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="11ab9-117">HTTP methods</span></span>

<span data-ttu-id="11ab9-118">Todas as URLs encontradas no suporte a recursos de registro os métodos HTTP `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="11ab9-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="11ab9-119">Enumerar as versões do pacote</span><span class="sxs-lookup"><span data-stu-id="11ab9-119">Enumerate package versions</span></span>

<span data-ttu-id="11ab9-120">Se o cliente sabe que uma ID de pacote e quer descobrir quais versões do pacote o pacote de origem tem disponível, o cliente pode construir uma URL previsível para enumerar todas as versões do pacote.</span><span class="sxs-lookup"><span data-stu-id="11ab9-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="11ab9-121">Essa lista deve ser uma "listagem de diretório" para a API de conteúdo do pacote mencionada a seguir.</span><span class="sxs-lookup"><span data-stu-id="11ab9-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="11ab9-122">Esta lista contém ambas as versões de pacote listadas e removido da lista.</span><span class="sxs-lookup"><span data-stu-id="11ab9-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="11ab9-123">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="11ab9-123">Request parameters</span></span>

<span data-ttu-id="11ab9-124">Nome</span><span class="sxs-lookup"><span data-stu-id="11ab9-124">Name</span></span>     | <span data-ttu-id="11ab9-125">No</span><span class="sxs-lookup"><span data-stu-id="11ab9-125">In</span></span>     | <span data-ttu-id="11ab9-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="11ab9-126">Type</span></span>    | <span data-ttu-id="11ab9-127">Necessária</span><span class="sxs-lookup"><span data-stu-id="11ab9-127">Required</span></span> | <span data-ttu-id="11ab9-128">Observações</span><span class="sxs-lookup"><span data-stu-id="11ab9-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="11ab9-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="11ab9-129">LOWER_ID</span></span> | <span data-ttu-id="11ab9-130">URL</span><span class="sxs-lookup"><span data-stu-id="11ab9-130">URL</span></span>    | <span data-ttu-id="11ab9-131">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="11ab9-131">string</span></span>  | <span data-ttu-id="11ab9-132">sim</span><span class="sxs-lookup"><span data-stu-id="11ab9-132">yes</span></span>      | <span data-ttu-id="11ab9-133">A ID do pacote, em minúsculas</span><span class="sxs-lookup"><span data-stu-id="11ab9-133">The package ID, lowercase</span></span>

<span data-ttu-id="11ab9-134">O `LOWER_ID` valor é a ID do pacote desejado em minúscula usando as regras implementadas pelo. Do NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.</span><span class="sxs-lookup"><span data-stu-id="11ab9-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="11ab9-135">Resposta</span><span class="sxs-lookup"><span data-stu-id="11ab9-135">Response</span></span>

<span data-ttu-id="11ab9-136">Se a origem do pacote não tiver nenhuma versão da ID do pacote fornecido, um código de 404 status será retornado.</span><span class="sxs-lookup"><span data-stu-id="11ab9-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="11ab9-137">Se a origem do pacote tem uma ou mais versões, um código de 200 status será retornado.</span><span class="sxs-lookup"><span data-stu-id="11ab9-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="11ab9-138">O corpo da resposta é um objeto JSON com a seguinte propriedade:</span><span class="sxs-lookup"><span data-stu-id="11ab9-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="11ab9-139">Nome</span><span class="sxs-lookup"><span data-stu-id="11ab9-139">Name</span></span>     | <span data-ttu-id="11ab9-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="11ab9-140">Type</span></span>             | <span data-ttu-id="11ab9-141">Necessária</span><span class="sxs-lookup"><span data-stu-id="11ab9-141">Required</span></span> | <span data-ttu-id="11ab9-142">Observações</span><span class="sxs-lookup"><span data-stu-id="11ab9-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="11ab9-143">versões</span><span class="sxs-lookup"><span data-stu-id="11ab9-143">versions</span></span> | <span data-ttu-id="11ab9-144">matriz de cadeias de caracteres</span><span class="sxs-lookup"><span data-stu-id="11ab9-144">array of strings</span></span> | <span data-ttu-id="11ab9-145">sim</span><span class="sxs-lookup"><span data-stu-id="11ab9-145">yes</span></span>      | <span data-ttu-id="11ab9-146">O pacote IDs disponíveis</span><span class="sxs-lookup"><span data-stu-id="11ab9-146">The package IDs available</span></span>

<span data-ttu-id="11ab9-147">Cadeias de caracteres a `versions` matriz estão todos em minúscula, [normalizados cadeias de caracteres de versão NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="11ab9-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="11ab9-148">As cadeias de caracteres de versão contém os metadados de compilação de SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="11ab9-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="11ab9-149">A intenção é que as cadeias de caracteres de versão encontradas nesta matriz podem ser usadas textual para o `LOWER_VERSION` tokens encontrados nos seguintes pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="11ab9-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="11ab9-150">Exemplo de solicitação</span><span class="sxs-lookup"><span data-stu-id="11ab9-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="11ab9-151">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="11ab9-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="11ab9-152">Baixar conteúdo do pacote (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="11ab9-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="11ab9-153">Se o cliente sabe que uma ID de pacote e a versão e quiser baixar o conteúdo do pacote, precisará apenas construir a URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="11ab9-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="11ab9-154">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="11ab9-154">Request parameters</span></span>

<span data-ttu-id="11ab9-155">Nome</span><span class="sxs-lookup"><span data-stu-id="11ab9-155">Name</span></span>          | <span data-ttu-id="11ab9-156">No</span><span class="sxs-lookup"><span data-stu-id="11ab9-156">In</span></span>     | <span data-ttu-id="11ab9-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="11ab9-157">Type</span></span>   | <span data-ttu-id="11ab9-158">Necessária</span><span class="sxs-lookup"><span data-stu-id="11ab9-158">Required</span></span> | <span data-ttu-id="11ab9-159">Observações</span><span class="sxs-lookup"><span data-stu-id="11ab9-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="11ab9-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="11ab9-160">LOWER_ID</span></span>      | <span data-ttu-id="11ab9-161">URL</span><span class="sxs-lookup"><span data-stu-id="11ab9-161">URL</span></span>    | <span data-ttu-id="11ab9-162">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="11ab9-162">string</span></span> | <span data-ttu-id="11ab9-163">sim</span><span class="sxs-lookup"><span data-stu-id="11ab9-163">yes</span></span>      | <span data-ttu-id="11ab9-164">A ID do pacote, em minúsculas</span><span class="sxs-lookup"><span data-stu-id="11ab9-164">The package ID, lowercase</span></span>
<span data-ttu-id="11ab9-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="11ab9-165">LOWER_VERSION</span></span> | <span data-ttu-id="11ab9-166">URL</span><span class="sxs-lookup"><span data-stu-id="11ab9-166">URL</span></span>    | <span data-ttu-id="11ab9-167">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="11ab9-167">string</span></span> | <span data-ttu-id="11ab9-168">sim</span><span class="sxs-lookup"><span data-stu-id="11ab9-168">yes</span></span>      | <span data-ttu-id="11ab9-169">A versão do pacote, normalizado e em minúscula</span><span class="sxs-lookup"><span data-stu-id="11ab9-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="11ab9-170">Ambos `LOWER_ID` e `LOWER_VERSION` em minúscula usando as regras implementadas pelo. Do NET [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="11ab9-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="11ab9-171">método.</span><span class="sxs-lookup"><span data-stu-id="11ab9-171">method.</span></span>

<span data-ttu-id="11ab9-172">O `LOWER_VERSION` é a versão do pacote desejado normalizada usando a versão do NuGet [regras de normalização](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="11ab9-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="11ab9-173">Isso significa que os metadados compilação que é permitido pela especificação de SemVer 2.0.0 devem ser excluídos nesse caso.</span><span class="sxs-lookup"><span data-stu-id="11ab9-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="11ab9-174">Corpo da resposta</span><span class="sxs-lookup"><span data-stu-id="11ab9-174">Response body</span></span>

<span data-ttu-id="11ab9-175">Se o pacote existe na origem do pacote, um código de 200 status será retornado.</span><span class="sxs-lookup"><span data-stu-id="11ab9-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="11ab9-176">O corpo da resposta será o conteúdo do pacote.</span><span class="sxs-lookup"><span data-stu-id="11ab9-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="11ab9-177">Se o pacote não existe na origem do pacote, um código de 404 status será retornado.</span><span class="sxs-lookup"><span data-stu-id="11ab9-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="11ab9-178">Exemplo de solicitação</span><span class="sxs-lookup"><span data-stu-id="11ab9-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="11ab9-179">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="11ab9-179">Sample response</span></span>

<span data-ttu-id="11ab9-180">O fluxo binário que é o. nupkg para newtonsoft. JSON 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="11ab9-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="11ab9-181">Baixe o manifesto do pacote (. NuSpec)</span><span class="sxs-lookup"><span data-stu-id="11ab9-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="11ab9-182">Se o cliente sabe que uma ID de pacote e a versão e quiser baixar o manifesto do pacote, precisará apenas construir a URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="11ab9-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="11ab9-183">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="11ab9-183">Request parameters</span></span>

<span data-ttu-id="11ab9-184">Nome</span><span class="sxs-lookup"><span data-stu-id="11ab9-184">Name</span></span>          | <span data-ttu-id="11ab9-185">No</span><span class="sxs-lookup"><span data-stu-id="11ab9-185">In</span></span>     | <span data-ttu-id="11ab9-186">Tipo</span><span class="sxs-lookup"><span data-stu-id="11ab9-186">Type</span></span>   | <span data-ttu-id="11ab9-187">Necessária</span><span class="sxs-lookup"><span data-stu-id="11ab9-187">Required</span></span> | <span data-ttu-id="11ab9-188">Observações</span><span class="sxs-lookup"><span data-stu-id="11ab9-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="11ab9-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="11ab9-189">LOWER_ID</span></span>      | <span data-ttu-id="11ab9-190">URL</span><span class="sxs-lookup"><span data-stu-id="11ab9-190">URL</span></span>    | <span data-ttu-id="11ab9-191">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="11ab9-191">string</span></span> | <span data-ttu-id="11ab9-192">sim</span><span class="sxs-lookup"><span data-stu-id="11ab9-192">yes</span></span>      | <span data-ttu-id="11ab9-193">A ID do pacote, em minúsculas</span><span class="sxs-lookup"><span data-stu-id="11ab9-193">The package ID, lowercase</span></span>
<span data-ttu-id="11ab9-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="11ab9-194">LOWER_VERSION</span></span> | <span data-ttu-id="11ab9-195">URL</span><span class="sxs-lookup"><span data-stu-id="11ab9-195">URL</span></span>    | <span data-ttu-id="11ab9-196">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="11ab9-196">string</span></span> | <span data-ttu-id="11ab9-197">sim</span><span class="sxs-lookup"><span data-stu-id="11ab9-197">yes</span></span>      | <span data-ttu-id="11ab9-198">A versão do pacote, normalizado e em minúscula</span><span class="sxs-lookup"><span data-stu-id="11ab9-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="11ab9-199">Ambos `LOWER_ID` e `LOWER_VERSION` em minúscula usando as regras implementadas pelo. Do NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.</span><span class="sxs-lookup"><span data-stu-id="11ab9-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="11ab9-200">O `LOWER_VERSION` é a versão do pacote desejado normalizada usando a versão do NuGet [regras de normalização](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="11ab9-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="11ab9-201">Isso significa que os metadados compilação que é permitido pela especificação de SemVer 2.0.0 devem ser excluídos nesse caso.</span><span class="sxs-lookup"><span data-stu-id="11ab9-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="11ab9-202">Corpo da resposta</span><span class="sxs-lookup"><span data-stu-id="11ab9-202">Response body</span></span>

<span data-ttu-id="11ab9-203">Se o pacote existe na origem do pacote, um código de 200 status será retornado.</span><span class="sxs-lookup"><span data-stu-id="11ab9-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="11ab9-204">O corpo da resposta será o manifesto de pacote, que é o. NuSpec contidos no. nupkg correspondente.</span><span class="sxs-lookup"><span data-stu-id="11ab9-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="11ab9-205">O. NuSpec é um documento XML.</span><span class="sxs-lookup"><span data-stu-id="11ab9-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="11ab9-206">Se o pacote não existe na origem do pacote, um código de 404 status será retornado.</span><span class="sxs-lookup"><span data-stu-id="11ab9-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="11ab9-207">Exemplo de solicitação</span><span class="sxs-lookup"><span data-stu-id="11ab9-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="11ab9-208">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="11ab9-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
