---
title: Relatar abuso de modelo de URL, API do NuGet
description: O modelo de URL de abuso de relatório permite que os clientes exibir um link para relatar abuso em sua interface do usuário.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b1fd65b12590a6c5eeb23d946eec6ca4a1c661bc
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020434"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="186ac-103">Modelo de URL de abuso de relatório</span><span class="sxs-lookup"><span data-stu-id="186ac-103">Report abuse URL template</span></span>

<span data-ttu-id="186ac-104">É possível que um cliente para criar uma URL que pode ser usada pelo usuário para relatar abuso sobre um pacote específico.</span><span class="sxs-lookup"><span data-stu-id="186ac-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="186ac-105">Isso é útil quando uma origem de pacote que deseja habilitar todas as experiências de cliente (mesmo 3ª parte) delegar a relatórios de abuso à origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="186ac-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="186ac-106">O recurso usado para criar essa URL é o `ReportAbuseUriTemplate` recurso encontrado na [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="186ac-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="186ac-107">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="186ac-107">Versioning</span></span>

<span data-ttu-id="186ac-108">O seguinte `@type` valores são usados:</span><span class="sxs-lookup"><span data-stu-id="186ac-108">The following `@type` values are used:</span></span>

<span data-ttu-id="186ac-109">Valor @type</span><span class="sxs-lookup"><span data-stu-id="186ac-109">@type value</span></span>                       | <span data-ttu-id="186ac-110">Observações</span><span class="sxs-lookup"><span data-stu-id="186ac-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="186ac-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="186ac-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="186ac-112">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="186ac-112">The initial release</span></span>
<span data-ttu-id="186ac-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="186ac-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="186ac-114">Alias de `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="186ac-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="186ac-115">Modelo de URL</span><span class="sxs-lookup"><span data-stu-id="186ac-115">URL template</span></span>

<span data-ttu-id="186ac-116">A URL para a seguinte API é o valor da `@id` propriedade associada a um do recurso mencionados anteriormente `@type` valores.</span><span class="sxs-lookup"><span data-stu-id="186ac-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="186ac-117">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="186ac-117">HTTP methods</span></span>

<span data-ttu-id="186ac-118">Embora o cliente não se destina para fazer solicitações para a URL para relatar abuso em nome do usuário, a página da web deve oferecer suporte a `GET` método para permitir que uma URL clicada ser aberto facilmente em um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="186ac-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="186ac-119">Construir a URL</span><span class="sxs-lookup"><span data-stu-id="186ac-119">Construct the URL</span></span>

<span data-ttu-id="186ac-120">Dada uma ID do pacote conhecidos e versão, a implementação do cliente pode construir uma URL usada para acessar uma interface da web.</span><span class="sxs-lookup"><span data-stu-id="186ac-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="186ac-121">A implementação do cliente deve exibir esse URL construída (ou um link clicável) para o usuário permitindo que ele abra um navegador da web para a URL e fazer com que qualquer relatório abuso necessárias.</span><span class="sxs-lookup"><span data-stu-id="186ac-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="186ac-122">A implementação do formulário de relatórios de abuso é determinada pela implementação do servidor.</span><span class="sxs-lookup"><span data-stu-id="186ac-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="186ac-123">O valor da `@id` é uma cadeia de caracteres de URL que contém qualquer um dos seguintes tokens de espaço reservado:</span><span class="sxs-lookup"><span data-stu-id="186ac-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="186ac-124">Espaços reservados de URL</span><span class="sxs-lookup"><span data-stu-id="186ac-124">URL placeholders</span></span>

<span data-ttu-id="186ac-125">Nome</span><span class="sxs-lookup"><span data-stu-id="186ac-125">Name</span></span>        | <span data-ttu-id="186ac-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="186ac-126">Type</span></span>    | <span data-ttu-id="186ac-127">Necessária</span><span class="sxs-lookup"><span data-stu-id="186ac-127">Required</span></span> | <span data-ttu-id="186ac-128">Observações</span><span class="sxs-lookup"><span data-stu-id="186ac-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="186ac-129">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="186ac-129">string</span></span>  | <span data-ttu-id="186ac-130">no</span><span class="sxs-lookup"><span data-stu-id="186ac-130">no</span></span>       | <span data-ttu-id="186ac-131">A ID do pacote para relatar abuso de</span><span class="sxs-lookup"><span data-stu-id="186ac-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="186ac-132">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="186ac-132">string</span></span>  | <span data-ttu-id="186ac-133">no</span><span class="sxs-lookup"><span data-stu-id="186ac-133">no</span></span>       | <span data-ttu-id="186ac-134">A versão do pacote para relatar abuso de</span><span class="sxs-lookup"><span data-stu-id="186ac-134">The package version to report abuse for</span></span>

<span data-ttu-id="186ac-135">O `{id}` e `{version}` valores interpretadas pela implementação do servidor devem ser diferencia maiusculas de minúsculas e não é afetado se a versão é normalizada.</span><span class="sxs-lookup"><span data-stu-id="186ac-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="186ac-136">Por exemplo, o modelo de abuso de relatório do nuget.org fica assim:</span><span class="sxs-lookup"><span data-stu-id="186ac-136">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="186ac-137">Se a implementação do cliente precisar exibir um link para o formulário de abuso de relatório para NuGet.Versioning 4.3.0, ele seria produzem a seguinte URL e fornecê-la ao usuário:</span><span class="sxs-lookup"><span data-stu-id="186ac-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
