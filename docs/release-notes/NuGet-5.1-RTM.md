---
title: Notas de versão do NuGet RTM 5.1
description: Notas de versão do 5.1 de NuGet, incluindo novos recursos, correções de bugs e DCRs.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 384145947b19af6577dc1255985df1a361c72bb5
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842575"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="6a707-103">Notas de versão 5.1 do NuGet</span><span class="sxs-lookup"><span data-stu-id="6a707-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="6a707-104">Veículos de distribuição do NuGet:</span><span class="sxs-lookup"><span data-stu-id="6a707-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="6a707-105">Versão do NuGet</span><span class="sxs-lookup"><span data-stu-id="6a707-105">NuGet version</span></span> | <span data-ttu-id="6a707-106">Disponível na versão do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6a707-106">Available in Visual Studio version</span></span>| <span data-ttu-id="6a707-107">Disponível em SDKs do .NET</span><span class="sxs-lookup"><span data-stu-id="6a707-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="6a707-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="6a707-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="6a707-109">Visual Studio 2019 versão 16.1</span><span class="sxs-lookup"><span data-stu-id="6a707-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="6a707-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="6a707-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="6a707-111"><sup>1</sup>instaladas com o Visual Studio de 2019 com carga de trabalho do .NET Core</span><span class="sxs-lookup"><span data-stu-id="6a707-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="6a707-112"><sup>2</sup>disponível como uma instalação opcional com o Visual Studio de 2019 com carga de trabalho do .NET Core</span><span class="sxs-lookup"><span data-stu-id="6a707-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="6a707-113">Resumo: O que há de novo no 5.1</span><span class="sxs-lookup"><span data-stu-id="6a707-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="6a707-114">Suporte para ignorar um envio por push do pacote se ele já existe para permitir uma melhor integração com fluxos de trabalho CI/CD - [1630 #](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="6a707-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="6a707-115">O Visual Studio agora fornece um link conveniente para a página da Galeria do pacote nuget.org - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="6a707-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="6a707-116">Suporte para novos ativos do .NET Core 3.0, como [pacotes de direcionamento](https://github.com/dotnet/cli/issues/10006) e [pacotes de tempo de execução](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="6a707-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="6a707-117">Suportam de pacote do NuGet e restauração para FrameworkReferences habilitar as referências de pacote de direcionamento e tempo de execução - [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="6a707-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="6a707-118">Cenário de pacote "baixar apenas" suporte com PackageDownload - [7339 #](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="6a707-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="6a707-119">Tempo de execução Exlcude e pacotes de resultados da pesquisa e a restauração de direcionamento do graph usando o tipo de pacote - [7337 #](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="6a707-119">Exlcude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="6a707-120">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="6a707-120">Issues fixed in this release</span></span>

<span data-ttu-id="6a707-121">**•s**</span><span class="sxs-lookup"><span data-stu-id="6a707-121">**Bugs**</span></span>

* <span data-ttu-id="6a707-122">Plug-ins: detalhes da exceção perdido durante a criação do plug-in - [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="6a707-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="6a707-123">Intervalo de PackageReference com o limite inferior exclusivo não funcionará se o limite inferior está presente em uma das fontes.</span><span class="sxs-lookup"><span data-stu-id="6a707-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="6a707-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="6a707-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="6a707-125">Melhorar a mensagem IsPackableFalseError - [8021 #](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="6a707-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="6a707-126">Empacota o arquivo de bloqueio – arquivo de bloqueio regenerar ao projeto gráfico muda - [8019 #](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="6a707-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="6a707-127">ProjectSystem bug: Obtendo automática de pacotes do NuGet removida - [8017 #](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="6a707-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="6a707-128">Adicionar um destino para retornar o FrameworkReference semelhantes a CollectPackageDownloads e CollectPackageReferences - [8005 #](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="6a707-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="6a707-129">Cache HTTP:  Recurso RepositoryResources não é armazenado em cache de uma forma de controle de versão - [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="6a707-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="6a707-130">Registro em log: pilhas de chamadas de exceção não são relatadas detalhado - [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="6a707-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="6a707-131">Alterar todas as URLs de NuGet Docs para usar HTTPS - [7950 #](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="6a707-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="6a707-132">Melhorar a mensagem de aviso NU3024 - [7933 #](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="6a707-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="6a707-133">arquivo de bloqueio não atualizando quando packagereference removido - [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="6a707-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="6a707-134">Melhorar a manipulação de caso de erro ao validar o elemento licenseurl e licença no nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="6a707-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="6a707-135">UI PM - clique com botão direito no cabeçalho da guia e clicando em "Abrir local do arquivo" resulta em erro de - [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="6a707-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="6a707-136">Plug-ins: registrar em log quando sai do processo de plug-in - [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="6a707-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="6a707-137">Plug-ins: taxa de colisão alta em valores de data e hora de registro em log - [7899 #](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="6a707-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="6a707-138">Manifest.ReadFrom falhar em qualquer nuspec com LicenseExpression - [7894 #](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="6a707-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="6a707-139">RestoreLockedMode: NU1004 inesperado quando ProjectReference refere-se a um projeto com AssemblyName personalizado - [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="6a707-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="6a707-140">Mensagem de erro melhor quando a inicialização do plug-in falhar com uma exceção - [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="6a707-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="6a707-141">Ao fazer uma restauração NoOp, evite \*. dgspec.json gravação no diretório obj - [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="6a707-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="6a707-142">GeneratePathProperty = true Falha ao gerar a propriedade em maiuscula incompatível - [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="6a707-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="6a707-143">Configurações: caractere inválido no caminho de origem pode causar falha no VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="6a707-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="6a707-144">Se o arquivo de bloqueio é excluído, restauração não gerar arquivo de bloqueio no NoOp - [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="6a707-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="6a707-145">URL de licença e as causas de licença ler erro com metadados - [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="6a707-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="6a707-146">Exceções sem tratamento no V2FeedParser - [7523 #](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="6a707-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="6a707-147">NuGet.exe retorna o código de saída zero argumentos inválidos - [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="6a707-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="6a707-148">Atualizar erros e documentos de aviso para refletir os cenários relacionados de assinatura - [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="6a707-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="6a707-149">Arquivo de ativos deve usar caminhos relativos para habilitar a movimentação de projetos com mais facilidade - [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="6a707-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="6a707-150">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="6a707-150">**DCRs**</span></span>

* <span data-ttu-id="6a707-151">Plug-ins: habilitar o log de diagnóstico - [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="6a707-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="6a707-152">Verifique Tizen 6 são mapeados para o NetStandard 2.1 - [7773 #](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="6a707-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="6a707-153">**[Lista de todos os problemas corrigidos nesta versão - RTM 5.1](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="6a707-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
