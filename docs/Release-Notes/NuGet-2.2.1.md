---
title: "Notas de versão do NuGet 2.2.1 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão do NuGet 2.2.1 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs."
keywords: "Notas de versão 2.2.1 o NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c3e912dcabeb3a26c880b42560a3cec6f7bf2db9
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="b0ba6-104">Notas de versão do NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="b0ba6-104">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="b0ba6-105">[Notas de versão do NuGet 2.2](../release-notes/nuget-2.2.md) | [notas de versão do NuGet 2.5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="b0ba6-105">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="b0ba6-106">NuGet 2.2.1 foi lançado em 15 de fevereiro de 2013.</span><span class="sxs-lookup"><span data-stu-id="b0ba6-106">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="b0ba6-107">O número de versão da extensão do VS é 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="b0ba6-107">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="b0ba6-108">Atualização de localização</span><span class="sxs-lookup"><span data-stu-id="b0ba6-108">Localization Refresh</span></span>
<span data-ttu-id="b0ba6-109">NuGet é fornecido como parte do Visual Studio 2012, ele foi totalmente localizado em inglês + 13 outros idiomas.</span><span class="sxs-lookup"><span data-stu-id="b0ba6-109">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="b0ba6-110">Desde então, NuGet 2.1 e 2.2 fornecidos, mas a localização não tinha sido atualizada.</span><span class="sxs-lookup"><span data-stu-id="b0ba6-110">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="b0ba6-111">A versão do NuGet 2.2.1 atualiza nossa localização.</span><span class="sxs-lookup"><span data-stu-id="b0ba6-111">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="b0ba6-112">Interface do usuário e o Console do PowerShell do NuGet são localizados em idiomas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0ba6-112">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="b0ba6-113">Chinês (simplificado)</span><span class="sxs-lookup"><span data-stu-id="b0ba6-113">Chinese (Simplified)</span></span>
1. <span data-ttu-id="b0ba6-114">Chinês (tradicional)</span><span class="sxs-lookup"><span data-stu-id="b0ba6-114">Chinese (Traditional)</span></span>
1. <span data-ttu-id="b0ba6-115">Tcheco</span><span class="sxs-lookup"><span data-stu-id="b0ba6-115">Czech</span></span>
1. <span data-ttu-id="b0ba6-116">Inglês</span><span class="sxs-lookup"><span data-stu-id="b0ba6-116">English</span></span>
1. <span data-ttu-id="b0ba6-117">Francês</span><span class="sxs-lookup"><span data-stu-id="b0ba6-117">French</span></span>
1. <span data-ttu-id="b0ba6-118">Alemão</span><span class="sxs-lookup"><span data-stu-id="b0ba6-118">German</span></span>
1. <span data-ttu-id="b0ba6-119">Italiano</span><span class="sxs-lookup"><span data-stu-id="b0ba6-119">Italian</span></span>
1. <span data-ttu-id="b0ba6-120">Japonês</span><span class="sxs-lookup"><span data-stu-id="b0ba6-120">Japanese</span></span>
1. <span data-ttu-id="b0ba6-121">Coreano</span><span class="sxs-lookup"><span data-stu-id="b0ba6-121">Korean</span></span>
1. <span data-ttu-id="b0ba6-122">Polonês</span><span class="sxs-lookup"><span data-stu-id="b0ba6-122">Polish</span></span>
1. <span data-ttu-id="b0ba6-123">Português (Brasil)</span><span class="sxs-lookup"><span data-stu-id="b0ba6-123">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="b0ba6-124">Russo</span><span class="sxs-lookup"><span data-stu-id="b0ba6-124">Russian</span></span>
1. <span data-ttu-id="b0ba6-125">Espanhol</span><span class="sxs-lookup"><span data-stu-id="b0ba6-125">Spanish</span></span>
1. <span data-ttu-id="b0ba6-126">Turco</span><span class="sxs-lookup"><span data-stu-id="b0ba6-126">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="b0ba6-127">Modelos do Visual Studio oferecem suporte a vários repositórios de pacote pré-instalado</span><span class="sxs-lookup"><span data-stu-id="b0ba6-127">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="b0ba6-128">Se você gerar modelos do Visual Studio, você pode usar o NuGet [pré-instalar pacotes](../visual-studio-extensibility/visual-studio-templates.md) como parte do modelo.</span><span class="sxs-lookup"><span data-stu-id="b0ba6-128">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="b0ba6-129">Até agora, esse recurso tinha uma limitação que todos os pacotes necessários para provenientes da mesma origem.</span><span class="sxs-lookup"><span data-stu-id="b0ba6-129">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="b0ba6-130">Com o NuGet 2.2.1 no entanto, você pode ter pacotes instalados vários repositórios (dentro do modelo, um VSIX ou uma pasta no disco definida no registro).</span><span class="sxs-lookup"><span data-stu-id="b0ba6-130">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="b0ba6-131">O cenário principal para esse recurso é personalizados modelos de projeto do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b0ba6-131">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="b0ba6-132">Os modelos internos do ASP.NET usam pacotes pré-instalados, extrair pacotes de disco local.</span><span class="sxs-lookup"><span data-stu-id="b0ba6-132">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="b0ba6-133">Agora você pode criar um modelo de projeto ASP.NET personalizado que usa os pacotes existentes instalados pelo ASP.NET mas adicionar extras pacotes do NuGet em seu modelo.</span><span class="sxs-lookup"><span data-stu-id="b0ba6-133">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="b0ba6-134">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="b0ba6-134">Bug Fixes</span></span>
<span data-ttu-id="b0ba6-135">NuGet 2.2.1 inclui algumas correções de bugs de destino.</span><span class="sxs-lookup"><span data-stu-id="b0ba6-135">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="b0ba6-136">Para obter uma lista de trabalho itens corrigidos no NuGet 2.2.1, por favor, exibir o [NuGet Issue Tracker para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="b0ba6-136">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="b0ba6-137">Problemas Conhecidos</span><span class="sxs-lookup"><span data-stu-id="b0ba6-137">Known Issues</span></span>

<span data-ttu-id="b0ba6-138">Se você estiver estendendo modelos de projeto do ASP.NET, todos os repositórios de pacote pré-instalado devem usar o mesmo valor para o `isPreunzipped` atributo.</span><span class="sxs-lookup"><span data-stu-id="b0ba6-138">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
