---
title: Comando de Ajuda do NuGet CLI
description: Referência para o comando de ajuda de nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d7112209a0a2a267343c3458ebacaf6b744786a9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818250"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="423f5-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="423f5-103">help or ?</span></span> <span data-ttu-id="423f5-104">Commando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="423f5-104">command (NuGet CLI)</span></span>

<span data-ttu-id="423f5-105">**Aplica-se a:** todos os &bullet; **versões com suporte**: todos os</span><span class="sxs-lookup"><span data-stu-id="423f5-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="423f5-106">Exibe geral informações de Ajuda e informações de ajuda sobre os comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="423f5-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="423f5-107">Uso</span><span class="sxs-lookup"><span data-stu-id="423f5-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="423f5-108">onde [comando] identifica um comando específico para o qual exibir a Ajuda.</span><span class="sxs-lookup"><span data-stu-id="423f5-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="423f5-109">Com alguns comandos, lembre-se de especificar *ajuda* primeiro, como com `nuget help install`, pois há um pacote denominado "Ajuda" em nuget.org. Se você fornecer o comando `nuget install help`, você não obter ajuda sobre o comando de instalação, mas em vez disso, instalará o pacote denominado ajuda.</span><span class="sxs-lookup"><span data-stu-id="423f5-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="423f5-110">Opções</span><span class="sxs-lookup"><span data-stu-id="423f5-110">Options</span></span>

| <span data-ttu-id="423f5-111">Opção</span><span class="sxs-lookup"><span data-stu-id="423f5-111">Option</span></span> | <span data-ttu-id="423f5-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="423f5-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="423f5-113">Todos</span><span class="sxs-lookup"><span data-stu-id="423f5-113">All</span></span> | <span data-ttu-id="423f5-114">Imprimir a ajuda detalhada para todos os comandos disponíveis; ignorado se for fornecido um comando específico.</span><span class="sxs-lookup"><span data-stu-id="423f5-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="423f5-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="423f5-115">ConfigFile</span></span> | <span data-ttu-id="423f5-116">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="423f5-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="423f5-117">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="423f5-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="423f5-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="423f5-118">ForceEnglishOutput</span></span> | <span data-ttu-id="423f5-119">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="423f5-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="423f5-120">Ajuda</span><span class="sxs-lookup"><span data-stu-id="423f5-120">Help</span></span> | <span data-ttu-id="423f5-121">Exibe informações de ajuda para o comando Ajuda.</span><span class="sxs-lookup"><span data-stu-id="423f5-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="423f5-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="423f5-122">Markdown</span></span> | <span data-ttu-id="423f5-123">Imprimir a ajuda detalhada no formato de redução quando usado com `-All`.</span><span class="sxs-lookup"><span data-stu-id="423f5-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="423f5-124">Caso contrário é ignorado.</span><span class="sxs-lookup"><span data-stu-id="423f5-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="423f5-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="423f5-125">NonInteractive</span></span> | <span data-ttu-id="423f5-126">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="423f5-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="423f5-127">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="423f5-127">Verbosity</span></span> | <span data-ttu-id="423f5-128">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="423f5-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="423f5-129">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="423f5-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="423f5-130">Exemplos</span><span class="sxs-lookup"><span data-stu-id="423f5-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
