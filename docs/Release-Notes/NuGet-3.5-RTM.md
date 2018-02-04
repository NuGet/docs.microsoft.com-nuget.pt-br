---
title: "Notas de versão do NuGet 3.5 Beta | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão 3.5 do NuGet incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão 3.5 do NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ee78ceb2ff032c05c0f8ef9a6623b94cc56ee0a9
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="89c6f-104">Notas de versão 3.5 do NuGet</span><span class="sxs-lookup"><span data-stu-id="89c6f-104">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="89c6f-105">[Notas de versão de RC 3.5 do NuGet](../release-notes/nuget-3.5-RC.md) | [notas de versão de RC do NuGet 4.0](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="89c6f-105">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="89c6f-106">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="89c6f-106">Bug Fixes</span></span>

* <span data-ttu-id="89c6f-107">Pacote de não usa o MSBuild 14,1 em mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="89c6f-107">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="89c6f-108">Guia de atualização não selecione a versão mais recente disponível para atualizar em vez disso, selecione a versão instalada atual - [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="89c6f-108">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="89c6f-109">Corrija a falha depois de autenticar uma v2 privada MyGet feed e clicando em "Mostrar x mais resultados"- [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="89c6f-109">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="89c6f-110">Mensagens de log parecem estar na ordem inversa para a interface do usuário - [#3446](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="89c6f-110">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="89c6f-111">gera de restauração do Nuget V3.4.4 - "formato do caminho especificado não é suportado" - [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="89c6f-111">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="89c6f-112">NuGet cmdLine 3.6 beta não honra - Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="89c6f-112">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="89c6f-113">Instalar o NuGet IKVM lenta em grande projeto - [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="89c6f-113">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="89c6f-114">NuGet.exe Update - Self mantém na atualização em si - [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="89c6f-114">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="89c6f-115">instalação/restaurar 3.5 do compartilhamento UNC tem desempenho regressão de 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="89c6f-115">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="89c6f-116">Erro ao instalar Moq do gerenciamento de pacote da interface do usuário para um projeto de net451 - [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="89c6f-116">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="89c6f-117">Guia de instalação no nível da solução não mostra a versão do pacote - [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="89c6f-117">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="89c6f-118">xproj `project.json` atualização instalada guia perde estado - [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="89c6f-118">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="89c6f-119">Pacote do NuGet em `.csproj` ignora o elemento de arquivos vazios no `.nuspec` arquivo - [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="89c6f-119">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="89c6f-120">Projetos de site hospedados no IIS não devem causar restauração falhe - [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="89c6f-120">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="89c6f-121">As credenciais não foram recuperadas do NuGet. config quando o ponto de extremidade v3 redireciona v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="89c6f-121">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="89c6f-122">Pacote do NuGet não conseguir resolver o assembly ao recuperar metadados de assembly portátil - [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="89c6f-122">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="89c6f-123">O NuGet não é possível localizar `msbuild.exe` em Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="89c6f-123">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="89c6f-124">pacote de NuGet.exe não permite uma marca de pré-lançamento que começa com números de - [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="89c6f-124">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="89c6f-125">Falha de instalação do pacote NuGet em VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="89c6f-125">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="89c6f-126">Allowedverdions filtrar não funcionar no nível da solução - [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="89c6f-126">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="89c6f-127">A restauração falhará aleatoriamente um item com a mesma chave já foi adicionada.</span><span class="sxs-lookup"><span data-stu-id="89c6f-127">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="89c6f-128"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="89c6f-128"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="89c6f-129">Não é possível instalar Nuget.Common em `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="89c6f-129">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="89c6f-130">Ao usar a interface do usuário para pesquisar uma fonte V2, FindPackagesById é chamado duas vezes para cada ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="89c6f-130">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="89c6f-131">Pacotes não podem depender de projetos - [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="89c6f-131">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="89c6f-132">pacote de NuGet.exe - Exclude é documentado mas não tem suporte - [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="89c6f-132">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="89c6f-133">Problemas com o erro mensagens quando a seção 'contentFiles' de `.nuspec` é inválida - [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="89c6f-133">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="89c6f-134">Push sempre envia todo pacote duas vezes com origens do pacote - autenticado [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="89c6f-134">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="89c6f-135">Nenhuma informação foi fornecida durante a chamada de nuget.exe atualização csproj enquanto o projeto não tem um `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="89c6f-135">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="89c6f-136">`packages.config`Restore não tenta novamente em códigos de status 5xx do código-fonte V2 - [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="89c6f-136">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="89c6f-137">Ponto duplo no arquivo src em `.nuspec` não funciona - [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="89c6f-137">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="89c6f-138">Restauração do CoreCLR precisa ignorar feeds com criptografia - [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="89c6f-138">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="89c6f-139">NuGet.exe push tratamento 403 - solicitação incorreta de credenciais - [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="89c6f-139">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="89c6f-140">NuGet atualização por meio do Gerenciador de pacotes remove propriedades a partir de `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="89c6f-140">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="89c6f-141">Tente carregar "NuGet.TeamFoundationServer14", mas que o nome da DLL alterado para "NuGet.TeamFoundationServer" - NuGet.PackageManagement.VisualStudio [#2857](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="89c6f-141">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="89c6f-142">Gerenciador de pacote UI não mostra recentemente atualizado versão - [&#2828;](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="89c6f-142">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="89c6f-143">pacote de atualização tentando usar packageid, versão, em vez de package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="89c6f-143">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="89c6f-144">NuGet restauração csproj deve erro se o projeto não está usando o nuget (`packages.config` ou `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="89c6f-144">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="89c6f-145">Erro do TFS "[arquivo] não ser encontrado no espaço de trabalho, ou você não tem permissão para acessá-lo" durante a atualização ou desinstalação ao projeto/solução está associado ao controle de origem do TFS - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="89c6f-145">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="89c6f-146">pacote de atualização não obter dependências de pacotes de destino não - [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="89c6f-146">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="89c6f-147">Não é possível definir o nível de verbosidade de logs para ações de interface do usuário de Gerenciador de pacote Nuget - [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="89c6f-147">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="89c6f-148">configuração do NuGet é inválida - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="89c6f-148">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="89c6f-149">DefaultPushSource em `NuGetDefaults.Config` (`ProgramData\NuGet`) não funciona - [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="89c6f-149">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="89c6f-150">versão do NuGet 3.4.3 - Obtendo o valor não pode ser nulo na compilação do pacote - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="89c6f-150">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="89c6f-151">a restauração não está usando credenciais armazenadas do NuGet. config para feeds do VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="89c6f-151">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="89c6f-152">[dotnet restauração] – configfile é relativo ao diretório de projeto em vez do dir cmd - [#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="89c6f-152">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="89c6f-153">Alocações excessivas no código da versão comparsion - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="89c6f-153">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="89c6f-154">Várias instâncias de nuget.exe tentando instalar o mesmo pacote em paralelo faz com que uma gravação dupla - [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="89c6f-154">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="89c6f-155">Informações de dependência não é armazenado em cache para operações de multiprojetos - [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="89c6f-155">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="89c6f-156">Instalar e atualizar os pacotes de download sem verificar a pasta pacotes primeiro - [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="89c6f-156">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="89c6f-157">Se a lista de origem do pacote está vazia, não é possível adicionar origem do pacote por meio da interface do usuário (NuGet 3.4. x)- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="89c6f-157">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="89c6f-158">Enganar erro ao tentar instalar o pacote que depende de tempo de design fachadas - [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="89c6f-158">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="89c6f-159">Instalação de um pacote do console PackageManager com a configuração de "All" tenta somente primeira fonte - [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="89c6f-159">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="89c6f-160">Versão beta mais recente não descompactar ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="89c6f-160">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="89c6f-161">VS2015 Falha na inicialização com o NuGet automática interna 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="89c6f-161">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="89c6f-162">Comando de atualização pode ser um pouco mais detalhado se exigir que ele seja portanto... - i [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="89c6f-162">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="89c6f-163">VSIX criado localmente deve ter o mesmo DLLs e arquivos que a compilação de CI.</span><span class="sxs-lookup"><span data-stu-id="89c6f-163">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="89c6f-164"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="89c6f-164"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="89c6f-165">Corrigir avisos de downgrade do NuGet em compilação - [#2396](https://github.com/NuGet/Home/issues/2396)</span><span class="sxs-lookup"><span data-stu-id="89c6f-165">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="89c6f-166">Falha ao autenticar a origem do pacote (3 vezes) está bloqueada para sempre - [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="89c6f-166">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="89c6f-167">Conteúdo do pacote não será restaurado corretamente quando instalar um pacote do nuget v3.3 + feed com o argumento - NoCache quando o pacote contiver `.nupkg` arquivos - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="89c6f-167">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="89c6f-168">Ocorre falha na instalação do NuGet com todas as fontes de pacote, mas o pacote ausente da fonte de 1 - [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="89c6f-168">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="89c6f-169">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt; &gt;c__DisplayClass_0 +&lt;&lt;Adicionarreferencia&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="89c6f-169">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="89c6f-170">Instalar blocos se uma única fonte não será autorizada - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="89c6f-170">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="89c6f-171">`.nuspec`versão do intervalo deve substituir a versão - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="89c6f-171">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="89c6f-172">Pacote de atualização muito lenta - "tentando coletar informações de dependências" - [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="89c6f-172">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="89c6f-173">Downgrades furtivos NuGet do pacote ao lote Atualizando suas dependências - [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="89c6f-173">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="89c6f-174">atualização de NuGet.exe descarta o nome forte do assembly e o atributo privado.</span><span class="sxs-lookup"><span data-stu-id="89c6f-174">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="89c6f-175"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="89c6f-175"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="89c6f-176">Caminho de arquivo relativo para "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="89c6f-176">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="89c6f-177">Melhorar a mensagens de falha de resolução - [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="89c6f-177">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="89c6f-178">Falha do pacote de atualização no v3 com pacotes não na origem especificada - [#1013](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="89c6f-178">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="89c6f-179">Usar caminhos relativos para fontes de pacote é problemático para usar - [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="89c6f-179">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="89c6f-180">Não tem dependência no arquivo NUPKG gerado do projeto, se a dependência indireta já existe com um requisito de versão inferior - [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="89c6f-180">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="89c6f-181">Excluir um projeto fecha a janela de interface do usuário correspondente, mas, renomear um projeto não renomeia a janela de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="89c6f-181">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="89c6f-182">Observe que PMC escuta renomeação de projeto e eventos do projeto remove - [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="89c6f-182">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="89c6f-183">[Willow carga de trabalho da Web] Criar Razor v3 WSP trava - [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="89c6f-183">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="89c6f-184">Instalação/restauração de um determinado pacote falha com "Pacote contêm vários arquivos nuspec."</span><span class="sxs-lookup"><span data-stu-id="89c6f-184">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="89c6f-185"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="89c6f-185"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="89c6f-186">Letras minúsculas IDs & `packages.config` cenários - [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="89c6f-186">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="89c6f-187">[beta2 3.5] Restauração do pacote não conseguir restaurar os pacotes "herdados" - [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="89c6f-187">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="89c6f-188">pacote do NuGet Force adiciona arquivos. TT para pasta de conteúdo, não importando qual - [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="89c6f-188">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="89c6f-189">pacote de atualização do aplicativo web ASP.NET gera o aviso relacionado ao arquivo: origem - [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="89c6f-189">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="89c6f-190">csproj de pacote do NuGet (com `project.json`) falha se não houver nenhum packOptions e proprietário no arquivo JSON - [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="89c6f-190">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="89c6f-191">pacote do NuGet para `project.json` ignora packOptions marcas como resumo, autores e proprietários etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="89c6f-191">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="89c6f-192">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="89c6f-192">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="89c6f-193">Pacote do NuGet ignora dependências na saída `.nuspec` para `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="89c6f-193">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="89c6f-194">Atualizar vários pacotes com a reversão deixa o projeto em um estado interrompido - [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="89c6f-194">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="89c6f-195">ContentFiles em qualquer não são adicionados para projetos de identificadores de netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="89c6f-195">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="89c6f-196">Não é possível empacotar biblioteca direcionado ao .net padrão corretamente - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="89c6f-196">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="89c6f-197">Arquivo -> Novo projeto -> Falha de projeto de biblioteca de classes (portátil) em VS2015 e Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="89c6f-197">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="89c6f-198">Erro do NuGet - 1.0.0-\* não é uma cadeia de caracteres de versão válida - [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="89c6f-198">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="89c6f-199">Find-Package falha para exibição, mas funciona Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="89c6f-199">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="89c6f-200">Erro ao "Install-Package jquery.validation" em dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="89c6f-200">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="89c6f-201">pacote de NuGet xproj é Padronizando para caminho de destino inválido - [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="89c6f-201">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="89c6f-202">Quando instalado VS 2015 atualização 3 em uma relação que usa NuGet versão 3.5.0 erro - [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="89c6f-202">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="89c6f-203">"Bloqueado por Packages" `project.json` (UWP, também conhecidos como compilação integrada) projeto - [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="89c6f-203">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="89c6f-204">Atualize dotnet cli instalada pelo script de compilação para preview2-003121, que é a compilação preview2 oficial.</span><span class="sxs-lookup"><span data-stu-id="89c6f-204">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="89c6f-205"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="89c6f-205"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="89c6f-206">Interface de usuário do Gerenciador de pacote: não exibir a nova versão depois de atualizar um pacote- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="89c6f-206">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="89c6f-207">-ApiKey na linha de comando de exclusão não é leitura/enviada em 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="89c6f-207">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="89c6f-208">Cadeia de caracteres incorreta: uma versão estável de um pacote não deve ter em uma dependência de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="89c6f-208">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="89c6f-209"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="89c6f-209"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="89c6f-210">Cache de OptimizedZipPackage deixa as pastas vazias - [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="89c6f-210">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="89c6f-211">Criando get de projeto PCL (net46 e windows 10) NullRef exceção.</span><span class="sxs-lookup"><span data-stu-id="89c6f-211">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="89c6f-212"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="89c6f-212"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="89c6f-213">Atualização do NuGet deve fornecer a mensagem informativa quando uma versão mais recente é restrito por restrição Allowedverdions - [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="89c6f-213">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="89c6f-214">Problemas de restauração do NuGet v3 - [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="89c6f-214">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="89c6f-215">Plug-in de credencial foi encerrado com erro -1 / erro baixar pacote ao usar os provedores de credenciais com várias fontes - [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="89c6f-215">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="89c6f-216">`project.json`restauração do NuGet provoca a recompilação quando nada alterado - [#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="89c6f-216">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="89c6f-217">Pacotes de símbolos nunca não devem ser usada na instalação ou atualização - [#2807](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="89c6f-217">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="89c6f-218">VS não oferece suporte a variáveis de ambiente no caminho do repositório (nuget.exe faz) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="89c6f-218">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="89c6f-219">Rótulo de UIElements sem rótulo na UI do Gerenciador de pacotes para acessibilidade - [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="89c6f-219">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="89c6f-220">Estruturas portátil com perfis hifenizadas são rejeitadas.</span><span class="sxs-lookup"><span data-stu-id="89c6f-220">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="89c6f-221"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="89c6f-221"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="89c6f-222">O Gerenciador de pacotes do NuGet deve esclarecer essa lista de opções em pacotes detalhes não se aplicam a `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="89c6f-222">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="89c6f-223">envio/excluir NuGet.exe não usam a chave de API - [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="89c6f-223">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="89c6f-224">Remova a propriedade locked do arquivo lock - [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="89c6f-224">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="89c6f-225">Falha de atualização do NuGet 3.3.0 '... uma restrição adicional definida no Packages impede esta operação.'</span><span class="sxs-lookup"><span data-stu-id="89c6f-225">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="89c6f-226"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="89c6f-226"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="89c6f-227">Instalando o pacote de um local de origem que não existe gera uma mensagem falso - [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="89c6f-227">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="89c6f-228">Filtro de "Atualização disponível" mostra as atualizações que violam a restrição de versão - [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="89c6f-228">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="89c6f-229">Não é possível atualizar os pacotes nativos - [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="89c6f-229">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="89c6f-230">Recursos</span><span class="sxs-lookup"><span data-stu-id="89c6f-230">Features</span></span>

* <span data-ttu-id="89c6f-231">Suporte à configuração CopyLocal como falso nas referências adicionadas pelo NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="89c6f-231">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="89c6f-232">suporte de NuGet.exe para 15 MSBuild - [#1937](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="89c6f-232">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="89c6f-233">Pacote de suporte.`csproj`</span><span class="sxs-lookup"><span data-stu-id="89c6f-233">Pack support for .`csproj`</span></span><span data-ttu-id="89c6f-234"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="89c6f-234"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="89c6f-235">Desabilitar ação do usuário quando há ações do usuário que está sendo executadas- [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="89c6f-235">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="89c6f-236">NuGet deve adicionar suporte para `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="89c6f-236">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="89c6f-237">Adicionar compatibilidades framework ausente no NuGet 2. x (que já estão em 3. x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="89c6f-237">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="89c6f-238">Suporte para pastas de pacote de fallback - [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="89c6f-238">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="89c6f-239">Projetar e implementar uma noção do tipo de pacote para dar suporte a pacotes de ferramenta - [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="89c6f-239">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="89c6f-240">Adicionar uma API para obter o caminho para a pasta de pacotes global - [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="89c6f-240">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="89c6f-241">Habilitar SemVer 2.0.0 no pacote - [#3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="89c6f-241">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="89c6f-242">DCRs</span><span class="sxs-lookup"><span data-stu-id="89c6f-242">DCRs</span></span>

* <span data-ttu-id="89c6f-243">NuGet.exe push - o parâmetro de tempo limite não funciona - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="89c6f-243">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="89c6f-244">Texto de descrição do pacote deve ser selecionável - [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="89c6f-244">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="89c6f-245">Habilitar nuget.exe produzir `.props` e `.targets` arquivos de `.nuproj` projetos [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="89c6f-245">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="89c6f-246">Adicionar extensibilidade API para comparar estruturas com importações - [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="89c6f-246">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="89c6f-247">Ocultar as opções da dependência ao usar `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="89c6f-247">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="89c6f-248">Impressão do cabeçalho de versão de nuget.exe na saída detalhada - [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="89c6f-248">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="89c6f-249">NuGet precisa que os usuários saibam que atualizar/instalar em um tfm dotnet com base em PCL pode causar problemas - [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="89c6f-249">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="89c6f-250">Avisar incorreta instalar ou atualizar para o projeto com tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="89c6f-250">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="89c6f-251">Corrigir problemas de desempenho com ReShaper e NuGet para Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="89c6f-251">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="89c6f-252">Adicionar suporte netcoreapp11 e netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="89c6f-252">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="89c6f-253">Atributo AssemblyMetadata aproveite `.nuspec` token substituições - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="89c6f-253">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
