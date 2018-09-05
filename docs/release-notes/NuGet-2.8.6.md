---
title: Notas de versão do NuGet 2.8.6
description: Notas de versão do NuGet 2.8.6 incluindo conhecidos problemas, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546485"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="21936-103">Notas de versão do NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="21936-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="21936-104">[Notas de versão do NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [notas de versão do NuGet 2.8.7](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="21936-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="21936-105">O NuGet 2.8.6 foi lançado 20 de julho de 2015 como uma pequena atualização para o nosso 2.8.5 direcionado de VSIX com algumas correções e aprimoramentos para oferecer suporte a pacotes que podem ser entregues com suporte para o modelo de desenvolvimento de UWP do Windows 10.</span><span class="sxs-lookup"><span data-stu-id="21936-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="21936-106">Esta versão do que a extensão de Gerenciador de pacotes do NuGet fornece suporte para Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="21936-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="21936-107">Nesta versão, a caixa de diálogo Gerenciador de pacotes NuGet tinha suporte adicionado para:</span><span class="sxs-lookup"><span data-stu-id="21936-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="21936-108">Introduziu o Moniker do Framework de destino UAP para dar suporte ao desenvolvimento de aplicativo do Windows 10.</span><span class="sxs-lookup"><span data-stu-id="21936-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="21936-109">Pontos de extremidade do NuGet protocol versão 3</span><span class="sxs-lookup"><span data-stu-id="21936-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="21936-110">Suporte para [NuGet. config](../consume-packages/configuring-nuget-behavior.md) atributo protocolVersion em fontes de repositório.</span><span class="sxs-lookup"><span data-stu-id="21936-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="21936-111">Valor padrão é "2"</span><span class="sxs-lookup"><span data-stu-id="21936-111">Default value is "2"</span></span>
* <span data-ttu-id="21936-112">Voltando para o repositório remoto se uma versão do pacote necessário não está disponível no cache local</span><span class="sxs-lookup"><span data-stu-id="21936-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>