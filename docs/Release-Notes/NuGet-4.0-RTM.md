---
title: Notas de Versão do NuGet 4.0 RC | Microsoft Docs
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Notas de versão do NuGet 4.0 RTM incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
keywords: Notas de versão do NuGet 4.0 RTM, correções de bugs, problemas conhecidos, recursos adicionados, DCRs
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 75ce757c209afd74f8d4f45d58d4e13a23b3b743
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-40-rtm-release-notes"></a><span data-ttu-id="dc217-104">Notas de Versão do NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="dc217-104">NuGet 4.0 RTM Release Notes</span></span>

<span data-ttu-id="dc217-105">O [Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) vem com o NuGet 4.0, que adiciona suporte para o .NET Core, tem várias correções de qualidade e melhora o desempenho.</span><span class="sxs-lookup"><span data-stu-id="dc217-105">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="dc217-106">Esta versão também proporciona várias melhorias, como suporte para PackageReference, comandos do NuGet como destinos do MSBuild, restauração do pacote em segundo plano e muito mais.</span><span class="sxs-lookup"><span data-stu-id="dc217-106">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="dc217-107">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="dc217-107">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="dc217-108">Talvez a restauração do NuGet falhe quando você tem vários projetos referenciando outro projeto em uma solução</span><span class="sxs-lookup"><span data-stu-id="dc217-108">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="dc217-109">Problema</span><span class="sxs-lookup"><span data-stu-id="dc217-109">Issue</span></span>

<span data-ttu-id="dc217-110">Talvez a restauração do NuGet não funcionará se, em uma solução, você tiver referências do projeto no mesmo projeto com maiúsculas e minúsculas diferentes ou com diferentes caminhos relativos.</span><span class="sxs-lookup"><span data-stu-id="dc217-110">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="dc217-111">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="dc217-111">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="dc217-112">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="dc217-112">Workaround</span></span>

<span data-ttu-id="dc217-113">Corrija as maiúsculas ou caminhos relativos para que eles sejam os mesmos para todas as referências do projeto.</span><span class="sxs-lookup"><span data-stu-id="dc217-113">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="dc217-114">Ao usar o Console do Gerenciador de Pacotes, talvez a tecla 'Enter' não funcione</span><span class="sxs-lookup"><span data-stu-id="dc217-114">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="dc217-115">Problema</span><span class="sxs-lookup"><span data-stu-id="dc217-115">Issue</span></span>

<span data-ttu-id="dc217-116">Às vezes, a tecla enter não funciona no Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="dc217-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="dc217-117">Se isso ocorrer, confira o progresso na correção e forneça informações úteis adicionais sobre as etapas de reprodução.</span><span class="sxs-lookup"><span data-stu-id="dc217-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="dc217-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="dc217-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="dc217-119">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="dc217-119">Workaround</span></span>

<span data-ttu-id="dc217-120">Reinicie o Visual Studio e abra o PMC antes de abrir a solução.</span><span class="sxs-lookup"><span data-stu-id="dc217-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="dc217-121">Como alternativa, experimente excluir o `project.lock.json` e restaurá-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="dc217-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="dc217-122">Em projetos .NET Core, talvez você acabe em loop de restauração infinito ao usar um pacote que contém um assembly com uma assinatura inválida</span><span class="sxs-lookup"><span data-stu-id="dc217-122">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>

#### <a name="issue"></a><span data-ttu-id="dc217-123">Problema</span><span class="sxs-lookup"><span data-stu-id="dc217-123">Issue</span></span>

<span data-ttu-id="dc217-124">Às vezes, quando você usa um pacote que contém um assembly com uma assinatura inválida ou quando a versão do pacote é definida com o ticker 'DateTime', isso faz com que a restauração automática de pacotes seja executada em loop infinito.</span><span class="sxs-lookup"><span data-stu-id="dc217-124">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="dc217-125">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="dc217-125">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="dc217-126">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="dc217-126">Workaround</span></span>

<span data-ttu-id="dc217-127">Não há nenhuma solução alternativa no momento.</span><span class="sxs-lookup"><span data-stu-id="dc217-127">There is no workaround at this time.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="dc217-128">Você não consegue exibir, adicionar ou atualizar o DotNetCLITools usando o Gerenciador de Pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="dc217-128">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="dc217-129">Problema</span><span class="sxs-lookup"><span data-stu-id="dc217-129">Issue</span></span>

<span data-ttu-id="dc217-130">O Gerenciador de Pacotes do NuGet não exibe nem permite a adição/atualização de DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="dc217-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="dc217-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="dc217-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="dc217-132">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="dc217-132">Workaround</span></span>

