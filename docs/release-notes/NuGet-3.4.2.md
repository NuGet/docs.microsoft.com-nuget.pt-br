---
title: Notas de versão do NuGet 3.4.2
description: Notas de versão do NuGet 3.4.2 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780256"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="1c20a-103">Notas de versão do NuGet 3.4.2</span><span class="sxs-lookup"><span data-stu-id="1c20a-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="1c20a-104">Notas de versão do [NuGet 3.4.1](../release-notes/nuget-3.4.1.md)  |  [Notas de versão do NuGet 3.4.3](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="1c20a-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="1c20a-105">O NuGet 3.4.2 foi lançado em 8 de abril de 2016 para resolver vários problemas identificados na versão 3,4 e 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="1c20a-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="1c20a-106">nuget.exe o 3.4.2 RC já está disponível</span><span class="sxs-lookup"><span data-stu-id="1c20a-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="1c20a-107">Você pode baixar a versão Release Candidate do nuget.exe 3.4.2 [aqui](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="1c20a-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="1c20a-108">Atualizações e aprimoramentos</span><span class="sxs-lookup"><span data-stu-id="1c20a-108">Updates and Improvements</span></span>

* <span data-ttu-id="1c20a-109">Melhoramos significativamente o desempenho das atualizações em um cenário específico, em que as atualizações em pacotes com grafos de dependência profunda levaram muito tempo e travaram o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1c20a-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="1c20a-110">a restauração do NuGet sem tráfego de rede é 2,5 x a 3 vezes mais rápido no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1c20a-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="1c20a-111">Além dessa alteração, corrigimos um problema em que estávamos atingindo a rede duas vezes ao buscar a contagem de atualizações na interface do usuário do VS.</span><span class="sxs-lookup"><span data-stu-id="1c20a-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="1c20a-112">Isso foi parcialmente responsável por alguns problemas de tempo limite que os clientes experimentaram em 3.4/3.4.1.</span><span class="sxs-lookup"><span data-stu-id="1c20a-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="1c20a-113">Adicionado suporte para no_proxy configuração</span><span class="sxs-lookup"><span data-stu-id="1c20a-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="1c20a-114">Correções</span><span class="sxs-lookup"><span data-stu-id="1c20a-114">Fixes</span></span>

* <span data-ttu-id="1c20a-115">Corrigido um problema em que a origem do nuget.org estava ausente nas configurações do NuGet ou na configuração após a atualização para o 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="1c20a-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="1c20a-116">Corrigido um problema em que uma alteração de maiúsculas e minúsculas em FindPackagesById no artefato de quebras de 3.4.1.</span><span class="sxs-lookup"><span data-stu-id="1c20a-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="1c20a-117">Correção de um problema com o FIPS que causou falhas com a restauração do NuGet com nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="1c20a-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="1c20a-118">Correção de uma falha ao procurar fontes com URL de ícone inválido.</span><span class="sxs-lookup"><span data-stu-id="1c20a-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="1c20a-119">Correção de problemas com as versões e entradas de mesclagem de ' todas as fontes '.</span><span class="sxs-lookup"><span data-stu-id="1c20a-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="1c20a-120">Problemas conhecidos no 3.4.2 Windows x86 CommandLine (RC)</span><span class="sxs-lookup"><span data-stu-id="1c20a-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="1c20a-121">Esses problemas serão corrigidos no início da próxima semana antes de atingirmos o RTM.</span><span class="sxs-lookup"><span data-stu-id="1c20a-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="1c20a-122">A execução da restauração do NuGet em uma solução falhará se o arquivo da solução for colocado em uma hierarquia de pastas inferior aos arquivos do projeto.</span><span class="sxs-lookup"><span data-stu-id="1c20a-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="1c20a-123">A execução do comando de exclusão do NuGet em um pacote usando o feed v2 falhará.</span><span class="sxs-lookup"><span data-stu-id="1c20a-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="1c20a-124">Em vez disso, use o feed v3.</span><span class="sxs-lookup"><span data-stu-id="1c20a-124">Use V3 feed instead.</span></span>


<span data-ttu-id="1c20a-125">Para obter uma lista completa de correções e aprimoramentos nesta versão, confira a lista de problemas [aqui](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span><span class="sxs-lookup"><span data-stu-id="1c20a-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>