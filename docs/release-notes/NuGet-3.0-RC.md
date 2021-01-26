---
title: Notas de versão do NuGet 3,0 RC
description: Notas de versão do NuGet 3,0 RC incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776571"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="8995f-103">Notas de versão do NuGet 3,0 RC</span><span class="sxs-lookup"><span data-stu-id="8995f-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="8995f-104">Notas de versão do [NuGet 3,0 beta](../release-notes/nuget-3.0-beta.md)  |  [Notas de versão do NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="8995f-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="8995f-105">O NuGet 3,0 RC foi lançado em 29 de abril de 2015 com a versão do Visual Studio 2015 RC.</span><span class="sxs-lookup"><span data-stu-id="8995f-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="8995f-106">Esta versão tem várias correções de bugs importantes, melhorias de desempenho e atualizações para dar suporte às novas estruturas.</span><span class="sxs-lookup"><span data-stu-id="8995f-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="8995f-107">Ele só está disponível para o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="8995f-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="8995f-108">Foco contínuo no desempenho</span><span class="sxs-lookup"><span data-stu-id="8995f-108">Continued Focus on Performance</span></span>

<span data-ttu-id="8995f-109">A estabilidade e o desempenho das consultas do NuGet continuam a ser um tópico dinâmico no qual estamos nos concentrando.</span><span class="sxs-lookup"><span data-stu-id="8995f-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="8995f-110">Com esta versão, você deve começar a ver operações de pesquisa muito rápidas na interface do usuário e no site do NuGet.</span><span class="sxs-lookup"><span data-stu-id="8995f-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="8995f-111">Estamos monitorando o serviço e como você pode usar o serviço para que possamos continuar a ajustar essas operações.</span><span class="sxs-lookup"><span data-stu-id="8995f-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="8995f-112">Problemas significativos resolvidos</span><span class="sxs-lookup"><span data-stu-id="8995f-112">Significant Issues Resolved</span></span>

<span data-ttu-id="8995f-113">Para estabilizar os clientes do NuGet, resolvemos muitos problemas como parte desta versão.</span><span class="sxs-lookup"><span data-stu-id="8995f-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="8995f-114">Aqui está apenas uma breve lista de alguns dos problemas mais importantes resolvidos:</span><span class="sxs-lookup"><span data-stu-id="8995f-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="8995f-115">Como parte da renomeação da estrutura K para ASP.NET 5, os monikers da estrutura foram atualizados para manipular o [link](https://github.com/NuGet/Home/issues/215) DNX e dnxcore</span><span class="sxs-lookup"><span data-stu-id="8995f-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="8995f-116">Documentação de ajuda adicionada de links no [link](https://github.com/NuGet/Home/issues/232) da interface do usuário do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8995f-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="8995f-117">Melhor manipulação de referências complexas no `.nuspec` com [link](https://github.com/NuGet/Home/issues/276) de referências de estrutura delimitada por vírgulas</span><span class="sxs-lookup"><span data-stu-id="8995f-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="8995f-118">Corrigido o suporte para o [link](https://github.com/NuGet/Home/issues/253) de culturas japonesas</span><span class="sxs-lookup"><span data-stu-id="8995f-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="8995f-119">Cliente atualizado para permitir que projetos ASP.NET 5 usem o [link](https://github.com/NuGet/Home/issues/219) de novos pontos de extremidade v3</span><span class="sxs-lookup"><span data-stu-id="8995f-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="8995f-120">Atualizado para melhor manipular a pasta de pacotes com o [link](https://github.com/NuGet/Home/issues/56) de controle do código-fonte</span><span class="sxs-lookup"><span data-stu-id="8995f-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="8995f-121">[Link](https://github.com/NuGet/Home/issues/17) de suporte fixo para pacotes satélite</span><span class="sxs-lookup"><span data-stu-id="8995f-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="8995f-122">[Link](https://github.com/NuGet/Home/issues/18) de suporte corrigido para arquivos de conteúdo específicos da estrutura</span><span class="sxs-lookup"><span data-stu-id="8995f-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="8995f-123">Revisão de presença do GitHub</span><span class="sxs-lookup"><span data-stu-id="8995f-123">GitHub presence overhaul</span></span>

<span data-ttu-id="8995f-124">Fizemos algumas alterações em nossos [repositórios de código-fonte no GitHub](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="8995f-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="8995f-125">Se você tiver problemas com o cliente NuGet do Visual Studio, os comandos do PowerShell ou o executável de linha de comando, poderá registrar esses problemas e monitorar seu progresso em nossa [lista de problemas do repositório inicial do GitHub](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="8995f-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="8995f-126">Estamos acompanhando problemas para a galeria em nosso [repositório NuGetGallery do GitHub](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="8995f-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="8995f-127">Fique atento</span><span class="sxs-lookup"><span data-stu-id="8995f-127">Stay Tuned</span></span>

<span data-ttu-id="8995f-128">Fique atento ao [nosso blog](http://blog.nuget.org) para obter mais progresso e anúncios para o NuGet 3,0!</span><span class="sxs-lookup"><span data-stu-id="8995f-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>