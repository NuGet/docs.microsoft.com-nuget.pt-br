---
title: Enviar por push e excluir, a API do NuGet
description: O serviço de publicação permite que os clientes publicar novos pacotes e remover da lista ou excluir os pacotes existentes.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6e81055796e20186c5769d2ec39849e6c551ff87
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426716"
---
# <a name="push-and-delete"></a><span data-ttu-id="5ab49-103">Enviar por push e excluir</span><span class="sxs-lookup"><span data-stu-id="5ab49-103">Push and Delete</span></span>

<span data-ttu-id="5ab49-104">É possível enviar por push, excluir (ou remover da lista, dependendo da implementação de servidor) e relist pacotes usando a API do NuGet V3.</span><span class="sxs-lookup"><span data-stu-id="5ab49-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="5ab49-105">Essas operações são baseadas fora do `PackagePublish` recurso encontrado na [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="5ab49-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="5ab49-106">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="5ab49-106">Versioning</span></span>

<span data-ttu-id="5ab49-107">O seguinte `@type` valor é usado:</span><span class="sxs-lookup"><span data-stu-id="5ab49-107">The following `@type` value is used:</span></span>

<span data-ttu-id="5ab49-108">Valor @type</span><span class="sxs-lookup"><span data-stu-id="5ab49-108">@type value</span></span>          | <span data-ttu-id="5ab49-109">Observações</span><span class="sxs-lookup"><span data-stu-id="5ab49-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="5ab49-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="5ab49-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="5ab49-111">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="5ab49-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="5ab49-112">URL Base</span><span class="sxs-lookup"><span data-stu-id="5ab49-112">Base URL</span></span>

