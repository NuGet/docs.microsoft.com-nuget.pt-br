---
title: Comando de pesquisa da CLI do NuGet
description: Referência para o comando nuget.exe search
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323655"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="2b25b-103">comando search (CLI do NuGet)</span><span class="sxs-lookup"><span data-stu-id="2b25b-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="2b25b-104">**Aplica-se a:** consumo de pacote &bullet; **Versões com suporte:** 5.8+</span><span class="sxs-lookup"><span data-stu-id="2b25b-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="2b25b-105">Pesquisa uma determinada fonte usando a cadeia de caracteres de consulta fornecida.</span><span class="sxs-lookup"><span data-stu-id="2b25b-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="2b25b-106">Se nenhuma fonte for especificada, todas as fontes definidas em %AppData%\NuGet\NuGet.Config serão usadas.</span><span class="sxs-lookup"><span data-stu-id="2b25b-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.Config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="2b25b-107">Uso</span><span class="sxs-lookup"><span data-stu-id="2b25b-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="2b25b-108">em que os termos de pesquisa são aplicados aos nomes de pacotes, marcas e descrições do pacote, assim como são ao usá-los no nuget.org.</span><span class="sxs-lookup"><span data-stu-id="2b25b-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="2b25b-109">Opções</span><span class="sxs-lookup"><span data-stu-id="2b25b-109">Options</span></span>

| <span data-ttu-id="2b25b-110">Nome</span><span class="sxs-lookup"><span data-stu-id="2b25b-110">Name</span></span> | <span data-ttu-id="2b25b-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="2b25b-111">Description</span></span> | <span data-ttu-id="2b25b-112">Uso</span><span class="sxs-lookup"><span data-stu-id="2b25b-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="2b25b-113">Pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="2b25b-113">PreRelease</span></span> | <span data-ttu-id="2b25b-114">Os pacotes de pré-lançamento não são incluídos por padrão, mas podem ser incluídos usando esse argumento</span><span class="sxs-lookup"><span data-stu-id="2b25b-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="2b25b-115">-PreRelease</span><span class="sxs-lookup"><span data-stu-id="2b25b-115">-PreRelease</span></span> |
| <span data-ttu-id="2b25b-116">Fonte</span><span class="sxs-lookup"><span data-stu-id="2b25b-116">Source</span></span> | <span data-ttu-id="2b25b-117">Origem(s) de pacote específica a ser pesquisada em vez de consultar as fontes padrão no __nuget.config__</span><span class="sxs-lookup"><span data-stu-id="2b25b-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="2b25b-118">-Source `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="2b25b-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="2b25b-119">Take</span><span class="sxs-lookup"><span data-stu-id="2b25b-119">Take</span></span> | <span data-ttu-id="2b25b-120">O número de resultados a retornar.</span><span class="sxs-lookup"><span data-stu-id="2b25b-120">The number of results to return.</span></span> <span data-ttu-id="2b25b-121">O valor padrão é 20.</span><span class="sxs-lookup"><span data-stu-id="2b25b-121">The default value is 20.</span></span> | <span data-ttu-id="2b25b-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="2b25b-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="2b25b-123">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="2b25b-123">Verbosity</span></span> | <span data-ttu-id="2b25b-124">O nível de detalhes a ser exibido na saída.</span><span class="sxs-lookup"><span data-stu-id="2b25b-124">The level of detail to display in the output.</span></span> <span data-ttu-id="2b25b-125">O padrão é _normal._</span><span class="sxs-lookup"><span data-stu-id="2b25b-125">The default is _normal_.</span></span> <span data-ttu-id="2b25b-126">(Veja a observação abaixo)</span><span class="sxs-lookup"><span data-stu-id="2b25b-126">(See the note below)</span></span>  | <span data-ttu-id="2b25b-127">-Verbosity `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="2b25b-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="2b25b-128">Ajuda</span><span class="sxs-lookup"><span data-stu-id="2b25b-128">Help</span></span> | <span data-ttu-id="2b25b-129">Exibe informações de ajuda para o comando</span><span class="sxs-lookup"><span data-stu-id="2b25b-129">Displays help information for the command</span></span> | <span data-ttu-id="2b25b-130">-Help</span><span class="sxs-lookup"><span data-stu-id="2b25b-130">-Help</span></span> |

<span data-ttu-id="2b25b-131">Consulte também [Variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2b25b-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="2b25b-132">Níveis de detalhes:</span><span class="sxs-lookup"><span data-stu-id="2b25b-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="2b25b-133">_quiet_ – ID do pacote, versão</span><span class="sxs-lookup"><span data-stu-id="2b25b-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="2b25b-134">_normal_ – ID do pacote, versão, downloads, visualização da descrição</span><span class="sxs-lookup"><span data-stu-id="2b25b-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="2b25b-135">_detalhado –_ ID do pacote, versão, downloads, descrição completa, outras informações, como a URL da consulta</span><span class="sxs-lookup"><span data-stu-id="2b25b-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="2b25b-136">Exemplos</span><span class="sxs-lookup"><span data-stu-id="2b25b-136">Examples</span></span>

<span data-ttu-id="2b25b-137">Pesquise *pacotes* relacionados ao registro em log de fontes padrão:</span><span class="sxs-lookup"><span data-stu-id="2b25b-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="2b25b-138">*Pesquise pacotes* relacionados ao registro em log com detalhamento detalhado:</span><span class="sxs-lookup"><span data-stu-id="2b25b-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="2b25b-139">*Pesquise pacotes* relacionados ao registro em log e mostre apenas os cinco principais resultados:</span><span class="sxs-lookup"><span data-stu-id="2b25b-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="2b25b-140">Pesquise pacotes relacionados a *JSON,* incluindo versões de pré-lançamento, do feed/origem especificado:</span><span class="sxs-lookup"><span data-stu-id="2b25b-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="2b25b-141">Pesquise pacotes relacionados a *JSON* de várias fontes/feeds:</span><span class="sxs-lookup"><span data-stu-id="2b25b-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
