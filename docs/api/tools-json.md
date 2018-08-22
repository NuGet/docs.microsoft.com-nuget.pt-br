---
title: Tools.JSON para descobrir as versões nuget.exe
description: O ponto de extremidade
author: jver
ms.author: jver
manager: skofman
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d11e79cd9109e1760189e848e35ff322be026a4d
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/21/2018
ms.locfileid: "40247645"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="c5f38-103">Tools.JSON para descobrir as versões nuget.exe</span><span class="sxs-lookup"><span data-stu-id="c5f38-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="c5f38-104">Atualmente, há algumas maneiras de obter a versão mais recente do nuget.exe em seu computador de forma programável por script.</span><span class="sxs-lookup"><span data-stu-id="c5f38-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="c5f38-105">Por exemplo, você pode baixar e extrair os [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) pacote em nuget.org. Isso tem alguma complexidade, pois ele exige que você já tenha nuget.exe (para `nuget.exe install`) ou você tem que descompactar o. nupkg usando uma ferramenta de descompactação básica e localizar os binário dentro.</span><span class="sxs-lookup"><span data-stu-id="c5f38-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="c5f38-106">Se você já tiver nuget.exe, você também pode usar `nuget.exe update -self`, no entanto, isso também requer que uma cópia existente do nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="c5f38-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="c5f38-107">Essa abordagem também atualiza a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="c5f38-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="c5f38-108">Ele não permite o uso de uma versão específica.</span><span class="sxs-lookup"><span data-stu-id="c5f38-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="c5f38-109">O `tools.json` ponto de extremidade está disponível para ambos resolve o problema de inicialização e oferecer controle da versão do nuget.exe que você baixar.</span><span class="sxs-lookup"><span data-stu-id="c5f38-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="c5f38-110">Isso pode ser usado em ambientes de CI/CD ou em scripts personalizados para descobrir e baixar qualquer versão de lançamento do nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="c5f38-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="c5f38-111">O `tools.json` ponto de extremidade pode ser obtido usando uma solicitação HTTP não autenticada (por exemplo, `Invoke-WebRequest` no PowerShell ou `wget`).</span><span class="sxs-lookup"><span data-stu-id="c5f38-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="c5f38-112">Pode ser analisada usando um desserializador JSON e download nuget.exe subsequentes que URLs também podem ser buscadas usando não autenticado a solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="c5f38-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="c5f38-113">O ponto de extremidade pode ser buscado usando o `GET` método:</span><span class="sxs-lookup"><span data-stu-id="c5f38-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="c5f38-114">O [esquema JSON](http://json-schema.org/) para o ponto de extremidade está disponível aqui:</span><span class="sxs-lookup"><span data-stu-id="c5f38-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="c5f38-115">Resposta</span><span class="sxs-lookup"><span data-stu-id="c5f38-115">Response</span></span>

<span data-ttu-id="c5f38-116">A resposta é um documento JSON que contém todas as versões disponíveis do nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="c5f38-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="c5f38-117">O objeto JSON de raiz tem a seguinte propriedade:</span><span class="sxs-lookup"><span data-stu-id="c5f38-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="c5f38-118">Nome</span><span class="sxs-lookup"><span data-stu-id="c5f38-118">Name</span></span>      | <span data-ttu-id="c5f38-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="c5f38-119">Type</span></span>             | <span data-ttu-id="c5f38-120">Necessária</span><span class="sxs-lookup"><span data-stu-id="c5f38-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="c5f38-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="c5f38-121">nuget.exe</span></span> | <span data-ttu-id="c5f38-122">matriz de objetos</span><span class="sxs-lookup"><span data-stu-id="c5f38-122">array of objects</span></span> | <span data-ttu-id="c5f38-123">sim</span><span class="sxs-lookup"><span data-stu-id="c5f38-123">yes</span></span>

