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
# <a name="nuget-client-sdk"></a>SDK do cliente NuGet

O *SDK do cliente NuGet* refere-se a um grupo de pacotes NuGet:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -usado para interagir com http e feeds do NuGet baseados em arquivo
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -usado para interagir com pacotes NuGet. `NuGet.Protocol` depende deste pacote

Você pode encontrar o código-fonte para esses pacotes no repositório do GitHub [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) .

> [!Note]
> Para obter a documentação sobre o protocolo de servidor NuGet, consulte a [API do servidor NuGet](~/api/overview.md).

## <a name="getting-started"></a>Introdução

### <a name="install-the-package"></a>Instalar o pacote

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a>Exemplos

Você pode encontrar esses exemplos no projeto [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) no github.

### <a name="list-package-versions"></a>Listar versões de pacote

Localize todas as versões de Newtonsoft. JSON usando a [API de conteúdo do pacote NuGet v3](../api/package-base-address-resource.md#enumerate-package-versions):

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Baixar um pacote

Baixe o Newtonsoft. JSON v 12.0.1 usando a [API de conteúdo do pacote NuGet v3](../api/package-base-address-resource.md):

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Obter metadados do pacote

Obtenha os metadados para o pacote "Newtonsoft. JSON" usando a [API de metadados do pacote NuGet v3](../api/registration-base-url-resource.md):

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Pesquisar pacotes

Pesquise pacotes "JSON" usando a [API de pesquisa do NuGet v3](../api/search-query-service-resource.md):

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

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
