---
title: Protocolos de NuGet.org | Microsoft Docs
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba1d9742-9f1c-42ff-8c30-8e953e23c501
description: "Os protocolos nuget.org em evolução para interagir com os clientes do NuGet."
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 0bc71795d120256b9eb14ca64141f0b69f01e620
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="f49db-103">Protocolos de NuGet.org</span><span class="sxs-lookup"><span data-stu-id="f49db-103">nuget.org Protocols</span></span>

<span data-ttu-id="f49db-104">Para interagir com nuget.org, os clientes precisam seguir determinados protocolos.</span><span class="sxs-lookup"><span data-stu-id="f49db-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="f49db-105">Como mantenham em evolução esses protocolos, clientes devem identificar a versão de protocolo usada ao chamar APIs do nuget.org específico.</span><span class="sxs-lookup"><span data-stu-id="f49db-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="f49db-106">Isso permite nuget.org introduzir alterações de forma incondicional para os clientes antigos.</span><span class="sxs-lookup"><span data-stu-id="f49db-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="f49db-107">As APIs documentadas nesta página são específicas para nuget.org e não há nenhuma expectativa de outras implementações de servidor NuGet introduzir essas APIs.</span><span class="sxs-lookup"><span data-stu-id="f49db-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="f49db-108">Para obter informações sobre a API do NuGet amplamente implementados em ecossistema do NuGet, consulte o [visão geral da API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="f49db-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="f49db-109">Este tópico lista os vários protocolos como e quando eles surgem existência.</span><span class="sxs-lookup"><span data-stu-id="f49db-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="f49db-110">Versão de protocolo do NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="f49db-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="f49db-111">O 4.1.0 protocolo Especifica o uso de chaves de escopo verificar para interagir com os serviços que não sejam nuget.org, para validar um pacote em uma conta do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f49db-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="f49db-112">Observe que o `4.1.0` versão número é uma cadeia de caracteres opaca mas acontece coincidir com a primeira versão do cliente NuGet oficial que suporte esse protocolo.</span><span class="sxs-lookup"><span data-stu-id="f49db-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="f49db-113">A validação garante que as chaves de API criada pelo usuário são usadas apenas com nuget.org, e essa verificação ou validação de um serviço de terceiros é tratada por meio de uma chave de escopo verificar uso uma única vez.</span><span class="sxs-lookup"><span data-stu-id="f49db-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="f49db-114">Essas chaves de escopo verificar podem ser usados para validar que o pacote pertence a um determinado usuário (conta) em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f49db-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="f49db-115">Requisito de cliente</span><span class="sxs-lookup"><span data-stu-id="f49db-115">Client requirement</span></span>

<span data-ttu-id="f49db-116">Os clientes precisam passar o seguinte cabeçalho quando fazem chamadas de API para **push** pacotes nuget.org:</span><span class="sxs-lookup"><span data-stu-id="f49db-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="f49db-117">Observe que o `X-NuGet-Client-Version` cabeçalho possui uma semântica semelhante, mas é reservado para ser usado apenas pelo cliente do NuGet oficial.</span><span class="sxs-lookup"><span data-stu-id="f49db-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="f49db-118">Os clientes de terceiros devem usar o `X-NuGet-Protocol-Version` cabeçalho e o valor.</span><span class="sxs-lookup"><span data-stu-id="f49db-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="f49db-119">O **push** próprio protocolo é descrito na documentação para o [ `PackagePublish` recurso](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="f49db-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="f49db-120">Se um cliente interage com serviços externos e precisa validar se um pacote pertence a um determinado usuário (conta), ele deve usar o protocolo a seguir e use as teclas de escopo de verificar e não as chaves de API do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f49db-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="f49db-121">API para solicitar uma chave de escopo de verificar</span><span class="sxs-lookup"><span data-stu-id="f49db-121">API to request a verify-scope key</span></span>

<span data-ttu-id="f49db-122">Essa API é usada para obter uma chave Verifique se o escopo para um autor nuget.org validar um pacote pertencente a ele.</span><span class="sxs-lookup"><span data-stu-id="f49db-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="f49db-123">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="f49db-123">Request parameters</span></span>

<span data-ttu-id="f49db-124">Nome</span><span class="sxs-lookup"><span data-stu-id="f49db-124">Name</span></span>           | <span data-ttu-id="f49db-125">No</span><span class="sxs-lookup"><span data-stu-id="f49db-125">In</span></span>     | <span data-ttu-id="f49db-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="f49db-126">Type</span></span>   | <span data-ttu-id="f49db-127">Necessária</span><span class="sxs-lookup"><span data-stu-id="f49db-127">Required</span></span> | <span data-ttu-id="f49db-128">Observações</span><span class="sxs-lookup"><span data-stu-id="f49db-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="f49db-129">ID</span><span class="sxs-lookup"><span data-stu-id="f49db-129">ID</span></span>             | <span data-ttu-id="f49db-130">URL</span><span class="sxs-lookup"><span data-stu-id="f49db-130">URL</span></span>    | <span data-ttu-id="f49db-131">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f49db-131">string</span></span> | <span data-ttu-id="f49db-132">sim</span><span class="sxs-lookup"><span data-stu-id="f49db-132">yes</span></span>      | <span data-ttu-id="f49db-133">O identidier de pacote para o qual a chave de escopo de verificar é solicitada</span><span class="sxs-lookup"><span data-stu-id="f49db-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="f49db-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="f49db-134">VERSION</span></span>        | <span data-ttu-id="f49db-135">URL</span><span class="sxs-lookup"><span data-stu-id="f49db-135">URL</span></span>    | <span data-ttu-id="f49db-136">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f49db-136">string</span></span> | <span data-ttu-id="f49db-137">no</span><span class="sxs-lookup"><span data-stu-id="f49db-137">no</span></span>       | <span data-ttu-id="f49db-138">A versão do pacote</span><span class="sxs-lookup"><span data-stu-id="f49db-138">The package version</span></span>
<span data-ttu-id="f49db-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="f49db-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="f49db-140">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="f49db-140">Header</span></span> | <span data-ttu-id="f49db-141">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f49db-141">string</span></span> | <span data-ttu-id="f49db-142">sim</span><span class="sxs-lookup"><span data-stu-id="f49db-142">yes</span></span>      | <span data-ttu-id="f49db-143">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="f49db-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="f49db-144">Resposta</span><span class="sxs-lookup"><span data-stu-id="f49db-144">Response</span></span>

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="f49db-145">API para verificar a chave de escopo de verificar</span><span class="sxs-lookup"><span data-stu-id="f49db-145">API to verify the verify scope key</span></span>

<span data-ttu-id="f49db-146">Essa API é usada para validar uma chave Verifique se o escopo para o pacote de propriedade pelo autor do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f49db-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="f49db-147">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="f49db-147">Request parameters</span></span>

<span data-ttu-id="f49db-148">Nome</span><span class="sxs-lookup"><span data-stu-id="f49db-148">Name</span></span>           | <span data-ttu-id="f49db-149">No</span><span class="sxs-lookup"><span data-stu-id="f49db-149">In</span></span>     | <span data-ttu-id="f49db-150">Tipo</span><span class="sxs-lookup"><span data-stu-id="f49db-150">Type</span></span>   | <span data-ttu-id="f49db-151">Necessária</span><span class="sxs-lookup"><span data-stu-id="f49db-151">Required</span></span> | <span data-ttu-id="f49db-152">Observações</span><span class="sxs-lookup"><span data-stu-id="f49db-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="f49db-153">ID</span><span class="sxs-lookup"><span data-stu-id="f49db-153">ID</span></span>             | <span data-ttu-id="f49db-154">URL</span><span class="sxs-lookup"><span data-stu-id="f49db-154">URL</span></span>    | <span data-ttu-id="f49db-155">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f49db-155">string</span></span> | <span data-ttu-id="f49db-156">sim</span><span class="sxs-lookup"><span data-stu-id="f49db-156">yes</span></span>      | <span data-ttu-id="f49db-157">O identificador de pacote para o qual a chave de escopo de verificar é solicitada</span><span class="sxs-lookup"><span data-stu-id="f49db-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="f49db-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="f49db-158">VERSION</span></span>        | <span data-ttu-id="f49db-159">URL</span><span class="sxs-lookup"><span data-stu-id="f49db-159">URL</span></span>    | <span data-ttu-id="f49db-160">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f49db-160">string</span></span> | <span data-ttu-id="f49db-161">no</span><span class="sxs-lookup"><span data-stu-id="f49db-161">no</span></span>       | <span data-ttu-id="f49db-162">A versão do pacote</span><span class="sxs-lookup"><span data-stu-id="f49db-162">The package version</span></span>
<span data-ttu-id="f49db-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="f49db-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="f49db-164">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="f49db-164">Header</span></span> | <span data-ttu-id="f49db-165">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f49db-165">string</span></span> | <span data-ttu-id="f49db-166">sim</span><span class="sxs-lookup"><span data-stu-id="f49db-166">yes</span></span>      | <span data-ttu-id="f49db-167">Por exemplo, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="f49db-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="f49db-168">Essa chave de API do escopo verificar expira em um dia ou no primeiro uso, o que ocorrer primeiro.</span><span class="sxs-lookup"><span data-stu-id="f49db-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="f49db-169">Resposta</span><span class="sxs-lookup"><span data-stu-id="f49db-169">Response</span></span>

<span data-ttu-id="f49db-170">Código de status</span><span class="sxs-lookup"><span data-stu-id="f49db-170">Status Code</span></span> | <span data-ttu-id="f49db-171">Significado</span><span class="sxs-lookup"><span data-stu-id="f49db-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="f49db-172">200</span><span class="sxs-lookup"><span data-stu-id="f49db-172">200</span></span>         | <span data-ttu-id="f49db-173">A chave de API é válida</span><span class="sxs-lookup"><span data-stu-id="f49db-173">The API key is valid</span></span>
<span data-ttu-id="f49db-174">403</span><span class="sxs-lookup"><span data-stu-id="f49db-174">403</span></span>         | <span data-ttu-id="f49db-175">A chave de API é inválida ou não autorizado a enviar por push contra o pacote</span><span class="sxs-lookup"><span data-stu-id="f49db-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="f49db-176">404</span><span class="sxs-lookup"><span data-stu-id="f49db-176">404</span></span>         | <span data-ttu-id="f49db-177">O pacote referenciado por `ID` e `VERSION` (opcional) não existe</span><span class="sxs-lookup"><span data-stu-id="f49db-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
