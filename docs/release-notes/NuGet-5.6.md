---
title: Notas de versão do NuGet 5,6
description: Notas de versão do NuGet 5,6, incluindo novos recursos, correções de bugs e DCRs.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727817"
---
# <a name="nuget-56-release-notes"></a><span data-ttu-id="509af-103">Notas de versão do NuGet 5,6</span><span class="sxs-lookup"><span data-stu-id="509af-103">NuGet 5.6 Release Notes</span></span>

<span data-ttu-id="509af-104">Veículos de distribuição do NuGet:</span><span class="sxs-lookup"><span data-stu-id="509af-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="509af-105">Versão do NuGet</span><span class="sxs-lookup"><span data-stu-id="509af-105">NuGet version</span></span> | <span data-ttu-id="509af-106">Disponível na versão do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="509af-106">Available in Visual Studio version</span></span>| <span data-ttu-id="509af-107">Disponível em SDKs do .NET</span><span class="sxs-lookup"><span data-stu-id="509af-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="509af-108">**5.6.0**</span><span class="sxs-lookup"><span data-stu-id="509af-108">**5.6.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="509af-109">Visual Studio 2019 versão 16,6</span><span class="sxs-lookup"><span data-stu-id="509af-109">Visual Studio 2019 version 16.6</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="509af-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="509af-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="509af-111"><sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core</span><span class="sxs-lookup"><span data-stu-id="509af-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-56"></a><span data-ttu-id="509af-112">Resumo: o que há de novo no 5,6</span><span class="sxs-lookup"><span data-stu-id="509af-112">Summary: What's New in 5.6</span></span>