<span data-ttu-id="dc217-133">O DotNetCLIToolReferences deve ser editado manualmente no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="dc217-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="dc217-134">Haverá falha na restauração do NuGet quando você definir a propriedade PackageId para projetos</span><span class="sxs-lookup"><span data-stu-id="dc217-134">NuGet restore will fail when you set PackageId property for projects</span></span>

#### <a name="issue"></a><span data-ttu-id="dc217-135">Problema</span><span class="sxs-lookup"><span data-stu-id="dc217-135">Issue</span></span>

<span data-ttu-id="dc217-136">Para projetos .NET Core, a restauração do NuGet no Visual Studio não respeita a propriedade PackageId de projetos.</span><span class="sxs-lookup"><span data-stu-id="dc217-136">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="dc217-137">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="dc217-137">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="dc217-138">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="dc217-138">Workaround</span></span>

<span data-ttu-id="dc217-139">Execute a restauração usando a linha de comando.</span><span class="sxs-lookup"><span data-stu-id="dc217-139">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="dc217-140">Quando seu projeto não tiver a pasta 'obj', poderá haver falha na restauração do pacote</span><span class="sxs-lookup"><span data-stu-id="dc217-140">When your project does not have 'obj' folder, package restore may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="dc217-141">Problema</span><span class="sxs-lookup"><span data-stu-id="dc217-141">Issue</span></span>

<span data-ttu-id="dc217-142">O Visual Studio não restaura PackageReferences quando a pasta 'obj' foi excluída do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dc217-142">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="dc217-143">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="dc217-143">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="dc217-144">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="dc217-144">Workaround</span></span>

<span data-ttu-id="dc217-145">Crie a pasta 'obj' manualmente e a restauração deverá funcionar.</span><span class="sxs-lookup"><span data-stu-id="dc217-145">Create 'obj' folder manually and the restore should work.</span></span>

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="dc217-146">Pode haver falha na atualização manual dos pacotes usando o pacote de atualização no console</span><span class="sxs-lookup"><span data-stu-id="dc217-146">Manually updating packages using Update-Package in console may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="dc217-147">Problema</span><span class="sxs-lookup"><span data-stu-id="dc217-147">Issue</span></span>

<span data-ttu-id="dc217-148">O uso manual do pacote de atualização no console funciona somente uma vez para projetos PackageReferences que acabaram de ser convertidos.</span><span class="sxs-lookup"><span data-stu-id="dc217-148">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="dc217-149">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="dc217-149">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="dc217-150">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="dc217-150">Workaround</span></span>

<span data-ttu-id="dc217-151">Não há nenhuma solução alternativa no momento.</span><span class="sxs-lookup"><span data-stu-id="dc217-151">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="dc217-152">Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto</span><span class="sxs-lookup"><span data-stu-id="dc217-152">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="dc217-153">Problema</span><span class="sxs-lookup"><span data-stu-id="dc217-153">Issue</span></span>

<span data-ttu-id="dc217-154">Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dc217-154">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="dc217-155">Isso acontece quando você está usando PackageReferences como o formato do gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="dc217-155">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="dc217-156">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="dc217-156">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="dc217-157">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="dc217-157">Workaround</span></span>

<span data-ttu-id="dc217-158">Faça uma restauração manual.</span><span class="sxs-lookup"><span data-stu-id="dc217-158">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="dc217-159">O msbuild /t:restore falha quando um projeto que define como destino o .NET461 referencia outro projeto que define como destino o .NETStandard</span><span class="sxs-lookup"><span data-stu-id="dc217-159">msbuild /t:restore fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="dc217-160">Problema</span><span class="sxs-lookup"><span data-stu-id="dc217-160">Issue</span></span>

<span data-ttu-id="dc217-161">O msbuild /t:restore falha quando um projeto baseado em PackageReferenece que define como destino o .NET461 referencia outro projeto baseado em PackageReference que define como destino o .NETStandard.</span><span class="sxs-lookup"><span data-stu-id="dc217-161">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="dc217-162">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="dc217-162">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="dc217-163">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="dc217-163">Workaround</span></span>

<span data-ttu-id="dc217-164">Não há nenhuma solução alternativa no momento.</span><span class="sxs-lookup"><span data-stu-id="dc217-164">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="dc217-165">Problemas corrigidos no período de tempo do NuGet 4.0 RTM</span><span class="sxs-lookup"><span data-stu-id="dc217-165">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="dc217-166">[Notas de Versão do NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md) -Lista todos os problemas corrigidos para o NuGet 4.0 RC</span><span class="sxs-lookup"><span data-stu-id="dc217-166">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

