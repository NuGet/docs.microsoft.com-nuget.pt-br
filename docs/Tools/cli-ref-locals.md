---
title: Comando de locais de CLI do NuGet
description: Referência para o comando de locais de nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ac07dc306bc23c2fedd33c5627e8d34a6098387c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="2d7d5-103">comando de locais (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2d7d5-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="2d7d5-104">**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="2d7d5-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="2d7d5-105">Desmarca ou lista os recursos locais do NuGet como o *cache http*, *global pacotes* pasta e a pasta temporária.</span><span class="sxs-lookup"><span data-stu-id="2d7d5-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="2d7d5-106">O `locals` comando também pode ser usado para exibir uma lista desses locais.</span><span class="sxs-lookup"><span data-stu-id="2d7d5-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="2d7d5-107">Para obter mais informações, consulte [Gerenciando os pacotes globais e as pastas do cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="2d7d5-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="2d7d5-108">Uso</span><span class="sxs-lookup"><span data-stu-id="2d7d5-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="2d7d5-109">onde `<folder>` é um dos `all`, `http-cache`, `packages-cache` *(3.5 e anteriores)*, `global-packages`, e `temp` *(3.4 ou posterior)*.</span><span class="sxs-lookup"><span data-stu-id="2d7d5-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="2d7d5-110">Opções</span><span class="sxs-lookup"><span data-stu-id="2d7d5-110">Options</span></span>

| <span data-ttu-id="2d7d5-111">Opção</span><span class="sxs-lookup"><span data-stu-id="2d7d5-111">Option</span></span> | <span data-ttu-id="2d7d5-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="2d7d5-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2d7d5-113">Clear</span><span class="sxs-lookup"><span data-stu-id="2d7d5-113">Clear</span></span> | <span data-ttu-id="2d7d5-114">Limpa a pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="2d7d5-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="2d7d5-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2d7d5-115">ConfigFile</span></span> | <span data-ttu-id="2d7d5-116">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="2d7d5-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2d7d5-117">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="2d7d5-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2d7d5-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2d7d5-118">ForceEnglishOutput</span></span> | <span data-ttu-id="2d7d5-119">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="2d7d5-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2d7d5-120">Ajuda</span><span class="sxs-lookup"><span data-stu-id="2d7d5-120">Help</span></span> | <span data-ttu-id="2d7d5-121">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="2d7d5-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="2d7d5-122">Lista</span><span class="sxs-lookup"><span data-stu-id="2d7d5-122">List</span></span> | <span data-ttu-id="2d7d5-123">Lista o local da pasta especificada, ou os locais de todas as pastas quando usado com *todos os*.</span><span class="sxs-lookup"><span data-stu-id="2d7d5-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="2d7d5-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2d7d5-124">NonInteractive</span></span> | <span data-ttu-id="2d7d5-125">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="2d7d5-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2d7d5-126">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="2d7d5-126">Verbosity</span></span> | <span data-ttu-id="2d7d5-127">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="2d7d5-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2d7d5-128">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2d7d5-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2d7d5-129">Exemplos</span><span class="sxs-lookup"><span data-stu-id="2d7d5-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="2d7d5-130">Para obter exemplos adicionais, consulte [Gerenciando os pacotes globais e as pastas do cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="2d7d5-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