* <span data-ttu-id="509af-113">Suporte a pacotes de pré-lançamento com versões flutuantes.</span><span class="sxs-lookup"><span data-stu-id="509af-113">Support prerelease packages with floating versions.</span></span> <span data-ttu-id="509af-114">`Version="*-*"`, `Version="1.*-*"` e float semelhante às versões mais recentes, incluindo versões de pré-lançamento, dentro do intervalo especificado- [#912](https://github.com/NuGet/Home/issues/912)</span><span class="sxs-lookup"><span data-stu-id="509af-114">`Version="*-*"`, `Version="1.*-*"`, and similar float to latest versions, including prerelease versions, within specified range  - [#912](https://github.com/NuGet/Home/issues/912)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="509af-115">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="509af-115">Issues fixed in this release</span></span>

<span data-ttu-id="509af-116">**Soluciona**</span><span class="sxs-lookup"><span data-stu-id="509af-116">**Bugs:**</span></span>

* <span data-ttu-id="509af-117">`nuget push *.nupkg`falha quando snupkg não existe- [#8148](https://github.com/NuGet/Home/issues/8148)</span><span class="sxs-lookup"><span data-stu-id="509af-117">`nuget push *.nupkg` fails when snupkg does not exist - [#8148](https://github.com/NuGet/Home/issues/8148)</span></span>

* <span data-ttu-id="509af-118">Pack, e vários outros caminhos de código, falham dependendo da localidade.</span><span class="sxs-lookup"><span data-stu-id="509af-118">Pack, and several other code paths, fail dependent on locale.</span></span> <span data-ttu-id="509af-119">Usar RegexOptions. CultureInvariant- [#8246](https://github.com/NuGet/Home/issues/8246)</span><span class="sxs-lookup"><span data-stu-id="509af-119">Use RegexOptions.CultureInvariant - [#8246](https://github.com/NuGet/Home/issues/8246)</span></span>

* <span data-ttu-id="509af-120">Perf: a especificação de DG para cenários de projetos descarregados não deve ser escrita em restaurações de visualização- [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="509af-120">Perf: DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="509af-121">Restauração: melhorar o desempenho ao armazenar em cache a especificação do grafo de dependência de solução- [#9201](https://github.com/NuGet/Home/issues/9201)</span><span class="sxs-lookup"><span data-stu-id="509af-121">Restore: Improve performance by caching solution dependency graph spec - [#9201](https://github.com/NuGet/Home/issues/9201)</span></span>

* <span data-ttu-id="509af-122">A interface do usuário do PM não funciona para projetos de estilo do SDK após a instalação de um pacote com o console PM- [#9203](https://github.com/NuGet/Home/issues/9203)</span><span class="sxs-lookup"><span data-stu-id="509af-122">PM UI doesn't work for SDK style projects after installing a package with PM Console - [#9203](https://github.com/NuGet/Home/issues/9203)</span></span>

* <span data-ttu-id="509af-123">O ícone inserido não pode ser mostrado na interface do usuário do PM com feed de pacote local-dependendo de/vs \ [#9225](https://github.com/NuGet/Home/issues/9225)</span><span class="sxs-lookup"><span data-stu-id="509af-123">Embedded icon can’t be shown in PM UI with local package feed - depending on / vs \ - [#9225](https://github.com/NuGet/Home/issues/9225)</span></span>

* <span data-ttu-id="509af-124">NuGetVersion. TryParseStrict () deverá retornar false se falhar ao analisar- [#9255](https://github.com/NuGet/Home/issues/9255)</span><span class="sxs-lookup"><span data-stu-id="509af-124">NuGetVersion.TryParseStrict() should return false if it fails to parse - [#9255](https://github.com/NuGet/Home/issues/9255)</span></span>

* <span data-ttu-id="509af-125">`nuget.exe push`ajuda para `-source` , deve sugerir o uso do nome de origem, não da URL de origem- [#9265](https://github.com/NuGet/Home/issues/9265)</span><span class="sxs-lookup"><span data-stu-id="509af-125">`nuget.exe push` help for `-source`, should suggest usage of source name, not source URL - [#9265](https://github.com/NuGet/Home/issues/9265)</span></span>

* <span data-ttu-id="509af-126">`dotnet nuget add package SourceUri`Cria um nome de origem de pacote padrão inválido- [#9277](https://github.com/NuGet/Home/issues/9277)</span><span class="sxs-lookup"><span data-stu-id="509af-126">`dotnet nuget add package SourceUri`  creates bad default package source name - [#9277](https://github.com/NuGet/Home/issues/9277)</span></span>

* <span data-ttu-id="509af-127">O leitor de tela não anuncia "pesquisando..." mensagem ao alternar guias- [#9307](https://github.com/NuGet/Home/issues/9307)</span><span class="sxs-lookup"><span data-stu-id="509af-127">Screen reader doesn't announce "Searching..." message when switching tabs - [#9307](https://github.com/NuGet/Home/issues/9307)</span></span>

* <span data-ttu-id="509af-128">Acessibilidade: a cor do retângulo de foco não está acessível nas guias de interface do usuário do PM no tema escuro- [#9336](https://github.com/NuGet/Home/issues/9336)</span><span class="sxs-lookup"><span data-stu-id="509af-128">Accessibility: Focus-rectangle color is not accessible PM UI tabs in dark theme - [#9336](https://github.com/NuGet/Home/issues/9336)</span></span>

* <span data-ttu-id="509af-129">falha na restauração do NuGet. exe 5,5 com o MSBuild 14 ou inferior- [#9458](https://github.com/NuGet/Home/issues/9458)</span><span class="sxs-lookup"><span data-stu-id="509af-129">nuget.exe 5.5 fails to restore with MSBuild 14 or below - [#9458](https://github.com/NuGet/Home/issues/9458)</span></span>

* <span data-ttu-id="509af-130">Não registrar horas de milissegundos em mensagens de restauração- [#8977](https://github.com/NuGet/Home/issues/8977)</span><span class="sxs-lookup"><span data-stu-id="509af-130">Don't log millisecond times in restore messages - [#8977](https://github.com/NuGet/Home/issues/8977)</span></span>

* <span data-ttu-id="509af-131">Tornar IOutputConsole Async- [#9268](https://github.com/NuGet/Home/issues/9268)</span><span class="sxs-lookup"><span data-stu-id="509af-131">Make IOutputConsole async - [#9268](https://github.com/NuGet/Home/issues/9268)</span></span>

* <span data-ttu-id="509af-132">A seleção de versão do MSBuild funciona mal em algumas culturas que não estão em inglês – [#9322](https://github.com/NuGet/Home/issues/9322)</span><span class="sxs-lookup"><span data-stu-id="509af-132">MSBuild version picking works poorly on some non-english cultures - [#9322](https://github.com/NuGet/Home/issues/9322)</span></span>

* <span data-ttu-id="509af-133">Padrão de formato ausente em `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)</span><span class="sxs-lookup"><span data-stu-id="509af-133">Missing format default on `dotnet nuget list source` - [#9337](https://github.com/NuGet/Home/issues/9337)</span></span>

* <span data-ttu-id="509af-134">Perf: RestoreOperationLogger tem afinidade de thread desnecessária- [#9288](https://github.com/NuGet/Home/issues/9288)</span><span class="sxs-lookup"><span data-stu-id="509af-134">Perf: RestoreOperationLogger has unnecessary thread affinity - [#9288](https://github.com/NuGet/Home/issues/9288)</span></span>

* <span data-ttu-id="509af-135">Criação automatizada de documentos para `dotnet nuget` comandos – [#9146](https://github.com/NuGet/Home/issues/9146)</span><span class="sxs-lookup"><span data-stu-id="509af-135">Automated creation of docs for `dotnet nuget` commands - [#9146](https://github.com/NuGet/Home/issues/9146)</span></span>

* <span data-ttu-id="509af-136">O detalhamento padrão não deve relatar a restauração de NOOP de cada projeto- [#8792](https://github.com/NuGet/Home/issues/8792)</span><span class="sxs-lookup"><span data-stu-id="509af-136">Default verbosity should not report each project's noop restore - [#8792](https://github.com/NuGet/Home/issues/8792)</span></span>

* <span data-ttu-id="509af-137">`-DependencyVersion`Parâmetro de suporte para `NuGet.exe update` , semelhante ao comando de instalação [#7694](https://github.com/NuGet/Home/issues/7694)</span><span class="sxs-lookup"><span data-stu-id="509af-137">Support `-DependencyVersion` parameter for `NuGet.exe update`, similar to install command - [#7694](https://github.com/NuGet/Home/issues/7694)</span></span>


<span data-ttu-id="509af-138">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="509af-138">**DCRs:**</span></span>

* <span data-ttu-id="509af-139">Adicionar suporte inicial à estrutura de destino do NET 5.0- [#9584](https://github.com/NuGet/Home/issues/9584)</span><span class="sxs-lookup"><span data-stu-id="509af-139">Add initial support for net5.0 target framework - [#9584](https://github.com/NuGet/Home/issues/9584)</span></span>

* <span data-ttu-id="509af-140">Classificar pacotes por ID na guia Atualizações da interface do usuário do PM- [#9278](https://github.com/NuGet/Home/issues/9278)</span><span class="sxs-lookup"><span data-stu-id="509af-140">Sort packages by ID in the Updates tab of the PM UI - [#9278](https://github.com/NuGet/Home/issues/9278)</span></span>


<span data-ttu-id="509af-141">**[Lista de todos os problemas corrigidos nesta versão-5,6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span><span class="sxs-lookup"><span data-stu-id="509af-141">**[List of all issues fixed in this release - 5.6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span></span>
