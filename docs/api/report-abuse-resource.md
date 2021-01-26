---
title: Relatar o modelo de URL de abuso, API do NuGet
description: O modelo de URL do relatório de abuso permite que os clientes exibam um link de abuso de relatório em sua interface do usuário.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775232"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="02fa4-103">Relatar o modelo de URL de abuso</span><span class="sxs-lookup"><span data-stu-id="02fa4-103">Report abuse URL template</span></span>

<span data-ttu-id="02fa4-104">É possível que um cliente crie uma URL que possa ser usada pelo usuário para relatar abusos sobre um pacote específico.</span><span class="sxs-lookup"><span data-stu-id="02fa4-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="02fa4-105">Isso é útil quando uma origem de pacote deseja habilitar todas as experiências do cliente (mesmo de terceiros) para delegar relatórios de abuso à origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="02fa4-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="02fa4-106">O recurso usado para criar essa URL é o `ReportAbuseUriTemplate` recurso encontrado no [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="02fa4-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="02fa4-107">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="02fa4-107">Versioning</span></span>

<span data-ttu-id="02fa4-108">Os seguintes `@type` valores são usados:</span><span class="sxs-lookup"><span data-stu-id="02fa4-108">The following `@type` values are used:</span></span>

<span data-ttu-id="02fa4-109">@type valor</span><span class="sxs-lookup"><span data-stu-id="02fa4-109">@type value</span></span>                       | <span data-ttu-id="02fa4-110">Observações</span><span class="sxs-lookup"><span data-stu-id="02fa4-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="02fa4-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="02fa4-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="02fa4-112">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="02fa4-112">The initial release</span></span>
<span data-ttu-id="02fa4-113">ReportAbuseUriTemplate/3.0.0-RC</span><span class="sxs-lookup"><span data-stu-id="02fa4-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="02fa4-114">Alias de `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="02fa4-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="02fa4-115">Modelo do URL</span><span class="sxs-lookup"><span data-stu-id="02fa4-115">URL template</span></span>

<span data-ttu-id="02fa4-116">A URL para a API a seguir é o valor da `@id` propriedade associada a um dos valores de recurso mencionados anteriormente `@type` .</span><span class="sxs-lookup"><span data-stu-id="02fa4-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="02fa4-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="02fa4-117">HTTP methods</span></span>

<span data-ttu-id="02fa4-118">Embora o cliente não se destine a fazer solicitações para a URL de abuso de relatório em nome do usuário, a página da Web deve dar suporte ao `GET` método para permitir que uma URL clicada seja aberta facilmente em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="02fa4-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="02fa4-119">Construir a URL</span><span class="sxs-lookup"><span data-stu-id="02fa4-119">Construct the URL</span></span>

<span data-ttu-id="02fa4-120">Dada uma ID de pacote e versão conhecidas, a implementação do cliente pode construir uma URL usada para acessar uma interface da Web.</span><span class="sxs-lookup"><span data-stu-id="02fa4-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="02fa4-121">A implementação do cliente deve exibir essa URL construída (ou link clicável) para o usuário, permitindo que ele abra um navegador da Web para a URL e faça qualquer relatório de abuso necessário.</span><span class="sxs-lookup"><span data-stu-id="02fa4-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="02fa4-122">A implementação do formulário de relatório de abuso é determinada pela implementação do servidor.</span><span class="sxs-lookup"><span data-stu-id="02fa4-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="02fa4-123">O valor de `@id` é uma cadeia de caracteres de URL que contém qualquer um dos seguintes tokens de espaço reservado:</span><span class="sxs-lookup"><span data-stu-id="02fa4-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="02fa4-124">Espaços reservados de URL</span><span class="sxs-lookup"><span data-stu-id="02fa4-124">URL placeholders</span></span>

<span data-ttu-id="02fa4-125">Nome</span><span class="sxs-lookup"><span data-stu-id="02fa4-125">Name</span></span>        | <span data-ttu-id="02fa4-126">Type</span><span class="sxs-lookup"><span data-stu-id="02fa4-126">Type</span></span>    | <span data-ttu-id="02fa4-127">Necessária</span><span class="sxs-lookup"><span data-stu-id="02fa4-127">Required</span></span> | <span data-ttu-id="02fa4-128">Observações</span><span class="sxs-lookup"><span data-stu-id="02fa4-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="02fa4-129">string</span><span class="sxs-lookup"><span data-stu-id="02fa4-129">string</span></span>  | <span data-ttu-id="02fa4-130">não</span><span class="sxs-lookup"><span data-stu-id="02fa4-130">no</span></span>       | <span data-ttu-id="02fa4-131">A ID do pacote para relatar abuso</span><span class="sxs-lookup"><span data-stu-id="02fa4-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="02fa4-132">string</span><span class="sxs-lookup"><span data-stu-id="02fa4-132">string</span></span>  | <span data-ttu-id="02fa4-133">não</span><span class="sxs-lookup"><span data-stu-id="02fa4-133">no</span></span>       | <span data-ttu-id="02fa4-134">A versão do pacote para relatar abuso</span><span class="sxs-lookup"><span data-stu-id="02fa4-134">The package version to report abuse for</span></span>

<span data-ttu-id="02fa4-135">Os `{id}` `{version}` valores e interpretados pela implementação do servidor devem diferenciar maiúsculas de minúsculas e não diferenciar se a versão for normalizada.</span><span class="sxs-lookup"><span data-stu-id="02fa4-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="02fa4-136">Por exemplo, o modelo de abuso de relatório do NuGet. org tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="02fa4-136">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="02fa4-137">Se a implementação do cliente precisar exibir um link para o formulário relatar abuso para NuGet. Versioning 4.3.0, ele produzirá a seguinte URL e a forneceria ao usuário:</span><span class="sxs-lookup"><span data-stu-id="02fa4-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
