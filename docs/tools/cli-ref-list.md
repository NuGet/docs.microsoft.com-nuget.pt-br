---
title: Comando de lista de CLI do NuGet
description: Referência para o comando de lista de nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b0f144d8abbba7388fe39cd113e4eeddccbca2c6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818432"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="e557f-103">comando Listar (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e557f-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="e557f-104">**Aplica-se a:** consumo de pacote, a publicação &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="e557f-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="e557f-105">Exibe uma lista de pacotes de uma origem específica.</span><span class="sxs-lookup"><span data-stu-id="e557f-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="e557f-106">Se nenhuma fonte for especificada, todas as fontes definidas no arquivo de configuração global, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config`, são usados.</span><span class="sxs-lookup"><span data-stu-id="e557f-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="e557f-107">Se `NuGet.Config` não especifica nenhuma fonte, em seguida, `list` usa o feed padrão (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="e557f-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="e557f-108">Uso</span><span class="sxs-lookup"><span data-stu-id="e557f-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="e557f-109">onde os termos de pesquisa opcional filtra a lista exibida.</span><span class="sxs-lookup"><span data-stu-id="e557f-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="e557f-110">Termos de pesquisa são aplicados para os nomes dos pacotes, marcas e descrições de pacote como elas são quando usá-los em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e557f-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="e557f-111">Opções</span><span class="sxs-lookup"><span data-stu-id="e557f-111">Options</span></span>

| <span data-ttu-id="e557f-112">Opção</span><span class="sxs-lookup"><span data-stu-id="e557f-112">Option</span></span> | <span data-ttu-id="e557f-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="e557f-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e557f-114">Todasas versões</span><span class="sxs-lookup"><span data-stu-id="e557f-114">AllVersions</span></span> | <span data-ttu-id="e557f-115">Lista todas as versões de um pacote.</span><span class="sxs-lookup"><span data-stu-id="e557f-115">List all versions of a package.</span></span> <span data-ttu-id="e557f-116">Por padrão, somente a versão mais recente do pacote é exibida.</span><span class="sxs-lookup"><span data-stu-id="e557f-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="e557f-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e557f-117">ConfigFile</span></span> | <span data-ttu-id="e557f-118">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="e557f-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e557f-119">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="e557f-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e557f-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e557f-120">ForceEnglishOutput</span></span> | <span data-ttu-id="e557f-121">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="e557f-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e557f-122">Ajuda</span><span class="sxs-lookup"><span data-stu-id="e557f-122">Help</span></span> | <span data-ttu-id="e557f-123">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="e557f-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="e557f-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="e557f-124">IncludeDelisted</span></span> | <span data-ttu-id="e557f-125">*(3.2 +)*  Exibir pacotes não listados.</span><span class="sxs-lookup"><span data-stu-id="e557f-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="e557f-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="e557f-126">NonInteractive</span></span> | <span data-ttu-id="e557f-127">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="e557f-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e557f-128">Versão de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="e557f-128">PreRelease</span></span> | <span data-ttu-id="e557f-129">Inclui pacotes pré-lançados na lista.</span><span class="sxs-lookup"><span data-stu-id="e557f-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="e557f-130">Origem</span><span class="sxs-lookup"><span data-stu-id="e557f-130">Source</span></span> | <span data-ttu-id="e557f-131">Especifica uma lista de fontes de pacotes para pesquisar.</span><span class="sxs-lookup"><span data-stu-id="e557f-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="e557f-132">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="e557f-132">Verbosity</span></span> | <span data-ttu-id="e557f-133">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="e557f-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="e557f-134">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e557f-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e557f-135">Exemplos</span><span class="sxs-lookup"><span data-stu-id="e557f-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
