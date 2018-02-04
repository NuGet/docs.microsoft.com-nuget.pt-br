---
title: Enviar por push e excluir, NuGet API | Microsoft Docs
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
description: "O serviço de publicação permite que os clientes publicar novos pacotes e remover da lista ou excluir os pacotes existentes."
keywords: Pacote de envio por push do NuGet API, API do NuGet excluir o pacote NuGet API remover da lista o pacote, o pacote de carregamento de API do NuGet, NuGet API criar pacote
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: f8051ca57fccae77917567d8c9f2f8a120a8d884
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="ba7ed-104">Enviar por push e excluir</span><span class="sxs-lookup"><span data-stu-id="ba7ed-104">Push and Delete</span></span>

<span data-ttu-id="ba7ed-105">É possível enviar por push, excluir (ou remover da lista, dependendo da implementação de servidor) e relist pacotes usando a API do NuGet V3.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-105">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="ba7ed-106">Essas operações baseiam-se do `PackagePublish` recurso encontrado na [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="ba7ed-106">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="ba7ed-107">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="ba7ed-107">Versioning</span></span>

<span data-ttu-id="ba7ed-108">O seguinte `@type` valor é usado:</span><span class="sxs-lookup"><span data-stu-id="ba7ed-108">The following `@type` value is used:</span></span>

<span data-ttu-id="ba7ed-109">Valor @type</span><span class="sxs-lookup"><span data-stu-id="ba7ed-109">@type value</span></span>          | <span data-ttu-id="ba7ed-110">Observações</span><span class="sxs-lookup"><span data-stu-id="ba7ed-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="ba7ed-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="ba7ed-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="ba7ed-112">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="ba7ed-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="ba7ed-113">URL Base</span><span class="sxs-lookup"><span data-stu-id="ba7ed-113">Base URL</span></span>

