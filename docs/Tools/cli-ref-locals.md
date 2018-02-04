---
title: Comando do NuGet CLI locais | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência para o comando de locais de nuget.exe"
keywords: "referência de locais do NuGet, comando locais"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="268d8-104">comando de locais (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="268d8-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="268d8-105">**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="268d8-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="268d8-106">Limpa ou lista os recursos locais do NuGet, como o cache de solicitação de http, cache de pacotes e a pasta pacotes global de todo o computador.</span><span class="sxs-lookup"><span data-stu-id="268d8-106">Clears or lists local NuGet resources such as the http-request cache, packages cache, and the machine-wide global packages folder.</span></span> <span data-ttu-id="268d8-107">O `locals` comando também pode ser usado para exibir uma lista desses locais.</span><span class="sxs-lookup"><span data-stu-id="268d8-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="268d8-108">Para obter mais informações, consulte [gerenciamento do Cache do NuGet](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="268d8-108">For more information, see [Managing the NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

## <a name="usage"></a><span data-ttu-id="268d8-109">Uso</span><span class="sxs-lookup"><span data-stu-id="268d8-109">Usage</span></span>

```cli
nuget locals <cache> [options]
```

<span data-ttu-id="268d8-110">onde `<cache>` é um dos `all`, `http-cache`, `packages-cache`, `global-packages`, e `temp` *(3.4 ou posterior)*.</span><span class="sxs-lookup"><span data-stu-id="268d8-110">where `<cache>` is one of `all`, `http-cache`, `packages-cache`, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="268d8-111">Opções</span><span class="sxs-lookup"><span data-stu-id="268d8-111">Options</span></span>

| <span data-ttu-id="268d8-112">Opção</span><span class="sxs-lookup"><span data-stu-id="268d8-112">Option</span></span> | <span data-ttu-id="268d8-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="268d8-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="268d8-114">Clear</span><span class="sxs-lookup"><span data-stu-id="268d8-114">Clear</span></span> | <span data-ttu-id="268d8-115">Limpa o cache especificado.</span><span class="sxs-lookup"><span data-stu-id="268d8-115">Clears the specified cache.</span></span> |
| <span data-ttu-id="268d8-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="268d8-116">ConfigFile</span></span> | <span data-ttu-id="268d8-117">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="268d8-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="268d8-118">Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado.</span><span class="sxs-lookup"><span data-stu-id="268d8-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="268d8-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="268d8-119">ForceEnglishOutput</span></span> | <span data-ttu-id="268d8-120">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="268d8-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="268d8-121">Ajuda</span><span class="sxs-lookup"><span data-stu-id="268d8-121">Help</span></span> | <span data-ttu-id="268d8-122">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="268d8-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="268d8-123">Lista</span><span class="sxs-lookup"><span data-stu-id="268d8-123">List</span></span> | <span data-ttu-id="268d8-124">Lista o local do cache especificado ou os locais de todos os caches quando usado com *todos os*.</span><span class="sxs-lookup"><span data-stu-id="268d8-124">Lists the location of the specified cache, or the locations of all caches when used with *all*.</span></span> |
| <span data-ttu-id="268d8-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="268d8-125">NonInteractive</span></span> | <span data-ttu-id="268d8-126">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="268d8-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="268d8-127">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="268d8-127">Verbosity</span></span> | <span data-ttu-id="268d8-128">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="268d8-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="268d8-129">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="268d8-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="268d8-130">Exemplos</span><span class="sxs-lookup"><span data-stu-id="268d8-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```
