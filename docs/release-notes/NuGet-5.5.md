---
title: Notas de versão do NuGet 5,5
description: Notas de versão do NuGet 5,5, incluindo novos recursos, correções de bugs e DCRs.
author: karann-msft
ms.author: karann
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0e8ab66c937058e84420bc3e3a5031cbc133aad7
ms.sourcegitcommit: 1a63a84da2719c8141823ac89a20bf507fd22b00
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80148293"
---
# <a name="nuget-55-release-notes"></a><span data-ttu-id="f3291-103">Notas de versão do NuGet 5,5</span><span class="sxs-lookup"><span data-stu-id="f3291-103">NuGet 5.5 Release Notes</span></span>

<span data-ttu-id="f3291-104">Veículos de distribuição do NuGet:</span><span class="sxs-lookup"><span data-stu-id="f3291-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="f3291-105">Versão do NuGet</span><span class="sxs-lookup"><span data-stu-id="f3291-105">NuGet version</span></span> | <span data-ttu-id="f3291-106">Disponível na versão do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f3291-106">Available in Visual Studio version</span></span>| <span data-ttu-id="f3291-107">Disponível em SDKs do .NET</span><span class="sxs-lookup"><span data-stu-id="f3291-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="f3291-108">**5.5.0**</span><span class="sxs-lookup"><span data-stu-id="f3291-108">**5.5.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="f3291-109">Visual Studio 2019 versão 16,5</span><span class="sxs-lookup"><span data-stu-id="f3291-109">Visual Studio 2019 version 16.5</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="f3291-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="f3291-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="f3291-111"><sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core</span><span class="sxs-lookup"><span data-stu-id="f3291-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-55"></a><span data-ttu-id="f3291-112">Resumo: o que há de novo no 5,5</span><span class="sxs-lookup"><span data-stu-id="f3291-112">Summary: What's New in 5.5</span></span>

