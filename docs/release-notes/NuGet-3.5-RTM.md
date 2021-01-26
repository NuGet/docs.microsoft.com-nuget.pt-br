---
title: Notas de Versão do NuGet 3.5 RTM
description: Notas de versão do NuGet 3,5 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776356"
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="9e8fb-103">Notas de versão do NuGet 3,5</span><span class="sxs-lookup"><span data-stu-id="9e8fb-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="9e8fb-104">Notas de versão do [NuGet 3,5-RC](../release-notes/nuget-3.5-RC.md)  |  [Notas de versão do NuGet 4,0 RC](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="9e8fb-105">Correções de bugs</span><span class="sxs-lookup"><span data-stu-id="9e8fb-105">Bug Fixes</span></span>

* <span data-ttu-id="9e8fb-106">O pacote não usa o MSBuild 14,1 em mono- [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="9e8fb-107">A guia atualizar não seleciona a versão mais recente disponível para atualizar em vez disso, selecione versão instalada atual- [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="9e8fb-108">Corrija a falha após autenticar um feed MyGet particular V2 e clicando em "mostrar mais resultados"- [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="9e8fb-109">As mensagens de log parecem estar em ordem inversa para [#3446](https://github.com/NuGet/Home/issues/3446) da interface do usuário</span><span class="sxs-lookup"><span data-stu-id="9e8fb-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="9e8fb-110">v 3.4.4-NuGet Restore lança "não há suporte para o formato do caminho fornecido"- [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="9e8fb-111">NuGet cmdLine 3,6 Beta não respeita-prop Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="9e8fb-112">IKVM do NuGet-instalação lenta em projeto grande- [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="9e8fb-113">Atualização nuget.exe-automantém a atualização propriamente dita – [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="9e8fb-114">3,5 instalar/restaurar do compartilhamento UNC tem regressão de desempenho do 3.4.4- [#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="9e8fb-115">Erro ao instalar o MOQ da interface do usuário de gerenciamento de pacotes para um projeto net451- [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="9e8fb-116">A guia instalar no nível da solução não mostra a versão do pacote- [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="9e8fb-117">xproj `project.json` atualização da guia instalada perde o estado [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="9e8fb-118">O NuGet Pack on `.csproj` ignora o elemento arquivos vazios no `.nuspec` arquivo- [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="9e8fb-119">Os projetos do site hospedados no IIS não devem causar falha na restauração [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="9e8fb-120">As credenciais não são recuperadas de Nuget.Config quando o ponto de extremidade v3 redireciona para v2- [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="9e8fb-121">O pacote NuGet não resolve o assembly ao recuperar metadados do assembly portátil- [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="9e8fb-122">O NuGet não pode ser encontrado `msbuild.exe` em mono- [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="9e8fb-123">O pacote de nuget.exe não permite uma marca de pré-lançamento que começa com números- [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="9e8fb-124">a instalação do pacote NuGet falha em VS2015E- [#1298](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="9e8fb-125">o filtro allowedVersions não está funcionando no nível da solução- [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="9e8fb-126">A restauração falha aleatoriamente com um item com a mesma chave já foi adicionado.</span><span class="sxs-lookup"><span data-stu-id="9e8fb-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="9e8fb-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="9e8fb-128">Não é possível instalar NuGet. Common no `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="9e8fb-129">Ao usar a interface do usuário para pesquisar uma fonte v2, FindPackagesById é chamado duas vezes para cada ID- [#2517](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="9e8fb-130">Os pacotes não podem depender de projetos- [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="9e8fb-131">nuget.exe Pack – excluir está documentado, mas sem suporte- [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="9e8fb-132">Problemas com mensagens de erro quando a seção ' contentFiles ' de `.nuspec` é inválida- [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="9e8fb-133">O push sempre envia o pacote inteiro duas vezes com fontes de pacote autenticadas- [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="9e8fb-134">Nenhuma informação foi fornecida ao chamar nuget.exe Update \*. csproj enquanto o projeto não tem um `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="9e8fb-135">`packages.config` Restore não tenta novamente em códigos de status 5xx de fontes v2- [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="9e8fb-136">O ponto duplo na src do arquivo `.nuspec` não funciona – [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="9e8fb-137">A restauração do CoreCLR precisa ignorar feeds com criptografia- [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="9e8fb-138">Manipulação de nuget.exe Push 403-solicitando incorretamente credenciais- [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="9e8fb-139">A atualização do NuGet por meio do Gerenciador de pacotes remove as propriedades do `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="9e8fb-140">NuGet. PackageManagement. VisualStudio tenta carregar "NuGet. TeamFoundationServer14", mas esse nome de DLL foi alterado para "NuGet. TeamFoundationServer"- [#2857](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="9e8fb-141">A interface do usuário do Gerenciador de pacotes não mostra a versão atualizada recentemente [#2828](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="9e8fb-142">Update-Package tentando usar PackageID, versão em vez de Package. Version- [#2771](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="9e8fb-143">o csproj de restauração do NuGet deve ser um erro se o projeto não estiver usando NuGet ( `packages.config` ou `project.json` )- [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="9e8fb-144">O erro do TFS "[File] não foi encontrado no seu espaço de trabalho ou você não tem permissão para acessá-lo" durante a atualização ou desinstalação quando a solução/projeto está associada ao controle do código-fonte do TFS- [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="9e8fb-145">o pacote de atualização não obtém dependências para pacotes que não são de destino- [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="9e8fb-146">Não há como definir o nível de detalhamento de logs para ações de interface do usuário do Gerenciador de pacotes NuGet- [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="9e8fb-147">a configuração do NuGet é inválida-VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="9e8fb-148">Defaultpushname in `NuGetDefaults.Config` ( `ProgramData\NuGet` ) não funciona – [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="9e8fb-149">versão 3.4.3 do NuGet-obter o valor não pode ser nulo no Build do pacote- [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="9e8fb-150">a restauração não está usando credenciais armazenadas do Nuget.Config para feeds do VSTS- [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="9e8fb-151">[dotnet restore]--ConfigFile é relativo ao diretório do projeto em vez da pasta cmd- [#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="9e8fb-152">Alocações excessivas no código de análise da versão- [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="9e8fb-153">Várias instâncias do nuget.exe tentando instalar o mesmo pacote em paralelo causam uma [#2628](https://github.com/NuGet/Home/issues/2628) de gravação dupla</span><span class="sxs-lookup"><span data-stu-id="9e8fb-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="9e8fb-154">As informações de dependência não são armazenadas em cache para operações de vários projetos- [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="9e8fb-155">Instalar e atualizar pacotes de download sem verificar a pasta de pacotes primeiro- [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="9e8fb-156">Se a lista de origem do pacote estiver vazia, não será possível adicionar a origem do pacote via interface do usuário (NuGet 3.4. x)- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="9e8fb-157">Erro enganoso ao tentar instalar o pacote que depende do tempo de design fachadas- [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="9e8fb-158">Instalar um pacote do console do PackageManager com a configuração "All" tenta somente a primeira fonte- [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="9e8fb-159">Beta mais recente não descompactar ModernHttpClient- [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="9e8fb-160">VS2015 falha na inicialização com 3.4.1 de NuGet autocompilado- [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="9e8fb-161">O comando Update pode ser um pouco mais detalhado se eu fizer isso...- [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="9e8fb-162">O VSIX criado localmente deve ter os mesmos arquivos e DLLs que o CI Build.</span><span class="sxs-lookup"><span data-stu-id="9e8fb-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="9e8fb-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="9e8fb-164">Corrigir avisos de downgrade do NuGet no [#2396](https://github.com/NuGet/Home/issues/2396) de compilação</span><span class="sxs-lookup"><span data-stu-id="9e8fb-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="9e8fb-165">Falha ao autenticar a origem do pacote (3 vezes) é bloqueada para sempre [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="9e8fb-166">O conteúdo do pacote não é restaurado corretamente ao instalar um pacote de um feed do NuGet v 3.3 + com o argumento-NoCache quando o pacote contém `.nupkg` arquivos- [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="9e8fb-167">Instalação do NuGet com todas as origens do pacote, mas o pacote ausente da fonte 1, falha- [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="9e8fb-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet. PackageManagement. VisualStudio. VSMSBuildNuGetProjectSystem + \* lt; &gt; c__DisplayClass_0 + &lt; &lt; addreference &gt; B__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="9e8fb-169">Instalar blocos se uma única fonte falhar na autorização- [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="9e8fb-170">`.nuspec` o intervalo de versão deve substituir-IncludeReferencedProjects versão- [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="9e8fb-171">Update-Package super lento-"tentando coletar informações sobre dependências"- [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="9e8fb-172">Pacote de downgrades do NuGet stealth ao atualizar o lote de suas dependências- [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="9e8fb-173">nuget.exe atualização descarta o nome forte do assembly e o atributo privado.</span><span class="sxs-lookup"><span data-stu-id="9e8fb-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="9e8fb-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="9e8fb-175">Caminho de arquivo relativo para "defaultpushexception"- [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="9e8fb-176">Melhorar mensagens de falha do resolvedor- [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="9e8fb-177">Update-Package in v3 falha com pacotes que não estão na fonte especificada- [#1013](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="9e8fb-178">O uso de caminhos relativos para origens de pacote é problemático para uso- [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="9e8fb-179">Dependência ausente no NUPKG-File gerado do projeto se a dependência indireta já existe com um requisito de versão inferior- [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="9e8fb-180">Excluir um projeto fecha a janela da interface do usuário correspondente, mas a renomeação de um projeto não renomeia a janela da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="9e8fb-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="9e8fb-181">Observe que o PMC escuta os eventos renomear projeto e remover projeto- [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="9e8fb-182">[Carga de trabalho da Web do Willow] Criação de travas de WSP do Razor v3- [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="9e8fb-183">A instalação/restauração de um pacote específico falha com "o pacote contém vários arquivos nuspec".</span><span class="sxs-lookup"><span data-stu-id="9e8fb-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="9e8fb-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="9e8fb-185">IDs em minúsculas & `packages.config` cenários- [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="9e8fb-186">[3,5-beta2] Falha na restauração do pacote ao restaurar os pacotes "herdados"- [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="9e8fb-187">o pacote NuGet adiciona arquivos. TT de maneira forçada à pasta de conteúdo, independentemente do que [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="9e8fb-188">o pacote de atualização do aplicativo Web ASP.NET gera um aviso relacionado ao arquivo: Source- [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="9e8fb-189">o NuGet Pack csproj (with `project.json` ) falhará se não houver packoptions e proprietário no arquivo JSON- [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="9e8fb-190">o pacote NuGet para `project.json` ignora marcas packoptions, como resumo, autores, proprietários etc- [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="9e8fb-191">NullReferenceException via NuGet. Packaging. PhysicalPackageFile. GetStream- [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="9e8fb-192">O pacote NuGet ignora dependências na saída `.nuspec` para `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="9e8fb-193">A atualização de vários pacotes com a reversão deixa o projeto em um estado desfeito- [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="9e8fb-194">ContentFiles em qualquer um não é adicionado para projetos netstandard- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="9e8fb-195">Não é possível empacotar a biblioteca com o padrão .net Standard corretamente- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="9e8fb-196">Arquivo-> novo projeto-> biblioteca de classes (portátil) falha em VS2015 e Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="9e8fb-197">erro do nuGet-1.0.0-\* não é uma cadeia de caracteres de versão válida- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="9e8fb-198">Find-Package falha ao exibir, mas Install-Package Works- [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="9e8fb-199">Erro quando "Install-Package jQuery. Validation" em dev15- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="9e8fb-200">o pacote NuGet de xproj está padronizando para o caminho de destino inválido- [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="9e8fb-201">Quando instalada VS 2015 atualização 3 em um VS que usa o erro do NuGet versão 3.5.0 ocorre- [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="9e8fb-202">"Bloqueado por packages.config" no `project.json` projeto (UWP, a. k. a Build Integrated)- [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="9e8fb-203">Atualize a CLI do dotnet instalada pelo script de compilação para Preview2-003121, que é a compilação oficial do Preview2.</span><span class="sxs-lookup"><span data-stu-id="9e8fb-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="9e8fb-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="9e8fb-205">Interface do usuário do Gerenciador de pacotes: não exibe a nova versão após atualizar um pacote- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="9e8fb-206">-ApiKey na linha de comando de exclusão não é lido/enviado em 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="9e8fb-207">Cadeia de caracteres incorreta: uma versão estável de um pacote não deve ter em uma dependência de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="9e8fb-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="9e8fb-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="9e8fb-209">Cache OptimizedZipPackage deixa pastas vazias – [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="9e8fb-210">Criando exceção NullRef de Get do projeto PCL (net46 e Windows 10).</span><span class="sxs-lookup"><span data-stu-id="9e8fb-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="9e8fb-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="9e8fb-212">A atualização do NuGet deve fornecer uma mensagem informativa quando uma versão superior é restrita pela restrição allowedVersions- [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="9e8fb-213">Problemas de restauração do NuGet v3- [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="9e8fb-214">O plug-in de credencial saiu com o erro-1/erro ao baixar o pacote ao usar provedores de credenciais com várias fontes- [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="9e8fb-215">`project.json` a restauração do NuGet causa recompilação quando nada é alterado- [#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="9e8fb-216">Os pacotes de símbolos não devem nunca ser usados na instalação ou atualização- [#2807](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="9e8fb-217">O VS não oferece suporte a variáveis de ambiente no repositoryPath (nuget.exe) – [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="9e8fb-218">Rotule os UIElements não rotulados na interface do usuário do Gerenciador de pacotes para acessibilidade- [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="9e8fb-219">Estruturas portáteis com perfis hifenizados são rejeitadas.</span><span class="sxs-lookup"><span data-stu-id="9e8fb-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="9e8fb-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="9e8fb-221">O Gerenciador de pacotes NuGet deve tornar claro que a lista de opções no detalhes dos pacotes não se aplica a `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="9e8fb-222">nuget.exe Push/excluir não usará a chave de API- [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="9e8fb-223">Remover a propriedade locked do arquivo de bloqueio- [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="9e8fb-224">Falha na atualização do NuGet 3.3.0 com ' uma restrição adicional... definido em packages.config impede esta operação. '</span><span class="sxs-lookup"><span data-stu-id="9e8fb-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="9e8fb-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="9e8fb-226">A instalação do pacote de uma fonte local que não existe gera um [#1674](https://github.com/NuGet/Home/issues/1674) de mensagens falso</span><span class="sxs-lookup"><span data-stu-id="9e8fb-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="9e8fb-227">O filtro "atualização disponível" mostra atualizações que violam a restrição de versão- [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="9e8fb-228">Não é possível atualizar os pacotes nativos- [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="9e8fb-229">Recursos</span><span class="sxs-lookup"><span data-stu-id="9e8fb-229">Features</span></span>

* <span data-ttu-id="9e8fb-230">Suporte à configuração CopyLocal como false nas referências adicionadas pelo NuGet- [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="9e8fb-231">Suporte de nuget.exe para MSBuild 15- [#1937](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="9e8fb-232">Suporte do pacote para.`csproj`</span><span class="sxs-lookup"><span data-stu-id="9e8fb-232">Pack support for .`csproj`</span></span><span data-ttu-id="9e8fb-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="9e8fb-234">Desabilitar a ação do usuário quando houver ações do usuário sendo executadas- [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="9e8fb-235">O NuGet deve adicionar suporte para `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="9e8fb-236">Adicionar compatibilidades de estrutura ausentes no NuGet 2. x (que já estão em 3. x)- [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="9e8fb-237">Suporte para pastas de pacotes de fallback- [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="9e8fb-238">Projete e implemente uma noção de tipo de pacote para oferecer suporte a pacotes de ferramentas- [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="9e8fb-239">Adicione uma API para obter o caminho para a pasta de pacotes globais- [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="9e8fb-240">Habilitar SemVer 2.0.0 no [#3356](https://github.com/NuGet/Home/issues/3356) Pack</span><span class="sxs-lookup"><span data-stu-id="9e8fb-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="9e8fb-241">DCRs</span><span class="sxs-lookup"><span data-stu-id="9e8fb-241">DCRs</span></span>

* <span data-ttu-id="9e8fb-242">nuget.exe parâmetro Push-timeout não funciona – [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="9e8fb-243">O texto de descrição do pacote deve ser selecionável- [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="9e8fb-244">Habilitar nuget.exe para produzir `.props` e `.targets` arquivos para `.nuproj` projetos [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="9e8fb-245">Adicionar API de extensibilidade para comparar estruturas com importações- [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="9e8fb-246">Ocultar opções de dependência ao usar `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="9e8fb-247">Imprimir nuget.exe cabeçalho da versão na saída detalhada- [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="9e8fb-248">O NuGet precisa permitir que os usuários saibam que a atualização/instalação em uma PCL baseada em TFM de dotnet pode causar problemas- [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="9e8fb-249">Avisar instalação/atualização inadequada para o projeto c/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="9e8fb-250">Corrigir problemas de desempenho com remodelador e NuGet para update- [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="9e8fb-251">Adicionar suporte a netcoreapp11 e netstandard17- [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="9e8fb-252">Aproveitar o atributo AssemblyMetadata para `.nuspec` substituições de token- [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="9e8fb-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
