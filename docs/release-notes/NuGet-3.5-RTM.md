---
title: Notas de versão Beta do NuGet 3.5
description: Notas de versão do NuGet 3.5, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d8df2cb51ddcc03fb3922d9e9def17b39fccc661
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550678"
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="fe833-103">Notas de versão 3.5 do NuGet</span><span class="sxs-lookup"><span data-stu-id="fe833-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="fe833-104">[Notas de versão do RC 3.5 do NuGet](../release-notes/nuget-3.5-RC.md) | [notas de versão do NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="fe833-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="fe833-105">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="fe833-105">Bug Fixes</span></span>

* <span data-ttu-id="fe833-106">Pacote de não usa o MSBuild 14,1 no mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="fe833-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="fe833-107">Guia de atualização não seleciona a versão mais recente disponível para atualizar em vez disso, selecione a versão instalada atual - [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="fe833-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="fe833-108">Corrigir falhas depois de autenticar uma privada v2 feed MyGet e clicando em "Mostrar x mais resultados"- [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="fe833-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="fe833-109">Mensagens de log parecem estar na ordem inversa para a interface do usuário – [3446 #](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="fe833-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="fe833-110">gera de restauração do Nuget V3.4.4 - "formato do caminho especificado não é suportado" - [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="fe833-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="fe833-111">NuGet cmdLine 3.6 beta não honra - Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="fe833-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="fe833-112">Instalar o NuGet IKVM lento em um projeto grande - [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="fe833-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="fe833-113">NuGet.exe Update - Self mantém em atualizar a próprio - [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="fe833-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="fe833-114">3.5 instalação/restauração de compartilhamento de UNC tem a regressão de desempenho de 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="fe833-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="fe833-115">Erro ao instalar Moq do gerenciamento de pacote da interface do usuário para um projeto de net451 - [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="fe833-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="fe833-116">Guia de instalação no nível da solução não mostra a versão do pacote - [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="fe833-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="fe833-117">xproj `project.json` atualização de aba instalado perde o estado - [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="fe833-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="fe833-118">Pacote do NuGet na `.csproj` ignora o elemento de arquivos vazios no `.nuspec` arquivo - [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="fe833-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="fe833-119">Projetos de site hospedados no IIS não devem causar restauração falhe - [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="fe833-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="fe833-120">As credenciais não são recuperadas do NuGet. config quando o ponto de extremidade v3 redireciona para a v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="fe833-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="fe833-121">Pacote do NuGet não conseguir resolver o assembly ao recuperar metadados de assembly portátil - [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="fe833-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="fe833-122">O NuGet não é possível localizar `msbuild.exe` em Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="fe833-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="fe833-123">pacote de NuGet.exe não permite que uma marca de pré-lançamento que começa com números de - [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="fe833-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="fe833-124">Falha de instalação do pacote NuGet em VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="fe833-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="fe833-125">allowedVersions filtrar não trabalhar no nível da solução - [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="fe833-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="fe833-126">Restauração aleatoriamente falhará com um item com a mesma chave já foi adicionada.</span><span class="sxs-lookup"><span data-stu-id="fe833-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="fe833-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="fe833-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="fe833-128">Não é possível instalar Nuget.Common em `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="fe833-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="fe833-129">Ao usar a interface do usuário para pesquisar uma fonte V2, FindPackagesById é chamado duas vezes para cada ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="fe833-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="fe833-130">Pacotes não podem depender de projetos – [2490 #](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="fe833-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="fe833-131">pacote de NuGet.exe - Exclude é documentado mas não tem suporte - [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="fe833-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="fe833-132">Problemas com o erro mensagens quando 'contentFiles' seção de `.nuspec` inválido - [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="fe833-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="fe833-133">Envio por push sempre envia todo pacote duas vezes com origens do pacote - autenticada [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="fe833-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="fe833-134">Nenhuma informação foi fornecida durante a chamada de nuget.exe atualização \*.csproj enquanto o projeto não tem um `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="fe833-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="fe833-135">`packages.config` Restore não tentará novamente em códigos de status 5xx do código-fonte V2 - [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="fe833-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="fe833-136">Um ponto duplo no arquivo src na `.nuspec` não funciona – [2947 #](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="fe833-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="fe833-137">Restauração de CoreCLR precisa ignorar feeds com criptografia - [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="fe833-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="fe833-138">NuGet.exe push tratamento 403 - incorretamente pedir credenciais – [2910 #](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="fe833-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="fe833-139">A atualização por meio do Gerenciador de pacotes do NuGet remove as propriedades do `project.json`  -  [2888 #](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="fe833-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="fe833-140">Tente carregar "NuGet.TeamFoundationServer14", mas que o nome da DLL alterado para "NuGet.TeamFoundationServer" - NuGet.PackageManagement.VisualStudio [#2857](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="fe833-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="fe833-141">Gerenciador de pacotes, interface do usuário não mostra recentemente atualizado versão - [2828 #](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="fe833-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="fe833-142">pacote de atualização tentando usar packageid, versão, em vez de package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="fe833-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="fe833-143">NuGet restauração csproj deve erro se o projeto não está usando o nuget (`packages.config` ou `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="fe833-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="fe833-144">Erro do TFS "[file] não ser encontrado no seu espaço de trabalho, ou você não tem permissão para acessá-lo" durante a atualizar ou desinstalar quando o projeto/solução está associado ao controle do código-fonte do TFS - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="fe833-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="fe833-145">pacote de atualização não obter dependências para pacotes de destino não - [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="fe833-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="fe833-146">Não é possível definir o nível de verbosidade de logs para ações de interface do usuário de Gerenciador de pacote Nuget - [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="fe833-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="fe833-147">configuração do NuGet é inválida - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="fe833-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="fe833-148">DefaultPushSource na `NuGetDefaults.Config` (`ProgramData\NuGet`) não funciona – [2653 #](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="fe833-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="fe833-149">versão do NuGet 3.4.3 - Obtendo o valor não pode ser nulo na compilação do pacote - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="fe833-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="fe833-150">restauração não está usando credenciais armazenadas do NuGet. config para feeds do VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="fe833-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="fe833-151">[dotnet restore] - configfile é relativo ao projeto dir em vez de dir cmd - [#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="fe833-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="fe833-152">Alocações excessivas no código da versão comparsion - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="fe833-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="fe833-153">Várias instâncias do nuget.exe tentando instalar o mesmo pacote em paralelo faz com que uma gravação dupla - [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="fe833-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="fe833-154">Informações de dependência não é armazenado em cache para operações de vários projetos – [2619 #](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="fe833-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="fe833-155">Instalar e atualizar os pacotes de download sem verificar a pasta pacotes primeiro - [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="fe833-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="fe833-156">Se a lista de origem do pacote está vazia, não é possível adicionar origem do pacote por meio da interface do usuário (NuGet 3.4. x)- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="fe833-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="fe833-157">Erro enganoso quando a tentativa de instalar o pacote que depende do tempo de design fachadas - [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="fe833-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="fe833-158">Instalação de um pacote no console do PackageManager com a configuração "All" tenta somente primeira fonte - [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="fe833-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="fe833-159">Versão beta mais recente não descompactar ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="fe833-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="fe833-160">VS2015 Falha na inicialização com o NuGet criado automaticamente 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="fe833-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="fe833-161">Comando de atualização pode ser um pouco mais detalhado se i pedir que ele seja portanto... - [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="fe833-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="fe833-162">VSIX criado localmente deve ter as mesmas DLLs e arquivos como o build de CI.</span><span class="sxs-lookup"><span data-stu-id="fe833-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="fe833-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="fe833-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="fe833-164">Corrigir avisos de downgrade do NuGet em compilação - [#2396](https://github.com/NuGet/Home/issues/2396)</span><span class="sxs-lookup"><span data-stu-id="fe833-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="fe833-165">Falha ao autenticar a origem do pacote (3 vezes) está bloqueada para sempre - [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="fe833-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="fe833-166">Conteúdo do pacote não será restaurado corretamente durante a instalação de um pacote do nuget v3.3 + feed com o argumento - NoCache quando o pacote contiver `.nupkg` arquivos - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="fe833-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="fe833-167">Falha na instalação do NuGet com todas as fontes de pacote, mas o pacote ausente da 1 fonte, - [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="fe833-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="fe833-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt; &gt;c__DisplayClass_0 +&lt;&lt;Adicionarreferencia&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="fe833-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="fe833-169">Instalar blocos se uma única fonte falhar autorização - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="fe833-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="fe833-170">`.nuspec` versão do intervalo deve substituir a versão - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="fe833-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="fe833-171">Pacote de atualização muito lenta - "tentando coletar informações de dependências" - [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="fe833-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="fe833-172">Downgrades furtivos NuGet do pacote ao lote Atualizando suas dependências - [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="fe833-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="fe833-173">atualização de NuGet.exe descarta o nome forte do assembly e o atributo particular.</span><span class="sxs-lookup"><span data-stu-id="fe833-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="fe833-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="fe833-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="fe833-175">Caminho relativo do arquivo para "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="fe833-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="fe833-176">Melhorar a mensagens de falha de resolvedor - [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="fe833-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="fe833-177">pacote de atualização na v3 falha com os pacotes não na fonte especificada - [#1013](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="fe833-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="fe833-178">Usando caminhos relativos para origens de pacote é problemático para usar - [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="fe833-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="fe833-179">Dependência no arquivo NUPKG gerado do projeto, se a dependência indireta já existe com um requisito de versão inferior - ausente [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="fe833-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="fe833-180">Exclusão de um projeto fecha a janela de interface do usuário correspondente, mas, renomear um projeto não renomeia a janela de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="fe833-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="fe833-181">Observe que o PMC escuta a renomeação de projeto e eventos de remover do projeto - [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="fe833-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="fe833-182">[Carga de trabalho de Web Willow] Criar o Razor v3 WSP trava - [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="fe833-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="fe833-183">Instalação/restauração de um determinado pacote falhar com "O pacote contém vários arquivos nuspec."</span><span class="sxs-lookup"><span data-stu-id="fe833-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="fe833-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="fe833-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="fe833-185">Letras minúsculas de IDs de & `packages.config` cenários - [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="fe833-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="fe833-186">[3.5-beta2] Restauração de pacote não conseguir restaurar pacotes "herdados" - [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="fe833-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="fe833-187">pacote NuGet adiciona forçada arquivos. TT para pasta de conteúdo importa - [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="fe833-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="fe833-188">pacote de atualização de aplicativo web ASP.NET gera o aviso relacionado ao arquivo: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="fe833-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="fe833-189">NuGet pack csproj (com `project.json`) falha se não houver nenhum packOptions e o proprietário do arquivo JSON - [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="fe833-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="fe833-190">pacote do NuGet para `project.json` ignora packOptions marcas como resumo, os autores, proprietários etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="fe833-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="fe833-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="fe833-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="fe833-192">Pacote do NuGet ignora as dependências na saída `.nuspec` para `project.json`  -  [3145 #](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="fe833-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="fe833-193">Atualizar vários pacotes com reversão deixa o projeto em um estado interrompido - [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="fe833-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="fe833-194">ContentFiles em qualquer não são adicionados para projetos de identificadores de netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="fe833-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="fe833-195">Não é possível empacotar a biblioteca destinados ao .net Standard corretamente - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="fe833-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="fe833-196">Arquivo -> Novo projeto -> Falha de projeto de biblioteca de classes (portátil) em VS2015 e Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="fe833-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="fe833-197">Erro do NuGet - 1.0.0-\* não é uma cadeia de caracteres de versão válida - [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="fe833-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="fe833-198">Find-Package falha para exibição, mas funciona de Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="fe833-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="fe833-199">Erro ao "Install-Package jquery.validation" em dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="fe833-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="fe833-200">pacote de NuGet xproj é Padronizando para caminho de destino inválido - [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="fe833-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="fe833-201">Quando instalado VS 2015 atualização 3 em uma que usa o NuGet, ocorre o erro de versão 3.5.0 - VS [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="fe833-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="fe833-202">"Bloqueado pelo Packages. config" `project.json` (build também conhecidas como integrado UWP) projeto - [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="fe833-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="fe833-203">Atualize a cli do dotnet instalada pelo script de compilação para visualização 2-003121, que é a compilação de visualização 2 oficial.</span><span class="sxs-lookup"><span data-stu-id="fe833-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="fe833-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="fe833-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="fe833-205">Interface do usuário do Gerenciador de pacotes: não exibe a nova versão depois de atualizar um pacote- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="fe833-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="fe833-206">-ApiKey na linha de comando de exclusão não é leitura/enviada em 3.5.0-Beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="fe833-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="fe833-207">Cadeia de caracteres incorreta: uma versão estável de um pacote não deve ter em uma dependência de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="fe833-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="fe833-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="fe833-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="fe833-209">Cache OptimizedZipPackage deixa pastas vazias - [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="fe833-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="fe833-210">Criando get de projeto PCL (net46 e windows 10) exceção NullRef.</span><span class="sxs-lookup"><span data-stu-id="fe833-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="fe833-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="fe833-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="fe833-212">Atualização do NuGet deve fornecer a mensagem informativa quando uma versão mais recente é restrito pela restrição allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="fe833-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="fe833-213">Problemas de restauração do NuGet v3 - [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="fe833-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="fe833-214">Plug-in de credencial foi encerrado com erro -1 / Erro ao baixar pacote ao usar provedores de credenciais com várias fontes - [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="fe833-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="fe833-215">`project.json` restauração do NuGet provoca a recompilação quando nada alterado - [#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="fe833-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="fe833-216">Pacotes de símbolos não devem nunca ser usado na instalação ou atualização - [#2807](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="fe833-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="fe833-217">VS não dá suporte a variáveis de ambiente no caminho do repositório (nuget.exe faz) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="fe833-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="fe833-218">Rótulo de UIElements sem rótulo na UI do Gerenciador de pacotes para acessibilidade - [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="fe833-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="fe833-219">Estruturas portátil com perfis hifenizadas são rejeitadas.</span><span class="sxs-lookup"><span data-stu-id="fe833-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="fe833-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="fe833-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="fe833-221">O Gerenciador de pacotes do NuGet deve esclarecer essa lista de opções em pacotes detalhes não se aplicam a `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="fe833-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="fe833-222">envio/excluir NuGet.exe não usam a chave de API - [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="fe833-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="fe833-223">Remova a propriedade locked do arquivo lock - [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="fe833-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="fe833-224">NuGet 3.3.0 atualização falha com '... uma restrição adicional definido em Packages. config impede que esta operação.'</span><span class="sxs-lookup"><span data-stu-id="fe833-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="fe833-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="fe833-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="fe833-226">Ao instalar o pacote de um local de origem que não existe gera uma mensagem de falso - [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="fe833-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="fe833-227">Filtro de "Atualização disponível" mostra as atualizações que violam a restrição de versão - [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="fe833-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="fe833-228">Não é possível atualizar pacotes nativos - [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="fe833-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="fe833-229">Recursos</span><span class="sxs-lookup"><span data-stu-id="fe833-229">Features</span></span>

* <span data-ttu-id="fe833-230">Suporte à configuração CopyLocal como falso nas referências adicionadas pelo NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="fe833-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="fe833-231">o suporte para o MSBuild 15 - NuGet.exe [1937 #](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="fe833-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="fe833-232">Pacote de suporte.`csproj`</span><span class="sxs-lookup"><span data-stu-id="fe833-232">Pack support for .`csproj`</span></span><span data-ttu-id="fe833-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="fe833-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="fe833-234">Desabilitar a ação do usuário quando há ações do usuário que está sendo executadas- [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="fe833-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="fe833-235">O NuGet deve adicionar suporte para `runtimes/{rid}/nativeassets/{txm}/`  -  [2782 #](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="fe833-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="fe833-236">Adicionar às compatibilidades de framework ausente no NuGet 2.x (que já estão em 3. x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="fe833-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="fe833-237">Suporte para pastas de pacote fallback - [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="fe833-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="fe833-238">Projetar e implementar uma noção de tipo de pacote para dar suporte a pacotes de ferramenta - [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="fe833-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="fe833-239">Adicionar uma API para obter o caminho para a pasta de pacotes globais - [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="fe833-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="fe833-240">Habilitar SemVer 2.0.0 no pacote - [#3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="fe833-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="fe833-241">DCRs</span><span class="sxs-lookup"><span data-stu-id="fe833-241">DCRs</span></span>

* <span data-ttu-id="fe833-242">NuGet.exe push - o parâmetro de tempo limite não funciona - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="fe833-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="fe833-243">Texto de descrição do pacote deve ser selecionável - [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="fe833-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="fe833-244">Habilitar nuget.exe produzir `.props` e `.targets` arquivos para `.nuproj` projetos [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="fe833-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="fe833-245">Adicionar a API para comparar as estruturas de importações - de extensibilidade [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="fe833-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="fe833-246">Ocultar as opções da dependência ao usar `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="fe833-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="fe833-247">Imprimir o cabeçalho de versão nuget.exe na saída detalhada - [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="fe833-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="fe833-248">O NuGet precisa que os usuários saibam que atualizar/instalar em um tfm dotnet com base em PCL poderá causar problemas - [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="fe833-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="fe833-249">Avisar ruim instalar/atualizar para o projeto c / tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="fe833-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="fe833-250">Corrigir problemas de desempenho com ReShaper e NuGet para Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="fe833-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="fe833-251">Adicionar suporte netcoreapp11 e netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="fe833-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="fe833-252">Atributo AssemblyMetadata aproveite `.nuspec` token substituições - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="fe833-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
