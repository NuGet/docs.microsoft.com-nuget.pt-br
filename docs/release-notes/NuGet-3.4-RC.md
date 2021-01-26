---
title: Notas de versão do NuGet 3,4-RC
description: Notas de versão do NuGet 3,4 RC incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780243"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="bd106-103">Notas de versão do NuGet 3,4-RC</span><span class="sxs-lookup"><span data-stu-id="bd106-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="bd106-104">Notas de versão do [NuGet 3,3](../release-notes/nuget-3.3.md)  |  [Notas de versão do NuGet 3,4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="bd106-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="bd106-105">O NuGet 3,4-RC foi lançado em 3 de março de 2016 juntamente com o Visual Studio 2015 atualização 2 RC e foi criado com algumas filosofias nas mentes:</span><span class="sxs-lookup"><span data-stu-id="bd106-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="bd106-106">Suporte de plataforma cruzada</span><span class="sxs-lookup"><span data-stu-id="bd106-106">Cross-Platform support</span></span>
* <span data-ttu-id="bd106-107">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="bd106-107">Performance improvements</span></span>
* <span data-ttu-id="bd106-108">Melhorias secundárias da interface do usuário</span><span class="sxs-lookup"><span data-stu-id="bd106-108">Minor UI improvements</span></span>

<span data-ttu-id="bd106-109">Os recursos a seguir estão disponíveis neste RC, com mais planejamento para a versão final de 3,4.</span><span class="sxs-lookup"><span data-stu-id="bd106-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="bd106-110">Novos recursos</span><span class="sxs-lookup"><span data-stu-id="bd106-110">New Features</span></span>

* <span data-ttu-id="bd106-111">Os clientes NuGet agora dão suporte à codificação de conteúdo gzip de repositórios</span><span class="sxs-lookup"><span data-stu-id="bd106-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="bd106-112">Suporte para PDBs de pacotes em projetos xproj</span><span class="sxs-lookup"><span data-stu-id="bd106-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="bd106-113">Suporte para ações de compilação do iOS e Android no elemento contentFiles</span><span class="sxs-lookup"><span data-stu-id="bd106-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="bd106-114">Suporte para os monikers do netstandard e do netstandardapp Framework</span><span class="sxs-lookup"><span data-stu-id="bd106-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="bd106-115">Novos recursos da interface do usuário</span><span class="sxs-lookup"><span data-stu-id="bd106-115">New User Interface Features</span></span>

* <span data-ttu-id="bd106-116">Melhorias significativas de desempenho, especialmente nas guias instalado, atualizações e consolidar</span><span class="sxs-lookup"><span data-stu-id="bd106-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="bd106-117">As guias instaladas e atualizadas agora são classificadas alfabeticamente</span><span class="sxs-lookup"><span data-stu-id="bd106-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="bd106-118">Adicionado um botão Atualizar que permite que uma pesquisa seja atualizada</span><span class="sxs-lookup"><span data-stu-id="bd106-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="bd106-119">Atualizações e aprimoramentos</span><span class="sxs-lookup"><span data-stu-id="bd106-119">Updates and Improvements</span></span>

* <span data-ttu-id="bd106-120">Os pacotes referenciados no `project.json` que têm uma versão flutuante não serão atualizados em cada compilação.</span><span class="sxs-lookup"><span data-stu-id="bd106-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="bd106-121">Em vez disso, eles serão atualizados somente quando forçados a restaurar, limpar, recompilar ou modificar `project.json` .</span><span class="sxs-lookup"><span data-stu-id="bd106-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="bd106-122">as fontes de repositório nuget.org não são mais forçadas para uma configuração de projeto quando você usa a interface do usuário de configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="bd106-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="bd106-123">O NuGet não restaura mais os pacotes em projetos compartilhados nem grava um arquivo de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="bd106-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="bd106-124">Melhoramos a falha de rede e a manipulação de tentativas para servidores inacessíveis ou lentos para responder.</span><span class="sxs-lookup"><span data-stu-id="bd106-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="bd106-125">Os comportamentos de teclado e mouse são aprimorados na interface do usuário do Gerenciador de pacotes do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bd106-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="bd106-126">Agora, damos suporte ao `project.json` esquema mais recente em DNX.</span><span class="sxs-lookup"><span data-stu-id="bd106-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="bd106-127">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="bd106-127">Known Issues</span></span>

<span data-ttu-id="bd106-128">Continuamos a acompanhar problemas em nossa lista de problemas do GitHub, que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="bd106-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>