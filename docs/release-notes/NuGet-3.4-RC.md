---
title: Notas de versão 3.4 RC do NuGet
description: Notas de versão do NuGet 3.4 RC incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e40d685a5256fdfee818f0cc1f1bc352c698f3c2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820814"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="c9afd-103">Notas de versão 3.4 RC do NuGet</span><span class="sxs-lookup"><span data-stu-id="c9afd-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="c9afd-104">[Notas de versão do NuGet 3.3](../release-notes/nuget-3.3.md) | [notas de versão do NuGet 3.4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="c9afd-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="c9afd-105">NuGet 3.4-RC foi lançado 3 de março de 2016, junto com o Visual Studio 2015 atualização 2 RC e foi criado com alguns princípios em mente:</span><span class="sxs-lookup"><span data-stu-id="c9afd-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="c9afd-106">Suporte de plataforma cruzada</span><span class="sxs-lookup"><span data-stu-id="c9afd-106">Cross-Platform support</span></span>
* <span data-ttu-id="c9afd-107">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="c9afd-107">Performance improvements</span></span>
* <span data-ttu-id="c9afd-108">Pequenos aperfeiçoamentos de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="c9afd-108">Minor UI improvements</span></span>

<span data-ttu-id="c9afd-109">Os seguintes recursos estarão disponíveis neste RC, com mais planejada para a versão final 3.4.</span><span class="sxs-lookup"><span data-stu-id="c9afd-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="c9afd-110">Novos recursos</span><span class="sxs-lookup"><span data-stu-id="c9afd-110">New Features</span></span>

* <span data-ttu-id="c9afd-111">Os clientes do NuGet agora suportam a codificação de conteúdo gzip dos repositórios</span><span class="sxs-lookup"><span data-stu-id="c9afd-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="c9afd-112">Suporte para PDBs de pacotes em projetos xproj</span><span class="sxs-lookup"><span data-stu-id="c9afd-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="c9afd-113">Suporte para iOS e Android criar ações no elemento contentFiles</span><span class="sxs-lookup"><span data-stu-id="c9afd-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="c9afd-114">Suporte para os identificadores de netstandard e netstandardapp monikers framework</span><span class="sxs-lookup"><span data-stu-id="c9afd-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="c9afd-115">Novos recursos de Interface do usuário</span><span class="sxs-lookup"><span data-stu-id="c9afd-115">New User Interface Features</span></span>

* <span data-ttu-id="c9afd-116">Melhorias de desempenho significativas, especialmente nas guias instalados, atualizações e consolidar</span><span class="sxs-lookup"><span data-stu-id="c9afd-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="c9afd-117">Instalado e guias de atualizações agora são classificados em ordem alfabética</span><span class="sxs-lookup"><span data-stu-id="c9afd-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="c9afd-118">Adicionar um botão de atualização que permite que uma pesquisa a ser atualizado</span><span class="sxs-lookup"><span data-stu-id="c9afd-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="c9afd-119">Atualizações e aprimoramentos</span><span class="sxs-lookup"><span data-stu-id="c9afd-119">Updates and Improvements</span></span>

* <span data-ttu-id="c9afd-120">Pacotes referenciados em `project.json` que têm um flutuante versão não será atualizado em cada compilação.</span><span class="sxs-lookup"><span data-stu-id="c9afd-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="c9afd-121">Em vez disso, elas serão atualizadas somente quando forçada a restaurar, limpar, recriar ou modificar `project.json`.</span><span class="sxs-lookup"><span data-stu-id="c9afd-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="c9afd-122">origens de repositório NuGet.org não são forçadas em uma configuração de projeto quando você usa a configuração do NuGet da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="c9afd-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="c9afd-123">O NuGet não restaura pacotes em projetos compartilhados nem grava um arquivo de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="c9afd-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="c9afd-124">Nós já aprimorado falha de rede e tente novamente tratamento para servidores inacessíveis ou lento para responder.</span><span class="sxs-lookup"><span data-stu-id="c9afd-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="c9afd-125">Comportamentos de teclado e mouse são aprimorados na UI do Gerenciador de pacote do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c9afd-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="c9afd-126">Agora temos suporte para a versão mais recente `project.json` esquema DNX.</span><span class="sxs-lookup"><span data-stu-id="c9afd-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="c9afd-127">Problemas Conhecidos</span><span class="sxs-lookup"><span data-stu-id="c9afd-127">Known Issues</span></span>

<span data-ttu-id="c9afd-128">Continuamos a rastrear problemas em nossa lista de problemas do GitHub que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="c9afd-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>