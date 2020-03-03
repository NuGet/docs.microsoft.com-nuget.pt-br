---
title: SDK do cliente NuGet
description: A API está em evolução e ainda não está documentada, mas exemplos estão disponíveis no blog de Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: a5c542379318f24ee35ccf25651d0e8de91253ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231234"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="44d44-103">SDK do cliente NuGet</span><span class="sxs-lookup"><span data-stu-id="44d44-103">NuGet Client SDK</span></span>

<span data-ttu-id="44d44-104">O *SDK do cliente NuGet* refere-se a um grupo de pacotes NuGet:</span><span class="sxs-lookup"><span data-stu-id="44d44-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="44d44-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -usado para interagir com http e feeds do NuGet baseados em arquivo</span><span class="sxs-lookup"><span data-stu-id="44d44-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="44d44-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -usado para interagir com pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="44d44-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="44d44-107">`NuGet.Protocol` depende deste pacote</span><span class="sxs-lookup"><span data-stu-id="44d44-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="44d44-108">Você pode encontrar o código-fonte para esses pacotes no repositório do GitHub [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) .</span><span class="sxs-lookup"><span data-stu-id="44d44-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="44d44-109">Para obter a documentação sobre o protocolo de servidor NuGet, consulte a [API do servidor NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="44d44-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="44d44-110">Introdução</span><span class="sxs-lookup"><span data-stu-id="44d44-110">Getting started</span></span>

### <a name="install-the-package"></a><span data-ttu-id="44d44-111">Instalar o pacote</span><span class="sxs-lookup"><span data-stu-id="44d44-111">Install the package</span></span>

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a><span data-ttu-id="44d44-112">Exemplos</span><span class="sxs-lookup"><span data-stu-id="44d44-112">Examples</span></span>

<span data-ttu-id="44d44-113">Você pode encontrar esses exemplos no projeto [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) no github.</span><span class="sxs-lookup"><span data-stu-id="44d44-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="44d44-114">Listar versões de pacote</span><span class="sxs-lookup"><span data-stu-id="44d44-114">List package versions</span></span>

<span data-ttu-id="44d44-115">Localize todas as versões de Newtonsoft. JSON usando a [API de conteúdo do pacote NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="44d44-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="44d44-116">Baixar um pacote</span><span class="sxs-lookup"><span data-stu-id="44d44-116">Download a package</span></span>

<span data-ttu-id="44d44-117">Baixe o Newtonsoft. JSON v 12.0.1 usando a [API de conteúdo do pacote NuGet v3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="44d44-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="44d44-118">Obter metadados do pacote</span><span class="sxs-lookup"><span data-stu-id="44d44-118">Get package metadata</span></span>

<span data-ttu-id="44d44-119">Obtenha os metadados para o pacote "Newtonsoft. JSON" usando a [API de metadados do pacote NuGet v3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="44d44-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="44d44-120">Pesquisar pacotes</span><span class="sxs-lookup"><span data-stu-id="44d44-120">Search packages</span></span>

<span data-ttu-id="44d44-121">Pesquise pacotes "JSON" usando a [API de pesquisa do NuGet v3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="44d44-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a><span data-ttu-id="44d44-122">Documentação de terceiros</span><span class="sxs-lookup"><span data-stu-id="44d44-122">Third-party documentation</span></span>

<span data-ttu-id="44d44-123">Você pode encontrar exemplos e documentação para algumas das APIs na série de Blogs a seguir de Dave Glick, publicada 2016:</span><span class="sxs-lookup"><span data-stu-id="44d44-123">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="44d44-124">Explorando as bibliotecas do NuGet v3, parte 1: introdução e conceitos</span><span class="sxs-lookup"><span data-stu-id="44d44-124">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="44d44-125">Explorando as bibliotecas do NuGet v3, parte 2: pesquisando pacotes</span><span class="sxs-lookup"><span data-stu-id="44d44-125">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="44d44-126">Explorando as bibliotecas do NuGet v3, parte 3: Instalando pacotes</span><span class="sxs-lookup"><span data-stu-id="44d44-126">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="44d44-127">Essas Postagens de blog foram escritas logo após a liberação da versão **3.4.3** dos pacotes do SDK do cliente NuGet.</span><span class="sxs-lookup"><span data-stu-id="44d44-127">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="44d44-128">As versões mais recentes dos pacotes podem ser incompatíveis com as informações nas postagens do blog.</span><span class="sxs-lookup"><span data-stu-id="44d44-128">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="44d44-129">Martin Björkström fez uma postagem no blog de acompanhamento na série de Blogs de Dave Glick, onde ele introduz uma abordagem diferente sobre o uso do SDK de cliente do NuGet para instalar os pacotes NuGet:</span><span class="sxs-lookup"><span data-stu-id="44d44-129">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="44d44-130">Revisitando as bibliotecas do NuGet v3</span><span class="sxs-lookup"><span data-stu-id="44d44-130">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
