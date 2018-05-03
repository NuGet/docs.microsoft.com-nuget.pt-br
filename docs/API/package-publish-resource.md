---
title: Enviar por push e excluir a API do NuGet
description: O serviço de publicação permite que os clientes publicar novos pacotes e remover da lista ou excluir os pacotes existentes.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 911c8238624f806b1fbb5c7938d02b6bdfbd8614
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="fe926-103">Enviar por push e excluir</span><span class="sxs-lookup"><span data-stu-id="fe926-103">Push and Delete</span></span>

<span data-ttu-id="fe926-104">É possível enviar por push, excluir (ou remover da lista, dependendo da implementação de servidor) e relist pacotes usando a API do NuGet V3.</span><span class="sxs-lookup"><span data-stu-id="fe926-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="fe926-105">Essas operações baseiam-se do `PackagePublish` recurso encontrado na [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="fe926-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="fe926-106">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="fe926-106">Versioning</span></span>

<span data-ttu-id="fe926-107">O seguinte `@type` valor é usado:</span><span class="sxs-lookup"><span data-stu-id="fe926-107">The following `@type` value is used:</span></span>

<span data-ttu-id="fe926-108">Valor @type</span><span class="sxs-lookup"><span data-stu-id="fe926-108">@type value</span></span>          | <span data-ttu-id="fe926-109">Observações</span><span class="sxs-lookup"><span data-stu-id="fe926-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="fe926-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="fe926-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="fe926-111">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="fe926-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="fe926-112">URL Base</span><span class="sxs-lookup"><span data-stu-id="fe926-112">Base URL</span></span>

