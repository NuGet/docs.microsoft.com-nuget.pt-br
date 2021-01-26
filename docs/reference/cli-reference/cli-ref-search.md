---
title: Comando de pesquisa da CLI do NuGet
description: Referência para o comando nuget.exe Search
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 6f4adcdf3981e5ec0e5e88337a8c3bcdd9158ca3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779164"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="955d4-103">comando Search (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="955d4-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="955d4-104">**Aplica-se a:** &bullet; **versões com suporte** do consumo de pacotes: 5.8 +</span><span class="sxs-lookup"><span data-stu-id="955d4-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="955d4-105">Pesquisa uma determinada fonte usando a cadeia de caracteres de consulta fornecida.</span><span class="sxs-lookup"><span data-stu-id="955d4-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="955d4-106">Se nenhuma fonte for especificada, todas as fontes definidas em% AppData% \NuGet\NuGet.config serão usadas.</span><span class="sxs-lookup"><span data-stu-id="955d4-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="955d4-107">Uso</span><span class="sxs-lookup"><span data-stu-id="955d4-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="955d4-108">onde os termos de pesquisa são aplicados aos nomes de pacotes, marcas e descrições de pacote, assim como são quando eles são usado em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="955d4-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="955d4-109">Opções</span><span class="sxs-lookup"><span data-stu-id="955d4-109">Options</span></span>

| <span data-ttu-id="955d4-110">Nome</span><span class="sxs-lookup"><span data-stu-id="955d4-110">Name</span></span> | <span data-ttu-id="955d4-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="955d4-111">Description</span></span> | <span data-ttu-id="955d4-112">Uso</span><span class="sxs-lookup"><span data-stu-id="955d4-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="955d4-113">Pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="955d4-113">PreRelease</span></span> | <span data-ttu-id="955d4-114">Os pacotes de pré-lançamento não são incluídos por padrão, mas podem ser incluídos usando esse argumento</span><span class="sxs-lookup"><span data-stu-id="955d4-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="955d4-115">-Pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="955d4-115">-PreRelease</span></span> |
| <span data-ttu-id="955d4-116">Fonte</span><span class="sxs-lookup"><span data-stu-id="955d4-116">Source</span></span> | <span data-ttu-id="955d4-117">Origem (s) de pacote específico para pesquisar em vez de consultar as fontes padrão no __nuget.config__</span><span class="sxs-lookup"><span data-stu-id="955d4-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="955d4-118">-Origem `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="955d4-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="955d4-119">Take</span><span class="sxs-lookup"><span data-stu-id="955d4-119">Take</span></span> | <span data-ttu-id="955d4-120">O número de resultados a serem retornados.</span><span class="sxs-lookup"><span data-stu-id="955d4-120">The number of results to return.</span></span> <span data-ttu-id="955d4-121">O valor padrão é 20.</span><span class="sxs-lookup"><span data-stu-id="955d4-121">The default value is 20.</span></span> | <span data-ttu-id="955d4-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="955d4-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="955d4-123">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="955d4-123">Verbosity</span></span> | <span data-ttu-id="955d4-124">O nível de detalhe a ser exibido na saída.</span><span class="sxs-lookup"><span data-stu-id="955d4-124">The level of detail to display in the output.</span></span> <span data-ttu-id="955d4-125">O padrão é _normal_.</span><span class="sxs-lookup"><span data-stu-id="955d4-125">The default is _normal_.</span></span> <span data-ttu-id="955d4-126">(Consulte a observação abaixo)</span><span class="sxs-lookup"><span data-stu-id="955d4-126">(See the note below)</span></span>  | <span data-ttu-id="955d4-127">-Detalhes `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="955d4-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="955d4-128">Ajuda</span><span class="sxs-lookup"><span data-stu-id="955d4-128">Help</span></span> | <span data-ttu-id="955d4-129">Exibe informações de ajuda para o comando</span><span class="sxs-lookup"><span data-stu-id="955d4-129">Displays help information for the command</span></span> | <span data-ttu-id="955d4-130">-Ajuda</span><span class="sxs-lookup"><span data-stu-id="955d4-130">-Help</span></span> |

<span data-ttu-id="955d4-131">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="955d4-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="955d4-132">Níveis de detalhamento:</span><span class="sxs-lookup"><span data-stu-id="955d4-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="955d4-133">_Quiet_ -ID do pacote, versão</span><span class="sxs-lookup"><span data-stu-id="955d4-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="955d4-134">_normal_ -ID do pacote, versão, downloads, visualização da descrição</span><span class="sxs-lookup"><span data-stu-id="955d4-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="955d4-135">_detalhado_ -ID do pacote, versão, downloads, descrição completa, outras informações, como a URL de consulta</span><span class="sxs-lookup"><span data-stu-id="955d4-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="955d4-136">Exemplos</span><span class="sxs-lookup"><span data-stu-id="955d4-136">Examples</span></span>

<span data-ttu-id="955d4-137">Pesquisar pacotes relacionados ao *log* de fontes padrão:</span><span class="sxs-lookup"><span data-stu-id="955d4-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="955d4-138">Pesquise pacotes relacionados ao *registro em log* com detalhes detalhados:</span><span class="sxs-lookup"><span data-stu-id="955d4-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="955d4-139">Pesquise pacotes relacionados ao *registro em log* e mostre apenas os 5 principais resultados:</span><span class="sxs-lookup"><span data-stu-id="955d4-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="955d4-140">Pesquisar pacotes relacionados a *JSON*, incluindo versões de pré-lançamento, de origem/feed especificado:</span><span class="sxs-lookup"><span data-stu-id="955d4-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="955d4-141">Pesquisar pacotes relacionados a *JSON* de várias fontes/feeds:</span><span class="sxs-lookup"><span data-stu-id="955d4-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
