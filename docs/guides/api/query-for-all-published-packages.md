---
title: Consulta para todos os pacotes publicados em nuget.org
description: Usando a API do NuGet, você pode consultar todos os pacotes publicados em nuget.org e manter-se atualizado com o passar do tempo.
author: joelverhagen
ms.author: jver
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 749d9466976d51c7cb65332c8b149e3a30862e63
ms.sourcegitcommit: 650c08f8bc3d48dfd206a111e5e2aaca3001f569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97523403"
---
# <a name="query-for-all-packages-published-to-nugetorg"></a>Consulta para todos os pacotes publicados em nuget.org

Um padrão de consulta comum na API OData V2 herdada estava enumerando todos os pacotes publicados em nuget.org, ordenados por quando o pacote foi publicado. Cenários que exigem esse tipo de consulta em nuget.org variam muito:

- Replicando o nuget.org totalmente
- Detectar o lançamento de novas versões dos pacotes
- Localizando os pacotes que dependem do seu pacote

O modo herdado de fazer isso normalmente depende da classificação da entidade de pacote de OData por um carimbo de data/hora e a paginação em um enorme conjunto de resultados usando os parâmetros `skip` e `top` (tamanho da página). Infelizmente, essa abordagem traz algumas desvantagens:

- Possibilidade de pacotes ausentes, pois as consultas estão sendo feitas em dados que geralmente têm a ordem alterada
- Tempo de resposta de consulta lento porque as consultas não são otimizadas (as consultas mais otimizadas são aquelas compatíveis com um cenário principal para o cliente do NuGet oficial)
- Uso de API preterida e não documentada, o que significa que não há garantia de suporte para tais consultas no futuro
- Incapacidade de reproduzir o histórico na ordem exata em que ele ocorreu

Por esse motivo, o guia a seguir pode ser seguido para resolver os cenários mencionados acima de maneira mais confiável e pronta para o futuro.

## <a name="overview"></a>Visão geral

No centro deste guia está o recurso na [API do NuGet](../../api/overview.md) chamado de **catálogo**. O catálogo é uma API somente de acréscimo que permite que o chamador Veja um histórico completo de pacotes adicionados a, modificados e excluídos do nuget.org. Se você estiver interessado em todos ou mesmo em um subconjunto de pacotes publicados no nuget.org, o catálogo é uma ótima maneira de se manter atualizado com o conjunto de pacotes disponíveis no momento, à medida que o tempo continua.

Este guia busca ser uma explicação passo a passo de alto nível, mas se você estiver interessado nos detalhes refinados do catálogo, consulte o [Documento de referência de API](../../api/catalog-resource.md).

