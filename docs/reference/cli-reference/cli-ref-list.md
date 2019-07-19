---
title: Comando de lista da CLI do NuGet
description: Referência para o comando de lista NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327733"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="04f3a-103">comando List (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="04f3a-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="04f3a-104">**Aplica-se a:** consumo de &bullet; pacote, **versões com suporte para publicação:** todos</span><span class="sxs-lookup"><span data-stu-id="04f3a-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="04f3a-105">Exibe uma lista de pacotes de uma determinada origem.</span><span class="sxs-lookup"><span data-stu-id="04f3a-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="04f3a-106">Se nenhuma fonte for especificada, todas as fontes definidas no arquivo de configuração global `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config`ou, serão usadas.</span><span class="sxs-lookup"><span data-stu-id="04f3a-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="04f3a-107">Se `NuGet.Config` não especificar nenhuma fonte `list` , o usará o feed padrão (NuGet.org).</span><span class="sxs-lookup"><span data-stu-id="04f3a-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="04f3a-108">Uso</span><span class="sxs-lookup"><span data-stu-id="04f3a-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="04f3a-109">onde os termos de pesquisa opcionais filtrarão a lista exibida.</span><span class="sxs-lookup"><span data-stu-id="04f3a-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="04f3a-110">Os termos de pesquisa são aplicados aos nomes de pacotes, marcas e descrições de pacote da mesma forma que quando estão usando-os no nuget.org.</span><span class="sxs-lookup"><span data-stu-id="04f3a-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="04f3a-111">Opções</span><span class="sxs-lookup"><span data-stu-id="04f3a-111">Options</span></span>

| <span data-ttu-id="04f3a-112">Opção</span><span class="sxs-lookup"><span data-stu-id="04f3a-112">Option</span></span> | <span data-ttu-id="04f3a-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="04f3a-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="04f3a-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="04f3a-114">AllVersions</span></span> | <span data-ttu-id="04f3a-115">Listar todas as versões de um pacote.</span><span class="sxs-lookup"><span data-stu-id="04f3a-115">List all versions of a package.</span></span> <span data-ttu-id="04f3a-116">Por padrão, somente a versão mais recente do pacote é exibida.</span><span class="sxs-lookup"><span data-stu-id="04f3a-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="04f3a-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="04f3a-117">ConfigFile</span></span> | <span data-ttu-id="04f3a-118">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="04f3a-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="04f3a-119">Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="04f3a-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="04f3a-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="04f3a-120">ForceEnglishOutput</span></span> | <span data-ttu-id="04f3a-121">*(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="04f3a-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="04f3a-122">Help</span><span class="sxs-lookup"><span data-stu-id="04f3a-122">Help</span></span> | <span data-ttu-id="04f3a-123">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="04f3a-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="04f3a-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="04f3a-124">IncludeDelisted</span></span> | <span data-ttu-id="04f3a-125">*(3,2 +)* Exibir pacotes não listados.</span><span class="sxs-lookup"><span data-stu-id="04f3a-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="04f3a-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="04f3a-126">NonInteractive</span></span> | <span data-ttu-id="04f3a-127">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="04f3a-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="04f3a-128">Pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="04f3a-128">PreRelease</span></span> | <span data-ttu-id="04f3a-129">Inclui pacotes de pré-lançamento na lista.</span><span class="sxs-lookup"><span data-stu-id="04f3a-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="04f3a-130">Origem</span><span class="sxs-lookup"><span data-stu-id="04f3a-130">Source</span></span> | <span data-ttu-id="04f3a-131">Especifica uma lista de fontes de pacotes a serem pesquisadas.</span><span class="sxs-lookup"><span data-stu-id="04f3a-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="04f3a-132">Verbosity</span><span class="sxs-lookup"><span data-stu-id="04f3a-132">Verbosity</span></span> | <span data-ttu-id="04f3a-133">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="04f3a-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="04f3a-134">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="04f3a-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="04f3a-135">Exemplos</span><span class="sxs-lookup"><span data-stu-id="04f3a-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
