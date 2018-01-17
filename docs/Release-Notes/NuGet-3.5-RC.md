---
title: "3.5 notas de versão RC | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 75a9b496-5762-48b6-922f-fdddf1369c45
description: "Notas de versão do NuGet 3.5 RC incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão RC do NuGet 3.5, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 09d566de6f53bc0f0ddd8049143dc647f3075671
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
#<a name="35-rc-release-notes"></a><span data-ttu-id="db10f-104">3.5 notas de versão RC</span><span class="sxs-lookup"><span data-stu-id="db10f-104">3.5 RC Release Notes</span></span>

<span data-ttu-id="db10f-105">[Notas de versão 3.5-Beta2 NuGet](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM notas de versão](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="db10f-105">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="db10f-106">versão 3.5 está se concentrou em melhorar a qualidade e o desempenho de clientes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="db10f-106">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="db10f-107">Além disso, podemos ter enviado alguns recursos, como suporte para [pastas Fallback](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) suporte em `.nuspec` e muito mais.</span><span class="sxs-lookup"><span data-stu-id="db10f-107">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="db10f-108">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="db10f-108">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5 RC")

## <a name="bug-fixes"></a><span data-ttu-id="db10f-109">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="db10f-109">Bug Fixes</span></span>

* <span data-ttu-id="db10f-110">Falha na instalação/restauração de um pacote com "pacote contém várias `.nuspec` arquivos."</span><span class="sxs-lookup"><span data-stu-id="db10f-110">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="db10f-111"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="db10f-111"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="db10f-112">pacote do NuGet forçada adiciona `.tt` arquivos para pasta de conteúdo, não importando qual - [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="db10f-112">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="db10f-113">csproj de pacote do NuGet (com `project.json`) falha se não houver nenhum packOptions e proprietário no arquivo JSON - [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="db10f-113">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="db10f-114">pacote do NuGet para `project.json` ignora packOptions marcas como resumo, autores e proprietários etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="db10f-114">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="db10f-115">pacote do NuGet ignora dependências na saída `.nuspec` para `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="db10f-115">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="db10f-116">Atualizar vários pacotes com a reversão deixa o projeto em um estado interrompido - [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="db10f-116">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="db10f-117">ContentFiles em qualquer não são adicionados para projetos de identificadores de netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="db10f-117">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="db10f-118">Não é possível empacotar biblioteca direcionado ao .net padrão corretamente - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="db10f-118">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="db10f-119">Arquivo -> Novo projeto -> Falha de projeto de biblioteca de classes (portátil) em VS2015 e Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="db10f-119">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="db10f-120">Erro do NuGet - 1.0.0-\* não é uma cadeia de caracteres de versão válida - [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="db10f-120">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="db10f-121">Find-Package falha para exibição, mas funciona Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="db10f-121">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="db10f-122">Erro ao "Install-Package jquery.validation" em dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="db10f-122">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="db10f-123">Quando instalado VS 2015 atualização 3 em uma relação que usa NuGet versão 3.5.0 erro - [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="db10f-123">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="db10f-124">Interface de usuário do Gerenciador de pacote: não exibir a nova versão depois de atualizar um pacote- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="db10f-124">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="db10f-125">-ApiKey na linha de comando de exclusão não é leitura/enviada em 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="db10f-125">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="db10f-126">Cadeia de caracteres incorreta: uma versão estável de um pacote não deve ter em uma dependência de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="db10f-126">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="db10f-127"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="db10f-127"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="db10f-128">Criando get de projeto PCL (net46 e windows 10) NullRef exceção.</span><span class="sxs-lookup"><span data-stu-id="db10f-128">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="db10f-129"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="db10f-129"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="db10f-130">Atualização do NuGet deve fornecer a mensagem informativa quando uma versão mais recente é restrito por restrição Allowedverdions - [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="db10f-130">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="db10f-131">Plug-in de credencial foi encerrado com erro -1 / erro baixar pacote ao usar os provedores de credenciais com várias fontes - [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="db10f-131">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="db10f-132">pacote do NuGet - newtonsoft. JSON ausente de dependência de pacote - [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="db10f-132">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="db10f-133">Erro no ExecuteSynchronizedCore no Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="db10f-133">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="db10f-134">VS não oferece suporte a variáveis de ambiente no caminho do repositório (nuget.exe faz) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="db10f-134">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="db10f-135">Corrigir problemas de acessibilidade - [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="db10f-135">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="db10f-136">Estruturas portátil com perfis hifenizadas são rejeitadas.</span><span class="sxs-lookup"><span data-stu-id="db10f-136">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="db10f-137"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="db10f-137"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="db10f-138">O Gerenciador de pacotes do NuGet deve esclarecer essa lista de opções em pacotes detalhes não se aplicam a `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="db10f-138">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="db10f-139">Falha de atualização do NuGet 3.3.0 '... uma restrição adicional definida no Packages impede esta operação.'</span><span class="sxs-lookup"><span data-stu-id="db10f-139">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="db10f-140"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="db10f-140"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="db10f-141">Instalando o pacote de um local de origem que não existe gera uma mensagem falso - [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="db10f-141">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="db10f-142">Filtro de "Atualização disponíveis" mostra as atualizações que violam a restrição de versão - [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="db10f-142">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="db10f-143">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="db10f-143">Performance Improvements</span></span>

* <span data-ttu-id="db10f-144">Desempenho: Melhorar o análise de framework de destino de ContentModel - [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="db10f-144">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="db10f-145">Desempenho: Evitar leitura `runtime.json` arquivos para restaurações que não têm RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="db10f-145">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="db10f-146">Em máquinas de CI, restaure de uma amostra de que aplicativo Web ASP.NET reduzido mais de 15 segundos para 3 segundos.</span><span class="sxs-lookup"><span data-stu-id="db10f-146">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="db10f-147">Desempenho: Tempo de carregamento Package Manager Console init.ps1 [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="db10f-147">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="db10f-148">Tempo para abrir PackageManagerConsole aprimorada em alguns casos de 132s por 10.</span><span class="sxs-lookup"><span data-stu-id="db10f-148">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="db10f-149">Solucionar problemas de desempenho ReSharper na atualização do NuGet - [#3044](https://github.com/NuGet/Home/issues/3044): em um projeto de exemplo, o tempo necessário para instalar pacotes reduzido de 140s para 68s.</span><span class="sxs-lookup"><span data-stu-id="db10f-149">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="db10f-150">DCRs</span><span class="sxs-lookup"><span data-stu-id="db10f-150">DCRs</span></span>

* <span data-ttu-id="db10f-151">NuGet precisa que os usuários saibam que atualizar/instalar em um tfm dotnet com base em PCL pode causar problemas - [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="db10f-151">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="db10f-152">Avisar incorreta instalar ou atualizar para o projeto com tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="db10f-152">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="db10f-153">Adicionar suporte netcoreapp11 e netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="db10f-153">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="db10f-154">Imprimir o conteúdo do cabeçalho de aviso do NuGet para o console no nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="db10f-154">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="db10f-155">Atributo AssemblyMetadata aproveite `.nuspec` token substituições - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="db10f-155">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="db10f-156">Remova a propriedade locked do arquivo lock - [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="db10f-156">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="db10f-157">Pacotes de símbolo já não devem ser usados em instalar ou atualizar #2807</span><span class="sxs-lookup"><span data-stu-id="db10f-157">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="db10f-158">Recursos</span><span class="sxs-lookup"><span data-stu-id="db10f-158">Features</span></span>

* <span data-ttu-id="db10f-159">Suporte para pastas de pacote de fallback - [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="db10f-159">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="db10f-160">Projetar e implementar uma noção do tipo de pacote para dar suporte a pacotes de ferramenta - [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="db10f-160">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="db10f-161">API para obter o caminho para a pasta de pacotes global - [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="db10f-161">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="db10f-162">Suporte - atualização de pacotes nativos [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="db10f-162">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
