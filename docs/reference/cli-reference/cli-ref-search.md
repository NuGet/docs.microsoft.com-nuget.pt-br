---
title: Comando de pesquisa da CLI do NuGet
description: Referência para o comando nuget.exe Search
author: advay26
ms.author: t-adtand
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 35e4906960534299418cb2a17c190476708b2634
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623262"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="6ed3f-103">comando Search (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6ed3f-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="6ed3f-104">**Aplica-se a:** &bullet; **versões com suporte** do consumo de pacotes: 5.8 +</span><span class="sxs-lookup"><span data-stu-id="6ed3f-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="6ed3f-105">Pesquisa uma determinada fonte usando a cadeia de caracteres de consulta fornecida.</span><span class="sxs-lookup"><span data-stu-id="6ed3f-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="6ed3f-106">Se nenhuma fonte for especificada, todas as fontes definidas em% AppData% \NuGet\NuGet.config serão usadas.</span><span class="sxs-lookup"><span data-stu-id="6ed3f-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="6ed3f-107">Uso</span><span class="sxs-lookup"><span data-stu-id="6ed3f-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="6ed3f-108">onde os termos de pesquisa são aplicados aos nomes de pacotes, marcas e descrições de pacote, assim como são quando eles são usado em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="6ed3f-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="6ed3f-109">Opções</span><span class="sxs-lookup"><span data-stu-id="6ed3f-109">Options</span></span>

| <span data-ttu-id="6ed3f-110">Nome</span><span class="sxs-lookup"><span data-stu-id="6ed3f-110">Name</span></span> | <span data-ttu-id="6ed3f-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ed3f-111">Description</span></span> | <span data-ttu-id="6ed3f-112">Uso</span><span class="sxs-lookup"><span data-stu-id="6ed3f-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="6ed3f-113">Pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="6ed3f-113">PreRelease</span></span> | <span data-ttu-id="6ed3f-114">Os pacotes de pré-lançamento não são incluídos por padrão, mas podem ser incluídos usando esse argumento</span><span class="sxs-lookup"><span data-stu-id="6ed3f-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="6ed3f-115">-Pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="6ed3f-115">-PreRelease</span></span> |
| <span data-ttu-id="6ed3f-116">Fonte</span><span class="sxs-lookup"><span data-stu-id="6ed3f-116">Source</span></span> | <span data-ttu-id="6ed3f-117">Origem (s) de pacote específico para pesquisar em vez de consultar as fontes padrão no __nuget.config__</span><span class="sxs-lookup"><span data-stu-id="6ed3f-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="6ed3f-118">-Origem `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="6ed3f-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="6ed3f-119">Take</span><span class="sxs-lookup"><span data-stu-id="6ed3f-119">Take</span></span> | <span data-ttu-id="6ed3f-120">O número de resultados a serem retornados.</span><span class="sxs-lookup"><span data-stu-id="6ed3f-120">The number of results to return.</span></span> <span data-ttu-id="6ed3f-121">O valor padrão é 20.</span><span class="sxs-lookup"><span data-stu-id="6ed3f-121">The default value is 20.</span></span> | <span data-ttu-id="6ed3f-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="6ed3f-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="6ed3f-123">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="6ed3f-123">Verbosity</span></span> | <span data-ttu-id="6ed3f-124">O nível de detalhe a ser exibido na saída.</span><span class="sxs-lookup"><span data-stu-id="6ed3f-124">The level of detail to display in the output.</span></span> <span data-ttu-id="6ed3f-125">O padrão é _normal_.</span><span class="sxs-lookup"><span data-stu-id="6ed3f-125">The default is _normal_.</span></span> <span data-ttu-id="6ed3f-126">(Consulte a observação abaixo)</span><span class="sxs-lookup"><span data-stu-id="6ed3f-126">(See the note below)</span></span>  | <span data-ttu-id="6ed3f-127">-Detalhes `<quiet\|normal\|detailed>`</span><span class="sxs-lookup"><span data-stu-id="6ed3f-127">-Verbosity `<quiet\|normal\|detailed>`</span></span> |
| <span data-ttu-id="6ed3f-128">Ajuda</span><span class="sxs-lookup"><span data-stu-id="6ed3f-128">Help</span></span> | <span data-ttu-id="6ed3f-129">Exibe informações de ajuda para o comando</span><span class="sxs-lookup"><span data-stu-id="6ed3f-129">Displays help information for the command</span></span> | <span data-ttu-id="6ed3f-130">-Ajuda</span><span class="sxs-lookup"><span data-stu-id="6ed3f-130">-Help</span></span> |

<span data-ttu-id="6ed3f-131">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6ed3f-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

<span data-ttu-id="6ed3f-132">__OBSERVAÇÃO__</span><span class="sxs-lookup"><span data-stu-id="6ed3f-132">__NOTE__</span></span>

<span data-ttu-id="6ed3f-133">Níveis de detalhamento:</span><span class="sxs-lookup"><span data-stu-id="6ed3f-133">Verbosity Levels:</span></span>

* <span data-ttu-id="6ed3f-134">_Quiet_ -ID do pacote, versão</span><span class="sxs-lookup"><span data-stu-id="6ed3f-134">_quiet_ - Package ID, Version</span></span>
* <span data-ttu-id="6ed3f-135">_normal_ -ID do pacote, versão, downloads, visualização da descrição</span><span class="sxs-lookup"><span data-stu-id="6ed3f-135">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
* <span data-ttu-id="6ed3f-136">_detalhado_ -ID do pacote, versão, downloads, descrição completa, outras informações, como a URL de consulta</span><span class="sxs-lookup"><span data-stu-id="6ed3f-136">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="6ed3f-137">Exemplos</span><span class="sxs-lookup"><span data-stu-id="6ed3f-137">Examples</span></span>

<span data-ttu-id="6ed3f-138">Pesquisar pacotes relacionados ao *log*de fontes padrão:</span><span class="sxs-lookup"><span data-stu-id="6ed3f-138">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="6ed3f-139">Pesquise pacotes relacionados ao *registro em log*com detalhes detalhados:</span><span class="sxs-lookup"><span data-stu-id="6ed3f-139">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="6ed3f-140">Pesquise pacotes relacionados ao *registro em log*e mostre apenas os 5 principais resultados:</span><span class="sxs-lookup"><span data-stu-id="6ed3f-140">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="6ed3f-141">Pesquisar pacotes relacionados a *JSON*, incluindo versões de pré-lançamento, de origem/feed especificado:</span><span class="sxs-lookup"><span data-stu-id="6ed3f-141">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="6ed3f-142">Pesquisar pacotes relacionados a *JSON*de várias fontes/feeds:</span><span class="sxs-lookup"><span data-stu-id="6ed3f-142">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
