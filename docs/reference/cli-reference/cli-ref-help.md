---
title: Comando de ajuda da CLI do NuGet
description: Referência para o comando de ajuda do NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327793"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="be602-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="be602-103">help or ?</span></span> <span data-ttu-id="be602-104">Commando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="be602-104">command (NuGet CLI)</span></span>

<span data-ttu-id="be602-105">**Aplica-se a:** todas &bullet; as **versões com suporte**: todas</span><span class="sxs-lookup"><span data-stu-id="be602-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="be602-106">Exibe informações gerais de ajuda e informações de ajuda sobre comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="be602-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="be602-107">Uso</span><span class="sxs-lookup"><span data-stu-id="be602-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="be602-108">em que [Command] identifica um comando específico para o qual exibir a ajuda.</span><span class="sxs-lookup"><span data-stu-id="be602-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="be602-109">Com alguns comandos, lembre-se de especificar a *ajuda* primeiro, `nuget help install`como com o, porque há um pacote chamado "Help" em NuGet.org. Se você fornecer o comando `nuget install help`, não obterá ajuda sobre o comando de instalação, mas, em vez disso, instalará o pacote chamado help.</span><span class="sxs-lookup"><span data-stu-id="be602-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="be602-110">Opções</span><span class="sxs-lookup"><span data-stu-id="be602-110">Options</span></span>

| <span data-ttu-id="be602-111">Opção</span><span class="sxs-lookup"><span data-stu-id="be602-111">Option</span></span> | <span data-ttu-id="be602-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="be602-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="be602-113">Todos</span><span class="sxs-lookup"><span data-stu-id="be602-113">All</span></span> | <span data-ttu-id="be602-114">Imprimir ajuda detalhada para todos os comandos disponíveis; ignorado se um comando específico for fornecido.</span><span class="sxs-lookup"><span data-stu-id="be602-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="be602-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="be602-115">ConfigFile</span></span> | <span data-ttu-id="be602-116">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="be602-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="be602-117">Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="be602-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="be602-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="be602-118">ForceEnglishOutput</span></span> | <span data-ttu-id="be602-119">*(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="be602-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="be602-120">Ajuda</span><span class="sxs-lookup"><span data-stu-id="be602-120">Help</span></span> | <span data-ttu-id="be602-121">Exibe informações de ajuda para o próprio comando de ajuda.</span><span class="sxs-lookup"><span data-stu-id="be602-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="be602-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="be602-122">Markdown</span></span> | <span data-ttu-id="be602-123">Imprima a ajuda detalhada em formato de redução quando `-All`usado com.</span><span class="sxs-lookup"><span data-stu-id="be602-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="be602-124">Caso contrário ignorado.</span><span class="sxs-lookup"><span data-stu-id="be602-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="be602-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="be602-125">NonInteractive</span></span> | <span data-ttu-id="be602-126">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="be602-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="be602-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="be602-127">Verbosity</span></span> | <span data-ttu-id="be602-128">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="be602-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="be602-129">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="be602-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="be602-130">Exemplos</span><span class="sxs-lookup"><span data-stu-id="be602-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
