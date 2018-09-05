---
title: Tools.JSON para descobrir as versões nuget.exe
description: O ponto de extremidade
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 6184fe8e987e0637cb912999f2e3fa3a3dc9b4ba
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546929"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="eddde-103">Tools.JSON para descobrir as versões nuget.exe</span><span class="sxs-lookup"><span data-stu-id="eddde-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="eddde-104">Atualmente, há algumas maneiras de obter a versão mais recente do nuget.exe em seu computador de forma programável por script.</span><span class="sxs-lookup"><span data-stu-id="eddde-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="eddde-105">Por exemplo, você pode baixar e extrair os [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) pacote em nuget.org. Isso tem alguma complexidade, pois ele exige que você já tenha nuget.exe (para `nuget.exe install`) ou você tem que descompactar o. nupkg usando uma ferramenta de descompactação básica e localizar os binário dentro.</span><span class="sxs-lookup"><span data-stu-id="eddde-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="eddde-106">Se você já tiver nuget.exe, você também pode usar `nuget.exe update -self`, no entanto, isso também requer que uma cópia existente do nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="eddde-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="eddde-107">Essa abordagem também atualiza a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="eddde-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="eddde-108">Ele não permite o uso de uma versão específica.</span><span class="sxs-lookup"><span data-stu-id="eddde-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="eddde-109">O `tools.json` ponto de extremidade está disponível para ambos resolve o problema de inicialização e oferecer controle da versão do nuget.exe que você baixar.</span><span class="sxs-lookup"><span data-stu-id="eddde-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="eddde-110">Isso pode ser usado em ambientes de CI/CD ou em scripts personalizados para descobrir e baixar qualquer versão de lançamento do nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="eddde-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="eddde-111">O `tools.json` ponto de extremidade pode ser obtido usando uma solicitação HTTP não autenticada (por exemplo, `Invoke-WebRequest` no PowerShell ou `wget`).</span><span class="sxs-lookup"><span data-stu-id="eddde-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="eddde-112">Pode ser analisada usando um desserializador JSON e download nuget.exe subsequentes que URLs também podem ser buscadas usando não autenticado a solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="eddde-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="eddde-113">O ponto de extremidade pode ser buscado usando o `GET` método:</span><span class="sxs-lookup"><span data-stu-id="eddde-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="eddde-114">O [esquema JSON](http://json-schema.org/) para o ponto de extremidade está disponível aqui:</span><span class="sxs-lookup"><span data-stu-id="eddde-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="eddde-115">Resposta</span><span class="sxs-lookup"><span data-stu-id="eddde-115">Response</span></span>

<span data-ttu-id="eddde-116">A resposta é um documento JSON que contém todas as versões disponíveis do nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="eddde-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="eddde-117">O objeto JSON de raiz tem a seguinte propriedade:</span><span class="sxs-lookup"><span data-stu-id="eddde-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="eddde-118">Nome</span><span class="sxs-lookup"><span data-stu-id="eddde-118">Name</span></span>      | <span data-ttu-id="eddde-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="eddde-119">Type</span></span>             | <span data-ttu-id="eddde-120">Necessária</span><span class="sxs-lookup"><span data-stu-id="eddde-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="eddde-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="eddde-121">nuget.exe</span></span> | <span data-ttu-id="eddde-122">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="eddde-122">array of objects</span></span> | <span data-ttu-id="eddde-123">sim</span><span class="sxs-lookup"><span data-stu-id="eddde-123">yes</span></span>

<span data-ttu-id="eddde-124">Cada objeto no `nuget.exe` matriz tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="eddde-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="eddde-125">Nome</span><span class="sxs-lookup"><span data-stu-id="eddde-125">Name</span></span>     | <span data-ttu-id="eddde-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="eddde-126">Type</span></span>   | <span data-ttu-id="eddde-127">Necessária</span><span class="sxs-lookup"><span data-stu-id="eddde-127">Required</span></span> | <span data-ttu-id="eddde-128">Observações</span><span class="sxs-lookup"><span data-stu-id="eddde-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="eddde-129">version</span><span class="sxs-lookup"><span data-stu-id="eddde-129">version</span></span>  | <span data-ttu-id="eddde-130">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eddde-130">string</span></span> | <span data-ttu-id="eddde-131">sim</span><span class="sxs-lookup"><span data-stu-id="eddde-131">yes</span></span>      | <span data-ttu-id="eddde-132">Uma cadeia de caracteres SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="eddde-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="eddde-133">url</span><span class="sxs-lookup"><span data-stu-id="eddde-133">url</span></span>      | <span data-ttu-id="eddde-134">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eddde-134">string</span></span> | <span data-ttu-id="eddde-135">sim</span><span class="sxs-lookup"><span data-stu-id="eddde-135">yes</span></span>      | <span data-ttu-id="eddde-136">Uma URL absoluta para baixar essa versão do nuget.exe</span><span class="sxs-lookup"><span data-stu-id="eddde-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="eddde-137">estágio</span><span class="sxs-lookup"><span data-stu-id="eddde-137">stage</span></span>    | <span data-ttu-id="eddde-138">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eddde-138">string</span></span> | <span data-ttu-id="eddde-139">sim</span><span class="sxs-lookup"><span data-stu-id="eddde-139">yes</span></span>      | <span data-ttu-id="eddde-140">Uma cadeia de caracteres de enum</span><span class="sxs-lookup"><span data-stu-id="eddde-140">An enum string</span></span>
<span data-ttu-id="eddde-141">carregado</span><span class="sxs-lookup"><span data-stu-id="eddde-141">uploaded</span></span> | <span data-ttu-id="eddde-142">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="eddde-142">string</span></span> | <span data-ttu-id="eddde-143">sim</span><span class="sxs-lookup"><span data-stu-id="eddde-143">yes</span></span>      | <span data-ttu-id="eddde-144">Um carimbo de hora aproximado de quando a versão foi disponibilizada</span><span class="sxs-lookup"><span data-stu-id="eddde-144">An approximate timestamp of when the version was made available</span></span>

<span data-ttu-id="eddde-145">Os itens na matriz serão classificados em ordem decrescente de, SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="eddde-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="eddde-146">Essa garantia é destinada a aliviar a carga em um cliente procurando a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="eddde-146">This guarantee is meant to ease the burden on a client looking for the latest version.</span></span> 

<span data-ttu-id="eddde-147">O `stage` propriedade indica como vettect esta versão da ferramenta.</span><span class="sxs-lookup"><span data-stu-id="eddde-147">The `stage` property indicates how vettect this version of the tool is.</span></span> 

<span data-ttu-id="eddde-148">Estágio</span><span class="sxs-lookup"><span data-stu-id="eddde-148">Stage</span></span>              | <span data-ttu-id="eddde-149">Significado</span><span class="sxs-lookup"><span data-stu-id="eddde-149">Meaning</span></span>
------------------ | ------
<span data-ttu-id="eddde-150">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="eddde-150">EarlyAccessPreview</span></span> | <span data-ttu-id="eddde-151">Ainda não estiver visível na [baixar a página da web](https://www.nuget.org/downloads) e devem ser validados por parceiros</span><span class="sxs-lookup"><span data-stu-id="eddde-151">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="eddde-152">Liberado</span><span class="sxs-lookup"><span data-stu-id="eddde-152">Released</span></span>           | <span data-ttu-id="eddde-153">Disponível no site de download, mas ainda não tiver sido recomendado para consumo ampla</span><span class="sxs-lookup"><span data-stu-id="eddde-153">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="eddde-154">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="eddde-154">ReleasedAndBlessed</span></span> | <span data-ttu-id="eddde-155">Disponível no site de download e é recomendado para consumo</span><span class="sxs-lookup"><span data-stu-id="eddde-155">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="eddde-156">Uma abordagem simples para ter a versão mais recente, versão recomendada é tirar a primeira versão na lista que tem o `stage` valor de `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="eddde-156">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span>

<span data-ttu-id="eddde-157">O `NuGet.CommandLine` pacote em nuget.org normalmente é atualizada apenas com `ReleasedAndBlessed` versões.</span><span class="sxs-lookup"><span data-stu-id="eddde-157">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="eddde-158">Exemplo de solicitação</span><span class="sxs-lookup"><span data-stu-id="eddde-158">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="eddde-159">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="eddde-159">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
