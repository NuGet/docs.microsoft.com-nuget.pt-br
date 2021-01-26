---
title: Notas de versão do NuGet 5,2 RTM
description: Notas de versão do NuGet 5,2, incluindo novos recursos, correções de bugs e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: 25fa1d09046a583fb987b9f3dd51a0099f4331a7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776211"
---
# <a name="nuget-52-release-notes"></a><span data-ttu-id="e1aed-103">Notas de versão do NuGet 5,2</span><span class="sxs-lookup"><span data-stu-id="e1aed-103">NuGet 5.2 Release Notes</span></span>

<span data-ttu-id="e1aed-104">Veículos de distribuição do NuGet:</span><span class="sxs-lookup"><span data-stu-id="e1aed-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="e1aed-105">Versão do NuGet</span><span class="sxs-lookup"><span data-stu-id="e1aed-105">NuGet version</span></span> | <span data-ttu-id="e1aed-106">Disponível na versão do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e1aed-106">Available in Visual Studio version</span></span>| <span data-ttu-id="e1aed-107">Disponível em SDKs do .NET</span><span class="sxs-lookup"><span data-stu-id="e1aed-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="e1aed-108">**5.2.0**</span><span class="sxs-lookup"><span data-stu-id="e1aed-108">**5.2.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="e1aed-109">Visual Studio 2019 versão 16,2</span><span class="sxs-lookup"><span data-stu-id="e1aed-109">Visual Studio 2019 version 16.2</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="e1aed-110">[2.1.80 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="e1aed-110">[2.1.80X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="e1aed-111"><sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core</span><span class="sxs-lookup"><span data-stu-id="e1aed-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="e1aed-112"><sup>2</sup> Disponível como uma instalação opcional com o Visual Studio 2019 com carga de trabalho do .NET Core</span><span class="sxs-lookup"><span data-stu-id="e1aed-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-52"></a><span data-ttu-id="e1aed-113">Resumo: o que há de novo no 5,2</span><span class="sxs-lookup"><span data-stu-id="e1aed-113">Summary: What's New in 5.2</span></span>

* <span data-ttu-id="e1aed-114">Correção de um bug crítico que causava falhas ocasionais de operação do NuGet devido a problemas de caminho no Linux & Mac- [#7341](https://github.com/NuGet/Home/issues/7341)</span><span class="sxs-lookup"><span data-stu-id="e1aed-114">Fixed a critical bug that caused occasional NuGet operation failures due to path issues on Linux & Mac - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

* <span data-ttu-id="e1aed-115">Melhor capacidade de resposta da interface do usuário ao procurar pacotes usando a interface do usuário do Gerenciador de pacotes NuGet no Visual Studio, especialmente perceptível para fontes lentas- [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="e1aed-115">Improved UI responsiveness when browsing packages using the NuGet package manager UI in Visual Studio especially noticeable for slow sources - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="e1aed-116">Toneladas de correções de confiabilidade para arquivos de bloqueio ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) e plug-in de autenticação ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))</span><span class="sxs-lookup"><span data-stu-id="e1aed-116">Tons of reliability fixes for lock file ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) and authentication plugin ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="e1aed-117">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="e1aed-117">Issues fixed in this release</span></span>

<span data-ttu-id="e1aed-118">**Bugs**</span><span class="sxs-lookup"><span data-stu-id="e1aed-118">**Bugs**</span></span>

