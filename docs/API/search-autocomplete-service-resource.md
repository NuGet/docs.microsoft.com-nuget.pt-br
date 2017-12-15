---
title: "Preenchimento automático, o NuGet API | Microsoft Docs"
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
ms.assetid: ead5cf7a-e51e-4cbb-8798-58226f4c853f
description: "O serviço de preenchimento automático de pesquisa oferece suporte a versões e descoberta interativa de IDs de pacote."
keywords: "API de preenchimento automático do NuGet, NuGet pacote ID, ID de pacote de subcadeia de caracteres de pesquisa"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 313ceb630947b46c34b98e14044ecf121b725087
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="autocomplete"></a><span data-ttu-id="ea527-104">Preenchimento Automático</span><span class="sxs-lookup"><span data-stu-id="ea527-104">Autocomplete</span></span>

<span data-ttu-id="ea527-105">É possível criar um pacote ID e a versão AutoCompletar experiência usando a API V3.</span><span class="sxs-lookup"><span data-stu-id="ea527-105">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="ea527-106">O recurso usado para fazer consultas de preenchimento automático é o `SearchAutocompleteService` recurso encontrado na [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="ea527-106">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="ea527-107">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="ea527-107">Versioning</span></span>

<span data-ttu-id="ea527-108">O seguinte `@type` valores são usados:</span><span class="sxs-lookup"><span data-stu-id="ea527-108">The following `@type` values are used:</span></span>

<span data-ttu-id="ea527-109">Valor @type</span><span class="sxs-lookup"><span data-stu-id="ea527-109">@type value</span></span>                          | <span data-ttu-id="ea527-110">Observações</span><span class="sxs-lookup"><span data-stu-id="ea527-110">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="ea527-111">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="ea527-111">SearchAutocompleteService</span></span>            | <span data-ttu-id="ea527-112">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="ea527-112">The initial release</span></span>
<span data-ttu-id="ea527-113">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="ea527-113">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="ea527-114">Alias de`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="ea527-114">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="ea527-115">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="ea527-115">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="ea527-116">Alias de`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="ea527-116">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="ea527-117">URL Base</span><span class="sxs-lookup"><span data-stu-id="ea527-117">Base URL</span></span>

<span data-ttu-id="ea527-118">A URL base para as seguintes APIs é o valor da `@id` propriedade associada a um recurso mencionados acima `@type` valores.</span><span class="sxs-lookup"><span data-stu-id="ea527-118">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="ea527-119">No documento a seguir, a URL base do espaço reservado `{@id}` será usado.</span><span class="sxs-lookup"><span data-stu-id="ea527-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="ea527-120">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="ea527-120">HTTP Methods</span></span>

<span data-ttu-id="ea527-121">Todas as URLs encontradas no suporte a recurso de registro os métodos HTTP `GET` e `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="ea527-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="ea527-122">Pesquise IDs de pacote</span><span class="sxs-lookup"><span data-stu-id="ea527-122">Search for package IDs</span></span>

<span data-ttu-id="ea527-123">O preenchimento automático de primeira API dá suporte ao procurar por parte de uma cadeia de caracteres de ID do pacote.</span><span class="sxs-lookup"><span data-stu-id="ea527-123">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="ea527-124">Isso é ótimo quando você deseja fornecer um recurso de typeahead do pacote em uma interface de usuário integrada com uma origem de pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="ea527-124">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="ea527-125">Um pacote com apenas as versões não aparecerão nos resultados.</span><span class="sxs-lookup"><span data-stu-id="ea527-125">A package with only unlisted versions will not appear in the results.</span></span>

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="ea527-126">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="ea527-126">Request parameters</span></span>

<span data-ttu-id="ea527-127">Nome</span><span class="sxs-lookup"><span data-stu-id="ea527-127">Name</span></span>        | <span data-ttu-id="ea527-128">No</span><span class="sxs-lookup"><span data-stu-id="ea527-128">In</span></span>     | <span data-ttu-id="ea527-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="ea527-129">Type</span></span>    | <span data-ttu-id="ea527-130">Necessária</span><span class="sxs-lookup"><span data-stu-id="ea527-130">Required</span></span> | <span data-ttu-id="ea527-131">Observações</span><span class="sxs-lookup"><span data-stu-id="ea527-131">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="ea527-132">q</span><span class="sxs-lookup"><span data-stu-id="ea527-132">q</span></span>           | <span data-ttu-id="ea527-133">URL</span><span class="sxs-lookup"><span data-stu-id="ea527-133">URL</span></span>    | <span data-ttu-id="ea527-134">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="ea527-134">string</span></span>  | <span data-ttu-id="ea527-135">no</span><span class="sxs-lookup"><span data-stu-id="ea527-135">no</span></span>       | <span data-ttu-id="ea527-136">A cadeia de caracteres a ser comparada com IDs de pacote</span><span class="sxs-lookup"><span data-stu-id="ea527-136">The string to compare against package IDs</span></span>
<span data-ttu-id="ea527-137">skip</span><span class="sxs-lookup"><span data-stu-id="ea527-137">skip</span></span>        | <span data-ttu-id="ea527-138">URL</span><span class="sxs-lookup"><span data-stu-id="ea527-138">URL</span></span>    | <span data-ttu-id="ea527-139">inteiro</span><span class="sxs-lookup"><span data-stu-id="ea527-139">integer</span></span> | <span data-ttu-id="ea527-140">no</span><span class="sxs-lookup"><span data-stu-id="ea527-140">no</span></span>       | <span data-ttu-id="ea527-141">O número de resultados a ignorar, de paginação</span><span class="sxs-lookup"><span data-stu-id="ea527-141">The number of results to skip, for pagination</span></span>
<span data-ttu-id="ea527-142">Take</span><span class="sxs-lookup"><span data-stu-id="ea527-142">take</span></span>        | <span data-ttu-id="ea527-143">URL</span><span class="sxs-lookup"><span data-stu-id="ea527-143">URL</span></span>    | <span data-ttu-id="ea527-144">inteiro</span><span class="sxs-lookup"><span data-stu-id="ea527-144">integer</span></span> | <span data-ttu-id="ea527-145">no</span><span class="sxs-lookup"><span data-stu-id="ea527-145">no</span></span>       | <span data-ttu-id="ea527-146">O número de resultados para retornar para a paginação</span><span class="sxs-lookup"><span data-stu-id="ea527-146">The number of results to return, for pagination</span></span>
<span data-ttu-id="ea527-147">versão de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="ea527-147">prerelease</span></span>  | <span data-ttu-id="ea527-148">URL</span><span class="sxs-lookup"><span data-stu-id="ea527-148">URL</span></span>    | <span data-ttu-id="ea527-149">boolean</span><span class="sxs-lookup"><span data-stu-id="ea527-149">boolean</span></span> | <span data-ttu-id="ea527-150">no</span><span class="sxs-lookup"><span data-stu-id="ea527-150">no</span></span>       | <span data-ttu-id="ea527-151">`true`ou `false` determinar a inclusão [pacotes de pré-lançamento](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="ea527-151">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="ea527-152">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="ea527-152">semVerLevel</span></span> | <span data-ttu-id="ea527-153">URL</span><span class="sxs-lookup"><span data-stu-id="ea527-153">URL</span></span>    | <span data-ttu-id="ea527-154">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="ea527-154">string</span></span>  | <span data-ttu-id="ea527-155">no</span><span class="sxs-lookup"><span data-stu-id="ea527-155">no</span></span>       | <span data-ttu-id="ea527-156">Uma cadeia de caracteres de versão SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="ea527-156">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="ea527-157">A consulta de preenchimento automático `q` é analisado em uma maneira que é definida pela implementação do servidor.</span><span class="sxs-lookup"><span data-stu-id="ea527-157">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="ea527-158">NuGet.org oferece suporte a consultas para o prefixo de tokens de ID de pacote, que fazem parte da ID produzido pelo spliting original por caracteres mista de caso e o símbolo.</span><span class="sxs-lookup"><span data-stu-id="ea527-158">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="ea527-159">O `skip` parâmetro padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="ea527-159">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="ea527-160">O `take` parâmetro deve ser um inteiro maior que zero.</span><span class="sxs-lookup"><span data-stu-id="ea527-160">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="ea527-161">A implementação do servidor pode impor um valor máximo.</span><span class="sxs-lookup"><span data-stu-id="ea527-161">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="ea527-162">Se `prerelease` não for fornecido, os pacotes de pré-lançamento serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="ea527-162">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="ea527-163">O `semVerLevel` parâmetro de consulta é usado para aceitar [SemVer 2.0.0 pacotes](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="ea527-163">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="ea527-164">Se esse parâmetro de consulta é excluído, IDs de pacote somente com as versões compatíveis do SemVer 1.0.0 será retornado (com o [padrão controle de versão do NuGet](../reference/package-versioning.md) limitações, como cadeias de caracteres de versão com 4 partes de inteiro).</span><span class="sxs-lookup"><span data-stu-id="ea527-164">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="ea527-165">Se `semVerLevel=2.0.0` for fornecido, SemVer 1.0.0 e pacotes compatíveis SemVer 2.0.0 serão retornados.</span><span class="sxs-lookup"><span data-stu-id="ea527-165">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="ea527-166">Consulte o [suporte SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="ea527-166">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="ea527-167">Resposta</span><span class="sxs-lookup"><span data-stu-id="ea527-167">Response</span></span>

<span data-ttu-id="ea527-168">A resposta é documento JSON que contém até `take` resultados de preenchimento automático.</span><span class="sxs-lookup"><span data-stu-id="ea527-168">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="ea527-169">A raiz do objeto JSON tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="ea527-169">The root JSON object has the following properties:</span></span>

<span data-ttu-id="ea527-170">Nome</span><span class="sxs-lookup"><span data-stu-id="ea527-170">Name</span></span>      | <span data-ttu-id="ea527-171">Tipo</span><span class="sxs-lookup"><span data-stu-id="ea527-171">Type</span></span>             | <span data-ttu-id="ea527-172">Necessária</span><span class="sxs-lookup"><span data-stu-id="ea527-172">Required</span></span> | <span data-ttu-id="ea527-173">Observações</span><span class="sxs-lookup"><span data-stu-id="ea527-173">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="ea527-174">totalHits</span><span class="sxs-lookup"><span data-stu-id="ea527-174">totalHits</span></span> | <span data-ttu-id="ea527-175">inteiro</span><span class="sxs-lookup"><span data-stu-id="ea527-175">integer</span></span>          | <span data-ttu-id="ea527-176">sim</span><span class="sxs-lookup"><span data-stu-id="ea527-176">yes</span></span>      | <span data-ttu-id="ea527-177">O número total de correspondências, desconsiderando `skip` e`take`</span><span class="sxs-lookup"><span data-stu-id="ea527-177">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="ea527-178">Dados</span><span class="sxs-lookup"><span data-stu-id="ea527-178">data</span></span>      | <span data-ttu-id="ea527-179">Matriz de cadeias de caracteres</span><span class="sxs-lookup"><span data-stu-id="ea527-179">array of strings</span></span> | <span data-ttu-id="ea527-180">sim</span><span class="sxs-lookup"><span data-stu-id="ea527-180">yes</span></span>      | <span data-ttu-id="ea527-181">O pacote correspondem às IDs de solicitação</span><span class="sxs-lookup"><span data-stu-id="ea527-181">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="ea527-182">Solicitação de amostra</span><span class="sxs-lookup"><span data-stu-id="ea527-182">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="ea527-183">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="ea527-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="ea527-184">Enumerar as versões do pacote</span><span class="sxs-lookup"><span data-stu-id="ea527-184">Enumerate package versions</span></span>

<span data-ttu-id="ea527-185">Depois que uma ID de pacote for descoberta usando a API anterior, um cliente pode usar o API de preenchimento automático para enumerar as versões do pacote para uma ID do pacote fornecido.</span><span class="sxs-lookup"><span data-stu-id="ea527-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="ea527-186">Uma versão do pacote que está na lista não aparecerão nos resultados.</span><span class="sxs-lookup"><span data-stu-id="ea527-186">A package version that is unlisted will not appear in the results.</span></span>

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="ea527-187">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="ea527-187">Request parameters</span></span>

<span data-ttu-id="ea527-188">Nome</span><span class="sxs-lookup"><span data-stu-id="ea527-188">Name</span></span>        | <span data-ttu-id="ea527-189">No</span><span class="sxs-lookup"><span data-stu-id="ea527-189">In</span></span>     | <span data-ttu-id="ea527-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="ea527-190">Type</span></span>    | <span data-ttu-id="ea527-191">Necessária</span><span class="sxs-lookup"><span data-stu-id="ea527-191">Required</span></span> | <span data-ttu-id="ea527-192">Observações</span><span class="sxs-lookup"><span data-stu-id="ea527-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="ea527-193">id</span><span class="sxs-lookup"><span data-stu-id="ea527-193">id</span></span>          | <span data-ttu-id="ea527-194">URL</span><span class="sxs-lookup"><span data-stu-id="ea527-194">URL</span></span>    | <span data-ttu-id="ea527-195">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="ea527-195">string</span></span>  | <span data-ttu-id="ea527-196">sim</span><span class="sxs-lookup"><span data-stu-id="ea527-196">yes</span></span>      | <span data-ttu-id="ea527-197">A ID do pacote para buscar versões para</span><span class="sxs-lookup"><span data-stu-id="ea527-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="ea527-198">versão de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="ea527-198">prerelease</span></span>  | <span data-ttu-id="ea527-199">URL</span><span class="sxs-lookup"><span data-stu-id="ea527-199">URL</span></span>    | <span data-ttu-id="ea527-200">boolean</span><span class="sxs-lookup"><span data-stu-id="ea527-200">boolean</span></span> | <span data-ttu-id="ea527-201">no</span><span class="sxs-lookup"><span data-stu-id="ea527-201">no</span></span>       | <span data-ttu-id="ea527-202">`true`ou `false` determinar a inclusão [pacotes de pré-lançamento](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="ea527-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="ea527-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="ea527-203">semVerLevel</span></span> | <span data-ttu-id="ea527-204">URL</span><span class="sxs-lookup"><span data-stu-id="ea527-204">URL</span></span>    | <span data-ttu-id="ea527-205">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="ea527-205">string</span></span>  | <span data-ttu-id="ea527-206">no</span><span class="sxs-lookup"><span data-stu-id="ea527-206">no</span></span>       | <span data-ttu-id="ea527-207">Uma cadeia de caracteres de versão SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="ea527-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="ea527-208">Se `prerelease` não for fornecido, os pacotes de pré-lançamento serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="ea527-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="ea527-209">O `semVerLevel` parâmetro de consulta é usado para aceitar a SemVer 2.0.0 pacotes.</span><span class="sxs-lookup"><span data-stu-id="ea527-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="ea527-210">Se esse parâmetro de consulta é excluído, apenas as versões SemVer 1.0.0 serão retornadas.</span><span class="sxs-lookup"><span data-stu-id="ea527-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="ea527-211">Se `semVerLevel=2.0.0` for fornecido, SemVer 1.0.0 e SemVer 2.0.0 versões serão retornadas.</span><span class="sxs-lookup"><span data-stu-id="ea527-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="ea527-212">Consulte o [suporte SemVer 2.0.0 nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="ea527-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="ea527-213">Resposta</span><span class="sxs-lookup"><span data-stu-id="ea527-213">Response</span></span>

<span data-ttu-id="ea527-214">A resposta é documento JSON que contém todas as versões do pacote da ID do pacote fornecido, filtrando os parâmetros de consulta.</span><span class="sxs-lookup"><span data-stu-id="ea527-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="ea527-215">A raiz do objeto JSON tem a seguinte propriedade:</span><span class="sxs-lookup"><span data-stu-id="ea527-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="ea527-216">Nome</span><span class="sxs-lookup"><span data-stu-id="ea527-216">Name</span></span>      | <span data-ttu-id="ea527-217">Tipo</span><span class="sxs-lookup"><span data-stu-id="ea527-217">Type</span></span>             | <span data-ttu-id="ea527-218">Necessária</span><span class="sxs-lookup"><span data-stu-id="ea527-218">Required</span></span> | <span data-ttu-id="ea527-219">Observações</span><span class="sxs-lookup"><span data-stu-id="ea527-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="ea527-220">Dados</span><span class="sxs-lookup"><span data-stu-id="ea527-220">data</span></span>      | <span data-ttu-id="ea527-221">Matriz de cadeias de caracteres</span><span class="sxs-lookup"><span data-stu-id="ea527-221">array of strings</span></span> | <span data-ttu-id="ea527-222">sim</span><span class="sxs-lookup"><span data-stu-id="ea527-222">yes</span></span>      | <span data-ttu-id="ea527-223">As versões do pacote correspondidas a solicitação</span><span class="sxs-lookup"><span data-stu-id="ea527-223">The package versions matched by the request</span></span>

<span data-ttu-id="ea527-224">As versões do pacote no `data` matriz pode conter metadados de compilação SemVer 2.0.0 (por exemplo, `1.0.0+metadata`) se o `semVerLevel=2.0.0` foi fornecido na cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="ea527-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="ea527-225">Solicitação de amostra</span><span class="sxs-lookup"><span data-stu-id="ea527-225">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="ea527-226">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="ea527-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
