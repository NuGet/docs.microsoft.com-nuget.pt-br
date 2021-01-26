---
title: Enviar por push e excluir, API do NuGet
description: O serviço de publicação permite que os clientes publiquem novos pacotes e deslistem ou excluam pacotes existentes.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773925"
---
# <a name="push-and-delete"></a><span data-ttu-id="cefb3-103">Enviar por push e excluir</span><span class="sxs-lookup"><span data-stu-id="cefb3-103">Push and Delete</span></span>

<span data-ttu-id="cefb3-104">É possível enviar por push, excluir (ou deslistar, dependendo da implementação do servidor) e relistar os pacotes usando a API do NuGet v3.</span><span class="sxs-lookup"><span data-stu-id="cefb3-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="cefb3-105">Essas operações são baseadas no `PackagePublish` recurso encontrado no [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="cefb3-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="cefb3-106">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="cefb3-106">Versioning</span></span>

<span data-ttu-id="cefb3-107">O seguinte `@type` valor é usado:</span><span class="sxs-lookup"><span data-stu-id="cefb3-107">The following `@type` value is used:</span></span>

<span data-ttu-id="cefb3-108">@type valor</span><span class="sxs-lookup"><span data-stu-id="cefb3-108">@type value</span></span>          | <span data-ttu-id="cefb3-109">Observações</span><span class="sxs-lookup"><span data-stu-id="cefb3-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="cefb3-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="cefb3-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="cefb3-111">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="cefb3-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="cefb3-112">URL base</span><span class="sxs-lookup"><span data-stu-id="cefb3-112">Base URL</span></span>

<span data-ttu-id="cefb3-113">A URL base para as APIs a seguir é o valor da `@id` Propriedade do `PackagePublish/2.0.0` recurso no [índice de serviço](service-index.md)da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="cefb3-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="cefb3-114">Para a documentação abaixo, a URL do NuGet. org é usada.</span><span class="sxs-lookup"><span data-stu-id="cefb3-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="cefb3-115">Considere `https://www.nuget.org/api/v2/package` como um espaço reservado para o `@id` valor encontrado no índice de serviço.</span><span class="sxs-lookup"><span data-stu-id="cefb3-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="cefb3-116">Observe que essa URL aponta para o mesmo local que o ponto de extremidade de push v2 herdado, pois o protocolo é o mesmo.</span><span class="sxs-lookup"><span data-stu-id="cefb3-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="cefb3-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="cefb3-117">HTTP methods</span></span>

<span data-ttu-id="cefb3-118">`PUT` `POST` `DELETE` Esse recurso oferece suporte aos métodos http e.</span><span class="sxs-lookup"><span data-stu-id="cefb3-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="cefb3-119">Para quais métodos têm suporte em cada ponto de extremidade, consulte abaixo.</span><span class="sxs-lookup"><span data-stu-id="cefb3-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="cefb3-120">Enviar por push um pacote</span><span class="sxs-lookup"><span data-stu-id="cefb3-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="cefb3-121">o nuget.org tem [requisitos adicionais](NuGet-Protocols.md) para interagir com o ponto de extremidade de push.</span><span class="sxs-lookup"><span data-stu-id="cefb3-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="cefb3-122">o nuget.org dá suporte ao envio de novos pacotes usando a API a seguir.</span><span class="sxs-lookup"><span data-stu-id="cefb3-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="cefb3-123">Se o pacote com a ID e a versão fornecidas já existir, o nuget.org rejeitará o envio por push.</span><span class="sxs-lookup"><span data-stu-id="cefb3-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="cefb3-124">Outras origens de pacote podem dar suporte à substituição de um pacote existente.</span><span class="sxs-lookup"><span data-stu-id="cefb3-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="cefb3-125">Parâmetros da solicitação</span><span class="sxs-lookup"><span data-stu-id="cefb3-125">Request parameters</span></span>

