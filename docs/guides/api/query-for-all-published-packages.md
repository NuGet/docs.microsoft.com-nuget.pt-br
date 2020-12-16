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
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="215e2-103">Consulta para todos os pacotes publicados em nuget.org</span><span class="sxs-lookup"><span data-stu-id="215e2-103">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="215e2-104">Um padrão de consulta comum na API OData V2 herdada estava enumerando todos os pacotes publicados em nuget.org, ordenados por quando o pacote foi publicado.</span><span class="sxs-lookup"><span data-stu-id="215e2-104">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="215e2-105">Cenários que exigem esse tipo de consulta em nuget.org variam muito:</span><span class="sxs-lookup"><span data-stu-id="215e2-105">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="215e2-106">Replicando o nuget.org totalmente</span><span class="sxs-lookup"><span data-stu-id="215e2-106">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="215e2-107">Detectar o lançamento de novas versões dos pacotes</span><span class="sxs-lookup"><span data-stu-id="215e2-107">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="215e2-108">Localizando os pacotes que dependem do seu pacote</span><span class="sxs-lookup"><span data-stu-id="215e2-108">Finding packages that depend on your package</span></span>

<span data-ttu-id="215e2-109">O modo herdado de fazer isso normalmente depende da classificação da entidade de pacote de OData por um carimbo de data/hora e a paginação em um enorme conjunto de resultados usando os parâmetros `skip` e `top` (tamanho da página).</span><span class="sxs-lookup"><span data-stu-id="215e2-109">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="215e2-110">Infelizmente, essa abordagem traz algumas desvantagens:</span><span class="sxs-lookup"><span data-stu-id="215e2-110">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="215e2-111">Possibilidade de pacotes ausentes, pois as consultas estão sendo feitas em dados que geralmente têm a ordem alterada</span><span class="sxs-lookup"><span data-stu-id="215e2-111">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="215e2-112">Tempo de resposta de consulta lento porque as consultas não são otimizadas (as consultas mais otimizadas são aquelas compatíveis com um cenário principal para o cliente do NuGet oficial)</span><span class="sxs-lookup"><span data-stu-id="215e2-112">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="215e2-113">Uso de API preterida e não documentada, o que significa que não há garantia de suporte para tais consultas no futuro</span><span class="sxs-lookup"><span data-stu-id="215e2-113">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="215e2-114">Incapacidade de reproduzir o histórico na ordem exata em que ele ocorreu</span><span class="sxs-lookup"><span data-stu-id="215e2-114">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="215e2-115">Por esse motivo, o guia a seguir pode ser seguido para resolver os cenários mencionados acima de maneira mais confiável e pronta para o futuro.</span><span class="sxs-lookup"><span data-stu-id="215e2-115">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="215e2-116">Visão geral</span><span class="sxs-lookup"><span data-stu-id="215e2-116">Overview</span></span>

