---
title: Protocolos de NuGet.org | Microsoft Docs
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Os protocolos nuget.org em evolução para interagir com os clientes do NuGet."
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 488a86a36a6bc83c91f0182bf437ddb83e707e31
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="98cde-103">protocolos de NuGet.org</span><span class="sxs-lookup"><span data-stu-id="98cde-103">nuget.org protocols</span></span>

<span data-ttu-id="98cde-104">Para interagir com nuget.org, os clientes precisam seguir determinados protocolos.</span><span class="sxs-lookup"><span data-stu-id="98cde-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="98cde-105">Como mantenham em evolução esses protocolos, clientes devem identificar a versão de protocolo usada ao chamar APIs do nuget.org específico.</span><span class="sxs-lookup"><span data-stu-id="98cde-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="98cde-106">Isso permite nuget.org introduzir alterações de forma incondicional para os clientes antigos.</span><span class="sxs-lookup"><span data-stu-id="98cde-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="98cde-107">As APIs documentadas nesta página são específicas para nuget.org e não há nenhuma expectativa de outras implementações de servidor NuGet introduzir essas APIs.</span><span class="sxs-lookup"><span data-stu-id="98cde-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="98cde-108">Para obter informações sobre a API do NuGet amplamente implementados em ecossistema do NuGet, consulte o [visão geral da API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="98cde-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="98cde-109">Este tópico lista os vários protocolos como e quando eles surgem existência.</span><span class="sxs-lookup"><span data-stu-id="98cde-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="98cde-110">Versão de protocolo do NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="98cde-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="98cde-111">O 4.1.0 protocolo Especifica o uso de chaves de escopo verificar para interagir com os serviços que não sejam nuget.org, para validar um pacote em uma conta do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="98cde-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="98cde-112">Observe que o `4.1.0` versão número é uma cadeia de caracteres opaca mas acontece coincidir com a primeira versão do cliente NuGet oficial que suporte esse protocolo.</span><span class="sxs-lookup"><span data-stu-id="98cde-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="98cde-113">A validação garante que as chaves de API criada pelo usuário são usadas apenas com nuget.org, e essa verificação ou validação de um serviço de terceiros é tratada por meio de uma chave de escopo verificar uso uma única vez.</span><span class="sxs-lookup"><span data-stu-id="98cde-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="98cde-114">Essas chaves de escopo verificar podem ser usados para validar que o pacote pertence a um determinado usuário (conta) em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="98cde-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="98cde-115">Requisito de cliente</span><span class="sxs-lookup"><span data-stu-id="98cde-115">Client requirement</span></span>

<span data-ttu-id="98cde-116">Os clientes precisam passar o seguinte cabeçalho quando fazem chamadas de API para **push** pacotes nuget.org:</span><span class="sxs-lookup"><span data-stu-id="98cde-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

    X-NuGet-Protocol-Version: 4.1.0

<span data-ttu-id="98cde-117">Observe que o `X-NuGet-Client-Version` cabeçalho possui uma semântica semelhante, mas é reservado para ser usado apenas pelo cliente do NuGet oficial.</span><span class="sxs-lookup"><span data-stu-id="98cde-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="98cde-118">Os clientes de terceiros devem usar o `X-NuGet-Protocol-Version` cabeçalho e o valor.</span><span class="sxs-lookup"><span data-stu-id="98cde-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="98cde-119">O **push** próprio protocolo é descrito na documentação para o [ `PackagePublish` recurso](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="98cde-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="98cde-120">Se um cliente interage com serviços externos e precisa validar se um pacote pertence a um determinado usuário (conta), ele deve usar o protocolo a seguir e use as teclas de escopo de verificar e não as chaves de API do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="98cde-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="98cde-121">API para solicitar uma chave de escopo de verificar</span><span class="sxs-lookup"><span data-stu-id="98cde-121">API to request a verify-scope key</span></span>

<span data-ttu-id="98cde-122">Essa API é usada para obter uma chave Verifique se o escopo para um autor nuget.org validar um pacote pertencente a ele.</span><span class="sxs-lookup"><span data-stu-id="98cde-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="98cde-123">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="98cde-123">Request parameters</span></span>

<span data-ttu-id="98cde-124">Nome</span><span class="sxs-lookup"><span data-stu-id="98cde-124">Name</span></span>           | <span data-ttu-id="98cde-125">No</span><span class="sxs-lookup"><span data-stu-id="98cde-125">In</span></span>     | <span data-ttu-id="98cde-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="98cde-126">Type</span></span>   | <span data-ttu-id="98cde-127">Necessária</span><span class="sxs-lookup"><span data-stu-id="98cde-127">Required</span></span> | <span data-ttu-id="98cde-128">Observações</span><span class="sxs-lookup"><span data-stu-id="98cde-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="98cde-129">ID</span><span class="sxs-lookup"><span data-stu-id="98cde-129">ID</span></span>             | <span data-ttu-id="98cde-130">URL</span><span class="sxs-lookup"><span data-stu-id="98cde-130">URL</span></span>    | <span data-ttu-id="98cde-131">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="98cde-131">string</span></span> | <span data-ttu-id="98cde-132">sim</span><span class="sxs-lookup"><span data-stu-id="98cde-132">yes</span></span>      | <span data-ttu-id="98cde-133">O identidier de pacote para o qual a chave de escopo de verificar é solicitada</span><span class="sxs-lookup"><span data-stu-id="98cde-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="98cde-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="98cde-134">VERSION</span></span>        | <span data-ttu-id="98cde-135">URL</span><span class="sxs-lookup"><span data-stu-id="98cde-135">URL</span></span>    | <span data-ttu-id="98cde-136">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="98cde-136">string</span></span> | <span data-ttu-id="98cde-137">no</span><span class="sxs-lookup"><span data-stu-id="98cde-137">no</span></span>       | <span data-ttu-id="98cde-138">A versão do pacote</span><span class="sxs-lookup"><span data-stu-id="98cde-138">The package version</span></span>
<span data-ttu-id="98cde-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="98cde-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="98cde-140">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="98cde-140">Header</span></span> | <span data-ttu-id="98cde-141">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="98cde-141">string</span></span> | <span data-ttu-id="98cde-142">sim</span><span class="sxs-lookup"><span data-stu-id="98cde-142">yes</span></span>      | <span data-ttu-id="98cde-143">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="98cde-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="98cde-144">Resposta</span><span class="sxs-lookup"><span data-stu-id="98cde-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="98cde-145">API para verificar a chave de escopo de verificar</span><span class="sxs-lookup"><span data-stu-id="98cde-145">API to verify the verify scope key</span></span>

<span data-ttu-id="98cde-146">Essa API é usada para validar uma chave Verifique se o escopo para o pacote de propriedade pelo autor do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="98cde-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="98cde-147">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="98cde-147">Request parameters</span></span>

<span data-ttu-id="98cde-148">Nome</span><span class="sxs-lookup"><span data-stu-id="98cde-148">Name</span></span>           | <span data-ttu-id="98cde-149">No</span><span class="sxs-lookup"><span data-stu-id="98cde-149">In</span></span>     | <span data-ttu-id="98cde-150">Tipo</span><span class="sxs-lookup"><span data-stu-id="98cde-150">Type</span></span>   | <span data-ttu-id="98cde-151">Necessária</span><span class="sxs-lookup"><span data-stu-id="98cde-151">Required</span></span> | <span data-ttu-id="98cde-152">Observações</span><span class="sxs-lookup"><span data-stu-id="98cde-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="98cde-153">ID</span><span class="sxs-lookup"><span data-stu-id="98cde-153">ID</span></span>             | <span data-ttu-id="98cde-154">URL</span><span class="sxs-lookup"><span data-stu-id="98cde-154">URL</span></span>    | <span data-ttu-id="98cde-155">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="98cde-155">string</span></span> | <span data-ttu-id="98cde-156">sim</span><span class="sxs-lookup"><span data-stu-id="98cde-156">yes</span></span>      | <span data-ttu-id="98cde-157">O identificador de pacote para o qual a chave de escopo de verificar é solicitada</span><span class="sxs-lookup"><span data-stu-id="98cde-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="98cde-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="98cde-158">VERSION</span></span>        | <span data-ttu-id="98cde-159">URL</span><span class="sxs-lookup"><span data-stu-id="98cde-159">URL</span></span>    | <span data-ttu-id="98cde-160">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="98cde-160">string</span></span> | <span data-ttu-id="98cde-161">no</span><span class="sxs-lookup"><span data-stu-id="98cde-161">no</span></span>       | <span data-ttu-id="98cde-162">A versão do pacote</span><span class="sxs-lookup"><span data-stu-id="98cde-162">The package version</span></span>
<span data-ttu-id="98cde-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="98cde-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="98cde-164">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="98cde-164">Header</span></span> | <span data-ttu-id="98cde-165">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="98cde-165">string</span></span> | <span data-ttu-id="98cde-166">sim</span><span class="sxs-lookup"><span data-stu-id="98cde-166">yes</span></span>      | <span data-ttu-id="98cde-167">Por exemplo, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="98cde-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="98cde-168">Essa chave de API do escopo verificar expira em um dia ou no primeiro uso, o que ocorrer primeiro.</span><span class="sxs-lookup"><span data-stu-id="98cde-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="98cde-169">Resposta</span><span class="sxs-lookup"><span data-stu-id="98cde-169">Response</span></span>

<span data-ttu-id="98cde-170">Código de status</span><span class="sxs-lookup"><span data-stu-id="98cde-170">Status Code</span></span> | <span data-ttu-id="98cde-171">Significado</span><span class="sxs-lookup"><span data-stu-id="98cde-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="98cde-172">200</span><span class="sxs-lookup"><span data-stu-id="98cde-172">200</span></span>         | <span data-ttu-id="98cde-173">A chave de API é válida</span><span class="sxs-lookup"><span data-stu-id="98cde-173">The API key is valid</span></span>
<span data-ttu-id="98cde-174">403</span><span class="sxs-lookup"><span data-stu-id="98cde-174">403</span></span>         | <span data-ttu-id="98cde-175">A chave de API é inválida ou não autorizado a enviar por push contra o pacote</span><span class="sxs-lookup"><span data-stu-id="98cde-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="98cde-176">404</span><span class="sxs-lookup"><span data-stu-id="98cde-176">404</span></span>         | <span data-ttu-id="98cde-177">O pacote referenciado por `ID` e `VERSION` (opcional) não existe</span><span class="sxs-lookup"><span data-stu-id="98cde-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
