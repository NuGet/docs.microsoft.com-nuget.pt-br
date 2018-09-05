---
title: Protocolos NuGet.org
description: Os protocolos nuget.org em evolução para interagir com os clientes do NuGet.
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547267"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="50eb0-103">protocolos NuGet.org</span><span class="sxs-lookup"><span data-stu-id="50eb0-103">nuget.org protocols</span></span>

<span data-ttu-id="50eb0-104">Para interagir com o nuget.org, os clientes precisam seguir determinados protocolos.</span><span class="sxs-lookup"><span data-stu-id="50eb0-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="50eb0-105">Porque esses protocolos mantenham evoluindo, os clientes devem identificar a versão do protocolo usarem ao chamar APIs de nuget.org específico.</span><span class="sxs-lookup"><span data-stu-id="50eb0-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="50eb0-106">Isso permite que o nuget.org introduzir alterações de forma incondicional para os clientes antigos.</span><span class="sxs-lookup"><span data-stu-id="50eb0-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="50eb0-107">As APIs documentadas nesta página são específicas para o nuget.org e não há nenhuma expectativa de outras implementações de servidor do NuGet introduzir essas APIs.</span><span class="sxs-lookup"><span data-stu-id="50eb0-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="50eb0-108">Para obter informações sobre a API do NuGet amplamente implementada no ecossistema do NuGet, consulte o [visão geral da API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="50eb0-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="50eb0-109">Este tópico lista os vários protocolos, como e quando eles vêm à existência.</span><span class="sxs-lookup"><span data-stu-id="50eb0-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="50eb0-110">Versão de protocolo do NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="50eb0-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="50eb0-111">A 4.1.0 especifica o protocolo de uso de chaves de escopo verificar para interagir com serviços diferentes do nuget.org, a fim de validar um pacote em uma conta do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="50eb0-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="50eb0-112">Observe que o `4.1.0` versão número é uma cadeia de caracteres opaca, mas coincidir com a primeira versão do cliente do NuGet oficial que suporte esse protocolo.</span><span class="sxs-lookup"><span data-stu-id="50eb0-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="50eb0-113">A validação garante que as chaves de API criados pelo usuário são usadas somente com nuget.org e essa verificação ou validação de um serviço de terceiros é tratada por meio de chaves de escopo verificar um único uso.</span><span class="sxs-lookup"><span data-stu-id="50eb0-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="50eb0-114">Essas chaves de escopo verificar podem ser usados para validar que o pacote pertence a um usuário específico (conta) em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="50eb0-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="50eb0-115">Requisito de cliente</span><span class="sxs-lookup"><span data-stu-id="50eb0-115">Client requirement</span></span>

<span data-ttu-id="50eb0-116">Os clientes devem passar o cabeçalho a seguir ao fazer chamadas à API **push** pacotes para nuget.org:</span><span class="sxs-lookup"><span data-stu-id="50eb0-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

    X-NuGet-Protocol-Version: 4.1.0

<span data-ttu-id="50eb0-117">Observe que o `X-NuGet-Client-Version` cabeçalho tem semântica semelhantes, mas está reservado para ser usado apenas pelo cliente do NuGet oficial.</span><span class="sxs-lookup"><span data-stu-id="50eb0-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="50eb0-118">Os clientes de terceiros devem usar o `X-NuGet-Protocol-Version` cabeçalho e o valor.</span><span class="sxs-lookup"><span data-stu-id="50eb0-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="50eb0-119">O **push** protocolo em si é descrito na documentação para o [ `PackagePublish` recurso](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="50eb0-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="50eb0-120">Se um cliente interage com serviços externos e necessidades para validar se um pacote pertence a um usuário específico (conta), ele deve usar o protocolo a seguir e usar as teclas de Verifique se o escopo e não as chaves de API do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="50eb0-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="50eb0-121">API para solicitar uma chave Verifique se o escopo</span><span class="sxs-lookup"><span data-stu-id="50eb0-121">API to request a verify-scope key</span></span>

<span data-ttu-id="50eb0-122">Essa API é usada para obter uma chave Verifique se o escopo para um autor de nuget.org validar um pacote pertencente a pessoa.</span><span class="sxs-lookup"><span data-stu-id="50eb0-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="50eb0-123">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="50eb0-123">Request parameters</span></span>

<span data-ttu-id="50eb0-124">Nome</span><span class="sxs-lookup"><span data-stu-id="50eb0-124">Name</span></span>           | <span data-ttu-id="50eb0-125">No</span><span class="sxs-lookup"><span data-stu-id="50eb0-125">In</span></span>     | <span data-ttu-id="50eb0-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="50eb0-126">Type</span></span>   | <span data-ttu-id="50eb0-127">Necessária</span><span class="sxs-lookup"><span data-stu-id="50eb0-127">Required</span></span> | <span data-ttu-id="50eb0-128">Observações</span><span class="sxs-lookup"><span data-stu-id="50eb0-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="50eb0-129">ID</span><span class="sxs-lookup"><span data-stu-id="50eb0-129">ID</span></span>             | <span data-ttu-id="50eb0-130">URL</span><span class="sxs-lookup"><span data-stu-id="50eb0-130">URL</span></span>    | <span data-ttu-id="50eb0-131">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="50eb0-131">string</span></span> | <span data-ttu-id="50eb0-132">sim</span><span class="sxs-lookup"><span data-stu-id="50eb0-132">yes</span></span>      | <span data-ttu-id="50eb0-133">O identidier de pacote para o qual a tecla de escopo de verificação é solicitada</span><span class="sxs-lookup"><span data-stu-id="50eb0-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="50eb0-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="50eb0-134">VERSION</span></span>        | <span data-ttu-id="50eb0-135">URL</span><span class="sxs-lookup"><span data-stu-id="50eb0-135">URL</span></span>    | <span data-ttu-id="50eb0-136">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="50eb0-136">string</span></span> | <span data-ttu-id="50eb0-137">no</span><span class="sxs-lookup"><span data-stu-id="50eb0-137">no</span></span>       | <span data-ttu-id="50eb0-138">A versão do pacote</span><span class="sxs-lookup"><span data-stu-id="50eb0-138">The package version</span></span>
<span data-ttu-id="50eb0-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="50eb0-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="50eb0-140">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="50eb0-140">Header</span></span> | <span data-ttu-id="50eb0-141">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="50eb0-141">string</span></span> | <span data-ttu-id="50eb0-142">sim</span><span class="sxs-lookup"><span data-stu-id="50eb0-142">yes</span></span>      | <span data-ttu-id="50eb0-143">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="50eb0-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="50eb0-144">Resposta</span><span class="sxs-lookup"><span data-stu-id="50eb0-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="50eb0-145">API para verificar se a tecla de escopo de verificação</span><span class="sxs-lookup"><span data-stu-id="50eb0-145">API to verify the verify scope key</span></span>

<span data-ttu-id="50eb0-146">Essa API é usada para validar uma chave de Verifique se o escopo para o pacote de propriedade pelo autor do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="50eb0-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="50eb0-147">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="50eb0-147">Request parameters</span></span>

<span data-ttu-id="50eb0-148">Nome</span><span class="sxs-lookup"><span data-stu-id="50eb0-148">Name</span></span>           | <span data-ttu-id="50eb0-149">No</span><span class="sxs-lookup"><span data-stu-id="50eb0-149">In</span></span>     | <span data-ttu-id="50eb0-150">Tipo</span><span class="sxs-lookup"><span data-stu-id="50eb0-150">Type</span></span>   | <span data-ttu-id="50eb0-151">Necessária</span><span class="sxs-lookup"><span data-stu-id="50eb0-151">Required</span></span> | <span data-ttu-id="50eb0-152">Observações</span><span class="sxs-lookup"><span data-stu-id="50eb0-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="50eb0-153">ID</span><span class="sxs-lookup"><span data-stu-id="50eb0-153">ID</span></span>             | <span data-ttu-id="50eb0-154">URL</span><span class="sxs-lookup"><span data-stu-id="50eb0-154">URL</span></span>    | <span data-ttu-id="50eb0-155">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="50eb0-155">string</span></span> | <span data-ttu-id="50eb0-156">sim</span><span class="sxs-lookup"><span data-stu-id="50eb0-156">yes</span></span>      | <span data-ttu-id="50eb0-157">O identificador de pacote para o qual a tecla de escopo de verificação é solicitada</span><span class="sxs-lookup"><span data-stu-id="50eb0-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="50eb0-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="50eb0-158">VERSION</span></span>        | <span data-ttu-id="50eb0-159">URL</span><span class="sxs-lookup"><span data-stu-id="50eb0-159">URL</span></span>    | <span data-ttu-id="50eb0-160">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="50eb0-160">string</span></span> | <span data-ttu-id="50eb0-161">no</span><span class="sxs-lookup"><span data-stu-id="50eb0-161">no</span></span>       | <span data-ttu-id="50eb0-162">A versão do pacote</span><span class="sxs-lookup"><span data-stu-id="50eb0-162">The package version</span></span>
<span data-ttu-id="50eb0-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="50eb0-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="50eb0-164">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="50eb0-164">Header</span></span> | <span data-ttu-id="50eb0-165">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="50eb0-165">string</span></span> | <span data-ttu-id="50eb0-166">sim</span><span class="sxs-lookup"><span data-stu-id="50eb0-166">yes</span></span>      | <span data-ttu-id="50eb0-167">Por exemplo, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="50eb0-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="50eb0-168">Essa chave de API do escopo de verificar expira em um dia ou na primeira utilização, o que ocorrer primeiro.</span><span class="sxs-lookup"><span data-stu-id="50eb0-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="50eb0-169">Resposta</span><span class="sxs-lookup"><span data-stu-id="50eb0-169">Response</span></span>

<span data-ttu-id="50eb0-170">Código de status</span><span class="sxs-lookup"><span data-stu-id="50eb0-170">Status Code</span></span> | <span data-ttu-id="50eb0-171">Significado</span><span class="sxs-lookup"><span data-stu-id="50eb0-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="50eb0-172">200</span><span class="sxs-lookup"><span data-stu-id="50eb0-172">200</span></span>         | <span data-ttu-id="50eb0-173">A chave de API é válida</span><span class="sxs-lookup"><span data-stu-id="50eb0-173">The API key is valid</span></span>
<span data-ttu-id="50eb0-174">403</span><span class="sxs-lookup"><span data-stu-id="50eb0-174">403</span></span>         | <span data-ttu-id="50eb0-175">A chave de API é inválida ou não autorizado a enviar por push contra o pacote</span><span class="sxs-lookup"><span data-stu-id="50eb0-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="50eb0-176">404</span><span class="sxs-lookup"><span data-stu-id="50eb0-176">404</span></span>         | <span data-ttu-id="50eb0-177">O pacote referenciado pela `ID` e `VERSION` (opcional) não existe</span><span class="sxs-lookup"><span data-stu-id="50eb0-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
