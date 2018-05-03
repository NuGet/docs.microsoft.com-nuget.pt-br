---
title: Notas de versão do NuGet 2.8.5
description: Notas de versão do NuGet 2.8.5 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="55218-103">Notas de versão do NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="55218-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="55218-104">[Notas de versão do NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [notas de versão do NuGet 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="55218-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="55218-105">NuGet 2.8.5 foi lançado em 30 de março de 2015.</span><span class="sxs-lookup"><span data-stu-id="55218-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="55218-106">É uma pequena atualização para nosso 2.8.3 VSIX com alguns direcionados correções.</span><span class="sxs-lookup"><span data-stu-id="55218-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="55218-107">Nesta versão, a caixa de diálogo Gerenciador de pacotes do NuGet foi adicionado suporte às [Monikers de Framework de destino do DNX](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="55218-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="55218-108">Esses novos identificadores de framework com suporte incluem:</span><span class="sxs-lookup"><span data-stu-id="55218-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="55218-109">**core50** - um moniker do framework (TFM) que é compatível com o CLR principal 'base' de destino.</span><span class="sxs-lookup"><span data-stu-id="55218-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="55218-110">**dnx452** - TFM A aplicativos específicos com base em DNX usando o 4.5.2 completo versão do framework</span><span class="sxs-lookup"><span data-stu-id="55218-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="55218-111">**dnx46** - TFM A aplicativos específicos com base em DNX usando a versão 4.6 completo do framework</span><span class="sxs-lookup"><span data-stu-id="55218-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="55218-112">**dnxcore50** - TFM A aplicativos específicos com base em DNX usando a versão 5.0 do núcleo do framework</span><span class="sxs-lookup"><span data-stu-id="55218-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="55218-113">Um bug foi corrigido que pacotes impedido de instalar nos projetos FSharp corretamente:</span><span class="sxs-lookup"><span data-stu-id="55218-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400