---
title: tools.json para descobrir nuget.exe versões
description: O ponto de extremidade para
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773816"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="bcc32-103">tools.json para descobrir nuget.exe versões</span><span class="sxs-lookup"><span data-stu-id="bcc32-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="bcc32-104">Hoje, há algumas maneiras de obter a versão mais recente do nuget.exe em seu computador de maneira programável.</span><span class="sxs-lookup"><span data-stu-id="bcc32-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="bcc32-105">Por exemplo, você pode baixar e extrair o [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) pacote do NuGet.org. Isso tem alguma complexidade, pois ela requer que você já tenha nuget.exe (para `nuget.exe install` ) ou precise descompactar o. nupkg usando uma ferramenta de descompactação básica e encontrar o binário interno.</span><span class="sxs-lookup"><span data-stu-id="bcc32-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="bcc32-106">Se você já tiver nuget.exe, também poderá usar `nuget.exe update -self` , mas isso também requer uma cópia existente do nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="bcc32-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="bcc32-107">Essa abordagem também o atualiza para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="bcc32-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="bcc32-108">Ele não permite o uso de uma versão específica.</span><span class="sxs-lookup"><span data-stu-id="bcc32-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="bcc32-109">O `tools.json` ponto de extremidade está disponível para resolver o problema de inicialização e para dar o controle da versão do nuget.exe que você baixa.</span><span class="sxs-lookup"><span data-stu-id="bcc32-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="bcc32-110">Isso pode ser usado em ambientes de CI/CD ou em scripts personalizados para descobrir e baixar qualquer versão de lançamento do nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="bcc32-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="bcc32-111">O `tools.json` ponto de extremidade pode ser obtido usando uma solicitação HTTP não autenticada (por exemplo, `Invoke-WebRequest` no PowerShell ou `wget` ).</span><span class="sxs-lookup"><span data-stu-id="bcc32-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="bcc32-112">Ele pode ser analisado usando um desserializador JSON e subseqüentes nuget.exe as URLs de download também podem ser buscadas usando solicitações HTTP não autenticadas.</span><span class="sxs-lookup"><span data-stu-id="bcc32-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="bcc32-113">O ponto de extremidade pode ser buscado usando o `GET` método:</span><span class="sxs-lookup"><span data-stu-id="bcc32-113">The endpoint can be fetched using the `GET` method:</span></span>

```
GET https://dist.nuget.org/tools.json
```