<span data-ttu-id="ba7ed-114">A URL base para as seguintes APIs é o valor da `@id` propriedade o `PackagePublish/2.0.0` recursos na origem do pacote [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="ba7ed-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="ba7ed-115">Para obter a documentação abaixo URL do nuget.org é usado.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="ba7ed-116">Considere `https://www.nuget.org/api/v2/package` como um espaço reservado para o `@id` valor encontrado no índice de serviço.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="ba7ed-117">Observe que essa URL aponta para o mesmo local que o ponto de extremidade de envio por push herdado V2 como o protocolo é o mesmo.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="ba7ed-118">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="ba7ed-118">HTTP methods</span></span>

<span data-ttu-id="ba7ed-119">O `PUT`, `POST` e `DELETE` métodos HTTP compatíveis com esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-119">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="ba7ed-120">Para quais métodos têm suporte em cada ponto de extremidade, consulte abaixo.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="ba7ed-121">Enviar um pacote</span><span class="sxs-lookup"><span data-stu-id="ba7ed-121">Push a package</span></span>

> [!Note]
> <span data-ttu-id="ba7ed-122">NuGet.org tem [requisitos adicionais](NuGet-Protocols.md) para interagir com o ponto de extremidade de envio por push.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-122">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="ba7ed-123">NuGet.org dá suporte a envio novos pacotes usando a seguinte API.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-123">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="ba7ed-124">Se o pacote com a ID e a versão fornecida já existir, nuget.org rejeitará o envio por push.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-124">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="ba7ed-125">Outras fontes de pacote podem oferecer suporte a substituição de um pacote existente.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-125">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="ba7ed-126">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="ba7ed-126">Request parameters</span></span>

<span data-ttu-id="ba7ed-127">Nome</span><span class="sxs-lookup"><span data-stu-id="ba7ed-127">Name</span></span>           | <span data-ttu-id="ba7ed-128">No</span><span class="sxs-lookup"><span data-stu-id="ba7ed-128">In</span></span>     | <span data-ttu-id="ba7ed-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="ba7ed-129">Type</span></span>   | <span data-ttu-id="ba7ed-130">Necessária</span><span class="sxs-lookup"><span data-stu-id="ba7ed-130">Required</span></span> | <span data-ttu-id="ba7ed-131">Observações</span><span class="sxs-lookup"><span data-stu-id="ba7ed-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="ba7ed-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="ba7ed-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="ba7ed-133">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="ba7ed-133">Header</span></span> | <span data-ttu-id="ba7ed-134">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="ba7ed-134">string</span></span> | <span data-ttu-id="ba7ed-135">sim</span><span class="sxs-lookup"><span data-stu-id="ba7ed-135">yes</span></span>      | <span data-ttu-id="ba7ed-136">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="ba7ed-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="ba7ed-137">A chave de API é uma cadeia de caracteres opaca obtidos de origem do pacote pelo usuário e configurado no cliente.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="ba7ed-138">Nenhum formato de cadeia de caracteres específica é obrigatória, mas o comprimento da chave de API não deve exceder um tamanho razoável para valores de cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="ba7ed-139">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="ba7ed-139">Request body</span></span>

<span data-ttu-id="ba7ed-140">O corpo da solicitação deve ser da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="ba7ed-140">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="ba7ed-141">Dados de formulário de várias partes</span><span class="sxs-lookup"><span data-stu-id="ba7ed-141">Multipart form data</span></span>

<span data-ttu-id="ba7ed-142">O cabeçalho de solicitação `Content-Type` é `multipart/form-data` e o primeiro item no corpo da solicitação é os bytes brutos do nupkg sendo enviado.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-142">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="ba7ed-143">Itens subsequentes no corpo com diversas partes são ignorados.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-143">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="ba7ed-144">O nome do arquivo ou quaisquer outros cabeçalhos dos itens de várias partes são ignorados.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-144">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="ba7ed-145">Resposta</span><span class="sxs-lookup"><span data-stu-id="ba7ed-145">Response</span></span>

<span data-ttu-id="ba7ed-146">Código de status</span><span class="sxs-lookup"><span data-stu-id="ba7ed-146">Status Code</span></span> | <span data-ttu-id="ba7ed-147">Significado</span><span class="sxs-lookup"><span data-stu-id="ba7ed-147">Meaning</span></span>
----------- | -------
<span data-ttu-id="ba7ed-148">201, 202</span><span class="sxs-lookup"><span data-stu-id="ba7ed-148">201, 202</span></span>    | <span data-ttu-id="ba7ed-149">O pacote foi enviado com êxito</span><span class="sxs-lookup"><span data-stu-id="ba7ed-149">The package was successfully pushed</span></span>
<span data-ttu-id="ba7ed-150">400</span><span class="sxs-lookup"><span data-stu-id="ba7ed-150">400</span></span>         | <span data-ttu-id="ba7ed-151">O pacote fornecido é inválido</span><span class="sxs-lookup"><span data-stu-id="ba7ed-151">The provided package is invalid</span></span>
<span data-ttu-id="ba7ed-152">409</span><span class="sxs-lookup"><span data-stu-id="ba7ed-152">409</span></span>         | <span data-ttu-id="ba7ed-153">Já existe um pacote com a ID e a versão fornecida</span><span class="sxs-lookup"><span data-stu-id="ba7ed-153">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="ba7ed-154">Implementações de servidor variam de acordo o código de status de êxito retornado quando um pacote é enviado com êxito.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-154">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="ba7ed-155">Excluir um pacote</span><span class="sxs-lookup"><span data-stu-id="ba7ed-155">Delete a package</span></span>

<span data-ttu-id="ba7ed-156">NuGet.org interpreta a solicitação de exclusão do pacote como um "remover da lista".</span><span class="sxs-lookup"><span data-stu-id="ba7ed-156">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="ba7ed-157">Isso significa que o pacote ainda está disponível para os consumidores existentes do pacote, mas o pacote não aparece nos resultados da pesquisa ou na interface da web.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-157">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="ba7ed-158">Para obter mais informações sobre esta prática, consulte o [pacotes excluído](../policies/deleting-packages.md) política.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-158">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="ba7ed-159">Outras implementações do servidor estão livres para interpretar esse sinal como uma exclusão de disco rígida, exclusão reversível ou remover da lista.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-159">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="ba7ed-160">Por exemplo, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (uma implementação de servidor somente com suporte a mais antiga API V2) oferece suporte à manipulação esta solicitação como um unlist ou uma exclusão de disco rígida com base em uma opção de configuração.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-160">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="ba7ed-161">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="ba7ed-161">Request parameters</span></span>

<span data-ttu-id="ba7ed-162">Nome</span><span class="sxs-lookup"><span data-stu-id="ba7ed-162">Name</span></span>           | <span data-ttu-id="ba7ed-163">No</span><span class="sxs-lookup"><span data-stu-id="ba7ed-163">In</span></span>     | <span data-ttu-id="ba7ed-164">Tipo</span><span class="sxs-lookup"><span data-stu-id="ba7ed-164">Type</span></span>   | <span data-ttu-id="ba7ed-165">Necessária</span><span class="sxs-lookup"><span data-stu-id="ba7ed-165">Required</span></span> | <span data-ttu-id="ba7ed-166">Observações</span><span class="sxs-lookup"><span data-stu-id="ba7ed-166">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="ba7ed-167">ID</span><span class="sxs-lookup"><span data-stu-id="ba7ed-167">ID</span></span>             | <span data-ttu-id="ba7ed-168">URL</span><span class="sxs-lookup"><span data-stu-id="ba7ed-168">URL</span></span>    | <span data-ttu-id="ba7ed-169">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="ba7ed-169">string</span></span> | <span data-ttu-id="ba7ed-170">sim</span><span class="sxs-lookup"><span data-stu-id="ba7ed-170">yes</span></span>      | <span data-ttu-id="ba7ed-171">A ID do pacote a ser excluído</span><span class="sxs-lookup"><span data-stu-id="ba7ed-171">The ID of the package to delete</span></span>
<span data-ttu-id="ba7ed-172">VERSION</span><span class="sxs-lookup"><span data-stu-id="ba7ed-172">VERSION</span></span>        | <span data-ttu-id="ba7ed-173">URL</span><span class="sxs-lookup"><span data-stu-id="ba7ed-173">URL</span></span>    | <span data-ttu-id="ba7ed-174">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="ba7ed-174">string</span></span> | <span data-ttu-id="ba7ed-175">sim</span><span class="sxs-lookup"><span data-stu-id="ba7ed-175">yes</span></span>      | <span data-ttu-id="ba7ed-176">A versão do pacote a excluir</span><span class="sxs-lookup"><span data-stu-id="ba7ed-176">The version of the package to delete</span></span>
<span data-ttu-id="ba7ed-177">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="ba7ed-177">X-NuGet-ApiKey</span></span> | <span data-ttu-id="ba7ed-178">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="ba7ed-178">Header</span></span> | <span data-ttu-id="ba7ed-179">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="ba7ed-179">string</span></span> | <span data-ttu-id="ba7ed-180">sim</span><span class="sxs-lookup"><span data-stu-id="ba7ed-180">yes</span></span>      | <span data-ttu-id="ba7ed-181">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="ba7ed-181">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="ba7ed-182">Resposta</span><span class="sxs-lookup"><span data-stu-id="ba7ed-182">Response</span></span>

<span data-ttu-id="ba7ed-183">Código de status</span><span class="sxs-lookup"><span data-stu-id="ba7ed-183">Status Code</span></span> | <span data-ttu-id="ba7ed-184">Significado</span><span class="sxs-lookup"><span data-stu-id="ba7ed-184">Meaning</span></span>
----------- | -------
<span data-ttu-id="ba7ed-185">204</span><span class="sxs-lookup"><span data-stu-id="ba7ed-185">204</span></span>         | <span data-ttu-id="ba7ed-186">O pacote foi excluído</span><span class="sxs-lookup"><span data-stu-id="ba7ed-186">The package was deleted</span></span>
<span data-ttu-id="ba7ed-187">404</span><span class="sxs-lookup"><span data-stu-id="ba7ed-187">404</span></span>         | <span data-ttu-id="ba7ed-188">Nenhum pacote com fornecido `ID` e `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="ba7ed-188">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="ba7ed-189">Relist um pacote</span><span class="sxs-lookup"><span data-stu-id="ba7ed-189">Relist a package</span></span>

<span data-ttu-id="ba7ed-190">Se um pacote não esteja listado, é possível fazer com que o pacote novamente visível nos resultados da pesquisa usando o ponto de extremidade de "relist".</span><span class="sxs-lookup"><span data-stu-id="ba7ed-190">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="ba7ed-191">Esse ponto de extremidade tem a mesma forma como o [excluir (remover da lista) ponto de extremidade](#delete-a-package) , mas usa o `POST` método HTTP em vez do `DELETE` método.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-191">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="ba7ed-192">Se o pacote já está listado, a solicitação ainda será bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="ba7ed-192">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="ba7ed-193">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="ba7ed-193">Request parameters</span></span>

<span data-ttu-id="ba7ed-194">Nome</span><span class="sxs-lookup"><span data-stu-id="ba7ed-194">Name</span></span>           | <span data-ttu-id="ba7ed-195">No</span><span class="sxs-lookup"><span data-stu-id="ba7ed-195">In</span></span>     | <span data-ttu-id="ba7ed-196">Tipo</span><span class="sxs-lookup"><span data-stu-id="ba7ed-196">Type</span></span>   | <span data-ttu-id="ba7ed-197">Necessária</span><span class="sxs-lookup"><span data-stu-id="ba7ed-197">Required</span></span> | <span data-ttu-id="ba7ed-198">Observações</span><span class="sxs-lookup"><span data-stu-id="ba7ed-198">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="ba7ed-199">ID</span><span class="sxs-lookup"><span data-stu-id="ba7ed-199">ID</span></span>             | <span data-ttu-id="ba7ed-200">URL</span><span class="sxs-lookup"><span data-stu-id="ba7ed-200">URL</span></span>    | <span data-ttu-id="ba7ed-201">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="ba7ed-201">string</span></span> | <span data-ttu-id="ba7ed-202">sim</span><span class="sxs-lookup"><span data-stu-id="ba7ed-202">yes</span></span>      | <span data-ttu-id="ba7ed-203">A ID do pacote para relist</span><span class="sxs-lookup"><span data-stu-id="ba7ed-203">The ID of the package to relist</span></span>
<span data-ttu-id="ba7ed-204">VERSION</span><span class="sxs-lookup"><span data-stu-id="ba7ed-204">VERSION</span></span>        | <span data-ttu-id="ba7ed-205">URL</span><span class="sxs-lookup"><span data-stu-id="ba7ed-205">URL</span></span>    | <span data-ttu-id="ba7ed-206">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="ba7ed-206">string</span></span> | <span data-ttu-id="ba7ed-207">sim</span><span class="sxs-lookup"><span data-stu-id="ba7ed-207">yes</span></span>      | <span data-ttu-id="ba7ed-208">A versão do pacote a ser relist</span><span class="sxs-lookup"><span data-stu-id="ba7ed-208">The version of the package to relist</span></span>
<span data-ttu-id="ba7ed-209">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="ba7ed-209">X-NuGet-ApiKey</span></span> | <span data-ttu-id="ba7ed-210">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="ba7ed-210">Header</span></span> | <span data-ttu-id="ba7ed-211">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="ba7ed-211">string</span></span> | <span data-ttu-id="ba7ed-212">sim</span><span class="sxs-lookup"><span data-stu-id="ba7ed-212">yes</span></span>      | <span data-ttu-id="ba7ed-213">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="ba7ed-213">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="ba7ed-214">Resposta</span><span class="sxs-lookup"><span data-stu-id="ba7ed-214">Response</span></span>

<span data-ttu-id="ba7ed-215">Código de status</span><span class="sxs-lookup"><span data-stu-id="ba7ed-215">Status Code</span></span> | <span data-ttu-id="ba7ed-216">Significado</span><span class="sxs-lookup"><span data-stu-id="ba7ed-216">Meaning</span></span>
----------- | -------
<span data-ttu-id="ba7ed-217">200</span><span class="sxs-lookup"><span data-stu-id="ba7ed-217">200</span></span>         | <span data-ttu-id="ba7ed-218">O pacote agora está listado</span><span class="sxs-lookup"><span data-stu-id="ba7ed-218">The package is now listed</span></span>
<span data-ttu-id="ba7ed-219">404</span><span class="sxs-lookup"><span data-stu-id="ba7ed-219">404</span></span>         | <span data-ttu-id="ba7ed-220">Nenhum pacote com fornecido `ID` e `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="ba7ed-220">No package with the provided `ID` and `VERSION` exists</span></span>
