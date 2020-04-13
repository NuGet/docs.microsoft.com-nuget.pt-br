---
title: Notas de Versão do NuGet 4.0 RC
description: Notas de versão do NuGet 4.0 RC incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 2d0bb6356c0a20843bdc884b68f5f61838b82e73
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496638"
---
# <a name="nuget-40-rc-release-notes"></a><span data-ttu-id="c0609-103">Notas de Versão do NuGet 4.0 RC</span><span class="sxs-lookup"><span data-stu-id="c0609-103">NuGet 4.0 RC Release Notes</span></span>

[<span data-ttu-id="c0609-104">Notas de Versão do NuGet 3.5 RTM</span><span class="sxs-lookup"><span data-stu-id="c0609-104">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="c0609-105">O [NuGet 4.0 RC para Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) se concentra em adicionar suporte para cenários do .NET Core, abordando os principais comentários dos clientes e melhorando o desempenho de uma variedade de cenários.</span><span class="sxs-lookup"><span data-stu-id="c0609-105">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="c0609-106">Esta versão proporciona várias melhorias, como suporte para PackageReference, comandos do NuGet como destinos do MSBuild, restauração do pacote em segundo plano e muito mais.</span><span class="sxs-lookup"><span data-stu-id="c0609-106">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="c0609-107">Correções de bugs</span><span class="sxs-lookup"><span data-stu-id="c0609-107">Bug Fixes</span></span>

- <span data-ttu-id="c0609-108">Alterações de comportamento em `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span><span class="sxs-lookup"><span data-stu-id="c0609-108">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

- <span data-ttu-id="c0609-109">Restauração do nuget.exe no computador do vs "15" somente falha – [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="c0609-109">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

- <span data-ttu-id="c0609-110">O novo projeto do .NETCore deve bloquear o build durante a restauração – [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="c0609-110">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

- <span data-ttu-id="c0609-111">Aplicativo Web do ASP.NET Core migrado do VS2015 para VS "15", não é possível restaurar.</span><span class="sxs-lookup"><span data-stu-id="c0609-111">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="c0609-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="c0609-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

- <span data-ttu-id="c0609-113">[Falha de Teste]O pacote ‘jQuery Validation’ não pode ser desinstalado pela interface do usuário do PM – [#3755](https://github.com/NuGet/Home/issues/3755)</span><span class="sxs-lookup"><span data-stu-id="c0609-113">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

- <span data-ttu-id="c0609-114">Quando um pacote é instalado para a UWP `project.json`, os projetos pai também devem ser restaurados – [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="c0609-114">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

- <span data-ttu-id="c0609-115">Modificar os destinos do NuGet para registrar as origens de pacote como Alto detalhamento em vez de Normal – [#3719](https://github.com/NuGet/Home/issues/3719)</span><span class="sxs-lookup"><span data-stu-id="c0609-115">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

- <span data-ttu-id="c0609-116">dotnet</span><span class="sxs-lookup"><span data-stu-id="c0609-116">dotnet</span></span>
  - <span data-ttu-id="c0609-117">dotnetcore pack3 deve incluir a documentação de XML por padrão – [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="c0609-117">dotnetcore pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

- <span data-ttu-id="c0609-118">Falha da atualização em lote da interface do usuário quando a origem sem o pacote é a primeira e a origem Todos é selecionada – [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="c0609-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

- <span data-ttu-id="c0609-119">O comando Nuget pack não inclui todos os arquivos – [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="c0609-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

- <span data-ttu-id="c0609-120">Problema do OOM – [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="c0609-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

- <span data-ttu-id="c0609-121">A seção de ProjectFileDependencyGroups do arquivo de ativos deve usar nomes de biblioteca para projetos – [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="c0609-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

- <span data-ttu-id="c0609-122">“dotnet restore” e diretórios recursivos – [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="c0609-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

- <span data-ttu-id="c0609-123">Falhas do Restore3 são registradas como avisos em vez de erros – [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="c0609-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

- <span data-ttu-id="c0609-124">Problema do TFS: “O [file] não pode ser encontrado no seu workspace ou você não tem permissão para acessá-lo.” – [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="c0609-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

- <span data-ttu-id="c0609-125">Digitar “nuget <packagename>“ na caixa de pesquisa de início rápido do vs mantém o prefixo “nuget” – [#2719](https://github.com/NuGet/Home/issues/2719)</span><span class="sxs-lookup"><span data-stu-id="c0609-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

- <span data-ttu-id="c0609-126">System.Xml.XmlException: elemento raiz não reconhecido na parte Core Properties.</span><span class="sxs-lookup"><span data-stu-id="c0609-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="c0609-127">Linha 2, posição 2.</span><span class="sxs-lookup"><span data-stu-id="c0609-127">Line 2, position 2.</span></span><span data-ttu-id="c0609-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="c0609-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

- <span data-ttu-id="c0609-129">`.nuspec` com &lt; ou &gt; de escape em campos de texto não é mais compilado – [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="c0609-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

- <span data-ttu-id="c0609-130">A exclusão do nuget.exe não solicita credenciais (está no modo não interativo) – [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="c0609-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

- <span data-ttu-id="c0609-131">A exclusão do nuget.exe avisa sobre a Chave de API para origens locais, mesmo que isso não faça sentido – [#2625](https://github.com/NuGet/Home/issues/2625)</span><span class="sxs-lookup"><span data-stu-id="c0609-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

- <span data-ttu-id="c0609-132">Erro de experiência ruim ao instalar o pacote EF -pre – [#2566](https://github.com/NuGet/Home/issues/2566)</span><span class="sxs-lookup"><span data-stu-id="c0609-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

- <span data-ttu-id="c0609-133">O Visual Studio travou ao tentar alterar a seleção no Gerenciador de Pacotes – [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="c0609-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

- <span data-ttu-id="c0609-134">dotnet</span><span class="sxs-lookup"><span data-stu-id="c0609-134">dotnet</span></span>
  - <span data-ttu-id="c0609-135">dotnetcore restore realiza pesquisas de ID que diferenciam maiúsculas de minúsculas nos repositórios locais de lista plana quando versões flutuantes são usadas – [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="c0609-135">dotnetcore restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

- <span data-ttu-id="c0609-136">A exclusão nuget.exe está interrompida para feed V2 ‑ [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="c0609-136">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

- <span data-ttu-id="c0609-137">O tempo limite de push do nuget.exe precisa de uma mensagem de erro melhor – [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="c0609-137">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

- <span data-ttu-id="c0609-138">A restauração da ferramenta sem as devidas importações falha silenciosamente.</span><span class="sxs-lookup"><span data-stu-id="c0609-138">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="c0609-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="c0609-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

- <span data-ttu-id="c0609-140">O NuGet solicita as credenciais quando há um feed privado mesmo ao instalar do nuget.org – [#2346](https://github.com/NuGet/Home/issues/2346)</span><span class="sxs-lookup"><span data-stu-id="c0609-140">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

- <span data-ttu-id="c0609-141">O pacote do ApplicationInsights 2.0 é listado, mas ainda não existe – [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="c0609-141">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

- <span data-ttu-id="c0609-142">UIDelay no VS "15" preview branch 5 – [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="c0609-142">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

- <span data-ttu-id="c0609-143">O primeiro evento OnBuild é perdido para a Restauração durante o Build para UWP – [#3489](https://github.com/NuGet/Home/issues/3489)</span><span class="sxs-lookup"><span data-stu-id="c0609-143">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

- <span data-ttu-id="c0609-144">O PowerShell5 interrompe a instalação do EntityFramework?</span><span class="sxs-lookup"><span data-stu-id="c0609-144">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="c0609-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="c0609-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

- <span data-ttu-id="c0609-146">Adicionar origem ao log detalhado (considere para 3.5) – [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="c0609-146">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

- <span data-ttu-id="c0609-147">O parâmetro NoCache não é observado na versão de cliente do nuget 3.4 ou superior – [#3074](https://github.com/NuGet/Home/issues/3074)</span><span class="sxs-lookup"><span data-stu-id="c0609-147">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

- <span data-ttu-id="c0609-148">Quando um provedor de credenciais falha ao carregar no VS, não interrompa o NuGet – [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="c0609-148">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>

## <a name="features"></a><span data-ttu-id="c0609-149">Recursos</span><span class="sxs-lookup"><span data-stu-id="c0609-149">Features</span></span>

- <span data-ttu-id="c0609-150">Configurar o IC para executar x86 – [#3868](https://github.com/NuGet/Home/issues/3868)</span><span class="sxs-lookup"><span data-stu-id="c0609-150">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

- <span data-ttu-id="c0609-151">Restauração automática 3/3: interface do usuário sem bloqueio – [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="c0609-151">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

- <span data-ttu-id="c0609-152">Restauração automática 2/3: restauração em segundo plano na indicação – [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="c0609-152">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

- <span data-ttu-id="c0609-153">Restaurar referências de projeto para corresponder ao comportamento de build (repetir) – [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="c0609-153">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

- <span data-ttu-id="c0609-154">Suporte a DPL no VS "15" – minbar – [#3614](https://github.com/NuGet/Home/issues/3614)</span><span class="sxs-lookup"><span data-stu-id="c0609-154">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

- <span data-ttu-id="c0609-155">Mover o arquivo de configurações para Arquivos de Programas – [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="c0609-155">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

- <span data-ttu-id="c0609-156">Objetos e destinos de restauração gerados precisam de suporte para a participação de direcionamento cruzado – [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="c0609-156">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

- <span data-ttu-id="c0609-157">Suporte à restauração do NuGet para PackageTargetFallback (importações f.k.a) – [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="c0609-157">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

- <span data-ttu-id="c0609-158">Implementação ToolsRef – [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="c0609-158">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

- <span data-ttu-id="c0609-159">Restore3 para um RID – [#3465](https://github.com/NuGet/Home/issues/3465)</span><span class="sxs-lookup"><span data-stu-id="c0609-159">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

- <span data-ttu-id="c0609-160">Interface do usuário do NuGet para dar suporte à Adição/Remoção/Atualização de PackageRefs – [#3457](https://github.com/NuGet/Home/issues/3457)</span><span class="sxs-lookup"><span data-stu-id="c0609-160">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

- <span data-ttu-id="c0609-161">Restauração automática 1/3: implementação da API de indicação por meio de cache das informações de restauração de projeto – [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="c0609-161">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

- <span data-ttu-id="c0609-162">[0] Tarefa e destinos de restauração do NuGet – [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="c0609-162">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

- <span data-ttu-id="c0609-163">[1] Habilitar a restauração no nível da solução no MSBuild – [#2993](https://github.com/NuGet/Home/issues/2993)</span><span class="sxs-lookup"><span data-stu-id="c0609-163">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

- <span data-ttu-id="c0609-164">Suporte à extensibilidade pública do provedor de credenciais no Visual Studio – [#2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="c0609-164">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

- <span data-ttu-id="c0609-165">Restauração de nuget recursiva – [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="c0609-165">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

- <span data-ttu-id="c0609-166">Não é possível carregar o Microsoft.TeamFoundation.Client dev15, é necessário atualizar a versão do Microsoft.TeamFoundation.Client para 15.0 para o VS "15" Preview – [#2392](https://github.com/NuGet/Home/issues/2392)</span><span class="sxs-lookup"><span data-stu-id="c0609-166">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

- <span data-ttu-id="c0609-167">Não é possível instalar o pacote C++ para um projeto UWP C++ no VS "15" Preview – [#2369](https://github.com/NuGet/Home/issues/2369)</span><span class="sxs-lookup"><span data-stu-id="c0609-167">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

- <span data-ttu-id="c0609-168">O Nupkg precisa dar suporte à pasta \buildCrossTargeting\ – e importar `.targets` / `.props` para escopo de “multiplataforma” do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="c0609-168">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="c0609-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="c0609-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

- <span data-ttu-id="c0609-170">Design de ToolsReference – [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="c0609-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

- <span data-ttu-id="c0609-171">Corrigir a interface do usuário do NuGet para dar suporte à restauração com PackageReferences em `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span><span class="sxs-lookup"><span data-stu-id="c0609-171">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

- <span data-ttu-id="c0609-172">Adicionar o botão Limpar cache às configurações do gerenciador de pacotes do VS – [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="c0609-172">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="c0609-173">DCRs</span><span class="sxs-lookup"><span data-stu-id="c0609-173">DCRs</span></span>

- <span data-ttu-id="c0609-174">A Restauração de solução deve ser bloqueada enquanto restauração automática está em andamento.</span><span class="sxs-lookup"><span data-stu-id="c0609-174">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="c0609-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="c0609-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

- <span data-ttu-id="c0609-176">A instalação NetCore da interface do usuário do Gerenciador de Pacotes do NuGet é instalada em todos os TFM, em vez daqueles compatíveis com o pacote – [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="c0609-176">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

- <span data-ttu-id="c0609-177">A API do indicador de restauração também precisa ser compatível com o DotNetCliToolsReferences.</span><span class="sxs-lookup"><span data-stu-id="c0609-177">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="c0609-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="c0609-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

- <span data-ttu-id="c0609-179">Marcar nosso VS "15" vsix como um systemcomponent – [#3700](https://github.com/NuGet/Home/issues/3700)</span><span class="sxs-lookup"><span data-stu-id="c0609-179">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

- <span data-ttu-id="c0609-180">Migrar do MS.VS.Services.Client de referência para MS.VS.Services.Client.Interactive – [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="c0609-180">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

- <span data-ttu-id="c0609-181">$(RestoreLegacyPackagesDirectory) deve ser respeitado no nível de projeto por restauração – [#3618](https://github.com/NuGet/Home/issues/3618)</span><span class="sxs-lookup"><span data-stu-id="c0609-181">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

- <span data-ttu-id="c0609-182">A restauração para o projeto com TargetFramework único não deve condicionar os objetos – [#3588](https://github.com/NuGet/Home/issues/3588)</span><span class="sxs-lookup"><span data-stu-id="c0609-182">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

- <span data-ttu-id="c0609-183">dotnet</span><span class="sxs-lookup"><span data-stu-id="c0609-183">dotnet</span></span>
  - <span data-ttu-id="c0609-184">dotnetcore restore3 foo.csproj deve seguir as dependências de projectref e restaurá-las também.</span><span class="sxs-lookup"><span data-stu-id="c0609-184">dotnetcore restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="c0609-185">Como o build.</span><span class="sxs-lookup"><span data-stu-id="c0609-185">Like build.</span></span><span data-ttu-id="c0609-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="c0609-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

- <span data-ttu-id="c0609-187">"type": dependências "platform" são representadas como "type":"package" no arquivo de bloqueio – [#2695](https://github.com/NuGet/Home/issues/2695)</span><span class="sxs-lookup"><span data-stu-id="c0609-187">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

- <span data-ttu-id="c0609-188">O Modo detalhado do nuget.exe deve mostrar a URL de download – [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="c0609-188">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

- <span data-ttu-id="c0609-189">Mover o xplat do NuGet para o Microsoft.NetCore.App e netcoreapp1.0 – [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="c0609-189">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

- <span data-ttu-id="c0609-190">Push – Deve ser possível substituir o servidor de símbolos ao efetuar push da linha de comando – [#2348](https://github.com/NuGet/Home/issues/2348)</span><span class="sxs-lookup"><span data-stu-id="c0609-190">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

- <span data-ttu-id="c0609-191">Consolidar o código para localizar caminho de pacotes globais – [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="c0609-191">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

- <span data-ttu-id="c0609-192">É necessário um nome melhor que suppressParent – [#2196](https://github.com/NuGet/Home/issues/2196)</span><span class="sxs-lookup"><span data-stu-id="c0609-192">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

- <span data-ttu-id="c0609-193">Determinar o nome da dependência `project.json` a ser usado para projetos do MSBuild – [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="c0609-193">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

- <span data-ttu-id="c0609-194">Adicionar suporte para SemVer 2.0.0 ao NuGet.Core – [#3383](https://github.com/NuGet/Home/issues/3383)</span><span class="sxs-lookup"><span data-stu-id="c0609-194">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

- <span data-ttu-id="c0609-195">Permitir NuPkgs de dependência transitiva com `.targets` disponíveis no MSBuild – [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="c0609-195">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

- <span data-ttu-id="c0609-196">Restauração do NuGet da linha de comando é significativamente mais lenta do que o VS – [#3330](https://github.com/NuGet/Home/issues/3330)</span><span class="sxs-lookup"><span data-stu-id="c0609-196">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

- <span data-ttu-id="c0609-197">Não diferenciação de maiúsculas e minúsculas na comparação de ID e a versão do pacote – [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="c0609-197">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

- <span data-ttu-id="c0609-198">A opção NoCache não funciona para restauração/instalação baseada em `packages.config` (GlobalPackagesFolder) – [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="c0609-198">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

- <span data-ttu-id="c0609-199">O recurso FindPackageByIdResource precisa de um contexto de cache padrão e agente – [#1357](https://github.com/NuGet/Home/issues/1357)</span><span class="sxs-lookup"><span data-stu-id="c0609-199">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
