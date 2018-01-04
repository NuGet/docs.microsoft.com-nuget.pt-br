---
title: Relatar abuso modelo de URL, o NuGet API | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 148d743a-09e5-4539-8454-675be11902db
description: "O modelo de URL do relatório abuso permite que os clientes exibir um link para relatar abuso em sua interface do usuário."
keywords: "Relatar abuso da API do NuGet, reclamação do arquivo NuGet API, o modelo de URL de relatório NuGet.org"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7b3413297f5a7fcf0e2c7757036b1f240ed0058a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="55cb7-104">Modelo de URL do relatório abuso</span><span class="sxs-lookup"><span data-stu-id="55cb7-104">Report Abuse URL Template</span></span>

<span data-ttu-id="55cb7-105">É possível que um cliente para criar uma URL que pode ser usada pelo usuário para relatar abuso sobre um pacote específico.</span><span class="sxs-lookup"><span data-stu-id="55cb7-105">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="55cb7-106">Isso é útil quando uma origem de pacote que deseja habilitar todas as experiências de cliente (mesmo 3ª parte) delegar abuso relatórios para a origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="55cb7-106">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="55cb7-107">O recurso usado para buscar o conteúdo do pacote é o `ReportAbuseUriTemplate` recurso encontrado na [índice de serviço](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="55cb7-107">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="55cb7-108">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="55cb7-108">Versioning</span></span>

<span data-ttu-id="55cb7-109">O seguinte `@type` valores são usados:</span><span class="sxs-lookup"><span data-stu-id="55cb7-109">The following `@type` values are used:</span></span>

<span data-ttu-id="55cb7-110">Valor @type</span><span class="sxs-lookup"><span data-stu-id="55cb7-110">@type value</span></span>                       | <span data-ttu-id="55cb7-111">Observações</span><span class="sxs-lookup"><span data-stu-id="55cb7-111">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="55cb7-112">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="55cb7-112">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="55cb7-113">A versão inicial</span><span class="sxs-lookup"><span data-stu-id="55cb7-113">The initial release</span></span>
<span data-ttu-id="55cb7-114">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="55cb7-114">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="55cb7-115">Alias de`ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="55cb7-115">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="55cb7-116">Modelo de URL</span><span class="sxs-lookup"><span data-stu-id="55cb7-116">URL template</span></span>

<span data-ttu-id="55cb7-117">A URL para a seguinte API é o valor de `@id` propriedade associada a um recurso mencionados acima `@type` valores.</span><span class="sxs-lookup"><span data-stu-id="55cb7-117">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="55cb7-118">Métodos HTTP</span><span class="sxs-lookup"><span data-stu-id="55cb7-118">HTTP methods</span></span>

<span data-ttu-id="55cb7-119">Embora o cliente não se destina para fazer solicitações para a URL do relatório abuso em nome do usuário, a página da web deve oferecer suporte a `GET` método para permitir que uma URL clicada facilmente ser aberto em um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="55cb7-119">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="55cb7-120">Construir a URL</span><span class="sxs-lookup"><span data-stu-id="55cb7-120">Construct the URL</span></span>

<span data-ttu-id="55cb7-121">Devido a uma ID de pacote conhecidos e versão, a implementação do cliente pode construir uma URL usada para acessar uma interface da web.</span><span class="sxs-lookup"><span data-stu-id="55cb7-121">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="55cb7-122">A implementação do cliente deve exibir essa URL construído (ou link clicável) para o usuário é avisado para abrir um navegador da web para a URL e fazer qualquer relatório abuso necessário.</span><span class="sxs-lookup"><span data-stu-id="55cb7-122">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="55cb7-123">A implementação do formulário de relatório abuso é determinada pela implementação do servidor.</span><span class="sxs-lookup"><span data-stu-id="55cb7-123">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="55cb7-124">O valor de `@id` é uma cadeia de caracteres de URL que contém qualquer um dos seguintes tokens de espaço reservado:</span><span class="sxs-lookup"><span data-stu-id="55cb7-124">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="55cb7-125">Espaços reservados de URL</span><span class="sxs-lookup"><span data-stu-id="55cb7-125">URL placeholders</span></span>

<span data-ttu-id="55cb7-126">Nome</span><span class="sxs-lookup"><span data-stu-id="55cb7-126">Name</span></span>        | <span data-ttu-id="55cb7-127">Tipo</span><span class="sxs-lookup"><span data-stu-id="55cb7-127">Type</span></span>    | <span data-ttu-id="55cb7-128">Necessária</span><span class="sxs-lookup"><span data-stu-id="55cb7-128">Required</span></span> | <span data-ttu-id="55cb7-129">Observações</span><span class="sxs-lookup"><span data-stu-id="55cb7-129">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="55cb7-130">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="55cb7-130">string</span></span>  | <span data-ttu-id="55cb7-131">no</span><span class="sxs-lookup"><span data-stu-id="55cb7-131">no</span></span>       | <span data-ttu-id="55cb7-132">A ID do pacote para relatar abuso para</span><span class="sxs-lookup"><span data-stu-id="55cb7-132">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="55cb7-133">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="55cb7-133">string</span></span>  | <span data-ttu-id="55cb7-134">no</span><span class="sxs-lookup"><span data-stu-id="55cb7-134">no</span></span>       | <span data-ttu-id="55cb7-135">A versão do pacote para relatar abuso para</span><span class="sxs-lookup"><span data-stu-id="55cb7-135">The package version to report abuse for</span></span>

<span data-ttu-id="55cb7-136">O `{id}` e `{version}` valores interpretados pela implementação do servidor devem ser o caso que e não é afetado se a versão é normalizada.</span><span class="sxs-lookup"><span data-stu-id="55cb7-136">The `{id}` and `{version}` values interpreted by the server implementation must be case insenstive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="55cb7-137">Por exemplo, o modelo de abuso de relatório do nuget.org tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="55cb7-137">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="55cb7-138">Se a implementação do cliente precisa exibir um link para o formulário de abuso do relatório para NuGet.Versioning 4.3.0, ele seria produzir a URL a seguir e fornecê-la para o usuário:</span><span class="sxs-lookup"><span data-stu-id="55cb7-138">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```