* <span data-ttu-id="e1aed-119">Perf: console do Gerenciador de pacotes: atraso da interface do usuário atualizando o valor selecionado da ComboBox "projeto padrão"- [#8235](https://github.com/NuGet/Home/issues/8235)</span><span class="sxs-lookup"><span data-stu-id="e1aed-119">Perf: Package Manager Console:  UI delay updating "Default project" combobox selected value - [#8235](https://github.com/NuGet/Home/issues/8235)</span></span>

* <span data-ttu-id="e1aed-120">Desempenho: melhorias de desempenho na interface do usuário do PM- [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="e1aed-120">Perf: Performance improvements in the PM UI - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="e1aed-121">Perf: atraso da interface do usuário ao ler o projeto padrão no PMC- [#6824](https://github.com/NuGet/Home/issues/6824)</span><span class="sxs-lookup"><span data-stu-id="e1aed-121">Perf: UI Delay when reading Default Project in PMC - [#6824](https://github.com/NuGet/Home/issues/6824)</span></span>

* <span data-ttu-id="e1aed-122">Perf: [vsfeedback] guia de atualização do NuGet congela para um pacote local fonte- [#6470](https://github.com/NuGet/Home/issues/6470)</span><span class="sxs-lookup"><span data-stu-id="e1aed-122">Perf: [vsfeedback] NuGet Update tab freezes for a local package source - [#6470](https://github.com/NuGet/Home/issues/6470)</span></span>

* <span data-ttu-id="e1aed-123">Plug-ins: o NuGet aguarda o tempo limite completo de handshake se o plug-in falhar ao iniciar ou encerrar o [#8300](https://github.com/NuGet/Home/issues/8300) inicial</span><span class="sxs-lookup"><span data-stu-id="e1aed-123">Plugins:  NuGet waits full handshake timeout if plugin fails to launch or terminates early - [#8300](https://github.com/NuGet/Home/issues/8300)</span></span>

* <span data-ttu-id="e1aed-124">Plugins: melhorar o diagnóstico da falha de inicialização do plug-in- [#8271](https://github.com/NuGet/Home/issues/8271)</span><span class="sxs-lookup"><span data-stu-id="e1aed-124">Plugins:  improve diagnosability of plugin launch failure - [#8271](https://github.com/NuGet/Home/issues/8271)</span></span>

* <span data-ttu-id="e1aed-125">Plug-ins: problema com a descoberta de nuget.exe de plugins internos- [#8269](https://github.com/NuGet/Home/issues/8269)</span><span class="sxs-lookup"><span data-stu-id="e1aed-125">Plugins: Issue with nuget.exe discovery of built in plugins - [#8269](https://github.com/NuGet/Home/issues/8269)</span></span>

* <span data-ttu-id="e1aed-126">Plugins: o arquivo de cache nunca é de leitura- [#8210](https://github.com/NuGet/Home/issues/8210)</span><span class="sxs-lookup"><span data-stu-id="e1aed-126">Plugins:  cache file is never read - [#8210](https://github.com/NuGet/Home/issues/8210)</span></span>

* <span data-ttu-id="e1aed-127">Plugins: "uma tarefa foi cancelada".</span><span class="sxs-lookup"><span data-stu-id="e1aed-127">Plugins:  "A task was canceled."</span></span> <span data-ttu-id="e1aed-128">erros com o plug-in de autenticação durante a restauração- [#8198](https://github.com/NuGet/Home/issues/8198)</span><span class="sxs-lookup"><span data-stu-id="e1aed-128">errors with authentication plugin during restore - [#8198](https://github.com/NuGet/Home/issues/8198)</span></span>

* <span data-ttu-id="e1aed-129">Cache de plugins não detectável intermitentemente em plataformas Linux- [#7845](https://github.com/NuGet/Home/issues/7845)</span><span class="sxs-lookup"><span data-stu-id="e1aed-129">Plugins cache not discoverable intermittently on linux platforms - [#7845](https://github.com/NuGet/Home/issues/7845)</span></span>

* <span data-ttu-id="e1aed-130">Lockfile: com o ATF, ele tem falso NU1004 devido a uma verificação de igualdade de estrutura de destino inadequada- [#8187](https://github.com/NuGet/Home/issues/8187)</span><span class="sxs-lookup"><span data-stu-id="e1aed-130">LockFile: with ATF, it has false NU1004 due to a bad target framework equality check - [#8187](https://github.com/NuGet/Home/issues/8187)</span></span>

* <span data-ttu-id="e1aed-131">Lockfile: '--modo bloqueado ' ' sinalizador de restauração não respeitado se o arquivo de bloqueio estiver vazio ou malformado- [#8160](https://github.com/NuGet/Home/issues/8160)</span><span class="sxs-lookup"><span data-stu-id="e1aed-131">LockFile: '--locked-mode' restore flag not respected if lock file is empty or malformed - [#8160](https://github.com/NuGet/Home/issues/8160)</span></span>

* <span data-ttu-id="e1aed-132">Lockfile: não há projetos em minúsculas com nomes de assembly personalizados em pacotes bloquear arquivo- [#8114](https://github.com/NuGet/Home/issues/8114)</span><span class="sxs-lookup"><span data-stu-id="e1aed-132">LockFile: Don't lowercase projects with custom assembly names in packages lock file - [#8114](https://github.com/NuGet/Home/issues/8114)</span></span>

* <span data-ttu-id="e1aed-133">Lockfile: tornar a referência do projeto em minúsculas no arquivo de bloqueio- [#7840](https://github.com/NuGet/Home/issues/7840)</span><span class="sxs-lookup"><span data-stu-id="e1aed-133">LockFile: Make project reference lower case in lock file  - [#7840](https://github.com/NuGet/Home/issues/7840)</span></span>

* <span data-ttu-id="e1aed-134">Restaurar: a instalação de um pacote assinado violado resulta em várias tentativas de instalação com falha (com saída repetida)- [#8175](https://github.com/NuGet/Home/issues/8175)</span><span class="sxs-lookup"><span data-stu-id="e1aed-134">Restore:  installing a tampered signed package results in multiple failed install attempts (with repeated output) - [#8175](https://github.com/NuGet/Home/issues/8175)</span></span>

* <span data-ttu-id="e1aed-135">VS: as opções de usuário da solução falham ao desserializar após a atualização do NuGet- [#8166](https://github.com/NuGet/Home/issues/8166)</span><span class="sxs-lookup"><span data-stu-id="e1aed-135">VS: solution user options fail to deserialize after NuGet update - [#8166](https://github.com/NuGet/Home/issues/8166)</span></span>

* <span data-ttu-id="e1aed-136">dotnet-List-Package em um projeto UnitTest retorna um erro- [#8154](https://github.com/NuGet/Home/issues/8154)</span><span class="sxs-lookup"><span data-stu-id="e1aed-136">dotnet-list-package in a UnitTest project returns an error - [#8154](https://github.com/NuGet/Home/issues/8154)</span></span>

* <span data-ttu-id="e1aed-137">Criar grupo de pacotes NuGet para o instalador do VS – corrigindo alguns problemas de configuração do VSIX- [#8033](https://github.com/NuGet/Home/issues/8033)</span><span class="sxs-lookup"><span data-stu-id="e1aed-137">Create NuGet package group for VS installer - fixing some VSIX setup problems - [#8033](https://github.com/NuGet/Home/issues/8033)</span></span>

* <span data-ttu-id="e1aed-138">GeneratePackageOnBuild não deve definir nobuild.</span><span class="sxs-lookup"><span data-stu-id="e1aed-138">GeneratePackageOnBuild should not set NoBuild.</span></span><span data-ttu-id="e1aed-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span><span class="sxs-lookup"><span data-stu-id="e1aed-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span></span>

* <span data-ttu-id="e1aed-140">A nova opção "-SymbolPackageFormat snupkg" gera um erro quando o arquivo. nuspec contém um elemento de referência de assembly explícito- [#7638](https://github.com/NuGet/Home/issues/7638)</span><span class="sxs-lookup"><span data-stu-id="e1aed-140">The new option "-SymbolPackageFormat snupkg" generates an error when the .nuspec file contains an explicit assembly reference element - [#7638](https://github.com/NuGet/Home/issues/7638)</span></span>

* <span data-ttu-id="e1aed-141">NuGet. targets (498, 5): erro: não foi possível encontrar uma parte do caminho '/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)</span><span class="sxs-lookup"><span data-stu-id="e1aed-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

<span data-ttu-id="e1aed-142">**DCR:**</span><span class="sxs-lookup"><span data-stu-id="e1aed-142">**DCR:**</span></span>

* <span data-ttu-id="e1aed-143">Adicione uma propriedade do MSBuild que indica que PackageDownload tem suporte- [#8106](https://github.com/NuGet/Home/issues/8106)</span><span class="sxs-lookup"><span data-stu-id="e1aed-143">Add an msbuild property that indicates that PackageDownload is supported - [#8106](https://github.com/NuGet/Home/issues/8106)</span></span>

* <span data-ttu-id="e1aed-144">FrameworkReference suprimir o fluxo de dependência por meio de FrameworkReference. PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)</span><span class="sxs-lookup"><span data-stu-id="e1aed-144">FrameworkReference suppress dependency flow via FrameworkReference.PrivateAssets - [#7988](https://github.com/NuGet/Home/issues/7988)</span></span>

* <span data-ttu-id="e1aed-145">Mecanismo para fornecer runtime.jsde fora de um pacote- [#7351](https://github.com/NuGet/Home/issues/7351)</span><span class="sxs-lookup"><span data-stu-id="e1aed-145">Mechanism for supplying runtime.json outside of a package - [#7351](https://github.com/NuGet/Home/issues/7351)</span></span>

<span data-ttu-id="e1aed-146">**[Lista de todos os problemas corrigidos nesta versão-5,2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span><span class="sxs-lookup"><span data-stu-id="e1aed-146">**[List of all issues fixed in this release - 5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span></span>


