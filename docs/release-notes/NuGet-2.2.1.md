---
title: Notas de versão do NuGet 2.2.1
description: Notas de versão do NuGet 2.2.1 incluindo conhecidos problemas, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550692"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="49c6b-103">Notas de versão do NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="49c6b-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="49c6b-104">[Notas de versão do NuGet 2.2](../release-notes/nuget-2.2.md) | [notas de versão do NuGet 2.5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="49c6b-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="49c6b-105">O NuGet 2.2.1 foi lançado em 15 de fevereiro de 2013.</span><span class="sxs-lookup"><span data-stu-id="49c6b-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="49c6b-106">O número de versão da extensão do VS é 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="49c6b-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="49c6b-107">Atualização de localização</span><span class="sxs-lookup"><span data-stu-id="49c6b-107">Localization Refresh</span></span>
<span data-ttu-id="49c6b-108">Quando o NuGet é fornecida como parte do Visual Studio 2012, ele foi totalmente localizado em inglês + 13 outros idiomas.</span><span class="sxs-lookup"><span data-stu-id="49c6b-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="49c6b-109">Desde então, ter enviado o NuGet 2.1 e 2.2, mas a localização não tinha sido atualizada.</span><span class="sxs-lookup"><span data-stu-id="49c6b-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="49c6b-110">A versão do NuGet 2.2.1 atualiza nossa localização.</span><span class="sxs-lookup"><span data-stu-id="49c6b-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="49c6b-111">Interface do usuário do NuGet e o Console do PowerShell são localizados para os seguintes idiomas:</span><span class="sxs-lookup"><span data-stu-id="49c6b-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="49c6b-112">Chinês (simplificado)</span><span class="sxs-lookup"><span data-stu-id="49c6b-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="49c6b-113">Chinês (tradicional)</span><span class="sxs-lookup"><span data-stu-id="49c6b-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="49c6b-114">Tcheco</span><span class="sxs-lookup"><span data-stu-id="49c6b-114">Czech</span></span>
1. <span data-ttu-id="49c6b-115">Inglês</span><span class="sxs-lookup"><span data-stu-id="49c6b-115">English</span></span>
1. <span data-ttu-id="49c6b-116">Francês</span><span class="sxs-lookup"><span data-stu-id="49c6b-116">French</span></span>
1. <span data-ttu-id="49c6b-117">Alemão</span><span class="sxs-lookup"><span data-stu-id="49c6b-117">German</span></span>
1. <span data-ttu-id="49c6b-118">Italiano</span><span class="sxs-lookup"><span data-stu-id="49c6b-118">Italian</span></span>
1. <span data-ttu-id="49c6b-119">Japonês</span><span class="sxs-lookup"><span data-stu-id="49c6b-119">Japanese</span></span>
1. <span data-ttu-id="49c6b-120">Coreano</span><span class="sxs-lookup"><span data-stu-id="49c6b-120">Korean</span></span>
1. <span data-ttu-id="49c6b-121">Polonês</span><span class="sxs-lookup"><span data-stu-id="49c6b-121">Polish</span></span>
1. <span data-ttu-id="49c6b-122">Português (Brasil)</span><span class="sxs-lookup"><span data-stu-id="49c6b-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="49c6b-123">Russo</span><span class="sxs-lookup"><span data-stu-id="49c6b-123">Russian</span></span>
1. <span data-ttu-id="49c6b-124">Espanhol</span><span class="sxs-lookup"><span data-stu-id="49c6b-124">Spanish</span></span>
1. <span data-ttu-id="49c6b-125">Turco</span><span class="sxs-lookup"><span data-stu-id="49c6b-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="49c6b-126">Modelos do Visual Studio dão suporte a vários repositórios de pacote pré-instalados</span><span class="sxs-lookup"><span data-stu-id="49c6b-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="49c6b-127">Se você gerar modelos do Visual Studio, você pode usar o NuGet para [pré-instalar pacotes](../visual-studio-extensibility/visual-studio-templates.md) como parte do modelo.</span><span class="sxs-lookup"><span data-stu-id="49c6b-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="49c6b-128">Até agora, esse recurso tinha uma limitação que todos os pacotes necessários para provenientes da mesma origem.</span><span class="sxs-lookup"><span data-stu-id="49c6b-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="49c6b-129">Com o NuGet 2.2.1, no entanto, você pode ter pacotes instalados de vários repositórios (dentro do modelo, um VSIX ou uma pasta no disco definido no registro).</span><span class="sxs-lookup"><span data-stu-id="49c6b-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="49c6b-130">O cenário principal para esse recurso é modelos de projeto personalizados do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="49c6b-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="49c6b-131">Os modelos internos do ASP.NET usam pacotes pré-instalados, receberão pacotes do disco local.</span><span class="sxs-lookup"><span data-stu-id="49c6b-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="49c6b-132">Agora você pode criar um modelo de projeto personalizado do ASP.NET que usa os pacotes existentes instalados pelo ASP.NET mas adicionar pacotes do NuGet extras ao seu modelo.</span><span class="sxs-lookup"><span data-stu-id="49c6b-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="49c6b-133">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="49c6b-133">Bug Fixes</span></span>
<span data-ttu-id="49c6b-134">O NuGet 2.2.1 inclui algumas correções de bugs de destino.</span><span class="sxs-lookup"><span data-stu-id="49c6b-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="49c6b-135">Para obter uma lista de trabalho itens corrigidos no NuGet 2.2.1, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="49c6b-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="49c6b-136">Problemas Conhecidos</span><span class="sxs-lookup"><span data-stu-id="49c6b-136">Known Issues</span></span>

<span data-ttu-id="49c6b-137">Se você estiver estendendo modelos de projeto do ASP.NET, todos os repositórios de pacote pré-instalado devem usar o mesmo valor para o `isPreunzipped` atributo.</span><span class="sxs-lookup"><span data-stu-id="49c6b-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
