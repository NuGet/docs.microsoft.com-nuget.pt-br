---
title: Modelo de URL de detalhes do pacote, API do NuGet
description: O modelo de URL de detalhes do pacote permite que os clientes exibir em sua interface do usuário que um link da web para obter mais detalhes do pacote
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638066"
---
# <a name="package-details-url-template"></a><span data-ttu-id="c33ae-103">Modelo de URL de detalhes do pacote</span><span class="sxs-lookup"><span data-stu-id="c33ae-103">Package details URL template</span></span>

<span data-ttu-id="c33ae-104">É possível que um cliente para criar uma URL que pode ser usada pelo usuário para ver mais detalhes do pacote em seu navegador da web.</span><span class="sxs-lookup"><span data-stu-id="c33ae-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="c33ae-105">Isso é útil quando uma origem de pacote que deseja mostrar informações adicionais sobre um pacote que não se encaixam dentro do escopo do que mostra o aplicativo de cliente do NuGet.</span><span class="sxs-lookup"><span data-stu-id="c33ae-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="c33ae-106">O recurso usado para criar essa URL é o `PackageDetailsUriTemplate` recurso encontrado na [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="c33ae-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="c33ae-107">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="c33ae-107">Versioning</span></span>

<span data-ttu-id="c33ae-108">O seguinte `@type` valores são usados:</span><span class="sxs-lookup"><span data-stu-id="c33ae-108">The following `@type` values are used:</span></span>

<span data-ttu-id="c33ae-109">Valor @type</span><span class="sxs-lookup"><span data-stu-id="c33ae-109">@type value</span></span>                     | <span data-ttu-id="c33ae-110">Observações</span><span class="sxs-lookup"><span data-stu-id="c33ae-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="c33ae-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="c33ae-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="c33ae-112">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="c33ae-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="c33ae-113">Modelo de URL</span><span class="sxs-lookup"><span data-stu-id="c33ae-113">URL template</span></span>

<span data-ttu-id="c33ae-114">A URL para a seguinte API é o valor da `@id` propriedade associada a um do recurso mencionados anteriormente `@type` valores.</span><span class="sxs-lookup"><span data-stu-id="c33ae-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="c33ae-115">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="c33ae-115">HTTP methods</span></span>

<span data-ttu-id="c33ae-116">Embora o cliente não se destina para fazer solicitações para a URL de detalhes do pacote em nome do usuário, a página da web deve oferecer suporte a `GET` método para permitir que uma URL clicada ser aberto facilmente em um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="c33ae-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="c33ae-117">Construir a URL</span><span class="sxs-lookup"><span data-stu-id="c33ae-117">Construct the URL</span></span>

<span data-ttu-id="c33ae-118">Dada uma ID do pacote conhecidos e versão, a implementação do cliente pode construir uma URL usada para acessar uma interface da web.</span><span class="sxs-lookup"><span data-stu-id="c33ae-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="c33ae-119">A implementação do cliente deve exibir esse URL construída (ou um link clicável) para o usuário, permitindo que eles para abrir um navegador da web para a URL e para saber mais sobre o pacote.</span><span class="sxs-lookup"><span data-stu-id="c33ae-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="c33ae-120">O conteúdo da página de detalhes do pacote é determinado pela implementação do servidor.</span><span class="sxs-lookup"><span data-stu-id="c33ae-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="c33ae-121">A URL deve ser uma URL absoluta e o esquema (protocol) deve ser HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c33ae-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="c33ae-122">O valor da `@id` no serviço de índice é uma cadeia de caracteres de URL que contém qualquer um dos seguintes tokens de espaço reservado:</span><span class="sxs-lookup"><span data-stu-id="c33ae-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="c33ae-123">Espaços reservados de URL</span><span class="sxs-lookup"><span data-stu-id="c33ae-123">URL placeholders</span></span>

<span data-ttu-id="c33ae-124">Nome</span><span class="sxs-lookup"><span data-stu-id="c33ae-124">Name</span></span>        | <span data-ttu-id="c33ae-125">Tipo</span><span class="sxs-lookup"><span data-stu-id="c33ae-125">Type</span></span>    | <span data-ttu-id="c33ae-126">Necessária</span><span class="sxs-lookup"><span data-stu-id="c33ae-126">Required</span></span> | <span data-ttu-id="c33ae-127">Observações</span><span class="sxs-lookup"><span data-stu-id="c33ae-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="c33ae-128">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="c33ae-128">string</span></span>  | <span data-ttu-id="c33ae-129">no</span><span class="sxs-lookup"><span data-stu-id="c33ae-129">no</span></span>       | <span data-ttu-id="c33ae-130">Para obter detalhes para a ID do pacote</span><span class="sxs-lookup"><span data-stu-id="c33ae-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="c33ae-131">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="c33ae-131">string</span></span>  | <span data-ttu-id="c33ae-132">no</span><span class="sxs-lookup"><span data-stu-id="c33ae-132">no</span></span>       | <span data-ttu-id="c33ae-133">Para obter detalhes para a versão do pacote</span><span class="sxs-lookup"><span data-stu-id="c33ae-133">The package version to get details for</span></span>

<span data-ttu-id="c33ae-134">O servidor deve aceitar `{id}` e `{version}` valores com qualquer uso de maiusculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c33ae-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="c33ae-135">Além disso, o servidor não deve ser sensível a se a versão está [normalizado](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="c33ae-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="c33ae-136">Em outras palavras, o servidor deve aceitar também aceitam versões não normalizado.</span><span class="sxs-lookup"><span data-stu-id="c33ae-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="c33ae-137">Por exemplo, o modelo de detalhes do pacote do nuget.org fica assim:</span><span class="sxs-lookup"><span data-stu-id="c33ae-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="c33ae-138">Se a implementação do cliente precisar exibir um link para os detalhes do pacote para NuGet.Versioning 4.3.0, ele seria produzem a seguinte URL e fornecê-la ao usuário:</span><span class="sxs-lookup"><span data-stu-id="c33ae-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
