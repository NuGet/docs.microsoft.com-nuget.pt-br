---
title: Notas de versão do NuGet 5.10
description: Notas sobre a versão do NuGet 5.10, incluindo novos recursos, correções de bugs e DCRs.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356532"
---
# <a name="nuget-510-release-notes"></a><span data-ttu-id="84a4f-103">Notas de versão do NuGet 5.10</span><span class="sxs-lookup"><span data-stu-id="84a4f-103">NuGet 5.10 Release Notes</span></span>

<span data-ttu-id="84a4f-104">Veículos de distribuição do NuGet:</span><span class="sxs-lookup"><span data-stu-id="84a4f-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="84a4f-105">Versão do NuGet</span><span class="sxs-lookup"><span data-stu-id="84a4f-105">NuGet version</span></span> | <span data-ttu-id="84a4f-106">Disponível na versão do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="84a4f-106">Available in Visual Studio version</span></span> | <span data-ttu-id="84a4f-107">Disponível em SDKs do .NET</span><span class="sxs-lookup"><span data-stu-id="84a4f-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="84a4f-108">**5.10.0**</span><span class="sxs-lookup"><span data-stu-id="84a4f-108">**5.10.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="84a4f-109">Visual Studio 2019 versão 16.10</span><span class="sxs-lookup"><span data-stu-id="84a4f-109">Visual Studio 2019 version 16.10</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="84a4f-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="84a4f-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |

<span data-ttu-id="84a4f-111"><sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core</span><span class="sxs-lookup"><span data-stu-id="84a4f-111"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="84a4f-112">Visual Studio 16.10, MSBuild 16.10 e .NET 5.0.300+ requer NuGet.exe 5.10 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="84a4f-112">Visual Studio 16.10, MSBuild 16.10, and .NET 5.0.300+ requires NuGet.exe 5.10 or later.</span></span>

## <a name="summary-whats-new-in-510"></a><span data-ttu-id="84a4f-113">Resumo: Novidades na versão 5.10</span><span class="sxs-lookup"><span data-stu-id="84a4f-113">Summary: What's New in 5.10</span></span>

