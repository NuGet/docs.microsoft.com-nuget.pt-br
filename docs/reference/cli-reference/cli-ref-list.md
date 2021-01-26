---
title: Comando de lista da CLI do NuGet
description: Referência para o comando de lista de nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 55ccf0d86ad6df8001e7401d430ec29cd7a154c3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780056"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="a7b2b-103">comando List (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a7b2b-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="a7b2b-104">**Aplica-se a:** consumo de pacote, &bullet; **versões com suporte para publicação:** todos</span><span class="sxs-lookup"><span data-stu-id="a7b2b-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a7b2b-105">Exibe uma lista de pacotes de uma determinada origem.</span><span class="sxs-lookup"><span data-stu-id="a7b2b-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="a7b2b-106">Se nenhuma fonte for especificada, todas as fontes definidas no arquivo de configuração global, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` , serão usadas.</span><span class="sxs-lookup"><span data-stu-id="a7b2b-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="a7b2b-107">Se `NuGet.Config` não especificar nenhuma fonte, `list` o usará o feed padrão (NuGet.org).</span><span class="sxs-lookup"><span data-stu-id="a7b2b-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="a7b2b-108">Uso</span><span class="sxs-lookup"><span data-stu-id="a7b2b-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="a7b2b-109">onde os termos de pesquisa opcionais filtrarão a lista exibida.</span><span class="sxs-lookup"><span data-stu-id="a7b2b-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="a7b2b-110">Os [termos de pesquisa](../../consume-packages/finding-and-choosing-packages.md#search-syntax) são aplicados aos nomes de pacotes, marcas e descrições de pacote da mesma forma que quando estão usando-os no NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="a7b2b-110">[Search terms](../../consume-packages/finding-and-choosing-packages.md#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="a7b2b-111">Opções</span><span class="sxs-lookup"><span data-stu-id="a7b2b-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="a7b2b-112">Listar todas as versões de um pacote.</span><span class="sxs-lookup"><span data-stu-id="a7b2b-112">List all versions of a package.</span></span> <span data-ttu-id="a7b2b-113">Por padrão, somente a versão mais recente do pacote é exibida.</span><span class="sxs-lookup"><span data-stu-id="a7b2b-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="a7b2b-114">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="a7b2b-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a7b2b-115">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="a7b2b-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="a7b2b-116">*(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="a7b2b-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a7b2b-117">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="a7b2b-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="a7b2b-118">*(3,2 +)* Exibir pacotes não listados.</span><span class="sxs-lookup"><span data-stu-id="a7b2b-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a7b2b-119">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="a7b2b-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="a7b2b-120">Inclui pacotes de pré-lançamento na lista.</span><span class="sxs-lookup"><span data-stu-id="a7b2b-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="a7b2b-121">A origem do pacote a ser pesquisado.</span><span class="sxs-lookup"><span data-stu-id="a7b2b-121">The package source to search.</span></span> <span data-ttu-id="a7b2b-122">Você pode especificar várias fontes usando a `-Source` opção várias vezes.</span><span class="sxs-lookup"><span data-stu-id="a7b2b-122">You can specify multiple sources by using the `-Source` option multiple times.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a7b2b-123">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="a7b2b-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="a7b2b-124">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a7b2b-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a7b2b-125">Exemplos</span><span class="sxs-lookup"><span data-stu-id="a7b2b-125">Examples</span></span>

<span data-ttu-id="a7b2b-126">Listar todos os pacotes de feeds configurados:</span><span class="sxs-lookup"><span data-stu-id="a7b2b-126">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="a7b2b-127">Listar pacotes relacionados ao Azure com detalhes detalhados:</span><span class="sxs-lookup"><span data-stu-id="a7b2b-127">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="a7b2b-128">Listar todas as versões de pacotes relacionados ao Azure de feeds configurados:</span><span class="sxs-lookup"><span data-stu-id="a7b2b-128">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="a7b2b-129">Listar todas as versões de pacotes relacionados ao JSON de origem/feed especificado:</span><span class="sxs-lookup"><span data-stu-id="a7b2b-129">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="a7b2b-130">Listar pacotes relacionados a JSON de várias fontes/feeds:</span><span class="sxs-lookup"><span data-stu-id="a7b2b-130">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```
