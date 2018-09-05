---
title: Notas de versão do RC 3.4 do NuGet
description: Notas de versão do NuGet 3.4 RC incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546748"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="77382-103">Notas de versão do RC 3.4 do NuGet</span><span class="sxs-lookup"><span data-stu-id="77382-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="77382-104">[Notas de versão do NuGet 3.3](../release-notes/nuget-3.3.md) | [notas de versão do NuGet 3.4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="77382-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="77382-105">RC do NuGet 3.4 foi lançado 3 de março de 2016, juntamente com o Visual Studio 2015 atualização 2 RC e foi criado com alguns princípios em mente:</span><span class="sxs-lookup"><span data-stu-id="77382-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="77382-106">Suporte de plataforma cruzada</span><span class="sxs-lookup"><span data-stu-id="77382-106">Cross-Platform support</span></span>
* <span data-ttu-id="77382-107">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="77382-107">Performance improvements</span></span>
* <span data-ttu-id="77382-108">Pequenos aperfeiçoamentos de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="77382-108">Minor UI improvements</span></span>

<span data-ttu-id="77382-109">Os seguintes recursos estão disponíveis neste RC, com mais planejado para a versão final 3.4.</span><span class="sxs-lookup"><span data-stu-id="77382-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="77382-110">Novos recursos</span><span class="sxs-lookup"><span data-stu-id="77382-110">New Features</span></span>

* <span data-ttu-id="77382-111">Os clientes do NuGet agora dão suporte a codificação de conteúdo gzip de repositórios</span><span class="sxs-lookup"><span data-stu-id="77382-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="77382-112">Suporte para PDBs de pacotes em projetos xproj</span><span class="sxs-lookup"><span data-stu-id="77382-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="77382-113">Suporte para iOS e ações de build do Android no elemento contentFiles</span><span class="sxs-lookup"><span data-stu-id="77382-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="77382-114">Suporte para o netstandard e netstandardapp monikers de estrutura</span><span class="sxs-lookup"><span data-stu-id="77382-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="77382-115">Novos recursos de Interface do usuário</span><span class="sxs-lookup"><span data-stu-id="77382-115">New User Interface Features</span></span>

* <span data-ttu-id="77382-116">Melhorias de desempenho significativas, especialmente nas guias instalado, as atualizações e consolidar</span><span class="sxs-lookup"><span data-stu-id="77382-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="77382-117">Instalado e guias de atualizações agora estão classificadas em ordem alfabética</span><span class="sxs-lookup"><span data-stu-id="77382-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="77382-118">Adicionado um botão de atualização que permite que uma pesquisa a ser atualizado</span><span class="sxs-lookup"><span data-stu-id="77382-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="77382-119">Atualizações e aprimoramentos</span><span class="sxs-lookup"><span data-stu-id="77382-119">Updates and Improvements</span></span>

* <span data-ttu-id="77382-120">Pacotes referenciados no `project.json` que têm um flutuante versão não será atualizada em cada compilação.</span><span class="sxs-lookup"><span data-stu-id="77382-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="77382-121">Em vez disso, eles serão atualizados somente quando forçado a restaurar, limpar, recompilar ou modificar `project.json`.</span><span class="sxs-lookup"><span data-stu-id="77382-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="77382-122">origens de repositório de NuGet.org não são forçadas em uma configuração de projeto quando você usa a interface do usuário de configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="77382-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="77382-123">Não há mais o NuGet restaura pacotes em projetos compartilhados nem grava um arquivo de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="77382-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="77382-124">Nós aprimoramos falha de rede e tente novamente o tratamento para servidores inacessíveis ou lento para responder.</span><span class="sxs-lookup"><span data-stu-id="77382-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="77382-125">Comportamentos de teclado e mouse estão aprimorados na UI do Gerenciador de pacotes do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="77382-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="77382-126">Agora, damos suporte a versão mais recente `project.json` esquema em DNX.</span><span class="sxs-lookup"><span data-stu-id="77382-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="77382-127">Problemas Conhecidos</span><span class="sxs-lookup"><span data-stu-id="77382-127">Known Issues</span></span>

<span data-ttu-id="77382-128">Continuamos a acompanhar os problemas em nossa lista de problemas do GitHub que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="77382-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>