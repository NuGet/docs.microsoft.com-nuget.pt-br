---
title: Notas de Versão do NuGet 4.4 RTM
description: Notas de versão do NuGet 4.3 RTM incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 9ea11ad5476b02940b171fdc69ac0bf56598418d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548408"
---
# <a name="nuget-44-rtm-release-notes"></a><span data-ttu-id="5f4aa-103">Notas de Versão do NuGet 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="5f4aa-103">NuGet 4.4 RTM Release Notes</span></span>

<span data-ttu-id="5f4aa-104">O [Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) vem com o NuGet 4.4 RTM.</span><span class="sxs-lookup"><span data-stu-id="5f4aa-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="known-issues"></a><span data-ttu-id="5f4aa-105">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="5f4aa-105">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="5f4aa-106">Problemas com o .NET Standard 2.0 com o .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="5f4aa-106">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="5f4aa-107">O .NET Standard e suas ferramentas foram projetados de modo que os projetos destinados ao .NET Framework 4.6.1 podem consumir pacotes do NuGet e projetos destinados ao .NET Standard 2.0 ou anterior.</span><span class="sxs-lookup"><span data-stu-id="5f4aa-107">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="5f4aa-108">[Este documento](https://github.com/dotnet/standard/issues/481) resume os problemas desse cenário, o plano para lidar com eles e soluções alternativas que você pode implantar com o estado atual das ferramentas.</span><span class="sxs-lookup"><span data-stu-id="5f4aa-108">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="5f4aa-109">Ao usar o Console do Gerenciador de Pacotes, talvez a tecla 'Enter' não funcione</span><span class="sxs-lookup"><span data-stu-id="5f4aa-109">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="5f4aa-110">Problema</span><span class="sxs-lookup"><span data-stu-id="5f4aa-110">Issue</span></span>

<span data-ttu-id="5f4aa-111">Às vezes, a tecla enter não funciona no Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="5f4aa-111">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="5f4aa-112">Se isso ocorrer, confira o progresso na correção e forneça informações úteis adicionais sobre as etapas de reprodução.</span><span class="sxs-lookup"><span data-stu-id="5f4aa-112">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="5f4aa-113">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-113">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="5f4aa-114">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="5f4aa-114">Workaround</span></span>

<span data-ttu-id="5f4aa-115">Reinicie o Visual Studio e abra o PMC antes de abrir a solução.</span><span class="sxs-lookup"><span data-stu-id="5f4aa-115">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="5f4aa-116">Como alternativa, experimente excluir o `project.lock.json` e restaurá-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="5f4aa-116">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="5f4aa-117">Você não consegue exibir, adicionar ou atualizar o DotNetCLITools usando o Gerenciador de Pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="5f4aa-117">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="5f4aa-118">Problema</span><span class="sxs-lookup"><span data-stu-id="5f4aa-118">Issue</span></span>

<span data-ttu-id="5f4aa-119">O Gerenciador de Pacotes do NuGet não exibe nem permite a adição/atualização de DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="5f4aa-119">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="5f4aa-120">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="5f4aa-120">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="5f4aa-121">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="5f4aa-121">Workaround</span></span>

<span data-ttu-id="5f4aa-122">O DotNetCLIToolReferences deve ser editado manualmente no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="5f4aa-122">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="5f4aa-123">Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto</span><span class="sxs-lookup"><span data-stu-id="5f4aa-123">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="5f4aa-124">Problema</span><span class="sxs-lookup"><span data-stu-id="5f4aa-124">Issue</span></span>

<span data-ttu-id="5f4aa-125">Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f4aa-125">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="5f4aa-126">Isso acontece quando você está usando PackageReferences como o formato do gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="5f4aa-126">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="5f4aa-127">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="5f4aa-127">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="5f4aa-128">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="5f4aa-128">Workaround</span></span>

<span data-ttu-id="5f4aa-129">Faça uma restauração manual.</span><span class="sxs-lookup"><span data-stu-id="5f4aa-129">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="5f4aa-130">Um pacote em um projeto do .NET Core que contém um assembly com uma assinatura inválida pode disparar um loop de restauração infinito</span><span class="sxs-lookup"><span data-stu-id="5f4aa-130">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="5f4aa-131">Problema</span><span class="sxs-lookup"><span data-stu-id="5f4aa-131">Issue</span></span>

