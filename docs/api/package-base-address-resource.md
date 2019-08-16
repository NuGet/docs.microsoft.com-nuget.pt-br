---
title: Conteúdo do pacote, API do NuGet
description: O endereço base do pacote é uma interface simples para buscar o pacote em si.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 5ec6c0e17a3e8b9a3f156a48685bcaafe42c744b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488228"
---
# <a name="package-content"></a><span data-ttu-id="e4ea4-103">Conteúdo do pacote</span><span class="sxs-lookup"><span data-stu-id="e4ea4-103">Package Content</span></span>

<span data-ttu-id="e4ea4-104">É possível gerar uma URL para buscar o conteúdo de um pacote arbitrário (o arquivo. nupkg) usando a API v3.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="e4ea4-105">O recurso usado para buscar o conteúdo do pacote é `PackageBaseAddress` o recurso encontrado no [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="e4ea4-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="e4ea4-106">Esse recurso também habilita a descoberta de todas as versões de um pacote, listadas ou não listadas.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="e4ea4-107">Esse recurso é comumente conhecido como "endereço base do pacote" ou como "contêiner simples".</span><span class="sxs-lookup"><span data-stu-id="e4ea4-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="e4ea4-108">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="e4ea4-108">Versioning</span></span>

<span data-ttu-id="e4ea4-109">O seguinte `@type` valor é usado:</span><span class="sxs-lookup"><span data-stu-id="e4ea4-109">The following `@type` value is used:</span></span>

<span data-ttu-id="e4ea4-110">Valor @type</span><span class="sxs-lookup"><span data-stu-id="e4ea4-110">@type value</span></span>              | <span data-ttu-id="e4ea4-111">Observações</span><span class="sxs-lookup"><span data-stu-id="e4ea4-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="e4ea4-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="e4ea4-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="e4ea4-113">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="e4ea4-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="e4ea4-114">URL Base</span><span class="sxs-lookup"><span data-stu-id="e4ea4-114">Base URL</span></span>

<span data-ttu-id="e4ea4-115">A URL base para as APIs a seguir é o valor da `@id` propriedade associada ao valor de recurso `@type` mencionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="e4ea4-116">No documento a seguir, a URL `{@id}` base do espaço reservado será usada.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e4ea4-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="e4ea4-117">HTTP methods</span></span>

<span data-ttu-id="e4ea4-118">Todas as URLs encontradas no recurso de registro dão suporte aos `GET` métodos `HEAD`http e.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="e4ea4-119">Enumerar versões de pacote</span><span class="sxs-lookup"><span data-stu-id="e4ea4-119">Enumerate package versions</span></span>

<span data-ttu-id="e4ea4-120">Se o cliente souber uma ID de pacote e quiser descobrir quais versões de pacote a origem do pacote está disponível, o cliente poderá construir uma URL previsível para enumerar todas as versões do pacote.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="e4ea4-121">Esta lista deve ser uma "listagem de diretório" para a API de conteúdo do pacote mencionada abaixo.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="e4ea4-122">Essa lista contém as versões de pacote listadas e não listadas.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="e4ea4-123">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="e4ea4-123">Request parameters</span></span>

<span data-ttu-id="e4ea4-124">Nome</span><span class="sxs-lookup"><span data-stu-id="e4ea4-124">Name</span></span>     | <span data-ttu-id="e4ea4-125">No</span><span class="sxs-lookup"><span data-stu-id="e4ea4-125">In</span></span>     | <span data-ttu-id="e4ea4-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="e4ea4-126">Type</span></span>    | <span data-ttu-id="e4ea4-127">Necessária</span><span class="sxs-lookup"><span data-stu-id="e4ea4-127">Required</span></span> | <span data-ttu-id="e4ea4-128">Observações</span><span class="sxs-lookup"><span data-stu-id="e4ea4-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="e4ea4-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="e4ea4-129">LOWER_ID</span></span> | <span data-ttu-id="e4ea4-130">URL</span><span class="sxs-lookup"><span data-stu-id="e4ea4-130">URL</span></span>    | <span data-ttu-id="e4ea4-131">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e4ea4-131">string</span></span>  | <span data-ttu-id="e4ea4-132">sim</span><span class="sxs-lookup"><span data-stu-id="e4ea4-132">yes</span></span>      | <span data-ttu-id="e4ea4-133">A ID do pacote, em minúsculas</span><span class="sxs-lookup"><span data-stu-id="e4ea4-133">The package ID, lowercase</span></span>

<span data-ttu-id="e4ea4-134">O `LOWER_ID` valor é a ID de pacote desejada com letras minúsculas usando as regras implementadas pelo. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Método net.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="e4ea4-135">Resposta</span><span class="sxs-lookup"><span data-stu-id="e4ea4-135">Response</span></span>

<span data-ttu-id="e4ea4-136">Se a origem do pacote não tiver nenhuma versão da ID de pacote fornecida, um código de status 404 será retornado.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="e4ea4-137">Se a origem do pacote tiver uma ou mais versões, um código de status 200 será retornado.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="e4ea4-138">O corpo da resposta é um objeto JSON com a seguinte propriedade:</span><span class="sxs-lookup"><span data-stu-id="e4ea4-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="e4ea4-139">Nome</span><span class="sxs-lookup"><span data-stu-id="e4ea4-139">Name</span></span>     | <span data-ttu-id="e4ea4-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="e4ea4-140">Type</span></span>             | <span data-ttu-id="e4ea4-141">Necessária</span><span class="sxs-lookup"><span data-stu-id="e4ea4-141">Required</span></span> | <span data-ttu-id="e4ea4-142">Observações</span><span class="sxs-lookup"><span data-stu-id="e4ea4-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="e4ea4-143">versões</span><span class="sxs-lookup"><span data-stu-id="e4ea4-143">versions</span></span> | <span data-ttu-id="e4ea4-144">matriz de cadeias de caracteres</span><span class="sxs-lookup"><span data-stu-id="e4ea4-144">array of strings</span></span> | <span data-ttu-id="e4ea4-145">sim</span><span class="sxs-lookup"><span data-stu-id="e4ea4-145">yes</span></span>      | <span data-ttu-id="e4ea4-146">As IDs de pacote disponíveis</span><span class="sxs-lookup"><span data-stu-id="e4ea4-146">The package IDs available</span></span>

<span data-ttu-id="e4ea4-147">As cadeias de `versions` caracteres na matriz são todas as [cadeias de caracteres de versão do NuGet normalizadas](../concepts/package-versioning.md#normalized-version-numbers)e em letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="e4ea4-148">As cadeias de caracteres de versão não contêm nenhum metadado de compilação SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="e4ea4-149">A intenção é que as cadeias de caracteres de versão encontradas nessa matriz possam ser usadas `LOWER_VERSION` em textual para os tokens encontrados nos pontos de extremidade a seguir.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e4ea4-150">Exemplo de solicitação</span><span class="sxs-lookup"><span data-stu-id="e4ea4-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="e4ea4-151">Exemplo de resposta</span><span class="sxs-lookup"><span data-stu-id="e4ea4-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="e4ea4-152">Baixar conteúdo do pacote (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="e4ea4-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="e4ea4-153">Se o cliente souber uma ID e uma versão do pacote e quiser baixar o conteúdo do pacote, ele só precisará construir a seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="e4ea4-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="e4ea4-154">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="e4ea4-154">Request parameters</span></span>

<span data-ttu-id="e4ea4-155">Nome</span><span class="sxs-lookup"><span data-stu-id="e4ea4-155">Name</span></span>          | <span data-ttu-id="e4ea4-156">No</span><span class="sxs-lookup"><span data-stu-id="e4ea4-156">In</span></span>     | <span data-ttu-id="e4ea4-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="e4ea4-157">Type</span></span>   | <span data-ttu-id="e4ea4-158">Necessária</span><span class="sxs-lookup"><span data-stu-id="e4ea4-158">Required</span></span> | <span data-ttu-id="e4ea4-159">Observações</span><span class="sxs-lookup"><span data-stu-id="e4ea4-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="e4ea4-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="e4ea4-160">LOWER_ID</span></span>      | <span data-ttu-id="e4ea4-161">URL</span><span class="sxs-lookup"><span data-stu-id="e4ea4-161">URL</span></span>    | <span data-ttu-id="e4ea4-162">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e4ea4-162">string</span></span> | <span data-ttu-id="e4ea4-163">sim</span><span class="sxs-lookup"><span data-stu-id="e4ea4-163">yes</span></span>      | <span data-ttu-id="e4ea4-164">A ID do pacote, em minúsculas</span><span class="sxs-lookup"><span data-stu-id="e4ea4-164">The package ID, lowercase</span></span>
<span data-ttu-id="e4ea4-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="e4ea4-165">LOWER_VERSION</span></span> | <span data-ttu-id="e4ea4-166">URL</span><span class="sxs-lookup"><span data-stu-id="e4ea4-166">URL</span></span>    | <span data-ttu-id="e4ea4-167">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e4ea4-167">string</span></span> | <span data-ttu-id="e4ea4-168">sim</span><span class="sxs-lookup"><span data-stu-id="e4ea4-168">yes</span></span>      | <span data-ttu-id="e4ea4-169">A versão do pacote, normalizada e minúscula</span><span class="sxs-lookup"><span data-stu-id="e4ea4-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="e4ea4-170">Ambos `LOWER_ID` e `LOWER_VERSION` estão em letras minúsculas usando as regras implementadas pelo. Da rede[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="e4ea4-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="e4ea4-171">método.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-171">method.</span></span>

<span data-ttu-id="e4ea4-172">O `LOWER_VERSION` é a versão de pacote desejada normalizada usando [as regras](../concepts/package-versioning.md#normalized-version-numbers)de normalização de versão do NuGet.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="e4ea4-173">Isso significa que os metadados de compilação permitidos pela especificação SemVer 2.0.0 devem ser excluídos nesse caso.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="e4ea4-174">Corpo da resposta</span><span class="sxs-lookup"><span data-stu-id="e4ea4-174">Response body</span></span>

<span data-ttu-id="e4ea4-175">Se o pacote existir na origem do pacote, um código de status 200 será retornado.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="e4ea4-176">O corpo da resposta será o próprio conteúdo do pacote.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="e4ea4-177">Se o pacote não existir na origem do pacote, um código de status 404 será retornado.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e4ea4-178">Exemplo de solicitação</span><span class="sxs-lookup"><span data-stu-id="e4ea4-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="e4ea4-179">Exemplo de resposta</span><span class="sxs-lookup"><span data-stu-id="e4ea4-179">Sample response</span></span>

<span data-ttu-id="e4ea4-180">O fluxo binário que é o. nupkg para Newtonsoft. JSON 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="e4ea4-181">Baixar o manifesto do pacote (. nuspec)</span><span class="sxs-lookup"><span data-stu-id="e4ea4-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="e4ea4-182">Se o cliente souber uma ID e uma versão do pacote e quiser baixar o manifesto do pacote, ele só precisará construir a seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="e4ea4-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="e4ea4-183">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="e4ea4-183">Request parameters</span></span>

<span data-ttu-id="e4ea4-184">Nome</span><span class="sxs-lookup"><span data-stu-id="e4ea4-184">Name</span></span>          | <span data-ttu-id="e4ea4-185">No</span><span class="sxs-lookup"><span data-stu-id="e4ea4-185">In</span></span>     | <span data-ttu-id="e4ea4-186">Tipo</span><span class="sxs-lookup"><span data-stu-id="e4ea4-186">Type</span></span>   | <span data-ttu-id="e4ea4-187">Necessária</span><span class="sxs-lookup"><span data-stu-id="e4ea4-187">Required</span></span> | <span data-ttu-id="e4ea4-188">Observações</span><span class="sxs-lookup"><span data-stu-id="e4ea4-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="e4ea4-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="e4ea4-189">LOWER_ID</span></span>      | <span data-ttu-id="e4ea4-190">URL</span><span class="sxs-lookup"><span data-stu-id="e4ea4-190">URL</span></span>    | <span data-ttu-id="e4ea4-191">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e4ea4-191">string</span></span> | <span data-ttu-id="e4ea4-192">sim</span><span class="sxs-lookup"><span data-stu-id="e4ea4-192">yes</span></span>      | <span data-ttu-id="e4ea4-193">A ID do pacote, em minúsculas</span><span class="sxs-lookup"><span data-stu-id="e4ea4-193">The package ID, lowercase</span></span>
<span data-ttu-id="e4ea4-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="e4ea4-194">LOWER_VERSION</span></span> | <span data-ttu-id="e4ea4-195">URL</span><span class="sxs-lookup"><span data-stu-id="e4ea4-195">URL</span></span>    | <span data-ttu-id="e4ea4-196">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e4ea4-196">string</span></span> | <span data-ttu-id="e4ea4-197">sim</span><span class="sxs-lookup"><span data-stu-id="e4ea4-197">yes</span></span>      | <span data-ttu-id="e4ea4-198">A versão do pacote, normalizada e minúscula</span><span class="sxs-lookup"><span data-stu-id="e4ea4-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="e4ea4-199">Ambos `LOWER_ID` e `LOWER_VERSION` estão em letras minúsculas usando as regras implementadas pelo. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Método net.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="e4ea4-200">O `LOWER_VERSION` é a versão de pacote desejada normalizada usando [as regras](../concepts/package-versioning.md#normalized-version-numbers)de normalização de versão do NuGet.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="e4ea4-201">Isso significa que os metadados de compilação permitidos pela especificação SemVer 2.0.0 devem ser excluídos nesse caso.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="e4ea4-202">Corpo da resposta</span><span class="sxs-lookup"><span data-stu-id="e4ea4-202">Response body</span></span>

<span data-ttu-id="e4ea4-203">Se o pacote existir na origem do pacote, um código de status 200 será retornado.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="e4ea4-204">O corpo da resposta será o manifesto do pacote, que é o. nuspec contido no. nupkg correspondente.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="e4ea4-205">O. nuspec é um documento XML.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="e4ea4-206">Se o pacote não existir na origem do pacote, um código de status 404 será retornado.</span><span class="sxs-lookup"><span data-stu-id="e4ea4-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e4ea4-207">Exemplo de solicitação</span><span class="sxs-lookup"><span data-stu-id="e4ea4-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="e4ea4-208">Exemplo de resposta</span><span class="sxs-lookup"><span data-stu-id="e4ea4-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
