---
title: Protocolos nuget.org
description: Os protocolos de nuget.org em evolução para interagir com clientes NuGet.
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773978"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="a9a3a-103">Protocolos nuget.org</span><span class="sxs-lookup"><span data-stu-id="a9a3a-103">nuget.org protocols</span></span>

<span data-ttu-id="a9a3a-104">Para interagir com o nuget.org, os clientes precisam seguir determinados protocolos.</span><span class="sxs-lookup"><span data-stu-id="a9a3a-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="a9a3a-105">Como esses protocolos continuam em evolução, os clientes devem identificar a versão do protocolo que usam ao chamar APIs nuget.org específicas.</span><span class="sxs-lookup"><span data-stu-id="a9a3a-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="a9a3a-106">Isso permite que o nuget.org introduza alterações de forma não-significativa para os clientes antigos.</span><span class="sxs-lookup"><span data-stu-id="a9a3a-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="a9a3a-107">As APIs documentadas nesta página são específicas do nuget.org e não há nenhuma expectativa para que outras implementações do servidor NuGet introduzam essas APIs.</span><span class="sxs-lookup"><span data-stu-id="a9a3a-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="a9a3a-108">Para obter informações sobre a API do NuGet implementada amplamente no ecossistema do NuGet, consulte a [visão geral da API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="a9a3a-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="a9a3a-109">Este tópico lista vários protocolos como e quando eles chegam à existência.</span><span class="sxs-lookup"><span data-stu-id="a9a3a-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="a9a3a-110">Versão do protocolo NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="a9a3a-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="a9a3a-111">O protocolo 4.1.0 especifica o uso de chaves de escopo de verificação para interagir com serviços diferentes de nuget.org, para validar um pacote em uma conta nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a9a3a-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="a9a3a-112">Observe que o `4.1.0` número de versão é uma cadeia de caracteres opaca, mas que ocorre coincidir com a primeira versão do cliente do NuGet oficial que tem suporte para esse protocolo.</span><span class="sxs-lookup"><span data-stu-id="a9a3a-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="a9a3a-113">A validação garante que as chaves de API criadas pelo usuário sejam usadas somente com nuget.org, e que outra verificação ou validação de um serviço de terceiros seja manipulada por meio de uma única utilização de chaves de escopo de verificação.</span><span class="sxs-lookup"><span data-stu-id="a9a3a-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="a9a3a-114">Essas chaves de escopo de verificação podem ser usadas para validar que o pacote pertence a um usuário específico (conta) em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a9a3a-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="a9a3a-115">Requisito do cliente</span><span class="sxs-lookup"><span data-stu-id="a9a3a-115">Client requirement</span></span>

<span data-ttu-id="a9a3a-116">Os clientes são obrigados a passar o seguinte cabeçalho quando fazem chamadas à API para **enviar pacotes por push** para NuGet.org:</span><span class="sxs-lookup"><span data-stu-id="a9a3a-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="a9a3a-117">Observe que o `X-NuGet-Client-Version` cabeçalho tem semântica semelhante, mas é reservado para ser usado apenas pelo cliente oficial do NuGet.</span><span class="sxs-lookup"><span data-stu-id="a9a3a-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="a9a3a-118">Clientes de terceiros devem usar o `X-NuGet-Protocol-Version` cabeçalho e o valor.</span><span class="sxs-lookup"><span data-stu-id="a9a3a-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="a9a3a-119">O próprio protocolo de **Push** é descrito na documentação do [ `PackagePublish` recurso](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="a9a3a-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="a9a3a-120">Se um cliente interage com serviços externos e precisa validar se um pacote pertence a um usuário específico (conta), ele deve usar o seguinte protocolo e usar as chaves de escopo de verificação e não as chaves de API de nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a9a3a-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="a9a3a-121">API para solicitar uma chave de verificação de escopo</span><span class="sxs-lookup"><span data-stu-id="a9a3a-121">API to request a verify-scope key</span></span>

<span data-ttu-id="a9a3a-122">Essa API é usada para obter uma chave de escopo de verificação para um autor de nuget.org para validar um pacote de propriedade dele.</span><span class="sxs-lookup"><span data-stu-id="a9a3a-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="a9a3a-123">Parâmetros da solicitação</span><span class="sxs-lookup"><span data-stu-id="a9a3a-123">Request parameters</span></span>

<span data-ttu-id="a9a3a-124">Nome</span><span class="sxs-lookup"><span data-stu-id="a9a3a-124">Name</span></span>           | <span data-ttu-id="a9a3a-125">Em</span><span class="sxs-lookup"><span data-stu-id="a9a3a-125">In</span></span>     | <span data-ttu-id="a9a3a-126">Type</span><span class="sxs-lookup"><span data-stu-id="a9a3a-126">Type</span></span>   | <span data-ttu-id="a9a3a-127">Necessária</span><span class="sxs-lookup"><span data-stu-id="a9a3a-127">Required</span></span> | <span data-ttu-id="a9a3a-128">Observações</span><span class="sxs-lookup"><span data-stu-id="a9a3a-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="a9a3a-129">ID</span><span class="sxs-lookup"><span data-stu-id="a9a3a-129">ID</span></span>             | <span data-ttu-id="a9a3a-130">URL</span><span class="sxs-lookup"><span data-stu-id="a9a3a-130">URL</span></span>    | <span data-ttu-id="a9a3a-131">string</span><span class="sxs-lookup"><span data-stu-id="a9a3a-131">string</span></span> | <span data-ttu-id="a9a3a-132">sim</span><span class="sxs-lookup"><span data-stu-id="a9a3a-132">yes</span></span>      | <span data-ttu-id="a9a3a-133">O pacote identidier para o qual a chave de verificação de escopo é solicitada</span><span class="sxs-lookup"><span data-stu-id="a9a3a-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="a9a3a-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="a9a3a-134">VERSION</span></span>        | <span data-ttu-id="a9a3a-135">URL</span><span class="sxs-lookup"><span data-stu-id="a9a3a-135">URL</span></span>    | <span data-ttu-id="a9a3a-136">string</span><span class="sxs-lookup"><span data-stu-id="a9a3a-136">string</span></span> | <span data-ttu-id="a9a3a-137">não</span><span class="sxs-lookup"><span data-stu-id="a9a3a-137">no</span></span>       | <span data-ttu-id="a9a3a-138">A versão do pacote</span><span class="sxs-lookup"><span data-stu-id="a9a3a-138">The package version</span></span>
<span data-ttu-id="a9a3a-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="a9a3a-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="a9a3a-140">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="a9a3a-140">Header</span></span> | <span data-ttu-id="a9a3a-141">string</span><span class="sxs-lookup"><span data-stu-id="a9a3a-141">string</span></span> | <span data-ttu-id="a9a3a-142">sim</span><span class="sxs-lookup"><span data-stu-id="a9a3a-142">yes</span></span>      | <span data-ttu-id="a9a3a-143">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="a9a3a-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="a9a3a-144">Resposta</span><span class="sxs-lookup"><span data-stu-id="a9a3a-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="a9a3a-145">API para verificar a chave de verificação de escopo</span><span class="sxs-lookup"><span data-stu-id="a9a3a-145">API to verify the verify scope key</span></span>

<span data-ttu-id="a9a3a-146">Essa API é usada para validar uma chave de escopo de verificação para o pacote de Propriedade do autor do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a9a3a-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="a9a3a-147">Parâmetros da solicitação</span><span class="sxs-lookup"><span data-stu-id="a9a3a-147">Request parameters</span></span>

<span data-ttu-id="a9a3a-148">Nome</span><span class="sxs-lookup"><span data-stu-id="a9a3a-148">Name</span></span>           | <span data-ttu-id="a9a3a-149">Em</span><span class="sxs-lookup"><span data-stu-id="a9a3a-149">In</span></span>     | <span data-ttu-id="a9a3a-150">Type</span><span class="sxs-lookup"><span data-stu-id="a9a3a-150">Type</span></span>   | <span data-ttu-id="a9a3a-151">Necessária</span><span class="sxs-lookup"><span data-stu-id="a9a3a-151">Required</span></span> | <span data-ttu-id="a9a3a-152">Observações</span><span class="sxs-lookup"><span data-stu-id="a9a3a-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="a9a3a-153">ID</span><span class="sxs-lookup"><span data-stu-id="a9a3a-153">ID</span></span>             | <span data-ttu-id="a9a3a-154">URL</span><span class="sxs-lookup"><span data-stu-id="a9a3a-154">URL</span></span>    | <span data-ttu-id="a9a3a-155">string</span><span class="sxs-lookup"><span data-stu-id="a9a3a-155">string</span></span> | <span data-ttu-id="a9a3a-156">sim</span><span class="sxs-lookup"><span data-stu-id="a9a3a-156">yes</span></span>      | <span data-ttu-id="a9a3a-157">O identificador de pacote para o qual a chave de verificação de escopo é solicitada</span><span class="sxs-lookup"><span data-stu-id="a9a3a-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="a9a3a-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="a9a3a-158">VERSION</span></span>        | <span data-ttu-id="a9a3a-159">URL</span><span class="sxs-lookup"><span data-stu-id="a9a3a-159">URL</span></span>    | <span data-ttu-id="a9a3a-160">string</span><span class="sxs-lookup"><span data-stu-id="a9a3a-160">string</span></span> | <span data-ttu-id="a9a3a-161">não</span><span class="sxs-lookup"><span data-stu-id="a9a3a-161">no</span></span>       | <span data-ttu-id="a9a3a-162">A versão do pacote</span><span class="sxs-lookup"><span data-stu-id="a9a3a-162">The package version</span></span>
<span data-ttu-id="a9a3a-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="a9a3a-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="a9a3a-164">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="a9a3a-164">Header</span></span> | <span data-ttu-id="a9a3a-165">string</span><span class="sxs-lookup"><span data-stu-id="a9a3a-165">string</span></span> | <span data-ttu-id="a9a3a-166">sim</span><span class="sxs-lookup"><span data-stu-id="a9a3a-166">yes</span></span>      | <span data-ttu-id="a9a3a-167">Por exemplo, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="a9a3a-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="a9a3a-168">Essa chave verificar API de escopo expira no horário de um dia ou no primeiro uso, o que ocorrer primeiro.</span><span class="sxs-lookup"><span data-stu-id="a9a3a-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="a9a3a-169">Resposta</span><span class="sxs-lookup"><span data-stu-id="a9a3a-169">Response</span></span>

<span data-ttu-id="a9a3a-170">Código de status</span><span class="sxs-lookup"><span data-stu-id="a9a3a-170">Status Code</span></span> | <span data-ttu-id="a9a3a-171">Significado</span><span class="sxs-lookup"><span data-stu-id="a9a3a-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="a9a3a-172">200</span><span class="sxs-lookup"><span data-stu-id="a9a3a-172">200</span></span>         | <span data-ttu-id="a9a3a-173">A chave de API é válida</span><span class="sxs-lookup"><span data-stu-id="a9a3a-173">The API key is valid</span></span>
<span data-ttu-id="a9a3a-174">403</span><span class="sxs-lookup"><span data-stu-id="a9a3a-174">403</span></span>         | <span data-ttu-id="a9a3a-175">A chave de API é inválida ou não está autorizada a enviar por push para o pacote</span><span class="sxs-lookup"><span data-stu-id="a9a3a-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="a9a3a-176">404</span><span class="sxs-lookup"><span data-stu-id="a9a3a-176">404</span></span>         | <span data-ttu-id="a9a3a-177">O pacote referido por `ID` e `VERSION` (opcional) não existe</span><span class="sxs-lookup"><span data-stu-id="a9a3a-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
