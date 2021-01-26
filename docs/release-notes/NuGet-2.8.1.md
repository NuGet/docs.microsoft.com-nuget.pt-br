---
title: Notas de versão do NuGet 2.8.1
description: Notas de versão do NuGet 2.8.1 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776770"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="1901f-103">Notas de versão do NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="1901f-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="1901f-104">Notas de versão do [NuGet 2,8](../release-notes/nuget-2.8.md)  |  [Notas de versão do NuGet 2.8.2](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="1901f-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="1901f-105">O NuGet 2.8.1 foi lançado em 2 de abril de 2014.</span><span class="sxs-lookup"><span data-stu-id="1901f-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="1901f-106">Recursos notáveis na versão</span><span class="sxs-lookup"><span data-stu-id="1901f-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="1901f-107">Suporte para projetos Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="1901f-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="1901f-108">Esta versão agora dá suporte aos seguintes novos monikers da estrutura de destino que podem ser usados para direcionar Windows Phone projetos 8,1:</span><span class="sxs-lookup"><span data-stu-id="1901f-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="1901f-109">WindowsPhone81/WP81 (para projetos Windows Phone baseados no Silverlight)</span><span class="sxs-lookup"><span data-stu-id="1901f-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="1901f-110">WindowsPhoneApp81/WPA81 (para projetos de aplicativo Windows Phone baseados em WinRT)</span><span class="sxs-lookup"><span data-stu-id="1901f-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="1901f-111">Atualização da extensão do WebMatrix do NuGet</span><span class="sxs-lookup"><span data-stu-id="1901f-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="1901f-112">Esta versão atualiza o cliente NuGet encontrado no WebMatrix para [NuGet. Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 e traz recursos de ti, como transformações de xdt.</span><span class="sxs-lookup"><span data-stu-id="1901f-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="1901f-113">O mais importante é que a atualização do 2.6.1 Core permite que o cliente do WebMatrix instale pacotes NuGet que contêm versões mais recentes do `.nuspec` esquema, que inclui os pacotes NuGet do ASP.net.</span><span class="sxs-lookup"><span data-stu-id="1901f-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="1901f-114">Para obter mais informações sobre a atualização de extensão do WebMatrix, consulte as [notas de versão](../release-notes/nuget-2.6.1-for-WebMatrix.md)específicas.</span><span class="sxs-lookup"><span data-stu-id="1901f-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="1901f-115">Correções de bugs</span><span class="sxs-lookup"><span data-stu-id="1901f-115">Bug Fixes</span></span>
<span data-ttu-id="1901f-116">Além desses recursos, esta versão do NuGet inclui outras correções de bugs.</span><span class="sxs-lookup"><span data-stu-id="1901f-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="1901f-117">Houve 16 problemas totais abordados na versão.</span><span class="sxs-lookup"><span data-stu-id="1901f-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="1901f-118">Para obter uma lista completa dos itens de trabalho corrigidos no NuGet 2.8.1, consulte o [rastreador de problemas do NuGet para esta versão](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="1901f-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="1901f-119">Reentregando com o Visual Studio "14" CTP</span><span class="sxs-lookup"><span data-stu-id="1901f-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="1901f-120">No Visual Studio "14" CTP lançado em 3 de junho de 2014, o NuGet 2.8.1 é fornecido na caixa.</span><span class="sxs-lookup"><span data-stu-id="1901f-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="1901f-121">Os recursos para os quais ele dá suporte permanecem em conta com outros VSIXs 2.8.1, como aquele para Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="1901f-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
