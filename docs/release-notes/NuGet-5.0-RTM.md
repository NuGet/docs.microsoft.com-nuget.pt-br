---
title: Notas de versão do NuGet 5,0 RTM
description: Notas de versão do NuGet 5,0 incluindo problemas conhecidos, correções de bugs, novos recursos e DCRs.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: e4a6be7fb26e3cc4bd297eaf02999f6ac1389b77
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236796"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="70749-103">Notas de versão do NuGet 5,0</span><span class="sxs-lookup"><span data-stu-id="70749-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="70749-104">Veículos de distribuição do NuGet:</span><span class="sxs-lookup"><span data-stu-id="70749-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="70749-105">Versão do NuGet</span><span class="sxs-lookup"><span data-stu-id="70749-105">NuGet version</span></span> | <span data-ttu-id="70749-106">Disponível na versão do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="70749-106">Available in Visual Studio version</span></span>| <span data-ttu-id="70749-107">Disponível em SDKs do .NET</span><span class="sxs-lookup"><span data-stu-id="70749-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="70749-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="70749-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="70749-109">Visual Studio 2019 versão 16,0</span><span class="sxs-lookup"><span data-stu-id="70749-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="70749-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="70749-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="70749-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="70749-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="70749-112">Visual Studio 2019 versão 16.0.4</span><span class="sxs-lookup"><span data-stu-id="70749-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="70749-113">[2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="70749-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="70749-114"><sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core</span><span class="sxs-lookup"><span data-stu-id="70749-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="70749-115"><sup>2</sup> Disponível como uma instalação opcional com o Visual Studio 2019 com carga de trabalho do .NET Core</span><span class="sxs-lookup"><span data-stu-id="70749-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="70749-116">Resumo: o que há de novo no 5,0</span><span class="sxs-lookup"><span data-stu-id="70749-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="70749-117">Suporte para restaurar [soluções filtradas](/visualstudio/ide/filtered-solutions?view=vs-2019) no Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="70749-117">Support for restoring [filtered solutions](/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="70749-118">`BuildTransitive` a pasta permite que os pacotes contribuam de forma transitiva destinos/props para o projeto de host- [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="70749-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="70749-119">Melhor suporte para cenários de PackageReference no NuGet IVs APIs- [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="70749-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="70749-120">`nuget.exe pack project.json` foi preterido- [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="70749-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="70749-121">O plugin do provedor de credenciais Gen 1 foi substituído pela [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) e em breve será preterido- [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="70749-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="70749-122">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="70749-122">Issues fixed in this release</span></span>

<span data-ttu-id="70749-123">**Bugs**</span><span class="sxs-lookup"><span data-stu-id="70749-123">**Bugs**</span></span>

* <span data-ttu-id="70749-124">Ao fazer uma restauração de NoOp, evite \* .dgspec.jsem gravar no diretório obj- [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="70749-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="70749-125">As permissões em arquivos criados dentro de ~/.NuGet são muito abertas- [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="70749-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="70749-126">`dotnet list package --outdated`Não funciona com fontes que precisam de [#7605](https://github.com/NuGet/Home/issues/7605) de autenticação</span><span class="sxs-lookup"><span data-stu-id="70749-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="70749-127">NuGet. VisualStudio. IVsPackageInstaller-a chamada em um projeto sem referências de pacote sempre usa packages.config, mesmo que o padrão esteja definido como PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="70749-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="70749-128">PMC: a reinstalação do Update-Package falha ("não é possível localizar o pacote") em pacotes deslistados.</span><span class="sxs-lookup"><span data-stu-id="70749-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="70749-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="70749-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="70749-130">Adicionar aviso de terceiros em nosso repositório e VSIX- [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="70749-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="70749-131">NuGet. VisualStudio. IVsPackageInstaller. InstallPackage deve instalar a versão mais recente quando nenhuma versão é fornecida- [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="70749-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="70749-132">--suporte interativo para o [#7519](https://github.com/NuGet/Home/issues/7519) dotnet do NuGet</span><span class="sxs-lookup"><span data-stu-id="70749-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="70749-133">Ao restaurar com o arquivo de bloqueio, o aviso de NU1603 não deve ser gerado.</span><span class="sxs-lookup"><span data-stu-id="70749-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="70749-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="70749-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="70749-135">O NuGet não deve imprimir o caminho do projeto durante a restauração com o mínimo de log- [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="70749-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="70749-136">--suporte interativo para o dotnet remover pacote- [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="70749-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="70749-137">Adicionar NuGet. Packaging. Core com TypeForwardedTo attrs- [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="70749-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="70749-138">plugins_cache precisa de um caminho mais curto para funcionar bem [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="70749-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="70749-139">Prefira o caminho para a descoberta do MSBuild se o usuário não solicitar uma versão do MSBuild específica- [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="70749-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="70749-140">`nuget.exe /?` deve listar as versões corretas do MSBuild- [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="70749-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="70749-141">NuGet. targets (498, 5): erro: não foi possível encontrar uma parte do caminho '/tmp/NuGetScratch-on mono- [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="70749-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="70749-142">restaurar desnecessariamente enumera o conteúdo de todas as versões do pacote referenciado no cache da máquina- [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="70749-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="70749-143">A detecção automática do MSBuild sempre seleciona 16,0 após a instalação do VS 2019 Preview- [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="70749-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="70749-144">o pacote de lista dotnet em uma solução gera entradas duplicadas para o Framework- [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="70749-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="70749-145">Exceção "o nome do caminho vazio não é válido" ao chamar IVsPackageInstaller. InstallPackage na pasta projetos e pacotes antigos não existe.</span><span class="sxs-lookup"><span data-stu-id="70749-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="70749-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="70749-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="70749-147">MSBuild/t: Restore o mínimo de detalhes deve ser mais mínimo [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="70749-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="70749-148">A interface do usuário do NuGet do VS 16.0 tem guias ilegíveis devido a problemas de cor- [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="70749-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="70749-149">NuGet. Core & NuGet. clients License.txt esclarecimento- [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="70749-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="70749-150">Restauração desnecessariamente enumera a pasta de pacote global em tentativa de determinar o tipo [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="70749-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="70749-151">Os erros da imposição de arquivos bloqueados devem aparecer na janela Lista de Erros- [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="70749-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="70749-152">Corrigir NuGet.Configproblemas de uração- [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="70749-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="70749-153">Adaptar ao MSBuild atualizando seu local de instalação- [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="70749-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="70749-154">NuGet. Build. Tasks. Pack deve ser uma dependência de desenvolvimento- [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="70749-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="70749-155">Adicionar ponto de extensão de pacote para incluir símbolos de depuração- [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="70749-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="70749-156">`dotnet pack` deve preservar o intervalo de versão de dependência no nupkg criado (mesmo se a versão flutuante for usada)- [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="70749-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="70749-157">`dotnet restore`falha na origem autenticada quando a configuração no nível do usuário também tem [#7209](https://github.com/NuGet/Home/issues/7209) de origem</span><span class="sxs-lookup"><span data-stu-id="70749-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="70749-158">O pacote não deve restringir o conjunto de BuildActions para arquivos de conteúdo- [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="70749-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="70749-159">Usando um ProjectReference que exige que o AssetTargetFallback tenha sucesso, deve avisar.</span><span class="sxs-lookup"><span data-stu-id="70749-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="70749-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="70749-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="70749-161">Deadlock devido a problemas de Threading ao chamar o CPS (CommonProjectSystem)- [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="70749-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="70749-162">`dotnet add package` Não usa credenciais da configuração global para uma origem especificada na configuração local- [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="70749-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="70749-163">Problemas de Threading com o MEF sendo chamado em caminhos de código assíncrono- [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="70749-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="70749-164">Assinatura: erro relatado duas vezes e sem pilha de chamadas- [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="70749-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="70749-165">A instalação de um pacote assinado com um certificado de autenticação não confiável deve mostrar o erro- [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="70749-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="70749-166">Restauração do NuGet incorretamente NoOps quando 2 projetos estão compartilhando Diretório obj- [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="70749-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="70749-167">Não é possível usar PAT com `dotnet restore` no Linux com pacotes do feed autenticado- [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="70749-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="70749-168">dotnet restore falha devido a um feed em todo o computador desabilitado- [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="70749-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="70749-169">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="70749-169">**DCRs**</span></span>

* <span data-ttu-id="70749-170">Aviso de futura remoção do "dotnet do project.jsdo pacote"- [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="70749-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="70749-171">Adicionar um aviso de reprovação para o plug-in de credencial Gen1- [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="70749-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="70749-172">Assinatura: repositório habilitado para exigir a verificação do cliente de cada pacote como assinado pelo repositório – por meio do recurso RepositorySignatures/5.0.0- [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="70749-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="70749-173">limitar o número de solicitação HTTP por origem por meio de NuGet.Config- [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="70749-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="70749-174">O NuGet deve direcionar Net472 (para ajudar a limpar a compilação 16,0 do VSIX) – [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="70749-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="70749-175">PMC: remover comando OpenPackagePage- [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="70749-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="70749-176">Fazer o mapa do NetCoreApp 3,0 para o netstandard 2,1- [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="70749-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="70749-177">Adicionar suporte do netstandard 2.0 a pacotes NuGet. \*- [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="70749-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="70749-178">Permitir que os autores de pacotes definam comportamento transitivo de compilação de ativos- [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="70749-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="70749-179">Suporte ao recurso de filtro de solução VS 2019.</span><span class="sxs-lookup"><span data-stu-id="70749-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="70749-180">Também dá suporte a projeto que não está na solução ou projetos descarregados.</span><span class="sxs-lookup"><span data-stu-id="70749-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="70749-181">Precisa restaurar a solução completa (via CLI ou VS) primeiro [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="70749-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="70749-182">Assemblies do NuGet 5,0 para exigir o .NET 4.7.2 (via alteração de TFM)- [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="70749-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="70749-183">NuGetLicenseData do NuGet. o empacotamento deve ser um tipo público.</span><span class="sxs-lookup"><span data-stu-id="70749-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="70749-184">Atualizar metadados de licença ingeridos de spdx.</span><span class="sxs-lookup"><span data-stu-id="70749-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="70749-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="70749-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="70749-186">Remover configurações obsoletas APIs- [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="70749-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="70749-187">Tempos limite de restauração de solução alternativa em sistemas com 1 [#6742](https://github.com/NuGet/Home/issues/6742) de CPU</span><span class="sxs-lookup"><span data-stu-id="70749-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="70749-188">O NuGet prefere a autenticação NTLM mesmo se houver credenciais na opção NuGet.config-adicionar configuração para filtrar tipos de autenticação para credenciais- [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="70749-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="70749-189">Habilitar EmbedInteropTypes para PackageReference (Packages.Config capacidade de correspondência) – [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="70749-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="70749-190">**[Lista de todos os problemas corrigidos nesta versão-5,0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="70749-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="70749-191">Resumo: o que há de novo no 5.0.2</span><span class="sxs-lookup"><span data-stu-id="70749-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="70749-192">Segurança (quando executado via dotnet.exe ou mono.exe)-a pasta obj deve ser criada com as permissões corretas [#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="70749-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="70749-193">A restauração de nuget.exe em mono/MacOS falha com nuget.config personalizado e `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span><span class="sxs-lookup"><span data-stu-id="70749-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="70749-194">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="70749-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="70749-195">Os pacotes em FallbackFolders instalados pelo SDK .NET Core são instalados de forma personalizada e falham ao validar a assinatura.</span><span class="sxs-lookup"><span data-stu-id="70749-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="70749-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="70749-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="70749-197">Problema</span><span class="sxs-lookup"><span data-stu-id="70749-197">Issue</span></span>
<span data-ttu-id="70749-198">Ao usar o dotnet.exe 2.x para restaurar um projeto que fará o direcionamento múltiplo para netcoreapp 1.x e netcoreapp 2.x, a pasta de fallback será tratada como um feed de arquivos.</span><span class="sxs-lookup"><span data-stu-id="70749-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="70749-199">Isso significa que, ao restaurar, o NuGet escolherá o pacote da pasta de fallback e tentará instalá-lo na pasta de pacotes globais e fazer a validação de assinatura usual que falha.</span><span class="sxs-lookup"><span data-stu-id="70749-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="70749-200">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="70749-200">Workaround</span></span>
<span data-ttu-id="70749-201">Desabilite o uso da pasta de fallback definindo o `RestoreAdditionalProjectSources` como nada:</span><span class="sxs-lookup"><span data-stu-id="70749-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="70749-202">Use isso com cuidado, pois os pacotes que seriam restaurados da pasta de fallback agora serão baixados de NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="70749-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>