<span data-ttu-id="bcc32-114">O [esquema JSON](https://json-schema.org/) para o ponto de extremidade está disponível aqui:</span><span class="sxs-lookup"><span data-stu-id="bcc32-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a><span data-ttu-id="bcc32-115">Resposta</span><span class="sxs-lookup"><span data-stu-id="bcc32-115">Response</span></span>

<span data-ttu-id="bcc32-116">A resposta é um documento JSON que contém todas as versões disponíveis do nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="bcc32-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="bcc32-117">O objeto JSON raiz tem a seguinte propriedade:</span><span class="sxs-lookup"><span data-stu-id="bcc32-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="bcc32-118">Nome</span><span class="sxs-lookup"><span data-stu-id="bcc32-118">Name</span></span>      | <span data-ttu-id="bcc32-119">Type</span><span class="sxs-lookup"><span data-stu-id="bcc32-119">Type</span></span>             | <span data-ttu-id="bcc32-120">Necessária</span><span class="sxs-lookup"><span data-stu-id="bcc32-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="bcc32-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="bcc32-121">nuget.exe</span></span> | <span data-ttu-id="bcc32-122">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="bcc32-122">array of objects</span></span> | <span data-ttu-id="bcc32-123">sim</span><span class="sxs-lookup"><span data-stu-id="bcc32-123">yes</span></span>

<span data-ttu-id="bcc32-124">Cada objeto na `nuget.exe` matriz tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="bcc32-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="bcc32-125">Nome</span><span class="sxs-lookup"><span data-stu-id="bcc32-125">Name</span></span>     | <span data-ttu-id="bcc32-126">Type</span><span class="sxs-lookup"><span data-stu-id="bcc32-126">Type</span></span>   | <span data-ttu-id="bcc32-127">Necessária</span><span class="sxs-lookup"><span data-stu-id="bcc32-127">Required</span></span> | <span data-ttu-id="bcc32-128">Observações</span><span class="sxs-lookup"><span data-stu-id="bcc32-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="bcc32-129">version</span><span class="sxs-lookup"><span data-stu-id="bcc32-129">version</span></span>  | <span data-ttu-id="bcc32-130">string</span><span class="sxs-lookup"><span data-stu-id="bcc32-130">string</span></span> | <span data-ttu-id="bcc32-131">sim</span><span class="sxs-lookup"><span data-stu-id="bcc32-131">yes</span></span>      | <span data-ttu-id="bcc32-132">Uma cadeia de caracteres SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="bcc32-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="bcc32-133">url</span><span class="sxs-lookup"><span data-stu-id="bcc32-133">url</span></span>      | <span data-ttu-id="bcc32-134">string</span><span class="sxs-lookup"><span data-stu-id="bcc32-134">string</span></span> | <span data-ttu-id="bcc32-135">sim</span><span class="sxs-lookup"><span data-stu-id="bcc32-135">yes</span></span>      | <span data-ttu-id="bcc32-136">Uma URL absoluta para baixar esta versão do nuget.exe</span><span class="sxs-lookup"><span data-stu-id="bcc32-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="bcc32-137">preparar</span><span class="sxs-lookup"><span data-stu-id="bcc32-137">stage</span></span>    | <span data-ttu-id="bcc32-138">string</span><span class="sxs-lookup"><span data-stu-id="bcc32-138">string</span></span> | <span data-ttu-id="bcc32-139">sim</span><span class="sxs-lookup"><span data-stu-id="bcc32-139">yes</span></span>      | <span data-ttu-id="bcc32-140">Uma cadeia de caracteres de enumeração</span><span class="sxs-lookup"><span data-stu-id="bcc32-140">An enum string</span></span>
<span data-ttu-id="bcc32-141">atualizada</span><span class="sxs-lookup"><span data-stu-id="bcc32-141">uploaded</span></span> | <span data-ttu-id="bcc32-142">string</span><span class="sxs-lookup"><span data-stu-id="bcc32-142">string</span></span> | <span data-ttu-id="bcc32-143">sim</span><span class="sxs-lookup"><span data-stu-id="bcc32-143">yes</span></span>      | <span data-ttu-id="bcc32-144">Um carimbo de data/hora ISO 8601 aproximado de quando a versão foi disponibilizada</span><span class="sxs-lookup"><span data-stu-id="bcc32-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="bcc32-145">Os itens na matriz serão classificados em ordem decrescente, SemVer 2.0.0 Order.</span><span class="sxs-lookup"><span data-stu-id="bcc32-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="bcc32-146">Essa garantia destina-se a reduzir a carga de um cliente que está interessado no número de versão mais alto.</span><span class="sxs-lookup"><span data-stu-id="bcc32-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="bcc32-147">No entanto, isso significa que a lista não está classificada em ordem cronológica.</span><span class="sxs-lookup"><span data-stu-id="bcc32-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="bcc32-148">Por exemplo, se uma versão principal inferior for atendida em uma data posterior à versão principal mais alta, essa versão de serviço não aparecerá na parte superior da lista.</span><span class="sxs-lookup"><span data-stu-id="bcc32-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="bcc32-149">Se você quiser que a versão mais recente seja liberada pelo *carimbo de data/hora*, basta classificar a matriz pela `uploaded` cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="bcc32-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="bcc32-150">Isso funciona porque o `uploaded` carimbo de data/hora está no formato [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) , que pode ser classificado cronologicamente usando uma classificação lexicográfica (ou seja, uma classificação de cadeia de caracteres simples).</span><span class="sxs-lookup"><span data-stu-id="bcc32-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="bcc32-151">A `stage` propriedade indica como verificados esta versão da ferramenta é.</span><span class="sxs-lookup"><span data-stu-id="bcc32-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="bcc32-152">Estágio</span><span class="sxs-lookup"><span data-stu-id="bcc32-152">Stage</span></span>              | <span data-ttu-id="bcc32-153">Significado</span><span class="sxs-lookup"><span data-stu-id="bcc32-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="bcc32-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="bcc32-154">EarlyAccessPreview</span></span> | <span data-ttu-id="bcc32-155">Ainda não está visível na [página de download da Web](https://www.nuget.org/downloads) e deve ser validada pelos parceiros</span><span class="sxs-lookup"><span data-stu-id="bcc32-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="bcc32-156">Liberado</span><span class="sxs-lookup"><span data-stu-id="bcc32-156">Released</span></span>           | <span data-ttu-id="bcc32-157">Disponível no site de download, mas ainda não é recomendado para consumo de larga propagação</span><span class="sxs-lookup"><span data-stu-id="bcc32-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="bcc32-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="bcc32-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="bcc32-159">Disponível no site de download e é recomendado para consumo</span><span class="sxs-lookup"><span data-stu-id="bcc32-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="bcc32-160">Uma abordagem simples para ter a versão mais recente e recomendada é usar a primeira versão na lista com o `stage` valor de `ReleasedAndBlessed` .</span><span class="sxs-lookup"><span data-stu-id="bcc32-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="bcc32-161">Isso funciona porque as versões são classificadas em SemVer 2.0.0 Order.</span><span class="sxs-lookup"><span data-stu-id="bcc32-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="bcc32-162">O `NuGet.CommandLine` pacote em NuGet.org normalmente é atualizado apenas com `ReleasedAndBlessed` versões.</span><span class="sxs-lookup"><span data-stu-id="bcc32-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="bcc32-163">Solicitação de exemplo</span><span class="sxs-lookup"><span data-stu-id="bcc32-163">Sample request</span></span>

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a><span data-ttu-id="bcc32-164">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="bcc32-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