<span data-ttu-id="5f4aa-132">Às vezes, quando você usa um pacote que contém um assembly com uma assinatura inválida ou quando a versão do pacote é definida com o ticker 'DateTime', isso faz com que a restauração automática de pacotes seja executada em loop infinito (dotnet/project-system#1457).</span><span class="sxs-lookup"><span data-stu-id="5f4aa-132">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="5f4aa-133">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="5f4aa-133">Workaround</span></span>

<span data-ttu-id="5f4aa-134">Não há nenhuma solução alternativa no momento.</span><span class="sxs-lookup"><span data-stu-id="5f4aa-134">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="5f4aa-135">Problemas corrigidos no período de tempo do NuGet 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="5f4aa-135">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="5f4aa-136">[Notas de Versão do NuGet 4.3 RTM](../release-notes/nuget-4.3-RTM.md) – Lista todos os problemas corrigidos no NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="5f4aa-136">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="5f4aa-137">Recursos</span><span class="sxs-lookup"><span data-stu-id="5f4aa-137">Features</span></span>

- <span data-ttu-id="5f4aa-138">Suporte para Lightweight Solution Load em cenários PMC e interface do usuário do PM do NuGet – [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-138">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="5f4aa-139">O destino do pacote msbuild deve ter um gancho público para destinos de usuário em execução antes de si mesmo – [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-139">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="5f4aa-140">Recurso: adicionar a opção dependencyVersion à instalação do nuget – [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-140">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="5f4aa-141">uap10.0.TODO.0 deve ser mapeado para o .NET Standard 2.0 para NuGet – [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-141">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="5f4aa-142">Suporte ao SKU das Ferramentas de Build do Visual Studio com o msbuild /t:restore – [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-142">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="5f4aa-143">Durante a restauração, gera um erro se o suporte do .NET 4.6.1 para o .NET Standard 2.0 for necessário, mas não está instalado – [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-143">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="5f4aa-144">Interface do usuário do cliente de reserva do prefixo da ID do pacote – [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-144">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="5f4aa-145">entregar componentes nuget localizados para dar suporte à localização dotnet.exe – [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-145">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="5f4aa-146">Bugs</span><span class="sxs-lookup"><span data-stu-id="5f4aa-146">Bugs</span></span>

- <span data-ttu-id="5f4aa-147">Caminhos de projeto com maiúsculas e minúsculas diferentes podem fazer com que a restauração perca PackageReferences – [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-147">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="5f4aa-148">Mover os códigos de erro com números de aviso para o intervalo de erro – [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-148">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="5f4aa-149">Erro enganoso quando a versão do .NET Standard não é conhecida como compatível com a estrutura de destino – [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-149">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="5f4aa-150">Arquivos de teste com licenças confusas – [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-150">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="5f4aa-151">Cabeçalhos de licença ausentes em modelos de teste EndToEnd – [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-151">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="5f4aa-152">A restauração de packages.config mostra erros como NU1000 – [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-152">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="5f4aa-153">A instalação do nuget.exe deve ter DisableParallelProcessing no mono – [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-153">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="5f4aa-154">A instalação do nuget.exe desabilita incorretamente o cache – [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-154">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="5f4aa-155">O VS executa o comando restore para packages.config quando a Restore está desabilitado exibe a mensagem incorreta – [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-155">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="5f4aa-156">VS; Executar o comando restore quando Restore está desabilitado exibe uma mensagem confusa – [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-156">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="5f4aa-157">GetRestoreDotnetCliToolsTask falha quando metadados da versão estão ausentes – [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-157">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="5f4aa-158">dotnet</span><span class="sxs-lookup"><span data-stu-id="5f4aa-158">dotnet</span></span>
  - <span data-ttu-id="5f4aa-159">dotnetcore add package pode limpar linhas vazias de um csproj – [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-159">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="5f4aa-160">Nomes de origens das configurações de credencial no NuGet.Config diferenciam maiúsculas de minúsculas – [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-160">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="5f4aa-161">Habilitar GeneratePackageOnBuild excluiu todo o meu histórico de pacotes – [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-161">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="5f4aa-162">A restauração não restaurará pacotes mono.cecil ou semver, mas todos os outros pacotes são restaurados.</span><span class="sxs-lookup"><span data-stu-id="5f4aa-162">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="5f4aa-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="5f4aa-164">Erros e avisos – erro inválido quando uma origem está indisponível.</span><span class="sxs-lookup"><span data-stu-id="5f4aa-164">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="5f4aa-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="5f4aa-166">[DesignConsistency] O texto de status de instalação do NuGet não aparece corretamente no tema escuro no momento.</span><span class="sxs-lookup"><span data-stu-id="5f4aa-166">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="5f4aa-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="5f4aa-168">Pacotes de atualização nas atualizações/instalações da solução para todos os projetos – [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-168">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="5f4aa-169">dotnet</span><span class="sxs-lookup"><span data-stu-id="5f4aa-169">dotnet</span></span>
  - <span data-ttu-id="5f4aa-170">dotnetcore pack demonstra um comportamento diferente entre TargetFramework e TargetFrameworks – [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-170">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="5f4aa-171">DLLs incluídas na pasta Ferramentas geram avisos – [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-171">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="5f4aa-172">O NuGet.ContentModel consome muita memória para operações de cadeia de caracteres – [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-172">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="5f4aa-173">RuntimeEnvironmentHelper.IsLinux retorna true para OSX – [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-173">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="5f4aa-174">'dotnet pack' coloca nuspec em obj em vez de obj\Debug – [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-174">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="5f4aa-175">Upgrade extremamente lento de pacote do Nuget – [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-175">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="5f4aa-176">CPS fora de sincronia com a Restauração de grandes soluções que ainda não ativou o LSL (lightweight solution restore) – [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-176">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="5f4aa-177">SemVer 2.0 – nuget pack com a versão fornecida ignora os metadados (3.5.0-rtm-1938) – [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-177">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="5f4aa-178">O NuGet.exe (3.+) instala o pacote com número de Versão e o sinalizador ExcludeVersion não atualiza o pacote para a versão mais recente – [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-178">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="5f4aa-179">A restauração do project.json deve avisar quando pacotes de nível superior violam as restrições – [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-179">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="5f4aa-180">-ConfigFile não está definindo a configuração personalizada no comando install – [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-180">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="5f4aa-181">A instalação do nuget.exe não honra a opção '-DisableParallelProcessing' – [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-181">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="5f4aa-182">Origens desabilitadas ainda são usadas pelo DotNet.exe ou msbuild.exe – [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-182">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="5f4aa-183">Corrigir travamentos no cenário LSL – [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-183">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="5f4aa-184">DCRs</span><span class="sxs-lookup"><span data-stu-id="5f4aa-184">DCRs</span></span>

- <span data-ttu-id="5f4aa-185">Suporte a TargetFramework na instalação do nuget.exe – [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-185">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="5f4aa-186">Adicionar diferentes cadeias de caracteres UserAgent de tarefa do msbuild (netcore vs msbuild da área de trabalho) – [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-186">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="5f4aa-187">PackagePathResolver.GetPackageDirectoryName deve ser virtual – [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-187">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="5f4aa-188">[DesignConsistency] Mensagem confusa durante a adição de um pacote do NuGet – [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-188">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="5f4aa-189">[Avisos e erros] NoWarn não flui transitivamente por referências P2P – [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-189">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="5f4aa-190">Carga de Solução Leve: núcleo comum para interface do usuário de PM, PMC e IVs – [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-190">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="5f4aa-191">Lightweight Solution Load: suporte – PMC – [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-191">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="5f4aa-192">Adicionar suporte para o destino do MSBuild pré-restauração que o Visual Studio dispara – [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-192">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="5f4aa-193">Adicione um destino público NuGet.targets que pode ser referenciado usando BeforeTargets- [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-193">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="5f4aa-194">O destino do pacote não pode criar contentFiles com ações de build corretamente – [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-194">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="5f4aa-195">RestoreOperationLogger.Do bloqueia os threads do pool de threads – [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-195">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="5f4aa-196">Docs</span><span class="sxs-lookup"><span data-stu-id="5f4aa-196">Docs</span></span>

- <span data-ttu-id="5f4aa-197">Documentos para o comando de instalação DependencyVersion e sinalizadores do Framework – [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-197">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="5f4aa-198">Atualização para documentos em avisos e erros do NuGet – [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="5f4aa-198">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="5f4aa-199">Links para problemas do GitHub corrigidos no RTM 4.4</span><span class="sxs-lookup"><span data-stu-id="5f4aa-199">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="5f4aa-200">Lista de Problemas 1</span><span class="sxs-lookup"><span data-stu-id="5f4aa-200">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="5f4aa-201">Lista de Problemas 2</span><span class="sxs-lookup"><span data-stu-id="5f4aa-201">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="5f4aa-202">Lista de Problemas 3</span><span class="sxs-lookup"><span data-stu-id="5f4aa-202">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
