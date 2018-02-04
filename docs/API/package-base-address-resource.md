---
title: "Pacote de conteúdo, o NuGet API | Microsoft Docs"
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
description: "O endereço base do pacote é uma interface simples para buscar o pacote propriamente dito."
keywords: "NuGet simples contêiner, o endereço base do pacote NuGet, o NuGet nupkg API, versões de pacote do NuGet API, API do NuGet não consta da lista de pacotes, o NuGet API download nuspec"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c2e631dc0bba95ac849430d77142f27ef591f741
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="package-content"></a><span data-ttu-id="04590-104">Conteúdo do pacote</span><span class="sxs-lookup"><span data-stu-id="04590-104">Package Content</span></span>

<span data-ttu-id="04590-105">É possível gerar uma URL para buscar o conteúdo de um pacote arbitrário (o arquivo. nupkg) usando a API V3.</span><span class="sxs-lookup"><span data-stu-id="04590-105">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="04590-106">O recurso usado para buscar o conteúdo do pacote é o `PackageBaseAddress` recurso encontrado na [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="04590-106">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="04590-107">Esse recurso também permite a descoberta de todas as versões de um pacote, listados ou não listadas.</span><span class="sxs-lookup"><span data-stu-id="04590-107">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="04590-108">Este recurso é conhecido como um "pacote base endereço" ou "contêiner simples".</span><span class="sxs-lookup"><span data-stu-id="04590-108">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="04590-109">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="04590-109">Versioning</span></span>

<span data-ttu-id="04590-110">O seguinte `@type` valor é usado:</span><span class="sxs-lookup"><span data-stu-id="04590-110">The following `@type` value is used:</span></span>

<span data-ttu-id="04590-111">Valor @type</span><span class="sxs-lookup"><span data-stu-id="04590-111">@type value</span></span>              | <span data-ttu-id="04590-112">Observações</span><span class="sxs-lookup"><span data-stu-id="04590-112">Notes</span></span>
------------------------ | -----
<span data-ttu-id="04590-113">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="04590-113">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="04590-114">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="04590-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="04590-115">URL Base</span><span class="sxs-lookup"><span data-stu-id="04590-115">Base URL</span></span>

<span data-ttu-id="04590-116">A URL base para as seguintes APIs é o valor da `@id` propriedade associada com o recurso mencionados acima `@type` valor.</span><span class="sxs-lookup"><span data-stu-id="04590-116">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="04590-117">No documento a seguir, a URL base do espaço reservado `{@id}` será usado.</span><span class="sxs-lookup"><span data-stu-id="04590-117">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="04590-118">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="04590-118">HTTP methods</span></span>

<span data-ttu-id="04590-119">Todas as URLs encontradas no suporte a recurso de registro os métodos HTTP `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="04590-119">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="04590-120">Enumerar as versões do pacote</span><span class="sxs-lookup"><span data-stu-id="04590-120">Enumerate package versions</span></span>

<span data-ttu-id="04590-121">Se o cliente sabe uma ID de pacote e quer descobrir quais versões do pacote do pacote de origem tem disponível, o cliente pode construir uma URL previsível para enumerar todas as versões do pacote.</span><span class="sxs-lookup"><span data-stu-id="04590-121">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="04590-122">Essa lista deve ser uma "listagem de diretório" para a API de conteúdo do pacote mencionada abaixo.</span><span class="sxs-lookup"><span data-stu-id="04590-122">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="04590-123">Essa lista contém as duas versões do pacote listados e não listados.</span><span class="sxs-lookup"><span data-stu-id="04590-123">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="04590-124">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="04590-124">Request parameters</span></span>

<span data-ttu-id="04590-125">Nome</span><span class="sxs-lookup"><span data-stu-id="04590-125">Name</span></span>     | <span data-ttu-id="04590-126">No</span><span class="sxs-lookup"><span data-stu-id="04590-126">In</span></span>     | <span data-ttu-id="04590-127">Tipo</span><span class="sxs-lookup"><span data-stu-id="04590-127">Type</span></span>    | <span data-ttu-id="04590-128">Necessária</span><span class="sxs-lookup"><span data-stu-id="04590-128">Required</span></span> | <span data-ttu-id="04590-129">Observações</span><span class="sxs-lookup"><span data-stu-id="04590-129">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="04590-130">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="04590-130">LOWER_ID</span></span> | <span data-ttu-id="04590-131">URL</span><span class="sxs-lookup"><span data-stu-id="04590-131">URL</span></span>    | <span data-ttu-id="04590-132">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="04590-132">string</span></span>  | <span data-ttu-id="04590-133">sim</span><span class="sxs-lookup"><span data-stu-id="04590-133">yes</span></span>      | <span data-ttu-id="04590-134">A ID do pacote, letras minúsculas</span><span class="sxs-lookup"><span data-stu-id="04590-134">The package ID, lowercase</span></span>

<span data-ttu-id="04590-135">O `LOWER_ID` valor é a ID do pacote desejado em minúscula usando as regras implementadas pelo. Do NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.</span><span class="sxs-lookup"><span data-stu-id="04590-135">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="04590-136">Resposta</span><span class="sxs-lookup"><span data-stu-id="04590-136">Response</span></span>

<span data-ttu-id="04590-137">Se a origem do pacote não tem nenhuma versão da ID do pacote fornecido, um código de 404 status será retornado.</span><span class="sxs-lookup"><span data-stu-id="04590-137">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="04590-138">Se a origem do pacote tem uma ou mais versões, um código de 200 status será retornado.</span><span class="sxs-lookup"><span data-stu-id="04590-138">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="04590-139">O corpo da resposta é um objeto JSON com a seguinte propriedade:</span><span class="sxs-lookup"><span data-stu-id="04590-139">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="04590-140">Nome</span><span class="sxs-lookup"><span data-stu-id="04590-140">Name</span></span>     | <span data-ttu-id="04590-141">Tipo</span><span class="sxs-lookup"><span data-stu-id="04590-141">Type</span></span>             | <span data-ttu-id="04590-142">Necessária</span><span class="sxs-lookup"><span data-stu-id="04590-142">Required</span></span> | <span data-ttu-id="04590-143">Observações</span><span class="sxs-lookup"><span data-stu-id="04590-143">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="04590-144">versões</span><span class="sxs-lookup"><span data-stu-id="04590-144">versions</span></span> | <span data-ttu-id="04590-145">Matriz de cadeias de caracteres</span><span class="sxs-lookup"><span data-stu-id="04590-145">array of strings</span></span> | <span data-ttu-id="04590-146">sim</span><span class="sxs-lookup"><span data-stu-id="04590-146">yes</span></span>      | <span data-ttu-id="04590-147">O pacote IDs disponíveis</span><span class="sxs-lookup"><span data-stu-id="04590-147">The package IDs available</span></span>

<span data-ttu-id="04590-148">As cadeias de caracteres no `versions` matriz estão todos em minúscula, [normalizado cadeias de caracteres de versão NuGet](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="04590-148">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="04590-149">As cadeias de caracteres de versão não contém metadados de compilação SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="04590-149">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="04590-150">A intenção é que as cadeias de caracteres de versão encontradas nesta matriz podem ser usadas textualmente para o `LOWER_VERSION` tokens encontrado nos seguintes pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="04590-150">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="04590-151">Solicitação de amostra</span><span class="sxs-lookup"><span data-stu-id="04590-151">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="04590-152">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="04590-152">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="04590-153">Baixar o conteúdo do pacote (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="04590-153">Download package content (.nupkg)</span></span>

<span data-ttu-id="04590-154">Se o cliente sabe um ID de pacote e a versão e deseja baixar o conteúdo do pacote, eles só precisam construir a URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="04590-154">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="04590-155">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="04590-155">Request parameters</span></span>

<span data-ttu-id="04590-156">Nome</span><span class="sxs-lookup"><span data-stu-id="04590-156">Name</span></span>          | <span data-ttu-id="04590-157">No</span><span class="sxs-lookup"><span data-stu-id="04590-157">In</span></span>     | <span data-ttu-id="04590-158">Tipo</span><span class="sxs-lookup"><span data-stu-id="04590-158">Type</span></span>   | <span data-ttu-id="04590-159">Necessária</span><span class="sxs-lookup"><span data-stu-id="04590-159">Required</span></span> | <span data-ttu-id="04590-160">Observações</span><span class="sxs-lookup"><span data-stu-id="04590-160">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="04590-161">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="04590-161">LOWER_ID</span></span>      | <span data-ttu-id="04590-162">URL</span><span class="sxs-lookup"><span data-stu-id="04590-162">URL</span></span>    | <span data-ttu-id="04590-163">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="04590-163">string</span></span> | <span data-ttu-id="04590-164">sim</span><span class="sxs-lookup"><span data-stu-id="04590-164">yes</span></span>      | <span data-ttu-id="04590-165">A ID do pacote, letras minúsculas</span><span class="sxs-lookup"><span data-stu-id="04590-165">The package ID, lowercase</span></span>
<span data-ttu-id="04590-166">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="04590-166">LOWER_VERSION</span></span> | <span data-ttu-id="04590-167">URL</span><span class="sxs-lookup"><span data-stu-id="04590-167">URL</span></span>    | <span data-ttu-id="04590-168">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="04590-168">string</span></span> | <span data-ttu-id="04590-169">sim</span><span class="sxs-lookup"><span data-stu-id="04590-169">yes</span></span>      | <span data-ttu-id="04590-170">A versão do pacote, padronizado e minúscula</span><span class="sxs-lookup"><span data-stu-id="04590-170">The package version, normalized and lowercased</span></span>

<span data-ttu-id="04590-171">Ambos `LOWER_ID` e `LOWER_VERSION` em minúscula usando as regras implementadas pelo. Do NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.</span><span class="sxs-lookup"><span data-stu-id="04590-171">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="04590-172">O `LOWER_VERSION` é a versão do pacote desejado normalizado de acordo com a versão do NuGet [as regras de normalização](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="04590-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="04590-173">Isso significa que os metadados de compilação que é permitido pela especificação SemVer 2.0.0 devem ser excluídos nesse caso.</span><span class="sxs-lookup"><span data-stu-id="04590-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="04590-174">Corpo da resposta</span><span class="sxs-lookup"><span data-stu-id="04590-174">Response body</span></span>

<span data-ttu-id="04590-175">Se o pacote existe na origem do pacote, um código de 200 status será retornado.</span><span class="sxs-lookup"><span data-stu-id="04590-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="04590-176">O corpo da resposta será o conteúdo do pacote.</span><span class="sxs-lookup"><span data-stu-id="04590-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="04590-177">Se o pacote não existe na origem do pacote, um código de 404 status será retornado.</span><span class="sxs-lookup"><span data-stu-id="04590-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="04590-178">Solicitação de amostra</span><span class="sxs-lookup"><span data-stu-id="04590-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="04590-179">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="04590-179">Sample response</span></span>

<span data-ttu-id="04590-180">O fluxo binário é nupkg para newtonsoft 9.0.1.</span><span class="sxs-lookup"><span data-stu-id="04590-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="04590-181">Baixe o manifesto de pacote (. NuSpec)</span><span class="sxs-lookup"><span data-stu-id="04590-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="04590-182">Se o cliente sabe um ID de pacote e a versão e deseja baixar o manifesto de pacote, eles só precisam construir a URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="04590-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="04590-183">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="04590-183">Request parameters</span></span>

<span data-ttu-id="04590-184">Nome</span><span class="sxs-lookup"><span data-stu-id="04590-184">Name</span></span>          | <span data-ttu-id="04590-185">No</span><span class="sxs-lookup"><span data-stu-id="04590-185">In</span></span>     | <span data-ttu-id="04590-186">Tipo</span><span class="sxs-lookup"><span data-stu-id="04590-186">Type</span></span>    | <span data-ttu-id="04590-187">Necessária</span><span class="sxs-lookup"><span data-stu-id="04590-187">Required</span></span> | <span data-ttu-id="04590-188">Observações</span><span class="sxs-lookup"><span data-stu-id="04590-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="04590-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="04590-189">LOWER_ID</span></span>      | <span data-ttu-id="04590-190">URL</span><span class="sxs-lookup"><span data-stu-id="04590-190">URL</span></span>    | <span data-ttu-id="04590-191">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="04590-191">string</span></span>  | <span data-ttu-id="04590-192">sim</span><span class="sxs-lookup"><span data-stu-id="04590-192">yes</span></span>      | <span data-ttu-id="04590-193">A ID do pacote, letras minúsculas</span><span class="sxs-lookup"><span data-stu-id="04590-193">The package ID, lowercase</span></span>
<span data-ttu-id="04590-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="04590-194">LOWER_VERSION</span></span> | <span data-ttu-id="04590-195">URL</span><span class="sxs-lookup"><span data-stu-id="04590-195">URL</span></span>    | <span data-ttu-id="04590-196">inteiro</span><span class="sxs-lookup"><span data-stu-id="04590-196">integer</span></span> | <span data-ttu-id="04590-197">sim</span><span class="sxs-lookup"><span data-stu-id="04590-197">yes</span></span>      | <span data-ttu-id="04590-198">A versão do pacote, padronizado e minúscula</span><span class="sxs-lookup"><span data-stu-id="04590-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="04590-199">Ambos `LOWER_ID` e `LOWER_VERSION` em minúscula usando as regras implementadas pelo. Do NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) método.</span><span class="sxs-lookup"><span data-stu-id="04590-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="04590-200">O `LOWER_VERSION` é a versão do pacote desejado normalizado de acordo com a versão do NuGet [as regras de normalização](../reference/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="04590-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="04590-201">Isso significa que os metadados de compilação que é permitido pela especificação SemVer 2.0.0 devem ser excluídos nesse caso.</span><span class="sxs-lookup"><span data-stu-id="04590-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="04590-202">Corpo da resposta</span><span class="sxs-lookup"><span data-stu-id="04590-202">Response body</span></span>

<span data-ttu-id="04590-203">Se o pacote existe na origem do pacote, um código de 200 status será retornado.</span><span class="sxs-lookup"><span data-stu-id="04590-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="04590-204">O corpo da resposta será o manifesto de pacote, que é o. NuSpec contidas o nupkg correspondente.</span><span class="sxs-lookup"><span data-stu-id="04590-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="04590-205">A. NuSpec é um documento XML.</span><span class="sxs-lookup"><span data-stu-id="04590-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="04590-206">Se o pacote não existe na origem do pacote, um código de 404 status será retornado.</span><span class="sxs-lookup"><span data-stu-id="04590-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="04590-207">Solicitação de amostra</span><span class="sxs-lookup"><span data-stu-id="04590-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="04590-208">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="04590-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
