---
title: "Notas de Versão do NuGet 4.5 RTM | Microsoft Docs"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 12/4/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão do NuGet 4.5 RTM incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs."
keywords: "Notas de versão do NuGet 4.5 RTM, correções de bugs, problemas conhecidos, recursos adicionados, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: e4727d46812cbfeb2e7094ddf28bf4e738e8aeea
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-45-rtm-release-notes"></a><span data-ttu-id="eed61-104">Notas de Versão do NuGet 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="eed61-104">NuGet 4.5 RTM Release Notes</span></span>

<span data-ttu-id="eed61-105">O [Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) vem com o [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="eed61-105">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="known-issues"></a><span data-ttu-id="eed61-106">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="eed61-106">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="eed61-107">Problemas com o .NET Standard 2.0 com o .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="eed61-107">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="eed61-108">O .NET Standard e suas ferramentas foram projetados de modo que os projetos destinados ao .NET Framework 4.6.1 podem consumir pacotes do NuGet e projetos destinados ao .NET Standard 2.0 ou anterior.</span><span class="sxs-lookup"><span data-stu-id="eed61-108">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="eed61-109">[Este documento](https://github.com/dotnet/standard/issues/481) resume os problemas desse cenário, o plano para lidar com eles e soluções alternativas que você pode implantar com o estado atual das ferramentas.</span><span class="sxs-lookup"><span data-stu-id="eed61-109">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="eed61-110">Você não consegue exibir, adicionar ou atualizar o DotNetCLITools usando o Gerenciador de Pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="eed61-110">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="eed61-111">Problema</span><span class="sxs-lookup"><span data-stu-id="eed61-111">Issue</span></span>

<span data-ttu-id="eed61-112">O Gerenciador de Pacotes do NuGet não exibe nem permite a adição/atualização de DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="eed61-112">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="eed61-113">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="eed61-113">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="eed61-114">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="eed61-114">Workaround</span></span>

<span data-ttu-id="eed61-115">O DotNetCLIToolReferences deve ser editado manualmente no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="eed61-115">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="eed61-116">Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto</span><span class="sxs-lookup"><span data-stu-id="eed61-116">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="eed61-117">Problema</span><span class="sxs-lookup"><span data-stu-id="eed61-117">Issue</span></span>

<span data-ttu-id="eed61-118">Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eed61-118">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="eed61-119">Isso acontece quando você está usando PackageReferences como o formato do gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="eed61-119">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="eed61-120">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="eed61-120">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="eed61-121">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="eed61-121">Workaround</span></span>

<span data-ttu-id="eed61-122">Faça uma restauração manual.</span><span class="sxs-lookup"><span data-stu-id="eed61-122">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="eed61-123">Um pacote em um projeto do .NET Core que contém um assembly com uma assinatura inválida pode disparar um loop de restauração infinito</span><span class="sxs-lookup"><span data-stu-id="eed61-123">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="eed61-124">Problema</span><span class="sxs-lookup"><span data-stu-id="eed61-124">Issue</span></span>

<span data-ttu-id="eed61-125">Às vezes, quando você usa um pacote que contém um assembly com uma assinatura inválida ou quando a versão do pacote é definida com o ticker 'DateTime', isso faz com que a restauração automática de pacotes seja executada em loop infinito [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span><span class="sxs-lookup"><span data-stu-id="eed61-125">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="eed61-126">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="eed61-126">Workaround</span></span>

<span data-ttu-id="eed61-127">Não há nenhuma solução alternativa no momento.</span><span class="sxs-lookup"><span data-stu-id="eed61-127">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="eed61-128">Problemas corrigidos no período de tempo do NuGet 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="eed61-128">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="eed61-129">Para problemas corrigidos no NuGet 4.4 RTM, consulte as [Notas de Versão do NuGet 4.4 RTM](../release-notes/nuget-4.4-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="eed61-129">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="eed61-130">Recursos</span><span class="sxs-lookup"><span data-stu-id="eed61-130">Features</span></span>

- <span data-ttu-id="eed61-131">Desabilitar push automático do pacote de símbolos – [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="eed61-131">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="eed61-132">Bugs</span><span class="sxs-lookup"><span data-stu-id="eed61-132">Bugs</span></span>

- <span data-ttu-id="eed61-133">[Regressão] em 15.5p1: Portable0.0 é ignorado – [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="eed61-133">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="eed61-134">Ativos de pacotes ausentes após a restauração – [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="eed61-134">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="eed61-135">Provedores de credenciais de plug-in não funcionam com URIs que contém espaços – [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="eed61-135">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="eed61-136">Em caso de falha ao restaurar o pacote, o erro deve ser impresso na saída mesmo com Detalhamento mínimo ON – [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="eed61-136">If package failed to restore, error should be printed i the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="eed61-137">dotnet restore no nível da solução não segue ProjectReference com ReferenceOutputAssembly falso, levando a falhas de build aleatórias – [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="eed61-137">dotnet restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="eed61-138">Preenchimento automático em PMC funciona incorretamente com métodos de objeto – [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="eed61-138">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="eed61-139">A restauração do nuget.exe falha com o conjunto de ferramentas do Visual Studio 2015 – [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="eed61-139">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="eed61-140">perf – pmc é caro para ser instanciado no vs2017 – [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="eed61-140">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="eed61-141">Lentidão para obter informações de dependência em uma conexão lenta – [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="eed61-141">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="eed61-142">uninstall-package com -RemoveDependencies falhará se vários pacotes compartilharem uma dependência comum – [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="eed61-142">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="eed61-143">Finalizar NuGet.Core.nupkg para publicação – [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="eed61-143">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="eed61-144">O pacote do NuGet resolve a ID de dependência do nome de diretório quando -IncludeProjectReferences é usado para csproj + project.json – [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="eed61-144">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="eed61-145">O inicializador de tipo para 'NuGet.ProxyCache' gerou uma exceção – [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="eed61-145">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="eed61-146">Problema de desempenho de restauração do nuget com kudu – [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="eed61-146">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="eed61-147">O cliente da interface do usuário falha ao mostrar qualquer erro ou aviso quando a pesquisa está à frente de blobs do Registro – [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="eed61-147">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="eed61-148">Get-Packages – Atualizações geram uma consulta incorreta – [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="eed61-148">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="eed61-149">Links para problemas do GitHub corrigidos no RTM 4.5</span><span class="sxs-lookup"><span data-stu-id="eed61-149">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="eed61-150">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="eed61-150">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
