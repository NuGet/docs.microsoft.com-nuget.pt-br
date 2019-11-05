---
title: Modelo de URL de detalhes do pacote, API do NuGet
description: O modelo de URL de detalhes do pacote permite que os clientes exibam em sua interface do usuário um link da Web para mais detalhes do pacote
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 3102cb9a20f354e92a0da8bba6457dc2ad0f0f2d
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610951"
---
# <a name="package-details-url-template"></a><span data-ttu-id="76176-103">Modelo de URL de detalhes do pacote</span><span class="sxs-lookup"><span data-stu-id="76176-103">Package details URL template</span></span>

<span data-ttu-id="76176-104">É possível que um cliente crie uma URL que possa ser usada pelo usuário para ver mais detalhes do pacote em seu navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="76176-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="76176-105">Isso é útil quando uma origem de pacote deseja mostrar informações adicionais sobre um pacote que talvez não caibam no escopo do que o aplicativo cliente NuGet mostra.</span><span class="sxs-lookup"><span data-stu-id="76176-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="76176-106">O recurso usado para criar essa URL é o `PackageDetailsUriTemplate` recurso encontrado no [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="76176-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="76176-107">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="76176-107">Versioning</span></span>

<span data-ttu-id="76176-108">Os seguintes valores de `@type` são usados:</span><span class="sxs-lookup"><span data-stu-id="76176-108">The following `@type` values are used:</span></span>

<span data-ttu-id="76176-109">Valor @type</span><span class="sxs-lookup"><span data-stu-id="76176-109">@type value</span></span>                     | <span data-ttu-id="76176-110">Anotações</span><span class="sxs-lookup"><span data-stu-id="76176-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="76176-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="76176-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="76176-112">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="76176-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="76176-113">Modelo de URL</span><span class="sxs-lookup"><span data-stu-id="76176-113">URL template</span></span>

<span data-ttu-id="76176-114">A URL para a API a seguir é o valor da propriedade `@id` associada a um dos valores de `@type` de recursos mencionados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="76176-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="76176-115">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="76176-115">HTTP methods</span></span>

<span data-ttu-id="76176-116">Embora o cliente não se destine a fazer solicitações para a URL de detalhes do pacote em nome do usuário, a página da Web deve dar suporte ao método `GET` para permitir que uma URL clicada seja aberta facilmente em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="76176-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="76176-117">Construir a URL</span><span class="sxs-lookup"><span data-stu-id="76176-117">Construct the URL</span></span>

<span data-ttu-id="76176-118">Dada uma ID de pacote e versão conhecidas, a implementação do cliente pode construir uma URL usada para acessar uma interface da Web.</span><span class="sxs-lookup"><span data-stu-id="76176-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="76176-119">A implementação do cliente deve exibir essa URL construída (ou link clicável) para o usuário, permitindo que ele abra um navegador da Web para a URL e saiba mais sobre o pacote.</span><span class="sxs-lookup"><span data-stu-id="76176-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="76176-120">O conteúdo da página de detalhes do pacote é determinado pela implementação do servidor.</span><span class="sxs-lookup"><span data-stu-id="76176-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="76176-121">A URL deve ser uma URL absoluta e o esquema (protocolo) deve ser HTTPS.</span><span class="sxs-lookup"><span data-stu-id="76176-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="76176-122">O valor do `@id` no índice de serviço é uma cadeia de caracteres de URL que contém qualquer um dos seguintes tokens de espaço reservado:</span><span class="sxs-lookup"><span data-stu-id="76176-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="76176-123">Espaços reservados de URL</span><span class="sxs-lookup"><span data-stu-id="76176-123">URL placeholders</span></span>

<span data-ttu-id="76176-124">Name</span><span class="sxs-lookup"><span data-stu-id="76176-124">Name</span></span>        | <span data-ttu-id="76176-125">Digite</span><span class="sxs-lookup"><span data-stu-id="76176-125">Type</span></span>    | <span data-ttu-id="76176-126">Necessária</span><span class="sxs-lookup"><span data-stu-id="76176-126">Required</span></span> | <span data-ttu-id="76176-127">Anotações</span><span class="sxs-lookup"><span data-stu-id="76176-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="76176-128">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="76176-128">string</span></span>  | <span data-ttu-id="76176-129">no</span><span class="sxs-lookup"><span data-stu-id="76176-129">no</span></span>       | <span data-ttu-id="76176-130">A ID do pacote para obter detalhes</span><span class="sxs-lookup"><span data-stu-id="76176-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="76176-131">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="76176-131">string</span></span>  | <span data-ttu-id="76176-132">no</span><span class="sxs-lookup"><span data-stu-id="76176-132">no</span></span>       | <span data-ttu-id="76176-133">A versão do pacote para obter detalhes</span><span class="sxs-lookup"><span data-stu-id="76176-133">The package version to get details for</span></span>

<span data-ttu-id="76176-134">O servidor deve aceitar `{id}` e `{version}` valores com maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="76176-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="76176-135">Além disso, o servidor não deve ser sensível a se a versão é [normalizada](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="76176-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="76176-136">Em outras palavras, o servidor também deve aceitar versões não normalizadas.</span><span class="sxs-lookup"><span data-stu-id="76176-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="76176-137">Por exemplo, o modelo de detalhes do pacote NuGet. org tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="76176-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="76176-138">Se a implementação do cliente precisar exibir um link para os detalhes do pacote para NuGet. Versioning 4.3.0, ele produzirá a seguinte URL e a forneceria ao usuário:</span><span class="sxs-lookup"><span data-stu-id="76176-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
