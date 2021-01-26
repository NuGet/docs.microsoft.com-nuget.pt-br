---
title: Notas de versão do NuGet 2.8.5
description: Notas de versão do NuGet 2.8.5 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780354"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="8be4a-103">Notas de versão do NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="8be4a-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="8be4a-104">Notas de versão do [NuGet 2.8.3](../release-notes/nuget-2.8.3.md)  |  [Notas de versão do NuGet 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="8be4a-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="8be4a-105">O NuGet 2.8.5 foi lançado em 30 de março de 2015.</span><span class="sxs-lookup"><span data-stu-id="8be4a-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="8be4a-106">É uma pequena atualização para nosso VSIX 2.8.3 com algumas correções direcionadas.</span><span class="sxs-lookup"><span data-stu-id="8be4a-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="8be4a-107">Nesta versão, a caixa de diálogo suporte para Gerenciador de pacotes NuGet foi adicionada para [monikers da estrutura de destino do DNX](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="8be4a-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="8be4a-108">Esses novos monikers de estrutura com suporte incluem:</span><span class="sxs-lookup"><span data-stu-id="8be4a-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="8be4a-109">**core50** -um "base" moniker da estrutura de destino (TFM) que é compatível com o CLR principal.</span><span class="sxs-lookup"><span data-stu-id="8be4a-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="8be4a-110">**dnx452** -um TFM específico para aplicativos baseados em DNX usando a versão 4.5.2 completa da estrutura</span><span class="sxs-lookup"><span data-stu-id="8be4a-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="8be4a-111">**dnx46** -um TFM específico para aplicativos baseados em DNX usando a versão 4,6 completa da estrutura</span><span class="sxs-lookup"><span data-stu-id="8be4a-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="8be4a-112">**dnxcore50** -um TFM específico para aplicativos baseados em DNX usando a versão Core 5,0 da estrutura</span><span class="sxs-lookup"><span data-stu-id="8be4a-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="8be4a-113">Foi corrigido um bug que impedia a instalação correta de pacotes em projetos FSharp:</span><span class="sxs-lookup"><span data-stu-id="8be4a-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400