<span data-ttu-id="fe926-113">A URL base para as seguintes APIs é o valor da `@id` propriedade o `PackagePublish/2.0.0` recursos na origem do pacote [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="fe926-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="fe926-114">Para obter a documentação abaixo URL do nuget.org é usado.</span><span class="sxs-lookup"><span data-stu-id="fe926-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="fe926-115">Considere `https://www.nuget.org/api/v2/package` como um espaço reservado para o `@id` valor encontrado no índice de serviço.</span><span class="sxs-lookup"><span data-stu-id="fe926-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="fe926-116">Observe que essa URL aponta para o mesmo local que o ponto de extremidade de envio por push herdado V2 como o protocolo é o mesmo.</span><span class="sxs-lookup"><span data-stu-id="fe926-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="fe926-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="fe926-117">HTTP methods</span></span>

<span data-ttu-id="fe926-118">O `PUT`, `POST` e `DELETE` métodos HTTP compatíveis com esse recurso.</span><span class="sxs-lookup"><span data-stu-id="fe926-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="fe926-119">Para quais métodos têm suporte em cada ponto de extremidade, consulte abaixo.</span><span class="sxs-lookup"><span data-stu-id="fe926-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="fe926-120">Enviar um pacote</span><span class="sxs-lookup"><span data-stu-id="fe926-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="fe926-121">NuGet.org tem [requisitos adicionais](NuGet-Protocols.md) para interagir com o ponto de extremidade de envio por push.</span><span class="sxs-lookup"><span data-stu-id="fe926-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="fe926-122">NuGet.org dá suporte a envio novos pacotes usando a seguinte API.</span><span class="sxs-lookup"><span data-stu-id="fe926-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="fe926-123">Se o pacote com a ID e a versão fornecida já existir, nuget.org rejeitará o envio por push.</span><span class="sxs-lookup"><span data-stu-id="fe926-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="fe926-124">Outras fontes de pacote podem oferecer suporte a substituição de um pacote existente.</span><span class="sxs-lookup"><span data-stu-id="fe926-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="fe926-125">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="fe926-125">Request parameters</span></span>

<span data-ttu-id="fe926-126">Nome</span><span class="sxs-lookup"><span data-stu-id="fe926-126">Name</span></span>           | <span data-ttu-id="fe926-127">No</span><span class="sxs-lookup"><span data-stu-id="fe926-127">In</span></span>     | <span data-ttu-id="fe926-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="fe926-128">Type</span></span>   | <span data-ttu-id="fe926-129">Necessária</span><span class="sxs-lookup"><span data-stu-id="fe926-129">Required</span></span> | <span data-ttu-id="fe926-130">Observações</span><span class="sxs-lookup"><span data-stu-id="fe926-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="fe926-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="fe926-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="fe926-132">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="fe926-132">Header</span></span> | <span data-ttu-id="fe926-133">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fe926-133">string</span></span> | <span data-ttu-id="fe926-134">sim</span><span class="sxs-lookup"><span data-stu-id="fe926-134">yes</span></span>      | <span data-ttu-id="fe926-135">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="fe926-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="fe926-136">A chave de API é uma cadeia de caracteres opaca obtidos de origem do pacote pelo usuário e configurado no cliente.</span><span class="sxs-lookup"><span data-stu-id="fe926-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="fe926-137">Nenhum formato de cadeia de caracteres específica é obrigatória, mas o comprimento da chave de API não deve exceder um tamanho razoável para valores de cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="fe926-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="fe926-138">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="fe926-138">Request body</span></span>

<span data-ttu-id="fe926-139">O corpo da solicitação deve ser da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="fe926-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="fe926-140">Dados de formulário de várias partes</span><span class="sxs-lookup"><span data-stu-id="fe926-140">Multipart form data</span></span>

<span data-ttu-id="fe926-141">O cabeçalho de solicitação `Content-Type` é `multipart/form-data` e o primeiro item no corpo da solicitação é os bytes brutos do nupkg sendo enviado.</span><span class="sxs-lookup"><span data-stu-id="fe926-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="fe926-142">Itens subsequentes no corpo com diversas partes são ignorados.</span><span class="sxs-lookup"><span data-stu-id="fe926-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="fe926-143">O nome do arquivo ou quaisquer outros cabeçalhos dos itens de várias partes são ignorados.</span><span class="sxs-lookup"><span data-stu-id="fe926-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="fe926-144">Resposta</span><span class="sxs-lookup"><span data-stu-id="fe926-144">Response</span></span>

<span data-ttu-id="fe926-145">Código de status</span><span class="sxs-lookup"><span data-stu-id="fe926-145">Status Code</span></span> | <span data-ttu-id="fe926-146">Significado</span><span class="sxs-lookup"><span data-stu-id="fe926-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="fe926-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="fe926-147">201, 202</span></span>    | <span data-ttu-id="fe926-148">O pacote foi enviado com êxito</span><span class="sxs-lookup"><span data-stu-id="fe926-148">The package was successfully pushed</span></span>
<span data-ttu-id="fe926-149">400</span><span class="sxs-lookup"><span data-stu-id="fe926-149">400</span></span>         | <span data-ttu-id="fe926-150">O pacote fornecido é inválido</span><span class="sxs-lookup"><span data-stu-id="fe926-150">The provided package is invalid</span></span>
<span data-ttu-id="fe926-151">409</span><span class="sxs-lookup"><span data-stu-id="fe926-151">409</span></span>         | <span data-ttu-id="fe926-152">Já existe um pacote com a ID e a versão fornecida</span><span class="sxs-lookup"><span data-stu-id="fe926-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="fe926-153">Implementações de servidor variam de acordo o código de status de êxito retornado quando um pacote é enviado com êxito.</span><span class="sxs-lookup"><span data-stu-id="fe926-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="fe926-154">Excluir um pacote</span><span class="sxs-lookup"><span data-stu-id="fe926-154">Delete a package</span></span>

<span data-ttu-id="fe926-155">NuGet.org interpreta a solicitação de exclusão do pacote como um "remover da lista".</span><span class="sxs-lookup"><span data-stu-id="fe926-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="fe926-156">Isso significa que o pacote ainda está disponível para os consumidores existentes do pacote, mas o pacote não aparece nos resultados da pesquisa ou na interface da web.</span><span class="sxs-lookup"><span data-stu-id="fe926-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="fe926-157">Para obter mais informações sobre esta prática, consulte o [pacotes excluído](../policies/deleting-packages.md) política.</span><span class="sxs-lookup"><span data-stu-id="fe926-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="fe926-158">Outras implementações do servidor estão livres para interpretar esse sinal como uma exclusão de disco rígida, exclusão reversível ou remover da lista.</span><span class="sxs-lookup"><span data-stu-id="fe926-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="fe926-159">Por exemplo, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (uma implementação de servidor somente com suporte a mais antiga API V2) oferece suporte à manipulação esta solicitação como um unlist ou uma exclusão de disco rígida com base em uma opção de configuração.</span><span class="sxs-lookup"><span data-stu-id="fe926-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="fe926-160">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="fe926-160">Request parameters</span></span>

<span data-ttu-id="fe926-161">Nome</span><span class="sxs-lookup"><span data-stu-id="fe926-161">Name</span></span>           | <span data-ttu-id="fe926-162">No</span><span class="sxs-lookup"><span data-stu-id="fe926-162">In</span></span>     | <span data-ttu-id="fe926-163">Tipo</span><span class="sxs-lookup"><span data-stu-id="fe926-163">Type</span></span>   | <span data-ttu-id="fe926-164">Necessária</span><span class="sxs-lookup"><span data-stu-id="fe926-164">Required</span></span> | <span data-ttu-id="fe926-165">Observações</span><span class="sxs-lookup"><span data-stu-id="fe926-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="fe926-166">ID</span><span class="sxs-lookup"><span data-stu-id="fe926-166">ID</span></span>             | <span data-ttu-id="fe926-167">URL</span><span class="sxs-lookup"><span data-stu-id="fe926-167">URL</span></span>    | <span data-ttu-id="fe926-168">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fe926-168">string</span></span> | <span data-ttu-id="fe926-169">sim</span><span class="sxs-lookup"><span data-stu-id="fe926-169">yes</span></span>      | <span data-ttu-id="fe926-170">A ID do pacote a ser excluído</span><span class="sxs-lookup"><span data-stu-id="fe926-170">The ID of the package to delete</span></span>
<span data-ttu-id="fe926-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="fe926-171">VERSION</span></span>        | <span data-ttu-id="fe926-172">URL</span><span class="sxs-lookup"><span data-stu-id="fe926-172">URL</span></span>    | <span data-ttu-id="fe926-173">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fe926-173">string</span></span> | <span data-ttu-id="fe926-174">sim</span><span class="sxs-lookup"><span data-stu-id="fe926-174">yes</span></span>      | <span data-ttu-id="fe926-175">A versão do pacote a excluir</span><span class="sxs-lookup"><span data-stu-id="fe926-175">The version of the package to delete</span></span>
<span data-ttu-id="fe926-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="fe926-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="fe926-177">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="fe926-177">Header</span></span> | <span data-ttu-id="fe926-178">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fe926-178">string</span></span> | <span data-ttu-id="fe926-179">sim</span><span class="sxs-lookup"><span data-stu-id="fe926-179">yes</span></span>      | <span data-ttu-id="fe926-180">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="fe926-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="fe926-181">Resposta</span><span class="sxs-lookup"><span data-stu-id="fe926-181">Response</span></span>

<span data-ttu-id="fe926-182">Código de status</span><span class="sxs-lookup"><span data-stu-id="fe926-182">Status Code</span></span> | <span data-ttu-id="fe926-183">Significado</span><span class="sxs-lookup"><span data-stu-id="fe926-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="fe926-184">204</span><span class="sxs-lookup"><span data-stu-id="fe926-184">204</span></span>         | <span data-ttu-id="fe926-185">O pacote foi excluído</span><span class="sxs-lookup"><span data-stu-id="fe926-185">The package was deleted</span></span>
<span data-ttu-id="fe926-186">404</span><span class="sxs-lookup"><span data-stu-id="fe926-186">404</span></span>         | <span data-ttu-id="fe926-187">Nenhum pacote com fornecido `ID` e `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="fe926-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="fe926-188">Relist um pacote</span><span class="sxs-lookup"><span data-stu-id="fe926-188">Relist a package</span></span>

<span data-ttu-id="fe926-189">Se um pacote não esteja listado, é possível fazer com que o pacote novamente visível nos resultados da pesquisa usando o ponto de extremidade de "relist".</span><span class="sxs-lookup"><span data-stu-id="fe926-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="fe926-190">Esse ponto de extremidade tem a mesma forma como o [excluir (remover da lista) ponto de extremidade](#delete-a-package) , mas usa o `POST` método HTTP em vez do `DELETE` método.</span><span class="sxs-lookup"><span data-stu-id="fe926-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="fe926-191">Se o pacote já está listado, a solicitação ainda será bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="fe926-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="fe926-192">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="fe926-192">Request parameters</span></span>

<span data-ttu-id="fe926-193">Nome</span><span class="sxs-lookup"><span data-stu-id="fe926-193">Name</span></span>           | <span data-ttu-id="fe926-194">No</span><span class="sxs-lookup"><span data-stu-id="fe926-194">In</span></span>     | <span data-ttu-id="fe926-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="fe926-195">Type</span></span>   | <span data-ttu-id="fe926-196">Necessária</span><span class="sxs-lookup"><span data-stu-id="fe926-196">Required</span></span> | <span data-ttu-id="fe926-197">Observações</span><span class="sxs-lookup"><span data-stu-id="fe926-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="fe926-198">ID</span><span class="sxs-lookup"><span data-stu-id="fe926-198">ID</span></span>             | <span data-ttu-id="fe926-199">URL</span><span class="sxs-lookup"><span data-stu-id="fe926-199">URL</span></span>    | <span data-ttu-id="fe926-200">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fe926-200">string</span></span> | <span data-ttu-id="fe926-201">sim</span><span class="sxs-lookup"><span data-stu-id="fe926-201">yes</span></span>      | <span data-ttu-id="fe926-202">A ID do pacote para relist</span><span class="sxs-lookup"><span data-stu-id="fe926-202">The ID of the package to relist</span></span>
<span data-ttu-id="fe926-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="fe926-203">VERSION</span></span>        | <span data-ttu-id="fe926-204">URL</span><span class="sxs-lookup"><span data-stu-id="fe926-204">URL</span></span>    | <span data-ttu-id="fe926-205">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fe926-205">string</span></span> | <span data-ttu-id="fe926-206">sim</span><span class="sxs-lookup"><span data-stu-id="fe926-206">yes</span></span>      | <span data-ttu-id="fe926-207">A versão do pacote a ser relist</span><span class="sxs-lookup"><span data-stu-id="fe926-207">The version of the package to relist</span></span>
<span data-ttu-id="fe926-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="fe926-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="fe926-209">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="fe926-209">Header</span></span> | <span data-ttu-id="fe926-210">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fe926-210">string</span></span> | <span data-ttu-id="fe926-211">sim</span><span class="sxs-lookup"><span data-stu-id="fe926-211">yes</span></span>      | <span data-ttu-id="fe926-212">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="fe926-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="fe926-213">Resposta</span><span class="sxs-lookup"><span data-stu-id="fe926-213">Response</span></span>

<span data-ttu-id="fe926-214">Código de status</span><span class="sxs-lookup"><span data-stu-id="fe926-214">Status Code</span></span> | <span data-ttu-id="fe926-215">Significado</span><span class="sxs-lookup"><span data-stu-id="fe926-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="fe926-216">200</span><span class="sxs-lookup"><span data-stu-id="fe926-216">200</span></span>         | <span data-ttu-id="fe926-217">O pacote agora está listado</span><span class="sxs-lookup"><span data-stu-id="fe926-217">The package is now listed</span></span>
<span data-ttu-id="fe926-218">404</span><span class="sxs-lookup"><span data-stu-id="fe926-218">404</span></span>         | <span data-ttu-id="fe926-219">Nenhum pacote com fornecido `ID` e `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="fe926-219">No package with the provided `ID` and `VERSION` exists</span></span>
