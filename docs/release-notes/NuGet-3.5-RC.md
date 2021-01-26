---
title: Notas de versão do 3,5 RC
description: Notas de versão do NuGet 3,5 RC incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780203"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="5b25a-103">Notas de versão do NuGet 3,5 RC</span><span class="sxs-lookup"><span data-stu-id="5b25a-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="5b25a-104">Notas de versão do [NuGet 3,5-beta2](../release-notes/nuget-3.5-Beta2.md)  |  [NuGet 3,5-notas de versão RTM](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="5b25a-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="5b25a-105">a versão 3,5 concentra-se em melhorar a qualidade e o desempenho de clientes NuGet.</span><span class="sxs-lookup"><span data-stu-id="5b25a-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="5b25a-106">Além disso, enviamos alguns recursos como suporte para pastas de [fallback](https://github.com/NuGet/Home/issues/2899), suporte a [PackageType](https://github.com/NuGet/Home/issues/2476) no `.nuspec` e mais.</span><span class="sxs-lookup"><span data-stu-id="5b25a-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="5b25a-107">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="5b25a-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="5b25a-108">Correções de bugs</span><span class="sxs-lookup"><span data-stu-id="5b25a-108">Bug Fixes</span></span>

* <span data-ttu-id="5b25a-109">Falha na instalação/restauração de um pacote com "o pacote contém vários `.nuspec` arquivos".</span><span class="sxs-lookup"><span data-stu-id="5b25a-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="5b25a-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="5b25a-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="5b25a-111">o pacote NuGet adiciona `.tt` arquivos à pasta de conteúdo de modo forçado, independentemente do que [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="5b25a-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="5b25a-112">o NuGet Pack csproj (with `project.json` ) falhará se não houver packoptions e proprietário no arquivo JSON- [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="5b25a-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="5b25a-113">o pacote NuGet para `project.json` ignora marcas packoptions, como resumo, autores, proprietários etc- [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="5b25a-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="5b25a-114">o pacote NuGet ignora dependências na saída `.nuspec` para `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="5b25a-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="5b25a-115">A atualização de vários pacotes com a reversão deixa o projeto em um estado desfeito- [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="5b25a-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="5b25a-116">ContentFiles em qualquer um não é adicionado para projetos netstandard- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="5b25a-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="5b25a-117">Não é possível empacotar a biblioteca com o padrão .net Standard corretamente- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="5b25a-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="5b25a-118">Arquivo-> novo projeto-> biblioteca de classes (portátil) falha em VS2015 e Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="5b25a-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="5b25a-119">Erro do NuGet-1.0.0-\* não é uma cadeia de caracteres de versão válida- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="5b25a-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="5b25a-120">Find-Package falha ao exibir, mas Install-Package Works- [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="5b25a-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="5b25a-121">Erro quando "Install-Package jQuery. Validation" em dev15- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="5b25a-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="5b25a-122">Quando instalada VS 2015 atualização 3 em um VS que usa o erro do NuGet versão 3.5.0 ocorre- [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="5b25a-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="5b25a-123">Interface do usuário do Gerenciador de pacotes: não exibe a nova versão após atualizar um pacote- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="5b25a-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="5b25a-124">-ApiKey na linha de comando de exclusão não é lido/enviado em 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="5b25a-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="5b25a-125">Cadeia de caracteres incorreta: uma versão estável de um pacote não deve ter em uma dependência de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="5b25a-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="5b25a-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="5b25a-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="5b25a-127">Criando exceção NullRef de Get do projeto PCL (net46 e Windows 10).</span><span class="sxs-lookup"><span data-stu-id="5b25a-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="5b25a-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="5b25a-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="5b25a-129">A atualização do NuGet deve fornecer uma mensagem informativa quando uma versão superior é restrita pela restrição allowedVersions- [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="5b25a-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="5b25a-130">O plug-in de credencial saiu com o erro-1/erro ao baixar o pacote ao usar provedores de credenciais com várias fontes- [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="5b25a-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="5b25a-131">pacote NuGet-faltando Newtonsoft.Jsna dependência de pacote- [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="5b25a-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="5b25a-132">Bug em ExecuteSynchronizedCore no linux/MacOS + mono- [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="5b25a-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="5b25a-133">O VS não oferece suporte a variáveis de ambiente no repositoryPath (nuget.exe) – [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="5b25a-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="5b25a-134">Corrigir problemas de acessibilidade- [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="5b25a-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="5b25a-135">Estruturas portáteis com perfis hifenizados são rejeitadas.</span><span class="sxs-lookup"><span data-stu-id="5b25a-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="5b25a-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="5b25a-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="5b25a-137">O Gerenciador de pacotes NuGet deve tornar claro que a lista de opções no detalhes dos pacotes não se aplica a `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="5b25a-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="5b25a-138">Falha na atualização do NuGet 3.3.0 com ' uma restrição adicional... definido em packages.config impede esta operação. '</span><span class="sxs-lookup"><span data-stu-id="5b25a-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="5b25a-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="5b25a-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="5b25a-140">A instalação do pacote de uma fonte local que não existe gera um [#1674](https://github.com/NuGet/Home/issues/1674) de mensagens falso</span><span class="sxs-lookup"><span data-stu-id="5b25a-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="5b25a-141">O filtro "atualizar disponíveis" mostra atualizações que violam a restrição de versão- [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="5b25a-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="5b25a-142">Melhorias no desempenho</span><span class="sxs-lookup"><span data-stu-id="5b25a-142">Performance Improvements</span></span>

* <span data-ttu-id="5b25a-143">Desempenho: melhorar a análise da estrutura de destino ContentModel- [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="5b25a-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="5b25a-144">Desempenho: Evite `runtime.json` a leitura de arquivos para restaurações que não têm RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span><span class="sxs-lookup"><span data-stu-id="5b25a-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="5b25a-145">Em máquinas de CI, a restauração de um aplicativo Web ASP.NET de exemplo foi reduzida de mais de 15 segundos para 3 segundos.</span><span class="sxs-lookup"><span data-stu-id="5b25a-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="5b25a-146">Desempenho: o console do Gerenciador de pacotes init.ps1 tempo de carregamento [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="5b25a-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="5b25a-147">Tempo para abrir o PackageManagerConsole melhorou em alguns casos de 132s para 10s.</span><span class="sxs-lookup"><span data-stu-id="5b25a-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="5b25a-148">Solucionar problemas de desempenho de resnitidez no NuGet update- [#3044](https://github.com/NuGet/Home/issues/3044): em um projeto de exemplo, tempo necessário para instalar pacotes reduzidos de 140s para 68S.</span><span class="sxs-lookup"><span data-stu-id="5b25a-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="5b25a-149">DCRs</span><span class="sxs-lookup"><span data-stu-id="5b25a-149">DCRs</span></span>

* <span data-ttu-id="5b25a-150">O NuGet precisa permitir que os usuários saibam que a atualização/instalação em uma PCL baseada em TFM de dotnet pode causar problemas- [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="5b25a-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="5b25a-151">Avisar instalação/atualização inadequada para o projeto c/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="5b25a-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="5b25a-152">Adicionar suporte a netcoreapp11 e netstandard17- [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="5b25a-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="5b25a-153">Imprimir NuGet-Warning conteúdo do cabeçalho no console do em nuget.exe- [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="5b25a-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="5b25a-154">Aproveitar o atributo AssemblyMetadata para `.nuspec` substituições de token- [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="5b25a-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="5b25a-155">Remover a propriedade locked do arquivo de bloqueio- [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="5b25a-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="5b25a-156">Os pacotes de símbolo não devem nunca ser usados na instalação ou atualização #2807</span><span class="sxs-lookup"><span data-stu-id="5b25a-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="5b25a-157">Recursos</span><span class="sxs-lookup"><span data-stu-id="5b25a-157">Features</span></span>

* <span data-ttu-id="5b25a-158">Suporte para pastas de pacotes de fallback- [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="5b25a-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="5b25a-159">Projete e implemente uma noção de tipo de pacote para oferecer suporte a pacotes de ferramentas- [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="5b25a-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="5b25a-160">API para obter o caminho para a pasta de pacotes globais- [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="5b25a-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="5b25a-161">Suporte à atualização de pacotes nativos- [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="5b25a-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
