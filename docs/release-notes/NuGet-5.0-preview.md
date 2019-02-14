---
title: Notas de versão prévia 5.0 do NuGet
description: Notas de versão para as visualizações do NuGet 5.0 incluindo problemas conhecidos, correções de bug, novos recursos e DCRs.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 5889ea52f993fa8fe841f8eb83b6da659cdede93
ms.sourcegitcommit: 1ab750ff17e55c763d646c50e7630138804ce8b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247653"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="c84c8-103">Notas de versão do NuGet versão prévia 5.0</span><span class="sxs-lookup"><span data-stu-id="c84c8-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="c84c8-104">Versões de visualização 5.0 do NuGet</span><span class="sxs-lookup"><span data-stu-id="c84c8-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="c84c8-105">13 de fevereiro de 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="c84c8-105">February 13, 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span></span>
* <span data-ttu-id="c84c8-106">23 de janeiro de 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="c84c8-106">January 23, 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span></span>

## <a name="summary-whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="c84c8-107">Resumo: O que há de novo no NuGet 5.0 Preview 3</span><span class="sxs-lookup"><span data-stu-id="c84c8-107">Summary: What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="c84c8-108">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="c84c8-108">Issues fixed in this release</span></span> 

<span data-ttu-id="c84c8-109">**Bugs:**</span><span class="sxs-lookup"><span data-stu-id="c84c8-109">**Bugs:**</span></span>