<span data-ttu-id="cefb3-126">Nome</span><span class="sxs-lookup"><span data-stu-id="cefb3-126">Name</span></span>           | <span data-ttu-id="cefb3-127">Em</span><span class="sxs-lookup"><span data-stu-id="cefb3-127">In</span></span>     | <span data-ttu-id="cefb3-128">Type</span><span class="sxs-lookup"><span data-stu-id="cefb3-128">Type</span></span>   | <span data-ttu-id="cefb3-129">Necessária</span><span class="sxs-lookup"><span data-stu-id="cefb3-129">Required</span></span> | <span data-ttu-id="cefb3-130">Observações</span><span class="sxs-lookup"><span data-stu-id="cefb3-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="cefb3-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="cefb3-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="cefb3-132">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="cefb3-132">Header</span></span> | <span data-ttu-id="cefb3-133">string</span><span class="sxs-lookup"><span data-stu-id="cefb3-133">string</span></span> | <span data-ttu-id="cefb3-134">sim</span><span class="sxs-lookup"><span data-stu-id="cefb3-134">yes</span></span>      | <span data-ttu-id="cefb3-135">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="cefb3-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="cefb3-136">A chave de API é uma cadeia de caracteres opaca proveniente da origem do pacote pelo usuário e configurada no cliente.</span><span class="sxs-lookup"><span data-stu-id="cefb3-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="cefb3-137">Nenhum formato de cadeia de caracteres específico é obrigatório, mas o comprimento da chave de API não deve exceder um tamanho razoável para valores de cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="cefb3-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="cefb3-138">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="cefb3-138">Request body</span></span>

<span data-ttu-id="cefb3-139">O corpo da solicitação deve estar no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="cefb3-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="cefb3-140">Dados de formulário com várias partes</span><span class="sxs-lookup"><span data-stu-id="cefb3-140">Multipart form data</span></span>

<span data-ttu-id="cefb3-141">O cabeçalho da solicitação `Content-Type` é `multipart/form-data` e o primeiro item no corpo da solicitação são os bytes brutos de. nupkg sendo enviados por push.</span><span class="sxs-lookup"><span data-stu-id="cefb3-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="cefb3-142">Os itens subsequentes no corpo com diversas partes são ignorados.</span><span class="sxs-lookup"><span data-stu-id="cefb3-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="cefb3-143">O nome do arquivo ou quaisquer outros cabeçalhos dos itens com diversas partes são ignorados.</span><span class="sxs-lookup"><span data-stu-id="cefb3-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="cefb3-144">Resposta</span><span class="sxs-lookup"><span data-stu-id="cefb3-144">Response</span></span>

<span data-ttu-id="cefb3-145">Código de status</span><span class="sxs-lookup"><span data-stu-id="cefb3-145">Status Code</span></span> | <span data-ttu-id="cefb3-146">Significado</span><span class="sxs-lookup"><span data-stu-id="cefb3-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="cefb3-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="cefb3-147">201, 202</span></span>    | <span data-ttu-id="cefb3-148">O pacote foi enviado por push com êxito</span><span class="sxs-lookup"><span data-stu-id="cefb3-148">The package was successfully pushed</span></span>
<span data-ttu-id="cefb3-149">400</span><span class="sxs-lookup"><span data-stu-id="cefb3-149">400</span></span>         | <span data-ttu-id="cefb3-150">O pacote fornecido é inválido</span><span class="sxs-lookup"><span data-stu-id="cefb3-150">The provided package is invalid</span></span>
<span data-ttu-id="cefb3-151">409</span><span class="sxs-lookup"><span data-stu-id="cefb3-151">409</span></span>         | <span data-ttu-id="cefb3-152">Já existe um pacote com a ID e a versão fornecidas</span><span class="sxs-lookup"><span data-stu-id="cefb3-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="cefb3-153">Implementações de servidor variam no código de status de êxito retornado quando um pacote é enviado por push com êxito.</span><span class="sxs-lookup"><span data-stu-id="cefb3-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="cefb3-154">Excluir um pacote</span><span class="sxs-lookup"><span data-stu-id="cefb3-154">Delete a package</span></span>

