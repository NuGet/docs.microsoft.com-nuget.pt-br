---
title: Notas de versão do NuGet 5,1 RTM
description: Notas de versão do NuGet 5,1, incluindo novos recursos, correções de bugs e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: d6f6bffc6b5fda9ee1b9d9830f6d7d3c0f5be654
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780133"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="ce667-103">Notas de versão do NuGet 5,1</span><span class="sxs-lookup"><span data-stu-id="ce667-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="ce667-104">Veículos de distribuição do NuGet:</span><span class="sxs-lookup"><span data-stu-id="ce667-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="ce667-105">Versão do NuGet</span><span class="sxs-lookup"><span data-stu-id="ce667-105">NuGet version</span></span> | <span data-ttu-id="ce667-106">Disponível na versão do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ce667-106">Available in Visual Studio version</span></span>| <span data-ttu-id="ce667-107">Disponível em SDKs do .NET</span><span class="sxs-lookup"><span data-stu-id="ce667-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="ce667-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="ce667-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="ce667-109">Visual Studio 2019 versão 16,1</span><span class="sxs-lookup"><span data-stu-id="ce667-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="ce667-110">[2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="ce667-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="ce667-111"><sup>1</sup> Instalado com o Visual Studio 2019 com carga de trabalho do .NET Core</span><span class="sxs-lookup"><span data-stu-id="ce667-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="ce667-112"><sup>2</sup> Disponível como uma instalação opcional com o Visual Studio 2019 com carga de trabalho do .NET Core</span><span class="sxs-lookup"><span data-stu-id="ce667-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="ce667-113">Resumo: o que há de novo no 5,1</span><span class="sxs-lookup"><span data-stu-id="ce667-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="ce667-114">Suporte para ignorar um push de pacote se ele já existir para permitir uma melhor integração com fluxos de trabalho de CI/CD- [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="ce667-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="ce667-115">Agora, o Visual Studio fornece um link conveniente para a página da Galeria nuget.org do pacote- [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="ce667-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="ce667-116">Suporte para novos ativos 3,0 do .NET Core, como [pacotes de direcionamento](https://github.com/dotnet/cli/issues/10006) e [pacotes de tempo de execução](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="ce667-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="ce667-117">NuGet Pack e Restore support for FrameworkReferences to Enable Targeting and Runtime Package References- [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="ce667-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="ce667-118">Suporte ao cenário de pacote "somente download" com PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="ce667-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="ce667-119">Excluir tempo de execução e pacotes de direcionamento dos resultados da pesquisa & restaurar grafo usando o Pacotetype- [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="ce667-119">Exclude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ce667-120">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="ce667-120">Issues fixed in this release</span></span>

<span data-ttu-id="ce667-121">**Bugs**</span><span class="sxs-lookup"><span data-stu-id="ce667-121">**Bugs**</span></span>

* <span data-ttu-id="ce667-122">Plug-ins: detalhes da exceção perdidos durante a criação do plug-in- [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="ce667-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="ce667-123">O intervalo de PackageReference com limite inferior exclusivo não funcionará se o limite inferior estiver presente em uma das fontes.</span><span class="sxs-lookup"><span data-stu-id="ce667-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="ce667-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="ce667-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="ce667-125">Melhorar a mensagem de IsPackableFalseError- [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="ce667-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="ce667-126">Pacotes de bloqueio de arquivo – gerar novamente o arquivo de bloqueio quando o Project Graph alterar- [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="ce667-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="ce667-127">Bug ProjectSystem: pacotes NuGet sendo removidos automaticamente- [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="ce667-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="ce667-128">Adicionar um destino para retornar o FrameworkReference semelhante a CollectPackageDownloads e CollectPackageReferences- [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="ce667-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="ce667-129">Cache HTTP: o recurso RepositoryResources não está armazenado em cache de maneira com versão [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="ce667-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="ce667-130">Registro em log: as pilhas de chamadas de exceção não são relatadas com detalhes detalhados- [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="ce667-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="ce667-131">Alterar todas as URLs de documentos do NuGet para usar HTTPS- [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="ce667-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="ce667-132">Melhorar a mensagem de aviso do NU3024- [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="ce667-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="ce667-133">bloquear arquivo não atualizando quando packagereference removido- [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="ce667-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="ce667-134">Melhorar o tratamento de casos de erro ao validar licenseurl e o elemento de licença no nuspec- [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="ce667-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="ce667-135">Interface do usuário do PM-clique com o botão direito do mouse no cabeçalho da guia e clique em "abrir local do arquivo" resulta em erro- [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="ce667-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="ce667-136">Plugins: log quando o processo do plug-in é encerrado- [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="ce667-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="ce667-137">Plug-ins: alta taxa de colisão no log de valores de data/hora- [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="ce667-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="ce667-138">Manifest. ReadFrom falha em qualquer nuspec com Licenseid- [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="ce667-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="ce667-139">RestoreLockedMode: NU1004 inesperado quando ProjectReference se refere a um projeto com AssemblyName- [#7889](https://github.com/NuGet/Home/issues/7889) personalizado</span><span class="sxs-lookup"><span data-stu-id="ce667-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="ce667-140">Melhor mensagem de erro quando a inicialização do plug-in falha com uma exceção- [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="ce667-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="ce667-141">Ao fazer uma restauração de NoOp, evite \* .dgspec.jsem gravar no diretório obj- [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="ce667-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="ce667-142">GeneratePathProperty = true falha ao gerar Propriedade em caso de incompatibilidade de caso- [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="ce667-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="ce667-143">Configurações: caractere inválido no caminho de origem do pacote pode falhar VS- [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="ce667-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="ce667-144">Se o arquivo de bloqueio for excluído, Restore não gerará o arquivo de bloqueio em NoOp- [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="ce667-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="ce667-145">A URL de licença e a licença causam erro de leitura com metadados- [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="ce667-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="ce667-146">Exceções sem tratamento em V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="ce667-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="ce667-147">nuget.exe retorna o código de saída zero para argumentos inválidos- [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="ce667-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="ce667-148">Atualizar os erros e documentos de aviso para refletir cenários relacionados à assinatura- [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="ce667-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="ce667-149">O arquivo de ativos deve usar caminhos relativos para habilitar a movimentação de projetos com mais facilidade [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="ce667-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="ce667-150">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="ce667-150">**DCRs**</span></span>

* <span data-ttu-id="ce667-151">Plug-ins: habilitar log de diagnóstico- [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="ce667-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="ce667-152">Fazer o tizen 6 mapear para o netstandard 2,1- [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="ce667-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="ce667-153">**[Lista de todos os problemas corrigidos nesta versão-5,1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="ce667-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
