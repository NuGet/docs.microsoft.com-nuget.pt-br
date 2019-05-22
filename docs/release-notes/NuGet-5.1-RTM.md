---
ms.openlocfilehash: 48306e77a017c11fa7dc0d695e0177edf4e79d1e
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65975830"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="03efb-101">Notas de versão 5.1 do NuGet</span><span class="sxs-lookup"><span data-stu-id="03efb-101">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="03efb-102">Veículos de distribuição do NuGet:</span><span class="sxs-lookup"><span data-stu-id="03efb-102">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="03efb-103">Versão do NuGet</span><span class="sxs-lookup"><span data-stu-id="03efb-103">NuGet version</span></span> | <span data-ttu-id="03efb-104">Disponível na versão do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="03efb-104">Available in Visual Studio version</span></span>| <span data-ttu-id="03efb-105">Disponível em SDKs do .NET</span><span class="sxs-lookup"><span data-stu-id="03efb-105">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="03efb-106">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="03efb-106">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="03efb-107">Visual Studio 2019 versão 16.1</span><span class="sxs-lookup"><span data-stu-id="03efb-107">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="03efb-108">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="03efb-108">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="03efb-109"><sup>1</sup>instaladas com o Visual Studio de 2019 com carga de trabalho do .NET Core</span><span class="sxs-lookup"><span data-stu-id="03efb-109"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="03efb-110"><sup>2</sup>disponível como uma instalação opcional com o Visual Studio de 2019 com carga de trabalho do .NET Core</span><span class="sxs-lookup"><span data-stu-id="03efb-110"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="03efb-111">Resumo: O que há de novo no 5.1</span><span class="sxs-lookup"><span data-stu-id="03efb-111">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="03efb-112">Suporte para ignorar um envio por push do pacote se ele já existe para permitir uma melhor integração com fluxos de trabalho CI/CD - [1630 #](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="03efb-112">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="03efb-113">O Visual Studio agora fornece um link conveniente para a página da Galeria do pacote nuget.org - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="03efb-113">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="03efb-114">Suporte para novos ativos do .NET Core 3.0, como [pacotes de direcionamento](https://github.com/dotnet/cli/issues/10006) e [pacotes de tempo de execução](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="03efb-114">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="03efb-115">Suportam de pacote do NuGet e restauração para FrameworkReferences habilitar as referências de pacote de direcionamento e tempo de execução - [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="03efb-115">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="03efb-116">Cenário de pacote "baixar apenas" suporte com PackageDownload - [7339 #](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="03efb-116">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="03efb-117">Tempo de execução Exlcude e pacotes de resultados da pesquisa e a restauração de direcionamento do graph usando o tipo de pacote - [7337 #](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="03efb-117">Exlcude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="03efb-118">Problemas corrigidos nesta versão</span><span class="sxs-lookup"><span data-stu-id="03efb-118">Issues fixed in this release</span></span>

<span data-ttu-id="03efb-119">**•s**</span><span class="sxs-lookup"><span data-stu-id="03efb-119">**Bugs**</span></span>

* <span data-ttu-id="03efb-120">Plug-ins: detalhes da exceção perdido durante a criação do plug-in - [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="03efb-120">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="03efb-121">Intervalo de PackageReference com o limite inferior exclusivo não funcionará se o limite inferior está presente em uma das fontes.</span><span class="sxs-lookup"><span data-stu-id="03efb-121">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="03efb-122"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="03efb-122"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="03efb-123">Melhorar a mensagem IsPackableFalseError - [8021 #](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="03efb-123">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="03efb-124">Empacota o arquivo de bloqueio – arquivo de bloqueio regenerar ao projeto gráfico muda - [8019 #](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="03efb-124">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="03efb-125">ProjectSystem bug: Obtendo automática de pacotes do NuGet removida - [8017 #](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="03efb-125">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="03efb-126">Adicionar um destino para retornar o FrameworkReference semelhantes a CollectPackageDownloads e CollectPackageReferences - [8005 #](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="03efb-126">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="03efb-127">Cache HTTP:  Recurso RepositoryResources não é armazenado em cache de uma forma de controle de versão - [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="03efb-127">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="03efb-128">Registro em log: pilhas de chamadas de exceção não são relatadas detalhado - [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="03efb-128">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="03efb-129">Alterar todas as URLs de NuGet Docs para usar HTTPS - [7950 #](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="03efb-129">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="03efb-130">Melhorar a mensagem de aviso NU3024 - [7933 #](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="03efb-130">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="03efb-131">arquivo de bloqueio não atualizando quando packagereference removido - [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="03efb-131">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="03efb-132">Melhorar a manipulação de caso de erro ao validar o elemento licenseurl e licença no nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="03efb-132">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="03efb-133">UI PM - clique com botão direito no cabeçalho da guia e clicando em "Abrir local do arquivo" resulta em erro de - [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="03efb-133">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="03efb-134">Plug-ins: registrar em log quando sai do processo de plug-in - [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="03efb-134">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="03efb-135">Plug-ins: taxa de colisão alta em valores de data e hora de registro em log - [7899 #](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="03efb-135">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="03efb-136">Manifest.ReadFrom falhar em qualquer nuspec com LicenseExpression - [7894 #](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="03efb-136">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="03efb-137">RestoreLockedMode: NU1004 inesperado quando ProjectReference refere-se a um projeto com AssemblyName personalizado - [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="03efb-137">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="03efb-138">Mensagem de erro melhor quando a inicialização do plug-in falhar com uma exceção - [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="03efb-138">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="03efb-139">Ao fazer uma restauração NoOp, evite \*. dgspec.json gravação no diretório obj - [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="03efb-139">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="03efb-140">GeneratePathProperty = true Falha ao gerar a propriedade em maiuscula incompatível - [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="03efb-140">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="03efb-141">Configurações: caractere inválido no caminho de origem pode causar falha no VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="03efb-141">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="03efb-142">Se o arquivo de bloqueio é excluído, restauração não gerar arquivo de bloqueio no NoOp - [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="03efb-142">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="03efb-143">URL de licença e as causas de licença ler erro com metadados - [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="03efb-143">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="03efb-144">Exceções sem tratamento no V2FeedParser - [7523 #](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="03efb-144">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="03efb-145">NuGet.exe retorna o código de saída zero argumentos inválidos - [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="03efb-145">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="03efb-146">Atualizar erros e documentos de aviso para refletir os cenários relacionados de assinatura - [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="03efb-146">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="03efb-147">Arquivo de ativos deve usar caminhos relativos para habilitar a movimentação de projetos com mais facilidade - [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="03efb-147">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="03efb-148">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="03efb-148">**DCRs**</span></span>

* <span data-ttu-id="03efb-149">Plug-ins: habilitar o log de diagnóstico - [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="03efb-149">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="03efb-150">Verifique Tizen 6 são mapeados para o NetStandard 2.1 - [7773 #](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="03efb-150">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="03efb-151">**[Lista de todos os problemas corrigidos nesta versão - RTM 5.1](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="03efb-151">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
