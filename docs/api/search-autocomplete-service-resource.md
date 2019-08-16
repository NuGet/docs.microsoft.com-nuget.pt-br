---
title: Preenchimento automático, API do NuGet
description: O serviço de preenchimento automático de pesquisa dá suporte à descoberta interativa de IDs e versões de pacote.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488301"
---
# <a name="autocomplete"></a><span data-ttu-id="17dae-103">Preenchimento Automático</span><span class="sxs-lookup"><span data-stu-id="17dae-103">Autocomplete</span></span>

<span data-ttu-id="17dae-104">É possível criar uma ID do pacote e uma experiência de preenchimento automático da versão usando a API v3.</span><span class="sxs-lookup"><span data-stu-id="17dae-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="17dae-105">O recurso usado para fazer consultas de preenchimento automático é `SearchAutocompleteService` o recurso encontrado no [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="17dae-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="17dae-106">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="17dae-106">Versioning</span></span>

<span data-ttu-id="17dae-107">Os seguintes `@type` valores são usados:</span><span class="sxs-lookup"><span data-stu-id="17dae-107">The following `@type` values are used:</span></span>

<span data-ttu-id="17dae-108">Valor @type</span><span class="sxs-lookup"><span data-stu-id="17dae-108">@type value</span></span>                          | <span data-ttu-id="17dae-109">Observações</span><span class="sxs-lookup"><span data-stu-id="17dae-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="17dae-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="17dae-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="17dae-111">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="17dae-111">The initial release</span></span>
<span data-ttu-id="17dae-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="17dae-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="17dae-113">Alias of `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="17dae-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="17dae-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="17dae-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="17dae-115">Alias of `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="17dae-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="17dae-116">URL Base</span><span class="sxs-lookup"><span data-stu-id="17dae-116">Base URL</span></span>

<span data-ttu-id="17dae-117">A URL base para as APIs a seguir é o valor da `@id` propriedade associada a um dos valores de recurso `@type` mencionados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="17dae-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="17dae-118">No documento a seguir, a URL `{@id}` base do espaço reservado será usada.</span><span class="sxs-lookup"><span data-stu-id="17dae-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="17dae-119">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="17dae-119">HTTP Methods</span></span>

<span data-ttu-id="17dae-120">Todas as URLs encontradas no recurso de registro dão suporte aos `GET` métodos `HEAD`http e.</span><span class="sxs-lookup"><span data-stu-id="17dae-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="17dae-121">Pesquisar por IDs de pacote</span><span class="sxs-lookup"><span data-stu-id="17dae-121">Search for package IDs</span></span>

<span data-ttu-id="17dae-122">A primeira API de preenchimento automático dá suporte à pesquisa de parte de uma cadeia de caracteres de ID de pacote.</span><span class="sxs-lookup"><span data-stu-id="17dae-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="17dae-123">Isso é ótimo quando você deseja fornecer um recurso typeahead de pacote em uma interface de usuário integrada com uma origem de pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="17dae-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="17dae-124">Um pacote com apenas versões não listadas não será exibido nos resultados.</span><span class="sxs-lookup"><span data-stu-id="17dae-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="17dae-125">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="17dae-125">Request parameters</span></span>

