---
title: Preenchimento automático, API do NuGet
description: O serviço de preenchimento automático de pesquisa dá suporte a versões e descoberta interativa de IDs de pacote.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2d2b20c1ea439ec0a3225cf983d9a4d2eedb0333
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324754"
---
# <a name="autocomplete"></a><span data-ttu-id="7263e-103">Preenchimento Automático</span><span class="sxs-lookup"><span data-stu-id="7263e-103">Autocomplete</span></span>

<span data-ttu-id="7263e-104">É possível criar um pacote ID e a versão AutoCompletar experiência usando a API V3.</span><span class="sxs-lookup"><span data-stu-id="7263e-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="7263e-105">O recurso usado para fazer consultas de preenchimento automático é o `SearchAutocompleteService` recurso encontrado na [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="7263e-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="7263e-106">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="7263e-106">Versioning</span></span>

<span data-ttu-id="7263e-107">O seguinte `@type` valores são usados:</span><span class="sxs-lookup"><span data-stu-id="7263e-107">The following `@type` values are used:</span></span>

<span data-ttu-id="7263e-108">Valor @type</span><span class="sxs-lookup"><span data-stu-id="7263e-108">@type value</span></span>                          | <span data-ttu-id="7263e-109">Observações</span><span class="sxs-lookup"><span data-stu-id="7263e-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="7263e-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="7263e-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="7263e-111">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="7263e-111">The initial release</span></span>
<span data-ttu-id="7263e-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="7263e-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="7263e-113">Alias of `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="7263e-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="7263e-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="7263e-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="7263e-115">Alias of `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="7263e-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="7263e-116">URL Base</span><span class="sxs-lookup"><span data-stu-id="7263e-116">Base URL</span></span>

<span data-ttu-id="7263e-117">A URL base para as APIs a seguir é o valor da `@id` propriedade associada a um do recurso mencionados anteriormente `@type` valores.</span><span class="sxs-lookup"><span data-stu-id="7263e-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="7263e-118">O seguinte documento, o espaço reservado de URL de base `{@id}` será usado.</span><span class="sxs-lookup"><span data-stu-id="7263e-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="7263e-119">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="7263e-119">HTTP Methods</span></span>

