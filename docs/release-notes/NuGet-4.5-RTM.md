---
title: Notas de Versão do NuGet 4.5 RTM
description: Notas de versão do NuGet 4.5 RTM incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 1d04c508d029a6d92bbd480fe3bd7dc14727970e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820710"
---
# <a name="nuget-45-rtm-release-notes"></a><span data-ttu-id="74249-103">Notas de Versão do NuGet 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="74249-103">NuGet 4.5 RTM Release Notes</span></span>

<span data-ttu-id="74249-104">O [Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) vem com o [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="74249-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="known-issues"></a><span data-ttu-id="74249-105">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="74249-105">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="74249-106">Problemas com o .NET Standard 2.0 com o .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="74249-106">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="74249-107">O .NET Standard e suas ferramentas foram projetados de modo que os projetos destinados ao .NET Framework 4.6.1 podem consumir pacotes do NuGet e projetos destinados ao .NET Standard 2.0 ou anterior.</span><span class="sxs-lookup"><span data-stu-id="74249-107">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="74249-108">[Este documento](https://github.com/dotnet/standard/issues/481) resume os problemas desse cenário, o plano para lidar com eles e soluções alternativas que você pode implantar com o estado atual das ferramentas.</span><span class="sxs-lookup"><span data-stu-id="74249-108">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="74249-109">Você não consegue exibir, adicionar ou atualizar o DotNetCLITools usando o Gerenciador de Pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="74249-109">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="74249-110">Problema</span><span class="sxs-lookup"><span data-stu-id="74249-110">Issue</span></span>

<span data-ttu-id="74249-111">O Gerenciador de Pacotes do NuGet não exibe nem permite a adição/atualização de DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="74249-111">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="74249-112">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="74249-112">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="74249-113">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="74249-113">Workaround</span></span>

<span data-ttu-id="74249-114">O DotNetCLIToolReferences deve ser editado manualmente no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="74249-114">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="74249-115">Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto</span><span class="sxs-lookup"><span data-stu-id="74249-115">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="74249-116">Problema</span><span class="sxs-lookup"><span data-stu-id="74249-116">Issue</span></span>

<span data-ttu-id="74249-117">Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="74249-117">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="74249-118">Isso acontece quando você está usando PackageReferences como o formato do gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="74249-118">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="74249-119">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="74249-119">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="74249-120">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="74249-120">Workaround</span></span>

<span data-ttu-id="74249-121">Faça uma restauração manual.</span><span class="sxs-lookup"><span data-stu-id="74249-121">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="74249-122">Um pacote em um projeto do .NET Core que contém um assembly com uma assinatura inválida pode disparar um loop de restauração infinito</span><span class="sxs-lookup"><span data-stu-id="74249-122">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="74249-123">Problema</span><span class="sxs-lookup"><span data-stu-id="74249-123">Issue</span></span>

<span data-ttu-id="74249-124">Às vezes, quando você usa um pacote que contém um assembly com uma assinatura inválida ou quando a versão do pacote é definida com o ticker 'DateTime', isso faz com que a restauração automática de pacotes seja executada em loop infinito [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span><span class="sxs-lookup"><span data-stu-id="74249-124">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="74249-125">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="74249-125">Workaround</span></span>

<span data-ttu-id="74249-126">Não há nenhuma solução alternativa no momento.</span><span class="sxs-lookup"><span data-stu-id="74249-126">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="74249-127">Problemas corrigidos no período de tempo do NuGet 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="74249-127">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="74249-128">Para problemas corrigidos no NuGet 4.4 RTM, consulte as [Notas de Versão do NuGet 4.4 RTM](../release-notes/nuget-4.4-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="74249-128">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="74249-129">Recursos</span><span class="sxs-lookup"><span data-stu-id="74249-129">Features</span></span>

- <span data-ttu-id="74249-130">Desabilitar push automático do pacote de símbolos – [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="74249-130">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="74249-131">Bugs</span><span class="sxs-lookup"><span data-stu-id="74249-131">Bugs</span></span>

- <span data-ttu-id="74249-132">[Regressão] em 15.5p1: Portable0.0 é ignorado – [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="74249-132">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="74249-133">Ativos de pacotes ausentes após a restauração – [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="74249-133">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="74249-134">Provedores de credenciais de plug-in não funcionam com URIs que contém espaços – [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="74249-134">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="74249-135">Em caso de falha ao restaurar o pacote, o erro deve ser impresso na saída mesmo com Detalhamento mínimo ATIVADO – [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="74249-135">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="74249-136">dotnet</span><span class="sxs-lookup"><span data-stu-id="74249-136">dotnet</span></span>
  - <span data-ttu-id="74249-137">dotnetcore restore no nível da solução não segue a ProjectReference com ReferenceOutputAssembly falso, levando a falhas de build aleatórias – [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="74249-137">dotnetcore restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="74249-138">Preenchimento automático em PMC funciona incorretamente com métodos de objeto – [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="74249-138">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="74249-139">A restauração do nuget.exe falha com o conjunto de ferramentas do Visual Studio 2015 – [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="74249-139">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="74249-140">perf – pmc é caro para ser instanciado no vs2017 – [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="74249-140">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="74249-141">Lentidão para obter informações de dependência em uma conexão lenta – [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="74249-141">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="74249-142">uninstall-package com -RemoveDependencies falhará se vários pacotes compartilharem uma dependência comum – [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="74249-142">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="74249-143">Finalizar NuGet.Core.nupkg para publicação – [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="74249-143">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="74249-144">O pacote do NuGet resolve a ID de dependência do nome de diretório quando -IncludeProjectReferences é usado para csproj + project.json – [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="74249-144">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="74249-145">O inicializador de tipo para 'NuGet.ProxyCache' gerou uma exceção – [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="74249-145">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="74249-146">Problema de desempenho de restauração do nuget com kudu – [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="74249-146">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="74249-147">O cliente da interface do usuário falha ao mostrar qualquer erro ou aviso quando a pesquisa está à frente de blobs do Registro – [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="74249-147">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="74249-148">Get-Packages – Atualizações geram uma consulta incorreta – [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="74249-148">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="74249-149">Links para problemas do GitHub corrigidos no RTM 4.5</span><span class="sxs-lookup"><span data-stu-id="74249-149">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="74249-150">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="74249-150">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
