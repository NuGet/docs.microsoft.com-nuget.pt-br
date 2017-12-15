---
title: "Notas de versão do NuGet 2.8.5 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 60b96b2e-2a61-4f10-b5ad-3299f5a6d453
description: "Notas de versão do NuGet 2.8.5 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs."
keywords: "Notas de versão NuGet 2.8.5, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3b297704968b8423f60e9de08e27860dc375c019
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="1b0a8-104">Notas de versão do NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="1b0a8-104">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="1b0a8-105">[Notas de versão do NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [notas de versão do NuGet 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="1b0a8-105">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="1b0a8-106">NuGet 2.8.5 foi lançado em 30 de março de 2015.</span><span class="sxs-lookup"><span data-stu-id="1b0a8-106">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="1b0a8-107">É uma pequena atualização para nosso 2.8.3 VSIX com alguns direcionados correções.</span><span class="sxs-lookup"><span data-stu-id="1b0a8-107">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="1b0a8-108">Nesta versão, a caixa de diálogo Gerenciador de pacotes do NuGet foi adicionado suporte às [Monikers de Framework de destino do DNX](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="1b0a8-108">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="1b0a8-109">Esses novos identificadores de framework com suporte incluem:</span><span class="sxs-lookup"><span data-stu-id="1b0a8-109">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="1b0a8-110">**core50** - um moniker do framework (TFM) que é compatível com o CLR principal 'base' de destino.</span><span class="sxs-lookup"><span data-stu-id="1b0a8-110">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="1b0a8-111">**dnx452** - TFM A aplicativos específicos com base em DNX usando o 4.5.2 completo versão do framework</span><span class="sxs-lookup"><span data-stu-id="1b0a8-111">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="1b0a8-112">**dnx46** - TFM A aplicativos específicos com base em DNX usando a versão 4.6 completo do framework</span><span class="sxs-lookup"><span data-stu-id="1b0a8-112">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="1b0a8-113">**dnxcore50** - TFM A aplicativos específicos com base em DNX usando a versão 5.0 do núcleo do framework</span><span class="sxs-lookup"><span data-stu-id="1b0a8-113">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="1b0a8-114">Um bug foi corrigido que pacotes impedido de instalar nos projetos FSharp corretamente:</span><span class="sxs-lookup"><span data-stu-id="1b0a8-114">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

<span data-ttu-id="1b0a8-115">https://NuGet.codeplex.com/WorkItem/4400</span><span class="sxs-lookup"><span data-stu-id="1b0a8-115">https://nuget.codeplex.com/workitem/4400</span></span>