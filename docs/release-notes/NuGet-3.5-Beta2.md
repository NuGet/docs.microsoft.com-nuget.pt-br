---
title: Notas de versão do 3,5 beta2
description: Notas de versão do NuGet 3,5 Beta 2, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776389"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="70c81-103">Notas de versão do NuGet 3,5 beta2</span><span class="sxs-lookup"><span data-stu-id="70c81-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="70c81-104">Notas de versão do [NuGet 3,5-Beta](../release-notes/nuget-3.5-Beta.md)  |  [Notas de versão do NuGet 3,5-RC](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="70c81-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="70c81-105">O NuGet 3,5 Beta 2 RTM foi lançado em 27 de junho de 2016 para Visual Studio 2013 e nuget.exe</span><span class="sxs-lookup"><span data-stu-id="70c81-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="70c81-106">Changelog completo</span><span class="sxs-lookup"><span data-stu-id="70c81-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="70c81-107">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="70c81-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="70c81-108">Correções de bugs</span><span class="sxs-lookup"><span data-stu-id="70c81-108">Bug Fixes</span></span>

* <span data-ttu-id="70c81-109">Mensagem de erro atualizada para falta de suporte para a senha decrpytion no .NET Core para feeds autenticados- [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="70c81-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="70c81-110">O console do Gerenciador de pacotes Get-Package falhará se o projeto do .NET Core estiver aberto- [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="70c81-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="70c81-111">Corrija o tratamento incorreto de 403 no comando de push do NuGet [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="70c81-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="70c81-112">Corrija problemas na desinstalação de pacotes em uma solução associada ao controle do código-fonte do TFS quando disableSourceControlIntegration está definido como true- [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="70c81-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="70c81-113">Corrija a atualização do pacote para levar em conta pacotes de não-destino- [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="70c81-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="70c81-114">Use o nível de detalhes do MSBuild para definir o nível de agente para ações de interface do usuário do Gerenciador de pacotes NuGet- [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="70c81-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="70c81-115">Corrigir a configuração do NuGet é um erro inválido nos projetos do site – VSIX do VS 2015 (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="70c81-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="70c81-116">Problemas de correção de pacote `.csproj` quando arquivos de conteúdo são incluídos- [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="70c81-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="70c81-117">Defaultpushname in `NuGetDefaults.Config` ( `ProgramData\NuGet` ) não funciona – [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="70c81-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="70c81-118">Correção do problema na versão do NuGet 3.4.3-o valor não pode ser nulo na criação do pacote- [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="70c81-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="70c81-119">Restore usa credenciais armazenadas do Nuget.Config para feeds do VSTS- [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="70c81-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="70c81-120">Desempenho-corrigir alocações excessivas no código de análise da versão- [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="70c81-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="70c81-121">Corrigir problemas quando várias instâncias do nuget.exe tentam instalar o mesmo pacote em paralelo- [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="70c81-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="70c81-122">Informações de dependência de cache de desempenho para operações de vários projetos- [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="70c81-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="70c81-123">Correção do problema em que as origens do pacote não foi possível ser adicionadas das configurações quando a lista de origem está vazia- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="70c81-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="70c81-124">Corrigir erro enganoso ao tentar instalar o pacote que depende do tempo de design fachadas- [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="70c81-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="70c81-125">Instalar um pacote do console do PackageManager com a configuração "All" tenta somente a primeira fonte- [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="70c81-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="70c81-126">Corrigir problemas com pacotes que têm arquivos com tempos de gravação no futuro (mono)- [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="70c81-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="70c81-127">Exibir exceção quando houver uma falha ao localizar projetos no comando update- [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="70c81-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="70c81-128">O conteúdo do pacote não é restaurado corretamente ao instalar um pacote de um feed do NuGet v 3.3 + com o argumento-NoCache quando o pacote contém `.nupkg` arquivos- [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="70c81-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="70c81-129">Correção do problema com a instalação do pacote (todas as fontes) quando o pacote está faltando em 1 fonte- [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="70c81-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="70c81-130">Instalar blocos se uma única fonte falhar na autorização- [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="70c81-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="70c81-131">`.nuspec` o intervalo de versão deve substituir-IncludeReferencedProjects versão- [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="70c81-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="70c81-132">Falha na atualização do NuGet 3.3.0 com ' uma restrição adicional... definido em packages.config impede esta operação. '</span><span class="sxs-lookup"><span data-stu-id="70c81-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="70c81-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="70c81-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="70c81-134">nuget.exe atualização descarta o nome forte do assembly e o atributo privado.</span><span class="sxs-lookup"><span data-stu-id="70c81-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="70c81-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="70c81-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="70c81-136">Corrigir problemas com o caminho de arquivo relativo para "defaultpushexception"- [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="70c81-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="70c81-137">Melhorar mensagens de falha do resolvedor de atualizações- [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="70c81-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="70c81-138">Recursos e alterações de comportamento</span><span class="sxs-lookup"><span data-stu-id="70c81-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="70c81-139">nuget.exe parâmetro Push-timeout não funciona – [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="70c81-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="70c81-140">nuget.exe Restore não produz `.props` e `.targets` arquivos para `.nuproj` projetos (regressão em v 3.4.3.855) – [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="70c81-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="70c81-141">Necessidade de API de extensibilidade para comparar estruturas com importações- [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="70c81-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="70c81-142">Ocultar opções de dependência ao usar `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="70c81-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="70c81-143">Imprimir nuget.exe cabeçalho da versão na saída detalhada- [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="70c81-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="70c81-144">O NuGet deve adicionar suporte para/runtimes/{RID}/nativeassets/{TXM}/- [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="70c81-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>