<span data-ttu-id="17dae-126">Nome</span><span class="sxs-lookup"><span data-stu-id="17dae-126">Name</span></span>        | <span data-ttu-id="17dae-127">No</span><span class="sxs-lookup"><span data-stu-id="17dae-127">In</span></span>     | <span data-ttu-id="17dae-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="17dae-128">Type</span></span>    | <span data-ttu-id="17dae-129">Necessária</span><span class="sxs-lookup"><span data-stu-id="17dae-129">Required</span></span> | <span data-ttu-id="17dae-130">Observações</span><span class="sxs-lookup"><span data-stu-id="17dae-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="17dae-131">q</span><span class="sxs-lookup"><span data-stu-id="17dae-131">q</span></span>           | <span data-ttu-id="17dae-132">URL</span><span class="sxs-lookup"><span data-stu-id="17dae-132">URL</span></span>    | <span data-ttu-id="17dae-133">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="17dae-133">string</span></span>  | <span data-ttu-id="17dae-134">no</span><span class="sxs-lookup"><span data-stu-id="17dae-134">no</span></span>       | <span data-ttu-id="17dae-135">A cadeia de caracteres para comparar com as IDs de pacote</span><span class="sxs-lookup"><span data-stu-id="17dae-135">The string to compare against package IDs</span></span>
<span data-ttu-id="17dae-136">skip</span><span class="sxs-lookup"><span data-stu-id="17dae-136">skip</span></span>        | <span data-ttu-id="17dae-137">URL</span><span class="sxs-lookup"><span data-stu-id="17dae-137">URL</span></span>    | <span data-ttu-id="17dae-138">inteiro</span><span class="sxs-lookup"><span data-stu-id="17dae-138">integer</span></span> | <span data-ttu-id="17dae-139">no</span><span class="sxs-lookup"><span data-stu-id="17dae-139">no</span></span>       | <span data-ttu-id="17dae-140">O número de resultados a serem ignorados, para paginação</span><span class="sxs-lookup"><span data-stu-id="17dae-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="17dae-141">ter</span><span class="sxs-lookup"><span data-stu-id="17dae-141">take</span></span>        | <span data-ttu-id="17dae-142">URL</span><span class="sxs-lookup"><span data-stu-id="17dae-142">URL</span></span>    | <span data-ttu-id="17dae-143">inteiro</span><span class="sxs-lookup"><span data-stu-id="17dae-143">integer</span></span> | <span data-ttu-id="17dae-144">no</span><span class="sxs-lookup"><span data-stu-id="17dae-144">no</span></span>       | <span data-ttu-id="17dae-145">O número de resultados a serem retornados, para paginação</span><span class="sxs-lookup"><span data-stu-id="17dae-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="17dae-146">pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="17dae-146">prerelease</span></span>  | <span data-ttu-id="17dae-147">URL</span><span class="sxs-lookup"><span data-stu-id="17dae-147">URL</span></span>    | <span data-ttu-id="17dae-148">boolean</span><span class="sxs-lookup"><span data-stu-id="17dae-148">boolean</span></span> | <span data-ttu-id="17dae-149">no</span><span class="sxs-lookup"><span data-stu-id="17dae-149">no</span></span>       | <span data-ttu-id="17dae-150">`true`ou `false` determinando se os [pacotes de pré-lançamento](../create-packages/prerelease-packages.md) devem ser incluídos</span><span class="sxs-lookup"><span data-stu-id="17dae-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="17dae-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="17dae-151">semVerLevel</span></span> | <span data-ttu-id="17dae-152">URL</span><span class="sxs-lookup"><span data-stu-id="17dae-152">URL</span></span>    | <span data-ttu-id="17dae-153">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="17dae-153">string</span></span>  | <span data-ttu-id="17dae-154">no</span><span class="sxs-lookup"><span data-stu-id="17dae-154">no</span></span>       | <span data-ttu-id="17dae-155">Uma cadeia de versão do SemVer 1.0.0</span><span class="sxs-lookup"><span data-stu-id="17dae-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="17dae-156">A consulta `q` de preenchimento automático é analisada de uma maneira que é definida pela implementação do servidor.</span><span class="sxs-lookup"><span data-stu-id="17dae-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="17dae-157">o nuget.org dá suporte à consulta do prefixo dos tokens de ID do pacote, que são partes da ID produzida pela divisão do original por caracteres de letras e símbolos do Camel.</span><span class="sxs-lookup"><span data-stu-id="17dae-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="17dae-158">O `skip` padrão do parâmetro é 0.</span><span class="sxs-lookup"><span data-stu-id="17dae-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="17dae-159">O `take` parâmetro deve ser um número inteiro maior que zero.</span><span class="sxs-lookup"><span data-stu-id="17dae-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="17dae-160">A implementação do servidor pode impor um valor máximo.</span><span class="sxs-lookup"><span data-stu-id="17dae-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="17dae-161">Se `prerelease` não for fornecido, os pacotes de pré-lançamento serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="17dae-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="17dae-162">O `semVerLevel` parâmetro de consulta é usado para aceitar [pacotes SemVer 2.0.0](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span><span class="sxs-lookup"><span data-stu-id="17dae-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="17dae-163">Se esse parâmetro de consulta for excluído, somente as IDs de pacote com versões compatíveis do SemVer 1.0.0 serão retornadas (com as advertências de [versão padrão do NuGet](../concepts/package-versioning.md) , como cadeias de caracteres de versão com 4 partes de inteiros).</span><span class="sxs-lookup"><span data-stu-id="17dae-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="17dae-164">Se `semVerLevel=2.0.0` for fornecido, os pacotes compatíveis SemVer 1.0.0 e SemVer 2.0.0 serão retornados.</span><span class="sxs-lookup"><span data-stu-id="17dae-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="17dae-165">Consulte o [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="17dae-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="17dae-166">Resposta</span><span class="sxs-lookup"><span data-stu-id="17dae-166">Response</span></span>

<span data-ttu-id="17dae-167">A resposta é um documento JSON que contém `take` até resultados de preenchimento automático.</span><span class="sxs-lookup"><span data-stu-id="17dae-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="17dae-168">O objeto JSON raiz tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="17dae-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="17dae-169">Nome</span><span class="sxs-lookup"><span data-stu-id="17dae-169">Name</span></span>      | <span data-ttu-id="17dae-170">Tipo</span><span class="sxs-lookup"><span data-stu-id="17dae-170">Type</span></span>             | <span data-ttu-id="17dae-171">Necessária</span><span class="sxs-lookup"><span data-stu-id="17dae-171">Required</span></span> | <span data-ttu-id="17dae-172">Observações</span><span class="sxs-lookup"><span data-stu-id="17dae-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="17dae-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="17dae-173">totalHits</span></span> | <span data-ttu-id="17dae-174">inteiro</span><span class="sxs-lookup"><span data-stu-id="17dae-174">integer</span></span>          | <span data-ttu-id="17dae-175">sim</span><span class="sxs-lookup"><span data-stu-id="17dae-175">yes</span></span>      | <span data-ttu-id="17dae-176">O número total de correspondências, desconsiderando `skip` e`take`</span><span class="sxs-lookup"><span data-stu-id="17dae-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="17dae-177">Dados</span><span class="sxs-lookup"><span data-stu-id="17dae-177">data</span></span>      | <span data-ttu-id="17dae-178">matriz de cadeias de caracteres</span><span class="sxs-lookup"><span data-stu-id="17dae-178">array of strings</span></span> | <span data-ttu-id="17dae-179">sim</span><span class="sxs-lookup"><span data-stu-id="17dae-179">yes</span></span>      | <span data-ttu-id="17dae-180">As IDs de pacote correspondentes à solicitação</span><span class="sxs-lookup"><span data-stu-id="17dae-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="17dae-181">Exemplo de solicitação</span><span class="sxs-lookup"><span data-stu-id="17dae-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="17dae-182">Exemplo de resposta</span><span class="sxs-lookup"><span data-stu-id="17dae-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="17dae-183">Enumerar versões de pacote</span><span class="sxs-lookup"><span data-stu-id="17dae-183">Enumerate package versions</span></span>

<span data-ttu-id="17dae-184">Depois que uma ID de pacote é descoberta usando a API anterior, um cliente pode usar a API de preenchimento automático para enumerar versões de pacote para uma ID de pacote fornecida.</span><span class="sxs-lookup"><span data-stu-id="17dae-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="17dae-185">Uma versão de pacote que não está listada não aparecerá nos resultados.</span><span class="sxs-lookup"><span data-stu-id="17dae-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="17dae-186">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="17dae-186">Request parameters</span></span>

<span data-ttu-id="17dae-187">Nome</span><span class="sxs-lookup"><span data-stu-id="17dae-187">Name</span></span>        | <span data-ttu-id="17dae-188">No</span><span class="sxs-lookup"><span data-stu-id="17dae-188">In</span></span>     | <span data-ttu-id="17dae-189">Tipo</span><span class="sxs-lookup"><span data-stu-id="17dae-189">Type</span></span>    | <span data-ttu-id="17dae-190">Necessária</span><span class="sxs-lookup"><span data-stu-id="17dae-190">Required</span></span> | <span data-ttu-id="17dae-191">Observações</span><span class="sxs-lookup"><span data-stu-id="17dae-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="17dae-192">id</span><span class="sxs-lookup"><span data-stu-id="17dae-192">id</span></span>          | <span data-ttu-id="17dae-193">URL</span><span class="sxs-lookup"><span data-stu-id="17dae-193">URL</span></span>    | <span data-ttu-id="17dae-194">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="17dae-194">string</span></span>  | <span data-ttu-id="17dae-195">sim</span><span class="sxs-lookup"><span data-stu-id="17dae-195">yes</span></span>      | <span data-ttu-id="17dae-196">A ID do pacote para buscar versões para</span><span class="sxs-lookup"><span data-stu-id="17dae-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="17dae-197">pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="17dae-197">prerelease</span></span>  | <span data-ttu-id="17dae-198">URL</span><span class="sxs-lookup"><span data-stu-id="17dae-198">URL</span></span>    | <span data-ttu-id="17dae-199">boolean</span><span class="sxs-lookup"><span data-stu-id="17dae-199">boolean</span></span> | <span data-ttu-id="17dae-200">no</span><span class="sxs-lookup"><span data-stu-id="17dae-200">no</span></span>       | <span data-ttu-id="17dae-201">`true`ou `false` determinando se os [pacotes de pré-lançamento](../create-packages/prerelease-packages.md) devem ser incluídos</span><span class="sxs-lookup"><span data-stu-id="17dae-201">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="17dae-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="17dae-202">semVerLevel</span></span> | <span data-ttu-id="17dae-203">URL</span><span class="sxs-lookup"><span data-stu-id="17dae-203">URL</span></span>    | <span data-ttu-id="17dae-204">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="17dae-204">string</span></span>  | <span data-ttu-id="17dae-205">no</span><span class="sxs-lookup"><span data-stu-id="17dae-205">no</span></span>       | <span data-ttu-id="17dae-206">Uma cadeia de caracteres de versão SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="17dae-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="17dae-207">Se `prerelease` não for fornecido, os pacotes de pré-lançamento serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="17dae-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="17dae-208">O `semVerLevel` parâmetro de consulta é usado para aceitar pacotes SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="17dae-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="17dae-209">Se esse parâmetro de consulta for excluído, somente as versões do SemVer 1.0.0 serão retornadas.</span><span class="sxs-lookup"><span data-stu-id="17dae-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="17dae-210">Se `semVerLevel=2.0.0` for fornecido, as versões SemVer 1.0.0 e SemVer 2.0.0 serão retornadas.</span><span class="sxs-lookup"><span data-stu-id="17dae-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="17dae-211">Consulte o [SemVer 2.0.0 support for NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="17dae-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="17dae-212">Resposta</span><span class="sxs-lookup"><span data-stu-id="17dae-212">Response</span></span>

<span data-ttu-id="17dae-213">A resposta é um documento JSON que contém todas as versões de pacote da ID de pacote fornecida, filtrando pelos parâmetros de consulta fornecidos.</span><span class="sxs-lookup"><span data-stu-id="17dae-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="17dae-214">O objeto JSON raiz tem a seguinte propriedade:</span><span class="sxs-lookup"><span data-stu-id="17dae-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="17dae-215">Nome</span><span class="sxs-lookup"><span data-stu-id="17dae-215">Name</span></span>      | <span data-ttu-id="17dae-216">Tipo</span><span class="sxs-lookup"><span data-stu-id="17dae-216">Type</span></span>             | <span data-ttu-id="17dae-217">Necessária</span><span class="sxs-lookup"><span data-stu-id="17dae-217">Required</span></span> | <span data-ttu-id="17dae-218">Observações</span><span class="sxs-lookup"><span data-stu-id="17dae-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="17dae-219">Dados</span><span class="sxs-lookup"><span data-stu-id="17dae-219">data</span></span>      | <span data-ttu-id="17dae-220">matriz de cadeias de caracteres</span><span class="sxs-lookup"><span data-stu-id="17dae-220">array of strings</span></span> | <span data-ttu-id="17dae-221">sim</span><span class="sxs-lookup"><span data-stu-id="17dae-221">yes</span></span>      | <span data-ttu-id="17dae-222">As versões de pacote correspondidas pela solicitação</span><span class="sxs-lookup"><span data-stu-id="17dae-222">The package versions matched by the request</span></span>

<span data-ttu-id="17dae-223">As versões de pacote na `data` matriz podem conter metadados de compilação SemVer 2.0.0 ( `1.0.0+metadata`por exemplo,) `semVerLevel=2.0.0` se o for fornecido na cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="17dae-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="17dae-224">Exemplo de solicitação</span><span class="sxs-lookup"><span data-stu-id="17dae-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="17dae-225">Exemplo de resposta</span><span class="sxs-lookup"><span data-stu-id="17dae-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
