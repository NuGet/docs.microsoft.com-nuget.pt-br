---
title: Notas de versão 3.4 do NuGet
description: Notas de versão do NuGet 3.4, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551185"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="bee21-103">Notas de versão 3.4 do NuGet</span><span class="sxs-lookup"><span data-stu-id="bee21-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="bee21-104">[Notas de versão do RC 3.4 do NuGet](../release-notes/nuget-3.4-RC.md) | [notas de versão do NuGet 3.4.1](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="bee21-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="bee21-105">NuGet 3.4 foi lançado em 30 de março de 2016 como parte do Visual Studio 2015 atualização 2 e versão de visualização do Visual Studio 15 e foi criado com alguns princípios em mente:</span><span class="sxs-lookup"><span data-stu-id="bee21-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="bee21-106">Suporte de plataforma cruzada</span><span class="sxs-lookup"><span data-stu-id="bee21-106">Cross-Platform support</span></span>
* <span data-ttu-id="bee21-107">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="bee21-107">Performance improvements</span></span>
* <span data-ttu-id="bee21-108">Pequenos aperfeiçoamentos de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="bee21-108">Minor UI improvements</span></span>

<span data-ttu-id="bee21-109">Os seguintes recursos foram adicionados anteriormente no RC e foram atualizados ou concluídos para a versão 3.4:</span><span class="sxs-lookup"><span data-stu-id="bee21-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="bee21-110">Novos recursos</span><span class="sxs-lookup"><span data-stu-id="bee21-110">New Features</span></span>

* <span data-ttu-id="bee21-111">Os clientes do NuGet agora dão suporte a codificação de conteúdo gzip de repositórios</span><span class="sxs-lookup"><span data-stu-id="bee21-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="bee21-112">Suporte para PDBs de pacotes em projetos xproj</span><span class="sxs-lookup"><span data-stu-id="bee21-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="bee21-113">Suporte para iOS e ações de build do Android no elemento contentFiles</span><span class="sxs-lookup"><span data-stu-id="bee21-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="bee21-114">Suporte para o netstandard e netstandardapp monikers de estrutura</span><span class="sxs-lookup"><span data-stu-id="bee21-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="bee21-115">Novos recursos de Interface do usuário</span><span class="sxs-lookup"><span data-stu-id="bee21-115">New User Interface Features</span></span>

* <span data-ttu-id="bee21-116">Melhorias de desempenho significativas, especialmente nas guias instalado, as atualizações e consolidar</span><span class="sxs-lookup"><span data-stu-id="bee21-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="bee21-117">Origem de 'Todas as origens de pacote' agregada está disponível com a mesclagem de resultados de pesquisa apropriada</span><span class="sxs-lookup"><span data-stu-id="bee21-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="bee21-118">Instalado e guias de atualizações agora estão classificadas em ordem alfabética</span><span class="sxs-lookup"><span data-stu-id="bee21-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="bee21-119">Adicionado um botão de atualização que permite que uma pesquisa a ser atualizado</span><span class="sxs-lookup"><span data-stu-id="bee21-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="bee21-120">Opções de Build mais recente na parte superior da lista de versão</span><span class="sxs-lookup"><span data-stu-id="bee21-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="bee21-121">Atualizações e aprimoramentos</span><span class="sxs-lookup"><span data-stu-id="bee21-121">Updates and Improvements</span></span>

* <span data-ttu-id="bee21-122">Pacotes referenciados no `project.json` que têm um flutuante versão não será atualizada em cada compilação.</span><span class="sxs-lookup"><span data-stu-id="bee21-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="bee21-123">Em vez disso, eles serão atualizados somente quando forçado a restaurar, limpar, recompilar ou modificar `project.json`.</span><span class="sxs-lookup"><span data-stu-id="bee21-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="bee21-124">origens de repositório de NuGet.org não são forçadas em uma configuração de projeto quando você usa a interface do usuário de configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="bee21-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="bee21-125">Não há mais o NuGet restaura pacotes em projetos compartilhados nem grava um arquivo de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="bee21-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="bee21-126">Nós aprimoramos falha de rede e tente novamente o tratamento para servidores inacessíveis ou lento para responder.</span><span class="sxs-lookup"><span data-stu-id="bee21-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="bee21-127">Comportamentos de teclado e mouse estão aprimorados na UI do Gerenciador de pacotes do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bee21-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="bee21-128">Agora, damos suporte a versão mais recente `project.json` esquema em DNX.</span><span class="sxs-lookup"><span data-stu-id="bee21-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="bee21-129">Alterações significativas</span><span class="sxs-lookup"><span data-stu-id="bee21-129">Breaking Changes</span></span>

* <span data-ttu-id="bee21-130">Números de versão do pacote agora são normalizados para o formato *principais*. *pequenas*. *patch*-*pré-lançamento* cada um dos principais, secundária e patch são tratados como inteiros e descartar quaisquer zeros à esquerda.</span><span class="sxs-lookup"><span data-stu-id="bee21-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="bee21-131">As informações de pré-lançamento são tratadas como uma cadeia de caracteres e nenhuma alteração será aplicada a ele.</span><span class="sxs-lookup"><span data-stu-id="bee21-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="bee21-132">Esses números são usados em consultas, os clientes do NuGet e a pesquisa fornecidos pelo serviço do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="bee21-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="bee21-133">Mais detalhes podem ser encontrados nos documentos do NuGet, sob [versões de pré-lançamento](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="bee21-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="bee21-134">Problemas Conhecidos</span><span class="sxs-lookup"><span data-stu-id="bee21-134">Known Issues</span></span>

* <span data-ttu-id="bee21-135">**Problema:** usuários do Windows 10 v1511 poderão enfrentar problemas ou até mesmo uma falha do Visual Studio com o Powershell no Visual Studio nos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="bee21-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="bee21-136">Instalar / desinstalar pacotes que tenham install.ps1 / scripts uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="bee21-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="bee21-137">Carregamento de projetos que têm um script init.ps1 causa (como o EntityFramework.)</span><span class="sxs-lookup"><span data-stu-id="bee21-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="bee21-138">Publicação de conteúdo da web</span><span class="sxs-lookup"><span data-stu-id="bee21-138">Publishing web content</span></span>

* <span data-ttu-id="bee21-139">**Solução alternativa:** Certifique-se de que a instalação do Windows 10 tem os patches mais recentes aplicados, expecially janeiro de 2016 (KB 3124263) ou uma atualização posterior.</span><span class="sxs-lookup"><span data-stu-id="bee21-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="bee21-140">Mais detalhes estão disponíveis em [problema do GitHub #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="bee21-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="bee21-141">**Problema:** os redirecionamentos de protocolo do NuGet v2 foram interrompidos.</span><span class="sxs-lookup"><span data-stu-id="bee21-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="bee21-142">Os repositórios NuGet personalizados que redirecionam solicitações para um host alternativo não consideram a solicitação de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="bee21-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="bee21-143">**Solução alternativa:** para contornar esse problema, configure o URI do repositório de pacote nas configurações para apontar para o local do servidor redirecionado.</span><span class="sxs-lookup"><span data-stu-id="bee21-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="bee21-144">Para obter mais informações, consulte [solicitação de recepção GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="bee21-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="bee21-145">Continuamos a acompanhar os problemas em nossa lista de problemas do GitHub que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="bee21-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>