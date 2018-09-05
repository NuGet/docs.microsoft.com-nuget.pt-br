---
title: Notas de versão do NuGet 2.8.5
description: Notas de versão do NuGet 2.8.5 incluindo conhecidos problemas, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548619"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="86b91-103">Notas de versão do NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="86b91-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="86b91-104">[Notas de versão do NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [notas de versão do NuGet 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="86b91-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="86b91-105">O NuGet 2.8.5 foi lançado em 30 de março de 2015.</span><span class="sxs-lookup"><span data-stu-id="86b91-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="86b91-106">Ele é uma pequena atualização para nossos 2.8.3 VSIX com alguns destino correções.</span><span class="sxs-lookup"><span data-stu-id="86b91-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="86b91-107">Nesta versão, a caixa de diálogo Gerenciador de pacotes do NuGet foi adicionado suporte às [Monikers da estrutura de destino DNX](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="86b91-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="86b91-108">Esses novos monikers de estrutura com suporte incluem:</span><span class="sxs-lookup"><span data-stu-id="86b91-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="86b91-109">**core50** – um moniker de estrutura (TFM) é compatível com o Core CLR de destino 'base'.</span><span class="sxs-lookup"><span data-stu-id="86b91-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="86b91-110">**dnx452** – aplicativos específicos com base em DNX um TFM, usando o 4.5.2 completo versão do framework</span><span class="sxs-lookup"><span data-stu-id="86b91-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="86b91-111">**dnx46** – aplicativos específicos com base em DNX um TFM, usando a versão 4.6 completa do framework</span><span class="sxs-lookup"><span data-stu-id="86b91-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="86b91-112">**dnxcore50** – aplicativos específicos com base em DNX um TFM, usando a versão 5.0 do núcleo do framework</span><span class="sxs-lookup"><span data-stu-id="86b91-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="86b91-113">Um bug foi corrigido que impedia pacotes seja instalado em projetos FSharp corretamente:</span><span class="sxs-lookup"><span data-stu-id="86b91-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400