<span data-ttu-id="5ab49-113">A URL base para as APIs a seguir é o valor da `@id` propriedade do `PackagePublish/2.0.0` recurso na origem do pacote [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="5ab49-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="5ab49-114">Para obter a documentação abaixo, a URL do nuget.org é usado.</span><span class="sxs-lookup"><span data-stu-id="5ab49-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="5ab49-115">Considere `https://www.nuget.org/api/v2/package` como um espaço reservado para o `@id` valor encontrado no índice de serviço.</span><span class="sxs-lookup"><span data-stu-id="5ab49-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="5ab49-116">Observe que essa URL aponta para o mesmo local que o ponto de extremidade de envio por push herdado V2, pois o protocolo é o mesmo.</span><span class="sxs-lookup"><span data-stu-id="5ab49-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="5ab49-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="5ab49-117">HTTP methods</span></span>

<span data-ttu-id="5ab49-118">O `PUT`, `POST` e `DELETE` métodos HTTP compatíveis com esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5ab49-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="5ab49-119">Para quais métodos são suportados em cada ponto de extremidade, consulte abaixo.</span><span class="sxs-lookup"><span data-stu-id="5ab49-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="5ab49-120">Enviar por push a um pacote</span><span class="sxs-lookup"><span data-stu-id="5ab49-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="5ab49-121">tem NuGet.org [requisitos adicionais](NuGet-Protocols.md) para interagir com o ponto de extremidade de envio por push.</span><span class="sxs-lookup"><span data-stu-id="5ab49-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="5ab49-122">NuGet.org dá suporte a enviar por push novos pacotes usando a API a seguir.</span><span class="sxs-lookup"><span data-stu-id="5ab49-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="5ab49-123">Se o pacote com a ID e a versão fornecido já existir, o nuget.org rejeitará o envio por push.</span><span class="sxs-lookup"><span data-stu-id="5ab49-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="5ab49-124">Outras fontes de pacote podem dar suporte a substituição de um pacote existente.</span><span class="sxs-lookup"><span data-stu-id="5ab49-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="5ab49-125">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="5ab49-125">Request parameters</span></span>

<span data-ttu-id="5ab49-126">Nome</span><span class="sxs-lookup"><span data-stu-id="5ab49-126">Name</span></span>           | <span data-ttu-id="5ab49-127">No</span><span class="sxs-lookup"><span data-stu-id="5ab49-127">In</span></span>     | <span data-ttu-id="5ab49-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="5ab49-128">Type</span></span>   | <span data-ttu-id="5ab49-129">Necessária</span><span class="sxs-lookup"><span data-stu-id="5ab49-129">Required</span></span> | <span data-ttu-id="5ab49-130">Observações</span><span class="sxs-lookup"><span data-stu-id="5ab49-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="5ab49-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="5ab49-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="5ab49-132">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="5ab49-132">Header</span></span> | <span data-ttu-id="5ab49-133">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5ab49-133">string</span></span> | <span data-ttu-id="5ab49-134">sim</span><span class="sxs-lookup"><span data-stu-id="5ab49-134">yes</span></span>      | <span data-ttu-id="5ab49-135">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="5ab49-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="5ab49-136">A chave de API é uma cadeia de caracteres opaca obtidos de origem do pacote pelo usuário e configurado no cliente.</span><span class="sxs-lookup"><span data-stu-id="5ab49-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="5ab49-137">Nenhum formato de cadeia de caracteres específica é obrigatória, mas o comprimento da chave de API não deve exceder um tamanho razoável para valores de cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="5ab49-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="5ab49-138">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="5ab49-138">Request body</span></span>

<span data-ttu-id="5ab49-139">O corpo da solicitação deve vir da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="5ab49-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="5ab49-140">Dados de formulário de várias partes</span><span class="sxs-lookup"><span data-stu-id="5ab49-140">Multipart form data</span></span>

<span data-ttu-id="5ab49-141">O cabeçalho de solicitação `Content-Type` é `multipart/form-data` e o primeiro item no corpo da solicitação é os bytes brutos da. nupkg que está sendo enviado por push.</span><span class="sxs-lookup"><span data-stu-id="5ab49-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="5ab49-142">Os itens subsequentes no corpo com diversas partes são ignorados.</span><span class="sxs-lookup"><span data-stu-id="5ab49-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="5ab49-143">O nome do arquivo ou quaisquer outros cabeçalhos dos itens de várias partes são ignorados.</span><span class="sxs-lookup"><span data-stu-id="5ab49-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="5ab49-144">Resposta</span><span class="sxs-lookup"><span data-stu-id="5ab49-144">Response</span></span>

<span data-ttu-id="5ab49-145">Código de status</span><span class="sxs-lookup"><span data-stu-id="5ab49-145">Status Code</span></span> | <span data-ttu-id="5ab49-146">Significado</span><span class="sxs-lookup"><span data-stu-id="5ab49-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="5ab49-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="5ab49-147">201, 202</span></span>    | <span data-ttu-id="5ab49-148">O pacote foi enviado com êxito</span><span class="sxs-lookup"><span data-stu-id="5ab49-148">The package was successfully pushed</span></span>
<span data-ttu-id="5ab49-149">400</span><span class="sxs-lookup"><span data-stu-id="5ab49-149">400</span></span>         | <span data-ttu-id="5ab49-150">O pacote fornecido é inválido</span><span class="sxs-lookup"><span data-stu-id="5ab49-150">The provided package is invalid</span></span>
<span data-ttu-id="5ab49-151">409</span><span class="sxs-lookup"><span data-stu-id="5ab49-151">409</span></span>         | <span data-ttu-id="5ab49-152">Já existe um pacote com a ID e a versão fornecida</span><span class="sxs-lookup"><span data-stu-id="5ab49-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="5ab49-153">Implementações de servidor variam de acordo o código de status de êxito retornado quando um pacote é enviado com êxito.</span><span class="sxs-lookup"><span data-stu-id="5ab49-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="5ab49-154">Excluir um pacote</span><span class="sxs-lookup"><span data-stu-id="5ab49-154">Delete a package</span></span>

<span data-ttu-id="5ab49-155">NuGet.org interpreta a solicitação de exclusão do pacote como um "remover da lista".</span><span class="sxs-lookup"><span data-stu-id="5ab49-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="5ab49-156">Isso significa que o pacote ainda está disponível para os consumidores existentes do pacote, mas o pacote não aparece nos resultados da pesquisa ou na interface da web.</span><span class="sxs-lookup"><span data-stu-id="5ab49-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="5ab49-157">Para obter mais informações sobre essa prática, consulte o [excluído pacotes](../nuget-org/policies/deleting-packages.md) política.</span><span class="sxs-lookup"><span data-stu-id="5ab49-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="5ab49-158">Outras implementações de servidor são livres para interpretar esse sinal como uma exclusão de disco rígida, exclusão reversível ou remover da lista.</span><span class="sxs-lookup"><span data-stu-id="5ab49-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="5ab49-159">Por exemplo, [NuGet. Server](https://www.nuget.org/packages/NuGet.Server) (uma implementação de servidor somente com suporte a mais antiga API V2) dá suporte a tratamento essa solicitação como um unlist ou uma exclusão de disco rígida com base em uma opção de configuração.</span><span class="sxs-lookup"><span data-stu-id="5ab49-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="5ab49-160">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="5ab49-160">Request parameters</span></span>

<span data-ttu-id="5ab49-161">Nome</span><span class="sxs-lookup"><span data-stu-id="5ab49-161">Name</span></span>           | <span data-ttu-id="5ab49-162">No</span><span class="sxs-lookup"><span data-stu-id="5ab49-162">In</span></span>     | <span data-ttu-id="5ab49-163">Tipo</span><span class="sxs-lookup"><span data-stu-id="5ab49-163">Type</span></span>   | <span data-ttu-id="5ab49-164">Necessária</span><span class="sxs-lookup"><span data-stu-id="5ab49-164">Required</span></span> | <span data-ttu-id="5ab49-165">Observações</span><span class="sxs-lookup"><span data-stu-id="5ab49-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="5ab49-166">ID</span><span class="sxs-lookup"><span data-stu-id="5ab49-166">ID</span></span>             | <span data-ttu-id="5ab49-167">URL</span><span class="sxs-lookup"><span data-stu-id="5ab49-167">URL</span></span>    | <span data-ttu-id="5ab49-168">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5ab49-168">string</span></span> | <span data-ttu-id="5ab49-169">sim</span><span class="sxs-lookup"><span data-stu-id="5ab49-169">yes</span></span>      | <span data-ttu-id="5ab49-170">A ID do pacote a ser excluído</span><span class="sxs-lookup"><span data-stu-id="5ab49-170">The ID of the package to delete</span></span>
<span data-ttu-id="5ab49-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="5ab49-171">VERSION</span></span>        | <span data-ttu-id="5ab49-172">URL</span><span class="sxs-lookup"><span data-stu-id="5ab49-172">URL</span></span>    | <span data-ttu-id="5ab49-173">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5ab49-173">string</span></span> | <span data-ttu-id="5ab49-174">sim</span><span class="sxs-lookup"><span data-stu-id="5ab49-174">yes</span></span>      | <span data-ttu-id="5ab49-175">A versão do pacote a ser excluído</span><span class="sxs-lookup"><span data-stu-id="5ab49-175">The version of the package to delete</span></span>
<span data-ttu-id="5ab49-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="5ab49-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="5ab49-177">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="5ab49-177">Header</span></span> | <span data-ttu-id="5ab49-178">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5ab49-178">string</span></span> | <span data-ttu-id="5ab49-179">sim</span><span class="sxs-lookup"><span data-stu-id="5ab49-179">yes</span></span>      | <span data-ttu-id="5ab49-180">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="5ab49-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="5ab49-181">Resposta</span><span class="sxs-lookup"><span data-stu-id="5ab49-181">Response</span></span>

<span data-ttu-id="5ab49-182">Código de status</span><span class="sxs-lookup"><span data-stu-id="5ab49-182">Status Code</span></span> | <span data-ttu-id="5ab49-183">Significado</span><span class="sxs-lookup"><span data-stu-id="5ab49-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="5ab49-184">204</span><span class="sxs-lookup"><span data-stu-id="5ab49-184">204</span></span>         | <span data-ttu-id="5ab49-185">O pacote foi excluído</span><span class="sxs-lookup"><span data-stu-id="5ab49-185">The package was deleted</span></span>
<span data-ttu-id="5ab49-186">404</span><span class="sxs-lookup"><span data-stu-id="5ab49-186">404</span></span>         | <span data-ttu-id="5ab49-187">Nenhum pacote fornecido `ID` e `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="5ab49-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="5ab49-188">Relist um pacote</span><span class="sxs-lookup"><span data-stu-id="5ab49-188">Relist a package</span></span>

<span data-ttu-id="5ab49-189">Se um pacote for removido da lista, é possível fazer com que o pacote novamente visível nos resultados da pesquisa usando o ponto de extremidade "relist".</span><span class="sxs-lookup"><span data-stu-id="5ab49-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="5ab49-190">Esse ponto de extremidade tem a mesma forma que o [excluir (remover da lista) ponto de extremidade](#delete-a-package) , mas usa o `POST` método HTTP em vez do `DELETE` método.</span><span class="sxs-lookup"><span data-stu-id="5ab49-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="5ab49-191">Se o pacote já estiver listado, a solicitação ainda terá êxito.</span><span class="sxs-lookup"><span data-stu-id="5ab49-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="5ab49-192">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="5ab49-192">Request parameters</span></span>

<span data-ttu-id="5ab49-193">Nome</span><span class="sxs-lookup"><span data-stu-id="5ab49-193">Name</span></span>           | <span data-ttu-id="5ab49-194">No</span><span class="sxs-lookup"><span data-stu-id="5ab49-194">In</span></span>     | <span data-ttu-id="5ab49-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="5ab49-195">Type</span></span>   | <span data-ttu-id="5ab49-196">Necessária</span><span class="sxs-lookup"><span data-stu-id="5ab49-196">Required</span></span> | <span data-ttu-id="5ab49-197">Observações</span><span class="sxs-lookup"><span data-stu-id="5ab49-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="5ab49-198">ID</span><span class="sxs-lookup"><span data-stu-id="5ab49-198">ID</span></span>             | <span data-ttu-id="5ab49-199">URL</span><span class="sxs-lookup"><span data-stu-id="5ab49-199">URL</span></span>    | <span data-ttu-id="5ab49-200">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5ab49-200">string</span></span> | <span data-ttu-id="5ab49-201">sim</span><span class="sxs-lookup"><span data-stu-id="5ab49-201">yes</span></span>      | <span data-ttu-id="5ab49-202">A ID do pacote para relist</span><span class="sxs-lookup"><span data-stu-id="5ab49-202">The ID of the package to relist</span></span>
<span data-ttu-id="5ab49-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="5ab49-203">VERSION</span></span>        | <span data-ttu-id="5ab49-204">URL</span><span class="sxs-lookup"><span data-stu-id="5ab49-204">URL</span></span>    | <span data-ttu-id="5ab49-205">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5ab49-205">string</span></span> | <span data-ttu-id="5ab49-206">sim</span><span class="sxs-lookup"><span data-stu-id="5ab49-206">yes</span></span>      | <span data-ttu-id="5ab49-207">A versão do pacote como relist</span><span class="sxs-lookup"><span data-stu-id="5ab49-207">The version of the package to relist</span></span>
<span data-ttu-id="5ab49-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="5ab49-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="5ab49-209">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="5ab49-209">Header</span></span> | <span data-ttu-id="5ab49-210">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5ab49-210">string</span></span> | <span data-ttu-id="5ab49-211">sim</span><span class="sxs-lookup"><span data-stu-id="5ab49-211">yes</span></span>      | <span data-ttu-id="5ab49-212">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="5ab49-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="5ab49-213">Resposta</span><span class="sxs-lookup"><span data-stu-id="5ab49-213">Response</span></span>

<span data-ttu-id="5ab49-214">Código de status</span><span class="sxs-lookup"><span data-stu-id="5ab49-214">Status Code</span></span> | <span data-ttu-id="5ab49-215">Significado</span><span class="sxs-lookup"><span data-stu-id="5ab49-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="5ab49-216">200</span><span class="sxs-lookup"><span data-stu-id="5ab49-216">200</span></span>         | <span data-ttu-id="5ab49-217">O pacote agora está listado</span><span class="sxs-lookup"><span data-stu-id="5ab49-217">The package is now listed</span></span>
<span data-ttu-id="5ab49-218">404</span><span class="sxs-lookup"><span data-stu-id="5ab49-218">404</span></span>         | <span data-ttu-id="5ab49-219">Nenhum pacote fornecido `ID` e `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="5ab49-219">No package with the provided `ID` and `VERSION` exists</span></span>
