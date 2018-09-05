---
title: Notas de versão do NuGet 3.4.2
description: Notas de versão do NuGet 3.4.2 incluindo conhecidos problemas, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549145"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="5c9da-103">Notas de versão do NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="5c9da-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="5c9da-104">[Notas de versão do NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [notas de versão do NuGet 3.4.3](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="5c9da-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="5c9da-105">O NuGet 3.4.2 foi lançado em 8 de abril de 2016 para abordar vários problemas que foram identificados na 3.4 e 3.4.1 de versão.</span><span class="sxs-lookup"><span data-stu-id="5c9da-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="5c9da-106">NuGet.exe 3.4.2 RC agora está disponível</span><span class="sxs-lookup"><span data-stu-id="5c9da-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="5c9da-107">Você pode baixar o versão Release candidate do nuget.exe 3.4.2 [aqui](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="5c9da-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="5c9da-108">Atualizações e aprimoramentos</span><span class="sxs-lookup"><span data-stu-id="5c9da-108">Updates and Improvements</span></span>

* <span data-ttu-id="5c9da-109">Aprimoramos consideravelmente o desempenho de atualizações em um cenário específico, onde as atualizações em pacotes com grafos de dependência profunda demoravam muito tempo e parou ao Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c9da-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="5c9da-110">restauração do NuGet sem que o tráfego de rede é 2,5 x – 3 vezes mais rápido dentro do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c9da-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="5c9da-111">Além dessa alteração, corrigimos um problema em que podemos foram acessando a rede duas vezes quando buscando a atualização de contagem na interface do usuário VS.</span><span class="sxs-lookup"><span data-stu-id="5c9da-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="5c9da-112">Isso foi parcialmente responsável por alguns clientes de problemas de tempo limite experientes em 3.4/3.4.1.</span><span class="sxs-lookup"><span data-stu-id="5c9da-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="5c9da-113">Adicionado suporte para configuração de no_proxy</span><span class="sxs-lookup"><span data-stu-id="5c9da-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="5c9da-114">Correções</span><span class="sxs-lookup"><span data-stu-id="5c9da-114">Fixes</span></span>

* <span data-ttu-id="5c9da-115">Corrigido um problema no qual origem nuget.org estava ausente nas configurações de NuGet ou configuração após a atualização para 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="5c9da-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="5c9da-116">Corrigido um problema em que uma alteração de maiusculas e minúsculas para FindPackagesById no 3.4.1 rompe Artifactory.</span><span class="sxs-lookup"><span data-stu-id="5c9da-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="5c9da-117">Corrigido um problema com o FIPS que causava falhas de restauração do NuGet com nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="5c9da-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="5c9da-118">Corrigida uma falha ao navegar por fontes com a URL do ícone inválido.</span><span class="sxs-lookup"><span data-stu-id="5c9da-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="5c9da-119">Correção de problemas com a mesclagem de versões e as entradas de 'Todas as fontes'.</span><span class="sxs-lookup"><span data-stu-id="5c9da-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="5c9da-120">Problemas conhecidos no 3.4.2 linha de comando do Windows x86 (RC)</span><span class="sxs-lookup"><span data-stu-id="5c9da-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="5c9da-121">Esses problemas serão corrigidos logo na próxima semana antes de que atingimos RTM.</span><span class="sxs-lookup"><span data-stu-id="5c9da-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="5c9da-122">Restauração do nuget em execução em uma solução falhará se o arquivo de solução é colocado em uma hierarquia de pastas menor que os arquivos de projeto.</span><span class="sxs-lookup"><span data-stu-id="5c9da-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="5c9da-123">A execução do comando de exclusão do nuget em um pacote usando o feed V2 falhará.</span><span class="sxs-lookup"><span data-stu-id="5c9da-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="5c9da-124">Use o feed V3.</span><span class="sxs-lookup"><span data-stu-id="5c9da-124">Use V3 feed instead.</span></span>


<span data-ttu-id="5c9da-125">Para obter uma lista de correções e aprimoramentos nesta versão, confira a lista de problemas [aqui](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="5c9da-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>