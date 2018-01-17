---
title: "3.5 notas de versão Beta2 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0b76064f-0607-438a-bbf8-dd862690f48e
description: "Notas de versão do NuGet 3.5 Beta 2, incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão Beta 2 do NuGet 3.5, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6dd388e52308d2f3cd32d4d6c66c2868f0ae2a41
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="35-beta2-release-notes"></a><span data-ttu-id="dbfa4-104">3.5 notas de versão Beta2</span><span class="sxs-lookup"><span data-stu-id="dbfa4-104">3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="dbfa4-105">[Notas de versão 3.5 Beta do NuGet](../release-notes/nuget-3.5-Beta.md) | [notas de versão de RC 3.5 do NuGet](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-105">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="dbfa4-106">NuGet 3.5 Beta 2 RTM foi lançado em 27 de junho de 2016 para Visual Studio 2013 e nuget.exe</span><span class="sxs-lookup"><span data-stu-id="dbfa4-106">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="dbfa4-107">Log de alteração completa</span><span class="sxs-lookup"><span data-stu-id="dbfa4-107">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="dbfa4-108">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="dbfa4-108">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

# <a name="notable-changes"></a><span data-ttu-id="dbfa4-109">Alterações importantes</span><span class="sxs-lookup"><span data-stu-id="dbfa4-109">Notable Changes</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="dbfa4-110">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="dbfa4-110">Bug Fixes</span></span>

* <span data-ttu-id="dbfa4-111">Mensagem de erro atualizado à falta de suporte para decrpytion de senha no núcleo do .NET para feeds autenticados - [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-111">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="dbfa4-112">Get-pacote do Console do Gerenciador de pacote falhará se o projeto .NET Core é aberto - [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-112">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="dbfa4-113">Corrija o tratamento incorreto de 403 no comando de envio por push do NuGet [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-113">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="dbfa4-114">Corrigir problemas de desinstalar os pacotes em uma solução associada ao controle de origem do TFS quando disableSourceControlIntegration está definido como true - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-114">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="dbfa4-115">Corrigir a atualização de pacote para pacotes de destino não conta - [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-115">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="dbfa4-116">Usar o nível de detalhamento do MSBuild para definir o nível de agente de log para o Gerenciador de pacote do Nuget ações de interface do usuário - [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-116">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="dbfa4-117">Configuração de NuGet de correção é erro inválido em projetos de site - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-117">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="dbfa4-118">Corrigir problemas do pacote de `.csproj` quando os arquivos de conteúdo são incluídos - [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-118">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="dbfa4-119">DefaultPushSource em `NuGetDefaults.Config` (`ProgramData\NuGet`) não funciona - [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-119">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="dbfa4-120">Corrija o problema na versão do Nuget 3.4.3 - valor não pode ser nulo na criação do pacote - [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-120">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="dbfa4-121">Restauração usa credenciais armazenadas do NuGet. config para feeds do VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-121">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="dbfa4-122">Desempenho - alocações excessivas de correção no código da versão comparsion - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-122">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="dbfa4-123">Corrigir problemas quando várias instâncias do nuget.exe tenta instalar o mesmo pacote em paralelo - [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-123">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="dbfa4-124">Desempenho - informações de dependência de Cache para operações de multiprojetos - [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-124">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="dbfa4-125">Corrija o problema onde adicionado das configurações de fontes de pacote não foi possível quando a lista de origem está vazia - [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-125">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="dbfa4-126">Corrija o erro falsas durante a tentativa de instalar o pacote que depende de tempo de design fachadas - [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-126">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="dbfa4-127">Instalação de um pacote do console PackageManager com a configuração de "All" tenta somente primeira fonte - [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-127">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="dbfa4-128">Corrigir problemas com os pacotes que têm arquivos com tempos de gravação no futuro (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-128">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="dbfa4-129">Exibir a exceção quando há uma falha de projetos de localização no comando update - [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-129">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="dbfa4-130">Conteúdo do pacote não será restaurado corretamente quando instalar um pacote do nuget v3.3 + feed com o argumento - NoCache quando o pacote contiver `.nupkg` arquivos - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-130">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="dbfa4-131">Corrigir o problema com o pacote de instalação (todas as fontes) quando o pacote está ausente da 1 origem - [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-131">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="dbfa4-132">Instalar blocos se uma única fonte não será autorizada - [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-132">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="dbfa4-133">`.nuspec`versão do intervalo deve substituir a versão - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-133">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="dbfa4-134">Falha de atualização do NuGet 3.3.0 '... uma restrição adicional definida no Packages impede esta operação.'</span><span class="sxs-lookup"><span data-stu-id="dbfa4-134">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="dbfa4-135"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-135"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="dbfa4-136">atualização de NuGet.exe descarta o nome forte do assembly e o atributo privado.</span><span class="sxs-lookup"><span data-stu-id="dbfa4-136">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="dbfa4-137"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-137"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="dbfa4-138">Corrigir problemas com o caminho de arquivo relativo para "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-138">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="dbfa4-139">Melhorar a mensagens de falha do resolvedor de atualização - [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-139">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="dbfa4-140">Recursos e alterações de comportamento</span><span class="sxs-lookup"><span data-stu-id="dbfa4-140">Features and Behavior Changes</span></span>

* <span data-ttu-id="dbfa4-141">NuGet.exe push - o parâmetro de tempo limite não funciona - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-141">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="dbfa4-142">restauração de NuGet.exe não produz `.props` e `.targets` arquivos de `.nuproj` projetos (regressão em v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-142">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="dbfa4-143">Precisa de extensibilidade de API para comparar estruturas com importações - [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-143">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="dbfa4-144">Ocultar as opções da dependência ao usar `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-144">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="dbfa4-145">Impressão do cabeçalho de versão de nuget.exe na saída detalhada - [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-145">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="dbfa4-146">NuGet deve adicionar suporte para /nativeassets/ /runtimes/ {rid} {txm}- [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="dbfa4-146">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>