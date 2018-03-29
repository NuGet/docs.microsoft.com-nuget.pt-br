---
title: Comando do NuGet CLI locais | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referência para o comando de locais de nuget.exe
keywords: referência de locais do NuGet, comando locais
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0122c79e55b12838bd123cf91bfcbc5dbbd2a65c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="6fd3c-104">comando de locais (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6fd3c-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="6fd3c-105">**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="6fd3c-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="6fd3c-106">Desmarca ou lista os recursos locais do NuGet como o *cache http*, *global pacotes* pasta e a pasta temporária.</span><span class="sxs-lookup"><span data-stu-id="6fd3c-106">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="6fd3c-107">O `locals` comando também pode ser usado para exibir uma lista desses locais.</span><span class="sxs-lookup"><span data-stu-id="6fd3c-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="6fd3c-108">Para obter mais informações, consulte [Gerenciando os pacotes globais e as pastas do cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="6fd3c-108">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="6fd3c-109">Uso</span><span class="sxs-lookup"><span data-stu-id="6fd3c-109">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="6fd3c-110">onde `<folder>` é um dos `all`, `http-cache`, `packages-cache` *(3.5 e anteriores)*, `global-packages`, e `temp` *(3.4 ou posterior)*.</span><span class="sxs-lookup"><span data-stu-id="6fd3c-110">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="6fd3c-111">Opções</span><span class="sxs-lookup"><span data-stu-id="6fd3c-111">Options</span></span>

| <span data-ttu-id="6fd3c-112">Opção</span><span class="sxs-lookup"><span data-stu-id="6fd3c-112">Option</span></span> | <span data-ttu-id="6fd3c-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="6fd3c-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6fd3c-114">Clear</span><span class="sxs-lookup"><span data-stu-id="6fd3c-114">Clear</span></span> | <span data-ttu-id="6fd3c-115">Limpa a pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="6fd3c-115">Clears the specified folder.</span></span> |
| <span data-ttu-id="6fd3c-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6fd3c-116">ConfigFile</span></span> | <span data-ttu-id="6fd3c-117">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="6fd3c-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6fd3c-118">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="6fd3c-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="6fd3c-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6fd3c-119">ForceEnglishOutput</span></span> | <span data-ttu-id="6fd3c-120">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="6fd3c-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6fd3c-121">Ajuda</span><span class="sxs-lookup"><span data-stu-id="6fd3c-121">Help</span></span> | <span data-ttu-id="6fd3c-122">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="6fd3c-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="6fd3c-123">Lista</span><span class="sxs-lookup"><span data-stu-id="6fd3c-123">List</span></span> | <span data-ttu-id="6fd3c-124">Lista o local da pasta especificada, ou os locais de todas as pastas quando usado com *todos os*.</span><span class="sxs-lookup"><span data-stu-id="6fd3c-124">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="6fd3c-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="6fd3c-125">NonInteractive</span></span> | <span data-ttu-id="6fd3c-126">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="6fd3c-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="6fd3c-127">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="6fd3c-127">Verbosity</span></span> | <span data-ttu-id="6fd3c-128">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="6fd3c-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="6fd3c-129">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6fd3c-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6fd3c-130">Exemplos</span><span class="sxs-lookup"><span data-stu-id="6fd3c-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="6fd3c-131">Para obter exemplos adicionais, consulte [Gerenciando os pacotes globais e as pastas do cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="6fd3c-131">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
