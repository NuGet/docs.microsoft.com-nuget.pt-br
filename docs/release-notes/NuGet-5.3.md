---
title: Notas de versão do NuGet 5,3
description: Notas de versão do NuGet 5,3, incluindo novos recursos, correções de bugs e DCRs.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 96d176beaa6b2f0c4f53488390e585b70c9ba846
ms.sourcegitcommit: 188ade66b7ac807ba1667c77cfb9325bf89a8a4a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71248165"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="79a31-103">Notas de versão do NuGet 5,3</span><span class="sxs-lookup"><span data-stu-id="79a31-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="79a31-104">Veículos de distribuição do NuGet:</span><span class="sxs-lookup"><span data-stu-id="79a31-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="79a31-105">Versão do NuGet</span><span class="sxs-lookup"><span data-stu-id="79a31-105">NuGet version</span></span> | <span data-ttu-id="79a31-106">Disponível na versão do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="79a31-106">Available in Visual Studio version</span></span>| <span data-ttu-id="79a31-107">Disponível em SDKs do .NET</span><span class="sxs-lookup"><span data-stu-id="79a31-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="79a31-108">**5.3.0**</span><span class="sxs-lookup"><span data-stu-id="79a31-108">**5.3.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="79a31-109">Visual Studio 2019 versão 16,3</span><span class="sxs-lookup"><span data-stu-id="79a31-109">Visual Studio 2019 version 16.3</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="79a31-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0) <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="79a31-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |

<span data-ttu-id="79a31-111"><sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core</span><span class="sxs-lookup"><span data-stu-id="79a31-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53"></a><span data-ttu-id="79a31-112">Resumo: O que há de novo no 5,3</span><span class="sxs-lookup"><span data-stu-id="79a31-112">Summary: What's New in 5.3</span></span>

* <span data-ttu-id="79a31-113">[O ícone de pacote pode ser inserido no pacote](../reference/msbuild-targets.md#packing-an-icon-image-file), em vez de precisar de uma URL externa.</span><span class="sxs-lookup"><span data-stu-id="79a31-113">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="79a31-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="79a31-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="79a31-115">Segurança aprimorada com rastreamento e imposição de SHA para Packages. config- [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="79a31-115">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="79a31-116">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="79a31-116">Issues fixed in this release</span></span>

<span data-ttu-id="79a31-117">**•s**</span><span class="sxs-lookup"><span data-stu-id="79a31-117">**Bugs**</span></span>

* <span data-ttu-id="79a31-118">Os pacotes NuGet produzidos com o SDK 3.0.100-preview9 não podem ser usados por usuários do SDK 2,2... dependendo do seu fuso horário [#8603](https://github.com/NuGet/Home/issues/8603)</span><span class="sxs-lookup"><span data-stu-id="79a31-118">NuGet packages produced with 3.0.100-preview9 SDK cannot be used by 2.2 SDK users...depending on your timezone [#8603](https://github.com/NuGet/Home/issues/8603)</span></span>

* <span data-ttu-id="79a31-119">Aspas "os caracteres no caminho causam uma falha de" caracteres ilegais no `nuget restore` caminho "em [#8168](https://github.com/NuGet/Home/issues/8168)</span><span class="sxs-lookup"><span data-stu-id="79a31-119">Quote " characters in PATH cause "Illegal characters in path" failure in `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span></span>

* <span data-ttu-id="79a31-120">VS: os assemblies são totalmente baseados em NGen-Ed não parcialmente-Ed- [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="79a31-120">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="79a31-121">Reduzir o uso de memória (cancelar assinatura de eventos)- [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="79a31-121">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="79a31-122">A mensagem "Error_UnableToFindProjectInfo" não está gramaticalmente correta- [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="79a31-122">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="79a31-123">Aprimoramentos do NU1403 – validar todos os pacotes, incluir os valores de Sha esperados/reais- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="79a31-123">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="79a31-124">Várias enumerações `NuGetPackageManager.PreviewUpdatePackagesAsync`em  -  [#8401](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="79a31-124">Multiple enumeration in `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="79a31-125">Reverter alteração "pública > interna" em PluginProcess- [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="79a31-125">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="79a31-126">IVsPackageSourceProvider. getsources (...) tem comportamento de exceção mal definido- [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="79a31-126">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="79a31-127">Tornar o Construtor PlugInManager público novamente- [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="79a31-127">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="79a31-128">Métricas para acompanhar a taxa de atualização da interface do usuário do PM- [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="79a31-128">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="79a31-129">Diminuir o número de atualizações da interface do usuário ao instalar por meio da interface do usuário do Gerenciador de pacotes- [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="79a31-129">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="79a31-130">Telemetria: os valores de DateTime usam formatos específicos de cultura- [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="79a31-130">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="79a31-131">Reduzir as atualizações da interface do usuário na guia procurar da interface do usuário do Gerenciador de pacotes #6570- [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="79a31-131">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="79a31-132">[Falha de teste] "Não é possível analisar o arquivo de configuração" solicitará duas vezes [#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="79a31-132">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="79a31-133">Gerar erro NU5037 com boa página de documento que explica as correções do cliente (o arquivo nuspec necessário está faltando no pacote)- [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="79a31-133">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="79a31-134">A restauração de modo bloqueado falha quando o RuntimeIdentifier de um projeto é alterado- [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="79a31-134">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="79a31-135">Fazer com que as configurações sejam lidas em VS Lazy- [#8156](https://github.com/NuGet/Home/issues/8156)</span><span class="sxs-lookup"><span data-stu-id="79a31-135">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="79a31-136">A regressão `Nuget sources add` em causa "o caractere": ", valor hexadecimal 0x3A, não pode ser incluído em um nome" erros- [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="79a31-136">Regression in `Nuget sources add` causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="79a31-137">Provedores de credenciais do plug-in NuGet-ocultar a janela processo- [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="79a31-137">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="79a31-138">Impor PackagePathResolver é um caminho absoluto- [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="79a31-138">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="79a31-139">Reduzir as atualizações da interface do usuário nas guias instalar e atualizar da interface do usuário do Gerenciador de pacotes- [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="79a31-139">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="79a31-140">**DCR:**</span><span class="sxs-lookup"><span data-stu-id="79a31-140">**DCR:**</span></span>

* <span data-ttu-id="79a31-141">Atualizar as estruturas do Xamarin para mapear para o netstandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="79a31-141">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="79a31-142">Habilitar a cópia do conteúdo da "janela de visualização" do Gerenciador de pacotes para instalar/atualizar- [#8324](https://github.com/NuGet/Home/issues/8324)</span><span class="sxs-lookup"><span data-stu-id="79a31-142">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="79a31-143">Habilitar a restauração em arquivos. proj- [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="79a31-143">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="79a31-144">Introduza `NUGET_NETFX_PLUGIN_PATHS` e`NUGET_NETCORE_PLUGIN_PATHS` para dar suporte à configuração de ambos ao mesmo tempo- [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="79a31-144">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="79a31-145">Habilitar várias versões para um PackageDownload por meio do atributo de versão- [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="79a31-145">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="79a31-146">Adicionar opções-SolutionDirectory e-PackageDirectory ao NuGet. exe Pack- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="79a31-146">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

<span data-ttu-id="79a31-147">**[Lista de todos os problemas corrigidos nesta versão-5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="79a31-147">**[List of all issues fixed in this release - 5.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>
