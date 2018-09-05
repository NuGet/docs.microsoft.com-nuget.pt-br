---
title: Comando de Ajuda da CLI do NuGet
description: Referência do comando de ajuda nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546557"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="ee7a8-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="ee7a8-103">help or ?</span></span> <span data-ttu-id="ee7a8-104">Commando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ee7a8-104">command (NuGet CLI)</span></span>

<span data-ttu-id="ee7a8-105">**Aplica-se a:** todos os &bullet; **versões com suporte**: todos</span><span class="sxs-lookup"><span data-stu-id="ee7a8-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="ee7a8-106">Geral de exibe informações de Ajuda e informações de ajuda sobre comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="ee7a8-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="ee7a8-107">Uso</span><span class="sxs-lookup"><span data-stu-id="ee7a8-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="ee7a8-108">onde [comando] identifica um comando específico para o qual exibir a Ajuda.</span><span class="sxs-lookup"><span data-stu-id="ee7a8-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="ee7a8-109">Com alguns comandos, lembre-se de especificar *ajudar* primeiro, como com `nuget help install`, pois há um pacote denominado "help" em nuget.org. Se você der o comando `nuget install help`, você não obter ajuda sobre o comando de instalação, mas em vez disso, instalará o pacote denominado ajuda.</span><span class="sxs-lookup"><span data-stu-id="ee7a8-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="ee7a8-110">Opções</span><span class="sxs-lookup"><span data-stu-id="ee7a8-110">Options</span></span>

| <span data-ttu-id="ee7a8-111">Opção</span><span class="sxs-lookup"><span data-stu-id="ee7a8-111">Option</span></span> | <span data-ttu-id="ee7a8-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="ee7a8-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ee7a8-113">Todos</span><span class="sxs-lookup"><span data-stu-id="ee7a8-113">All</span></span> | <span data-ttu-id="ee7a8-114">Imprimir a ajuda detalhada para todos os comandos disponíveis; ignorado se recebe um comando específico.</span><span class="sxs-lookup"><span data-stu-id="ee7a8-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="ee7a8-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ee7a8-115">ConfigFile</span></span> | <span data-ttu-id="ee7a8-116">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="ee7a8-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ee7a8-117">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="ee7a8-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ee7a8-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ee7a8-118">ForceEnglishOutput</span></span> | <span data-ttu-id="ee7a8-119">*(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="ee7a8-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ee7a8-120">Ajuda</span><span class="sxs-lookup"><span data-stu-id="ee7a8-120">Help</span></span> | <span data-ttu-id="ee7a8-121">Exibe informações de ajuda para o comando de Ajuda.</span><span class="sxs-lookup"><span data-stu-id="ee7a8-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="ee7a8-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="ee7a8-122">Markdown</span></span> | <span data-ttu-id="ee7a8-123">Imprimir no formato markdown quando usado com a ajuda detalhada `-All`.</span><span class="sxs-lookup"><span data-stu-id="ee7a8-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="ee7a8-124">Caso contrário é ignorado.</span><span class="sxs-lookup"><span data-stu-id="ee7a8-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="ee7a8-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ee7a8-125">NonInteractive</span></span> | <span data-ttu-id="ee7a8-126">Suprime a solicitações de entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="ee7a8-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ee7a8-127">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="ee7a8-127">Verbosity</span></span> | <span data-ttu-id="ee7a8-128">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="ee7a8-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ee7a8-129">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ee7a8-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ee7a8-130">Exemplos</span><span class="sxs-lookup"><span data-stu-id="ee7a8-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
