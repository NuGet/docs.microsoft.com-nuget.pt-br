---
title: Notas de versão do NuGet 3,4
description: Notas de versão do NuGet 3,4 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776417"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="0b317-103">Notas de versão do NuGet 3,4</span><span class="sxs-lookup"><span data-stu-id="0b317-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="0b317-104">Notas de versão do [NuGet 3,4-RC](../release-notes/nuget-3.4-RC.md)  |  [Notas de versão do NuGet 3.4.1](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="0b317-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="0b317-105">O NuGet 3,4 foi lançado em 30 de março de 2016 como parte do Visual Studio 2015 atualização 2 e da versão de visualização do Visual Studio 15 e foi criado com algumas filosofias nas mentes:</span><span class="sxs-lookup"><span data-stu-id="0b317-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="0b317-106">Suporte de plataforma cruzada</span><span class="sxs-lookup"><span data-stu-id="0b317-106">Cross-Platform support</span></span>
* <span data-ttu-id="0b317-107">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="0b317-107">Performance improvements</span></span>
* <span data-ttu-id="0b317-108">Melhorias secundárias da interface do usuário</span><span class="sxs-lookup"><span data-stu-id="0b317-108">Minor UI improvements</span></span>

<span data-ttu-id="0b317-109">Os seguintes recursos foram adicionados anteriormente no RC e foram atualizados ou concluídos para a versão 3,4:</span><span class="sxs-lookup"><span data-stu-id="0b317-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="0b317-110">Novos recursos</span><span class="sxs-lookup"><span data-stu-id="0b317-110">New Features</span></span>

* <span data-ttu-id="0b317-111">Os clientes NuGet agora dão suporte à codificação de conteúdo gzip de repositórios</span><span class="sxs-lookup"><span data-stu-id="0b317-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="0b317-112">Suporte para PDBs de pacotes em projetos xproj</span><span class="sxs-lookup"><span data-stu-id="0b317-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="0b317-113">Suporte para ações de compilação do iOS e Android no elemento contentFiles</span><span class="sxs-lookup"><span data-stu-id="0b317-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="0b317-114">Suporte para os monikers do netstandard e do netstandardapp Framework</span><span class="sxs-lookup"><span data-stu-id="0b317-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="0b317-115">Novos recursos da interface do usuário</span><span class="sxs-lookup"><span data-stu-id="0b317-115">New User Interface Features</span></span>

* <span data-ttu-id="0b317-116">Melhorias significativas de desempenho, especialmente nas guias instalado, atualizações e consolidar</span><span class="sxs-lookup"><span data-stu-id="0b317-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="0b317-117">A origem ' todas as fontes de pacote ' agregada está disponível com a mesclagem apropriada de resultados de pesquisa</span><span class="sxs-lookup"><span data-stu-id="0b317-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="0b317-118">As guias instaladas e atualizadas agora são classificadas alfabeticamente</span><span class="sxs-lookup"><span data-stu-id="0b317-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="0b317-119">Adicionado um botão Atualizar que permite que uma pesquisa seja atualizada</span><span class="sxs-lookup"><span data-stu-id="0b317-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="0b317-120">Opções de Build mais recentes na parte superior da lista de versões</span><span class="sxs-lookup"><span data-stu-id="0b317-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="0b317-121">Atualizações e aprimoramentos</span><span class="sxs-lookup"><span data-stu-id="0b317-121">Updates and Improvements</span></span>

* <span data-ttu-id="0b317-122">Os pacotes referenciados no `project.json` que têm uma versão flutuante não serão atualizados em cada compilação.</span><span class="sxs-lookup"><span data-stu-id="0b317-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="0b317-123">Em vez disso, eles serão atualizados somente quando forçados a restaurar, limpar, recompilar ou modificar `project.json` .</span><span class="sxs-lookup"><span data-stu-id="0b317-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="0b317-124">as fontes de repositório nuget.org não são mais forçadas para uma configuração de projeto quando você usa a interface do usuário de configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="0b317-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="0b317-125">O NuGet não restaura mais os pacotes em projetos compartilhados nem grava um arquivo de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="0b317-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="0b317-126">Melhoramos a falha de rede e a manipulação de tentativas para servidores inacessíveis ou lentos para responder.</span><span class="sxs-lookup"><span data-stu-id="0b317-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="0b317-127">Os comportamentos de teclado e mouse são aprimorados na interface do usuário do Gerenciador de pacotes do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b317-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="0b317-128">Agora, damos suporte ao `project.json` esquema mais recente em DNX.</span><span class="sxs-lookup"><span data-stu-id="0b317-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="0b317-129">Alterações de quebra</span><span class="sxs-lookup"><span data-stu-id="0b317-129">Breaking Changes</span></span>

* <span data-ttu-id="0b317-130">Os números de versão do pacote agora são normalizados para o formato *principal*. *secundária*. *patch* - do *pré-lançamento*   Cada um dos principais, os menores e os patches são tratados como inteiros e descartam qualquer zero à esquerda.</span><span class="sxs-lookup"><span data-stu-id="0b317-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="0b317-131">As informações de pré-lançamento são tratadas como uma cadeia de caracteres e nenhuma alteração é aplicada a ela.</span><span class="sxs-lookup"><span data-stu-id="0b317-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="0b317-132">Esses números são usados em consultas pelos clientes do NuGet e pela pesquisa fornecida pelo serviço nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0b317-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="0b317-133">Mais detalhes podem ser encontrados nos documentos do NuGet em [versões de pré-lançamento](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="0b317-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="0b317-134">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="0b317-134">Known Issues</span></span>

* <span data-ttu-id="0b317-135">**Problema:** Os usuários do Windows 10 v1511 podem enfrentar problemas ou até mesmo uma falha do Visual Studio com o PowerShell no Visual Studio nos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="0b317-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="0b317-136">Instalando/desinstalando pacotes que têm scripts de install.ps1/uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="0b317-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="0b317-137">Carregando projetos que têm um script de init.ps1 (como o EntityFramework)</span><span class="sxs-lookup"><span data-stu-id="0b317-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="0b317-138">Publicando conteúdo da Web</span><span class="sxs-lookup"><span data-stu-id="0b317-138">Publishing web content</span></span>

* <span data-ttu-id="0b317-139">**Solução alternativa:** Verifique se a instalação do Windows 10 tem os patches mais recentes aplicados, expecially o 2016 de Janeiro (KB 3124263) ou uma atualização posterior.</span><span class="sxs-lookup"><span data-stu-id="0b317-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="0b317-140">Mais detalhes estão disponíveis no [problema do GitHub #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="0b317-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="0b317-141">**Problema:** os redirecionamentos de protocolo do NuGet v2 foram interrompidos.</span><span class="sxs-lookup"><span data-stu-id="0b317-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="0b317-142">Os repositórios NuGet personalizados que redirecionam solicitações para um host alternativo não consideram a solicitação de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="0b317-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="0b317-143">**Solução alternativa:**  Para contornar esse problema, configure o URI do repositório de pacotes em configurações para apontar para o local do servidor Redirecionado.</span><span class="sxs-lookup"><span data-stu-id="0b317-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="0b317-144">Para obter mais informações, consulte [solicitação pull do GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).</span><span class="sxs-lookup"><span data-stu-id="0b317-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="0b317-145">Continuamos a acompanhar problemas em nossa lista de problemas do GitHub, que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="0b317-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>