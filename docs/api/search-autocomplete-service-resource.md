---
title: Preenchimento automático, o NuGet API
description: O serviço de preenchimento automático de pesquisa oferece suporte a versões e descoberta interativa de IDs de pacote.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d5e1936c6c5406a1a376c16b2bad5351320dfb4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822130"
---
# <a name="autocomplete"></a><span data-ttu-id="72422-103">Preenchimento Automático</span><span class="sxs-lookup"><span data-stu-id="72422-103">Autocomplete</span></span>

<span data-ttu-id="72422-104">É possível criar um pacote ID e a versão AutoCompletar experiência usando a API V3.</span><span class="sxs-lookup"><span data-stu-id="72422-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="72422-105">O recurso usado para fazer consultas de preenchimento automático é o `SearchAutocompleteService` recurso encontrado na [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="72422-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="72422-106">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="72422-106">Versioning</span></span>

<span data-ttu-id="72422-107">O seguinte `@type` valores são usados:</span><span class="sxs-lookup"><span data-stu-id="72422-107">The following `@type` values are used:</span></span>

<span data-ttu-id="72422-108">Valor @type</span><span class="sxs-lookup"><span data-stu-id="72422-108">@type value</span></span>                          | <span data-ttu-id="72422-109">Observações</span><span class="sxs-lookup"><span data-stu-id="72422-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="72422-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="72422-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="72422-111">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="72422-111">The initial release</span></span>
<span data-ttu-id="72422-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="72422-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="72422-113">Alias de `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="72422-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="72422-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="72422-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="72422-115">Alias de `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="72422-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="72422-116">URL Base</span><span class="sxs-lookup"><span data-stu-id="72422-116">Base URL</span></span>

<span data-ttu-id="72422-117">A URL base para as seguintes APIs é o valor da `@id` propriedade associada a um recurso mencionados acima `@type` valores.</span><span class="sxs-lookup"><span data-stu-id="72422-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="72422-118">No documento a seguir, a URL base do espaço reservado `{@id}` será usado.</span><span class="sxs-lookup"><span data-stu-id="72422-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="72422-119">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="72422-119">HTTP Methods</span></span>

