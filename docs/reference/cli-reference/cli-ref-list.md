---
title: Comando de lista da CLI do NuGet
description: Referência para o comando de lista NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813332"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="8acd9-103">comando List (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8acd9-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="8acd9-104">**Aplica-se a:** consumo de pacote, publicação &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="8acd9-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8acd9-105">Exibe uma lista de pacotes de uma determinada origem.</span><span class="sxs-lookup"><span data-stu-id="8acd9-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="8acd9-106">Se nenhuma fonte for especificada, todas as fontes definidas no arquivo de configuração global, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config`, serão usadas.</span><span class="sxs-lookup"><span data-stu-id="8acd9-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="8acd9-107">Se `NuGet.Config` não especificar nenhuma fonte, `list` usará o feed padrão (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="8acd9-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="8acd9-108">Medição de</span><span class="sxs-lookup"><span data-stu-id="8acd9-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="8acd9-109">onde os termos de pesquisa opcionais filtrarão a lista exibida.</span><span class="sxs-lookup"><span data-stu-id="8acd9-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="8acd9-110">Os termos de pesquisa são aplicados aos nomes de pacotes, marcas e descrições de pacote da mesma forma que quando estão usando-os no nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8acd9-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="8acd9-111">Opções</span><span class="sxs-lookup"><span data-stu-id="8acd9-111">Options</span></span>

| <span data-ttu-id="8acd9-112">Opção</span><span class="sxs-lookup"><span data-stu-id="8acd9-112">Option</span></span> | <span data-ttu-id="8acd9-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="8acd9-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8acd9-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="8acd9-114">AllVersions</span></span> | <span data-ttu-id="8acd9-115">Listar todas as versões de um pacote.</span><span class="sxs-lookup"><span data-stu-id="8acd9-115">List all versions of a package.</span></span> <span data-ttu-id="8acd9-116">Por padrão, somente a versão mais recente do pacote é exibida.</span><span class="sxs-lookup"><span data-stu-id="8acd9-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="8acd9-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8acd9-117">ConfigFile</span></span> | <span data-ttu-id="8acd9-118">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="8acd9-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8acd9-119">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="8acd9-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8acd9-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8acd9-120">ForceEnglishOutput</span></span> | <span data-ttu-id="8acd9-121">*(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="8acd9-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8acd9-122">Ajuda</span><span class="sxs-lookup"><span data-stu-id="8acd9-122">Help</span></span> | <span data-ttu-id="8acd9-123">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="8acd9-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="8acd9-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="8acd9-124">IncludeDelisted</span></span> | <span data-ttu-id="8acd9-125">*(3,2 +)* Exibir pacotes não listados.</span><span class="sxs-lookup"><span data-stu-id="8acd9-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="8acd9-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8acd9-126">NonInteractive</span></span> | <span data-ttu-id="8acd9-127">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="8acd9-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8acd9-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="8acd9-128">PreRelease</span></span> | <span data-ttu-id="8acd9-129">Inclui pacotes de pré-lançamento na lista.</span><span class="sxs-lookup"><span data-stu-id="8acd9-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="8acd9-130">Source</span><span class="sxs-lookup"><span data-stu-id="8acd9-130">Source</span></span> | <span data-ttu-id="8acd9-131">Especifica uma lista de fontes de pacotes a serem pesquisadas.</span><span class="sxs-lookup"><span data-stu-id="8acd9-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="8acd9-132">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="8acd9-132">Verbosity</span></span> | <span data-ttu-id="8acd9-133">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="8acd9-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8acd9-134">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8acd9-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8acd9-135">Exemplos</span><span class="sxs-lookup"><span data-stu-id="8acd9-135">Examples</span></span>

<span data-ttu-id="8acd9-136">Listar todos os pacotes de feeds configurados:</span><span class="sxs-lookup"><span data-stu-id="8acd9-136">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="8acd9-137">Listar pacotes relacionados ao Azure com detalhes detalhados:</span><span class="sxs-lookup"><span data-stu-id="8acd9-137">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="8acd9-138">Listar todas as versões de pacotes relacionados ao Azure de feeds configurados:</span><span class="sxs-lookup"><span data-stu-id="8acd9-138">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="8acd9-139">Listar todas as versões de pacotes relacionados ao JSON de origem/feed especificado:</span><span class="sxs-lookup"><span data-stu-id="8acd9-139">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="8acd9-140">Listar pacotes relacionados a JSON de várias fontes/feeds:</span><span class="sxs-lookup"><span data-stu-id="8acd9-140">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

