---
title: Notas de versão do NuGet 2.8.1
description: Notas de versão do NuGet 2.8.1 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8787aee36d31ed5d8071b35a8c243823029d135f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820515"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="7c040-103">Notas de versão do NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="7c040-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="7c040-104">[Notas de versão do NuGet 2.8](../release-notes/nuget-2.8.md) | [notas de versão do NuGet 2.8.2](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="7c040-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="7c040-105">NuGet 2.8.1 foi lançado em 2 de abril de 2014.</span><span class="sxs-lookup"><span data-stu-id="7c040-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="7c040-106">Recursos importantes da versão</span><span class="sxs-lookup"><span data-stu-id="7c040-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="7c040-107">Suporte para projetos do Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="7c040-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="7c040-108">Esta versão agora dá suporte a seguinte nova monikers destino do framework que podem ser usado para projetos de destino Windows Phone 8.1:</span><span class="sxs-lookup"><span data-stu-id="7c040-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="7c040-109">WindowsPhone81 / WP81 (para projetos do Windows Phone baseados no Silverlight)</span><span class="sxs-lookup"><span data-stu-id="7c040-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="7c040-110">WindowsPhoneApp81 / WPA81 (para projetos do WinRT com base no aplicativo do Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="7c040-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="7c040-111">Atualização da extensão do WebMatrix NuGet</span><span class="sxs-lookup"><span data-stu-id="7c040-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="7c040-112">Esta versão atualiza o cliente do NuGet encontrado no WebMatrix para [Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 e coloca com recursos como transformações XDT.</span><span class="sxs-lookup"><span data-stu-id="7c040-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="7c040-113">Mais importante, a versão 2.6.1 atualização core permite que o cliente o WebMatrix instalar os pacotes do NuGet que contêm versões mais recentes do `.nuspec` esquema, que inclui os pacotes do NuGet do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7c040-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="7c040-114">Para obter mais informações sobre a atualização da extensão do WebMatrix, consulte os específico [notas de versão](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="7c040-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="7c040-115">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="7c040-115">Bug Fixes</span></span>
<span data-ttu-id="7c040-116">Além desses recursos, esta versão do NuGet inclui outras correções de bug.</span><span class="sxs-lookup"><span data-stu-id="7c040-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="7c040-117">Não havia 16 questões total na versão.</span><span class="sxs-lookup"><span data-stu-id="7c040-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="7c040-118">Para obter uma lista completa do trabalho de itens corrigidos no NuGet 2.8.1,. exibir o [NuGet Issue Tracker para esta versão](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="7c040-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="7c040-119">Reshipping com o Visual Studio CTP "14"</span><span class="sxs-lookup"><span data-stu-id="7c040-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="7c040-120">No CTP do Visual Studio "14" lançada em 3ª de junho de 2014, NuGet 2.8.1 é fornecido na caixa.</span><span class="sxs-lookup"><span data-stu-id="7c040-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="7c040-121">Os recursos que ele oferece suporte à permanecem no par com outros 2.8.1 VSIXes como do Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="7c040-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
