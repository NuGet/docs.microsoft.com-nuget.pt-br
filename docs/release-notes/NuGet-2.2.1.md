---
title: Notas de versão do NuGet 2.2.1
description: Notas de versão do NuGet 2.2.1 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776805"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="1fec5-103">Notas de versão do NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="1fec5-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="1fec5-104">Notas de versão do [NuGet 2,2](../release-notes/nuget-2.2.md)  |  [Notas de versão do NuGet 2,5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="1fec5-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="1fec5-105">O NuGet 2.2.1 foi lançado em 15 de fevereiro de 2013.</span><span class="sxs-lookup"><span data-stu-id="1fec5-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="1fec5-106">O número de versão da extensão VS é 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="1fec5-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="1fec5-107">Atualização de localização</span><span class="sxs-lookup"><span data-stu-id="1fec5-107">Localization Refresh</span></span>
<span data-ttu-id="1fec5-108">Quando o NuGet é fornecido como parte do Visual Studio 2012, ele foi totalmente localizado em inglês + 13 outras linguagens.</span><span class="sxs-lookup"><span data-stu-id="1fec5-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="1fec5-109">Desde então, o NuGet 2,1 e o 2,2 foram enviados, mas a localização não tinha sido atualizada.</span><span class="sxs-lookup"><span data-stu-id="1fec5-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="1fec5-110">A versão 2.2.1 do NuGet atualiza nossa localização.</span><span class="sxs-lookup"><span data-stu-id="1fec5-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="1fec5-111">A interface do usuário do NuGet e o console do PowerShell estão localizados nos seguintes idiomas:</span><span class="sxs-lookup"><span data-stu-id="1fec5-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="1fec5-112">Chinês (Simplificado)</span><span class="sxs-lookup"><span data-stu-id="1fec5-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="1fec5-113">Chinês (Tradicional)</span><span class="sxs-lookup"><span data-stu-id="1fec5-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="1fec5-114">Tcheco</span><span class="sxs-lookup"><span data-stu-id="1fec5-114">Czech</span></span>
1. <span data-ttu-id="1fec5-115">Inglês</span><span class="sxs-lookup"><span data-stu-id="1fec5-115">English</span></span>
1. <span data-ttu-id="1fec5-116">Francês</span><span class="sxs-lookup"><span data-stu-id="1fec5-116">French</span></span>
1. <span data-ttu-id="1fec5-117">Alemão</span><span class="sxs-lookup"><span data-stu-id="1fec5-117">German</span></span>
1. <span data-ttu-id="1fec5-118">Italiano</span><span class="sxs-lookup"><span data-stu-id="1fec5-118">Italian</span></span>
1. <span data-ttu-id="1fec5-119">Japonês</span><span class="sxs-lookup"><span data-stu-id="1fec5-119">Japanese</span></span>
1. <span data-ttu-id="1fec5-120">Coreano</span><span class="sxs-lookup"><span data-stu-id="1fec5-120">Korean</span></span>
1. <span data-ttu-id="1fec5-121">Polonês</span><span class="sxs-lookup"><span data-stu-id="1fec5-121">Polish</span></span>
1. <span data-ttu-id="1fec5-122">Português (Brasil)</span><span class="sxs-lookup"><span data-stu-id="1fec5-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="1fec5-123">Russo</span><span class="sxs-lookup"><span data-stu-id="1fec5-123">Russian</span></span>
1. <span data-ttu-id="1fec5-124">Espanhol</span><span class="sxs-lookup"><span data-stu-id="1fec5-124">Spanish</span></span>
1. <span data-ttu-id="1fec5-125">Turco</span><span class="sxs-lookup"><span data-stu-id="1fec5-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="1fec5-126">Os modelos do Visual Studio dão suporte a vários repositórios de pacotes pré-instalados</span><span class="sxs-lookup"><span data-stu-id="1fec5-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="1fec5-127">Se você produzir modelos do Visual Studio, poderá usar o NuGet para [pré-instalar pacotes](../visual-studio-extensibility/visual-studio-templates.md) como parte do modelo.</span><span class="sxs-lookup"><span data-stu-id="1fec5-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="1fec5-128">Até agora, esse recurso tinha uma limitação de que todos os pacotes precisavam vir da mesma origem.</span><span class="sxs-lookup"><span data-stu-id="1fec5-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="1fec5-129">No entanto, com o NuGet 2.2.1, você pode ter pacotes instalados de vários repositórios (dentro do modelo, um VSIX ou uma pasta no disco definida no registro).</span><span class="sxs-lookup"><span data-stu-id="1fec5-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="1fec5-130">O cenário principal para esse recurso são os modelos de projeto ASP.NET personalizados.</span><span class="sxs-lookup"><span data-stu-id="1fec5-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="1fec5-131">Os modelos internos do ASP.NET usam pacotes pré-instalados, obtendo pacotes do disco local.</span><span class="sxs-lookup"><span data-stu-id="1fec5-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="1fec5-132">Agora você pode criar um modelo de projeto ASP.NET personalizado que usa os pacotes existentes instalados pelo ASP.NET, mas adicionar pacotes NuGet extras ao seu modelo.</span><span class="sxs-lookup"><span data-stu-id="1fec5-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="1fec5-133">Correções de bugs</span><span class="sxs-lookup"><span data-stu-id="1fec5-133">Bug Fixes</span></span>
<span data-ttu-id="1fec5-134">O NuGet 2.2.1 inclui algumas correções de bugs direcionadas.</span><span class="sxs-lookup"><span data-stu-id="1fec5-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="1fec5-135">Para obter uma lista de itens de trabalho corrigidos no NuGet 2.2.1, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="1fec5-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="1fec5-136">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="1fec5-136">Known Issues</span></span>

<span data-ttu-id="1fec5-137">Se você estiver estendendo modelos de projeto ASP.NET, todos os repositórios de pacote pré-instalados deverão usar o mesmo valor para o `isPreunzipped` atributo.</span><span class="sxs-lookup"><span data-stu-id="1fec5-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