### <a name="features"></a><span data-ttu-id="dc217-167">Recursos</span><span class="sxs-lookup"><span data-stu-id="dc217-167">Features</span></span>

- <span data-ttu-id="dc217-168">Localizar cadeias de caracteres em NuGet.Core.sln – [#2041](https://github.com/NuGet/Home/issues/2041)</span><span class="sxs-lookup"><span data-stu-id="dc217-168">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

- <span data-ttu-id="dc217-169">O NuGet força o carregamento de projetos de aplicativo Web no modo LSL – [#4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="dc217-169">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

- <span data-ttu-id="dc217-170">Suporte a AutoReferenced PackageReference para bloquear alterações de versão na interface do usuário para pacotes com “sdk instalado” – [#4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="dc217-170">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

- <span data-ttu-id="dc217-171">Comunicar corretamente PackageSpec.Version para todas as dependências do projeto (PackageRef) – [#3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="dc217-171">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

- <span data-ttu-id="dc217-172">suporte à remoção de referências em `.csproj` das linhas de comando – [#4101](https://github.com/NuGet/Home/issues/4101)</span><span class="sxs-lookup"><span data-stu-id="dc217-172">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

- <span data-ttu-id="dc217-173">Suporte à restauração de projetos de PackageReference (normal e xplat) e Lightweight Solution Load – [#4003](https://github.com/NuGet/Home/issues/4003)</span><span class="sxs-lookup"><span data-stu-id="dc217-173">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

- <span data-ttu-id="dc217-174">suporte à adição de referências em `.csproj` das linhas de comando – [#3751](https://github.com/NuGet/Home/issues/3751)</span><span class="sxs-lookup"><span data-stu-id="dc217-174">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

- <span data-ttu-id="dc217-175">Suporte de restauração do NuGet para Lightweight Solution Load para `packages.config` ou `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span><span class="sxs-lookup"><span data-stu-id="dc217-175">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

- <span data-ttu-id="dc217-176">Suporte para contentFiles no arquivo de destino gerado no nuget – [#3683](https://github.com/NuGet/Home/issues/3683)</span><span class="sxs-lookup"><span data-stu-id="dc217-176">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

- <span data-ttu-id="dc217-177">Estabelecer um IC Mono para validação do nuget.exe no Mac usando o MSBuild – [#3646](https://github.com/NuGet/Home/issues/3646)</span><span class="sxs-lookup"><span data-stu-id="dc217-177">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

- <span data-ttu-id="dc217-178">Retirar o NuGet de dependências do NuGet.Core v2 – [#3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="dc217-178">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>

### <a name="bugs"></a><span data-ttu-id="dc217-179">Bugs</span><span class="sxs-lookup"><span data-stu-id="dc217-179">Bugs</span></span>

- <span data-ttu-id="dc217-180">A restauração do NuGet no Visual Studio não respeita a propriedade PackageId de projetos – [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="dc217-180">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

- <span data-ttu-id="dc217-181">Erro de NuGet ProjectSystemCache ao adicionar o pacote no pacote do vsix – [#4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="dc217-181">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

- <span data-ttu-id="dc217-182">O pacote gera uma exceção se IncludeSource for usado em um projeto com várias TFMs – [#4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="dc217-182">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

- <span data-ttu-id="dc217-183">Falha no VS 2017 RC3 ao usar a atualização do gerenciamento de pacotes de toda a solução – [#4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="dc217-183">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

- <span data-ttu-id="dc217-184">Não é possível desinstalar o pacote recém-instalado – [#4435](https://github.com/NuGet/Home/issues/4435)</span><span class="sxs-lookup"><span data-stu-id="dc217-184">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

- <span data-ttu-id="dc217-185">Ao migrar para o PackageRef, soluções híbridas demonstram um comportamento estranho de restauração – [#4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="dc217-185">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

- <span data-ttu-id="dc217-186">Compilar logo após iniciar a operação do NuGet (instalação, atualização, restauração) pode fazer com que o VS pare de responder – [#4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="dc217-186">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

- <span data-ttu-id="dc217-187">Interface do usuário sem resposta – Deadlock ao inicializar NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span><span class="sxs-lookup"><span data-stu-id="dc217-187">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

- <span data-ttu-id="dc217-188">adicionar o comando ao pacote deverá adicionar a versão como atributo, em vez de elemento – [#4325](https://github.com/NuGet/Home/issues/4325)</span><span class="sxs-lookup"><span data-stu-id="dc217-188">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

- <span data-ttu-id="dc217-189">Dotnet Restore foo.sln – falha quando as configurações no SLN podem causar projetos duplicados (mas com configurações diferentes) no grafo de restauração – [#4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="dc217-189">Dotnet Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

- <span data-ttu-id="dc217-190">Pacotes somente de conteúdo – [#3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="dc217-190">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

- <span data-ttu-id="dc217-191">Por padrão, recuse a opção do seletor de formato de pacote – [#4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="dc217-191">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

- <span data-ttu-id="dc217-192">Desempenho: o projeto CreateUAP_CSharp_VS.01.1.Create regrediu Duration_TotalElapsedTime 3.153,570 ms (149,1%).</span><span class="sxs-lookup"><span data-stu-id="dc217-192">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="dc217-193">Linha de base 26129.02 – [#4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="dc217-193">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

- <span data-ttu-id="dc217-194">Desempenho: a solução ManagedLangs_CS_DDRIT.0300.Rebuild regrediu Duration_TotalElapsedTime em 1,5 segundo.</span><span class="sxs-lookup"><span data-stu-id="dc217-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="dc217-195">Linha de base 26105 – [#4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="dc217-195">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

- <span data-ttu-id="dc217-196">A indicação falha em projetos multi-TFM – [#4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="dc217-196">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

- <span data-ttu-id="dc217-197">Desempenho: a solução WebForms_DDRIT.1200.Close regrediu VM_ImagesInMemory_Total_devenv pela contagem de 3,000 (0,5%).</span><span class="sxs-lookup"><span data-stu-id="dc217-197">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="dc217-198">Linha de base 26123.04 – [#4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="dc217-198">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

- <span data-ttu-id="dc217-199">vsfeedback – Avisos de pacote durante o direcionamento para netcoreapp1.1 – [#4397](https://github.com/NuGet/Home/issues/4397)</span><span class="sxs-lookup"><span data-stu-id="dc217-199">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

- <span data-ttu-id="dc217-200">PathTooLongException ao tentar adicionar um pacote do NuGet ao aplicativo Web vazio do ASP.NET Core – [#4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="dc217-200">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

- <span data-ttu-id="dc217-201">Execução de pacote frequente de mais -- o dotnet pack falha com o erro Há uma dependência circular no grafo de dependência de destino envolvendo o destino “Pack” – [#4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="dc217-201">Pack runs too often -- dotnet pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

- <span data-ttu-id="dc217-202">O pacote é executado com muita frequência – A geração de pacote do NuGet não inclui todas as configurações – [#4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="dc217-202">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

- <span data-ttu-id="dc217-203">O nuget que adiciona NullReferenceException com packageref em projetos do C++ – [#4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="dc217-203">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

- <span data-ttu-id="dc217-204">Acessibilidade: o narrator não narrar a caixa de seleção para escolher os projetos para instalar o pacote – [#4366](https://github.com/NuGet/Home/issues/4366)</span><span class="sxs-lookup"><span data-stu-id="dc217-204">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

- <span data-ttu-id="dc217-205">O NuGet VS17 esporadicamente falha ao se conectar com feeds VSO/VSTS – Bug do VS 365798 – [#4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="dc217-205">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

- <span data-ttu-id="dc217-206">contentFiles são colocados no local incorreto se o PackagePath especificar o caminho como “contentFiles” – [#4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="dc217-206">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

- <span data-ttu-id="dc217-207">O destino do pacote acrescenta a propriedade PackageVersion com VersionSuffix – [#4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="dc217-207">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

- <span data-ttu-id="dc217-208">Especificar o caminho do pacote não funciona com o dotnet pack – [#4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="dc217-208">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

- <span data-ttu-id="dc217-209">O NuGet produz diversos avisos sobre importações duplicadas durante a restauração – [#4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="dc217-209">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

- <span data-ttu-id="dc217-210">A escolha da caixa de diálogo “Formato do Gerenciador de Pacotes do NuGet” é exibida incorretamente no tema escuro – [#4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="dc217-210">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

- <span data-ttu-id="dc217-211">Falha do VS na restauração de build – [#4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="dc217-211">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

- <span data-ttu-id="dc217-212">Deadlocks do Visual Studio se você adicionar TFM no targetframeworks, salvar e depois compilar.</span><span class="sxs-lookup"><span data-stu-id="dc217-212">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="dc217-213">10% do tempo – [#4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="dc217-213">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

- <span data-ttu-id="dc217-214">nuget pack não produz a mensagem de êxito quando o empacotamento de um projeto é bem-sucedido – [#4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="dc217-214">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

- <span data-ttu-id="dc217-215">PackTask falha porque System.IO.Compression 4.1 não foi encontrado – [#4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="dc217-215">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

- <span data-ttu-id="dc217-216">O pacote é executado com muita frequência – PackTask falha com frequência com conflito de acesso de arquivo – [#4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="dc217-216">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

- <span data-ttu-id="dc217-217">O NuGet abre a janela de saída durante a restauração de tela de fundo – [#4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="dc217-217">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

- <span data-ttu-id="dc217-218">Eliminar ServiceProvider como padrão de codificação perigoso (o que pode fazer o sistema parar de responder) – [#4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="dc217-218">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

- <span data-ttu-id="dc217-219">Perf/UIHang – Melhorar leituras de DownloadTimeoutStream – [#4266](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="dc217-219">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

- <span data-ttu-id="dc217-220">Ocorre um deadklock no Visual Studio se você tentar fechar um projeto antes do NuGet concluir a restauração – [#4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="dc217-220">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

- <span data-ttu-id="dc217-221">Problemas com PackTask e empacotamento `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span><span class="sxs-lookup"><span data-stu-id="dc217-221">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

- <span data-ttu-id="dc217-222">[vsfeedback] Não é possível resolver pacotes do nuget no novo projeto (é preciso reiniciar o visual studio) – [#4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="dc217-222">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

- <span data-ttu-id="dc217-223">[vsfeedback] A lista suspensa “Version” que mostra as versões de pacote disponíveis se esforça para permanecer em sincronia com o pacote do nuGet selecionado... – [#4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="dc217-223">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

- <span data-ttu-id="dc217-224">O Nuget.Client deve usar CPS JoinableTaskFactory ao interagir com o CPS para evitar deadlocks – [#4185](https://github.com/NuGet/Home/issues/4185)</span><span class="sxs-lookup"><span data-stu-id="dc217-224">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

- <span data-ttu-id="dc217-225">O NuGet 3.5.0 não desempacota `.targets` do pacote – [#4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="dc217-225">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

- <span data-ttu-id="dc217-226">dotnet pack não é compatível com o título no `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span><span class="sxs-lookup"><span data-stu-id="dc217-226">dotnet pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

- <span data-ttu-id="dc217-227">Install-Package resulta em uma caixa de diálogo de erro no VS2017 RC – [#4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="dc217-227">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

- <span data-ttu-id="dc217-228">A atualização de um pacote para o projeto do .net core parece não funcionar, pois a interface do usuário não obtém a atualização do CPS do indicado.</span><span class="sxs-lookup"><span data-stu-id="dc217-228">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="dc217-229"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="dc217-229"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

- <span data-ttu-id="dc217-230">Melhorar o aviso de referência não resolvida – [#3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="dc217-230">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

- <span data-ttu-id="dc217-231">dotnet pack – ProjectReference perde informações de versão – [#3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="dc217-231">dotnet pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

- <span data-ttu-id="dc217-232">Criar o projeto de criação de aplicativos UWP e recompilar as regressões no tempo decorrido – [#3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="dc217-232">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

- <span data-ttu-id="dc217-233">A mensagem de restauração bem-sucedida é exibida mesmo após um erro durante a restauração.</span><span class="sxs-lookup"><span data-stu-id="dc217-233">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="dc217-234"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="dc217-234"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

- <span data-ttu-id="dc217-235">Publicar novamente o Nuget.CommandLine 3.4.4 para Nuget.org – [#2931](https://github.com/NuGet/Home/issues/2931)</span><span class="sxs-lookup"><span data-stu-id="dc217-235">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

- <span data-ttu-id="dc217-236">Na Migração, os projetos mudam de `project.json` para `.csproj` ---falha de restauração – [#4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="dc217-236">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

- <span data-ttu-id="dc217-237">Falha de restauração no Projeto de teste xunit recém-criado – [#4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="dc217-237">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

- <span data-ttu-id="dc217-238">Projetos do Core podem parar de responder, travando a interface do usuário ao abrir – [#4269](https://github.com/NuGet/Home/issues/4269)</span><span class="sxs-lookup"><span data-stu-id="dc217-238">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

- <span data-ttu-id="dc217-239">corrigir o arquivo de destino para tarefas de build – [#4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="dc217-239">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

- <span data-ttu-id="dc217-240">A lista de erros tem um erro após a solução de build que descarrega o projeto referenciado – [#4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="dc217-240">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

- <span data-ttu-id="dc217-241">MSB4057: o destino “_GenerateRestoreGraphProjectEntry” não existe no projeto.</span><span class="sxs-lookup"><span data-stu-id="dc217-241">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="dc217-242"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="dc217-242"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

- <span data-ttu-id="dc217-243">vsfeedback: a interface do usuário de gerenciador do nuget para a solução falha ao selecionar todos os projetos – [#4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="dc217-243">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

- <span data-ttu-id="dc217-244">O msbuildpath do nuget.exe falha quando há uma barra à direita – [#4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="dc217-244">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

- <span data-ttu-id="dc217-245">vsfeedback: a restauração do NuGet fornece vários avisos de referência de projeto para o projeto LinqToTwitter – [#4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="dc217-245">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

- <span data-ttu-id="dc217-246">O pacote de `.csproj` não inclui o atributo minClientVersion – [#4135](https://github.com/NuGet/Home/issues/4135)</span><span class="sxs-lookup"><span data-stu-id="dc217-246">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

- <span data-ttu-id="dc217-247">Atraso do fornecimento de NuGet.Build.Tasks.Pack.dll quando conectado ao VS2017 (d15rel 26014.00) – [#4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="dc217-247">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

- <span data-ttu-id="dc217-248">VSFeedback: falha na restauração de um projeto do VS 2015 gerado com CMake 3.7.1 – [#4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="dc217-248">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

- <span data-ttu-id="dc217-249">VSFeedback: erros de restauração podem obscurecer mensagens de erro mais completas que poderiam ser mostradas pelo build – [#4113](https://github.com/NuGet/Home/issues/4113)</span><span class="sxs-lookup"><span data-stu-id="dc217-249">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

- <span data-ttu-id="dc217-250">[VSFeedback] Erro ao restaurar pacotes do NuGet para o projeto de site: o valor não pode ser nulo.</span><span class="sxs-lookup"><span data-stu-id="dc217-250">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="dc217-251"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="dc217-251"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

- <span data-ttu-id="dc217-252">A migração gera “Exceção de referência do objeto” em NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker – [#4067](https://github.com/NuGet/Home/issues/4067)</span><span class="sxs-lookup"><span data-stu-id="dc217-252">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

- <span data-ttu-id="dc217-253">dotnet pack deve empacotar ferramentas com as versões de compilação do pacote – [#4063](https://github.com/NuGet/Home/issues/4063)</span><span class="sxs-lookup"><span data-stu-id="dc217-253">dotnet pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

- <span data-ttu-id="dc217-254">Restauração do nova tela de fundo grava milissegundos na barra de status quando a restauração leva segundos – [#4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="dc217-254">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

- <span data-ttu-id="dc217-255">Erro de digitação na falha ao resolver todas as referências do projeto – [#4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="dc217-255">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

- <span data-ttu-id="dc217-256">Habilitar fluxos de trabalho PCM em cenários de referência do pacote – [#4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="dc217-256">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

- <span data-ttu-id="dc217-257">Não é possível localizar os pacotes instalados na interface do usuário do gerenciador de pacotes – [#4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="dc217-257">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

- <span data-ttu-id="dc217-258">dotnet pack falha quando PackagePath está vazio – [#3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="dc217-258">dotnet pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

- <span data-ttu-id="dc217-259">Falha ao restaurar a tarefa em um cenário com vários usuários – [#3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="dc217-259">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

- <span data-ttu-id="dc217-260">Não é possível alterar o tipo de Conteúdo ao usar a Tarefa de Pacote do NuGet para o empacotamento – [#3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="dc217-260">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

- <span data-ttu-id="dc217-261">A cópia padrão do ContentFiles está incorreta para MsBuild /t:pack – [#3894](https://github.com/NuGet/Home/issues/3894)</span><span class="sxs-lookup"><span data-stu-id="dc217-261">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

- <span data-ttu-id="dc217-262">A restauração do pacote de instalação duplica os logs da mensagem de restauração de pacotes – [#3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="dc217-262">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

- <span data-ttu-id="dc217-263">Remover as grades de proteção – A restauração da seção “tempos de execução” deve se aplicar somente ao projeto atual – [#3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="dc217-263">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

- <span data-ttu-id="dc217-264">A tarefa do pacote coloca arquivos de conteúdo tanto em 'content/' quanto em 'contentFiles/' – [#3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="dc217-264">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

- <span data-ttu-id="dc217-265">dotnet pack3 realiza divisão de marca extra – [#3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="dc217-265">dotnet pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

- <span data-ttu-id="dc217-266">dotnet pack: empacotar projetos com referências de pacote resulta em aviso de importação duplicada – [#3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="dc217-266">dotnet pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

- <span data-ttu-id="dc217-267">O log de restauração no VS nem sempre é exibido – [#3633](https://github.com/NuGet/Home/issues/3633)</span><span class="sxs-lookup"><span data-stu-id="dc217-267">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

- <span data-ttu-id="dc217-268">Texto de ajuda de locais de NuGet locais ainda menciona cache de pacotes – [#3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="dc217-268">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

- <span data-ttu-id="dc217-269">O Restore3 associa PackageReferences a TargetFrameworks.</span><span class="sxs-lookup"><span data-stu-id="dc217-269">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="dc217-270"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="dc217-270"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

- <span data-ttu-id="dc217-271">O Nuget escolhe uma versão inesperada do MSBuild no VS "15" Preview 4 dev.</span><span class="sxs-lookup"><span data-stu-id="dc217-271">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="dc217-272">prompt de comando – [#3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="dc217-272">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

- <span data-ttu-id="dc217-273">Gravar arquivos de objetos/destinos em caso de restauração com falha – [#3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="dc217-273">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

- <span data-ttu-id="dc217-274">O NuGet não respeita as mesma correções de compatibilidade durante a restauração que o MSBuild ao ser executado no prompt de comando do VS 15 – [#3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="dc217-274">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

- <span data-ttu-id="dc217-275">Habilitar novamente o PackFromProjectWithDevelopmentDependencySet para VS15 – [#3272](https://github.com/NuGet/Home/issues/3272)</span><span class="sxs-lookup"><span data-stu-id="dc217-275">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

- <span data-ttu-id="dc217-276">Problemas do Blend com o NuGet – [#4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="dc217-276">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

- <span data-ttu-id="dc217-277">Integrar 4.0.0.2067 em repositórios de CLI e SDK para fornecimento com o RC2 – [#4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="dc217-277">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

- <span data-ttu-id="dc217-278">O VS para de responder ao Criar novo aplicativo de Console Core, Fechar a solução, Abrir a solução e Fechar a solução – [#4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="dc217-278">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

- <span data-ttu-id="dc217-279">O sistema para de responder ao abrir o projeto em d15prerel.25916.01 – [#3982](https://github.com/NuGet/Home/issues/3982)</span><span class="sxs-lookup"><span data-stu-id="dc217-279">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

- <span data-ttu-id="dc217-280">Corrigir a mensagem doc/help de locais do dotnet/nuget.exe – [#3919](https://github.com/NuGet/Home/issues/3919)</span><span class="sxs-lookup"><span data-stu-id="dc217-280">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

- <span data-ttu-id="dc217-281">Inspecionar PackTask em busca de problemas com espaço em branco à direita ou à esquerda – [#3906](https://github.com/NuGet/Home/issues/3906)</span><span class="sxs-lookup"><span data-stu-id="dc217-281">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

- <span data-ttu-id="dc217-282">dotnet pack empacota do obj, não do bin – [#3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="dc217-282">dotnet pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

- <span data-ttu-id="dc217-283">dotnet pack sempre parece definir ProjectReference para 1.0.0 – [#3874](https://github.com/NuGet/Home/issues/3874)</span><span class="sxs-lookup"><span data-stu-id="dc217-283">dotnet pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

- <span data-ttu-id="dc217-284">dotnet pack falha com referências de projeto e <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span><span class="sxs-lookup"><span data-stu-id="dc217-284">dotnet pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

- <span data-ttu-id="dc217-285">LockRecursionException em ProjectSystemCache.TryGetProjectNameByShortName – [#3861](https://github.com/NuGet/Home/issues/3861)</span><span class="sxs-lookup"><span data-stu-id="dc217-285">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

- <span data-ttu-id="dc217-286">Cortar espaços em branco de propriedades do MSBuild – [#3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="dc217-286">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

- <span data-ttu-id="dc217-287">Consolide os dois eventos de projeto acionados no carregamento do projeto – [#3759](https://github.com/NuGet/Home/issues/3759)</span><span class="sxs-lookup"><span data-stu-id="dc217-287">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

- <span data-ttu-id="dc217-288">Bibliotecas de P2P no arquivo `project.assets.json` tem uma Versão incorreta – [#3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="dc217-288">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

- <span data-ttu-id="dc217-289">Falha na restauração devido ao feed sem resposta e ao pacote indisponível – [#3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="dc217-289">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

- <span data-ttu-id="dc217-290">O nuget.exe pode ficar sem responder devido a uma grande quantidade de saídas de erro do MSBuild – [#3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="dc217-290">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

- <span data-ttu-id="dc217-291">A restauração no build falha para o Blend na primeira vez e é bem-sucedida na segunda (cenário de VS corrigido) – [#2121](https://github.com/NuGet/Home/issues/2121)</span><span class="sxs-lookup"><span data-stu-id="dc217-291">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

### <a name="dcrs"></a><span data-ttu-id="dc217-292">DCRs</span><span class="sxs-lookup"><span data-stu-id="dc217-292">DCRs</span></span>

- <span data-ttu-id="dc217-293">migrar vsix de vsix v2 para v3 – [#4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="dc217-293">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

- <span data-ttu-id="dc217-294">O NuGet deve ter um mecanismo para obter o caminho para o arquivo de bloqueio no MSBuild – [#3351](https://github.com/NuGet/Home/issues/3351)</span><span class="sxs-lookup"><span data-stu-id="dc217-294">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

- <span data-ttu-id="dc217-295">Adicionar ativos de build à verificação de compatibilidade de TFM e ao arquivo de ativos – [#3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="dc217-295">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

- <span data-ttu-id="dc217-296">Definir um novo “Pacote” ProjectCapability nos destinos de Pacote para habilitar funcionalidades relacionadas a Pacotes – [#4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="dc217-296">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

- <span data-ttu-id="dc217-297">Executar o pacote como um destino pós-build condicionado na propriedade "GeneratePackageOnBuild" do MSBuild – [#4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="dc217-297">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

- <span data-ttu-id="dc217-298">Use a propriedade RestoreProjectStyle do NuGet para criar um projeto específico do NuGet – [#4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="dc217-298">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

- <span data-ttu-id="dc217-299">Adaptar a restauração para alteração de referências transitivas do projeto – [#4076](https://github.com/NuGet/Home/issues/4076)</span><span class="sxs-lookup"><span data-stu-id="dc217-299">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

- <span data-ttu-id="dc217-300">Adicionar propriedades do NuGet ao arquivo de destino para projetos não UWP – [#4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="dc217-300">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

- <span data-ttu-id="dc217-301">Suporte a UWP TargetPlatformVersion – [#3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="dc217-301">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

- <span data-ttu-id="dc217-302">Comunicar metadados de referência de projeto no sistema de projeto do NuGet – [#3922](https://github.com/NuGet/Home/issues/3922)</span><span class="sxs-lookup"><span data-stu-id="dc217-302">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

- <span data-ttu-id="dc217-303">Adicionar interface do usuário ao modo de empacotamento – [#3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="dc217-303">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

- <span data-ttu-id="dc217-304">`.csproj` herdado precisa de NugetTargetMoniker e RuntimeIdentifiers definidos no projeto/destinos – [#3854](https://github.com/NuGet/Home/issues/3854)</span><span class="sxs-lookup"><span data-stu-id="dc217-304">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

- <span data-ttu-id="dc217-305">O pacote de instalação pode se sobrepor a recuperação automática – [#3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="dc217-305">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

- <span data-ttu-id="dc217-306">O menu de contexto QueryStatus não aparece quando o VSPackage não está carregado – [#3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="dc217-306">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

- <span data-ttu-id="dc217-307">Restauração de Solução e Restauração de Build ainda mostram caixas de diálogo – [#3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="dc217-307">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

- <span data-ttu-id="dc217-308">Isolar a versão VSSDK no build da solução NuGet.Clients – [#3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="dc217-308">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="dc217-309">Links para problemas do GitHub corrigidos no RTM</span><span class="sxs-lookup"><span data-stu-id="dc217-309">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="dc217-310">Lista de problemas 1</span><span class="sxs-lookup"><span data-stu-id="dc217-310">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RTM")  
[<span data-ttu-id="dc217-311">Lista de problemas 2</span><span class="sxs-lookup"><span data-stu-id="dc217-311">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC4")  
[<span data-ttu-id="dc217-312">Lista de problemas 3</span><span class="sxs-lookup"><span data-stu-id="dc217-312">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC3")  
[<span data-ttu-id="dc217-313">Lista de problemas 4</span><span class="sxs-lookup"><span data-stu-id="dc217-313">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC2")  
[<span data-ttu-id="dc217-314">Lista de problemas 5</span><span class="sxs-lookup"><span data-stu-id="dc217-314">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC")