<span data-ttu-id="215e2-117">No centro deste guia está o recurso na [API do NuGet](../../api/overview.md) chamado de **catálogo**.</span><span class="sxs-lookup"><span data-stu-id="215e2-117">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="215e2-118">O catálogo é uma API somente de acréscimo que permite que o chamador Veja um histórico completo de pacotes adicionados a, modificados e excluídos do nuget.org. Se você estiver interessado em todos ou mesmo em um subconjunto de pacotes publicados no nuget.org, o catálogo é uma ótima maneira de se manter atualizado com o conjunto de pacotes disponíveis no momento, à medida que o tempo continua.</span><span class="sxs-lookup"><span data-stu-id="215e2-118">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="215e2-119">Este guia busca ser uma explicação passo a passo de alto nível, mas se você estiver interessado nos detalhes refinados do catálogo, consulte o [Documento de referência de API](../../api/catalog-resource.md).</span><span class="sxs-lookup"><span data-stu-id="215e2-119">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="215e2-120">As etapas a seguir podem ser implementadas em qualquer linguagem de programação de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="215e2-120">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="215e2-121">Se você quiser um exemplo completo de execução, examine o [exemplo de C#](#c-sample-code) mencionado abaixo.</span><span class="sxs-lookup"><span data-stu-id="215e2-121">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="215e2-122">Caso contrário, siga o guia abaixo para compilar um leitor de catálogo confiável.</span><span class="sxs-lookup"><span data-stu-id="215e2-122">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="215e2-123">Inicializar um cursor</span><span class="sxs-lookup"><span data-stu-id="215e2-123">Initialize a cursor</span></span>

<span data-ttu-id="215e2-124">A primeira etapa na compilação de um leitor de catálogo confiável é a implementação de um cursor.</span><span class="sxs-lookup"><span data-stu-id="215e2-124">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="215e2-125">Para ver detalhes completos sobre o design de um cursor de catálogo, consulte o [documento de referência do catálogo](../../api/catalog-resource.md#cursor).</span><span class="sxs-lookup"><span data-stu-id="215e2-125">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="215e2-126">Em resumo, o cursor é um ponto no tempo até o momento em que você processou eventos no catálogo.</span><span class="sxs-lookup"><span data-stu-id="215e2-126">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="215e2-127">Eventos no catálogo representam publicações de pacote e outras alterações de pacote.</span><span class="sxs-lookup"><span data-stu-id="215e2-127">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="215e2-128">Se você tem interesse em todos os pacotes já publicados no NuGet (desde o início dos tempos), inicialize seu cursor para um carimbo de data/hora de “valor mínimo” (por exemplo, `DateTime.MinValue` no .NET).</span><span class="sxs-lookup"><span data-stu-id="215e2-128">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="215e2-129">Se você tem interesse apenas nos pacotes publicados a partir de agora, use o carimbo de data/hora atual como o valor inicial do cursor.</span><span class="sxs-lookup"><span data-stu-id="215e2-129">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="215e2-130">Para este guia, inicializaremos nosso cursor para um carimbo de data/hora de uma hora atrás.</span><span class="sxs-lookup"><span data-stu-id="215e2-130">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="215e2-131">Por enquanto, memorize esse carimbo de data/hora.</span><span class="sxs-lookup"><span data-stu-id="215e2-131">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="215e2-132">Determinar a URL do índice do catálogo</span><span class="sxs-lookup"><span data-stu-id="215e2-132">Determine catalog index URL</span></span>

<span data-ttu-id="215e2-133">A localização de cada recurso (ponto de extremidade) na API do NuGet deve ser descoberta usando o [índice de serviço](../../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="215e2-133">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="215e2-134">Como este guia se concentra no nuget.org, usaremos o índice de serviço do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="215e2-134">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

    GET https://api.nuget.org/v3/index.json

<span data-ttu-id="215e2-135">O documento de serviço é um documento JSON que contém todos os recursos em nuget.org. Procure o recurso que tem o `@type` valor da propriedade de `Catalog/3.0.0` .</span><span class="sxs-lookup"><span data-stu-id="215e2-135">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="215e2-136">O valor da propriedade `@id` associado é a URL para o próprio índice do catálogo.</span><span class="sxs-lookup"><span data-stu-id="215e2-136">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="215e2-137">Localizar novas folhas de catálogo</span><span class="sxs-lookup"><span data-stu-id="215e2-137">Find new catalog leaves</span></span>

<span data-ttu-id="215e2-138">Usando o valor da propriedade `@id` na etapa anterior, baixe o índice do catálogo:</span><span class="sxs-lookup"><span data-stu-id="215e2-138">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

    GET https://api.nuget.org/v3/catalog0/index.json

<span data-ttu-id="215e2-139">Desserialize o [índice do catálogo](../../api/catalog-resource.md#catalog-index).</span><span class="sxs-lookup"><span data-stu-id="215e2-139">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="215e2-140">Filtre todos os [objetos de página de catálogo](../../api/catalog-resource.md#catalog-page-object-in-the-index) com `commitTimeStamp` menor ou igual ao valor atual do cursor.</span><span class="sxs-lookup"><span data-stu-id="215e2-140">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="215e2-141">Para cada página de catálogo restante, baixe o documento completo usando a propriedade `@id`.</span><span class="sxs-lookup"><span data-stu-id="215e2-141">For each remaining catalog page, download the full document using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/page2926.json

<span data-ttu-id="215e2-142">Desserialize a [página do catálogo](../../api/catalog-resource.md#catalog-page).</span><span class="sxs-lookup"><span data-stu-id="215e2-142">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="215e2-143">Filtre todos os [objetos de folha de catálogo](../../api/catalog-resource.md#catalog-item-object-in-a-page) com `commitTimeStamp` menor ou igual ao seu valor atual do cursor.</span><span class="sxs-lookup"><span data-stu-id="215e2-143">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="215e2-144">Depois de baixar todas as páginas de catálogo não filtradas, você terá um conjunto de objetos de folha de catálogo que representam os pacotes que foram publicados, não listados, listados ou excluídos no período entre o carimbo de data/hora do cursor e o momento atual.</span><span class="sxs-lookup"><span data-stu-id="215e2-144">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="215e2-145">Processar folhas de catálogo</span><span class="sxs-lookup"><span data-stu-id="215e2-145">Process catalog leaves</span></span>

<span data-ttu-id="215e2-146">Neste ponto, você pode executar qualquer processamento personalizado que desejar nos itens de catálogo.</span><span class="sxs-lookup"><span data-stu-id="215e2-146">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="215e2-147">Se tudo o que você precisa é a ID e a versão do pacote, é possível inspecionar as propriedades `nuget:id` e `nuget:version` nos objetos de itens do catálogo encontrados nas páginas.</span><span class="sxs-lookup"><span data-stu-id="215e2-147">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="215e2-148">Examine a propriedade `@type` para saber se o item de catálogo se refere a um pacote existente ou um pacote excluído.</span><span class="sxs-lookup"><span data-stu-id="215e2-148">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="215e2-149">Se você estiver interessado nos metadados sobre o pacote (como a descrição, dependências, tamanho do .nupkg, etc), busque o [documento de folha de catálogo](../../api/catalog-resource.md#catalog-leaf) usando a propriedade `@id`.</span><span class="sxs-lookup"><span data-stu-id="215e2-149">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

<span data-ttu-id="215e2-150">Este documento contém todos os metadados incluídos nos [recursos de metadados do pacote](../../api/registration-base-url-resource.md) e muito mais.</span><span class="sxs-lookup"><span data-stu-id="215e2-150">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="215e2-151">É nesta etapa que sua lógica personalizada é implementada.</span><span class="sxs-lookup"><span data-stu-id="215e2-151">This step is where you implement your custom logic.</span></span> <span data-ttu-id="215e2-152">As outras etapas neste guia são implementadas praticamente da mesma forma, independentemente do que você está fazendo com as folhas de catálogo.</span><span class="sxs-lookup"><span data-stu-id="215e2-152">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="215e2-153">Baixar o .nupkg</span><span class="sxs-lookup"><span data-stu-id="215e2-153">Downloading the .nupkg</span></span>

<span data-ttu-id="215e2-154">Se você estiver interessado em baixar o .nupkg para pacotes encontrado no catálogo, utilize o [recurso de conteúdo do pacote](../../api/package-base-address-resource.md).</span><span class="sxs-lookup"><span data-stu-id="215e2-154">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="215e2-155">No entanto, observe que há um breve atraso entre quando um pacote é encontrado no catálogo e quando ele está disponível no recurso de conteúdo do pacote.</span><span class="sxs-lookup"><span data-stu-id="215e2-155">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="215e2-156">Portanto, se você encontrar `404 Not Found` ao tentar baixar um .nupkg para um pacote encontrado no catálogo, basta tentar novamente um pouco mais tarde.</span><span class="sxs-lookup"><span data-stu-id="215e2-156">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="215e2-157">A correção desse atraso é acompanhada pelo problema do GitHub [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span><span class="sxs-lookup"><span data-stu-id="215e2-157">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="215e2-158">Mover o cursor para frente</span><span class="sxs-lookup"><span data-stu-id="215e2-158">Move the cursor forward</span></span>

<span data-ttu-id="215e2-159">Depois de você ter processado com êxito os itens de catálogo, será necessário determinar o novo valor de cursor a ser salvo.</span><span class="sxs-lookup"><span data-stu-id="215e2-159">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="215e2-160">Para fazer isso, localize o `commitTimeStamp` máximo (mais recentes em ordem cronológica) de todos os itens de catálogo que você processou.</span><span class="sxs-lookup"><span data-stu-id="215e2-160">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="215e2-161">Este é o novo valor do cursor.</span><span class="sxs-lookup"><span data-stu-id="215e2-161">This is your new cursor value.</span></span> <span data-ttu-id="215e2-162">Salve-o em um repositório permanente, como um banco de dados, sistema de arquivos ou armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="215e2-162">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="215e2-163">Quando você desejar obter mais itens de catálogo, basta iniciar da [primeira etapa](#initialize-a-cursor) inicializando o valor do cursor desse repositório persistente.</span><span class="sxs-lookup"><span data-stu-id="215e2-163">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="215e2-164">Se seu aplicativo gerar uma exceção ou falhas, não mova o cursor para a frente.</span><span class="sxs-lookup"><span data-stu-id="215e2-164">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="215e2-165">Mover o cursor para a frente significa nunca precisar processar itens de catálogo novamente antes do cursor.</span><span class="sxs-lookup"><span data-stu-id="215e2-165">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="215e2-166">Se, por algum motivo, você tiver um bug no modo de processamento de catálogo, basta simplesmente mover o cursor para trás no tempo e permitir que seu código reprocesse os itens antigos do catálogo.</span><span class="sxs-lookup"><span data-stu-id="215e2-166">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="215e2-167">Código de exemplo C#</span><span class="sxs-lookup"><span data-stu-id="215e2-167">C# sample code</span></span>

<span data-ttu-id="215e2-168">Como o catálogo é um conjunto de documentos JSON disponíveis por HTTP, é possível interagir com ele usando qualquer linguagem de programação que tenha um cliente HTTP e um desserializador JSON.</span><span class="sxs-lookup"><span data-stu-id="215e2-168">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="215e2-169">Exemplos de C# estão disponíveis no [repositório do NuGet/Samples](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="215e2-169">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="215e2-170">SDK do Catálogo</span><span class="sxs-lookup"><span data-stu-id="215e2-170">Catalog SDK</span></span>

<span data-ttu-id="215e2-171">A maneira mais fácil de consumir o catálogo é usar o pacote de pré-lançamento do SDK do catálogo do .NET `NuGet.Protocol.Catalog` , que está disponível em Azure Artifacts usando a seguinte URL de origem do pacote NuGet: `https://pkgs.dev.azure.com/dnceng/public/_packaging/nuget-build/nuget/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="215e2-171">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package `NuGet.Protocol.Catalog`, which is available on Azure Artifacts using the following NuGet package source URL: `https://pkgs.dev.azure.com/dnceng/public/_packaging/nuget-build/nuget/v3/index.json`.</span></span>

<span data-ttu-id="215e2-172">Você pode instalar esse pacote em um projeto compatível com `netstandard1.3` ou superior (como o .NET Framework 4.6).</span><span class="sxs-lookup"><span data-stu-id="215e2-172">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="215e2-173">Um exemplo que usa este pacote está disponível no GitHub no [projeto NuGet.Protocol.Catalog.Sample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span><span class="sxs-lookup"><span data-stu-id="215e2-173">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="215e2-174">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="215e2-174">Sample output</span></span>

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

### <a name="minimal-sample"></a><span data-ttu-id="215e2-175">Exemplo mínimo</span><span class="sxs-lookup"><span data-stu-id="215e2-175">Minimal sample</span></span>

<span data-ttu-id="215e2-176">Para ver um exemplo com menos dependências que ilustra a interação com o catálogo em mais detalhes, consulte o [projeto de exemplo CatalogReaderExample](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span><span class="sxs-lookup"><span data-stu-id="215e2-176">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="215e2-177">Os projeto é voltado para `netcoreapp2.0` e depende do [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (para resolver o índice de serviço) e [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (para desserialização JSON).</span><span class="sxs-lookup"><span data-stu-id="215e2-177">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="215e2-178">A lógica principal do código pode ser vista no [arquivo Program.cs](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="215e2-178">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="215e2-179">Saída de exemplo</span><span class="sxs-lookup"><span data-stu-id="215e2-179">Sample output</span></span>

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