<span data-ttu-id="c5f38-124">Cada objeto no `nuget.exe` matriz tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="c5f38-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="c5f38-125">Nome</span><span class="sxs-lookup"><span data-stu-id="c5f38-125">Name</span></span>     | <span data-ttu-id="c5f38-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="c5f38-126">Type</span></span>   | <span data-ttu-id="c5f38-127">Necessária</span><span class="sxs-lookup"><span data-stu-id="c5f38-127">Required</span></span> | <span data-ttu-id="c5f38-128">Observações</span><span class="sxs-lookup"><span data-stu-id="c5f38-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="c5f38-129">version</span><span class="sxs-lookup"><span data-stu-id="c5f38-129">version</span></span>  | <span data-ttu-id="c5f38-130">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="c5f38-130">string</span></span> | <span data-ttu-id="c5f38-131">sim</span><span class="sxs-lookup"><span data-stu-id="c5f38-131">yes</span></span>      | <span data-ttu-id="c5f38-132">Uma cadeia de caracteres SemVer 2.0.0</span><span class="sxs-lookup"><span data-stu-id="c5f38-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="c5f38-133">url</span><span class="sxs-lookup"><span data-stu-id="c5f38-133">url</span></span>      | <span data-ttu-id="c5f38-134">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="c5f38-134">string</span></span> | <span data-ttu-id="c5f38-135">sim</span><span class="sxs-lookup"><span data-stu-id="c5f38-135">yes</span></span>      | <span data-ttu-id="c5f38-136">Uma URL absoluta para baixar essa versão do nuget.exe</span><span class="sxs-lookup"><span data-stu-id="c5f38-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="c5f38-137">estágio</span><span class="sxs-lookup"><span data-stu-id="c5f38-137">stage</span></span>    | <span data-ttu-id="c5f38-138">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="c5f38-138">string</span></span> | <span data-ttu-id="c5f38-139">sim</span><span class="sxs-lookup"><span data-stu-id="c5f38-139">yes</span></span>      | <span data-ttu-id="c5f38-140">Uma cadeia de caracteres de enum</span><span class="sxs-lookup"><span data-stu-id="c5f38-140">An enum string</span></span>
<span data-ttu-id="c5f38-141">carregado</span><span class="sxs-lookup"><span data-stu-id="c5f38-141">uploaded</span></span> | <span data-ttu-id="c5f38-142">cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="c5f38-142">string</span></span> | <span data-ttu-id="c5f38-143">sim</span><span class="sxs-lookup"><span data-stu-id="c5f38-143">yes</span></span>      | <span data-ttu-id="c5f38-144">Um carimbo de hora aproximado de quando a versão foi disponibilizada</span><span class="sxs-lookup"><span data-stu-id="c5f38-144">An approximate timestamp of when the version was made available</span></span>

<span data-ttu-id="c5f38-145">Os itens na matriz serão classificados em ordem decrescente de, SemVer 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="c5f38-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="c5f38-146">Essa garantia é destinada a aliviar a carga em um cliente procurando a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="c5f38-146">This guarantee is meant to ease the burden on a client looking for the latest version.</span></span> 

<span data-ttu-id="c5f38-147">O `stage` propriedade indica como vettect esta versão da ferramenta.</span><span class="sxs-lookup"><span data-stu-id="c5f38-147">The `stage` property indicates how vettect this version of the tool is.</span></span> 

<span data-ttu-id="c5f38-148">Estágio</span><span class="sxs-lookup"><span data-stu-id="c5f38-148">Stage</span></span>              | <span data-ttu-id="c5f38-149">Significado</span><span class="sxs-lookup"><span data-stu-id="c5f38-149">Meaning</span></span>
------------------ | ------
<span data-ttu-id="c5f38-150">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="c5f38-150">EarlyAccessPreview</span></span> | <span data-ttu-id="c5f38-151">Ainda não estiver visível na [baixar a página da web](https://www.nuget.org/downloads) e devem ser validados por parceiros</span><span class="sxs-lookup"><span data-stu-id="c5f38-151">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="c5f38-152">Liberado</span><span class="sxs-lookup"><span data-stu-id="c5f38-152">Released</span></span>           | <span data-ttu-id="c5f38-153">Disponível no site de download, mas ainda não tiver sido recomendado para consumo ampla</span><span class="sxs-lookup"><span data-stu-id="c5f38-153">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="c5f38-154">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="c5f38-154">ReleasedAndBlessed</span></span> | <span data-ttu-id="c5f38-155">Disponível no site de download e é recomendado para consumo</span><span class="sxs-lookup"><span data-stu-id="c5f38-155">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="c5f38-156">Uma abordagem simples para ter a versão mais recente, versão recomendada é tirar a primeira versão na lista que tem o `stage` valor de `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="c5f38-156">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span>

<span data-ttu-id="c5f38-157">O `NuGet.CommandLine` pacote em nuget.org normalmente é atualizada apenas com `ReleasedAndBlessed` versões.</span><span class="sxs-lookup"><span data-stu-id="c5f38-157">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="c5f38-158">Exemplo de solicitação</span><span class="sxs-lookup"><span data-stu-id="c5f38-158">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="c5f38-159">Resposta de exemplo</span><span class="sxs-lookup"><span data-stu-id="c5f38-159">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
