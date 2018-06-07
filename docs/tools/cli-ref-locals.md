---
title: Comando de locais de CLI do NuGet
description: Referência para o comando de locais de nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 90e8c85e7a3e0e9520933e2ddd6dd84447475f2b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818195"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="af668-103">Commando locals (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="af668-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="af668-104">**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="af668-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="af668-105">Desmarca ou lista os recursos locais do NuGet como o *cache http*, *global pacotes* pasta e a pasta temporária.</span><span class="sxs-lookup"><span data-stu-id="af668-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="af668-106">O `locals` comando também pode ser usado para exibir uma lista desses locais.</span><span class="sxs-lookup"><span data-stu-id="af668-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="af668-107">Para obter mais informações, consulte [Gerenciando os pacotes globais e as pastas do cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="af668-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="af668-108">Uso</span><span class="sxs-lookup"><span data-stu-id="af668-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="af668-109">onde `<folder>` é um dos `all`, `http-cache`, `packages-cache` *(3.5 e anteriores)*, `global-packages`, e `temp` *(3.4 ou posterior)*.</span><span class="sxs-lookup"><span data-stu-id="af668-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="af668-110">Opções</span><span class="sxs-lookup"><span data-stu-id="af668-110">Options</span></span>

| <span data-ttu-id="af668-111">Opção</span><span class="sxs-lookup"><span data-stu-id="af668-111">Option</span></span> | <span data-ttu-id="af668-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="af668-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="af668-113">Clear</span><span class="sxs-lookup"><span data-stu-id="af668-113">Clear</span></span> | <span data-ttu-id="af668-114">Limpa a pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="af668-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="af668-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="af668-115">ConfigFile</span></span> | <span data-ttu-id="af668-116">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="af668-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="af668-117">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="af668-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="af668-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="af668-118">ForceEnglishOutput</span></span> | <span data-ttu-id="af668-119">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="af668-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="af668-120">Ajuda</span><span class="sxs-lookup"><span data-stu-id="af668-120">Help</span></span> | <span data-ttu-id="af668-121">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="af668-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="af668-122">Lista</span><span class="sxs-lookup"><span data-stu-id="af668-122">List</span></span> | <span data-ttu-id="af668-123">Lista o local da pasta especificada, ou os locais de todas as pastas quando usado com *todos os*.</span><span class="sxs-lookup"><span data-stu-id="af668-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="af668-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="af668-124">NonInteractive</span></span> | <span data-ttu-id="af668-125">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="af668-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="af668-126">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="af668-126">Verbosity</span></span> | <span data-ttu-id="af668-127">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="af668-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="af668-128">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="af668-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="af668-129">Exemplos</span><span class="sxs-lookup"><span data-stu-id="af668-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="af668-130">Para obter exemplos adicionais, consulte [Gerenciando os pacotes globais e as pastas do cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="af668-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