As etapas a seguir podem ser implementadas em qualquer linguagem de programação de sua escolha. Se você quiser um exemplo completo de execução, examine o [exemplo de C#](#c-sample-code) mencionado abaixo.

Caso contrário, siga o guia abaixo para compilar um leitor de catálogo confiável.

## <a name="initialize-a-cursor"></a>Inicializar um cursor

A primeira etapa na compilação de um leitor de catálogo confiável é a implementação de um cursor. Para ver detalhes completos sobre o design de um cursor de catálogo, consulte o [documento de referência do catálogo](../../api/catalog-resource.md#cursor). Em resumo, o cursor é um ponto no tempo até o momento em que você processou eventos no catálogo. Eventos no catálogo representam publicações de pacote e outras alterações de pacote. Se você tem interesse em todos os pacotes já publicados no NuGet (desde o início dos tempos), inicialize seu cursor para um carimbo de data/hora de “valor mínimo” (por exemplo, `DateTime.MinValue` no .NET). Se você tem interesse apenas nos pacotes publicados a partir de agora, use o carimbo de data/hora atual como o valor inicial do cursor.

Para este guia, inicializaremos nosso cursor para um carimbo de data/hora de uma hora atrás. Por enquanto, memorize esse carimbo de data/hora.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>Determinar a URL do índice do catálogo

A localização de cada recurso (ponto de extremidade) na API do NuGet deve ser descoberta usando o [índice de serviço](../../api/service-index.md). Como este guia se concentra no nuget.org, usaremos o índice de serviço do nuget.org.

    GET https://api.nuget.org/v3/index.json

O documento de serviço é um documento JSON que contém todos os recursos em nuget.org. Procure o recurso que tem o `@type` valor da propriedade de `Catalog/3.0.0` . O valor da propriedade `@id` associado é a URL para o próprio índice do catálogo. 

## <a name="find-new-catalog-leaves"></a>Localizar novas folhas de catálogo

Usando o valor da propriedade `@id` na etapa anterior, baixe o índice do catálogo:

    GET https://api.nuget.org/v3/catalog0/index.json

Desserialize o [índice do catálogo](../../api/catalog-resource.md#catalog-index). Filtre todos os [objetos de página de catálogo](../../api/catalog-resource.md#catalog-page-object-in-the-index) com `commitTimeStamp` menor ou igual ao valor atual do cursor.

Para cada página de catálogo restante, baixe o documento completo usando a propriedade `@id`.

    GET https://api.nuget.org/v3/catalog0/page2926.json

Desserialize a [página do catálogo](../../api/catalog-resource.md#catalog-page). Filtre todos os [objetos de folha de catálogo](../../api/catalog-resource.md#catalog-item-object-in-a-page) com `commitTimeStamp` menor ou igual ao seu valor atual do cursor.

Depois de baixar todas as páginas de catálogo não filtradas, você terá um conjunto de objetos de folha de catálogo que representam os pacotes que foram publicados, não listados, listados ou excluídos no período entre o carimbo de data/hora do cursor e o momento atual.

## <a name="process-catalog-leaves"></a>Processar folhas de catálogo

Neste ponto, você pode executar qualquer processamento personalizado que desejar nos itens de catálogo. Se tudo o que você precisa é a ID e a versão do pacote, é possível inspecionar as propriedades `nuget:id` e `nuget:version` nos objetos de itens do catálogo encontrados nas páginas. Examine a propriedade `@type` para saber se o item de catálogo se refere a um pacote existente ou um pacote excluído.

Se você estiver interessado nos metadados sobre o pacote (como a descrição, dependências, tamanho do .nupkg, etc), busque o [documento de folha de catálogo](../../api/catalog-resource.md#catalog-leaf) usando a propriedade `@id`.

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

Este documento contém todos os metadados incluídos nos [recursos de metadados do pacote](../../api/registration-base-url-resource.md) e muito mais.

É nesta etapa que sua lógica personalizada é implementada. As outras etapas neste guia são implementadas praticamente da mesma forma, independentemente do que você está fazendo com as folhas de catálogo.

### <a name="downloading-the-nupkg"></a>Baixar o .nupkg

Se você estiver interessado em baixar o .nupkg para pacotes encontrado no catálogo, utilize o [recurso de conteúdo do pacote](../../api/package-base-address-resource.md). No entanto, observe que há um breve atraso entre quando um pacote é encontrado no catálogo e quando ele está disponível no recurso de conteúdo do pacote. Portanto, se você encontrar `404 Not Found` ao tentar baixar um .nupkg para um pacote encontrado no catálogo, basta tentar novamente um pouco mais tarde. A correção desse atraso é acompanhada pelo problema do GitHub [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).

## <a name="move-the-cursor-forward"></a>Mover o cursor para frente

Depois de você ter processado com êxito os itens de catálogo, será necessário determinar o novo valor de cursor a ser salvo. Para fazer isso, localize o `commitTimeStamp` máximo (mais recentes em ordem cronológica) de todos os itens de catálogo que você processou. Este é o novo valor do cursor. Salve-o em um repositório permanente, como um banco de dados, sistema de arquivos ou armazenamento de blobs. Quando você desejar obter mais itens de catálogo, basta iniciar da [primeira etapa](#initialize-a-cursor) inicializando o valor do cursor desse repositório persistente.

Se seu aplicativo gerar uma exceção ou falhas, não mova o cursor para a frente. Mover o cursor para a frente significa nunca precisar processar itens de catálogo novamente antes do cursor.

Se, por algum motivo, você tiver um bug no modo de processamento de catálogo, basta simplesmente mover o cursor para trás no tempo e permitir que seu código reprocesse os itens antigos do catálogo.

## <a name="c-sample-code"></a>Código de exemplo C#

Como o catálogo é um conjunto de documentos JSON disponíveis por HTTP, é possível interagir com ele usando qualquer linguagem de programação que tenha um cliente HTTP e um desserializador JSON.

Exemplos de C# estão disponíveis no [repositório do NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>SDK do Catálogo

A maneira mais fácil de consumir o catálogo é usar o pacote de pré-lançamento do SDK do catálogo do .NET `NuGet.Protocol.Catalog` , que está disponível em Azure Artifacts usando a seguinte URL de origem do pacote NuGet: `https://pkgs.dev.azure.com/dnceng/public/_packaging/nuget-build/nuget/v3/index.json` .

Você pode instalar esse pacote em um projeto compatível com `netstandard1.3` ou superior (como o .NET Framework 4.6).

Um exemplo que usa este pacote está disponível no GitHub no [projeto NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).

#### <a name="sample-output"></a>Saída de exemplo

```output
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a>Exemplo mínimo

Para ver um exemplo com menos dependências que ilustra a interação com o catálogo em mais detalhes, consulte o [projeto de exemplo CatalogReaderExample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample). Os projeto é voltado para `netcoreapp2.0` e depende do [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (para resolver o índice de serviço) e [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (para desserialização JSON).

A lógica principal do código pode ser vista no [arquivo Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).

#### <a name="sample-output"></a>Saída de exemplo

```output
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
