---
title: Notas de Versão do NuGet 4.5 RTM
description: Notas de versão do NuGet 4.5 RTM incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 321aedb471bc6f86e9c03878093b199267e31195
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432498"
---
# <a name="nuget-45-release-notes"></a><span data-ttu-id="6e2e1-103">Notas sobre a versão do NuGet 4.5</span><span class="sxs-lookup"><span data-stu-id="6e2e1-103">NuGet 4.5 Release Notes</span></span>

<span data-ttu-id="6e2e1-104">O [Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) vem com o [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="6e2e1-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-450"></a><span data-ttu-id="6e2e1-105">Resumo: Novidades na versão 4.5.0</span><span class="sxs-lookup"><span data-stu-id="6e2e1-105">Summary: What's New in 4.5.0</span></span>

## <a name="summary-whats-new-in-452"></a><span data-ttu-id="6e2e1-106">Resumo: Novidades na versão 4.5.2</span><span class="sxs-lookup"><span data-stu-id="6e2e1-106">Summary: What's New in 4.5.2</span></span>

* <span data-ttu-id="6e2e1-107">Correção de segurança: Permissões em arquivos criados dentro de ~/.nuget são muito abertas [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-453"></a><span data-ttu-id="6e2e1-108">Resumo: Novidades na versão 4.5.3</span><span class="sxs-lookup"><span data-stu-id="6e2e1-108">Summary: What's New in 4.5.3</span></span>

* <span data-ttu-id="6e2e1-109">Correção de segurança: Arquivos dentro de NUPKGs podem ter um caminho relativo acima do diretório NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="6e2e1-110">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="6e2e1-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="6e2e1-111">Problemas com o .NET Standard 2.0 com o .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="6e2e1-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="6e2e1-112">O .NET Standard e suas ferramentas foram projetados de modo que os projetos destinados ao .NET Framework 4.6.1 podem consumir pacotes do NuGet e projetos destinados ao .NET Standard 2.0 ou anterior.</span><span class="sxs-lookup"><span data-stu-id="6e2e1-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="6e2e1-113">[Este documento](https://github.com/dotnet/standard/issues/481) resume os problemas desse cenário, o plano para lidar com eles e soluções alternativas que você pode implantar com o estado atual das ferramentas.</span><span class="sxs-lookup"><span data-stu-id="6e2e1-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="6e2e1-114">Você não consegue exibir, adicionar ou atualizar o DotNetCLITools usando o Gerenciador de Pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="6e2e1-114">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="6e2e1-115">Problema</span><span class="sxs-lookup"><span data-stu-id="6e2e1-115">Issue</span></span>

<span data-ttu-id="6e2e1-116">O Gerenciador de Pacotes do NuGet não exibe nem permite a adição/atualização de DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="6e2e1-116">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="6e2e1-117">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="6e2e1-117">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="6e2e1-118">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="6e2e1-118">Workaround</span></span>

<span data-ttu-id="6e2e1-119">O DotNetCLIToolReferences deve ser editado manualmente no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="6e2e1-119">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="6e2e1-120">Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto</span><span class="sxs-lookup"><span data-stu-id="6e2e1-120">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="6e2e1-121">Problema</span><span class="sxs-lookup"><span data-stu-id="6e2e1-121">Issue</span></span>

<span data-ttu-id="6e2e1-122">Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6e2e1-122">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="6e2e1-123">Isso acontece quando você está usando PackageReferences como o formato do gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="6e2e1-123">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="6e2e1-124">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="6e2e1-124">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="6e2e1-125">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="6e2e1-125">Workaround</span></span>

<span data-ttu-id="6e2e1-126">Faça uma restauração manual.</span><span class="sxs-lookup"><span data-stu-id="6e2e1-126">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="6e2e1-127">Um pacote em um projeto do .NET Core que contém um assembly com uma assinatura inválida pode disparar um loop de restauração infinito</span><span class="sxs-lookup"><span data-stu-id="6e2e1-127">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="6e2e1-128">Problema</span><span class="sxs-lookup"><span data-stu-id="6e2e1-128">Issue</span></span>

<span data-ttu-id="6e2e1-129">Às vezes, quando você usa um pacote que contém um assembly com uma assinatura inválida ou quando a versão do pacote é definida com o ticker 'DateTime', isso faz com que a restauração automática de pacotes seja executada em loop infinito [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span><span class="sxs-lookup"><span data-stu-id="6e2e1-129">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="6e2e1-130">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="6e2e1-130">Workaround</span></span>

<span data-ttu-id="6e2e1-131">Não há nenhuma solução alternativa no momento.</span><span class="sxs-lookup"><span data-stu-id="6e2e1-131">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="6e2e1-132">Problemas corrigidos no período de tempo do NuGet 4.5 RTM</span><span class="sxs-lookup"><span data-stu-id="6e2e1-132">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="6e2e1-133">Para problemas corrigidos no NuGet 4.4 RTM, consulte as [Notas de Versão do NuGet 4.4 RTM](../release-notes/nuget-4.4-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-133">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="6e2e1-134">Recursos</span><span class="sxs-lookup"><span data-stu-id="6e2e1-134">Features</span></span>

- <span data-ttu-id="6e2e1-135">Desabilitar push automático do pacote de símbolos – [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-135">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="6e2e1-136">Bugs</span><span class="sxs-lookup"><span data-stu-id="6e2e1-136">Bugs</span></span>

- <span data-ttu-id="6e2e1-137">[Regressão] em 15.5p1: Portable0.0 é ignorado – [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-137">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="6e2e1-138">Ativos de pacotes ausentes após a restauração – [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-138">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="6e2e1-139">Provedores de credenciais de plug-in não funcionam com URIs que contém espaços – [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-139">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="6e2e1-140">Em caso de falha ao restaurar o pacote, o erro deve ser impresso na saída mesmo com Detalhamento mínimo ATIVADO – [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-140">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="6e2e1-141">dotnet</span><span class="sxs-lookup"><span data-stu-id="6e2e1-141">dotnet</span></span>
  - <span data-ttu-id="6e2e1-142">dotnetcore restore no nível da solução não segue a ProjectReference com ReferenceOutputAssembly falso, levando a falhas de build aleatórias – [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-142">dotnetcore restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="6e2e1-143">Preenchimento automático em PMC funciona incorretamente com métodos de objeto – [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-143">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="6e2e1-144">A restauração do nuget.exe falha com o conjunto de ferramentas do Visual Studio 2015 – [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-144">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="6e2e1-145">perf – pmc é caro para ser instanciado no vs2017 – [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-145">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="6e2e1-146">Lentidão para obter informações de dependência em uma conexão lenta – [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-146">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="6e2e1-147">uninstall-package com -RemoveDependencies falhará se vários pacotes compartilharem uma dependência comum – [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-147">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="6e2e1-148">Finalizar NuGet.Core.nupkg para publicação – [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-148">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="6e2e1-149">O pacote do NuGet resolve a ID de dependência do nome de diretório quando -IncludeProjectReferences é usado para csproj + project.json – [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-149">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="6e2e1-150">O inicializador de tipo para 'NuGet.ProxyCache' gerou uma exceção – [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-150">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="6e2e1-151">Problema de desempenho de restauração do nuget com kudu – [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-151">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="6e2e1-152">O cliente da interface do usuário falha ao mostrar qualquer erro ou aviso quando a pesquisa está à frente de blobs do Registro – [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-152">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="6e2e1-153">Get-Packages – Atualizações geram uma consulta incorreta – [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="6e2e1-153">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="6e2e1-154">Links para problemas do GitHub corrigidos no RTM 4.5</span><span class="sxs-lookup"><span data-stu-id="6e2e1-154">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="6e2e1-155">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="6e2e1-155">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
