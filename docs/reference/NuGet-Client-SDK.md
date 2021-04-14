---
title: SDK do cliente NuGet
description: A API está em evolução e ainda não está documentada, mas exemplos estão disponíveis no blog de Dave Glick.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 6417c971dc13cf9ed05dcec4e4156af94c0ea058
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387381"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="97b48-103">SDK do cliente NuGet</span><span class="sxs-lookup"><span data-stu-id="97b48-103">NuGet Client SDK</span></span>

<span data-ttu-id="97b48-104">O *SDK do cliente NuGet* refere-se a um grupo de pacotes NuGet:</span><span class="sxs-lookup"><span data-stu-id="97b48-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="97b48-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -Usado para interagir com HTTP e feeds do NuGet baseados em arquivo</span><span class="sxs-lookup"><span data-stu-id="97b48-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="97b48-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -Usado para interagir com pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="97b48-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="97b48-107">`NuGet.Protocol` depende deste pacote</span><span class="sxs-lookup"><span data-stu-id="97b48-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="97b48-108">Você pode encontrar o código-fonte para esses pacotes no repositório do GitHub [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) .</span><span class="sxs-lookup"><span data-stu-id="97b48-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>
<span data-ttu-id="97b48-109">Você pode encontrar o código-fonte para esses exemplos no projeto [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) no github.</span><span class="sxs-lookup"><span data-stu-id="97b48-109">You can find the source code for these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) project on GitHub.</span></span>

> [!Note]
> <span data-ttu-id="97b48-110">Para obter a documentação sobre o protocolo de servidor NuGet, consulte a [API do servidor NuGet](~/api/overview.md).</span><span class="sxs-lookup"><span data-stu-id="97b48-110">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="nugetprotocol"></a><span data-ttu-id="97b48-111">NuGet. Protocol</span><span class="sxs-lookup"><span data-stu-id="97b48-111">NuGet.Protocol</span></span>

<span data-ttu-id="97b48-112">Instale o `NuGet.Protocol` pacote para interagir com os feeds de pacote NuGet baseados em pasta e http:</span><span class="sxs-lookup"><span data-stu-id="97b48-112">Install the `NuGet.Protocol` package to interact with HTTP and folder-based NuGet package feeds:</span></span>

```ps1
dotnet add package NuGet.Protocol
```

> [!Tip]
> <span data-ttu-id="97b48-113">`Repository.Factory` é definido no `NuGet.Protocol.Core.Types` namespace, e o `GetCoreV3` método é um método de extensão definido no `NuGet.Protocol` namespace.</span><span class="sxs-lookup"><span data-stu-id="97b48-113">`Repository.Factory` is defined in the `NuGet.Protocol.Core.Types` namespace, and the `GetCoreV3` method is an extension method defined in the `NuGet.Protocol` namespace.</span></span> <span data-ttu-id="97b48-114">Portanto, você precisará adicionar `using` instruções para ambos os namespaces.</span><span class="sxs-lookup"><span data-stu-id="97b48-114">Therefore, you will need to add `using` statements for both namespaces.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="97b48-115">Listar versões de pacote</span><span class="sxs-lookup"><span data-stu-id="97b48-115">List package versions</span></span>

<span data-ttu-id="97b48-116">Localize todas as versões do Newtonsoft.Jsusando a [API de conteúdo do pacote NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):</span><span class="sxs-lookup"><span data-stu-id="97b48-116">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="97b48-117">Baixar um pacote</span><span class="sxs-lookup"><span data-stu-id="97b48-117">Download a package</span></span>

<span data-ttu-id="97b48-118">Baixe Newtonsoft.Jsem v 12.0.1 usando a [API de conteúdo do pacote NuGet v3](../api/package-base-address-resource.md):</span><span class="sxs-lookup"><span data-stu-id="97b48-118">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="97b48-119">Obter metadados do pacote</span><span class="sxs-lookup"><span data-stu-id="97b48-119">Get package metadata</span></span>

<span data-ttu-id="97b48-120">Obtenha os metadados para o pacote "Newtonsoft.Json" usando a [API de metadados do pacote NuGet v3](../api/registration-base-url-resource.md):</span><span class="sxs-lookup"><span data-stu-id="97b48-120">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="97b48-121">Pesquisar pacotes</span><span class="sxs-lookup"><span data-stu-id="97b48-121">Search packages</span></span>

<span data-ttu-id="97b48-122">Pesquise pacotes "JSON" usando a [API de pesquisa do NuGet v3](../api/search-query-service-resource.md):</span><span class="sxs-lookup"><span data-stu-id="97b48-122">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a><span data-ttu-id="97b48-123">Enviar por push um pacote</span><span class="sxs-lookup"><span data-stu-id="97b48-123">Push a package</span></span>

