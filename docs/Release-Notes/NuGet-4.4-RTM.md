---
title: "Notas de Versão do NuGet 4.4 RTM | Microsoft Docs"
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
ms.openlocfilehash: 25f41649807b29d39900aa86e2c26f05463e91eb
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-44-rtm-release-notes"></a><span data-ttu-id="c2341-104">Notas de Versão do NuGet 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="c2341-104">NuGet 4.4 RTM Release Notes</span></span>

<span data-ttu-id="c2341-105">O [Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) vem com o NuGet 4.4 RTM.</span><span class="sxs-lookup"><span data-stu-id="c2341-105">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="known-issues"></a><span data-ttu-id="c2341-106">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="c2341-106">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="c2341-107">Problemas com o .NET Standard 2.0 com o .NET Framework & NuGet</span><span class="sxs-lookup"><span data-stu-id="c2341-107">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="c2341-108">O .NET Standard e suas ferramentas foram projetados de modo que os projetos destinados ao .NET Framework 4.6.1 podem consumir pacotes do NuGet e projetos destinados ao .NET Standard 2.0 ou anterior.</span><span class="sxs-lookup"><span data-stu-id="c2341-108">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="c2341-109">[Este documento](https://github.com/dotnet/standard/issues/481) resume os problemas desse cenário, o plano para lidar com eles e soluções alternativas que você pode implantar com o estado atual das ferramentas.</span><span class="sxs-lookup"><span data-stu-id="c2341-109">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="c2341-110">Ao usar o Console do Gerenciador de Pacotes, talvez a tecla 'Enter' não funcione</span><span class="sxs-lookup"><span data-stu-id="c2341-110">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="c2341-111">Problema</span><span class="sxs-lookup"><span data-stu-id="c2341-111">Issue</span></span>

<span data-ttu-id="c2341-112">Às vezes, a tecla enter não funciona no Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="c2341-112">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="c2341-113">Se isso ocorrer, confira o progresso na correção e forneça informações úteis adicionais sobre as etapas de reprodução.</span><span class="sxs-lookup"><span data-stu-id="c2341-113">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="c2341-114">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="c2341-114">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="c2341-115">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="c2341-115">Workaround</span></span>

<span data-ttu-id="c2341-116">Reinicie o Visual Studio e abra o PMC antes de abrir a solução.</span><span class="sxs-lookup"><span data-stu-id="c2341-116">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="c2341-117">Como alternativa, experimente excluir o `project.lock.json` e restaurá-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="c2341-117">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="c2341-118">Você não consegue exibir, adicionar ou atualizar o DotNetCLITools usando o Gerenciador de Pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="c2341-118">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="c2341-119">Problema</span><span class="sxs-lookup"><span data-stu-id="c2341-119">Issue</span></span>

<span data-ttu-id="c2341-120">O Gerenciador de Pacotes do NuGet não exibe nem permite a adição/atualização de DotNetCLITools.</span><span class="sxs-lookup"><span data-stu-id="c2341-120">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="c2341-121">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="c2341-121">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="c2341-122">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="c2341-122">Workaround</span></span>

<span data-ttu-id="c2341-123">O DotNetCLIToolReferences deve ser editado manualmente no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="c2341-123">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="c2341-124">Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto</span><span class="sxs-lookup"><span data-stu-id="c2341-124">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="c2341-125">Problema</span><span class="sxs-lookup"><span data-stu-id="c2341-125">Issue</span></span>

<span data-ttu-id="c2341-126">Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c2341-126">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="c2341-127">Isso acontece quando você está usando PackageReferences como o formato do gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="c2341-127">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="c2341-128">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="c2341-128">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="c2341-129">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="c2341-129">Workaround</span></span>

<span data-ttu-id="c2341-130">Faça uma restauração manual.</span><span class="sxs-lookup"><span data-stu-id="c2341-130">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="c2341-131">Um pacote em um projeto do .NET Core que contém um assembly com uma assinatura inválida pode disparar um loop de restauração infinito</span><span class="sxs-lookup"><span data-stu-id="c2341-131">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="c2341-132">Problema</span><span class="sxs-lookup"><span data-stu-id="c2341-132">Issue</span></span>

<span data-ttu-id="c2341-133">Às vezes, quando você usa um pacote que contém um assembly com uma assinatura inválida ou quando a versão do pacote é definida com o ticker 'DateTime', isso faz com que a restauração automática de pacotes seja executada em loop infinito (dotnet/project-system#1457).</span><span class="sxs-lookup"><span data-stu-id="c2341-133">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="c2341-134">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="c2341-134">Workaround</span></span>

<span data-ttu-id="c2341-135">Não há nenhuma solução alternativa no momento.</span><span class="sxs-lookup"><span data-stu-id="c2341-135">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="c2341-136">Problemas corrigidos no período de tempo do NuGet 4.4 RTM</span><span class="sxs-lookup"><span data-stu-id="c2341-136">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="c2341-137">[Notas de Versão do NuGet 4.3 RTM](../release-notes/nuget-4.3-RTM.md) – Lista todos os problemas corrigidos no NuGet 4.3 RTM</span><span class="sxs-lookup"><span data-stu-id="c2341-137">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="c2341-138">Recursos</span><span class="sxs-lookup"><span data-stu-id="c2341-138">Features</span></span>

- <span data-ttu-id="c2341-139">Suporte para Lightweight Solution Load em cenários PMC e interface do usuário do PM do NuGet – [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="c2341-139">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="c2341-140">O destino do pacote msbuild deve ter um gancho público para destinos de usuário em execução antes de si mesmo – [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="c2341-140">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="c2341-141">Recurso: adicionar a opção dependencyVersion à instalação do nuget – [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="c2341-141">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="c2341-142">uap10.0.TODO.0 deve ser mapeado para o .NET Standard 2.0 para NuGet – [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="c2341-142">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="c2341-143">Suporte ao SKU das Ferramentas de Build do Visual Studio com o msbuild /t:restore – [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="c2341-143">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="c2341-144">Durante a restauração, gera um erro se o suporte do .NET 4.6.1 para o .NET Standard 2.0 for necessário, mas não está instalado – [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="c2341-144">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="c2341-145">Interface do usuário do cliente de reserva do prefixo da ID do pacote – [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="c2341-145">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="c2341-146">entregar componentes nuget localizados para dar suporte à localização dotnet.exe – [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="c2341-146">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="c2341-147">Bugs</span><span class="sxs-lookup"><span data-stu-id="c2341-147">Bugs</span></span>

- <span data-ttu-id="c2341-148">Caminhos de projeto com maiúsculas e minúsculas diferentes podem fazer com que a restauração perca PackageReferences – [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="c2341-148">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="c2341-149">Mover os códigos de erro com números de aviso para o intervalo de erro – [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="c2341-149">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="c2341-150">Erro enganoso quando a versão do .NET Standard não é conhecida como compatível com a estrutura de destino – [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="c2341-150">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="c2341-151">Arquivos de teste com licenças confusas – [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="c2341-151">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="c2341-152">Cabeçalhos de licença ausentes em modelos de teste EndToEnd – [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="c2341-152">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="c2341-153">A restauração de packages.config mostra erros como NU1000 – [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="c2341-153">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="c2341-154">A instalação do nuget.exe deve ter DisableParallelProcessing no mono – [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="c2341-154">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="c2341-155">A instalação do nuget.exe desabilita incorretamente o cache – [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="c2341-155">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="c2341-156">O VS executa o comando restore para packages.config quando a Restore está desabilitado exibe a mensagem incorreta – [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="c2341-156">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="c2341-157">VS; Executar o comando restore quando Restore está desabilitado exibe uma mensagem confusa – [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="c2341-157">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="c2341-158">GetRestoreDotnetCliToolsTask falha quando metadados da versão estão ausentes – [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="c2341-158">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="c2341-159">dotnet add package pode apagar linhas vazias de um csproj – [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="c2341-159">dotnet add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="c2341-160">Nomes de origens das configurações de credencial no NuGet.Config diferenciam maiúsculas de minúsculas – [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="c2341-160">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="c2341-161">Habilitar GeneratePackageOnBuild excluiu todo o meu histórico de pacotes – [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="c2341-161">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="c2341-162">A restauração não restaurará pacotes mono.cecil ou semver, mas todos os outros pacotes são restaurados.</span><span class="sxs-lookup"><span data-stu-id="c2341-162">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="c2341-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="c2341-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="c2341-164">Erros e avisos – erro inválido quando uma origem está indisponível.</span><span class="sxs-lookup"><span data-stu-id="c2341-164">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="c2341-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="c2341-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="c2341-166">[DesignConsistency] O texto de status de instalação do NuGet não aparece corretamente no tema escuro no momento.</span><span class="sxs-lookup"><span data-stu-id="c2341-166">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="c2341-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="c2341-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="c2341-168">Pacotes de atualização nas atualizações/instalações da solução para todos os projetos – [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="c2341-168">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="c2341-169">dotnet pack demonstra um comportamento diferente entre TargetFramework e TargetFrameworks – [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="c2341-169">dotnet pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="c2341-170">DLLs incluídas na pasta Ferramentas geram avisos – [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="c2341-170">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="c2341-171">O NuGet.ContentModel consome muita memória para operações de cadeia de caracteres – [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="c2341-171">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="c2341-172">RuntimeEnvironmentHelper.IsLinux retorna true para OSX – [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="c2341-172">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="c2341-173">'dotnet pack' coloca nuspec em obj em vez de obj\Debug – [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="c2341-173">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="c2341-174">Upgrade extremamente lento de pacote do Nuget – [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="c2341-174">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="c2341-175">CPS fora de sincronia com a Restauração de grandes soluções que ainda não ativou o LSL (lightweight solution restore) – [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="c2341-175">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="c2341-176">SemVer 2.0 – nuget pack com a versão fornecida ignora os metadados (3.5.0-rtm-1938) – [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="c2341-176">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="c2341-177">O NuGet.exe (3.+) instala o pacote com número de Versão e o sinalizador ExcludeVersion não atualiza o pacote para a versão mais recente – [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="c2341-177">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="c2341-178">A restauração do project.json deve avisar quando pacotes de nível superior violam as restrições – [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="c2341-178">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="c2341-179">-ConfigFile não está definindo a configuração personalizada no comando install – [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="c2341-179">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="c2341-180">A instalação do nuget.exe não honra a opção '-DisableParallelProcessing' – [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="c2341-180">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="c2341-181">Origens desabilitadas ainda são usadas pelo DotNet.exe ou msbuild.exe – [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="c2341-181">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="c2341-182">Corrigir travamentos no cenário LSL – [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="c2341-182">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="c2341-183">DCRs</span><span class="sxs-lookup"><span data-stu-id="c2341-183">DCRs</span></span>

- <span data-ttu-id="c2341-184">Suporte a TargetFramework na instalação do nuget.exe – [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="c2341-184">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="c2341-185">Adicionar diferentes cadeias de caracteres UserAgent de tarefa do msbuild (netcore vs msbuild da área de trabalho) – [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="c2341-185">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="c2341-186">PackagePathResolver.GetPackageDirectoryName deve ser virtual – [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="c2341-186">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="c2341-187">[DesignConsistency] Mensagem confusa durante a adição de um pacote do NuGet – [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="c2341-187">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="c2341-188">[Avisos e erros] NoWarn não flui transitivamente por referências P2P – [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="c2341-188">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="c2341-189">Carga de Solução Leve: núcleo comum para interface do usuário de PM, PMC e IVs\* – [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="c2341-189">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="c2341-190">Lightweight Solution Load: suporte – PMC – [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="c2341-190">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="c2341-191">Adicionar suporte para o destino do MSBuild pré-restauração que o Visual Studio dispara – [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="c2341-191">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="c2341-192">Adicione um destino público NuGet.targets que pode ser referenciado usando BeforeTargets- [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="c2341-192">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="c2341-193">O destino do pacote não pode criar contentFiles com ações de build corretamente – [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="c2341-193">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="c2341-194">RestoreOperationLogger.Do bloqueia os threads do pool de threads – [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="c2341-194">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="c2341-195">Docs</span><span class="sxs-lookup"><span data-stu-id="c2341-195">Docs</span></span>

- <span data-ttu-id="c2341-196">Documentos para o comando de instalação DependencyVersion e sinalizadores do Framework – [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="c2341-196">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="c2341-197">Atualização para documentos em avisos e erros do NuGet – [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="c2341-197">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="c2341-198">Links para problemas do GitHub corrigidos no RTM 4.4</span><span class="sxs-lookup"><span data-stu-id="c2341-198">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="c2341-199">Lista de Problemas 1</span><span class="sxs-lookup"><span data-stu-id="c2341-199">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="c2341-200">Lista de Problemas 2</span><span class="sxs-lookup"><span data-stu-id="c2341-200">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="c2341-201">Lista de Problemas 3</span><span class="sxs-lookup"><span data-stu-id="c2341-201">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
