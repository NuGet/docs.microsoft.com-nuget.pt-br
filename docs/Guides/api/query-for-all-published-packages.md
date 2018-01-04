---
title: Consulta para todos os pacotes publicados em nuget.org | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 11/2/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 5d017cd4-3d75-4341-ba90-3c57be093b7d
description: "Usando a API do NuGet, você pode consultar todos os pacotes publicados em nuget.org e manter-se atualizado com o passar do tempo."
keywords: "A API do NuGet enumera todos os pacotes, pacotes de replicação da API do NuGet, os pacotes mais recentes publicados em nuget.org"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 50a5be4cb0405ad78a72d0497612781a4b346060
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="0ffca-104">Consulta para todos os pacotes publicados em nuget.org</span><span class="sxs-lookup"><span data-stu-id="0ffca-104">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="0ffca-105">Um padrão de consulta comum na API OData V2 herdada estava enumerando todos os pacotes publicados em nuget.org, ordenados por quando o pacote foi publicado.</span><span class="sxs-lookup"><span data-stu-id="0ffca-105">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="0ffca-106">Cenários que exigem esse tipo de consulta em nuget.org variam muito:</span><span class="sxs-lookup"><span data-stu-id="0ffca-106">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="0ffca-107">Replicando o nuget.org totalmente</span><span class="sxs-lookup"><span data-stu-id="0ffca-107">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="0ffca-108">Detectar o lançamento de novas versões dos pacotes</span><span class="sxs-lookup"><span data-stu-id="0ffca-108">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="0ffca-109">Localizando os pacotes que dependem do seu pacote</span><span class="sxs-lookup"><span data-stu-id="0ffca-109">Finding packages that depend on your package</span></span>

<span data-ttu-id="0ffca-110">O modo herdado de fazer isso normalmente depende da classificação da entidade de pacote de OData por um carimbo de data/hora e a paginação em um enorme conjunto de resultados usando os parâmetros `skip` e `top` (tamanho da página).</span><span class="sxs-lookup"><span data-stu-id="0ffca-110">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="0ffca-111">Infelizmente, essa abordagem traz algumas desvantagens:</span><span class="sxs-lookup"><span data-stu-id="0ffca-111">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="0ffca-112">Possibilidade de pacotes ausentes, pois as consultas estão sendo feitas em dados que geralmente têm a ordem alterada</span><span class="sxs-lookup"><span data-stu-id="0ffca-112">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="0ffca-113">Tempo de resposta de consulta lento porque as consultas não são otimizadas (as consultas mais otimizadas são aquelas compatíveis com um cenário principal para o cliente do NuGet oficial)</span><span class="sxs-lookup"><span data-stu-id="0ffca-113">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="0ffca-114">Uso de API preterida e não documentada, o que significa que não há garantia de suporte para tais consultas no futuro</span><span class="sxs-lookup"><span data-stu-id="0ffca-114">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="0ffca-115">Incapacidade de reproduzir o histórico na ordem exata em que ele ocorreu</span><span class="sxs-lookup"><span data-stu-id="0ffca-115">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="0ffca-116">Por esse motivo, o guia a seguir pode ser seguido para resolver os cenários mencionados acima de maneira mais confiável e pronta para o futuro.</span><span class="sxs-lookup"><span data-stu-id="0ffca-116">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="0ffca-117">Visão Geral</span><span class="sxs-lookup"><span data-stu-id="0ffca-117">Overview</span></span>

