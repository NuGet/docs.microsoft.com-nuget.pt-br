---
title: 3.5 notas de versão de RC
description: Notas de versão do NuGet 3.5 RC incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548532"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="6b472-103">Notas de versão do NuGet 3.5 RC</span><span class="sxs-lookup"><span data-stu-id="6b472-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="6b472-104">[Notas de versão do NuGet 3.5-Beta2](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-notas de versão RTM](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="6b472-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="6b472-105">versão 3.5 tem como foco melhorar a qualidade e desempenho de clientes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="6b472-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="6b472-106">Além disso, podemos enviar alguns recursos, como suporte para [pastas de Fallback](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) suporte no `.nuspec` e muito mais.</span><span class="sxs-lookup"><span data-stu-id="6b472-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="6b472-107">Lista de Problemas</span><span class="sxs-lookup"><span data-stu-id="6b472-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="6b472-108">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="6b472-108">Bug Fixes</span></span>

* <span data-ttu-id="6b472-109">Instalação/restauração de um pacote falha com "pacote contém vários `.nuspec` arquivos."</span><span class="sxs-lookup"><span data-stu-id="6b472-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="6b472-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="6b472-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="6b472-111">pacote NuGet adiciona forçada `.tt` arquivos para pasta de conteúdo importa - [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="6b472-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="6b472-112">NuGet pack csproj (com `project.json`) falha se não houver nenhum packOptions e o proprietário do arquivo JSON - [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="6b472-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="6b472-113">pacote do NuGet para `project.json` ignora packOptions marcas como resumo, os autores, proprietários etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="6b472-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="6b472-114">pacote do NuGet ignora as dependências na saída `.nuspec` para `project.json`  -  [3145 #](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="6b472-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="6b472-115">Atualizar vários pacotes com reversão deixa o projeto em um estado interrompido - [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="6b472-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="6b472-116">ContentFiles em qualquer não são adicionados para projetos de identificadores de netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="6b472-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="6b472-117">Não é possível empacotar a biblioteca destinados ao .net Standard corretamente - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="6b472-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="6b472-118">Arquivo -> Novo projeto -> Falha de projeto de biblioteca de classes (portátil) em VS2015 e Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="6b472-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="6b472-119">Erro do NuGet - 1.0.0-\* não é uma cadeia de caracteres de versão válida - [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="6b472-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="6b472-120">Find-Package falha para exibição, mas funciona de Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="6b472-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="6b472-121">Erro ao "Install-Package jquery.validation" em dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="6b472-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="6b472-122">Quando instalado VS 2015 atualização 3 em uma que usa o NuGet, ocorre o erro de versão 3.5.0 - VS [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="6b472-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="6b472-123">Interface do usuário do Gerenciador de pacotes: não exibe a nova versão depois de atualizar um pacote- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="6b472-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="6b472-124">-ApiKey na linha de comando de exclusão não é leitura/enviada em 3.5.0-Beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="6b472-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="6b472-125">Cadeia de caracteres incorreta: uma versão estável de um pacote não deve ter em uma dependência de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="6b472-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="6b472-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="6b472-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="6b472-127">Criando get de projeto PCL (net46 e windows 10) exceção NullRef.</span><span class="sxs-lookup"><span data-stu-id="6b472-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="6b472-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="6b472-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="6b472-129">Atualização do NuGet deve fornecer a mensagem informativa quando uma versão mais recente é restrito pela restrição allowedVersions - [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="6b472-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="6b472-130">Plug-in de credencial foi encerrado com erro -1 / Erro ao baixar pacote ao usar provedores de credenciais com várias fontes - [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="6b472-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="6b472-131">pacote do NuGet - dependência de pacote ausente newtonsoft. JSON - [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="6b472-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="6b472-132">Erro no ExecuteSynchronizedCore no Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="6b472-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="6b472-133">VS não dá suporte a variáveis de ambiente no caminho do repositório (nuget.exe faz) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="6b472-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="6b472-134">Corrigir problemas de acessibilidade - [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="6b472-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="6b472-135">Estruturas portátil com perfis hifenizadas são rejeitadas.</span><span class="sxs-lookup"><span data-stu-id="6b472-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="6b472-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="6b472-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="6b472-137">O Gerenciador de pacotes do NuGet deve esclarecer essa lista de opções em pacotes detalhes não se aplicam a `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="6b472-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="6b472-138">NuGet 3.3.0 atualização falha com '... uma restrição adicional definido em Packages. config impede que esta operação.'</span><span class="sxs-lookup"><span data-stu-id="6b472-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="6b472-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="6b472-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="6b472-140">Ao instalar o pacote de um local de origem que não existe gera uma mensagem de falso - [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="6b472-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="6b472-141">Filtro de "Atualização veis" mostra as atualizações que violam a restrição de versão - [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="6b472-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="6b472-142">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="6b472-142">Performance Improvements</span></span>

* <span data-ttu-id="6b472-143">Desempenho: Melhorar o análise de framework de destino de ContentModel - [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="6b472-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="6b472-144">Desempenho: Evitar leitura `runtime.json` arquivos para restaurações que não têm RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="6b472-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="6b472-145">Em máquinas de CI, restaure de uma amostra de que aplicativo Web ASP.NET reduzido mais de 15 segundos para 3 segundos.</span><span class="sxs-lookup"><span data-stu-id="6b472-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="6b472-146">Desempenho: Tempo de carregamento Package Manager Console init.ps1 [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="6b472-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="6b472-147">Tempo para abrir PackageManagerConsole aprimorada em alguns casos de 132s para 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="6b472-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="6b472-148">Solucionar problemas de desempenho do ReSharper na atualização do NuGet - [#3044](https://github.com/NuGet/Home/issues/3044): em um projeto de exemplo, o tempo necessário para instalar pacotes reduzido de 140s para 68s.</span><span class="sxs-lookup"><span data-stu-id="6b472-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="6b472-149">DCRs</span><span class="sxs-lookup"><span data-stu-id="6b472-149">DCRs</span></span>

* <span data-ttu-id="6b472-150">O NuGet precisa que os usuários saibam que atualizar/instalar em um tfm dotnet com base em PCL poderá causar problemas - [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="6b472-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="6b472-151">Avisar ruim instalar/atualizar para o projeto c / tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="6b472-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="6b472-152">Adicionar suporte netcoreapp11 e netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="6b472-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="6b472-153">Imprimir o conteúdo do cabeçalho de aviso do NuGet para o console no nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="6b472-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="6b472-154">Atributo AssemblyMetadata aproveite `.nuspec` token substituições - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="6b472-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="6b472-155">Remova a propriedade locked do arquivo lock - [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="6b472-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="6b472-156">Pacotes de símbolo já não devem ser usados em instalar ou atualizar #2807</span><span class="sxs-lookup"><span data-stu-id="6b472-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="6b472-157">Recursos</span><span class="sxs-lookup"><span data-stu-id="6b472-157">Features</span></span>

* <span data-ttu-id="6b472-158">Suporte para pastas de pacote fallback - [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="6b472-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="6b472-159">Projetar e implementar uma noção de tipo de pacote para dar suporte a pacotes de ferramenta - [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="6b472-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="6b472-160">API para obter o caminho para a pasta de pacotes globais - [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="6b472-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="6b472-161">Suporte - atualização de pacotes nativos [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="6b472-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
