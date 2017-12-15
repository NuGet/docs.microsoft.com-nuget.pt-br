---
title: "Notas de versão do NuGet 2.8.6 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 920c551c-18a7-40f4-a32b-ce84de6ea766
description: "Notas de versão do NuGet 2.8.6 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs."
keywords: "Notas de versão NuGet 2.8.6, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f33c1edd3ef703a8cd97b7bdd97c37e12426aafa
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="94a00-104">Notas de versão do NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="94a00-104">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="94a00-105">[Notas de versão do NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [notas de versão do NuGet 2.8.7](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="94a00-105">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="94a00-106">NuGet 2.8.6 foi liberado 20 de julho de 2015 como uma pequena atualização para o nosso 2.8.5 direcionado de VSIX com algumas correções e aprimoramentos para oferecer suporte a pacotes que podem ser entregues com suporte para o modelo de desenvolvimento de UWP do Windows 10.</span><span class="sxs-lookup"><span data-stu-id="94a00-106">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="94a00-107">Esta versão da extensão de Gerenciador de pacote do NuGet fornece suporte para Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="94a00-107">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="94a00-108">Nesta versão, a caixa de diálogo Gerenciador de pacotes do NuGet tinha suporte adicionado para:</span><span class="sxs-lookup"><span data-stu-id="94a00-108">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="94a00-109">Introduziu o Moniker do Framework de destino UAP para dar suporte a desenvolvimento de aplicativos do Windows 10.</span><span class="sxs-lookup"><span data-stu-id="94a00-109">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="94a00-110">Pontos de extremidade do NuGet protocol versão 3</span><span class="sxs-lookup"><span data-stu-id="94a00-110">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="94a00-111">Suporte para [config](../consume-packages/configuring-nuget-behavior.md) atributo protocolVersion em fontes de repositório.</span><span class="sxs-lookup"><span data-stu-id="94a00-111">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="94a00-112">O valor padrão é "2"</span><span class="sxs-lookup"><span data-stu-id="94a00-112">Default value is "2"</span></span>
* <span data-ttu-id="94a00-113">Voltando para o repositório remoto se uma versão de pacote necessária não está disponível no cache local</span><span class="sxs-lookup"><span data-stu-id="94a00-113">Falling back to remote repository if a required package version is not available in the local cache</span></span>