* <span data-ttu-id="c84c8-110">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="c84c8-110">nuget.exe /?</span></span> <span data-ttu-id="c84c8-111">deve listar as versões corretas do msbuild – [7794 #](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="c84c8-111">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="c84c8-112">NuGet.targets(498,5): error : Não foi possível localizar uma parte do caminho ' / tmp/NuGetScratch - no mono - [7793 #](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="c84c8-112">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="c84c8-113">restauração desnecessariamente enumera o conteúdo de todas as versões do pacote referenciado no cache do computador - [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="c84c8-113">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="c84c8-114">Detecção automática de MSBuild sempre seleciona 16.0 após a instalação VS 2019 visualizar - [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="c84c8-114">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="c84c8-115">pacote do dotnet lista em uma solução gera entradas duplicadas para o framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="c84c8-115">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="c84c8-116">Exceção "o nome de caminho vazio não é legal" quando chamada IVsPackageInstaller.InstallPackage antigo projetos e pacotes de pasta não existe.</span><span class="sxs-lookup"><span data-stu-id="c84c8-116">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="c84c8-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="c84c8-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="c84c8-118">detalhamento do MSBuild /t: Restore mínimo deve ser mais mínimo - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="c84c8-118">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="c84c8-119">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="c84c8-119">**DCRs**</span></span>

* <span data-ttu-id="c84c8-120">Permitir que os autores de pacote definir o comportamento de transitiva de ativos de build - [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="c84c8-120">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="c84c8-121">Habilitar a restauração no VS para ter êxito se um projeto não é parte da solução ou não está carregado, mas anteriormente foi restaurado - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="c84c8-121">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="c84c8-122">Resumo: O que há de novo no 5.0 Preview 2</span><span class="sxs-lookup"><span data-stu-id="c84c8-122">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="c84c8-123">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="c84c8-123">Issues fixed in this release</span></span>

<span data-ttu-id="c84c8-124">**Bugs:**</span><span class="sxs-lookup"><span data-stu-id="c84c8-124">**Bugs:**</span></span>

* <span data-ttu-id="c84c8-125">O VS do 16.0 UI NuGet tem guias ilegíveis devido a problemas de cor - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="c84c8-125">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="c84c8-126">NuGet. Core & esclarecimento Clients License - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="c84c8-126">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="c84c8-127">Restauração desnecessariamente enumera a pasta de pacote global na tentativa de determinar o tipo - [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="c84c8-127">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="c84c8-128">Erros de imposição de arquivo de bloqueio deverá aparecer na janela de lista de erros - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="c84c8-128">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="c84c8-129">Corrigir problemas de NuGet.Configuration - [7326 #](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="c84c8-129">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="c84c8-130">Adaptar-se a atualização do MSBuild é um local de instalação.</span><span class="sxs-lookup"><span data-stu-id="c84c8-130">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="c84c8-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="c84c8-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="c84c8-132">NuGet.Build.Tasks.Pack deve ser uma dependência de desenvolvimento - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="c84c8-132">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="c84c8-133">Adicionar ponto de extensão do pacote para a inclusão de depurar símbolos - [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="c84c8-133">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="c84c8-134">dotnet pack deve preservar o intervalo de versão de dependência no nupkg criado.</span><span class="sxs-lookup"><span data-stu-id="c84c8-134">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="c84c8-135">(mesmo se for usada a versão flutuante) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="c84c8-135">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="c84c8-136">restauração do dotnet falhará em fonte autenticada quando config de nível de usuário também tem origem - [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="c84c8-136">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="c84c8-137">Pacote não deve restringir o conjunto de BuildActions para arquivos de conteúdo - [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="c84c8-137">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="c84c8-138">Usando um projectreference que exige AssetTargetFallback tenha êxito, deverá avisar.</span><span class="sxs-lookup"><span data-stu-id="c84c8-138">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="c84c8-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="c84c8-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="c84c8-140">Deadlock devido a problemas de threading durante uma chamada a CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="c84c8-140">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="c84c8-141">dotnet Adicionar pacote não usa as credenciais de configuração global para uma fonte especificada na configuração local – [6935 #](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="c84c8-141">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="c84c8-142">Problemas de Threading com MEF que está sendo chamado em caminhos do código assíncrono - [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="c84c8-142">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="c84c8-143">De autenticação: erro relatado duas vezes e sem a pilha de chamadas - [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="c84c8-143">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="c84c8-144">Instalar um pacote assinado com um certificado de assinatura não confiável deve mostrar o erro - [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="c84c8-144">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="c84c8-145">Restauração do NuGet incorretamente NoOps quando 2 projetos estão compartilhando a pasta obj - [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="c84c8-145">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="c84c8-146">Não é possível usar PAT com o comando dotnet restore no Linux com pacotes de feed autenticado - [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="c84c8-146">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="c84c8-147">dotnet restore falha devido a ampla de máquina desabilitada feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="c84c8-147">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="c84c8-148">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="c84c8-148">**DCRs**</span></span>

* <span data-ttu-id="c84c8-149">Assemblies de NuGet 5.0 para exigir o .NET 4.7.2 (por meio da alteração TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="c84c8-149">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="c84c8-150">NuGetLicenseData de Struktury deve ser um tipo público.</span><span class="sxs-lookup"><span data-stu-id="c84c8-150">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="c84c8-151">Atualize metadados de licença ingeridos de spdx.</span><span class="sxs-lookup"><span data-stu-id="c84c8-151">Update license metadata ingested from spdx.</span></span><span data-ttu-id="c84c8-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="c84c8-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="c84c8-153">Remover APIs obsoletas de configurações - [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="c84c8-153">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="c84c8-154">Solução alternativa tempos limite de restauração em sistemas com 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="c84c8-154">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="c84c8-155">NuGet prefere autenticação NTLM, mesmo se houver credenciais no NuGet. config - adicionar a opção de configuração para os tipos de autenticação de filtro para credenciais - [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="c84c8-155">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="c84c8-156">Habilitar EmbedInteropTypes para PackageReference (recurso de Packages. config correspondente) - [2365 #](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="c84c8-156">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="c84c8-157">Lista de todos os problemas corrigidos 5.0.0-preview2 esta versão</span><span class="sxs-lookup"><span data-stu-id="c84c8-157">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="c84c8-158">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="c84c8-158">Known issues</span></span>

#### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="c84c8-159">dotnet nuget push –-a interatividade gera um erro no Mac.</span><span class="sxs-lookup"><span data-stu-id="c84c8-159">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="c84c8-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="c84c8-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>
<span data-ttu-id="c84c8-161">**Problema** as `--interactive` argumento não está sendo encaminhado pela cli do dotnet e resulta no erro `error: Missing value for option 'interactive'` 
 **solução alternativa** executar qualquer outro comando dotnet com a opção interativa, como `dotnet restore --interactive` e se autenticar.</span><span class="sxs-lookup"><span data-stu-id="c84c8-161">**Issue** The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`
**Workaround** Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="c84c8-162">A autenticação deve ser armazenada em cache pelo provedor das credenciais.</span><span class="sxs-lookup"><span data-stu-id="c84c8-162">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="c84c8-163">Em seguida, execute `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="c84c8-163">Then run `dotnet nuget push`.</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="c84c8-164">Os pacotes em FallbackFolders instalados pelo SDK .NET Core são instalados de forma personalizada e falham ao validar a assinatura.</span><span class="sxs-lookup"><span data-stu-id="c84c8-164">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="c84c8-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="c84c8-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="c84c8-166">**Problema** ao usar dotnet.exe 2.x para restaurar um projeto que netcoreapp vários destinos 1.x e netcoreapp 2. x, a pasta de fallback é tratado como um arquivo de feed.</span><span class="sxs-lookup"><span data-stu-id="c84c8-166">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="c84c8-167">Isso significa que, ao restaurar, o NuGet escolherá o pacote da pasta de fallback e tentará instalá-lo na pasta de pacotes globais e fazer a validação de assinatura usual que falha.</span><span class="sxs-lookup"><span data-stu-id="c84c8-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="c84c8-168">**Solução alternativa** desabilitar o uso da pasta de fallback, definindo o `RestoreAdditionalProjectSources` como nothing.</span><span class="sxs-lookup"><span data-stu-id="c84c8-168">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="c84c8-169">`<RestoreAdditionalProjectSources/>` Use essa opção com cuidado porque ela pode fazer com que muitos dos pacotes sejam baixados do NuGet.org, os quais, normalmente, seriam restaurados da pasta de fallback.</span><span class="sxs-lookup"><span data-stu-id="c84c8-169">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