* <span data-ttu-id="f3291-113">Experiência aprimorada de acessibilidade e leitor de tela para a interface do usuário do Gerenciador de pacotes NuGet no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f3291-113">Improved accessibility and screen reader experience for the NuGet package manager UI in Visual Studio</span></span>
    * <span data-ttu-id="f3291-114">Problemas de acessibilidade nas experiências do leitor de tela, altText ausente e nome acessível para a caixa de texto instalada, etc.,- [#9059](https://github.com/NuGet/Home/issues/9059)</span><span class="sxs-lookup"><span data-stu-id="f3291-114">Accessibility issues in Screen Reader experiences, missing altText and accessible name for Installed textbox, etc., - [#9059](https://github.com/NuGet/Home/issues/9059)</span></span>
    * <span data-ttu-id="f3291-115">Problemas de acessibilidade nas experiências do leitor de tela na lista de pacotes- [#9077](https://github.com/NuGet/Home/issues/9077)</span><span class="sxs-lookup"><span data-stu-id="f3291-115">Accessibility issues in Screen Reader experiences in Packages List - [#9077](https://github.com/NuGet/Home/issues/9077)</span></span>
    * <span data-ttu-id="f3291-116">Problemas de acessibilidade nas experiências do leitor de tela relacionadas às guias "procurar", "instalar", "atualizar"- [#9078](https://github.com/NuGet/Home/issues/9078)</span><span class="sxs-lookup"><span data-stu-id="f3291-116">Accessibility issues in Screen Reader experiences related to "browse","install","update" Tabs - [#9078](https://github.com/NuGet/Home/issues/9078)</span></span>
    * <span data-ttu-id="f3291-117">O Narrator não anuncia o rótulo de link "blank", "no Dependencies", "NuGet. org", "MIT" [#9157](https://github.com/NuGet/Home/issues/9157)</span><span class="sxs-lookup"><span data-stu-id="f3291-117">Narrator does not announce "Blank","No Dependencies","nuget.org","MIT" link label [#9157](https://github.com/NuGet/Home/issues/9157)</span></span>

* <span data-ttu-id="f3291-118">Suporte para ícones independentes do identificando na interface do usuário do Gerenciador de pacotes do Visual Studio para pacotes hospedados em feeds locais- [#8189](https://github.com/NuGet/Home/issues/8189)</span><span class="sxs-lookup"><span data-stu-id="f3291-118">Support for surfacing self-contained icons in Visual Studio package manager UI for packages hosted on local feeds - [#8189](https://github.com/NuGet/Home/issues/8189)</span></span>

* <span data-ttu-id="f3291-119">Desempenho de restauração não operacional significativamente melhorado usando `RestoreUseStaticGraphEvaluation` que acelera as avaliações chamando as APIs do grafo estático do MSBuild- [8791](https://github.com/NuGet/Home/issues/8791)</span><span class="sxs-lookup"><span data-stu-id="f3291-119">Significantly improved no-op restore performance using `RestoreUseStaticGraphEvaluation` which speeds up evaluations by calling MSBuild Static Graph APIs - [8791](https://github.com/NuGet/Home/issues/8791)</span></span>

* <span data-ttu-id="f3291-120">Confiabilidade do dotnet. exe aprimorada com plug-ins de autenticação entre plataformas</span><span class="sxs-lookup"><span data-stu-id="f3291-120">Improved dotnet.exe reliability with cross-platform authentication plugins</span></span>
    * <span data-ttu-id="f3291-121">dotnet restore falha com TaskCanceledException- [#7842](https://github.com/NuGet/Home/issues/7842)</span><span class="sxs-lookup"><span data-stu-id="f3291-121">dotnet restore failing with TaskCanceledException - [#7842](https://github.com/NuGet/Home/issues/7842)</span></span>
    * <span data-ttu-id="f3291-122">Plug-in: "uma tarefa foi cancelada"-problema com a autenticação ADO devido a isso.</span><span class="sxs-lookup"><span data-stu-id="f3291-122">Plugin:  "A task was cancelled" - problem with ADO authentication due to this.</span></span><span data-ttu-id="f3291-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span><span class="sxs-lookup"><span data-stu-id="f3291-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span></span>

* <span data-ttu-id="f3291-124">Adicionar `dotnet nuget <add|remove|update|disable|enable|list> source` comando- [#4126](https://github.com/NuGet/Home/issues/4126)</span><span class="sxs-lookup"><span data-stu-id="f3291-124">add `dotnet nuget <add|remove|update|disable|enable|list> source` command - [#4126](https://github.com/NuGet/Home/issues/4126)</span></span>

* <span data-ttu-id="f3291-125">Suporte para `--skip-duplicate` usando dotNet do NuGet Push- [#8778](https://github.com/NuGet/Home/issues/8778)</span><span class="sxs-lookup"><span data-stu-id="f3291-125">Suport for `--skip-duplicate`  using dotnet nuget push - [#8778](https://github.com/NuGet/Home/issues/8778)</span></span>

* <span data-ttu-id="f3291-126">Suporte a `packages.config` com o MSBuild/Restore- [#8506](https://github.com/NuGet/Home/issues/8506)</span><span class="sxs-lookup"><span data-stu-id="f3291-126">Support `packages.config` with msbuild /restore - [#8506](https://github.com/NuGet/Home/issues/8506)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="f3291-127">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="f3291-127">Issues fixed in this release</span></span>

<span data-ttu-id="f3291-128">**•s**</span><span class="sxs-lookup"><span data-stu-id="f3291-128">**Bugs**</span></span>

* <span data-ttu-id="f3291-129">Retrabalho de autoatendimento com APIs v3- [#4197](https://github.com/NuGet/Home/issues/4197)</span><span class="sxs-lookup"><span data-stu-id="f3291-129">Rework Self-Updater with V3 Apis - [#4197](https://github.com/NuGet/Home/issues/4197)</span></span>

* <span data-ttu-id="f3291-130">Versão de dependência de pacote incorreta se a versão de dependência do pacote estiver definida como ' \* '- [#6697](https://github.com/NuGet/Home/issues/6697)</span><span class="sxs-lookup"><span data-stu-id="f3291-130">Wrong package dependency version If package dependency version is set to '\*' - [#6697](https://github.com/NuGet/Home/issues/6697)</span></span>

* <span data-ttu-id="f3291-131">A mensagem de erro ErrorUnsafePackageEntry não está apontando para a origem do problema- [#7505](https://github.com/NuGet/Home/issues/7505)</span><span class="sxs-lookup"><span data-stu-id="f3291-131">ErrorUnsafePackageEntry error message is not pointing to source of problem - [#7505](https://github.com/NuGet/Home/issues/7505)</span></span>

* <span data-ttu-id="f3291-132">O arquivo de bloqueio não é respeitado nos cenários "\*"- [#8073](https://github.com/NuGet/Home/issues/8073)</span><span class="sxs-lookup"><span data-stu-id="f3291-132">Lock file is not honored in "\*" scenarios  - [#8073](https://github.com/NuGet/Home/issues/8073)</span></span>

* <span data-ttu-id="f3291-133">O NuGet. exe não é resolvido para a versão mais recente de um pacote ao usar \* no PackageReference (MSBuild/dotnet/VS Restore do)- [#8432](https://github.com/NuGet/Home/issues/8432)</span><span class="sxs-lookup"><span data-stu-id="f3291-133">NuGet.exe does not resolve to the latest version of a package when using \* in PackageReference (MSBuild/Dotnet/VS restore do) - [#8432](https://github.com/NuGet/Home/issues/8432)</span></span>

* <span data-ttu-id="f3291-134">pacote de lista dotnet com várias direcionamentos de projeto WPF- [#8463](https://github.com/NuGet/Home/issues/8463)</span><span class="sxs-lookup"><span data-stu-id="f3291-134">dotnet list package with multi targeting WPF project - [#8463](https://github.com/NuGet/Home/issues/8463)</span></span>

* <span data-ttu-id="f3291-135">Melhorar o ConcurrencyUtilities (reduzir o uso da CPU)- [#8653](https://github.com/NuGet/Home/issues/8653)</span><span class="sxs-lookup"><span data-stu-id="f3291-135">Improve ConcurrencyUtilities (reduce CPU usage) - [#8653](https://github.com/NuGet/Home/issues/8653)</span></span>

* <span data-ttu-id="f3291-136">A especificação de DG para cenários de projetos descarregados não deve ser escrita em restaurações de visualização- [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="f3291-136">DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="f3291-137">Os pacotes NuGet do Visual Studio (RestoreManagerPackage) precisam ser carregados automaticamente em eventos de compilação de solução- [#8796](https://github.com/NuGet/Home/issues/8796)</span><span class="sxs-lookup"><span data-stu-id="f3291-137">The Visual Studio NuGet packages (RestoreManagerPackage) needs to auto load on solution build events - [#8796](https://github.com/NuGet/Home/issues/8796)</span></span>

* <span data-ttu-id="f3291-138">Deadlock em VSSettings Init- [#8842](https://github.com/NuGet/Home/issues/8842)</span><span class="sxs-lookup"><span data-stu-id="f3291-138">Deadlock in VSSettings init - [#8842](https://github.com/NuGet/Home/issues/8842)</span></span>

* <span data-ttu-id="f3291-139">A caixa de ferramentas do VisualStudio não será populada a partir de um pacote NuGet se um projeto for colocado em uma pasta de solução- [#8868](https://github.com/NuGet/Home/issues/8868)</span><span class="sxs-lookup"><span data-stu-id="f3291-139">VisualStudio ToolBox is not populated from a NuGet package if a project is placed in a solution folder - [#8868](https://github.com/NuGet/Home/issues/8868)</span></span>

* <span data-ttu-id="f3291-140">VS: a restauração da solução falha perpétua devido a uma condição de corrida- [#8881](https://github.com/NuGet/Home/issues/8881)</span><span class="sxs-lookup"><span data-stu-id="f3291-140">VS:  solution restore perpetually fails due to race condition - [#8881](https://github.com/NuGet/Home/issues/8881)</span></span>

* <span data-ttu-id="f3291-141">Constante "carregando." na guia instalado e "pesquisando</span><span class="sxs-lookup"><span data-stu-id="f3291-141">Constant "loading.." on installed tab, and "searching</span></span> <term><span data-ttu-id="f3291-142">.. "na guia Atualizações – [#8890](https://github.com/NuGet/Home/issues/8890)</span><span class="sxs-lookup"><span data-stu-id="f3291-142">.." on updates tab - [#8890](https://github.com/NuGet/Home/issues/8890)</span></span>

* <span data-ttu-id="f3291-143">Ícones inseridos ausentes na interface do usuário do VS PM após o cache expirar- [#9069](https://github.com/NuGet/Home/issues/9069)</span><span class="sxs-lookup"><span data-stu-id="f3291-143">Missing Embedded Icons in VS PM UI after cache expires - [#9069](https://github.com/NuGet/Home/issues/9069)</span></span>

* <span data-ttu-id="f3291-144">Inicialização da interface do usuário do FireAndForget PM – [#9112](https://github.com/NuGet/Home/issues/9112)</span><span class="sxs-lookup"><span data-stu-id="f3291-144">FireAndForget PM UI startup - [#9112](https://github.com/NuGet/Home/issues/9112)</span></span>

* <span data-ttu-id="f3291-145">Restore: a implementação de IncludeExcludeFiles. Equals (...) está incorreta- [#9167](https://github.com/NuGet/Home/issues/9167)</span><span class="sxs-lookup"><span data-stu-id="f3291-145">Restore: IncludeExcludeFiles.Equals(...) implementation is incorrect - [#9167](https://github.com/NuGet/Home/issues/9167)</span></span>

* <span data-ttu-id="f3291-146">Restore: especificação. Clone () cria clones desiguais [#9211](https://github.com/NuGet/Home/issues/9211)</span><span class="sxs-lookup"><span data-stu-id="f3291-146">Restore: PackageSpec.Clone() creates unequal clone - [#9211](https://github.com/NuGet/Home/issues/9211)</span></span>

* <span data-ttu-id="f3291-147">Lista de erros mostrada embora "sempre mostrar Lista de Erros se a compilação for concluída com erros" não está marcada- [#8190](https://github.com/NuGet/Home/issues/8190)</span><span class="sxs-lookup"><span data-stu-id="f3291-147">Error list shown although "Always show Error List if build finishes with errors" is not checked - [#8190](https://github.com/NuGet/Home/issues/8190)</span></span>

* <span data-ttu-id="f3291-148">A restauração estática do grafo não deve passar SolutionPath vazio- [#9061](https://github.com/NuGet/Home/issues/9061)</span><span class="sxs-lookup"><span data-stu-id="f3291-148">Static Graph restore should not pass empty SolutionPath - [#9061](https://github.com/NuGet/Home/issues/9061)</span></span>

* <span data-ttu-id="f3291-149">Restore: fechamento calculado para cada projeto 4 vezes- [#9042](https://github.com/NuGet/Home/issues/9042)</span><span class="sxs-lookup"><span data-stu-id="f3291-149">Restore: closure computed for each project 4 times - [#9042](https://github.com/NuGet/Home/issues/9042)</span></span>

* <span data-ttu-id="f3291-150">Restore: DependencyGraphSpec. Load (...) não precisa de JObject- [#9040](https://github.com/NuGet/Home/issues/9040)</span><span class="sxs-lookup"><span data-stu-id="f3291-150">Restore: DependencyGraphSpec.Load(...) does not need JObject - [#9040](https://github.com/NuGet/Home/issues/9040)</span></span>

* <span data-ttu-id="f3291-151">Restore: cadeias de caracteres grandes criadas em LOH (Large Object heap)- [#9031](https://github.com/NuGet/Home/issues/9031)</span><span class="sxs-lookup"><span data-stu-id="f3291-151">Restore: large strings created on large object heap (LOH) - [#9031](https://github.com/NuGet/Home/issues/9031)</span></span>

* <span data-ttu-id="f3291-152">O NuGet. exe personalizado no mono mais recente pode falhar devido ao resolvedor do SDK do MSBuild- [8848](https://github.com/NuGet/Home/issues/8848)</span><span class="sxs-lookup"><span data-stu-id="f3291-152">Custom nuget.exe on newer mono might break due to the MSBuild SDK Resolver - [8848](https://github.com/NuGet/Home/issues/8848)</span></span>

* <span data-ttu-id="f3291-153">a restauração falha quando NuGet. dgspec. JSON é "usado por outro processo"- [8692](https://github.com/NuGet/Home/issues/8692)</span><span class="sxs-lookup"><span data-stu-id="f3291-153">restore fails when nuget.dgspec.json is "used by another process" - [8692](https://github.com/NuGet/Home/issues/8692)</span></span>

<span data-ttu-id="f3291-154">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="f3291-154">**DCRs**</span></span>

* <span data-ttu-id="f3291-155">A lógica no _GetRestoreProjectStyle deve estar em uma tarefa- [#8804](https://github.com/NuGet/Home/issues/8804)</span><span class="sxs-lookup"><span data-stu-id="f3291-155">Logic in _GetRestoreProjectStyle should be in a task - [#8804](https://github.com/NuGet/Home/issues/8804)</span></span>

* <span data-ttu-id="f3291-156">Adicionar informações de reprovação por padrão na guia instalada- [#8541](https://github.com/NuGet/Home/issues/8541)</span><span class="sxs-lookup"><span data-stu-id="f3291-156">Add deprecation information by default on the installed tab - [#8541](https://github.com/NuGet/Home/issues/8541)</span></span>

<span data-ttu-id="f3291-157">**[Lista de todos os problemas corrigidos nesta versão-5,5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span><span class="sxs-lookup"><span data-stu-id="f3291-157">**[List of all issues fixed in this release - 5.5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span></span>
