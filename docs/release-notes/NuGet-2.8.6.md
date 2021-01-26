---
title: Notas de versão do NuGet 2.8.6
description: Notas de versão do NuGet 2.8.6 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776707"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="51c19-103">Notas de versão do NuGet 2.8.6</span><span class="sxs-lookup"><span data-stu-id="51c19-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="51c19-104">Notas de versão do [NuGet 2.8.5](../release-notes/nuget-2.8.5.md)  |  [Notas de versão do NuGet 2.8.7](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="51c19-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="51c19-105">O NuGet 2.8.6 foi lançado em 20 de julho de 2015 como uma pequena atualização para nosso VSIX 2.8.5 com algumas correções e aprimoramentos direcionados para oferecer suporte a pacotes que podem ser fornecidos com suporte para o modelo de desenvolvimento UWP do Windows 10.</span><span class="sxs-lookup"><span data-stu-id="51c19-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="51c19-106">Esta versão da extensão do Gerenciador de pacotes NuGet fornece suporte somente para Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="51c19-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="51c19-107">Nesta versão, a caixa de diálogo Gerenciador de pacotes NuGet tinha suporte adicionado para:</span><span class="sxs-lookup"><span data-stu-id="51c19-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="51c19-108">Introduziu o moniker da estrutura de destino UAP para dar suporte ao desenvolvimento de aplicativos do Windows 10.</span><span class="sxs-lookup"><span data-stu-id="51c19-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="51c19-109">Pontos de extremidade da versão 3 do protocolo NuGet</span><span class="sxs-lookup"><span data-stu-id="51c19-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="51c19-110">Suporte para [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) atributo protocolVersion em fontes de repositório.</span><span class="sxs-lookup"><span data-stu-id="51c19-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="51c19-111">O valor padrão é "2"</span><span class="sxs-lookup"><span data-stu-id="51c19-111">Default value is "2"</span></span>
* <span data-ttu-id="51c19-112">Voltando ao repositório remoto se uma versão de pacote necessária não estiver disponível no cache local</span><span class="sxs-lookup"><span data-stu-id="51c19-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>