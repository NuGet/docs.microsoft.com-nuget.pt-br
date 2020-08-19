---
title: SDK do cliente NuGet
description: A API está em evolução e ainda não está documentada, mas exemplos estão disponíveis no blog de Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 39a4de4071eec70c88a2add158f2a3a734f7d7b7
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622922"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="883fc-103">SDK do cliente NuGet</span><span class="sxs-lookup"><span data-stu-id="883fc-103">NuGet Client SDK</span></span>

<span data-ttu-id="883fc-104">O *SDK do cliente NuGet* refere-se a um grupo de pacotes NuGet:</span><span class="sxs-lookup"><span data-stu-id="883fc-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="883fc-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -Usado para interagir com HTTP e feeds do NuGet baseados em arquivo</span><span class="sxs-lookup"><span data-stu-id="883fc-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="883fc-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -Usado para interagir com pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="883fc-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="883fc-107">`NuGet.Protocol` depende deste pacote</span><span class="sxs-lookup"><span data-stu-id="883fc-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="883fc-108">Você pode encontrar o código-fonte para esses pacotes no repositório do GitHub [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) .</span><span class="sxs-lookup"><span data-stu-id="883fc-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="883fc-109">Para obter a documentação sobre o protocolo de servidor NuGet, consulte a [API do servidor NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="883fc-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="883fc-110">Introdução</span><span class="sxs-lookup"><span data-stu-id="883fc-110">Getting started</span></span>

### <a name="install-the-packages"></a><span data-ttu-id="883fc-111">Instalar os pacotes</span><span class="sxs-lookup"><span data-stu-id="883fc-111">Install the packages</span></span>

```ps1
dotnet add package NuGet.Protocol  # interact with HTTP and folder-based NuGet package feeds, includes NuGet.Packaging

dotnet add package NuGet.Packaging # interact with .nupkg and .nuspec files from a stream
```

## <a name="examples"></a><span data-ttu-id="883fc-112">Exemplos</span><span class="sxs-lookup"><span data-stu-id="883fc-112">Examples</span></span>

<span data-ttu-id="883fc-113">Você pode encontrar esses exemplos no projeto [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) no github.</span><span class="sxs-lookup"><span data-stu-id="883fc-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="883fc-114">Listar versões de pacote</span><span class="sxs-lookup"><span data-stu-id="883fc-114">List package versions</span></span>

<span data-ttu-id="883fc-115">Localize todas as versões do Newtonsoft.Jsusando a [API de conteúdo do pacote NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="883fc-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="883fc-116">Baixar um pacote</span><span class="sxs-lookup"><span data-stu-id="883fc-116">Download a package</span></span>

<span data-ttu-id="883fc-117">Baixe Newtonsoft.Jsem v 12.0.1 usando a [API de conteúdo do pacote NuGet v3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="883fc-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="883fc-118">Obter metadados do pacote</span><span class="sxs-lookup"><span data-stu-id="883fc-118">Get package metadata</span></span>

<span data-ttu-id="883fc-119">Obtenha os metadados para o pacote "Newtonsoft.Json" usando a [API de metadados do pacote NuGet v3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="883fc-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="883fc-120">Pesquisar pacotes</span><span class="sxs-lookup"><span data-stu-id="883fc-120">Search packages</span></span>

<span data-ttu-id="883fc-121">Pesquise pacotes "JSON" usando a [API de pesquisa do NuGet v3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="883fc-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="create-a-package"></a><span data-ttu-id="883fc-122">Criar um pacote</span><span class="sxs-lookup"><span data-stu-id="883fc-122">Create a package</span></span>

<span data-ttu-id="883fc-123">Crie um pacote, defina metadados e adicione dependências usando [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="883fc-123">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="883fc-124">É altamente recomendável que os pacotes NuGet sejam criados usando as ferramentas oficiais do NuGet e **não** usem essa API de nível baixo.</span><span class="sxs-lookup"><span data-stu-id="883fc-124">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="883fc-125">Há uma variedade de características importantes para um pacote bem formado e a versão mais recente das ferramentas ajuda a incorporar essas práticas recomendadas.</span><span class="sxs-lookup"><span data-stu-id="883fc-125">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="883fc-126">Para obter mais informações sobre como criar pacotes NuGet, consulte a visão geral do [fluxo de trabalho de criação de pacote](../create-packages/overview-and-workflow.md) e a documentação para ferramentas de pacote oficial (por exemplo, [usando a CLI do dotnet](../create-packages/creating-a-package-dotnet-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="883fc-126">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="883fc-127">Ler um pacote</span><span class="sxs-lookup"><span data-stu-id="883fc-127">Read a package</span></span>

<span data-ttu-id="883fc-128">Ler um pacote de um fluxo de arquivos usando [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="883fc-128">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="883fc-129">Documentação de terceiros</span><span class="sxs-lookup"><span data-stu-id="883fc-129">Third-party documentation</span></span>

<span data-ttu-id="883fc-130">Você pode encontrar exemplos e documentação para algumas das APIs na série de Blogs a seguir de Dave Glick, publicada 2016:</span><span class="sxs-lookup"><span data-stu-id="883fc-130">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="883fc-131">Explorando as bibliotecas do NuGet v3, parte 1: introdução e conceitos</span><span class="sxs-lookup"><span data-stu-id="883fc-131">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="883fc-132">Explorando as bibliotecas do NuGet v3, parte 2: pesquisando pacotes</span><span class="sxs-lookup"><span data-stu-id="883fc-132">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="883fc-133">Explorando as bibliotecas do NuGet v3, parte 3: Instalando pacotes</span><span class="sxs-lookup"><span data-stu-id="883fc-133">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="883fc-134">Essas Postagens de blog foram escritas logo após a liberação da versão **3.4.3** dos pacotes do SDK do cliente NuGet.</span><span class="sxs-lookup"><span data-stu-id="883fc-134">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="883fc-135">As versões mais recentes dos pacotes podem ser incompatíveis com as informações nas postagens do blog.</span><span class="sxs-lookup"><span data-stu-id="883fc-135">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="883fc-136">Martin Björkström fez uma postagem no blog de acompanhamento na série de Blogs de Dave Glick, onde ele introduz uma abordagem diferente sobre o uso do SDK de cliente do NuGet para instalar os pacotes NuGet:</span><span class="sxs-lookup"><span data-stu-id="883fc-136">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="883fc-137">Revisitando as bibliotecas do NuGet v3</span><span class="sxs-lookup"><span data-stu-id="883fc-137">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
