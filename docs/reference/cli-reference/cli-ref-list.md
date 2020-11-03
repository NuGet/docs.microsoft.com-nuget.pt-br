---
title: Comando de lista da CLI do NuGet
description: Referência para o comando de lista de nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a6a4ee434c43ad4865dba12f039b5d545a90d3c4
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238160"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="89ba8-103">comando List (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="89ba8-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="89ba8-104">**Aplica-se a:** consumo de pacote, &bullet; **versões com suporte para publicação:** todos</span><span class="sxs-lookup"><span data-stu-id="89ba8-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="89ba8-105">Exibe uma lista de pacotes de uma determinada origem.</span><span class="sxs-lookup"><span data-stu-id="89ba8-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="89ba8-106">Se nenhuma fonte for especificada, todas as fontes definidas no arquivo de configuração global, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` , serão usadas.</span><span class="sxs-lookup"><span data-stu-id="89ba8-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="89ba8-107">Se `NuGet.Config` não especificar nenhuma fonte, `list` o usará o feed padrão (NuGet.org).</span><span class="sxs-lookup"><span data-stu-id="89ba8-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="89ba8-108">Uso</span><span class="sxs-lookup"><span data-stu-id="89ba8-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="89ba8-109">onde os termos de pesquisa opcionais filtrarão a lista exibida.</span><span class="sxs-lookup"><span data-stu-id="89ba8-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="89ba8-110">Os [termos de pesquisa](../../consume-packages/finding-and-choosing-packages.md#search-syntax) são aplicados aos nomes de pacotes, marcas e descrições de pacote da mesma forma que quando estão usando-os no NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="89ba8-110">[Search terms](../../consume-packages/finding-and-choosing-packages.md#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="89ba8-111">Opções</span><span class="sxs-lookup"><span data-stu-id="89ba8-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="89ba8-112">Listar todas as versões de um pacote.</span><span class="sxs-lookup"><span data-stu-id="89ba8-112">List all versions of a package.</span></span> <span data-ttu-id="89ba8-113">Por padrão, somente a versão mais recente do pacote é exibida.</span><span class="sxs-lookup"><span data-stu-id="89ba8-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="89ba8-114">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="89ba8-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="89ba8-115">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="89ba8-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="89ba8-116">*(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="89ba8-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="89ba8-117">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="89ba8-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="89ba8-118">*(3,2 +)* Exibir pacotes não listados.</span><span class="sxs-lookup"><span data-stu-id="89ba8-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="89ba8-119">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="89ba8-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="89ba8-120">Inclui pacotes de pré-lançamento na lista.</span><span class="sxs-lookup"><span data-stu-id="89ba8-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="89ba8-121">Especifica uma lista de fontes de pacotes a serem pesquisadas.</span><span class="sxs-lookup"><span data-stu-id="89ba8-121">Specifies a list of packages sources to search.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="89ba8-122">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="89ba8-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="89ba8-123">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="89ba8-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="89ba8-124">Exemplos</span><span class="sxs-lookup"><span data-stu-id="89ba8-124">Examples</span></span>

<span data-ttu-id="89ba8-125">Listar todos os pacotes de feeds configurados:</span><span class="sxs-lookup"><span data-stu-id="89ba8-125">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="89ba8-126">Listar pacotes relacionados ao Azure com detalhes detalhados:</span><span class="sxs-lookup"><span data-stu-id="89ba8-126">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="89ba8-127">Listar todas as versões de pacotes relacionados ao Azure de feeds configurados:</span><span class="sxs-lookup"><span data-stu-id="89ba8-127">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="89ba8-128">Listar todas as versões de pacotes relacionados ao JSON de origem/feed especificado:</span><span class="sxs-lookup"><span data-stu-id="89ba8-128">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="89ba8-129">Listar pacotes relacionados a JSON de várias fontes/feeds:</span><span class="sxs-lookup"><span data-stu-id="89ba8-129">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```