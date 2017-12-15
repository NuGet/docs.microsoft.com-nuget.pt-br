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
ms.openlocfilehash: 1fa3c0e1698a11208d9ef29fdf26a4980cb60cf5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="push-and-delete"></a><span data-ttu-id="9a16b-104">Enviar por push e excluir</span><span class="sxs-lookup"><span data-stu-id="9a16b-104">Push and Delete</span></span>

<span data-ttu-id="9a16b-105">É possível enviar por push e excluir (ou remover da lista, dependendo da implementação de servidor) pacotes usando a API do NuGet V3.</span><span class="sxs-lookup"><span data-stu-id="9a16b-105">It is possible to push and delete (or unlist, depending on the server implementation) packages using the NuGet V3 API.</span></span>
<span data-ttu-id="9a16b-106">As duas operações baseiam-se do `PackagePublish` recurso encontrado na [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="9a16b-106">Both operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="9a16b-107">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="9a16b-107">Versioning</span></span>

<span data-ttu-id="9a16b-108">O seguinte `@type` valor é usado:</span><span class="sxs-lookup"><span data-stu-id="9a16b-108">The following `@type` value is used:</span></span>

<span data-ttu-id="9a16b-109">Valor @type</span><span class="sxs-lookup"><span data-stu-id="9a16b-109">@type value</span></span>          | <span data-ttu-id="9a16b-110">Observações</span><span class="sxs-lookup"><span data-stu-id="9a16b-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="9a16b-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="9a16b-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="9a16b-112">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="9a16b-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="9a16b-113">URL Base</span><span class="sxs-lookup"><span data-stu-id="9a16b-113">Base URL</span></span>

<span data-ttu-id="9a16b-114">A URL base para as seguintes APIs é o valor da `@id` propriedade o `PackagePublish/2.0.0` recursos na origem do pacote [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="9a16b-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="9a16b-115">Para obter a documentação abaixo URL do nuget.org é usado.</span><span class="sxs-lookup"><span data-stu-id="9a16b-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="9a16b-116">Considere `https://www.nuget.org/api/v2/package` como um espaço reservado para o `@id` valor encontrado no índice de serviço.</span><span class="sxs-lookup"><span data-stu-id="9a16b-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="9a16b-117">Observe que essa URL aponta para o mesmo local que o ponto de extremidade de envio por push herdado V2 como o protocolo é o mesmo.</span><span class="sxs-lookup"><span data-stu-id="9a16b-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="9a16b-118">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="9a16b-118">HTTP methods</span></span>

<span data-ttu-id="9a16b-119">O `PUT` e `DELETE` métodos HTTP compatíveis com esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9a16b-119">The `PUT` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="9a16b-120">Para quais métodos têm suporte em cada ponto de extremidade, consulte abaixo.</span><span class="sxs-lookup"><span data-stu-id="9a16b-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="9a16b-121">Enviar um pacote</span><span class="sxs-lookup"><span data-stu-id="9a16b-121">Push a package</span></span>

<span data-ttu-id="9a16b-122">NuGet.org dá suporte a envio novos pacotes usando a seguinte API.</span><span class="sxs-lookup"><span data-stu-id="9a16b-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="9a16b-123">Se o pacote com a ID e a versão fornecida já existir, nuget.org rejeitará o envio por push.</span><span class="sxs-lookup"><span data-stu-id="9a16b-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="9a16b-124">Outras fontes de pacote podem oferecer suporte a substituição de um pacote existente.</span><span class="sxs-lookup"><span data-stu-id="9a16b-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="9a16b-125">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="9a16b-125">Request parameters</span></span>

<span data-ttu-id="9a16b-126">Nome</span><span class="sxs-lookup"><span data-stu-id="9a16b-126">Name</span></span>           | <span data-ttu-id="9a16b-127">No</span><span class="sxs-lookup"><span data-stu-id="9a16b-127">In</span></span>     | <span data-ttu-id="9a16b-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="9a16b-128">Type</span></span>   | <span data-ttu-id="9a16b-129">Necessária</span><span class="sxs-lookup"><span data-stu-id="9a16b-129">Required</span></span> | <span data-ttu-id="9a16b-130">Observações</span><span class="sxs-lookup"><span data-stu-id="9a16b-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="9a16b-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="9a16b-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="9a16b-132">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="9a16b-132">Header</span></span> | <span data-ttu-id="9a16b-133">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9a16b-133">string</span></span> | <span data-ttu-id="9a16b-134">sim</span><span class="sxs-lookup"><span data-stu-id="9a16b-134">yes</span></span>      | <span data-ttu-id="9a16b-135">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="9a16b-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="9a16b-136">A chave de API é uma cadeia de caracteres opaca obtidos de origem do pacote pelo usuário e configurado no cliente.</span><span class="sxs-lookup"><span data-stu-id="9a16b-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="9a16b-137">Nenhum formato de cadeia de caracteres específica é obrigatória, mas o comprimento da chave de API não deve exceder um tamanho razoável para valores de cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="9a16b-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="9a16b-138">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="9a16b-138">Request body</span></span>

<span data-ttu-id="9a16b-139">O corpo da solicitação deve ser da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="9a16b-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="9a16b-140">Dados de formulário de várias partes</span><span class="sxs-lookup"><span data-stu-id="9a16b-140">Multipart form data</span></span>

<span data-ttu-id="9a16b-141">O cabeçalho de solicitação `Content-Type` é `multipart/form-data` e o primeiro item no corpo da solicitação é os bytes brutos do nupkg sendo enviado.</span><span class="sxs-lookup"><span data-stu-id="9a16b-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="9a16b-142">Itens subsequentes no corpo com diversas partes são ignorados.</span><span class="sxs-lookup"><span data-stu-id="9a16b-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="9a16b-143">O nome do arquivo ou quaisquer outros cabeçalhos dos itens de várias partes são ignorados.</span><span class="sxs-lookup"><span data-stu-id="9a16b-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="9a16b-144">Resposta</span><span class="sxs-lookup"><span data-stu-id="9a16b-144">Response</span></span>

<span data-ttu-id="9a16b-145">Código de status</span><span class="sxs-lookup"><span data-stu-id="9a16b-145">Status Code</span></span> | <span data-ttu-id="9a16b-146">Significado</span><span class="sxs-lookup"><span data-stu-id="9a16b-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="9a16b-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="9a16b-147">201, 202</span></span>    | <span data-ttu-id="9a16b-148">O pacote foi enviado com êxito</span><span class="sxs-lookup"><span data-stu-id="9a16b-148">The package was successfully pushed</span></span>
<span data-ttu-id="9a16b-149">400</span><span class="sxs-lookup"><span data-stu-id="9a16b-149">400</span></span>         | <span data-ttu-id="9a16b-150">O pacote fornecido é inválido</span><span class="sxs-lookup"><span data-stu-id="9a16b-150">The provided package is invalid</span></span>
<span data-ttu-id="9a16b-151">409</span><span class="sxs-lookup"><span data-stu-id="9a16b-151">409</span></span>         | <span data-ttu-id="9a16b-152">Já existe um pacote com a ID e a versão fornecida</span><span class="sxs-lookup"><span data-stu-id="9a16b-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="9a16b-153">Implementações de servidor variam de acordo o código de status de êxito retornado quando um pacote é enviado com êxito.</span><span class="sxs-lookup"><span data-stu-id="9a16b-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="9a16b-154">Excluir um pacote</span><span class="sxs-lookup"><span data-stu-id="9a16b-154">Delete a package</span></span>

<span data-ttu-id="9a16b-155">NuGet.org interpreta a solicitação de exclusão do pacote como um "remover da lista".</span><span class="sxs-lookup"><span data-stu-id="9a16b-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="9a16b-156">Isso significa que o pacote ainda está disponível para os consumidores existentes do pacote, mas o pacote não aparece nos resultados da pesquisa ou na interface da web.</span><span class="sxs-lookup"><span data-stu-id="9a16b-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="9a16b-157">Para obter mais informações sobre esta prática, consulte o [pacotes excluído](../policies/deleting-packages.md) política.</span><span class="sxs-lookup"><span data-stu-id="9a16b-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="9a16b-158">Outras implementações do servidor estão livres para interpretar esse sinal como uma exclusão de disco rígida, exclusão reversível ou remover da lista.</span><span class="sxs-lookup"><span data-stu-id="9a16b-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="9a16b-159">Por exemplo, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (uma implementação de servidor somente com suporte a mais antiga API V2) oferece suporte à manipulação esta solicitação como um unlist ou uma exclusão de disco rígida com base em uma opção de configuração.</span><span class="sxs-lookup"><span data-stu-id="9a16b-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="9a16b-160">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="9a16b-160">Request parameters</span></span>

<span data-ttu-id="9a16b-161">Nome</span><span class="sxs-lookup"><span data-stu-id="9a16b-161">Name</span></span>           | <span data-ttu-id="9a16b-162">No</span><span class="sxs-lookup"><span data-stu-id="9a16b-162">In</span></span>     | <span data-ttu-id="9a16b-163">Tipo</span><span class="sxs-lookup"><span data-stu-id="9a16b-163">Type</span></span>   | <span data-ttu-id="9a16b-164">Necessária</span><span class="sxs-lookup"><span data-stu-id="9a16b-164">Required</span></span> | <span data-ttu-id="9a16b-165">Observações</span><span class="sxs-lookup"><span data-stu-id="9a16b-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="9a16b-166">ID</span><span class="sxs-lookup"><span data-stu-id="9a16b-166">ID</span></span>             | <span data-ttu-id="9a16b-167">URL</span><span class="sxs-lookup"><span data-stu-id="9a16b-167">URL</span></span>    | <span data-ttu-id="9a16b-168">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9a16b-168">string</span></span> | <span data-ttu-id="9a16b-169">sim</span><span class="sxs-lookup"><span data-stu-id="9a16b-169">yes</span></span>      | <span data-ttu-id="9a16b-170">A ID do pacote a ser excluído</span><span class="sxs-lookup"><span data-stu-id="9a16b-170">The ID of the package to delete</span></span>
<span data-ttu-id="9a16b-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="9a16b-171">VERSION</span></span>        | <span data-ttu-id="9a16b-172">URL</span><span class="sxs-lookup"><span data-stu-id="9a16b-172">URL</span></span>    | <span data-ttu-id="9a16b-173">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9a16b-173">string</span></span> | <span data-ttu-id="9a16b-174">sim</span><span class="sxs-lookup"><span data-stu-id="9a16b-174">yes</span></span>      | <span data-ttu-id="9a16b-175">A versão do pacote a excluir</span><span class="sxs-lookup"><span data-stu-id="9a16b-175">The version of the package to delete</span></span>
<span data-ttu-id="9a16b-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="9a16b-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="9a16b-177">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="9a16b-177">Header</span></span> | <span data-ttu-id="9a16b-178">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="9a16b-178">string</span></span> | <span data-ttu-id="9a16b-179">sim</span><span class="sxs-lookup"><span data-stu-id="9a16b-179">yes</span></span>      | <span data-ttu-id="9a16b-180">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="9a16b-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="9a16b-181">Resposta</span><span class="sxs-lookup"><span data-stu-id="9a16b-181">Response</span></span>

<span data-ttu-id="9a16b-182">Código de status</span><span class="sxs-lookup"><span data-stu-id="9a16b-182">Status Code</span></span> | <span data-ttu-id="9a16b-183">Significado</span><span class="sxs-lookup"><span data-stu-id="9a16b-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="9a16b-184">204</span><span class="sxs-lookup"><span data-stu-id="9a16b-184">204</span></span>         | <span data-ttu-id="9a16b-185">O pacote foi excluído</span><span class="sxs-lookup"><span data-stu-id="9a16b-185">The package was deleted</span></span>
<span data-ttu-id="9a16b-186">404</span><span class="sxs-lookup"><span data-stu-id="9a16b-186">404</span></span>         | <span data-ttu-id="9a16b-187">Nenhum pacote com fornecido `ID` e `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="9a16b-187">No package with the provided `ID` and `VERSION` exists</span></span>
