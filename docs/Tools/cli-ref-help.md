---
title: Comando de Ajuda do NuGet CLI | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência para o comando de ajuda de nuget.exe"
keywords: "referência da Ajuda NuGet, o comando de ajuda"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b4255c353e412cf1d1a59590ee816b7887c90653
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="4391b-104">Ajuda ou?</span><span class="sxs-lookup"><span data-stu-id="4391b-104">help or ?</span></span> <span data-ttu-id="4391b-105">comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4391b-105">command (NuGet CLI)</span></span>

<span data-ttu-id="4391b-106">**Aplica-se a:** todos os &bullet; **versões com suporte**: todos os</span><span class="sxs-lookup"><span data-stu-id="4391b-106">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="4391b-107">Exibe geral informações de Ajuda e informações de ajuda sobre os comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="4391b-107">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="4391b-108">Uso</span><span class="sxs-lookup"><span data-stu-id="4391b-108">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="4391b-109">onde [comando] identifica um comando específico para o qual exibir a Ajuda.</span><span class="sxs-lookup"><span data-stu-id="4391b-109">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="4391b-110">Com alguns comandos, lembre-se de especificar *ajuda* primeiro, como com `nuget help install`, pois há um pacote denominado "Ajuda" em nuget.org. Se você fornecer o comando `nuget install help`, você não obter ajuda sobre o comando de instalação, mas em vez disso, instalará o pacote denominado ajuda.</span><span class="sxs-lookup"><span data-stu-id="4391b-110">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="4391b-111">Opções</span><span class="sxs-lookup"><span data-stu-id="4391b-111">Options</span></span>

| <span data-ttu-id="4391b-112">Opção</span><span class="sxs-lookup"><span data-stu-id="4391b-112">Option</span></span> | <span data-ttu-id="4391b-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="4391b-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4391b-114">Todos</span><span class="sxs-lookup"><span data-stu-id="4391b-114">All</span></span> | <span data-ttu-id="4391b-115">Imprimir a ajuda detalhada para todos os comandos disponíveis; ignorado se for fornecido um comando específico.</span><span class="sxs-lookup"><span data-stu-id="4391b-115">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="4391b-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="4391b-116">ConfigFile</span></span> | <span data-ttu-id="4391b-117">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="4391b-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4391b-118">Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado.</span><span class="sxs-lookup"><span data-stu-id="4391b-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="4391b-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4391b-119">ForceEnglishOutput</span></span> | <span data-ttu-id="4391b-120">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="4391b-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4391b-121">Ajuda</span><span class="sxs-lookup"><span data-stu-id="4391b-121">Help</span></span> | <span data-ttu-id="4391b-122">Exibe informações de ajuda para o comando Ajuda.</span><span class="sxs-lookup"><span data-stu-id="4391b-122">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="4391b-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="4391b-123">Markdown</span></span> | <span data-ttu-id="4391b-124">Imprimir a ajuda detalhada no formato de redução quando usado com `-All`.</span><span class="sxs-lookup"><span data-stu-id="4391b-124">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="4391b-125">Caso contrário é ignorado.</span><span class="sxs-lookup"><span data-stu-id="4391b-125">Ignored otherwise.</span></span> |
| <span data-ttu-id="4391b-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="4391b-126">NonInteractive</span></span> | <span data-ttu-id="4391b-127">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="4391b-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4391b-128">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="4391b-128">Verbosity</span></span> | <span data-ttu-id="4391b-129">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="4391b-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="4391b-130">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4391b-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4391b-131">Exemplos</span><span class="sxs-lookup"><span data-stu-id="4391b-131">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
