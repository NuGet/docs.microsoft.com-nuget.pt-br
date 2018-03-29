---
title: Comando de lista do NuGet CLI | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referência para o comando de lista de nuget.exe
keywords: referência de lista do NuGet, comando de pacotes de lista
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 61ad02eb99d6c56968c38841498df8aa9f74159d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="8e886-104">comando Listar (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8e886-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="8e886-105">**Aplica-se a:** consumo de pacote, a publicação &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="8e886-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8e886-106">Exibe uma lista de pacotes de uma origem específica.</span><span class="sxs-lookup"><span data-stu-id="8e886-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="8e886-107">Se nenhuma fonte for especificada, todas as fontes definidas no arquivo de configuração global, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config`, são usados.</span><span class="sxs-lookup"><span data-stu-id="8e886-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="8e886-108">Se `NuGet.Config` não especifica nenhuma fonte, em seguida, `list` usa o feed padrão (nuget.org).</span><span class="sxs-lookup"><span data-stu-id="8e886-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="8e886-109">Uso</span><span class="sxs-lookup"><span data-stu-id="8e886-109">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="8e886-110">onde os termos de pesquisa opcional filtra a lista exibida.</span><span class="sxs-lookup"><span data-stu-id="8e886-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="8e886-111">Termos de pesquisa são aplicados para os nomes dos pacotes, marcas e descrições de pacote como elas são quando usá-los em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8e886-111">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="8e886-112">Opções</span><span class="sxs-lookup"><span data-stu-id="8e886-112">Options</span></span>

| <span data-ttu-id="8e886-113">Opção</span><span class="sxs-lookup"><span data-stu-id="8e886-113">Option</span></span> | <span data-ttu-id="8e886-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="8e886-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8e886-115">Todasas versões</span><span class="sxs-lookup"><span data-stu-id="8e886-115">AllVersions</span></span> | <span data-ttu-id="8e886-116">Lista todas as versões de um pacote.</span><span class="sxs-lookup"><span data-stu-id="8e886-116">List all versions of a package.</span></span> <span data-ttu-id="8e886-117">Por padrão, somente a versão mais recente do pacote é exibida.</span><span class="sxs-lookup"><span data-stu-id="8e886-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="8e886-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8e886-118">ConfigFile</span></span> | <span data-ttu-id="8e886-119">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="8e886-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8e886-120">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="8e886-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8e886-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8e886-121">ForceEnglishOutput</span></span> | <span data-ttu-id="8e886-122">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="8e886-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8e886-123">Ajuda</span><span class="sxs-lookup"><span data-stu-id="8e886-123">Help</span></span> | <span data-ttu-id="8e886-124">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="8e886-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="8e886-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="8e886-125">IncludeDelisted</span></span> | <span data-ttu-id="8e886-126">*(3.2 +)*  Exibir pacotes não listados.</span><span class="sxs-lookup"><span data-stu-id="8e886-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="8e886-127">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8e886-127">NonInteractive</span></span> | <span data-ttu-id="8e886-128">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="8e886-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8e886-129">Versão de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="8e886-129">PreRelease</span></span> | <span data-ttu-id="8e886-130">Inclui pacotes pré-lançados na lista.</span><span class="sxs-lookup"><span data-stu-id="8e886-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="8e886-131">Origem</span><span class="sxs-lookup"><span data-stu-id="8e886-131">Source</span></span> | <span data-ttu-id="8e886-132">Especifica uma lista de fontes de pacotes para pesquisar.</span><span class="sxs-lookup"><span data-stu-id="8e886-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="8e886-133">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="8e886-133">Verbosity</span></span> | <span data-ttu-id="8e886-134">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="8e886-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8e886-135">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8e886-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8e886-136">Exemplos</span><span class="sxs-lookup"><span data-stu-id="8e886-136">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
