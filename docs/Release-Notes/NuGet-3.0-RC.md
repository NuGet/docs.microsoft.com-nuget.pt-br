---
title: "Notas de versão do NuGet 3.0 RC | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão do NuGet 3.0 RC, incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão RC do NuGet 3.0, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4693fd8884283e01d3c0a8ad74e0692c1ca00659
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="db0a4-104">Notas de versão do NuGet 3.0 RC</span><span class="sxs-lookup"><span data-stu-id="db0a4-104">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="db0a4-105">[Notas de versão do NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md) | [notas de versão do NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="db0a4-105">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="db0a4-106">Com o lançamento do Visual Studio 2015 RC, NuGet 3.0 RC foi lançado em 29 de abril de 2015.</span><span class="sxs-lookup"><span data-stu-id="db0a4-106">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="db0a4-107">Esta versão tem um número de correções de bugs importantes, melhorias de desempenho e atualizações para dar suporte as novas estruturas.</span><span class="sxs-lookup"><span data-stu-id="db0a4-107">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="db0a4-108">Só está disponível para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="db0a4-108">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="db0a4-109">Enfoque no desempenho</span><span class="sxs-lookup"><span data-stu-id="db0a4-109">Continued Focus on Performance</span></span>

<span data-ttu-id="db0a4-110">Estabilidade e desempenho de consultas do NuGet continuam a ser um assunto foco.</span><span class="sxs-lookup"><span data-stu-id="db0a4-110">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="db0a4-111">Com esta versão, você começará a ver as operações de pesquisa muito rápida do NuGet UI e do site.</span><span class="sxs-lookup"><span data-stu-id="db0a4-111">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="db0a4-112">Estamos monitorando o serviço e como usar o serviço para que possamos continuar a ajustar essas operações.</span><span class="sxs-lookup"><span data-stu-id="db0a4-112">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="db0a4-113">Problemas significativos resolvidos</span><span class="sxs-lookup"><span data-stu-id="db0a4-113">Significant Issues Resolved</span></span>

<span data-ttu-id="db0a4-114">Para estabilizar os clientes do NuGet, solucionado muitos problemas como parte desta versão.</span><span class="sxs-lookup"><span data-stu-id="db0a4-114">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="db0a4-115">Aqui está a apenas uma lista breve de alguns dos problemas mais importantes resolvidos:</span><span class="sxs-lookup"><span data-stu-id="db0a4-115">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="db0a4-116">Como parte da renomeação do framework K para ASP.NET 5, identificadores de framework foram atualizados para tratar dnx e dnxcore [link](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="db0a4-116">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="db0a4-117">Adicionada a documentação de ajuda de links na interface do usuário do Visual Studio [link](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="db0a4-117">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="db0a4-118">Melhor tratamento de referências complexas em `.nuspec` com referências de framework delimitada por vírgulas [link](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="db0a4-118">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="db0a4-119">Corrigido o suporte para japonês culturas [link](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="db0a4-119">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="db0a4-120">O cliente atualizado para permitir que os projetos ASP.NET 5 usar os novos pontos de extremidade v3 [link](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="db0a4-120">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="db0a4-121">Pasta de pacotes de identificador atualizado para melhor com controle de origem [link](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="db0a4-121">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="db0a4-122">Corrigido o suporte para pacotes de satélite [link](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="db0a4-122">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="db0a4-123">Corrigido o suporte para os arquivos de conteúdo específica da estrutura [link](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="db0a4-123">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="db0a4-124">Revisão de presença do GitHub</span><span class="sxs-lookup"><span data-stu-id="db0a4-124">GitHub presence overhaul</span></span>

<span data-ttu-id="db0a4-125">Fizemos algumas alterações para nosso [da fonte de repositórios de código no GitHub](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="db0a4-125">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="db0a4-126">Se você tiver problemas com o cliente do NuGet Visual Studio, os comandos do Powershell ou a linha de comando executável faça esses problemas e monitorar seu progresso em nosso [lista de problemas do repositório GitHub Home](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="db0a4-126">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="db0a4-127">Estamos acompanhando problemas para a galeria no nosso [repositório GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="db0a4-127">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="db0a4-128">Fique atento</span><span class="sxs-lookup"><span data-stu-id="db0a4-128">Stay Tuned</span></span>

<span data-ttu-id="db0a4-129">Fique atento [nosso blog](http://blog.nuget.org) para mais de progresso e avisos do NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="db0a4-129">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>