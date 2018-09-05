---
title: 3.5 notas de versão Beta2
description: Notas de versão do NuGet 3.5 Beta 2, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551985"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="e3469-103">Notas de versão do NuGet 3.5 Beta2</span><span class="sxs-lookup"><span data-stu-id="e3469-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="e3469-104">[Notas de versão 3.5 Beta do NuGet](../release-notes/nuget-3.5-Beta.md) | [notas de versão do RC 3.5 do NuGet](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="e3469-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="e3469-105">RTM do NuGet 3.5 Beta 2 foi lançado em 27 de junho de 2016 para o Visual Studio 2013 e nuget.exe</span><span class="sxs-lookup"><span data-stu-id="e3469-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="e3469-106">Log de alterações completo</span><span class="sxs-lookup"><span data-stu-id="e3469-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="e3469-107">Lista de Problemas</span><span class="sxs-lookup"><span data-stu-id="e3469-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="e3469-108">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="e3469-108">Bug Fixes</span></span>

* <span data-ttu-id="e3469-109">Mensagem de erro atualizado será falta de suporte para decrpytion de senha no .NET Core para feeds autenticados - [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="e3469-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="e3469-110">Console do Gerenciador de pacotes do Get-Package falhará se o projeto .NET Core está aberto - [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="e3469-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="e3469-111">Corrija a manipulação incorreta de 403 no comando NuGet push [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="e3469-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="e3469-112">Corrigir problemas da desinstalação de pacotes em uma solução associada ao controle de origem do TFS quando disableSourceControlIntegration é definido como true - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="e3469-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="e3469-113">Correção de atualização de pacote entrem em pacotes de destino não conta - [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="e3469-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="e3469-114">Usar o nível de detalhamento do MSBuild para definir o nível de agente de log para o Gerenciador de pacote do Nuget ações de interface do usuário - [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="e3469-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="e3469-115">Correção de configuração do NuGet é erro inválido em projetos de site - VSIX de VS 2015 (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="e3469-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="e3469-116">Corrigir problemas do pacote do `.csproj` quando os arquivos de conteúdo são incluídos - [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="e3469-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="e3469-117">DefaultPushSource na `NuGetDefaults.Config` (`ProgramData\NuGet`) não funciona – [2653 #](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="e3469-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="e3469-118">Corrigir o problema na versão do Nuget 3.4.3 - valor não pode ser nulo na criação do pacote - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="e3469-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="e3469-119">A restauração usa credenciais armazenadas do NuGet. config para feeds do VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="e3469-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="e3469-120">Desempenho - alocações excessivas de correção no código da versão comparsion - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="e3469-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="e3469-121">Corrigir problemas quando várias instâncias do nuget.exe tenta instalar o mesmo pacote em paralelo, [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="e3469-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="e3469-122">Desempenho - informações de dependência de Cache para operações de multiprojetos - [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="e3469-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="e3469-123">Corrija o problema onde adicionado das configurações de fontes de pacote não foi possível quando a lista de origem está vazia - [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="e3469-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="e3469-124">Corrigir o erro falsas ao tentar instalar o pacote que depende do tempo de design fachadas - [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="e3469-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="e3469-125">Instalação de um pacote no console do PackageManager com a configuração "All" tenta somente primeira fonte - [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="e3469-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="e3469-126">Corrigir problemas com os pacotes que têm arquivos com tempos de gravação no futuro (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="e3469-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="e3469-127">Exibir a exceção quando há uma falha de projetos de localização no comando update - [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="e3469-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="e3469-128">Conteúdo do pacote não será restaurado corretamente durante a instalação de um pacote do nuget v3.3 + feed com o argumento - NoCache quando o pacote contiver `.nupkg` arquivos - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="e3469-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="e3469-129">Corrigir problema com o pacote para instalar (todas as fontes) quando o pacote está ausente da 1 origem - [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="e3469-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="e3469-130">Instalar blocos se uma única fonte falhar autorização - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="e3469-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="e3469-131">`.nuspec` versão do intervalo deve substituir a versão - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="e3469-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="e3469-132">NuGet 3.3.0 atualização falha com '... uma restrição adicional definido em Packages. config impede que esta operação.'</span><span class="sxs-lookup"><span data-stu-id="e3469-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="e3469-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="e3469-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="e3469-134">atualização de NuGet.exe descarta o nome forte do assembly e o atributo particular.</span><span class="sxs-lookup"><span data-stu-id="e3469-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="e3469-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="e3469-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="e3469-136">Corrigir problemas com o caminho relativo do arquivo para "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="e3469-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="e3469-137">Melhorar a mensagens de falha de resolvedor de Update - [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="e3469-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="e3469-138">Recursos e alterações de comportamento</span><span class="sxs-lookup"><span data-stu-id="e3469-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="e3469-139">NuGet.exe push - o parâmetro de tempo limite não funciona - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="e3469-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="e3469-140">restauração de NuGet.exe não produza `.props` e `.targets` arquivos para `.nuproj` projetos (regressão v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="e3469-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="e3469-141">Precisa de extensibilidade de API para comparar as estruturas de importações - [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="e3469-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="e3469-142">Ocultar as opções da dependência ao usar `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="e3469-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="e3469-143">Imprimir o cabeçalho de versão nuget.exe na saída detalhada - [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="e3469-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="e3469-144">NuGet deve adicionar suporte para /nativeassets/ /runtimes/ {rid} {txm}- [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="e3469-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>