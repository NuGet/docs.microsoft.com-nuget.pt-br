---
title: "Notas de versão do NuGet 2.8.1 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão do NuGet 2.8.1 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs."
keywords: "Notas de versão NuGet 2.8.1, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 99dd050eb06024972132d5b0dcc9f97f965adc12
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="ce94e-104">Notas de versão do NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="ce94e-104">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="ce94e-105">[Notas de versão do NuGet 2.8](../release-notes/nuget-2.8.md) | [notas de versão do NuGet 2.8.2](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="ce94e-105">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="ce94e-106">NuGet 2.8.1 foi lançado em 2 de abril de 2014.</span><span class="sxs-lookup"><span data-stu-id="ce94e-106">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="ce94e-107">Recursos importantes da versão</span><span class="sxs-lookup"><span data-stu-id="ce94e-107">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="ce94e-108">Suporte para projetos do Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="ce94e-108">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="ce94e-109">Esta versão agora dá suporte a seguinte nova monikers destino do framework que podem ser usado para projetos de destino Windows Phone 8.1:</span><span class="sxs-lookup"><span data-stu-id="ce94e-109">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="ce94e-110">WindowsPhone81 / WP81 (para projetos do Windows Phone baseados no Silverlight)</span><span class="sxs-lookup"><span data-stu-id="ce94e-110">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="ce94e-111">WindowsPhoneApp81 / WPA81 (para projetos do WinRT com base no aplicativo do Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="ce94e-111">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="ce94e-112">Atualização da extensão do WebMatrix NuGet</span><span class="sxs-lookup"><span data-stu-id="ce94e-112">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="ce94e-113">Esta versão atualiza o cliente do NuGet encontrado no WebMatrix para [Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 e coloca com recursos como transformações XDT.</span><span class="sxs-lookup"><span data-stu-id="ce94e-113">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="ce94e-114">Mais importante, a versão 2.6.1 atualização core permite que o cliente o WebMatrix instalar os pacotes do NuGet que contêm versões mais recentes do `.nuspec` esquema, que inclui os pacotes do NuGet do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ce94e-114">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="ce94e-115">Para obter mais informações sobre a atualização da extensão do WebMatrix, consulte os específico [notas de versão](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="ce94e-115">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="ce94e-116">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="ce94e-116">Bug Fixes</span></span>
<span data-ttu-id="ce94e-117">Além desses recursos, esta versão do NuGet inclui outras correções de bug.</span><span class="sxs-lookup"><span data-stu-id="ce94e-117">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="ce94e-118">Não havia 16 questões total na versão.</span><span class="sxs-lookup"><span data-stu-id="ce94e-118">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="ce94e-119">Para obter uma lista completa do trabalho de itens corrigidos no NuGet 2.8.1,. exibir o [NuGet Issue Tracker para esta versão](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="ce94e-119">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="ce94e-120">Reshipping com o Visual Studio CTP "14"</span><span class="sxs-lookup"><span data-stu-id="ce94e-120">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="ce94e-121">No CTP do Visual Studio "14" lançada em 3ª de junho de 2014, NuGet 2.8.1 é fornecido na caixa.</span><span class="sxs-lookup"><span data-stu-id="ce94e-121">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="ce94e-122">Os recursos que ele oferece suporte à permanecem no par com outros 2.8.1 VSIXes como do Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="ce94e-122">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
