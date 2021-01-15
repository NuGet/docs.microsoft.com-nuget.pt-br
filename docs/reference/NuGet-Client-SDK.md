---
title: SDK do cliente NuGet
description: A API está em evolução e ainda não está documentada, mas exemplos estão disponíveis no blog de Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 0eca8478b4d6509dbc1407560d2c86069c7575dd
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235731"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="5497d-103">SDK do cliente NuGet</span><span class="sxs-lookup"><span data-stu-id="5497d-103">NuGet Client SDK</span></span>

<span data-ttu-id="5497d-104">O *SDK do cliente NuGet* refere-se a um grupo de pacotes NuGet:</span><span class="sxs-lookup"><span data-stu-id="5497d-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="5497d-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -Usado para interagir com HTTP e feeds do NuGet baseados em arquivo</span><span class="sxs-lookup"><span data-stu-id="5497d-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="5497d-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -Usado para interagir com pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="5497d-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="5497d-107">`NuGet.Protocol` depende deste pacote</span><span class="sxs-lookup"><span data-stu-id="5497d-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="5497d-108">Você pode encontrar o código-fonte para esses pacotes no repositório do GitHub [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) .</span><span class="sxs-lookup"><span data-stu-id="5497d-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>
<span data-ttu-id="5497d-109">Você pode encontrar o código-fonte para esses exemplos no projeto [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) no github.</span><span class="sxs-lookup"><span data-stu-id="5497d-109">You can find the source code for these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

