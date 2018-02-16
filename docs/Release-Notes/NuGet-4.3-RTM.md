---
title: "Notas de Versão do NuGet 4.3 RTM | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão do NuGet 4.3 RTM incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs."
keywords: "Notas de versão do NuGet 4.3 RTM, correções de bugs, problemas conhecidos, recursos adicionados, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: a2b61d854f4a5f1490832dab9a272c3a13b56adf
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-43-rtm-release-notes"></a><span data-ttu-id="cc35f-104">Notas de Versão do NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="cc35f-104">NuGet 4.3 RTM Release Notes</span></span>

<span data-ttu-id="cc35f-105">O [Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) vem com o NuGet 4.3 RTM, que adiciona suporte para novos cenários como o .NET Standard 2.0/.NET Core 2.0, contém várias correções de qualidade e melhora o desempenho.</span><span class="sxs-lookup"><span data-stu-id="cc35f-105">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="cc35f-106">Esta versão também oferece várias melhorias, como suporte para Controle de versão semântico 2.0.0, integração do MSBuild de avisos e erros do NuGet e muito mais.</span><span class="sxs-lookup"><span data-stu-id="cc35f-106">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="cc35f-107">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="cc35f-107">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="cc35f-108">A restauração do NuGet pode tratar as origens de pacotes desabilitadas como habilitadas em alguns casos</span><span class="sxs-lookup"><span data-stu-id="cc35f-108">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="cc35f-109">Problema</span><span class="sxs-lookup"><span data-stu-id="cc35f-109">Issue</span></span>

<span data-ttu-id="cc35f-110">As seguintes técnicas de linha de comando de restauração tratam as origens de pacotes desabilitadas como habilitadas.</span><span class="sxs-lookup"><span data-stu-id="cc35f-110">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="cc35f-111">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="cc35f-111">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="cc35f-112">`dotnet restore` (com o dotnet.exe que acompanha o VS ou com o que vem com o SDK do NetCore 2.0.0)</span><span class="sxs-lookup"><span data-stu-id="cc35f-112">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="cc35f-113">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="cc35f-113">Workaround</span></span>

1. <span data-ttu-id="cc35f-114">Usar o Visual Studio (2017 15.3 ou posterior) ou o NuGet.exe (v4.3.0 ou posterior)</span><span class="sxs-lookup"><span data-stu-id="cc35f-114">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="cc35f-115">Exclua a fonte desabilitada e continue a usar o msbuild ou o dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="cc35f-115">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="cc35f-116">Para sua solução, você poderá usar "Limpar" no NuGet.config e, em seguida, definir as fontes necessárias para a solução.</span><span class="sxs-lookup"><span data-stu-id="cc35f-116">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="cc35f-117">Ao usar o Console do Gerenciador de Pacotes, talvez a tecla 'Enter' não funcione</span><span class="sxs-lookup"><span data-stu-id="cc35f-117">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="cc35f-118">Problema</span><span class="sxs-lookup"><span data-stu-id="cc35f-118">Issue</span></span>

<span data-ttu-id="cc35f-119">Às vezes, a tecla enter não funciona no Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="cc35f-119">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="cc35f-120">Se isso ocorrer, confira o progresso na correção e forneça informações úteis adicionais sobre as etapas de reprodução.</span><span class="sxs-lookup"><span data-stu-id="cc35f-120">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="cc35f-121">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="cc35f-121">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="cc35f-122">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="cc35f-122">Workaround</span></span>

<span data-ttu-id="cc35f-123">Reinicie o Visual Studio e abra o PMC antes de abrir a solução.</span><span class="sxs-lookup"><span data-stu-id="cc35f-123">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="cc35f-124">Como alternativa, experimente excluir o `project.lock.json` e restaurá-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="cc35f-124">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="cc35f-125">Você não consegue exibir, adicionar ou atualizar o DotNetCLITools usando o Gerenciador de Pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="cc35f-125">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="cc35f-126">Problema</span><span class="sxs-lookup"><span data-stu-id="cc35f-126">Issue</span></span>

<span data-ttu-id="cc35f-127">O Gerenciador de Pacotes do NuGet não exibe nem permite a adição/atualização de DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="cc35f-127">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="cc35f-128">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="cc35f-128">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="cc35f-129">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="cc35f-129">Workaround</span></span>

<span data-ttu-id="cc35f-130">O DotNetCLIToolReferences deve ser editado manualmente no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="cc35f-130">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="cc35f-131">Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto</span><span class="sxs-lookup"><span data-stu-id="cc35f-131">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="cc35f-132">Problema</span><span class="sxs-lookup"><span data-stu-id="cc35f-132">Issue</span></span>

<span data-ttu-id="cc35f-133">Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cc35f-133">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="cc35f-134">Isso acontece quando você está usando PackageReferences como o formato do gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="cc35f-134">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="cc35f-135">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="cc35f-135">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="cc35f-136">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="cc35f-136">Workaround</span></span>

<span data-ttu-id="cc35f-137">Faça uma restauração manual.</span><span class="sxs-lookup"><span data-stu-id="cc35f-137">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="cc35f-138">Problemas corrigidos no período de tempo do NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="cc35f-138">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="cc35f-139">[Notas de Versão do NuGet 4.0 RTM](../release-notes/nuget-4.0-RTM.md) – Lista todos os problemas corrigidos no NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="cc35f-139">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="cc35f-140">Recursos</span><span class="sxs-lookup"><span data-stu-id="cc35f-140">Features</span></span>

