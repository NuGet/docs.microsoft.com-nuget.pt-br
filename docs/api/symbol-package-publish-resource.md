---
title: Pacotes de símbolo de push, API do NuGet | Microsoft Docs
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: O serviço de publicação permite que os clientes publiquem novos pacotes de símbolo.
keywords: Pacote de símbolos de push da API do NuGet
ms.reviewer: karann
ms.openlocfilehash: bd4a10cc976c9d0775a63cfe61c35327c196065c
ms.sourcegitcommit: e39e5a5ddf68bf41e816617e7f0339308523bbb3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96738871"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="097a1-104">Pacotes de símbolo de push</span><span class="sxs-lookup"><span data-stu-id="097a1-104">Push Symbol Packages</span></span>

<span data-ttu-id="097a1-105">É possível enviar por push os pacotes de símbolos ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) usando a API do NuGet v3.</span><span class="sxs-lookup"><span data-stu-id="097a1-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="097a1-106">Essas operações são baseadas no `SymbolPackagePublish` recurso encontrado no [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="097a1-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="097a1-107">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="097a1-107">Versioning</span></span>

<span data-ttu-id="097a1-108">O seguinte `@type` valor é usado:</span><span class="sxs-lookup"><span data-stu-id="097a1-108">The following `@type` value is used:</span></span>

<span data-ttu-id="097a1-109">@type valor</span><span class="sxs-lookup"><span data-stu-id="097a1-109">@type value</span></span>                 | <span data-ttu-id="097a1-110">Observações</span><span class="sxs-lookup"><span data-stu-id="097a1-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="097a1-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="097a1-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="097a1-112">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="097a1-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="097a1-113">URL base</span><span class="sxs-lookup"><span data-stu-id="097a1-113">Base URL</span></span>

<span data-ttu-id="097a1-114">A URL base para as APIs a seguir é o valor da `@id` Propriedade do `SymbolPackagePublish/4.9.0` recurso no [índice de serviço](service-index.md)da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="097a1-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="097a1-115">Para a documentação abaixo, a URL do NuGet. org é usada.</span><span class="sxs-lookup"><span data-stu-id="097a1-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="097a1-116">Considere `https://www.nuget.org/api/v2/symbolpackage` como um espaço reservado para o `@id` valor encontrado no índice de serviço.</span><span class="sxs-lookup"><span data-stu-id="097a1-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="097a1-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="097a1-117">HTTP methods</span></span>

<span data-ttu-id="097a1-118">`PUT`Este recurso dá suporte ao método http.</span><span class="sxs-lookup"><span data-stu-id="097a1-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="097a1-119">Enviar por push um pacote de símbolos</span><span class="sxs-lookup"><span data-stu-id="097a1-119">Push a symbol package</span></span>

<span data-ttu-id="097a1-120">o nuget.org dá suporte ao envio de novo formato de pacotes de símbolo ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) usando a API a seguir.</span><span class="sxs-lookup"><span data-stu-id="097a1-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="097a1-121">Pacotes de símbolos com a mesma ID e versão podem ser enviados várias vezes.</span><span class="sxs-lookup"><span data-stu-id="097a1-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="097a1-122">Um pacote de símbolos será rejeitado nos casos a seguir.</span><span class="sxs-lookup"><span data-stu-id="097a1-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="097a1-123">Não existe um pacote com a mesma ID e versão.</span><span class="sxs-lookup"><span data-stu-id="097a1-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="097a1-124">Um pacote de símbolos com a mesma ID e versão foi enviado por push, mas ainda não foi publicado.</span><span class="sxs-lookup"><span data-stu-id="097a1-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="097a1-125">O pacote de símbolos ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) é inválido (consulte [restrições de pacote de símbolo](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="097a1-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="097a1-126">Parâmetros da solicitação</span><span class="sxs-lookup"><span data-stu-id="097a1-126">Request parameters</span></span>

<span data-ttu-id="097a1-127">Nome</span><span class="sxs-lookup"><span data-stu-id="097a1-127">Name</span></span>           | <span data-ttu-id="097a1-128">Em</span><span class="sxs-lookup"><span data-stu-id="097a1-128">In</span></span>     | <span data-ttu-id="097a1-129">Type</span><span class="sxs-lookup"><span data-stu-id="097a1-129">Type</span></span>   | <span data-ttu-id="097a1-130">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="097a1-130">Required</span></span> | <span data-ttu-id="097a1-131">Observações</span><span class="sxs-lookup"><span data-stu-id="097a1-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="097a1-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="097a1-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="097a1-133">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="097a1-133">Header</span></span> | <span data-ttu-id="097a1-134">string</span><span class="sxs-lookup"><span data-stu-id="097a1-134">string</span></span> | <span data-ttu-id="097a1-135">sim</span><span class="sxs-lookup"><span data-stu-id="097a1-135">yes</span></span>      | <span data-ttu-id="097a1-136">Por exemplo, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="097a1-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="097a1-137">A chave de API é uma cadeia de caracteres opaca proveniente da origem do pacote pelo usuário e configurada no cliente.</span><span class="sxs-lookup"><span data-stu-id="097a1-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="097a1-138">Nenhum formato de cadeia de caracteres específico é obrigatório, mas o comprimento da chave de API não deve exceder um tamanho razoável para valores de cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="097a1-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="097a1-139">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="097a1-139">Request body</span></span>

<span data-ttu-id="097a1-140">O corpo da solicitação para o símbolo Push é o mesmo que com o corpo da solicitação de uma solicitação de push de pacote (consulte [push e Delete do pacote](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="097a1-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="097a1-141">Resposta</span><span class="sxs-lookup"><span data-stu-id="097a1-141">Response</span></span>

<span data-ttu-id="097a1-142">Código de status</span><span class="sxs-lookup"><span data-stu-id="097a1-142">Status Code</span></span> | <span data-ttu-id="097a1-143">Significado</span><span class="sxs-lookup"><span data-stu-id="097a1-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="097a1-144">201</span><span class="sxs-lookup"><span data-stu-id="097a1-144">201</span></span>         | <span data-ttu-id="097a1-145">O pacote de símbolos foi enviado por push com êxito.</span><span class="sxs-lookup"><span data-stu-id="097a1-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="097a1-146">400</span><span class="sxs-lookup"><span data-stu-id="097a1-146">400</span></span>         | <span data-ttu-id="097a1-147">O pacote de símbolos fornecido é inválido.</span><span class="sxs-lookup"><span data-stu-id="097a1-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="097a1-148">401</span><span class="sxs-lookup"><span data-stu-id="097a1-148">401</span></span>         | <span data-ttu-id="097a1-149">O usuário não está autorizado a executar esta ação.</span><span class="sxs-lookup"><span data-stu-id="097a1-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="097a1-150">404</span><span class="sxs-lookup"><span data-stu-id="097a1-150">404</span></span>         | <span data-ttu-id="097a1-151">Não existe um pacote correspondente com a ID e a versão fornecidas.</span><span class="sxs-lookup"><span data-stu-id="097a1-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="097a1-152">409</span><span class="sxs-lookup"><span data-stu-id="097a1-152">409</span></span>         | <span data-ttu-id="097a1-153">Um pacote de símbolos com a ID e a versão fornecidas foi enviado por push, mas ainda não está disponível.</span><span class="sxs-lookup"><span data-stu-id="097a1-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="097a1-154">413</span><span class="sxs-lookup"><span data-stu-id="097a1-154">413</span></span>         | <span data-ttu-id="097a1-155">O pacote é muito grande.</span><span class="sxs-lookup"><span data-stu-id="097a1-155">The package is too large.</span></span>

