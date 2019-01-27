---
title: Notas de versão prévia 5.0 do NuGet
description: Notas de versão para as visualizações do NuGet 5.0 incluindo problemas conhecidos, correções de bug, novos recursos e DCRs.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: ed3294f88ff99d5e26f630bdbca03aa8446b6e7f
ms.sourcegitcommit: 0cb4c9853cde3647291062eadee2298dd273311e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2019
ms.locfileid: "55084932"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="ad52e-103">Notas de versão do NuGet versão prévia 5.0</span><span class="sxs-lookup"><span data-stu-id="ad52e-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="ad52e-104">Resumo: O que há de novo no 5.0 Preview 2</span><span class="sxs-lookup"><span data-stu-id="ad52e-104">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ad52e-105">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="ad52e-105">Issues fixed in this release</span></span>

#### <a name="bugs"></a><span data-ttu-id="ad52e-106">Bugs:</span><span class="sxs-lookup"><span data-stu-id="ad52e-106">Bugs:</span></span>

* <span data-ttu-id="ad52e-107">O VS do 16.0 UI NuGet tem guias ilegíveis devido a problemas de cor - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="ad52e-107">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="ad52e-108">NuGet. Core & esclarecimento Clients License - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="ad52e-108">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="ad52e-109">Restauração desnecessariamente enumera a pasta de pacote global na tentativa de determinar o tipo - [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="ad52e-109">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="ad52e-110">Erros de imposição de arquivo de bloqueio deverá aparecer na janela de lista de erros - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="ad52e-110">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="ad52e-111">Corrigir problemas de NuGet.Configuration - [7326 #](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="ad52e-111">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="ad52e-112">Adaptar-se a atualização do MSBuild é um local de instalação.</span><span class="sxs-lookup"><span data-stu-id="ad52e-112">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="ad52e-113">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="ad52e-113">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="ad52e-114">NuGet.Build.Tasks.Pack deve ser uma dependência de desenvolvimento - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="ad52e-114">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="ad52e-115">Adicionar ponto de extensão do pacote para a inclusão de depurar símbolos - [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="ad52e-115">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="ad52e-116">dotnet pack deve preservar o intervalo de versão de dependência no nupkg criado.</span><span class="sxs-lookup"><span data-stu-id="ad52e-116">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="ad52e-117">(mesmo se for usada a versão flutuante) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="ad52e-117">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="ad52e-118">restauração do dotnet falhará em fonte autenticada quando config de nível de usuário também tem origem - [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="ad52e-118">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="ad52e-119">Pacote não deve restringir o conjunto de BuildActions para arquivos de conteúdo - [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="ad52e-119">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="ad52e-120">Usando um projectreference que exige AssetTargetFallback tenha êxito, deverá avisar.</span><span class="sxs-lookup"><span data-stu-id="ad52e-120">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="ad52e-121"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="ad52e-121"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="ad52e-122">Deadlock devido a problemas de threading durante uma chamada a CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="ad52e-122">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="ad52e-123">dotnet Adicionar pacote não usa as credenciais de configuração global para uma fonte especificada na configuração local – [6935 #](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="ad52e-123">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="ad52e-124">Problemas de Threading com MEF que está sendo chamado em caminhos do código assíncrono - [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="ad52e-124">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="ad52e-125">De autenticação: erro relatado duas vezes e sem a pilha de chamadas - [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="ad52e-125">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="ad52e-126">Instalar um pacote assinado com um certificado de assinatura não confiável deve mostrar o erro - [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="ad52e-126">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="ad52e-127">Restauração do NuGet incorretamente NoOps quando 2 projetos estão compartilhando a pasta obj - [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="ad52e-127">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="ad52e-128">Não é possível usar PAT com o comando dotnet restore no Linux com pacotes de feed autenticado - [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="ad52e-128">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="ad52e-129">dotnet restore falha devido a ampla de máquina desabilitada feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="ad52e-129">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

#### <a name="dcrs"></a><span data-ttu-id="ad52e-130">DCRs</span><span class="sxs-lookup"><span data-stu-id="ad52e-130">DCRs</span></span>

* <span data-ttu-id="ad52e-131">Assemblies de NuGet 5.0 para exigir o .NET 4.7.2 (por meio da alteração TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="ad52e-131">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="ad52e-132">NuGetLicenseData de Struktury deve ser um tipo público.</span><span class="sxs-lookup"><span data-stu-id="ad52e-132">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="ad52e-133">Atualize metadados de licença ingeridos de spdx.</span><span class="sxs-lookup"><span data-stu-id="ad52e-133">Update license metadata ingested from spdx.</span></span><span data-ttu-id="ad52e-134"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="ad52e-134"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="ad52e-135">Remover APIs obsoletas de configurações - [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="ad52e-135">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="ad52e-136">Solução alternativa tempos limite de restauração em sistemas com 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="ad52e-136">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="ad52e-137">NuGet prefere autenticação NTLM, mesmo se houver credenciais no NuGet. config - adicionar a opção de configuração para os tipos de autenticação de filtro para credenciais - [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="ad52e-137">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="ad52e-138">Habilitar EmbedInteropTypes para PackageReference (recurso de Packages. config correspondente) - [2365 #](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="ad52e-138">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="ad52e-139">Lista de todos os problemas corrigidos 5.0.0-preview2 esta versão</span><span class="sxs-lookup"><span data-stu-id="ad52e-139">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")


## <a name="known-issues"></a><span data-ttu-id="ad52e-140">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="ad52e-140">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="ad52e-141">dotnet nuget push –-a interatividade gera um erro no Mac.</span><span class="sxs-lookup"><span data-stu-id="ad52e-141">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="ad52e-142"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="ad52e-142"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="ad52e-143">Problema</span><span class="sxs-lookup"><span data-stu-id="ad52e-143">Issue</span></span>
<span data-ttu-id="ad52e-144">O argumento `--interactive` não está sendo encaminhado pela cli do dotnet, resultando no erro `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="ad52e-144">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="ad52e-145">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="ad52e-145">Workaround</span></span>
<span data-ttu-id="ad52e-146">Execute qualquer outro comando dotnet com a opção interativa, como `dotnet restore --interactive`, e autentique.</span><span class="sxs-lookup"><span data-stu-id="ad52e-146">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="ad52e-147">A autenticação deve ser armazenada em cache pelo provedor das credenciais.</span><span class="sxs-lookup"><span data-stu-id="ad52e-147">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="ad52e-148">Em seguida, execute `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="ad52e-148">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="ad52e-149">Os pacotes em FallbackFolders instalados pelo SDK .NET Core são instalados de forma personalizada e falham ao validar a assinatura.</span><span class="sxs-lookup"><span data-stu-id="ad52e-149">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="ad52e-150"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="ad52e-150"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="ad52e-151">Problema</span><span class="sxs-lookup"><span data-stu-id="ad52e-151">Issue</span></span>
<span data-ttu-id="ad52e-152">Ao usar o dotnet.exe 2.x para restaurar um projeto que fará o direcionamento múltiplo para netcoreapp 1.x e netcoreapp 2.x, a pasta de fallback será tratada como um feed de arquivos.</span><span class="sxs-lookup"><span data-stu-id="ad52e-152">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="ad52e-153">Isso significa que, ao restaurar, o NuGet escolherá o pacote da pasta de fallback e tentará instalá-lo na pasta de pacotes globais e fazer a validação de assinatura usual que falha.</span><span class="sxs-lookup"><span data-stu-id="ad52e-153">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="ad52e-154">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="ad52e-154">Workaround</span></span>
<span data-ttu-id="ad52e-155">Desabilite a pasta de fallback configurando `RestoreAdditionalProjectSources` como nada.</span><span class="sxs-lookup"><span data-stu-id="ad52e-155">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="ad52e-156">`<RestoreAdditionalProjectSources/>` Use essa opção com cuidado porque ela pode fazer com que muitos dos pacotes sejam baixados do NuGet.org, os quais, normalmente, seriam restaurados da pasta de fallback.</span><span class="sxs-lookup"><span data-stu-id="ad52e-156">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
