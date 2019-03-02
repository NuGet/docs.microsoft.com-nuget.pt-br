---
title: Notas de versão prévia 5.0 do NuGet
description: Notas de versão para as visualizações do NuGet 5.0 incluindo problemas conhecidos, correções de bug, novos recursos e DCRs.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 4b05dcb9a2960c1e3231e81d4b4c122d3a518753
ms.sourcegitcommit: 571644118e3c5a2fd818891d305b4b8de8ef21de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2019
ms.locfileid: "57225882"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="30b22-103">Notas de versão do NuGet versão prévia 5.0</span><span class="sxs-lookup"><span data-stu-id="30b22-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="30b22-104">Versões de visualização 5.0 do NuGet</span><span class="sxs-lookup"><span data-stu-id="30b22-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="30b22-105">27 de fevereiro de 2019 - [NuGet 5.0 visualização 4](#whats-new-in-nuget-50-preview-4)</span><span class="sxs-lookup"><span data-stu-id="30b22-105">February 27, 2019 - [NuGet 5.0 Preview 4](#whats-new-in-nuget-50-preview-4)</span></span>
* <span data-ttu-id="30b22-106">13 de fevereiro de 2019 - [NuGet 5.0 Preview 3](#whats-new-in-nuget-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="30b22-106">February 13, 2019 - [NuGet 5.0 Preview 3](#whats-new-in-nuget-50-preview-3)</span></span>
* <span data-ttu-id="30b22-107">23 de janeiro de 2019 - [NuGet 5.0 Preview 2](#whats-new-in-nuget-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="30b22-107">January 23, 2019 - [NuGet 5.0 Preview 2](#whats-new-in-nuget-50-preview-2)</span></span>

## <a name="whats-new-in-nuget-50-preview-4"></a><span data-ttu-id="30b22-108">O que há de novo no NuGet 5.0 visualização 4</span><span class="sxs-lookup"><span data-stu-id="30b22-108">What's New in NuGet 5.0 Preview 4</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="30b22-109">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="30b22-109">Issues fixed in this release</span></span>

<span data-ttu-id="30b22-110">**•s**</span><span class="sxs-lookup"><span data-stu-id="30b22-110">**Bugs**</span></span>

* <span data-ttu-id="30b22-111">NuGet.VisualStudio.IVsPackageInstaller - chamada em um projeto com nenhum pacote referencia sempre Packages. config usa, mesmo se o padrão é definido na PackageReference – [7005 #](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="30b22-111">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="30b22-112">PMC: Pacote de atualização reinstalar falhar ("não é possível localizar o pacote") removido da lista de pacotes.</span><span class="sxs-lookup"><span data-stu-id="30b22-112">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="30b22-113"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="30b22-113"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="30b22-114">Adicionar um aviso de terceiros em nosso repositório e VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="30b22-114">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="30b22-115">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage deve instalar a versão mais recente quando nenhuma versão considerando - [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="30b22-115">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="30b22-116">– suporte interativo para dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="30b22-116">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="30b22-117">Quando a restauração do arquivo de bloqueio, o aviso de NU1603 não deve ser gerado.</span><span class="sxs-lookup"><span data-stu-id="30b22-117">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="30b22-118"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="30b22-118"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="30b22-119">O NuGet não deve imprimir o caminho do projeto durante a restauração com log mínimo - [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="30b22-119">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="30b22-120">– suporte interativo para dotnet remover pacote - [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="30b22-120">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="30b22-121">Adicionar de volta NuGet.Packaging.Core com TypeForwardedTo attrs - [7768 #](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="30b22-121">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="30b22-122">plugins_cache precisa de um caminho mais curto para funcionar bem - [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="30b22-122">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="30b22-123">Prefira o caminho para a descoberta do msbuild se o usuário não foi solicitado para a versão do msbuild específicas - [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="30b22-123">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

<span data-ttu-id="30b22-124">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="30b22-124">**DCRs**</span></span>

* <span data-ttu-id="30b22-125">limitar o número de solicitação http por origem por meio do NuGet. config - [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="30b22-125">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="30b22-126">O NuGet deve ter como destino Net472 (para ajudar a limpar a compilação 16.0 do VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="30b22-126">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="30b22-127">PMC: Remover comando OpenPackagePage - [7384 #](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="30b22-127">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="30b22-128">Verifique NetCoreApp 3.0 são mapeados para o NetStandard 2.1 - [7762 #](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="30b22-128">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="30b22-129">Adicionar suporte a netstandard2.0 para pacotes NuGet.\* - [6516 #](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="30b22-129">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>


## <a name="whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="30b22-130">O que há de novo no NuGet 5.0 Preview 3</span><span class="sxs-lookup"><span data-stu-id="30b22-130">What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="30b22-131">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="30b22-131">Issues fixed in this release</span></span> 

<span data-ttu-id="30b22-132">**•s**</span><span class="sxs-lookup"><span data-stu-id="30b22-132">**Bugs**</span></span>

* <span data-ttu-id="30b22-133">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="30b22-133">nuget.exe /?</span></span> <span data-ttu-id="30b22-134">deve listar as versões corretas do msbuild – [7794 #](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="30b22-134">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="30b22-135">NuGet.targets(498,5): error : Não foi possível localizar uma parte do caminho ' / tmp/NuGetScratch - no mono - [7793 #](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="30b22-135">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="30b22-136">restauração desnecessariamente enumera o conteúdo de todas as versões do pacote referenciado no cache do computador - [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="30b22-136">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="30b22-137">Detecção automática de MSBuild sempre seleciona 16.0 após a instalação VS 2019 visualizar - [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="30b22-137">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="30b22-138">pacote do dotnet lista em uma solução gera entradas duplicadas para o framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="30b22-138">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="30b22-139">Exceção "o nome de caminho vazio não é legal" quando chamada IVsPackageInstaller.InstallPackage antigo projetos e pacotes de pasta não existe.</span><span class="sxs-lookup"><span data-stu-id="30b22-139">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="30b22-140"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="30b22-140"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="30b22-141">detalhamento do MSBuild /t: Restore mínimo deve ser mais mínimo - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="30b22-141">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="30b22-142">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="30b22-142">**DCRs**</span></span>

* <span data-ttu-id="30b22-143">Permitir que os autores de pacote definir o comportamento de transitiva de ativos de build - [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="30b22-143">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="30b22-144">Habilitar a restauração no VS para ter êxito se um projeto não é parte da solução ou não está carregado, mas anteriormente foi restaurado - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="30b22-144">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="whats-new-in-nuget-50-preview-2"></a><span data-ttu-id="30b22-145">O que há de novo no NuGet 5.0 Preview 2</span><span class="sxs-lookup"><span data-stu-id="30b22-145">What's New in NuGet 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="30b22-146">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="30b22-146">Issues fixed in this release</span></span>

<span data-ttu-id="30b22-147">**•s**</span><span class="sxs-lookup"><span data-stu-id="30b22-147">**Bugs**</span></span>

* <span data-ttu-id="30b22-148">O VS do 16.0 UI NuGet tem guias ilegíveis devido a problemas de cor - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="30b22-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="30b22-149">NuGet. Core & esclarecimento Clients License - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="30b22-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="30b22-150">Restauração desnecessariamente enumera a pasta de pacote global na tentativa de determinar o tipo - [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="30b22-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="30b22-151">Erros de imposição de arquivo de bloqueio deverá aparecer na janela de lista de erros - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="30b22-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="30b22-152">Corrigir problemas de NuGet.Configuration - [7326 #](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="30b22-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="30b22-153">Adaptar-se a atualização do MSBuild é um local de instalação.</span><span class="sxs-lookup"><span data-stu-id="30b22-153">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="30b22-154">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="30b22-154">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="30b22-155">NuGet.Build.Tasks.Pack deve ser uma dependência de desenvolvimento - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="30b22-155">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="30b22-156">Adicionar ponto de extensão do pacote para a inclusão de depurar símbolos - [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="30b22-156">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="30b22-157">dotnet pack deve preservar o intervalo de versão de dependência no nupkg criado.</span><span class="sxs-lookup"><span data-stu-id="30b22-157">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="30b22-158">(mesmo se for usada a versão flutuante) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="30b22-158">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="30b22-159">restauração do dotnet falhará em fonte autenticada quando config de nível de usuário também tem origem - [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="30b22-159">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="30b22-160">Pacote não deve restringir o conjunto de BuildActions para arquivos de conteúdo - [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="30b22-160">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="30b22-161">Usando um projectreference que exige AssetTargetFallback tenha êxito, deverá avisar.</span><span class="sxs-lookup"><span data-stu-id="30b22-161">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="30b22-162"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="30b22-162"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="30b22-163">Deadlock devido a problemas de threading durante uma chamada a CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="30b22-163">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="30b22-164">dotnet Adicionar pacote não usa as credenciais de configuração global para uma fonte especificada na configuração local – [6935 #](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="30b22-164">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="30b22-165">Problemas de Threading com MEF que está sendo chamado em caminhos do código assíncrono - [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="30b22-165">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="30b22-166">De autenticação: erro relatado duas vezes e sem a pilha de chamadas - [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="30b22-166">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="30b22-167">Instalar um pacote assinado com um certificado de assinatura não confiável deve mostrar o erro - [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="30b22-167">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="30b22-168">Restauração do NuGet incorretamente NoOps quando 2 projetos estão compartilhando a pasta obj - [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="30b22-168">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="30b22-169">Não é possível usar PAT com o comando dotnet restore no Linux com pacotes de feed autenticado - [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="30b22-169">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="30b22-170">dotnet restore falha devido a ampla de máquina desabilitada feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="30b22-170">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="30b22-171">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="30b22-171">**DCRs**</span></span>

* <span data-ttu-id="30b22-172">Assemblies de NuGet 5.0 para exigir o .NET 4.7.2 (por meio da alteração TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="30b22-172">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="30b22-173">NuGetLicenseData de Struktury deve ser um tipo público.</span><span class="sxs-lookup"><span data-stu-id="30b22-173">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="30b22-174">Atualize metadados de licença ingeridos de spdx.</span><span class="sxs-lookup"><span data-stu-id="30b22-174">Update license metadata ingested from spdx.</span></span><span data-ttu-id="30b22-175"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="30b22-175"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="30b22-176">Remover APIs obsoletas de configurações - [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="30b22-176">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="30b22-177">Solução alternativa tempos limite de restauração em sistemas com 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="30b22-177">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="30b22-178">NuGet prefere autenticação NTLM, mesmo se houver credenciais no NuGet. config - adicionar a opção de configuração para os tipos de autenticação de filtro para credenciais - [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="30b22-178">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="30b22-179">Habilitar EmbedInteropTypes para PackageReference (recurso de Packages. config correspondente) - [2365 #](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="30b22-179">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="30b22-180">Lista de todos os problemas corrigidos 5.0.0-preview2 esta versão</span><span class="sxs-lookup"><span data-stu-id="30b22-180">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="30b22-181">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="30b22-181">Known issues</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="30b22-182">Os pacotes em FallbackFolders instalados pelo SDK .NET Core são instalados de forma personalizada e falham ao validar a assinatura.</span><span class="sxs-lookup"><span data-stu-id="30b22-182">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="30b22-183"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="30b22-183"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="30b22-184">**Problema** ao usar dotnet.exe 2.x para restaurar um projeto que netcoreapp vários destinos 1.x e netcoreapp 2. x, a pasta de fallback é tratado como um arquivo de feed.</span><span class="sxs-lookup"><span data-stu-id="30b22-184">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="30b22-185">Isso significa que, ao restaurar, o NuGet escolherá o pacote da pasta de fallback e tentará instalá-lo na pasta de pacotes globais e fazer a validação de assinatura usual que falha.</span><span class="sxs-lookup"><span data-stu-id="30b22-185">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="30b22-186">**Solução alternativa** desabilitar o uso da pasta de fallback, definindo o `RestoreAdditionalProjectSources` como nothing.</span><span class="sxs-lookup"><span data-stu-id="30b22-186">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="30b22-187">`<RestoreAdditionalProjectSources/>` Use essa opção com cuidado porque ela pode fazer com que muitos dos pacotes sejam baixados do NuGet.org, os quais, normalmente, seriam restaurados da pasta de fallback.</span><span class="sxs-lookup"><span data-stu-id="30b22-187">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
