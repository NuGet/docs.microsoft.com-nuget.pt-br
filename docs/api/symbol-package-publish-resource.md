---
title: Enviar por push pacotes de símbolos, API do NuGet | Microsoft Docs
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: O serviço de publicação permite que os clientes publicar novos pacotes de símbolo.
keywords: Pacote de símbolos de envio por push de API do NuGet
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580409"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="e30ab-104">Pacotes de símbolos por push</span><span class="sxs-lookup"><span data-stu-id="e30ab-104">Push Symbol Packages</span></span>

<span data-ttu-id="e30ab-105">É possível aos pacotes de símbolos por push ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) usando a API do NuGet V3.</span><span class="sxs-lookup"><span data-stu-id="e30ab-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="e30ab-106">Essas operações são baseadas fora do `SymbolPackagePublish` recurso encontrado na [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="e30ab-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="e30ab-107">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="e30ab-107">Versioning</span></span>

<span data-ttu-id="e30ab-108">O seguinte `@type` valor é usado:</span><span class="sxs-lookup"><span data-stu-id="e30ab-108">The following `@type` value is used:</span></span>

<span data-ttu-id="e30ab-109">Valor @type</span><span class="sxs-lookup"><span data-stu-id="e30ab-109">@type value</span></span>                 | <span data-ttu-id="e30ab-110">Observações</span><span class="sxs-lookup"><span data-stu-id="e30ab-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="e30ab-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="e30ab-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="e30ab-112">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="e30ab-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="e30ab-113">URL Base</span><span class="sxs-lookup"><span data-stu-id="e30ab-113">Base URL</span></span>

<span data-ttu-id="e30ab-114">A URL base para as APIs a seguir é o valor da `@id` propriedade do `SymbolPackagePublish/4.9.0` recurso na origem do pacote [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="e30ab-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="e30ab-115">Para obter a documentação abaixo, a URL do nuget.org é usado.</span><span class="sxs-lookup"><span data-stu-id="e30ab-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="e30ab-116">Considere `https://www.nuget.org/api/v2/symbolpackage` como um espaço reservado para o `@id` valor encontrado no índice de serviço.</span><span class="sxs-lookup"><span data-stu-id="e30ab-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e30ab-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="e30ab-117">HTTP methods</span></span>

<span data-ttu-id="e30ab-118">O `PUT` método HTTP tem suporte por esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e30ab-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="e30ab-119">Enviar por push a um pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="e30ab-119">Push a symbol package</span></span>

<span data-ttu-id="e30ab-120">NuGet.org dá suporte ao novo formato enviar por push de pacotes de símbolo ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) usando a API a seguir.</span><span class="sxs-lookup"><span data-stu-id="e30ab-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="e30ab-121">Pacotes de símbolo com a mesma ID e versão podem ser enviados várias vezes.</span><span class="sxs-lookup"><span data-stu-id="e30ab-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="e30ab-122">Um pacote de símbolos será rejeitado nos seguintes casos.</span><span class="sxs-lookup"><span data-stu-id="e30ab-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="e30ab-123">Não existe um pacote com o mesmo ID e versão.</span><span class="sxs-lookup"><span data-stu-id="e30ab-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="e30ab-124">Um pacote de símbolos com a mesma ID e versão foi enviado por push, mas ainda não foi publicado.</span><span class="sxs-lookup"><span data-stu-id="e30ab-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="e30ab-125">O pacote de símbolos ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) é inválido (consulte [restrições de pacote de símbolos](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="e30ab-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="e30ab-126">Parâmetros de solicitação</span><span class="sxs-lookup"><span data-stu-id="e30ab-126">Request parameters</span></span>

<span data-ttu-id="e30ab-127">Nome</span><span class="sxs-lookup"><span data-stu-id="e30ab-127">Name</span></span>           | <span data-ttu-id="e30ab-128">No</span><span class="sxs-lookup"><span data-stu-id="e30ab-128">In</span></span>     | <span data-ttu-id="e30ab-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="e30ab-129">Type</span></span>   | <span data-ttu-id="e30ab-130">Necessária</span><span class="sxs-lookup"><span data-stu-id="e30ab-130">Required</span></span> | <span data-ttu-id="e30ab-131">Observações</span><span class="sxs-lookup"><span data-stu-id="e30ab-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="e30ab-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="e30ab-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="e30ab-133">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="e30ab-133">Header</span></span> | <span data-ttu-id="e30ab-134">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e30ab-134">string</span></span> | <span data-ttu-id="e30ab-135">sim</span><span class="sxs-lookup"><span data-stu-id="e30ab-135">yes</span></span>      | <span data-ttu-id="e30ab-136">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="e30ab-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="e30ab-137">A chave de API é uma cadeia de caracteres opaca obtidos de origem do pacote pelo usuário e configurado no cliente.</span><span class="sxs-lookup"><span data-stu-id="e30ab-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="e30ab-138">Nenhum formato de cadeia de caracteres específica é obrigatória, mas o comprimento da chave de API não deve exceder um tamanho razoável para valores de cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="e30ab-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="e30ab-139">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e30ab-139">Request body</span></span>

<span data-ttu-id="e30ab-140">O corpo da solicitação para o envio por push do símbolo é o mesmo que com o corpo de solicitação de uma solicitação de envio do pacote (consulte [de pacote por push e excluir](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="e30ab-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="e30ab-141">Resposta</span><span class="sxs-lookup"><span data-stu-id="e30ab-141">Response</span></span>

<span data-ttu-id="e30ab-142">Código de status</span><span class="sxs-lookup"><span data-stu-id="e30ab-142">Status Code</span></span> | <span data-ttu-id="e30ab-143">Significado</span><span class="sxs-lookup"><span data-stu-id="e30ab-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="e30ab-144">201</span><span class="sxs-lookup"><span data-stu-id="e30ab-144">201</span></span>         | <span data-ttu-id="e30ab-145">O pacote de símbolos foi enviado com êxito.</span><span class="sxs-lookup"><span data-stu-id="e30ab-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="e30ab-146">400</span><span class="sxs-lookup"><span data-stu-id="e30ab-146">400</span></span>         | <span data-ttu-id="e30ab-147">O pacote de símbolos fornecido é inválido.</span><span class="sxs-lookup"><span data-stu-id="e30ab-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="e30ab-148">401</span><span class="sxs-lookup"><span data-stu-id="e30ab-148">401</span></span>         | <span data-ttu-id="e30ab-149">O usuário não está autorizado para executar esta ação.</span><span class="sxs-lookup"><span data-stu-id="e30ab-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="e30ab-150">404</span><span class="sxs-lookup"><span data-stu-id="e30ab-150">404</span></span>         | <span data-ttu-id="e30ab-151">Um pacote correspondente com a ID e a versão fornecida não existe.</span><span class="sxs-lookup"><span data-stu-id="e30ab-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="e30ab-152">409</span><span class="sxs-lookup"><span data-stu-id="e30ab-152">409</span></span>         | <span data-ttu-id="e30ab-153">Um pacote de símbolos com a ID e a versão fornecida foi enviado por push, mas ele ainda não está disponível.</span><span class="sxs-lookup"><span data-stu-id="e30ab-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="e30ab-154">413</span><span class="sxs-lookup"><span data-stu-id="e30ab-154">413</span></span>         | <span data-ttu-id="e30ab-155">O pacote é muito grande.</span><span class="sxs-lookup"><span data-stu-id="e30ab-155">The package is too large.</span></span>