<span data-ttu-id="72422-120">Todas as URLs encontradas no suporte a recurso de registro os métodos HTTP `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="72422-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="72422-121">Pesquise IDs de pacote</span><span class="sxs-lookup"><span data-stu-id="72422-121">Search for package IDs</span></span>

<span data-ttu-id="72422-122">O preenchimento automático de primeira API dá suporte ao procurar por parte de uma cadeia de caracteres de ID do pacote.</span><span class="sxs-lookup"><span data-stu-id="72422-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="72422-123">Isso é ótimo quando você deseja fornecer um recurso de typeahead do pacote em uma interface de usuário integrada com uma origem de pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="72422-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="72422-124">Um pacote com apenas as versões não aparecerão nos resultados.</span><span class="sxs-lookup"><span data-stu-id="72422-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="72422-125">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="72422-125">Request parameters</span></span>

<span data-ttu-id="72422-126">Nome</span><span class="sxs-lookup"><span data-stu-id="72422-126">Name</span></span>        | <span data-ttu-id="72422-127">No</span><span class="sxs-lookup"><span data-stu-id="72422-127">In</span></span>     | <span data-ttu-id="72422-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="72422-128">Type</span></span>    | <span data-ttu-id="72422-129">Necessária</span><span class="sxs-lookup"><span data-stu-id="72422-129">Required</span></span> | <span data-ttu-id="72422-130">Observações</span><span class="sxs-lookup"><span data-stu-id="72422-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="72422-131">q</span><span class="sxs-lookup"><span data-stu-id="72422-131">q</span></span>           | <span data-ttu-id="72422-132">URL</span><span class="sxs-lookup"><span data-stu-id="72422-132">URL</span></span>    | <span data-ttu-id="72422-133">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="72422-133">string</span></span>  | <span data-ttu-id="72422-134">no</span><span class="sxs-lookup"><span data-stu-id="72422-134">no</span></span>       | <span data-ttu-id="72422-135">A cadeia de caracteres a ser comparada com IDs de pacote</span><span class="sxs-lookup"><span data-stu-id="72422-135">The string to compare against package IDs</span></span>
<span data-ttu-id="72422-136">skip</span><span class="sxs-lookup"><span data-stu-id="72422-136">skip</span></span>        | <span data-ttu-id="72422-137">URL</span><span class="sxs-lookup"><span data-stu-id="72422-137">URL</span></span>    | <span data-ttu-id="72422-138">inteiro</span><span class="sxs-lookup"><span data-stu-id="72422-138">integer</span></span> | <span data-ttu-id="72422-139">no</span><span class="sxs-lookup"><span data-stu-id="72422-139">no</span></span>       | <span data-ttu-id="72422-140">O número de resultados a ignorar, de paginação</span><span class="sxs-lookup"><span data-stu-id="72422-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="72422-141">Take</span><span class="sxs-lookup"><span data-stu-id="72422-141">take</span></span>        | <span data-ttu-id="72422-142">URL</span><span class="sxs-lookup"><span data-stu-id="72422-142">URL</span></span>    | <span data-ttu-id="72422-143">inteiro</span><span class="sxs-lookup"><span data-stu-id="72422-143">integer</span></span> | <span data-ttu-id="72422-144">no</span><span class="sxs-lookup"><span data-stu-id="72422-144">no</span></span>       | <span data-ttu-id="72422-145">O número de resultados para retornar para a paginação</span><span class="sxs-lookup"><span data-stu-id="72422-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="72422-146">versão de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="72422-146">prerelease</span></span>  | <span data-ttu-id="72422-147">URL</span><span class="sxs-lookup"><span data-stu-id="72422-147">URL</span></span>    | <span data-ttu-id="72422-148">boolean</span><span class="sxs-lookup"><span data-stu-id="72422-148">boolean</span></span> | <span data-ttu-id="72422-149">no</span><span class="sxs-lookup"><span data-stu-id="72422-149">no</span></span>       | <span data-ttu-id="72422-150">`true` ou `false` determinar a inclusão [pacotes de pré-lançamento](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="72422-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="72422-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="72422-151">semVerLevel</span></span> | <span data-ttu-id="72422-152">URL</span><span class="sxs-lookup"><span data-stu-id="72422-152">URL</span></span>    | <span data-ttu-id="72422-153">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="72422-153">string</span></span>  | <span data-ttu-id="72422-154">no</span><span class="sxs-lookup"><span data-stu-id="72422-154">no</span></span>       | <span data-ttu-id="72422-155">Uma cadeia de caracteres de versão SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="72422-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="72422-156">A consulta de preenchimento automático `q` é analisado em uma maneira que é definida pela implementação do servidor.</span><span class="sxs-lookup"><span data-stu-id="72422-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="72422-157">NuGet.org oferece suporte a consultas para o prefixo de tokens de ID de pacote, que fazem parte da ID produzido pelo spliting original por caracteres mista de caso e o símbolo.</span><span class="sxs-lookup"><span data-stu-id="72422-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="72422-158">O `skip` parâmetro padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="72422-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="72422-159">O `take` parâmetro deve ser um inteiro maior que zero.</span><span class="sxs-lookup"><span data-stu-id="72422-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="72422-160">A implementação do servidor pode impor um valor máximo.</span><span class="sxs-lookup"><span data-stu-id="72422-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="72422-161">Se `prerelease` não for fornecido, os pacotes de pré-lançamento serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="72422-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="72422-162">O `semVerLevel` parâmetro de consulta é usado para aceitar [SemVer 2.0.0 pacotes](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="72422-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="72422-163">Se esse parâmetro de consulta é excluído, IDs de pacote somente com as versões compatíveis do SemVer 1.0.0 será retornado (com o [padrão controle de versão do NuGet](../reference/package-versioning.md) limitações, como cadeias de caracteres de versão com 4 partes de inteiro).</span><span class="sxs-lookup"><span data-stu-id="72422-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="72422-164">Se `semVerLevel=2.0.0` for fornecido, SemVer 1.0.0 e pacotes compatíveis SemVer 2.0.0 serão retornados.</span><span class="sxs-lookup"><span data-stu-id="72422-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="72422-165">Consulte o [suporte SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="72422-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="72422-166">Resposta</span><span class="sxs-lookup"><span data-stu-id="72422-166">Response</span></span>

<span data-ttu-id="72422-167">A resposta é documento JSON que contém até `take` resultados de preenchimento automático.</span><span class="sxs-lookup"><span data-stu-id="72422-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="72422-168">A raiz do objeto JSON tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="72422-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="72422-169">Nome</span><span class="sxs-lookup"><span data-stu-id="72422-169">Name</span></span>      | <span data-ttu-id="72422-170">Tipo</span><span class="sxs-lookup"><span data-stu-id="72422-170">Type</span></span>             | <span data-ttu-id="72422-171">Necessária</span><span class="sxs-lookup"><span data-stu-id="72422-171">Required</span></span> | <span data-ttu-id="72422-172">Observações</span><span class="sxs-lookup"><span data-stu-id="72422-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="72422-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="72422-173">totalHits</span></span> | <span data-ttu-id="72422-174">inteiro</span><span class="sxs-lookup"><span data-stu-id="72422-174">integer</span></span>          | <span data-ttu-id="72422-175">sim</span><span class="sxs-lookup"><span data-stu-id="72422-175">yes</span></span>      | <span data-ttu-id="72422-176">O número total de correspondências, desconsiderando `skip` e `take`</span><span class="sxs-lookup"><span data-stu-id="72422-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="72422-177">Dados</span><span class="sxs-lookup"><span data-stu-id="72422-177">data</span></span>      | <span data-ttu-id="72422-178">Matriz de cadeias de caracteres</span><span class="sxs-lookup"><span data-stu-id="72422-178">array of strings</span></span> | <span data-ttu-id="72422-179">sim</span><span class="sxs-lookup"><span data-stu-id="72422-179">yes</span></span>      | <span data-ttu-id="72422-180">O pacote correspondem às IDs de solicitação</span><span class="sxs-lookup"><span data-stu-id="72422-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="72422-181">Solicitação de amostra</span><span class="sxs-lookup"><span data-stu-id="72422-181">Sample request</span></span>

<span data-ttu-id="72422-182">OBTER https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="72422-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="72422-183">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="72422-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="72422-184">Enumerar as versões do pacote</span><span class="sxs-lookup"><span data-stu-id="72422-184">Enumerate package versions</span></span>

<span data-ttu-id="72422-185">Depois que uma ID de pacote for descoberta usando a API anterior, um cliente pode usar o API de preenchimento automático para enumerar as versões do pacote para uma ID do pacote fornecido.</span><span class="sxs-lookup"><span data-stu-id="72422-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="72422-186">Uma versão do pacote que está na lista não aparecerão nos resultados.</span><span class="sxs-lookup"><span data-stu-id="72422-186">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="72422-187">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="72422-187">Request parameters</span></span>

<span data-ttu-id="72422-188">Nome</span><span class="sxs-lookup"><span data-stu-id="72422-188">Name</span></span>        | <span data-ttu-id="72422-189">No</span><span class="sxs-lookup"><span data-stu-id="72422-189">In</span></span>     | <span data-ttu-id="72422-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="72422-190">Type</span></span>    | <span data-ttu-id="72422-191">Necessária</span><span class="sxs-lookup"><span data-stu-id="72422-191">Required</span></span> | <span data-ttu-id="72422-192">Observações</span><span class="sxs-lookup"><span data-stu-id="72422-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="72422-193">id</span><span class="sxs-lookup"><span data-stu-id="72422-193">id</span></span>          | <span data-ttu-id="72422-194">URL</span><span class="sxs-lookup"><span data-stu-id="72422-194">URL</span></span>    | <span data-ttu-id="72422-195">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="72422-195">string</span></span>  | <span data-ttu-id="72422-196">sim</span><span class="sxs-lookup"><span data-stu-id="72422-196">yes</span></span>      | <span data-ttu-id="72422-197">A ID do pacote para buscar versões para</span><span class="sxs-lookup"><span data-stu-id="72422-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="72422-198">versão de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="72422-198">prerelease</span></span>  | <span data-ttu-id="72422-199">URL</span><span class="sxs-lookup"><span data-stu-id="72422-199">URL</span></span>    | <span data-ttu-id="72422-200">boolean</span><span class="sxs-lookup"><span data-stu-id="72422-200">boolean</span></span> | <span data-ttu-id="72422-201">no</span><span class="sxs-lookup"><span data-stu-id="72422-201">no</span></span>       | <span data-ttu-id="72422-202">`true` ou `false` determinar a inclusão [pacotes de pré-lançamento](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="72422-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="72422-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="72422-203">semVerLevel</span></span> | <span data-ttu-id="72422-204">URL</span><span class="sxs-lookup"><span data-stu-id="72422-204">URL</span></span>    | <span data-ttu-id="72422-205">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="72422-205">string</span></span>  | <span data-ttu-id="72422-206">no</span><span class="sxs-lookup"><span data-stu-id="72422-206">no</span></span>       | <span data-ttu-id="72422-207">Uma cadeia de caracteres de versão SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="72422-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="72422-208">Se `prerelease` não for fornecido, os pacotes de pré-lançamento serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="72422-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="72422-209">O `semVerLevel` parâmetro de consulta é usado para aceitar a SemVer 2.0.0 pacotes.</span><span class="sxs-lookup"><span data-stu-id="72422-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="72422-210">Se esse parâmetro de consulta é excluído, apenas as versões SemVer 1.0.0 serão retornadas.</span><span class="sxs-lookup"><span data-stu-id="72422-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="72422-211">Se `semVerLevel=2.0.0` for fornecido, SemVer 1.0.0 e SemVer 2.0.0 versões serão retornadas.</span><span class="sxs-lookup"><span data-stu-id="72422-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="72422-212">Consulte o [suporte SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="72422-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="72422-213">Resposta</span><span class="sxs-lookup"><span data-stu-id="72422-213">Response</span></span>

<span data-ttu-id="72422-214">A resposta é documento JSON que contém todas as versões do pacote da ID do pacote fornecido, filtrando os parâmetros de consulta.</span><span class="sxs-lookup"><span data-stu-id="72422-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="72422-215">A raiz do objeto JSON tem a seguinte propriedade:</span><span class="sxs-lookup"><span data-stu-id="72422-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="72422-216">Nome</span><span class="sxs-lookup"><span data-stu-id="72422-216">Name</span></span>      | <span data-ttu-id="72422-217">Tipo</span><span class="sxs-lookup"><span data-stu-id="72422-217">Type</span></span>             | <span data-ttu-id="72422-218">Necessária</span><span class="sxs-lookup"><span data-stu-id="72422-218">Required</span></span> | <span data-ttu-id="72422-219">Observações</span><span class="sxs-lookup"><span data-stu-id="72422-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="72422-220">Dados</span><span class="sxs-lookup"><span data-stu-id="72422-220">data</span></span>      | <span data-ttu-id="72422-221">Matriz de cadeias de caracteres</span><span class="sxs-lookup"><span data-stu-id="72422-221">array of strings</span></span> | <span data-ttu-id="72422-222">sim</span><span class="sxs-lookup"><span data-stu-id="72422-222">yes</span></span>      | <span data-ttu-id="72422-223">As versões do pacote correspondidas a solicitação</span><span class="sxs-lookup"><span data-stu-id="72422-223">The package versions matched by the request</span></span>

<span data-ttu-id="72422-224">As versões do pacote no `data` matriz pode conter metadados de compilação SemVer 2.0.0 (por exemplo, `1.0.0+metadata`) se o `semVerLevel=2.0.0` foi fornecido na cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="72422-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="72422-225">Solicitação de amostra</span><span class="sxs-lookup"><span data-stu-id="72422-225">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="72422-226">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="72422-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
