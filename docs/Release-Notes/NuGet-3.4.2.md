---
title: Notas de versão do NuGet 3.4.2
description: Notas de versão do NuGet 3.4.2 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 88d29a84e280433663ab6c1c04ae16e1329420f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="ca580-103">Notas de versão do NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="ca580-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="ca580-104">[Notas de versão do NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [notas de versão do NuGet 3.4.3](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="ca580-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="ca580-105">NuGet 3.4.2 foi lançado em 8 de abril de 2016 para abordar vários problemas que foram identificados no 3.4 e 3.4.1 de versão.</span><span class="sxs-lookup"><span data-stu-id="ca580-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="ca580-106">NuGet.exe 3.4.2 RC agora está disponível</span><span class="sxs-lookup"><span data-stu-id="ca580-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="ca580-107">Você pode baixar a versão release candidate do nuget.exe 3.4.2 [aqui](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="ca580-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="ca580-108">Atualizações e aprimoramentos</span><span class="sxs-lookup"><span data-stu-id="ca580-108">Updates and Improvements</span></span>

* <span data-ttu-id="ca580-109">Aprimoramos significativamente o desempenho de atualizações em um cenário específico, onde as atualizações em pacotes com gráficos de dependência profunda levaram muito tempo e suspenso Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca580-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="ca580-110">restauração do NuGet sem o tráfego de rede é 2,5 x – 3 vezes mais rápido do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca580-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="ca580-111">Além dessa alteração, corrigimos um problema em que podemos foram atingir a rede duas vezes quando buscar a atualização de contagem na IU do VS.</span><span class="sxs-lookup"><span data-stu-id="ca580-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="ca580-112">Isso foi parcialmente responsável por alguns clientes de problemas de tempo limite experiência em 3.4/3.4.1.</span><span class="sxs-lookup"><span data-stu-id="ca580-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="ca580-113">Adicionado suporte para configuração de no_proxy</span><span class="sxs-lookup"><span data-stu-id="ca580-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="ca580-114">Correções</span><span class="sxs-lookup"><span data-stu-id="ca580-114">Fixes</span></span>

* <span data-ttu-id="ca580-115">Corrigido um problema em que nuget.org fonte estava ausente nas configurações do NuGet ou de configuração após a atualização para 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="ca580-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="ca580-116">Corrigido um problema em que uma alteração de maiusculas e minúsculas para FindPackagesById no 3.4.1 quebras Artifactory.</span><span class="sxs-lookup"><span data-stu-id="ca580-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="ca580-117">Corrigido um problema com o FIPS que causou a falhas de restauração do NuGet com nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="ca580-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="ca580-118">Corrigido uma falha durante a navegação de fontes com a URL do ícone inválido.</span><span class="sxs-lookup"><span data-stu-id="ca580-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="ca580-119">Correção de problemas com a mesclagem de versões e as entradas de 'Todas as fontes'.</span><span class="sxs-lookup"><span data-stu-id="ca580-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="ca580-120">Problemas conhecidos no 3.4.2 linha de comando do Windows x86 (RC)</span><span class="sxs-lookup"><span data-stu-id="ca580-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="ca580-121">Esses problemas serão corrigidos antecipado próxima semana antes de que atingiremos RTM.</span><span class="sxs-lookup"><span data-stu-id="ca580-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="ca580-122">Restauração do nuget em execução em uma solução falhará se o arquivo de solução é colocado em uma hierarquia de pasta menor que os arquivos de projeto.</span><span class="sxs-lookup"><span data-stu-id="ca580-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="ca580-123">Executar o comando de exclusão do nuget em um pacote usando o feed V2 falhará.</span><span class="sxs-lookup"><span data-stu-id="ca580-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="ca580-124">Use o feed V3.</span><span class="sxs-lookup"><span data-stu-id="ca580-124">Use V3 feed instead.</span></span>


<span data-ttu-id="ca580-125">Para obter uma lista de correções e aperfeiçoamentos desta versão, confira a lista de problemas [aqui](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="ca580-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>