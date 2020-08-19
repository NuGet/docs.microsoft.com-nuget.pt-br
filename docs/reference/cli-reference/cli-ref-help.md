---
title: Comando de ajuda da CLI do NuGet
description: Referência para o comando de ajuda do nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 12776b7c16aeef223a0b682ee2468edec8ea3295
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623104"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="d6d94-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="d6d94-103">help or ?</span></span> <span data-ttu-id="d6d94-104">comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d6d94-104">command (NuGet CLI)</span></span>

<span data-ttu-id="d6d94-105">**Aplica-se a:** todas as &bullet; **versões com suporte**: todas</span><span class="sxs-lookup"><span data-stu-id="d6d94-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="d6d94-106">Exibe informações gerais de ajuda e informações de ajuda sobre comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="d6d94-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="d6d94-107">Uso</span><span class="sxs-lookup"><span data-stu-id="d6d94-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="d6d94-108">em que [Command] identifica um comando específico para o qual exibir a ajuda.</span><span class="sxs-lookup"><span data-stu-id="d6d94-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="d6d94-109">Com alguns comandos, lembre-se de especificar a *ajuda* primeiro, como com `nuget help install` o, porque há um pacote chamado "help" em NuGet.org. Se você fornecer o comando `nuget install help` , não obterá ajuda sobre o comando de instalação, mas, em vez disso, instalará o pacote chamado help.</span><span class="sxs-lookup"><span data-stu-id="d6d94-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="d6d94-110">Opções</span><span class="sxs-lookup"><span data-stu-id="d6d94-110">Options</span></span>

- **`-All`**

  <span data-ttu-id="d6d94-111">Imprimir ajuda detalhada para todos os comandos disponíveis; ignorado se um comando específico for fornecido.</span><span class="sxs-lookup"><span data-stu-id="d6d94-111">Print detailed help for all available commands; ignored if a specific command is given.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="d6d94-112">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="d6d94-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d6d94-113">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="d6d94-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="d6d94-114">*(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="d6d94-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="d6d94-115">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="d6d94-115">Displays help information for the command.</span></span>

- **`-Markdown`**

  <span data-ttu-id="d6d94-116">Imprima a ajuda detalhada em formato de redução quando usado com `-All` .</span><span class="sxs-lookup"><span data-stu-id="d6d94-116">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="d6d94-117">Caso contrário ignorado.</span><span class="sxs-lookup"><span data-stu-id="d6d94-117">Ignored otherwise.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="d6d94-118">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="d6d94-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="d6d94-119">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="d6d94-119">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="d6d94-120">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d6d94-120">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d6d94-121">Exemplos</span><span class="sxs-lookup"><span data-stu-id="d6d94-121">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