<span data-ttu-id="97b48-124">Enviar por push um pacote usando a [API de envio por push e exclusão do NuGet v3](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="97b48-124">Push a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a><span data-ttu-id="97b48-125">Excluir um pacote</span><span class="sxs-lookup"><span data-stu-id="97b48-125">Delete a package</span></span>

<span data-ttu-id="97b48-126">Excluir um pacote usando a [API de envio por push e exclusão do NuGet v3](../api/package-publish-resource.md):</span><span class="sxs-lookup"><span data-stu-id="97b48-126">Delete a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

> [!Note]
> <span data-ttu-id="97b48-127">Os servidores NuGet são livres para interpretar uma solicitação de exclusão de pacote como "exclusão rígida", "exclusão reversível" ou "deslistar".</span><span class="sxs-lookup"><span data-stu-id="97b48-127">NuGet servers are free to interpret a package delete request as a "hard delete", "soft delete", or "unlist".</span></span>
> <span data-ttu-id="97b48-128">Por exemplo, nuget.org interpreta a solicitação de exclusão de pacote como uma "deslista".</span><span class="sxs-lookup"><span data-stu-id="97b48-128">For example, nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="97b48-129">Para obter mais informações sobre essa prática, consulte a política [excluindo pacotes](../nuget-org/policies/deleting-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="97b48-129">For more information about this practice, see the [Deleting Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span>

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a><span data-ttu-id="97b48-130">Trabalhar com feeds autenticados</span><span class="sxs-lookup"><span data-stu-id="97b48-130">Work with authenticated feeds</span></span>

<span data-ttu-id="97b48-131">Use o [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) para trabalhar com feeds autenticados.</span><span class="sxs-lookup"><span data-stu-id="97b48-131">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) to work with authenticated feeds.</span></span>

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a><span data-ttu-id="97b48-132">NuGet. Packaging</span><span class="sxs-lookup"><span data-stu-id="97b48-132">NuGet.Packaging</span></span>

<span data-ttu-id="97b48-133">Instale o `NuGet.Packaging` pacote para interagir com `.nupkg` `.nuspec` arquivos e de um fluxo:</span><span class="sxs-lookup"><span data-stu-id="97b48-133">Install the `NuGet.Packaging` package to interact with `.nupkg` and `.nuspec` files from a stream:</span></span>

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a><span data-ttu-id="97b48-134">Criar um pacote</span><span class="sxs-lookup"><span data-stu-id="97b48-134">Create a package</span></span>

<span data-ttu-id="97b48-135">Crie um pacote, defina metadados e adicione dependências usando [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="97b48-135">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97b48-136">É altamente recomendável que os pacotes NuGet sejam criados usando as ferramentas oficiais do NuGet e **não** usem essa API de nível baixo.</span><span class="sxs-lookup"><span data-stu-id="97b48-136">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="97b48-137">Há uma variedade de características importantes para um pacote bem formado e a versão mais recente das ferramentas ajuda a incorporar essas práticas recomendadas.</span><span class="sxs-lookup"><span data-stu-id="97b48-137">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="97b48-138">Para obter mais informações sobre como criar pacotes NuGet, consulte a visão geral do [fluxo de trabalho de criação de pacote](../create-packages/overview-and-workflow.md) e a documentação para ferramentas de pacote oficial (por exemplo, [usando a CLI do dotnet](../create-packages/creating-a-package-dotnet-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="97b48-138">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="97b48-139">Ler um pacote</span><span class="sxs-lookup"><span data-stu-id="97b48-139">Read a package</span></span>

<span data-ttu-id="97b48-140">Ler um pacote de um fluxo de arquivos usando [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="97b48-140">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="97b48-141">Documentação de terceiros</span><span class="sxs-lookup"><span data-stu-id="97b48-141">Third-party documentation</span></span>

<span data-ttu-id="97b48-142">Você pode encontrar exemplos e documentação para algumas das APIs na série de Blogs a seguir de Dave Glick, publicada 2016:</span><span class="sxs-lookup"><span data-stu-id="97b48-142">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="97b48-143">Explorando as bibliotecas do NuGet v3, parte 1: introdução e conceitos</span><span class="sxs-lookup"><span data-stu-id="97b48-143">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="97b48-144">Explorando as bibliotecas do NuGet v3, parte 2: pesquisando pacotes</span><span class="sxs-lookup"><span data-stu-id="97b48-144">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="97b48-145">Explorando as bibliotecas do NuGet v3, parte 3: Instalando pacotes</span><span class="sxs-lookup"><span data-stu-id="97b48-145">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="97b48-146">Essas Postagens de blog foram escritas logo após a liberação da versão **3.4.3** dos pacotes do SDK do cliente NuGet.</span><span class="sxs-lookup"><span data-stu-id="97b48-146">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="97b48-147">As versões mais recentes dos pacotes podem ser incompatíveis com as informações nas postagens do blog.</span><span class="sxs-lookup"><span data-stu-id="97b48-147">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="97b48-148">Martin Björkström fez uma postagem no blog de acompanhamento na série de Blogs de Dave Glick, onde ele introduz uma abordagem diferente sobre o uso do SDK de cliente do NuGet para instalar os pacotes NuGet:</span><span class="sxs-lookup"><span data-stu-id="97b48-148">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="97b48-149">Revisitando as bibliotecas do NuGet v3</span><span class="sxs-lookup"><span data-stu-id="97b48-149">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
