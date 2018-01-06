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
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "O serviço de publicação permite que os clientes publicar novos pacotes e remover da lista ou excluir os pacotes existentes."
keywords: Pacote de envio por push do NuGet API, API do NuGet excluir o pacote NuGet API remover da lista o pacote, o pacote de carregamento de API do NuGet, NuGet API criar pacote
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 87970a701c63bce2b74c619069ec1d231ea77ab5
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="2ad4f-104">Enviar por push e excluir</span><span class="sxs-lookup"><span data-stu-id="2ad4f-104">Push and Delete</span></span>

<span data-ttu-id="2ad4f-105">É possível enviar por push, excluir (ou remover da lista, dependendo da implementação de servidor) e relist pacotes usando a API do NuGet V3.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-105">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="2ad4f-106">Essas operações baseiam-se do `PackagePublish` recurso encontrado na [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="2ad4f-106">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="2ad4f-107">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="2ad4f-107">Versioning</span></span>

<span data-ttu-id="2ad4f-108">O seguinte `@type` valor é usado:</span><span class="sxs-lookup"><span data-stu-id="2ad4f-108">The following `@type` value is used:</span></span>

<span data-ttu-id="2ad4f-109">Valor @type</span><span class="sxs-lookup"><span data-stu-id="2ad4f-109">@type value</span></span>          | <span data-ttu-id="2ad4f-110">Observações</span><span class="sxs-lookup"><span data-stu-id="2ad4f-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="2ad4f-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="2ad4f-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="2ad4f-112">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="2ad4f-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="2ad4f-113">URL Base</span><span class="sxs-lookup"><span data-stu-id="2ad4f-113">Base URL</span></span>

