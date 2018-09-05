---
title: Notas de versão do NuGet 3.0 RC
description: Notas de versão do NuGet 3.0 RC incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551713"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="5bf05-103">Notas de versão do NuGet 3.0 RC</span><span class="sxs-lookup"><span data-stu-id="5bf05-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="5bf05-104">[Notas de versão do NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md) | [notas de versão do NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="5bf05-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="5bf05-105">RC do NuGet 3.0 foi lançado em 29 de abril de 2015 com o lançamento do Visual Studio 2015 RC.</span><span class="sxs-lookup"><span data-stu-id="5bf05-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="5bf05-106">Esta versão tem uma série de correções de bugs importantes, melhorias de desempenho e as atualizações para dar suporte a novas estruturas.</span><span class="sxs-lookup"><span data-stu-id="5bf05-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="5bf05-107">Ele só está disponível para o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="5bf05-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="5bf05-108">Sobre o desempenho</span><span class="sxs-lookup"><span data-stu-id="5bf05-108">Continued Focus on Performance</span></span>

<span data-ttu-id="5bf05-109">Estabilidade e desempenho de consultas do NuGet continuam sendo um assunto que estamos nos concentrando no.</span><span class="sxs-lookup"><span data-stu-id="5bf05-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="5bf05-110">Com esta versão, você deve iniciar ver as operações de pesquisa muito rápida no site de UI NuGet e.</span><span class="sxs-lookup"><span data-stu-id="5bf05-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="5bf05-111">Estamos monitorando o serviço e como usar o serviço para que possamos continuar a ajustar essas operações.</span><span class="sxs-lookup"><span data-stu-id="5bf05-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="5bf05-112">Problemas significativos resolvidos</span><span class="sxs-lookup"><span data-stu-id="5bf05-112">Significant Issues Resolved</span></span>

<span data-ttu-id="5bf05-113">Para se estabilizar os clientes do NuGet, resolvemos muitos problemas como parte desta versão.</span><span class="sxs-lookup"><span data-stu-id="5bf05-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="5bf05-114">Aqui é apenas uma lista breve de alguns dos problemas mais importantes que são resolvidos:</span><span class="sxs-lookup"><span data-stu-id="5bf05-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="5bf05-115">Como parte da renomeação do framework K para ASP.NET 5, monikers de estrutura foram atualizados para lidar com o dnx e dnxcore [link](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="5bf05-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="5bf05-116">Adicionada a documentação de ajuda de links na IU do Visual Studio [link](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="5bf05-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="5bf05-117">Melhor tratamento de referências complexas em `.nuspec` com referências de estrutura delimitada por vírgulas de [link](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="5bf05-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="5bf05-118">Corrigido o suporte para culturas japonês [link](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="5bf05-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="5bf05-119">O cliente atualizado para permitir que os projetos ASP.NET 5 usar os novos pontos de extremidade v3 [link](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="5bf05-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="5bf05-120">Atualizado para melhor identificador de pasta de pacotes com controle do código-fonte [link](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="5bf05-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="5bf05-121">Corrigido o suporte para pacotes satélite [link](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="5bf05-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="5bf05-122">Corrigido o suporte para arquivos de conteúdo específicos de estrutura [link](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="5bf05-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="5bf05-123">Revisão de presença do GitHub</span><span class="sxs-lookup"><span data-stu-id="5bf05-123">GitHub presence overhaul</span></span>

<span data-ttu-id="5bf05-124">Fizemos algumas alterações em nossos [fonte de repositórios de código no GitHub](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="5bf05-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="5bf05-125">Se você tiver problemas com o cliente do NuGet Visual Studio, os comandos do Powershell ou da linha de comando executável faça esses problemas e monitorar seu progresso em nossa [lista de problemas do repositório GitHub Home](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="5bf05-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="5bf05-126">Estamos acompanhando problemas para a Galeria em nossa [repositório GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="5bf05-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="5bf05-127">Fique ligado</span><span class="sxs-lookup"><span data-stu-id="5bf05-127">Stay Tuned</span></span>

<span data-ttu-id="5bf05-128">Por favor, fique atento [nosso blog](http://blog.nuget.org) para obter mais progresso e anúncios para NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="5bf05-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>