<span data-ttu-id="cefb3-155">nuget.org interpreta a solicitação de exclusão de pacote como uma "deslista".</span><span class="sxs-lookup"><span data-stu-id="cefb3-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="cefb3-156">Isso significa que o pacote ainda está disponível para os consumidores existentes do pacote, mas o pacote não aparece mais nos resultados da pesquisa ou na interface da Web.</span><span class="sxs-lookup"><span data-stu-id="cefb3-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="cefb3-157">Para obter mais informações sobre essa prática, consulte a política de [pacotes excluídos](../nuget-org/policies/deleting-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="cefb3-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="cefb3-158">Outras implementações de servidor são livres para interpretar esse sinal como uma exclusão rígida, exclusão reversível ou deslistar.</span><span class="sxs-lookup"><span data-stu-id="cefb3-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="cefb3-159">Por exemplo, o [NuGet. Server](https://www.nuget.org/packages/NuGet.Server) (uma implementação de servidor que dá suporte apenas à API v2 mais antiga) dá suporte ao tratamento dessa solicitação como uma exclusão incorreta ou um disco rígido com base em uma opção de configuração.</span><span class="sxs-lookup"><span data-stu-id="cefb3-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="cefb3-160">Parâmetros da solicitação</span><span class="sxs-lookup"><span data-stu-id="cefb3-160">Request parameters</span></span>

<span data-ttu-id="cefb3-161">Nome</span><span class="sxs-lookup"><span data-stu-id="cefb3-161">Name</span></span>           | <span data-ttu-id="cefb3-162">Em</span><span class="sxs-lookup"><span data-stu-id="cefb3-162">In</span></span>     | <span data-ttu-id="cefb3-163">Type</span><span class="sxs-lookup"><span data-stu-id="cefb3-163">Type</span></span>   | <span data-ttu-id="cefb3-164">Necessária</span><span class="sxs-lookup"><span data-stu-id="cefb3-164">Required</span></span> | <span data-ttu-id="cefb3-165">Observações</span><span class="sxs-lookup"><span data-stu-id="cefb3-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="cefb3-166">ID</span><span class="sxs-lookup"><span data-stu-id="cefb3-166">ID</span></span>             | <span data-ttu-id="cefb3-167">URL</span><span class="sxs-lookup"><span data-stu-id="cefb3-167">URL</span></span>    | <span data-ttu-id="cefb3-168">string</span><span class="sxs-lookup"><span data-stu-id="cefb3-168">string</span></span> | <span data-ttu-id="cefb3-169">sim</span><span class="sxs-lookup"><span data-stu-id="cefb3-169">yes</span></span>      | <span data-ttu-id="cefb3-170">A ID do pacote a ser excluído</span><span class="sxs-lookup"><span data-stu-id="cefb3-170">The ID of the package to delete</span></span>
<span data-ttu-id="cefb3-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="cefb3-171">VERSION</span></span>        | <span data-ttu-id="cefb3-172">URL</span><span class="sxs-lookup"><span data-stu-id="cefb3-172">URL</span></span>    | <span data-ttu-id="cefb3-173">string</span><span class="sxs-lookup"><span data-stu-id="cefb3-173">string</span></span> | <span data-ttu-id="cefb3-174">sim</span><span class="sxs-lookup"><span data-stu-id="cefb3-174">yes</span></span>      | <span data-ttu-id="cefb3-175">A versão do pacote a ser excluído</span><span class="sxs-lookup"><span data-stu-id="cefb3-175">The version of the package to delete</span></span>
<span data-ttu-id="cefb3-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="cefb3-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="cefb3-177">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="cefb3-177">Header</span></span> | <span data-ttu-id="cefb3-178">string</span><span class="sxs-lookup"><span data-stu-id="cefb3-178">string</span></span> | <span data-ttu-id="cefb3-179">sim</span><span class="sxs-lookup"><span data-stu-id="cefb3-179">yes</span></span>      | <span data-ttu-id="cefb3-180">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="cefb3-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="cefb3-181">Resposta</span><span class="sxs-lookup"><span data-stu-id="cefb3-181">Response</span></span>

<span data-ttu-id="cefb3-182">Código de status</span><span class="sxs-lookup"><span data-stu-id="cefb3-182">Status Code</span></span> | <span data-ttu-id="cefb3-183">Significado</span><span class="sxs-lookup"><span data-stu-id="cefb3-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="cefb3-184">204</span><span class="sxs-lookup"><span data-stu-id="cefb3-184">204</span></span>         | <span data-ttu-id="cefb3-185">O pacote foi excluído</span><span class="sxs-lookup"><span data-stu-id="cefb3-185">The package was deleted</span></span>
<span data-ttu-id="cefb3-186">404</span><span class="sxs-lookup"><span data-stu-id="cefb3-186">404</span></span>         | <span data-ttu-id="cefb3-187">Nenhum pacote com o fornecido `ID` e `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="cefb3-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="cefb3-188">Relistar um pacote</span><span class="sxs-lookup"><span data-stu-id="cefb3-188">Relist a package</span></span>

<span data-ttu-id="cefb3-189">Se um pacote estiver deslistado, será possível tornar esse pacote mais uma vez visível nos resultados da pesquisa usando o ponto de extremidade "relistar".</span><span class="sxs-lookup"><span data-stu-id="cefb3-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="cefb3-190">Esse ponto de extremidade tem a mesma forma que o [ponto de extremidade de exclusão (deslistar)](#delete-a-package) , mas usa o `POST` método http em vez do `DELETE` método.</span><span class="sxs-lookup"><span data-stu-id="cefb3-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="cefb3-191">Se o pacote já estiver listado, a solicitação ainda terá sucesso.</span><span class="sxs-lookup"><span data-stu-id="cefb3-191">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="cefb3-192">Parâmetros da solicitação</span><span class="sxs-lookup"><span data-stu-id="cefb3-192">Request parameters</span></span>

<span data-ttu-id="cefb3-193">Nome</span><span class="sxs-lookup"><span data-stu-id="cefb3-193">Name</span></span>           | <span data-ttu-id="cefb3-194">Em</span><span class="sxs-lookup"><span data-stu-id="cefb3-194">In</span></span>     | <span data-ttu-id="cefb3-195">Type</span><span class="sxs-lookup"><span data-stu-id="cefb3-195">Type</span></span>   | <span data-ttu-id="cefb3-196">Necessária</span><span class="sxs-lookup"><span data-stu-id="cefb3-196">Required</span></span> | <span data-ttu-id="cefb3-197">Observações</span><span class="sxs-lookup"><span data-stu-id="cefb3-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="cefb3-198">ID</span><span class="sxs-lookup"><span data-stu-id="cefb3-198">ID</span></span>             | <span data-ttu-id="cefb3-199">URL</span><span class="sxs-lookup"><span data-stu-id="cefb3-199">URL</span></span>    | <span data-ttu-id="cefb3-200">string</span><span class="sxs-lookup"><span data-stu-id="cefb3-200">string</span></span> | <span data-ttu-id="cefb3-201">sim</span><span class="sxs-lookup"><span data-stu-id="cefb3-201">yes</span></span>      | <span data-ttu-id="cefb3-202">A ID do pacote a ser relistado</span><span class="sxs-lookup"><span data-stu-id="cefb3-202">The ID of the package to relist</span></span>
<span data-ttu-id="cefb3-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="cefb3-203">VERSION</span></span>        | <span data-ttu-id="cefb3-204">URL</span><span class="sxs-lookup"><span data-stu-id="cefb3-204">URL</span></span>    | <span data-ttu-id="cefb3-205">string</span><span class="sxs-lookup"><span data-stu-id="cefb3-205">string</span></span> | <span data-ttu-id="cefb3-206">sim</span><span class="sxs-lookup"><span data-stu-id="cefb3-206">yes</span></span>      | <span data-ttu-id="cefb3-207">A versão do pacote a ser relistada</span><span class="sxs-lookup"><span data-stu-id="cefb3-207">The version of the package to relist</span></span>
<span data-ttu-id="cefb3-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="cefb3-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="cefb3-209">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="cefb3-209">Header</span></span> | <span data-ttu-id="cefb3-210">string</span><span class="sxs-lookup"><span data-stu-id="cefb3-210">string</span></span> | <span data-ttu-id="cefb3-211">sim</span><span class="sxs-lookup"><span data-stu-id="cefb3-211">yes</span></span>      | <span data-ttu-id="cefb3-212">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="cefb3-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="cefb3-213">Resposta</span><span class="sxs-lookup"><span data-stu-id="cefb3-213">Response</span></span>

<span data-ttu-id="cefb3-214">Código de status</span><span class="sxs-lookup"><span data-stu-id="cefb3-214">Status Code</span></span> | <span data-ttu-id="cefb3-215">Significado</span><span class="sxs-lookup"><span data-stu-id="cefb3-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="cefb3-216">200</span><span class="sxs-lookup"><span data-stu-id="cefb3-216">200</span></span>         | <span data-ttu-id="cefb3-217">O pacote agora está listado</span><span class="sxs-lookup"><span data-stu-id="cefb3-217">The package is now listed</span></span>
<span data-ttu-id="cefb3-218">404</span><span class="sxs-lookup"><span data-stu-id="cefb3-218">404</span></span>         | <span data-ttu-id="cefb3-219">Nenhum pacote com o fornecido `ID` e `VERSION` existe</span><span class="sxs-lookup"><span data-stu-id="cefb3-219">No package with the provided `ID` and `VERSION` exists</span></span>