- <span data-ttu-id="cc35f-141">Melhorar o desempenho da restauração do NuGet – Implementar NoOp para restaurações de linha de comando e do VS – [#5080](https://github.com/NuGet/Home/issues/5080)</span><span class="sxs-lookup"><span data-stu-id="cc35f-141">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="cc35f-142">NET Core 2.0: a CLI do VS/Dotnet deve começar a usar a funcionalidade NuGet existente: pastas de FallBack – [#4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="cc35f-142">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="cc35f-143">NET Core 2.0: permitir que os usuários ignorem os avisos específicos de restauração (ou elevar para erro) – [#4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="cc35f-143">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="cc35f-144">NET Core 2.0: assemblies localizadas de CLI – [#4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="cc35f-144">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="cc35f-145">NET Core 2.0: registrar todos os avisos/erros no arquivo de ativos (incluindo PackageTargetFallback) – [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="cc35f-145">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="cc35f-146">Habilitar suporte a TFM: NetStandard2.0, Tizen – [#4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="cc35f-146">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="cc35f-147">Reduzir o número de projetos NuGet.Core e NuGet.Client (e, portanto, de DLLs) – [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="cc35f-147">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="cc35f-148">Adicionar capacidade de marcar avisos nuget como erros – [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="cc35f-148">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="cc35f-149">Bugs</span><span class="sxs-lookup"><span data-stu-id="cc35f-149">Bugs</span></span>

- <span data-ttu-id="cc35f-150">msbuild /t:pack falha, pois o parâmetro “DevelopmentDependency” é incompatível com a tarefa “PackTask” – [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="cc35f-150">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="cc35f-151">A estrutura do diretórios para arquivos de conteúdo nivelados se o separador de diretório do Windows não for adicionado ao final de PackagePath – [#4795](https://github.com/NuGet/Home/issues/4795)</span><span class="sxs-lookup"><span data-stu-id="cc35f-151">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="cc35f-152">Projetos netcore não são compatíveis com a configuração como developmentDependency – [#4694](https://github.com/NuGet/Home/issues/4694)</span><span class="sxs-lookup"><span data-stu-id="cc35f-152">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="cc35f-153">RestoreManagerPackage está sendo carregado de forma síncrona, o que bloqueou o thread de interface do usuário e VS em deadlock – [#4679](https://github.com/NuGet/Home/issues/4679)</span><span class="sxs-lookup"><span data-stu-id="cc35f-153">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="cc35f-154">dotnet Restore (e, portanto, /t:restore do msbuild) ignora projetos com uma dependência de projeto da solução explícita [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="cc35f-154">dotnet Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="cc35f-155">Se a solução tiver projectreferences que se referem ao mesmo projeto, mas com maiúsculas e minúsculas diferentes, a restauração poderá não funcionar.</span><span class="sxs-lookup"><span data-stu-id="cc35f-155">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="cc35f-156">Isso também afeta diferentes caminhos relativos, sem diferenciação de maiúsculas e minúsculas – [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="cc35f-156">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="cc35f-157">Executáveis restaurados de pacotes do NuGet não podem mais ser executados com o .NET Core 2.0 – [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="cc35f-157">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="cc35f-158">O NuGet.exe absorve detalhes da exceção ao analisar o arquivo da solução – [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="cc35f-158">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="cc35f-159">O pacote coloca os arquivos de conteúdo no local errado se ContentTargetFolders contiver um caminho que termina com '/' no Windows – [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="cc35f-159">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="cc35f-160">Não é possível restaurar um DotNetCliToolReference para um pacote de ferramentas voltado para o netcoreapp1.1 – [#4396](https://github.com/NuGet/Home/issues/4396)</span><span class="sxs-lookup"><span data-stu-id="cc35f-160">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="cc35f-161">A CLI de atualização do Nuget deixa a condição de versão do pacote antigo no arquivo de projeto (C++) – [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="cc35f-161">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="cc35f-162">DCRs</span><span class="sxs-lookup"><span data-stu-id="cc35f-162">DCRs</span></span>

- <span data-ttu-id="cc35f-163">Ler DotnetCliToolTargetFramework da indicação do CPS – [#5397](https://github.com/NuGet/Home/issues/5397)</span><span class="sxs-lookup"><span data-stu-id="cc35f-163">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="cc35f-164">A verificação de TPMinV deve funcionar para o pj estilo UWP – [#4763](https://github.com/NuGet/Home/issues/4763)</span><span class="sxs-lookup"><span data-stu-id="cc35f-164">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="cc35f-165">Melhorar a descrição da interface do usuário para pacotes AutoReferenced – [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="cc35f-165">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="cc35f-166">A restauração do NuGet está selecionando ativos de compilação da seção de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="cc35f-166">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="cc35f-167"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="cc35f-167"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="cc35f-168">Colocar o diagnóstico de dependência no arquivo de bloqueio – [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="cc35f-168">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="cc35f-169">Links para problemas do GitHub corrigidos no RTM 4.3</span><span class="sxs-lookup"><span data-stu-id="cc35f-169">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="cc35f-170">Lista de Problemas</span><span class="sxs-lookup"><span data-stu-id="cc35f-170">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