<span data-ttu-id="2ad4f-114">A URL base para as seguintes APIs é o valor da `@id` propriedade o `PackagePublish/2.0.0` recursos na origem do pacote [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="2ad4f-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="2ad4f-115">Para obter a documentação abaixo URL do nuget.org é usado.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="2ad4f-116">Considere `https://www.nuget.org/api/v2/package` como um espaço reservado para o `@id` valor encontrado no índice de serviço.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="2ad4f-117">Observe que essa URL aponta para o mesmo local que o ponto de extremidade de envio por push herdado V2 como o protocolo é o mesmo.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="2ad4f-118">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="2ad4f-118">HTTP methods</span></span>

<span data-ttu-id="2ad4f-119">O `PUT`, `POST` e `DELETE` métodos HTTP compatíveis com esse recurso.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-119">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="2ad4f-120">Para quais métodos têm suporte em cada ponto de extremidade, consulte abaixo.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="2ad4f-121">Enviar um pacote</span><span class="sxs-lookup"><span data-stu-id="2ad4f-121">Push a package</span></span>

> [!Note]
> <span data-ttu-id="2ad4f-122">NuGet.org tem [requisitos adicionais](NuGet-Protocols.md) para interagir com o ponto de extremidade de envio por push.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-122">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="2ad4f-123">NuGet.org dá suporte a envio novos pacotes usando a seguinte API.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-123">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="2ad4f-124">Se o pacote com a ID e a versão fornecida já existir, nuget.org rejeitará o envio por push.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-124">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="2ad4f-125">Outras fontes de pacote podem oferecer suporte a substituição de um pacote existente.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-125">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="2ad4f-126">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="2ad4f-126">Request parameters</span></span>

<span data-ttu-id="2ad4f-127">Nome</span><span class="sxs-lookup"><span data-stu-id="2ad4f-127">Name</span></span>           | <span data-ttu-id="2ad4f-128">No</span><span class="sxs-lookup"><span data-stu-id="2ad4f-128">In</span></span>     | <span data-ttu-id="2ad4f-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="2ad4f-129">Type</span></span>   | <span data-ttu-id="2ad4f-130">Necessária</span><span class="sxs-lookup"><span data-stu-id="2ad4f-130">Required</span></span> | <span data-ttu-id="2ad4f-131">Observações</span><span class="sxs-lookup"><span data-stu-id="2ad4f-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="2ad4f-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="2ad4f-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="2ad4f-133">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="2ad4f-133">Header</span></span> | <span data-ttu-id="2ad4f-134">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="2ad4f-134">string</span></span> | <span data-ttu-id="2ad4f-135">sim</span><span class="sxs-lookup"><span data-stu-id="2ad4f-135">yes</span></span>      | <span data-ttu-id="2ad4f-136">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="2ad4f-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="2ad4f-137">A chave de API é uma cadeia de caracteres opaca obtidos de origem do pacote pelo usuário e configurado no cliente.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="2ad4f-138">Nenhum formato de cadeia de caracteres específica é obrigatória, mas o comprimento da chave de API não deve exceder um tamanho razoável para valores de cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="2ad4f-139">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="2ad4f-139">Request body</span></span>

<span data-ttu-id="2ad4f-140">O corpo da solicitação deve ser da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="2ad4f-140">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="2ad4f-141">Dados de formulário de várias partes</span><span class="sxs-lookup"><span data-stu-id="2ad4f-141">Multipart form data</span></span>

<span data-ttu-id="2ad4f-142">O cabeçalho de solicitação `Content-Type` é `multipart/form-data` e o primeiro item no corpo da solicitação é os bytes brutos do nupkg sendo enviado.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-142">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="2ad4f-143">Itens subsequentes no corpo com diversas partes são ignorados.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-143">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="2ad4f-144">O nome do arquivo ou quaisquer outros cabeçalhos dos itens de várias partes são ignorados.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-144">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="2ad4f-145">Resposta</span><span class="sxs-lookup"><span data-stu-id="2ad4f-145">Response</span></span>

<span data-ttu-id="2ad4f-146">Código de status</span><span class="sxs-lookup"><span data-stu-id="2ad4f-146">Status Code</span></span> | <span data-ttu-id="2ad4f-147">Significado</span><span class="sxs-lookup"><span data-stu-id="2ad4f-147">Meaning</span></span>
----------- | -------
<span data-ttu-id="2ad4f-148">201, 202</span><span class="sxs-lookup"><span data-stu-id="2ad4f-148">201, 202</span></span>    | <span data-ttu-id="2ad4f-149">O pacote foi enviado com êxito</span><span class="sxs-lookup"><span data-stu-id="2ad4f-149">The package was successfully pushed</span></span>
<span data-ttu-id="2ad4f-150">400</span><span class="sxs-lookup"><span data-stu-id="2ad4f-150">400</span></span>         | <span data-ttu-id="2ad4f-151">O pacote fornecido é inválido</span><span class="sxs-lookup"><span data-stu-id="2ad4f-151">The provided package is invalid</span></span>
<span data-ttu-id="2ad4f-152">409</span><span class="sxs-lookup"><span data-stu-id="2ad4f-152">409</span></span>         | <span data-ttu-id="2ad4f-153">Já existe um pacote com a ID e a versão fornecida</span><span class="sxs-lookup"><span data-stu-id="2ad4f-153">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="2ad4f-154">Implementações de servidor variam de acordo o código de status de êxito retornado quando um pacote é enviado com êxito.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-154">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="2ad4f-155">Excluir um pacote</span><span class="sxs-lookup"><span data-stu-id="2ad4f-155">Delete a package</span></span>

<span data-ttu-id="2ad4f-156">NuGet.org interpreta a solicitação de exclusão do pacote como um "remover da lista".</span><span class="sxs-lookup"><span data-stu-id="2ad4f-156">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="2ad4f-157">Isso significa que o pacote ainda está disponível para os consumidores existentes do pacote, mas o pacote não aparece nos resultados da pesquisa ou na interface da web.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-157">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="2ad4f-158">Para obter mais informações sobre esta prática, consulte o [pacotes excluído](../policies/deleting-packages.md) política.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-158">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="2ad4f-159">Outras implementações do servidor estão livres para interpretar esse sinal como uma exclusão de disco rígida, exclusão reversível ou remover da lista.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-159">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="2ad4f-160">Por exemplo, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (uma implementação de servidor somente com suporte a mais antiga API V2) oferece suporte à manipulação esta solicitação como um unlist ou uma exclusão de disco rígida com base em uma opção de configuração.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-160">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="2ad4f-161">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="2ad4f-161">Request parameters</span></span>

<span data-ttu-id="2ad4f-162">Nome</span><span class="sxs-lookup"><span data-stu-id="2ad4f-162">Name</span></span>           | <span data-ttu-id="2ad4f-163">No</span><span class="sxs-lookup"><span data-stu-id="2ad4f-163">In</span></span>     | <span data-ttu-id="2ad4f-164">Tipo</span><span class="sxs-lookup"><span data-stu-id="2ad4f-164">Type</span></span>   | <span data-ttu-id="2ad4f-165">Necessária</span><span class="sxs-lookup"><span data-stu-id="2ad4f-165">Required</span></span> | <span data-ttu-id="2ad4f-166">Observações</span><span class="sxs-lookup"><span data-stu-id="2ad4f-166">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="2ad4f-167">ID</span><span class="sxs-lookup"><span data-stu-id="2ad4f-167">ID</span></span>             | <span data-ttu-id="2ad4f-168">URL</span><span class="sxs-lookup"><span data-stu-id="2ad4f-168">URL</span></span>    | <span data-ttu-id="2ad4f-169">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="2ad4f-169">string</span></span> | <span data-ttu-id="2ad4f-170">sim</span><span class="sxs-lookup"><span data-stu-id="2ad4f-170">yes</span></span>      | <span data-ttu-id="2ad4f-171">A ID do pacote a ser excluído</span><span class="sxs-lookup"><span data-stu-id="2ad4f-171">The ID of the package to delete</span></span>
<span data-ttu-id="2ad4f-172">VERSION</span><span class="sxs-lookup"><span data-stu-id="2ad4f-172">VERSION</span></span>        | <span data-ttu-id="2ad4f-173">URL</span><span class="sxs-lookup"><span data-stu-id="2ad4f-173">URL</span></span>    | <span data-ttu-id="2ad4f-174">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="2ad4f-174">string</span></span> | <span data-ttu-id="2ad4f-175">sim</span><span class="sxs-lookup"><span data-stu-id="2ad4f-175">yes</span></span>      | <span data-ttu-id="2ad4f-176">A versão do pacote a excluir</span><span class="sxs-lookup"><span data-stu-id="2ad4f-176">The version of the package to delete</span></span>
<span data-ttu-id="2ad4f-177">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="2ad4f-177">X-NuGet-ApiKey</span></span> | <span data-ttu-id="2ad4f-178">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="2ad4f-178">Header</span></span> | <span data-ttu-id="2ad4f-179">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="2ad4f-179">string</span></span> | <span data-ttu-id="2ad4f-180">sim</span><span class="sxs-lookup"><span data-stu-id="2ad4f-180">yes</span></span>      | <span data-ttu-id="2ad4f-181">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="2ad4f-181">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="2ad4f-182">Resposta</span><span class="sxs-lookup"><span data-stu-id="2ad4f-182">Response</span></span>

<span data-ttu-id="2ad4f-183">Código de status</span><span class="sxs-lookup"><span data-stu-id="2ad4f-183">Status Code</span></span> | <span data-ttu-id="2ad4f-184">Significado</span><span class="sxs-lookup"><span data-stu-id="2ad4f-184">Meaning</span></span>
----------- | -------
<span data-ttu-id="2ad4f-185">204</span><span class="sxs-lookup"><span data-stu-id="2ad4f-185">204</span></span>         | <span data-ttu-id="2ad4f-186">O pacote foi excluído</span><span class="sxs-lookup"><span data-stu-id="2ad4f-186">The package was deleted</span></span>
<span data-ttu-id="2ad4f-187">404</span><span class="sxs-lookup"><span data-stu-id="2ad4f-187">404</span></span>         | <span data-ttu-id="2ad4f-188">Nenhum pacote com fornecido `ID` e `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="2ad4f-188">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="2ad4f-189">Relist um pacote</span><span class="sxs-lookup"><span data-stu-id="2ad4f-189">Relist a package</span></span>

<span data-ttu-id="2ad4f-190">Se um pacote não esteja listado, é possível fazer com que o pacote novamente visível nos resultados da pesquisa usando o ponto de extremidade de "relist".</span><span class="sxs-lookup"><span data-stu-id="2ad4f-190">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="2ad4f-191">Esse ponto de extremidade tem a mesma forma como o [excluir (remover da lista) ponto de extremidade](#delete-a-package) , mas usa o `POST` método HTTP em vez do `DELETE` método.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-191">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="2ad4f-192">Se o pacote já está listado, a solicitação ainda será bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="2ad4f-192">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="2ad4f-193">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="2ad4f-193">Request parameters</span></span>

<span data-ttu-id="2ad4f-194">Nome</span><span class="sxs-lookup"><span data-stu-id="2ad4f-194">Name</span></span>           | <span data-ttu-id="2ad4f-195">No</span><span class="sxs-lookup"><span data-stu-id="2ad4f-195">In</span></span>     | <span data-ttu-id="2ad4f-196">Tipo</span><span class="sxs-lookup"><span data-stu-id="2ad4f-196">Type</span></span>   | <span data-ttu-id="2ad4f-197">Necessária</span><span class="sxs-lookup"><span data-stu-id="2ad4f-197">Required</span></span> | <span data-ttu-id="2ad4f-198">Observações</span><span class="sxs-lookup"><span data-stu-id="2ad4f-198">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="2ad4f-199">ID</span><span class="sxs-lookup"><span data-stu-id="2ad4f-199">ID</span></span>             | <span data-ttu-id="2ad4f-200">URL</span><span class="sxs-lookup"><span data-stu-id="2ad4f-200">URL</span></span>    | <span data-ttu-id="2ad4f-201">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="2ad4f-201">string</span></span> | <span data-ttu-id="2ad4f-202">sim</span><span class="sxs-lookup"><span data-stu-id="2ad4f-202">yes</span></span>      | <span data-ttu-id="2ad4f-203">A ID do pacote para relist</span><span class="sxs-lookup"><span data-stu-id="2ad4f-203">The ID of the package to relist</span></span>
<span data-ttu-id="2ad4f-204">VERSION</span><span class="sxs-lookup"><span data-stu-id="2ad4f-204">VERSION</span></span>        | <span data-ttu-id="2ad4f-205">URL</span><span class="sxs-lookup"><span data-stu-id="2ad4f-205">URL</span></span>    | <span data-ttu-id="2ad4f-206">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="2ad4f-206">string</span></span> | <span data-ttu-id="2ad4f-207">sim</span><span class="sxs-lookup"><span data-stu-id="2ad4f-207">yes</span></span>      | <span data-ttu-id="2ad4f-208">A versão do pacote a ser relist</span><span class="sxs-lookup"><span data-stu-id="2ad4f-208">The version of the package to relist</span></span>
<span data-ttu-id="2ad4f-209">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="2ad4f-209">X-NuGet-ApiKey</span></span> | <span data-ttu-id="2ad4f-210">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="2ad4f-210">Header</span></span> | <span data-ttu-id="2ad4f-211">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="2ad4f-211">string</span></span> | <span data-ttu-id="2ad4f-212">sim</span><span class="sxs-lookup"><span data-stu-id="2ad4f-212">yes</span></span>      | <span data-ttu-id="2ad4f-213">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="2ad4f-213">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="2ad4f-214">Resposta</span><span class="sxs-lookup"><span data-stu-id="2ad4f-214">Response</span></span>

<span data-ttu-id="2ad4f-215">Código de status</span><span class="sxs-lookup"><span data-stu-id="2ad4f-215">Status Code</span></span> | <span data-ttu-id="2ad4f-216">Significado</span><span class="sxs-lookup"><span data-stu-id="2ad4f-216">Meaning</span></span>
----------- | -------
<span data-ttu-id="2ad4f-217">204</span><span class="sxs-lookup"><span data-stu-id="2ad4f-217">204</span></span>         | <span data-ttu-id="2ad4f-218">O pacote agora está listado</span><span class="sxs-lookup"><span data-stu-id="2ad4f-218">The package is now listed</span></span>
<span data-ttu-id="2ad4f-219">404</span><span class="sxs-lookup"><span data-stu-id="2ad4f-219">404</span></span>         | <span data-ttu-id="2ad4f-220">Nenhum pacote com fornecido `ID` e `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="2ad4f-220">No package with the provided `ID` and `VERSION` exists</span></span>