<span data-ttu-id="0ffca-118">No centro deste guia está o recurso na [API do NuGet](../../api/overview.md) chamado de **catálogo**.</span><span class="sxs-lookup"><span data-stu-id="0ffca-118">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="0ffca-119">O catálogo é uma API somente de acréscimo que permite que o chamador veja um histórico completo de pacotes adicionados, modificados e excluídos do nuget.org. Se você estiver interessado em todos ou até mesmo em um subconjunto dos pacotes publicados no nuget.org, o catálogo é uma ótima maneira de se manter atualizado com o conjunto de pacotes disponíveis atualmente à medida que o tempo passa.</span><span class="sxs-lookup"><span data-stu-id="0ffca-119">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="0ffca-120">Este guia busca ser uma explicação passo a passo de alto nível, mas se você estiver interessado nos detalhes refinados do catálogo, consulte o [Documento de referência de API](../../api/catalog-resource.md).</span><span class="sxs-lookup"><span data-stu-id="0ffca-120">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="0ffca-121">As etapas a seguir podem ser implementadas em qualquer linguagem de programação de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="0ffca-121">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="0ffca-122">Se você quiser um exemplo completo de execução, examine o [exemplo de C#](#c-sample-code) mencionado abaixo.</span><span class="sxs-lookup"><span data-stu-id="0ffca-122">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="0ffca-123">Caso contrário, siga o guia abaixo para compilar um leitor de catálogo confiável.</span><span class="sxs-lookup"><span data-stu-id="0ffca-123">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="0ffca-124">Inicializar um cursor</span><span class="sxs-lookup"><span data-stu-id="0ffca-124">Initialize a cursor</span></span>

<span data-ttu-id="0ffca-125">A primeira etapa na compilação de um leitor de catálogo confiável é a implementação de um cursor.</span><span class="sxs-lookup"><span data-stu-id="0ffca-125">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="0ffca-126">Para ver detalhes completos sobre o design de um cursor de catálogo, consulte o [documento de referência do catálogo](../../api/catalog-resource.md#cursor).</span><span class="sxs-lookup"><span data-stu-id="0ffca-126">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="0ffca-127">Em resumo, o cursor é um ponto no tempo até o momento em que você processou eventos no catálogo.</span><span class="sxs-lookup"><span data-stu-id="0ffca-127">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="0ffca-128">Eventos no catálogo representam publicações de pacote e outras alterações de pacote.</span><span class="sxs-lookup"><span data-stu-id="0ffca-128">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="0ffca-129">Se você tem interesse em todos os pacotes já publicados no NuGet (desde o início dos tempos), inicialize seu cursor para um carimbo de data/hora de “valor mínimo” (por exemplo, `DateTime.MinValue` no .NET).</span><span class="sxs-lookup"><span data-stu-id="0ffca-129">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="0ffca-130">Se você tem interesse apenas nos pacotes publicados a partir de agora, use o carimbo de data/hora atual como o valor inicial do cursor.</span><span class="sxs-lookup"><span data-stu-id="0ffca-130">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="0ffca-131">Para este guia, inicializaremos nosso cursor para um carimbo de data/hora de uma hora atrás.</span><span class="sxs-lookup"><span data-stu-id="0ffca-131">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="0ffca-132">Por enquanto, memorize esse carimbo de data/hora.</span><span class="sxs-lookup"><span data-stu-id="0ffca-132">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="0ffca-133">Determinar a URL do índice do catálogo</span><span class="sxs-lookup"><span data-stu-id="0ffca-133">Determine catalog index URL</span></span>

<span data-ttu-id="0ffca-134">A localização de cada recurso (ponto de extremidade) na API do NuGet deve ser descoberta usando o [índice de serviço](../../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="0ffca-134">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="0ffca-135">Como este guia se concentra no nuget.org, usaremos o índice de serviço do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0ffca-135">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

```
GET https://api.nuget.org/v3/index.json
```

<span data-ttu-id="0ffca-136">O documento de serviço é um documento JSON que contém todos os recursos em nuget.org. Procure o recurso com a propriedade `@type` com valor `Catalog/3.0.0`.</span><span class="sxs-lookup"><span data-stu-id="0ffca-136">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="0ffca-137">O valor da propriedade `@id` associado é a URL para o próprio índice do catálogo.</span><span class="sxs-lookup"><span data-stu-id="0ffca-137">The associated `@id` property value is the URL to the catalog index itself.</span></span>

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="0ffca-138">Localizar novas folhas de catálogo</span><span class="sxs-lookup"><span data-stu-id="0ffca-138">Find new catalog leaves</span></span>

<span data-ttu-id="0ffca-139">Usando o valor da propriedade `@id` na etapa anterior, baixe o índice do catálogo:</span><span class="sxs-lookup"><span data-stu-id="0ffca-139">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

```
GET https://api.nuget.org/v3/catalog0/index.json
```

<span data-ttu-id="0ffca-140">Desserialize o [índice do catálogo](../../api/catalog-resource.md#catalog-index).</span><span class="sxs-lookup"><span data-stu-id="0ffca-140">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="0ffca-141">Filtre todos os [objetos de página de catálogo](../../api/catalog-resource.md#catalog-page-object-in-the-index) com `commitTimeStamp` menor ou igual ao valor atual do cursor.</span><span class="sxs-lookup"><span data-stu-id="0ffca-141">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="0ffca-142">Para cada página de catálogo restante, baixe o documento completo usando a propriedade `@id`.</span><span class="sxs-lookup"><span data-stu-id="0ffca-142">For each remaining catalog page, download the full document using the `@id` property.</span></span>

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

<span data-ttu-id="0ffca-143">Desserialize a [página do catálogo](../../api/catalog-resource.md#catalog-page).</span><span class="sxs-lookup"><span data-stu-id="0ffca-143">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="0ffca-144">Filtre todos os [objetos de folha de catálogo](../../api/catalog-resource.md#catalog-item-object-in-a-page) com `commitTimeStamp` menor ou igual ao seu valor atual do cursor.</span><span class="sxs-lookup"><span data-stu-id="0ffca-144">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="0ffca-145">Depois de baixar todas as páginas de catálogo não filtradas, você terá um conjunto de objetos de folha de catálogo que representam os pacotes que foram publicados, não listados, listados ou excluídos no período entre o carimbo de data/hora do cursor e o momento atual.</span><span class="sxs-lookup"><span data-stu-id="0ffca-145">After you have downloaded all of the catalog pages not filtered out, you will have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="0ffca-146">Processar folhas de catálogo</span><span class="sxs-lookup"><span data-stu-id="0ffca-146">Process catalog leaves</span></span>

<span data-ttu-id="0ffca-147">Neste ponto, você pode executar qualquer processamento personalizado que desejar nos itens de catálogo.</span><span class="sxs-lookup"><span data-stu-id="0ffca-147">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="0ffca-148">Se tudo o que você precisa é a ID e a versão do pacote, é possível inspecionar as propriedades `nuget:id` e `nuget:version` nos objetos de itens do catálogo encontrados nas páginas.</span><span class="sxs-lookup"><span data-stu-id="0ffca-148">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="0ffca-149">Examine a propriedade `@type` para saber se o item de catálogo se refere a um pacote existente ou um pacote excluído.</span><span class="sxs-lookup"><span data-stu-id="0ffca-149">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="0ffca-150">Se você estiver interessado nos metadados sobre o pacote (como a descrição, dependências, tamanho do .nupkg, etc), busque o [documento de folha de catálogo](../../api/catalog-resource.md#catalog-leaf) usando a propriedade `@id`.</span><span class="sxs-lookup"><span data-stu-id="0ffca-150">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

<span data-ttu-id="0ffca-151">Este documento contém todos os metadados incluídos nos [recursos de metadados do pacote](../../api/registration-base-url-resource.md) e muito mais.</span><span class="sxs-lookup"><span data-stu-id="0ffca-151">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="0ffca-152">É nesta etapa que sua lógica personalizada é implementada.</span><span class="sxs-lookup"><span data-stu-id="0ffca-152">This step is where you implement your custom logic.</span></span> <span data-ttu-id="0ffca-153">As outras etapas neste guia são implementadas praticamente da mesma forma, independentemente do que você está fazendo com as folhas de catálogo.</span><span class="sxs-lookup"><span data-stu-id="0ffca-153">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="0ffca-154">Baixar o .nupkg</span><span class="sxs-lookup"><span data-stu-id="0ffca-154">Downloading the .nupkg</span></span>

<span data-ttu-id="0ffca-155">Se você estiver interessado em baixar o .nupkg para pacotes encontrado no catálogo, utilize o [recurso de conteúdo do pacote](../../api/package-base-address-resource.md).</span><span class="sxs-lookup"><span data-stu-id="0ffca-155">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="0ffca-156">No entanto, observe que há um breve atraso entre quando um pacote é encontrado no catálogo e quando ele está disponível no recurso de conteúdo do pacote.</span><span class="sxs-lookup"><span data-stu-id="0ffca-156">However, note that there is a short delay between when a package is found in catalog and when it is available in the package content resource.</span></span> <span data-ttu-id="0ffca-157">Portanto, se você encontrar `404 Not Found` ao tentar baixar um .nupkg para um pacote encontrado no catálogo, basta tentar novamente um pouco mais tarde.</span><span class="sxs-lookup"><span data-stu-id="0ffca-157">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="0ffca-158">A correção desse atraso é acompanhada pelo problema do GitHub [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span><span class="sxs-lookup"><span data-stu-id="0ffca-158">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="0ffca-159">Mover o cursor para frente</span><span class="sxs-lookup"><span data-stu-id="0ffca-159">Move the cursor forward</span></span>

<span data-ttu-id="0ffca-160">Depois de você ter processado com êxito os itens de catálogo, será necessário determinar o novo valor de cursor a ser salvo.</span><span class="sxs-lookup"><span data-stu-id="0ffca-160">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="0ffca-161">Para fazer isso, localize o `commitTimeStamp` máximo (mais recentes em ordem cronológica) de todos os itens de catálogo que você processou.</span><span class="sxs-lookup"><span data-stu-id="0ffca-161">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="0ffca-162">Este é o novo valor do cursor.</span><span class="sxs-lookup"><span data-stu-id="0ffca-162">This is your new cursor value.</span></span> <span data-ttu-id="0ffca-163">Salve-o em um repositório permanente, como um banco de dados, sistema de arquivos ou armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="0ffca-163">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="0ffca-164">Quando você desejar obter mais itens de catálogo, basta iniciar da [primeira etapa](#initialize-a-cursor) inicializando o valor do cursor desse repositório persistente.</span><span class="sxs-lookup"><span data-stu-id="0ffca-164">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="0ffca-165">Se seu aplicativo gerar uma exceção ou falhas, não mova o cursor para a frente.</span><span class="sxs-lookup"><span data-stu-id="0ffca-165">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="0ffca-166">Mover o cursor para a frente significa nunca precisar processar itens de catálogo novamente antes do cursor.</span><span class="sxs-lookup"><span data-stu-id="0ffca-166">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="0ffca-167">Se, por algum motivo, você tiver um bug no modo de processamento de catálogo, basta simplesmente mover o cursor para trás no tempo e permitir que seu código reprocesse os itens antigos do catálogo.</span><span class="sxs-lookup"><span data-stu-id="0ffca-167">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="0ffca-168">Código de exemplo C#</span><span class="sxs-lookup"><span data-stu-id="0ffca-168">C# sample code</span></span>

<span data-ttu-id="0ffca-169">Como o catálogo é um conjunto de documentos JSON disponíveis por HTTP, é possível interagir com ele usando qualquer linguagem de programação que tenha um cliente HTTP e um desserializador JSON.</span><span class="sxs-lookup"><span data-stu-id="0ffca-169">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="0ffca-170">Exemplos de C# estão disponíveis no [repositório do NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="0ffca-170">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="0ffca-171">SDK do Catálogo</span><span class="sxs-lookup"><span data-stu-id="0ffca-171">Catalog SDK</span></span>

<span data-ttu-id="0ffca-172">A maneira mais fácil de consumir o catálogo é usar o pacote do SDK do catálogo de pré-lançamento .NET: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span><span class="sxs-lookup"><span data-stu-id="0ffca-172">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span></span>
<span data-ttu-id="0ffca-173">Este pacote está disponível no feed `nuget-build` MyGet, para o qual você usa a URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json` de origem do pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="0ffca-173">This package is available on the `nuget-build` MyGet feed, for which you use the NuGet package source URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span></span>

<span data-ttu-id="0ffca-174">Você pode instalar esse pacote em um projeto compatível com `netstandard1.3` ou superior (como o .NET Framework 4.6).</span><span class="sxs-lookup"><span data-stu-id="0ffca-174">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="0ffca-175">Um exemplo que usa este pacote está disponível no GitHub no [projeto NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span><span class="sxs-lookup"><span data-stu-id="0ffca-175">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="0ffca-176">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="0ffca-176">Sample output</span></span>

```
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

### <a name="minimal-sample"></a><span data-ttu-id="0ffca-177">Exemplo mínimo</span><span class="sxs-lookup"><span data-stu-id="0ffca-177">Minimal sample</span></span>

<span data-ttu-id="0ffca-178">Para ver um exemplo com menos dependências que ilustra a interação com o catálogo em mais detalhes, consulte o [projeto de exemplo CatalogReaderExample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="0ffca-178">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span>
<span data-ttu-id="0ffca-179">Os projeto é voltado para `netcoreapp2.0` e depende do [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (para resolver o índice de serviço) e [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (para desserialização JSON).</span><span class="sxs-lookup"><span data-stu-id="0ffca-179">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="0ffca-180">A lógica principal do código pode ser vista no [arquivo Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="0ffca-180">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="0ffca-181">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="0ffca-181">Sample output</span></span>

```
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
