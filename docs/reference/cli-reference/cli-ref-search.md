---
title: Comando de pesquisa da CLI do NuGet
description: Referência para o comando nuget.exe Search
author: advay26
ms.author: t-adtand
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 8d63efefb8f14c03fbe3986d8d7eebcc3eb5bcac
ms.sourcegitcommit: 6cda91f135e58cf57a2471b0c7c4a2f748f40024
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "89359676"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="294cd-103">comando Search (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="294cd-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="294cd-104">**Aplica-se a:** &bullet; **versões com suporte** do consumo de pacotes: 5.8 +</span><span class="sxs-lookup"><span data-stu-id="294cd-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="294cd-105">Pesquisa uma determinada fonte usando a cadeia de caracteres de consulta fornecida.</span><span class="sxs-lookup"><span data-stu-id="294cd-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="294cd-106">Se nenhuma fonte for especificada, todas as fontes definidas em% AppData% \NuGet\NuGet.config serão usadas.</span><span class="sxs-lookup"><span data-stu-id="294cd-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="294cd-107">Uso</span><span class="sxs-lookup"><span data-stu-id="294cd-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="294cd-108">onde os termos de pesquisa são aplicados aos nomes de pacotes, marcas e descrições de pacote, assim como são quando eles são usado em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="294cd-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="294cd-109">Opções</span><span class="sxs-lookup"><span data-stu-id="294cd-109">Options</span></span>

| <span data-ttu-id="294cd-110">Nome</span><span class="sxs-lookup"><span data-stu-id="294cd-110">Name</span></span> | <span data-ttu-id="294cd-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="294cd-111">Description</span></span> | <span data-ttu-id="294cd-112">Uso</span><span class="sxs-lookup"><span data-stu-id="294cd-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="294cd-113">Pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="294cd-113">PreRelease</span></span> | <span data-ttu-id="294cd-114">Os pacotes de pré-lançamento não são incluídos por padrão, mas podem ser incluídos usando esse argumento</span><span class="sxs-lookup"><span data-stu-id="294cd-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="294cd-115">-Pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="294cd-115">-PreRelease</span></span> |
| <span data-ttu-id="294cd-116">Fonte</span><span class="sxs-lookup"><span data-stu-id="294cd-116">Source</span></span> | <span data-ttu-id="294cd-117">Origem (s) de pacote específico para pesquisar em vez de consultar as fontes padrão no __nuget.config__</span><span class="sxs-lookup"><span data-stu-id="294cd-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="294cd-118">-Origem `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="294cd-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="294cd-119">Take</span><span class="sxs-lookup"><span data-stu-id="294cd-119">Take</span></span> | <span data-ttu-id="294cd-120">O número de resultados a serem retornados.</span><span class="sxs-lookup"><span data-stu-id="294cd-120">The number of results to return.</span></span> <span data-ttu-id="294cd-121">O valor padrão é 20.</span><span class="sxs-lookup"><span data-stu-id="294cd-121">The default value is 20.</span></span> | <span data-ttu-id="294cd-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="294cd-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="294cd-123">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="294cd-123">Verbosity</span></span> | <span data-ttu-id="294cd-124">O nível de detalhe a ser exibido na saída.</span><span class="sxs-lookup"><span data-stu-id="294cd-124">The level of detail to display in the output.</span></span> <span data-ttu-id="294cd-125">O padrão é _normal_.</span><span class="sxs-lookup"><span data-stu-id="294cd-125">The default is _normal_.</span></span> <span data-ttu-id="294cd-126">(Consulte a observação abaixo)</span><span class="sxs-lookup"><span data-stu-id="294cd-126">(See the note below)</span></span>  | <span data-ttu-id="294cd-127">-Detalhes `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="294cd-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="294cd-128">Ajuda</span><span class="sxs-lookup"><span data-stu-id="294cd-128">Help</span></span> | <span data-ttu-id="294cd-129">Exibe informações de ajuda para o comando</span><span class="sxs-lookup"><span data-stu-id="294cd-129">Displays help information for the command</span></span> | <span data-ttu-id="294cd-130">-Ajuda</span><span class="sxs-lookup"><span data-stu-id="294cd-130">-Help</span></span> |

<span data-ttu-id="294cd-131">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="294cd-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="294cd-132">Níveis de detalhamento:</span><span class="sxs-lookup"><span data-stu-id="294cd-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="294cd-133">_Quiet_ -ID do pacote, versão</span><span class="sxs-lookup"><span data-stu-id="294cd-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="294cd-134">_normal_ -ID do pacote, versão, downloads, visualização da descrição</span><span class="sxs-lookup"><span data-stu-id="294cd-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="294cd-135">_detalhado_ -ID do pacote, versão, downloads, descrição completa, outras informações, como a URL de consulta</span><span class="sxs-lookup"><span data-stu-id="294cd-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="294cd-136">Exemplos</span><span class="sxs-lookup"><span data-stu-id="294cd-136">Examples</span></span>

<span data-ttu-id="294cd-137">Pesquisar pacotes relacionados ao *log*de fontes padrão:</span><span class="sxs-lookup"><span data-stu-id="294cd-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="294cd-138">Pesquise pacotes relacionados ao *registro em log*com detalhes detalhados:</span><span class="sxs-lookup"><span data-stu-id="294cd-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="294cd-139">Pesquise pacotes relacionados ao *registro em log*e mostre apenas os 5 principais resultados:</span><span class="sxs-lookup"><span data-stu-id="294cd-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="294cd-140">Pesquisar pacotes relacionados a *JSON*, incluindo versões de pré-lançamento, de origem/feed especificado:</span><span class="sxs-lookup"><span data-stu-id="294cd-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="294cd-141">Pesquisar pacotes relacionados a *JSON*de várias fontes/feeds:</span><span class="sxs-lookup"><span data-stu-id="294cd-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