* <span data-ttu-id="84a4f-114">Assinatura: implementar o comando dotnet trusted-signers – [#8053](https://github.com/NuGet/Home/issues/8053)</span><span class="sxs-lookup"><span data-stu-id="84a4f-114">Signing: implement dotnet trusted-signers command - [#8053](https://github.com/NuGet/Home/issues/8053)</span></span>

* <span data-ttu-id="84a4f-115">Tornar a validação padrão desabilitada no Linux, mas habilitada por padrão no Windows – [#10713](https://github.com/NuGet/Home/issues/10713)</span><span class="sxs-lookup"><span data-stu-id="84a4f-115">Make default validation disabled on Linux, but enabled by default on Windows - [#10713](https://github.com/NuGet/Home/issues/10713)</span></span>

* <span data-ttu-id="84a4f-116">Adicionar uma variável ENV para verificação de assinatura de pacote no .NET 5+ Linux/MAC – [#10742](https://github.com/NuGet/Home/issues/10742)</span><span class="sxs-lookup"><span data-stu-id="84a4f-116">Add an ENV Variable for Package Signing Verification on .NET 5+ Linux/MAC - [#10742](https://github.com/NuGet/Home/issues/10742)</span></span>

* <span data-ttu-id="84a4f-117">Melhorar o desempenho da instalação do novo pacote para soluções [grandes – #10166](https://github.com/NuGet/Home/issues/10166)</span><span class="sxs-lookup"><span data-stu-id="84a4f-117">Improve install new package performance for large solutions - [#10166](https://github.com/NuGet/Home/issues/10166)</span></span>

* <span data-ttu-id="84a4f-118">Adicione o tipo de `nfproj` projeto à lista de supportedProjectExtensions para a CLI do Nuget.</span><span class="sxs-lookup"><span data-stu-id="84a4f-118">Add the project type `nfproj` to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="84a4f-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="84a4f-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="84a4f-120">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="84a4f-120">Issues fixed in this release</span></span>

* <span data-ttu-id="84a4f-121">Suprimir <requireLicenseAcceptance> o elemento ao empacotar um projeto – [#5133](https://github.com/NuGet/Home/issues/5133)</span><span class="sxs-lookup"><span data-stu-id="84a4f-121">Suppress the <requireLicenseAcceptance> element when packing a project - [#5133](https://github.com/NuGet/Home/issues/5133)</span></span>

* <span data-ttu-id="84a4f-122">O aviso de visualização [CPVM] deve ser mostrado na cli do dotnet – [#10226](https://github.com/NuGet/Home/issues/10226)</span><span class="sxs-lookup"><span data-stu-id="84a4f-122">[CPVM] preview warning should be shown on dotnet cli - [#10226](https://github.com/NuGet/Home/issues/10226)</span></span>

* <span data-ttu-id="84a4f-123">Atualize os tokens de cor da tela de fundo e de primeiro plano do PMUI para CommonDocumentColors – [#10608](https://github.com/NuGet/Home/issues/10608)</span><span class="sxs-lookup"><span data-stu-id="84a4f-123">Update the background and foreground color tokens of the PMUI to CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)</span></span>

* <span data-ttu-id="84a4f-124">[Bug Bash] O erro "operação cancelada pelo usuário" aparece na janela Lista de Erros ao alternar entre guias rapidamente na interface do usuário do PM [– #10671](https://github.com/NuGet/Home/issues/10671)</span><span class="sxs-lookup"><span data-stu-id="84a4f-124">[Bug Bash] Error “operation canceled by user” show in Error List window when switching between tabs quickly in PM UI - [#10671](https://github.com/NuGet/Home/issues/10671)</span></span>

* <span data-ttu-id="84a4f-125">Interface do usuário do PM: melhorar o desempenho da instalação do pacote no nível da solução – [#10210](https://github.com/NuGet/Home/issues/10210)</span><span class="sxs-lookup"><span data-stu-id="84a4f-125">PM UI:  Improve package installation performance on the solution level - [#10210](https://github.com/NuGet/Home/issues/10210)</span></span>

* <span data-ttu-id="84a4f-126">Substitua GetService por GetServiceAsync em todos os lugares no NuGet.Clients – [#3784](https://github.com/NuGet/Home/issues/3784)</span><span class="sxs-lookup"><span data-stu-id="84a4f-126">Replace GetService with GetServiceAsync everywhere in NuGet.Clients - [#3784](https://github.com/NuGet/Home/issues/3784)</span></span>

* <span data-ttu-id="84a4f-127">NuGet.exe de desempenho do pacote com `..` caminho relativo – [#5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="84a4f-127">NuGet.exe pack performance problem with `..` relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>

* <span data-ttu-id="84a4f-128">O desempenho do "pacote nuget" diminui com níveis crescentes nos caminhos de origem – [#5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="84a4f-128">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>

* <span data-ttu-id="84a4f-129">O NuGet não erro ao empacotar nuspec com arquivos duplicados.</span><span class="sxs-lookup"><span data-stu-id="84a4f-129">NuGet doesn't error when packaging nuspec with duplicate files.</span></span><span data-ttu-id="84a4f-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span><span class="sxs-lookup"><span data-stu-id="84a4f-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span></span>

* <span data-ttu-id="84a4f-131">Pacote NuGet "O DateTimeOffset especificado não pode ser convertido em um data/hora do arquivo Zip" – [#7001](https://github.com/NuGet/Home/issues/7001)</span><span class="sxs-lookup"><span data-stu-id="84a4f-131">NuGet pack "The DateTimeOffset specified cannot be converted into a Zip file timestamp" - [#7001](https://github.com/NuGet/Home/issues/7001)</span></span>

* <span data-ttu-id="84a4f-132">Os tempos de data/hora do arquivo do pacote empacotado são deslocados pelo timezone – [#7395](https://github.com/NuGet/Home/issues/7395)</span><span class="sxs-lookup"><span data-stu-id="84a4f-132">Timestamps of file of packed package is shifted by the timezone - [#7395](https://github.com/NuGet/Home/issues/7395)</span></span>

* <span data-ttu-id="84a4f-133">NU1004 deve conter informações [](https://github.com/NuGet/Home/issues/7696) mais a #7696</span><span class="sxs-lookup"><span data-stu-id="84a4f-133">NU1004 should contain more actionable information  - [#7696](https://github.com/NuGet/Home/issues/7696)</span></span>

* <span data-ttu-id="84a4f-134">[Bug Bash] [Falha de teste] O arquivo de bloqueio vazio/malformado não deve ser atualizado ao executar 'dotnet restore --use-lock-file --locked-mode' – [#8640](https://github.com/NuGet/Home/issues/8640)</span><span class="sxs-lookup"><span data-stu-id="84a4f-134">[Bug Bash][Test Failure] The empty/malformed lock file should not be updated when running ‘dotnet restore --use-lock-file --locked-mode’ - [#8640](https://github.com/NuGet/Home/issues/8640)</span></span>

* <span data-ttu-id="84a4f-135">NuGetVersionRange permite que intervalos logicamente incorretos sejam analisados – [#9145](https://github.com/NuGet/Home/issues/9145)</span><span class="sxs-lookup"><span data-stu-id="84a4f-135">NuGetVersionRange allows logically incorrect ranges to be parsed - [#9145](https://github.com/NuGet/Home/issues/9145)</span></span>

* <span data-ttu-id="84a4f-136">A interface do usuário do PM não pode mostrar a cor da tela de fundo distinguível entre as fontes de pacote selecionadas e com foco – [#9538](https://github.com/NuGet/Home/issues/9538)</span><span class="sxs-lookup"><span data-stu-id="84a4f-136">PM UI can’t show distinguishable background color between selected and hovered package sources - [#9538](https://github.com/NuGet/Home/issues/9538)</span></span>

* <span data-ttu-id="84a4f-137">A caixa de seleção para selecionar projetos a serem instalados não está sendo lida pelo leitor de tela – [#9578](https://github.com/NuGet/Home/issues/9578)</span><span class="sxs-lookup"><span data-stu-id="84a4f-137">Checkbox for selecting projects to install to isn't being read by screen reader - [#9578](https://github.com/NuGet/Home/issues/9578)</span></span>

* <span data-ttu-id="84a4f-138">A seleção padrão do menu suspenso Versões do Painel de Detalhes deve ser Installed/LatestStable nas guias [Instalados/Atualizações – #9887](https://github.com/NuGet/Home/issues/9887)</span><span class="sxs-lookup"><span data-stu-id="84a4f-138">Details Pane Versions Dropdown default selection should be Installed/LatestStable on Installed/Updates tabs - [#9887](https://github.com/NuGet/Home/issues/9887)</span></span>

* <span data-ttu-id="84a4f-139">Remover a conta alternativa de alguns SDKs do .NET 5 report TargetPlatformMoniker da ` ,Version= `  -  [#9913](https://github.com/NuGet/Home/issues/9913)</span><span class="sxs-lookup"><span data-stu-id="84a4f-139">Remove workaround account for some .NET 5 SDKs report TargetPlatformMoniker of ` ,Version= ` - [#9913](https://github.com/NuGet/Home/issues/9913)</span></span>

* <span data-ttu-id="84a4f-140">dotnet nuget verify is too quiet - [#10316](https://github.com/NuGet/Home/issues/10316)</span><span class="sxs-lookup"><span data-stu-id="84a4f-140">dotnet nuget verify is too quiet - [#10316](https://github.com/NuGet/Home/issues/10316)</span></span>

* <span data-ttu-id="84a4f-141">VersionRange não pode analisar intervalos de dígito único [– #10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="84a4f-141">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>

* <span data-ttu-id="84a4f-142">O Gerenciador de Soluções do VS lança uma exceção nula para durante a depuração [– #10352](https://github.com/NuGet/Home/issues/10352)</span><span class="sxs-lookup"><span data-stu-id="84a4f-142">VS Solution manager throws null exception for during debugging - [#10352](https://github.com/NuGet/Home/issues/10352)</span></span>

* <span data-ttu-id="84a4f-143">Mover mensagens de exceção da CLI para arquivos de Recurso de Cadeia de Caracteres [– #10392](https://github.com/NuGet/Home/issues/10392)</span><span class="sxs-lookup"><span data-stu-id="84a4f-143">Move CLI exception messages to String Resource files - [#10392](https://github.com/NuGet/Home/issues/10392)</span></span>

* <span data-ttu-id="84a4f-144">Remover código morto (TabItemButtonAutomationPeer) – [#10435](https://github.com/NuGet/Home/issues/10435)</span><span class="sxs-lookup"><span data-stu-id="84a4f-144">Remove dead code (TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)</span></span>

* <span data-ttu-id="84a4f-145">O menu de contexto de atualização deve rolar até o primeiro item [selecionado – #10498](https://github.com/NuGet/Home/issues/10498)</span><span class="sxs-lookup"><span data-stu-id="84a4f-145">Update context menu should scroll to first selected item - [#10498](https://github.com/NuGet/Home/issues/10498)</span></span>

* <span data-ttu-id="84a4f-146">Detalhes da PMUI da Solução tem barra horizontal sobreposta – [#10533](https://github.com/NuGet/Home/issues/10533)</span><span class="sxs-lookup"><span data-stu-id="84a4f-146">Solution PMUI Details has overlapping horizontal bar - [#10533](https://github.com/NuGet/Home/issues/10533)</span></span>

* <span data-ttu-id="84a4f-147">Assinatura: detalhes da assinatura primária não exibidos quando o certificado expirou e o registro de data/hora não é [#10535](https://github.com/NuGet/Home/issues/10535)</span><span class="sxs-lookup"><span data-stu-id="84a4f-147">Signing:  primary signature details not displayed when certificate expired and timestamp untrusted - [#10535](https://github.com/NuGet/Home/issues/10535)</span></span>

* <span data-ttu-id="84a4f-148">Não ter fontes habilitadas impede que a interface do usuário do PM seja [#10541](https://github.com/NuGet/Home/issues/10541)</span><span class="sxs-lookup"><span data-stu-id="84a4f-148">Having no enabled sources prevents the PM UI from showing - [#10541](https://github.com/NuGet/Home/issues/10541)</span></span>

* <span data-ttu-id="84a4f-149">Os metadados do pacote (detalhes, preterição) às vezes não são retirados nuget.org em CodeSpaces – [#10549](https://github.com/NuGet/Home/issues/10549)</span><span class="sxs-lookup"><span data-stu-id="84a4f-149">Package Metadata (details, deprecation) are sometimes not pulled from nuget.org in CodeSpaces - [#10549](https://github.com/NuGet/Home/issues/10549)</span></span>

* <span data-ttu-id="84a4f-150">A inicialização do PMUI falha com exceção durante a sessão de depuração – [#10559](https://github.com/NuGet/Home/issues/10559)</span><span class="sxs-lookup"><span data-stu-id="84a4f-150">PMUI initialization fails with exception during debug session - [#10559](https://github.com/NuGet/Home/issues/10559)</span></span>

* <span data-ttu-id="84a4f-151">A restauração do nuget resulta em uma falha de verificação de integridade do pacote big endian sistema – [#10567](https://github.com/NuGet/Home/issues/10567)</span><span class="sxs-lookup"><span data-stu-id="84a4f-151">nuget restore results in a package integrity check failure on big endian system - [#10567](https://github.com/NuGet/Home/issues/10567)</span></span>

* <span data-ttu-id="84a4f-152">FormatException é lançada em vez de PackagingException [– #10595](https://github.com/NuGet/Home/issues/10595)</span><span class="sxs-lookup"><span data-stu-id="84a4f-152">FormatException is thrown instead of PackagingException - [#10595](https://github.com/NuGet/Home/issues/10595)</span></span>

* <span data-ttu-id="84a4f-153">CPVM – Problemas de concurreência no algoritmo de trilha de grafo – [#10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="84a4f-153">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>

* <span data-ttu-id="84a4f-154">Adicionar telemetria de versão do PMC powershell [– #10609](https://github.com/NuGet/Home/issues/10609)</span><span class="sxs-lookup"><span data-stu-id="84a4f-154">Add PMC powershell version telemetry - [#10609](https://github.com/NuGet/Home/issues/10609)</span></span>

* <span data-ttu-id="84a4f-155">Melhorar o desempenho de classificação do NuGetVersion [– #10611](https://github.com/NuGet/Home/issues/10611)</span><span class="sxs-lookup"><span data-stu-id="84a4f-155">Improve NuGetVersion sort performance - [#10611](https://github.com/NuGet/Home/issues/10611)</span></span>

* <span data-ttu-id="84a4f-156">Trusted-signers Add tem argumentos inconsistentes – [#10647](https://github.com/NuGet/Home/issues/10647)</span><span class="sxs-lookup"><span data-stu-id="84a4f-156">Trusted-signers Add has inconsistent arguments - [#10647](https://github.com/NuGet/Home/issues/10647)</span></span>

* <span data-ttu-id="84a4f-157">Vs2019 v16.9.0: Alternar guias no NuGet Gerenciador de Pacotes de "Atualizações" para "Instalado" não atualiza o quadro.</span><span class="sxs-lookup"><span data-stu-id="84a4f-157">Vs2019 v16.9.0: Switching tabs in NuGet Package Manager from "Updates" to "Installed" doesn't update the frame.</span></span><span data-ttu-id="84a4f-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span><span class="sxs-lookup"><span data-stu-id="84a4f-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span></span>

* <span data-ttu-id="84a4f-159">Remova o "v" do número de versão no PMUI – [#10677](https://github.com/NuGet/Home/issues/10677)</span><span class="sxs-lookup"><span data-stu-id="84a4f-159">Remove the "v" from the version number in PMUI - [#10677](https://github.com/NuGet/Home/issues/10677)</span></span>

* <span data-ttu-id="84a4f-160">INuGetProjectService.GetInstalledPackagesAsync é lançado antes de receber a indicação do sistema de projeto CPS – [#10681](https://github.com/NuGet/Home/issues/10681)</span><span class="sxs-lookup"><span data-stu-id="84a4f-160">INuGetProjectService.GetInstalledPackagesAsync throws before receiving CPS project system nomination - [#10681](https://github.com/NuGet/Home/issues/10681)</span></span>

* <span data-ttu-id="84a4f-161">Ícones inseridos causam Acesso Negado da fonte "Microsoft Visual Studio offline" na guia Procurar – [#10687](https://github.com/NuGet/Home/issues/10687)</span><span class="sxs-lookup"><span data-stu-id="84a4f-161">Embedded Icons cause Access Denied from source "Microsoft Visual Studio Offline Packages" on Browse tab - [#10687](https://github.com/NuGet/Home/issues/10687)</span></span>

* <span data-ttu-id="84a4f-162">INuGetProjectService.GetInstalledPackagesAsync é lançado quando MSBuildProjectExtensionsPath não está [definido – #10739](https://github.com/NuGet/Home/issues/10739)</span><span class="sxs-lookup"><span data-stu-id="84a4f-162">INuGetProjectService.GetInstalledPackagesAsync throws when MSBuildProjectExtensionsPath is not set - [#10739](https://github.com/NuGet/Home/issues/10739)</span></span>

* <span data-ttu-id="84a4f-163">"dotnet nuget remove source nuget.org" não funciona na primeira vez – [#10745](https://github.com/NuGet/Home/issues/10745)</span><span class="sxs-lookup"><span data-stu-id="84a4f-163">"dotnet nuget remove source nuget.org" doesn't work the first time - [#10745](https://github.com/NuGet/Home/issues/10745)</span></span>

* <span data-ttu-id="84a4f-164">O Nuget bloqueia um threadpool em um método assíncrono que faz uma chamada síncrona para o thread da interface do usuário – [#10775](https://github.com/NuGet/Home/issues/10775)</span><span class="sxs-lookup"><span data-stu-id="84a4f-164">Nuget blocks a threadpool thread in an async method making a synchronous call to the UI thread - [#10775](https://github.com/NuGet/Home/issues/10775)</span></span>

* <span data-ttu-id="84a4f-165">Ferramentas -> Opções -> cadeia de caracteres Gerenciador de Pacotes NuGet está truncada - [#10779](https://github.com/NuGet/Home/issues/10779)</span><span class="sxs-lookup"><span data-stu-id="84a4f-165">Tools -> Options -> NuGet Package Manager string is truncated - [#10779](https://github.com/NuGet/Home/issues/10779)</span></span>

* <span data-ttu-id="84a4f-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` é código inodado e prejudica o desempenho [– #10790](https://github.com/NuGet/Home/issues/10790)</span><span class="sxs-lookup"><span data-stu-id="84a4f-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` is dead code and hurting performance - [#10790](https://github.com/NuGet/Home/issues/10790)</span></span>

* <span data-ttu-id="84a4f-167">Usar o ícone inserido em pacotes do SDK do NuGet [– #10795](https://github.com/NuGet/Home/issues/10795)</span><span class="sxs-lookup"><span data-stu-id="84a4f-167">Use embedded icon in NuGet SDK packages - [#10795](https://github.com/NuGet/Home/issues/10795)</span></span>

* <span data-ttu-id="84a4f-168">Atualizar a lista de licenças SPDX [– #10806](https://github.com/NuGet/Home/issues/10806)</span><span class="sxs-lookup"><span data-stu-id="84a4f-168">Update the SPDX license list - [#10806](https://github.com/NuGet/Home/issues/10806)</span></span>

<span data-ttu-id="84a4f-169">**[Lista de todos os problemas corrigidos nesta versão – 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span><span class="sxs-lookup"><span data-stu-id="84a4f-169">**[List of all issues fixed in this release - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span></span>
  
<span data-ttu-id="84a4f-170">**[Lista de confirmações nesta versão – 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span><span class="sxs-lookup"><span data-stu-id="84a4f-170">**[List of commits in this release - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span></span>
  
### <a name="community-contributions"></a><span data-ttu-id="84a4f-171">Contribuições da comunidade</span><span class="sxs-lookup"><span data-stu-id="84a4f-171">Community contributions</span></span>

<span data-ttu-id="84a4f-172">Agradecemos a todos os colaboradores que ajudaram a tornar essa versão do NuGet incrível!</span><span class="sxs-lookup"><span data-stu-id="84a4f-172">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="84a4f-173">Quem</span><span class="sxs-lookup"><span data-stu-id="84a4f-173">Who</span></span>|<span data-ttu-id="84a4f-174">Prs</span><span class="sxs-lookup"><span data-stu-id="84a4f-174">PRs</span></span>|<span data-ttu-id="84a4f-175">Problemas</span><span class="sxs-lookup"><span data-stu-id="84a4f-175">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="84a4f-176">oda-z</span><span class="sxs-lookup"><span data-stu-id="84a4f-176">louis-z</span></span>](https://github.com/louis-z) | [<span data-ttu-id="84a4f-177">3991</span><span class="sxs-lookup"><span data-stu-id="84a4f-177">3991</span></span>](https://github.com/NuGet/NuGet.Client/pull/3991) | <span data-ttu-id="84a4f-178">VersionRange não pode analisar intervalos de dígito único [– #10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="84a4f-178">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>
[<span data-ttu-id="84a4f-179">omajid</span><span class="sxs-lookup"><span data-stu-id="84a4f-179">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="84a4f-180">3860</span><span class="sxs-lookup"><span data-stu-id="84a4f-180">3860</span></span>](https://github.com/NuGet/NuGet.Client/pull/3860) | <span data-ttu-id="84a4f-181">O build.sh NuGet.Client está [desfeito – #10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="84a4f-181">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="84a4f-182">Nirmal4G</span><span class="sxs-lookup"><span data-stu-id="84a4f-182">Nirmal4G</span></span>](https://github.com/Nirmal4G) | [<span data-ttu-id="84a4f-183">3623</span><span class="sxs-lookup"><span data-stu-id="84a4f-183">3623</span></span>](https://github.com/NuGet/NuGet.Client/pull/3623) | <span data-ttu-id="84a4f-184">O build.sh NuGet.Client está [desfeito – #10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="84a4f-184">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="84a4f-185">BlackGad</span><span class="sxs-lookup"><span data-stu-id="84a4f-185">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="84a4f-186">3953</span><span class="sxs-lookup"><span data-stu-id="84a4f-186">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="84a4f-187">O desempenho do "pacote nuget" diminui com níveis crescentes nos caminhos de origem – [#5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="84a4f-187">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>
[<span data-ttu-id="84a4f-188">BlackGad</span><span class="sxs-lookup"><span data-stu-id="84a4f-188">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="84a4f-189">3953</span><span class="sxs-lookup"><span data-stu-id="84a4f-189">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="84a4f-190">NuGet.exe de desempenho do pacote com ..</span><span class="sxs-lookup"><span data-stu-id="84a4f-190">NuGet.exe pack performance problem with ..</span></span> <span data-ttu-id="84a4f-191">caminho relativo – [#5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="84a4f-191">relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>
[<span data-ttu-id="84a4f-192">marcin-kryscianc</span><span class="sxs-lookup"><span data-stu-id="84a4f-192">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="84a4f-193">3940</span><span class="sxs-lookup"><span data-stu-id="84a4f-193">3940</span></span>](https://github.com/NuGet/NuGet.Client/pull/3940) | <span data-ttu-id="84a4f-194">CPVM – Problemas de concurreência no algoritmo de trilha de grafo – [#10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="84a4f-194">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>
[<span data-ttu-id="84a4f-195">simoes</span><span class="sxs-lookup"><span data-stu-id="84a4f-195">josesimoes</span></span>](https://github.com/josesimoes) | [<span data-ttu-id="84a4f-196">3943</span><span class="sxs-lookup"><span data-stu-id="84a4f-196">3943</span></span>](https://github.com/NuGet/NuGet.Client/pull/3943) | <span data-ttu-id="84a4f-197">Adicione o tipo de projeto nfproj à lista de supportedProjectExtensions para a CLI do Nuget.</span><span class="sxs-lookup"><span data-stu-id="84a4f-197">Add the project type nfproj to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="84a4f-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="84a4f-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

## <a name="feedback-welcome"></a><span data-ttu-id="84a4f-199">Boas-vindas aos comentários</span><span class="sxs-lookup"><span data-stu-id="84a4f-199">Feedback welcome</span></span>

<span data-ttu-id="84a4f-200">Seus comentários são importantes para nós.</span><span class="sxs-lookup"><span data-stu-id="84a4f-200">Your feedback is important to us.</span></span>  <span data-ttu-id="84a4f-201">Se houver problemas com esta versão, verifique os problemas do [GitHub](https://github.com/NuGet/Home/issues) e a [comunidade de desenvolvedores do Visual Studio](https://developercommunity.visualstudio.com/) para obter os problemas existentes.</span><span class="sxs-lookup"><span data-stu-id="84a4f-201">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="84a4f-202">Para novos problemas no NuGet, informe um [problema do GitHub](https://github.com/NuGet/Home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="84a4f-202">For new issues within NuGet, please report a [GitHub Issue](https://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="84a4f-203">Para problemas gerais de experiência do NuGet, informe-nos por meio do [relatório uma opção de problema](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) encontrada em seu IDE favorito em **ajuda > relatar um problema**.</span><span class="sxs-lookup"><span data-stu-id="84a4f-203">For general NuGet experience issues, let us know via the [Report a Problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>
