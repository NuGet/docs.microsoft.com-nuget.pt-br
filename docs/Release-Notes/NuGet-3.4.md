---
title: "Notas de versão do NuGet 3.4 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 80a429f5-7569-4349-ad7f-4fe9218eac23
description: "Notas de versão do NuGet 3.4, incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão NuGet 3.4, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 911e4377ad9c8b1f865b0721f43ff73b62df6d1e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="b674f-104">Notas de versão 3.4 do NuGet</span><span class="sxs-lookup"><span data-stu-id="b674f-104">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="b674f-105">[Notas de versão 3.4 RC NuGet](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 notas de versão](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="b674f-105">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="b674f-106">NuGet 3.4 foi lançada em 30 de março de 2016 como parte do Visual Studio 2015 atualização 2 e versão de visualização do Visual Studio 15 e foi criado com alguns princípios em mente:</span><span class="sxs-lookup"><span data-stu-id="b674f-106">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

*  <span data-ttu-id="b674f-107">Suporte de plataforma cruzada</span><span class="sxs-lookup"><span data-stu-id="b674f-107">Cross-Platform support</span></span>
*  <span data-ttu-id="b674f-108">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="b674f-108">Performance improvements</span></span>
*  <span data-ttu-id="b674f-109">Pequenos aperfeiçoamentos de interface do usuário</span><span class="sxs-lookup"><span data-stu-id="b674f-109">Minor UI improvements</span></span>

<span data-ttu-id="b674f-110">Os seguintes recursos foram adicionados anteriormente no RC e foram atualizados ou concluídos para a versão 3.4:</span><span class="sxs-lookup"><span data-stu-id="b674f-110">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="b674f-111">Novos recursos</span><span class="sxs-lookup"><span data-stu-id="b674f-111">New Features</span></span>

* <span data-ttu-id="b674f-112">Os clientes do NuGet agora suportam a codificação de conteúdo gzip dos repositórios</span><span class="sxs-lookup"><span data-stu-id="b674f-112">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="b674f-113">Suporte para PDBs de pacotes em projetos xproj</span><span class="sxs-lookup"><span data-stu-id="b674f-113">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="b674f-114">Suporte para iOS e Android criar ações no elemento contentFiles</span><span class="sxs-lookup"><span data-stu-id="b674f-114">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="b674f-115">Suporte para os identificadores de netstandard e netstandardapp monikers framework</span><span class="sxs-lookup"><span data-stu-id="b674f-115">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="b674f-116">Novos recursos de Interface do usuário</span><span class="sxs-lookup"><span data-stu-id="b674f-116">New User Interface Features</span></span>

* <span data-ttu-id="b674f-117">Melhorias de desempenho significativas, especialmente nas guias instalados, atualizações e consolidar</span><span class="sxs-lookup"><span data-stu-id="b674f-117">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="b674f-118">Origem de agregação 'Todas as fontes de pacote' está disponível com a mesclagem de resultados de pesquisa apropriada</span><span class="sxs-lookup"><span data-stu-id="b674f-118">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="b674f-119">Instalado e guias de atualizações agora são classificados em ordem alfabética</span><span class="sxs-lookup"><span data-stu-id="b674f-119">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="b674f-120">Adicionar um botão de atualização que permite que uma pesquisa a ser atualizado</span><span class="sxs-lookup"><span data-stu-id="b674f-120">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="b674f-121">Opções de compilação mais recentes na parte superior da lista de versão</span><span class="sxs-lookup"><span data-stu-id="b674f-121">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="b674f-122">Atualizações e aprimoramentos</span><span class="sxs-lookup"><span data-stu-id="b674f-122">Updates and Improvements</span></span>

* <span data-ttu-id="b674f-123">Pacotes referenciados em `project.json` que têm um flutuante versão não será atualizado em cada compilação.</span><span class="sxs-lookup"><span data-stu-id="b674f-123">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="b674f-124">Em vez disso, elas serão atualizadas somente quando forçada a restaurar, limpar, recriar ou modificar `project.json`.</span><span class="sxs-lookup"><span data-stu-id="b674f-124">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="b674f-125">origens de repositório NuGet.org não são forçadas em uma configuração de projeto quando você usa a configuração do NuGet da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="b674f-125">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="b674f-126">O NuGet não restaura pacotes em projetos compartilhados nem grava um arquivo de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="b674f-126">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="b674f-127">Nós já aprimorado falha de rede e tente novamente tratamento para servidores inacessíveis ou lento para responder.</span><span class="sxs-lookup"><span data-stu-id="b674f-127">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="b674f-128">Comportamentos de teclado e mouse são aprimorados na UI do Gerenciador de pacote do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b674f-128">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="b674f-129">Agora temos suporte para a versão mais recente `project.json` esquema DNX.</span><span class="sxs-lookup"><span data-stu-id="b674f-129">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="b674f-130">Alterações significativas</span><span class="sxs-lookup"><span data-stu-id="b674f-130">Breaking Changes</span></span>

* <span data-ttu-id="b674f-131">Números de versão do pacote agora são normalizados para o formato *principais*. *pequenas*. *patch*-*pré-lançamento* cada um dos principais, secundária e patch são tratados como inteiros e descartar qualquer zeros à esquerda.</span><span class="sxs-lookup"><span data-stu-id="b674f-131">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="b674f-132">As informações de pré-lançamento são tratadas como uma cadeia de caracteres e nenhuma alteração será aplicada a ele.</span><span class="sxs-lookup"><span data-stu-id="b674f-132">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="b674f-133">Esses números são usados em consultas, os clientes do NuGet e a pesquisa fornecidos pelo serviço do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b674f-133">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="b674f-134">Mais detalhes podem ser encontrados em documentos do NuGet em [versões de pré-lançamento](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="b674f-134">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="b674f-135">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="b674f-135">Known Issues</span></span>

* <span data-ttu-id="b674f-136">**Problema:** Windows 10 v1511 usuários podem enfrentar problemas ou até mesmo uma falha Visual Studio com o Powershell no Visual Studio nos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="b674f-136">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="b674f-137">Instalar / desinstalar os pacotes que têm install.ps1 / uninstall.ps1 scripts</span><span class="sxs-lookup"><span data-stu-id="b674f-137">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="b674f-138">Carregando projetos com um script init.ps1 (como EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="b674f-138">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="b674f-139">Publicação de conteúdo da web</span><span class="sxs-lookup"><span data-stu-id="b674f-139">Publishing web content</span></span>

* <span data-ttu-id="b674f-140">**Solução alternativa:** Certifique-se de que a instalação do Windows 10 tem os patches mais recentes aplicados, expecially janeiro de 2016 (3124263 KB) ou uma atualização posterior.</span><span class="sxs-lookup"><span data-stu-id="b674f-140">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="b674f-141">Mais detalhes estão disponíveis em [problema do GitHub #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="b674f-141">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="b674f-142">**Problema:** os redirecionamentos de protocolo do NuGet v2 foram interrompidos.</span><span class="sxs-lookup"><span data-stu-id="b674f-142">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="b674f-143">Os repositórios NuGet personalizados que redirecionam solicitações para um host alternativo não consideram a solicitação de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="b674f-143">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="b674f-144">**Solução alternativa:** para contornar esse problema, configure o URI do repositório de pacote nas configurações para apontar para o local do servidor redirecionado.</span><span class="sxs-lookup"><span data-stu-id="b674f-144">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="b674f-145">Para obter mais informações, consulte [solicitação de recepção GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="b674f-145">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="b674f-146">Continuamos a rastrear problemas em nossa lista de problemas do GitHub que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="b674f-146">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>