> [!Note]
> <span data-ttu-id="5497d-110">Para obter a documentação sobre o protocolo de servidor NuGet, consulte a [API do servidor NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="5497d-110">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="nugetprotocol"></a><span data-ttu-id="5497d-111">NuGet. Protocol</span><span class="sxs-lookup"><span data-stu-id="5497d-111">NuGet.Protocol</span></span>

<span data-ttu-id="5497d-112">Instale o `NuGet.Protocol` pacote para interagir com os feeds de pacote NuGet baseados em pasta e http:</span><span class="sxs-lookup"><span data-stu-id="5497d-112">Install the `NuGet.Protocol` package to interact with HTTP and folder-based NuGet package feeds:</span></span>

```ps1
dotnet add package NuGet.Protocol
```

### <a name="list-package-versions"></a><span data-ttu-id="5497d-113">Listar versões de pacote</span><span class="sxs-lookup"><span data-stu-id="5497d-113">List package versions</span></span>

<span data-ttu-id="5497d-114">Localize todas as versões do Newtonsoft.Jsusando a [API de conteúdo do pacote NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="5497d-114">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="5497d-115">Baixar um pacote</span><span class="sxs-lookup"><span data-stu-id="5497d-115">Download a package</span></span>

<span data-ttu-id="5497d-116">Baixe Newtonsoft.Jsem v 12.0.1 usando a [API de conteúdo do pacote NuGet v3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="5497d-116">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="5497d-117">Obter metadados do pacote</span><span class="sxs-lookup"><span data-stu-id="5497d-117">Get package metadata</span></span>

<span data-ttu-id="5497d-118">Obtenha os metadados para o pacote "Newtonsoft.Json" usando a [API de metadados do pacote NuGet v3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="5497d-118">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="5497d-119">Pesquisar pacotes</span><span class="sxs-lookup"><span data-stu-id="5497d-119">Search packages</span></span>

<span data-ttu-id="5497d-120">Pesquise pacotes "JSON" usando a [API de pesquisa do NuGet v3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="5497d-120">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a><span data-ttu-id="5497d-121">Enviar por push um pacote</span><span class="sxs-lookup"><span data-stu-id="5497d-121">Push a package</span></span>

<span data-ttu-id="5497d-122">Enviar por push um pacote usando a [API de envio por push e exclusão do NuGet v3](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="5497d-122">Push a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a><span data-ttu-id="5497d-123">Excluir um pacote</span><span class="sxs-lookup"><span data-stu-id="5497d-123">Delete a package</span></span>

<span data-ttu-id="5497d-124">Excluir um pacote usando a [API de envio por push e exclusão do NuGet v3](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="5497d-124">Delete a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

> [!Note]
> <span data-ttu-id="5497d-125">Os servidores NuGet são livres para interpretar uma solicitação de exclusão de pacote como "exclusão rígida", "exclusão reversível" ou "deslistar".</span><span class="sxs-lookup"><span data-stu-id="5497d-125">NuGet servers are free to interpret a package delete request as a "hard delete", "soft delete", or "unlist".</span></span>
> <span data-ttu-id="5497d-126">Por exemplo, nuget.org interpreta a solicitação de exclusão de pacote como uma "deslista".</span><span class="sxs-lookup"><span data-stu-id="5497d-126">For example, nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="5497d-127">Para obter mais informações sobre essa prática, consulte a política [excluindo pacotes](../nuget-org/policies/deleting-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="5497d-127">For more information about this practice, see the [Deleting Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span>

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a><span data-ttu-id="5497d-128">Trabalhar com feeds autenticados</span><span class="sxs-lookup"><span data-stu-id="5497d-128">Work with authenticated feeds</span></span>

<span data-ttu-id="5497d-129">Use o [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) para trabalhar com feeds autenticados.</span><span class="sxs-lookup"><span data-stu-id="5497d-129">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) to work with authenticated feeds.</span></span>

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a><span data-ttu-id="5497d-130">NuGet. Packaging</span><span class="sxs-lookup"><span data-stu-id="5497d-130">NuGet.Packaging</span></span>

<span data-ttu-id="5497d-131">Instale o `NuGet.Packaging` pacote para interagir com `.nupkg` `.nuspec` arquivos e de um fluxo:</span><span class="sxs-lookup"><span data-stu-id="5497d-131">Install the `NuGet.Packaging` package to interact with `.nupkg` and `.nuspec` files from a stream:</span></span>

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a><span data-ttu-id="5497d-132">Criar um pacote</span><span class="sxs-lookup"><span data-stu-id="5497d-132">Create a package</span></span>

<span data-ttu-id="5497d-133">Crie um pacote, defina metadados e adicione dependências usando [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="5497d-133">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5497d-134">É altamente recomendável que os pacotes NuGet sejam criados usando as ferramentas oficiais do NuGet e **não** usem essa API de nível baixo.</span><span class="sxs-lookup"><span data-stu-id="5497d-134">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="5497d-135">Há uma variedade de características importantes para um pacote bem formado e a versão mais recente das ferramentas ajuda a incorporar essas práticas recomendadas.</span><span class="sxs-lookup"><span data-stu-id="5497d-135">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="5497d-136">Para obter mais informações sobre como criar pacotes NuGet, consulte a visão geral do [fluxo de trabalho de criação de pacote](../create-packages/overview-and-workflow.md) e a documentação para ferramentas de pacote oficial (por exemplo, [usando a CLI do dotnet](../create-packages/creating-a-package-dotnet-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="5497d-136">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="5497d-137">Ler um pacote</span><span class="sxs-lookup"><span data-stu-id="5497d-137">Read a package</span></span>

<span data-ttu-id="5497d-138">Ler um pacote de um fluxo de arquivos usando [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="5497d-138">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="5497d-139">Documentação de terceiros</span><span class="sxs-lookup"><span data-stu-id="5497d-139">Third-party documentation</span></span>

<span data-ttu-id="5497d-140">Você pode encontrar exemplos e documentação para algumas das APIs na série de Blogs a seguir de Dave Glick, publicada 2016:</span><span class="sxs-lookup"><span data-stu-id="5497d-140">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="5497d-141">Explorando as bibliotecas do NuGet v3, parte 1: introdução e conceitos</span><span class="sxs-lookup"><span data-stu-id="5497d-141">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="5497d-142">Explorando as bibliotecas do NuGet v3, parte 2: pesquisando pacotes</span><span class="sxs-lookup"><span data-stu-id="5497d-142">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="5497d-143">Explorando as bibliotecas do NuGet v3, parte 3: Instalando pacotes</span><span class="sxs-lookup"><span data-stu-id="5497d-143">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="5497d-144">Essas Postagens de blog foram escritas logo após a liberação da versão **3.4.3** dos pacotes do SDK do cliente NuGet.</span><span class="sxs-lookup"><span data-stu-id="5497d-144">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="5497d-145">As versões mais recentes dos pacotes podem ser incompatíveis com as informações nas postagens do blog.</span><span class="sxs-lookup"><span data-stu-id="5497d-145">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="5497d-146">Martin Björkström fez uma postagem no blog de acompanhamento na série de Blogs de Dave Glick, onde ele introduz uma abordagem diferente sobre o uso do SDK de cliente do NuGet para instalar os pacotes NuGet:</span><span class="sxs-lookup"><span data-stu-id="5497d-146">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="5497d-147">Revisitando as bibliotecas do NuGet v3</span><span class="sxs-lookup"><span data-stu-id="5497d-147">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