<span data-ttu-id="7263e-120">Todas as URLs encontradas no suporte a recursos de registro os métodos HTTP `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="7263e-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="7263e-121">Procure as IDs de pacote</span><span class="sxs-lookup"><span data-stu-id="7263e-121">Search for package IDs</span></span>

<span data-ttu-id="7263e-122">O preenchimento automático de primeira API dá suporte a procurar por parte de uma cadeia de caracteres de ID do pacote.</span><span class="sxs-lookup"><span data-stu-id="7263e-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="7263e-123">Isso é ótimo quando você deseja fornecer um recurso de digitação antecipada de pacote em uma interface de usuário integrada com uma origem de pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="7263e-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="7263e-124">Um pacote com apenas as versões não listados não aparecerão nos resultados.</span><span class="sxs-lookup"><span data-stu-id="7263e-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="7263e-125">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="7263e-125">Request parameters</span></span>

<span data-ttu-id="7263e-126">Nome</span><span class="sxs-lookup"><span data-stu-id="7263e-126">Name</span></span>        | <span data-ttu-id="7263e-127">No</span><span class="sxs-lookup"><span data-stu-id="7263e-127">In</span></span>     | <span data-ttu-id="7263e-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="7263e-128">Type</span></span>    | <span data-ttu-id="7263e-129">Necessária</span><span class="sxs-lookup"><span data-stu-id="7263e-129">Required</span></span> | <span data-ttu-id="7263e-130">Observações</span><span class="sxs-lookup"><span data-stu-id="7263e-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="7263e-131">q</span><span class="sxs-lookup"><span data-stu-id="7263e-131">q</span></span>           | <span data-ttu-id="7263e-132">URL</span><span class="sxs-lookup"><span data-stu-id="7263e-132">URL</span></span>    | <span data-ttu-id="7263e-133">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7263e-133">string</span></span>  | <span data-ttu-id="7263e-134">no</span><span class="sxs-lookup"><span data-stu-id="7263e-134">no</span></span>       | <span data-ttu-id="7263e-135">A cadeia de caracteres a ser comparada com as IDs de pacote</span><span class="sxs-lookup"><span data-stu-id="7263e-135">The string to compare against package IDs</span></span>
<span data-ttu-id="7263e-136">skip</span><span class="sxs-lookup"><span data-stu-id="7263e-136">skip</span></span>        | <span data-ttu-id="7263e-137">URL</span><span class="sxs-lookup"><span data-stu-id="7263e-137">URL</span></span>    | <span data-ttu-id="7263e-138">inteiro</span><span class="sxs-lookup"><span data-stu-id="7263e-138">integer</span></span> | <span data-ttu-id="7263e-139">no</span><span class="sxs-lookup"><span data-stu-id="7263e-139">no</span></span>       | <span data-ttu-id="7263e-140">O número de resultados a ignorar, para paginação</span><span class="sxs-lookup"><span data-stu-id="7263e-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="7263e-141">Take</span><span class="sxs-lookup"><span data-stu-id="7263e-141">take</span></span>        | <span data-ttu-id="7263e-142">URL</span><span class="sxs-lookup"><span data-stu-id="7263e-142">URL</span></span>    | <span data-ttu-id="7263e-143">inteiro</span><span class="sxs-lookup"><span data-stu-id="7263e-143">integer</span></span> | <span data-ttu-id="7263e-144">no</span><span class="sxs-lookup"><span data-stu-id="7263e-144">no</span></span>       | <span data-ttu-id="7263e-145">O número de resultados a serem retornados para a paginação</span><span class="sxs-lookup"><span data-stu-id="7263e-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="7263e-146">versão de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="7263e-146">prerelease</span></span>  | <span data-ttu-id="7263e-147">URL</span><span class="sxs-lookup"><span data-stu-id="7263e-147">URL</span></span>    | <span data-ttu-id="7263e-148">boolean</span><span class="sxs-lookup"><span data-stu-id="7263e-148">boolean</span></span> | <span data-ttu-id="7263e-149">no</span><span class="sxs-lookup"><span data-stu-id="7263e-149">no</span></span>       | <span data-ttu-id="7263e-150">`true` ou `false` determinar se é necessário incluir [pacotes de pré-lançamento](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="7263e-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="7263e-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="7263e-151">semVerLevel</span></span> | <span data-ttu-id="7263e-152">URL</span><span class="sxs-lookup"><span data-stu-id="7263e-152">URL</span></span>    | <span data-ttu-id="7263e-153">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7263e-153">string</span></span>  | <span data-ttu-id="7263e-154">no</span><span class="sxs-lookup"><span data-stu-id="7263e-154">no</span></span>       | <span data-ttu-id="7263e-155">Uma cadeia de caracteres de versão 1.0.0 de SemVer</span><span class="sxs-lookup"><span data-stu-id="7263e-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="7263e-156">A consulta de preenchimento automático `q` é analisado de uma maneira que é definida pela implementação do servidor.</span><span class="sxs-lookup"><span data-stu-id="7263e-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="7263e-157">NuGet.org dá suporte à consulta para o prefixo de tokens de ID de pacote, que são partes da ID produzido pelo dividindo original pela concatenação com caracteres de símbolo e caso.</span><span class="sxs-lookup"><span data-stu-id="7263e-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="7263e-158">O `skip` parâmetro padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="7263e-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="7263e-159">O `take` parâmetro deve ser um inteiro maior que zero.</span><span class="sxs-lookup"><span data-stu-id="7263e-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="7263e-160">A implementação do servidor pode impor um valor máximo.</span><span class="sxs-lookup"><span data-stu-id="7263e-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="7263e-161">Se `prerelease` não for fornecido, pacotes de pré-lançamento são excluídos.</span><span class="sxs-lookup"><span data-stu-id="7263e-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="7263e-162">O `semVerLevel` parâmetro de consulta é usado para participar [SemVer 2.0.0 pacotes](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="7263e-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="7263e-163">Se esse parâmetro de consulta é excluído, as IDs de pacote somente com as versões compatíveis do SemVer 1.0.0 serão retornada (com o [padrão controle de versão do NuGet](../reference/package-versioning.md) advertências, como cadeias de caracteres de versão com partes de inteiro de 4).</span><span class="sxs-lookup"><span data-stu-id="7263e-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="7263e-164">Se `semVerLevel=2.0.0` for fornecido, SemVer 1.0.0 e pacotes de SemVer 2.0.0 compatíveis serão retornados.</span><span class="sxs-lookup"><span data-stu-id="7263e-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="7263e-165">Consulte a [SemVer 2.0.0 suporte para nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="7263e-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="7263e-166">Resposta</span><span class="sxs-lookup"><span data-stu-id="7263e-166">Response</span></span>

<span data-ttu-id="7263e-167">A resposta é o documento JSON que contém até `take` resultados de preenchimento automático.</span><span class="sxs-lookup"><span data-stu-id="7263e-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="7263e-168">O objeto JSON de raiz tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="7263e-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="7263e-169">Nome</span><span class="sxs-lookup"><span data-stu-id="7263e-169">Name</span></span>      | <span data-ttu-id="7263e-170">Tipo</span><span class="sxs-lookup"><span data-stu-id="7263e-170">Type</span></span>             | <span data-ttu-id="7263e-171">Necessária</span><span class="sxs-lookup"><span data-stu-id="7263e-171">Required</span></span> | <span data-ttu-id="7263e-172">Observações</span><span class="sxs-lookup"><span data-stu-id="7263e-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="7263e-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="7263e-173">totalHits</span></span> | <span data-ttu-id="7263e-174">inteiro</span><span class="sxs-lookup"><span data-stu-id="7263e-174">integer</span></span>          | <span data-ttu-id="7263e-175">sim</span><span class="sxs-lookup"><span data-stu-id="7263e-175">yes</span></span>      | <span data-ttu-id="7263e-176">O número total de correspondências, desconsiderando `skip` e `take`</span><span class="sxs-lookup"><span data-stu-id="7263e-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="7263e-177">Dados</span><span class="sxs-lookup"><span data-stu-id="7263e-177">data</span></span>      | <span data-ttu-id="7263e-178">matriz de cadeias de caracteres</span><span class="sxs-lookup"><span data-stu-id="7263e-178">array of strings</span></span> | <span data-ttu-id="7263e-179">sim</span><span class="sxs-lookup"><span data-stu-id="7263e-179">yes</span></span>      | <span data-ttu-id="7263e-180">O pacote IDs correspondidos pela solicitação</span><span class="sxs-lookup"><span data-stu-id="7263e-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="7263e-181">Exemplo de solicitação</span><span class="sxs-lookup"><span data-stu-id="7263e-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="7263e-182">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="7263e-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="7263e-183">Enumerar as versões do pacote</span><span class="sxs-lookup"><span data-stu-id="7263e-183">Enumerate package versions</span></span>

<span data-ttu-id="7263e-184">Quando uma ID de pacote for descoberta usando a API anterior, um cliente pode usar a API de preenchimento automático para enumerar as versões do pacote para uma ID do pacote fornecido.</span><span class="sxs-lookup"><span data-stu-id="7263e-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="7263e-185">Uma versão do pacote é removido da lista não aparecerão nos resultados.</span><span class="sxs-lookup"><span data-stu-id="7263e-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="7263e-186">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="7263e-186">Request parameters</span></span>

<span data-ttu-id="7263e-187">Nome</span><span class="sxs-lookup"><span data-stu-id="7263e-187">Name</span></span>        | <span data-ttu-id="7263e-188">No</span><span class="sxs-lookup"><span data-stu-id="7263e-188">In</span></span>     | <span data-ttu-id="7263e-189">Tipo</span><span class="sxs-lookup"><span data-stu-id="7263e-189">Type</span></span>    | <span data-ttu-id="7263e-190">Necessária</span><span class="sxs-lookup"><span data-stu-id="7263e-190">Required</span></span> | <span data-ttu-id="7263e-191">Observações</span><span class="sxs-lookup"><span data-stu-id="7263e-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="7263e-192">id</span><span class="sxs-lookup"><span data-stu-id="7263e-192">id</span></span>          | <span data-ttu-id="7263e-193">URL</span><span class="sxs-lookup"><span data-stu-id="7263e-193">URL</span></span>    | <span data-ttu-id="7263e-194">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7263e-194">string</span></span>  | <span data-ttu-id="7263e-195">sim</span><span class="sxs-lookup"><span data-stu-id="7263e-195">yes</span></span>      | <span data-ttu-id="7263e-196">A ID do pacote para buscar as versões para</span><span class="sxs-lookup"><span data-stu-id="7263e-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="7263e-197">versão de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="7263e-197">prerelease</span></span>  | <span data-ttu-id="7263e-198">URL</span><span class="sxs-lookup"><span data-stu-id="7263e-198">URL</span></span>    | <span data-ttu-id="7263e-199">boolean</span><span class="sxs-lookup"><span data-stu-id="7263e-199">boolean</span></span> | <span data-ttu-id="7263e-200">no</span><span class="sxs-lookup"><span data-stu-id="7263e-200">no</span></span>       | <span data-ttu-id="7263e-201">`true` ou `false` determinar se é necessário incluir [pacotes de pré-lançamento](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="7263e-201">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="7263e-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="7263e-202">semVerLevel</span></span> | <span data-ttu-id="7263e-203">URL</span><span class="sxs-lookup"><span data-stu-id="7263e-203">URL</span></span>    | <span data-ttu-id="7263e-204">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7263e-204">string</span></span>  | <span data-ttu-id="7263e-205">no</span><span class="sxs-lookup"><span data-stu-id="7263e-205">no</span></span>       | <span data-ttu-id="7263e-206">Uma cadeia de caracteres de versão de SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="7263e-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="7263e-207">Se `prerelease` não for fornecido, pacotes de pré-lançamento são excluídos.</span><span class="sxs-lookup"><span data-stu-id="7263e-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="7263e-208">O `semVerLevel` parâmetro de consulta é usado para participar de pacotes de SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="7263e-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="7263e-209">Se esse parâmetro de consulta é excluído, somente as versões de SemVer 1.0.0 serão retornadas.</span><span class="sxs-lookup"><span data-stu-id="7263e-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="7263e-210">Se `semVerLevel=2.0.0` for fornecido, as versões de SemVer 2.0.0 e SemVer 1.0.0 serão retornadas.</span><span class="sxs-lookup"><span data-stu-id="7263e-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="7263e-211">Consulte a [SemVer 2.0.0 suporte para nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="7263e-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="7263e-212">Resposta</span><span class="sxs-lookup"><span data-stu-id="7263e-212">Response</span></span>

<span data-ttu-id="7263e-213">A resposta é um documento JSON que contém todas as versões de pacote da ID do pacote fornecido, filtrando por parâmetros de consulta fornecidos.</span><span class="sxs-lookup"><span data-stu-id="7263e-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="7263e-214">O objeto JSON de raiz tem a seguinte propriedade:</span><span class="sxs-lookup"><span data-stu-id="7263e-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="7263e-215">Nome</span><span class="sxs-lookup"><span data-stu-id="7263e-215">Name</span></span>      | <span data-ttu-id="7263e-216">Tipo</span><span class="sxs-lookup"><span data-stu-id="7263e-216">Type</span></span>             | <span data-ttu-id="7263e-217">Necessária</span><span class="sxs-lookup"><span data-stu-id="7263e-217">Required</span></span> | <span data-ttu-id="7263e-218">Observações</span><span class="sxs-lookup"><span data-stu-id="7263e-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="7263e-219">Dados</span><span class="sxs-lookup"><span data-stu-id="7263e-219">data</span></span>      | <span data-ttu-id="7263e-220">matriz de cadeias de caracteres</span><span class="sxs-lookup"><span data-stu-id="7263e-220">array of strings</span></span> | <span data-ttu-id="7263e-221">sim</span><span class="sxs-lookup"><span data-stu-id="7263e-221">yes</span></span>      | <span data-ttu-id="7263e-222">As versões do pacote correspondidas pela solicitação</span><span class="sxs-lookup"><span data-stu-id="7263e-222">The package versions matched by the request</span></span>

<span data-ttu-id="7263e-223">As versões do pacote a `data` matriz pode conter metadados de compilação de SemVer 2.0.0 (por exemplo, `1.0.0+metadata`) se o `semVerLevel=2.0.0` foi fornecido na cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="7263e-223">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="7263e-224">Exemplo de solicitação</span><span class="sxs-lookup"><span data-stu-id="7263e-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="7263e-225">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="7263e-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
