---
title: Comando de Ajuda do NuGet CLI
description: Referência para o comando de ajuda de nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: dbfc803e24c824d30e128d6e86cfa3c43660668f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="c3678-103">Ajuda ou?</span><span class="sxs-lookup"><span data-stu-id="c3678-103">help or ?</span></span> <span data-ttu-id="c3678-104">Commando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c3678-104">command (NuGet CLI)</span></span>

<span data-ttu-id="c3678-105">**Aplica-se a:** todos os &bullet; **versões com suporte**: todos os</span><span class="sxs-lookup"><span data-stu-id="c3678-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="c3678-106">Exibe geral informações de Ajuda e informações de ajuda sobre os comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="c3678-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="c3678-107">Uso</span><span class="sxs-lookup"><span data-stu-id="c3678-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="c3678-108">onde [comando] identifica um comando específico para o qual exibir a Ajuda.</span><span class="sxs-lookup"><span data-stu-id="c3678-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="c3678-109">Com alguns comandos, lembre-se de especificar *ajuda* primeiro, como com `nuget help install`, pois há um pacote denominado "Ajuda" em nuget.org. Se você fornecer o comando `nuget install help`, você não obter ajuda sobre o comando de instalação, mas em vez disso, instalará o pacote denominado ajuda.</span><span class="sxs-lookup"><span data-stu-id="c3678-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="c3678-110">Opções</span><span class="sxs-lookup"><span data-stu-id="c3678-110">Options</span></span>

| <span data-ttu-id="c3678-111">Opção</span><span class="sxs-lookup"><span data-stu-id="c3678-111">Option</span></span> | <span data-ttu-id="c3678-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="c3678-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c3678-113">Todos</span><span class="sxs-lookup"><span data-stu-id="c3678-113">All</span></span> | <span data-ttu-id="c3678-114">Imprimir a ajuda detalhada para todos os comandos disponíveis; ignorado se for fornecido um comando específico.</span><span class="sxs-lookup"><span data-stu-id="c3678-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="c3678-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c3678-115">ConfigFile</span></span> | <span data-ttu-id="c3678-116">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="c3678-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c3678-117">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="c3678-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c3678-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c3678-118">ForceEnglishOutput</span></span> | <span data-ttu-id="c3678-119">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="c3678-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c3678-120">Ajuda</span><span class="sxs-lookup"><span data-stu-id="c3678-120">Help</span></span> | <span data-ttu-id="c3678-121">Exibe informações de ajuda para o comando Ajuda.</span><span class="sxs-lookup"><span data-stu-id="c3678-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="c3678-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="c3678-122">Markdown</span></span> | <span data-ttu-id="c3678-123">Imprimir a ajuda detalhada no formato de redução quando usado com `-All`.</span><span class="sxs-lookup"><span data-stu-id="c3678-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="c3678-124">Caso contrário é ignorado.</span><span class="sxs-lookup"><span data-stu-id="c3678-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="c3678-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c3678-125">NonInteractive</span></span> | <span data-ttu-id="c3678-126">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="c3678-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c3678-127">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="c3678-127">Verbosity</span></span> | <span data-ttu-id="c3678-128">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="c3678-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c3678-129">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c3678-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c3678-130">Exemplos</span><span class="sxs-lookup"><span data-stu-id="c3678-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
