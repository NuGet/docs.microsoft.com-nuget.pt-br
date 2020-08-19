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
# <a name="nuget-client-sdk"></a>SDK do cliente NuGet

O *SDK do cliente NuGet* refere-se a um grupo de pacotes NuGet:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -Usado para interagir com HTTP e feeds do NuGet baseados em arquivo
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -Usado para interagir com pacotes NuGet. `NuGet.Protocol` depende deste pacote

Você pode encontrar o código-fonte para esses pacotes no repositório do GitHub [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) .

> [!Note]
> Para obter a documentação sobre o protocolo de servidor NuGet, consulte a [API do servidor NuGet](~/api/overview.md).

## <a name="getting-started"></a>Introdução

### <a name="install-the-packages"></a>Instalar os pacotes

```ps1
dotnet add package NuGet.Protocol  # interact with HTTP and folder-based NuGet package feeds, includes NuGet.Packaging

dotnet add package NuGet.Packaging # interact with .nupkg and .nuspec files from a stream
```

## <a name="examples"></a>Exemplos

Você pode encontrar esses exemplos no projeto [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) no github.

### <a name="list-package-versions"></a>Listar versões de pacote

Localize todas as versões do Newtonsoft.Jsusando a [API de conteúdo do pacote NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Baixar um pacote

Baixe Newtonsoft.Jsem v 12.0.1 usando a [API de conteúdo do pacote NuGet v3](../api/package-base-address-resource.md):

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Obter metadados do pacote

Obtenha os metadados para o pacote "Newtonsoft.Json" usando a [API de metadados do pacote NuGet v3](../api/registration-base-url-resource.md):

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Pesquisar pacotes

Pesquise pacotes "JSON" usando a [API de pesquisa do NuGet v3](../api/search-query-service-resource.md):

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="create-a-package"></a>Criar um pacote

Crie um pacote, defina metadados e adicione dependências usando [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

> [!IMPORTANT]
> É altamente recomendável que os pacotes NuGet sejam criados usando as ferramentas oficiais do NuGet e **não** usem essa API de nível baixo. Há uma variedade de características importantes para um pacote bem formado e a versão mais recente das ferramentas ajuda a incorporar essas práticas recomendadas.
> 
> Para obter mais informações sobre como criar pacotes NuGet, consulte a visão geral do [fluxo de trabalho de criação de pacote](../create-packages/overview-and-workflow.md) e a documentação para ferramentas de pacote oficial (por exemplo, [usando a CLI do dotnet](../create-packages/creating-a-package-dotnet-cli.md)).

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a>Ler um pacote

Ler um pacote de um fluxo de arquivos usando [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a>Documentação de terceiros

Você pode encontrar exemplos e documentação para algumas das APIs na série de Blogs a seguir de Dave Glick, publicada 2016:

- [Explorando as bibliotecas do NuGet v3, parte 1: introdução e conceitos](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Explorando as bibliotecas do NuGet v3, parte 2: pesquisando pacotes](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Explorando as bibliotecas do NuGet v3, parte 3: Instalando pacotes](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Essas Postagens de blog foram escritas logo após a liberação da versão **3.4.3** dos pacotes do SDK do cliente NuGet.
> As versões mais recentes dos pacotes podem ser incompatíveis com as informações nas postagens do blog.

Martin Björkström fez uma postagem no blog de acompanhamento na série de Blogs de Dave Glick, onde ele introduz uma abordagem diferente sobre o uso do SDK de cliente do NuGet para instalar os pacotes NuGet:

- [Revisitando as bibliotecas do NuGet v3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
