---
title: Comando local da CLI do NuGet
description: Referência para o comando nuget.exe locais
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 25feb29c7b96c47681cedd8208b8595952d3ca49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779201"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="bc75f-103">comando locals (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="bc75f-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="bc75f-104">**Aplica-se a:** &bullet; **versões com suporte** de consumo de pacote: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="bc75f-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="bc75f-105">Limpa ou lista os recursos do NuGet local, como a pasta *http-cache*, *global-Packages* e a pasta Temp.</span><span class="sxs-lookup"><span data-stu-id="bc75f-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="bc75f-106">O `locals` comando também pode ser usado para exibir uma lista desses locais.</span><span class="sxs-lookup"><span data-stu-id="bc75f-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="bc75f-107">Para obter mais informações, consulte [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="bc75f-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="bc75f-108">Uso</span><span class="sxs-lookup"><span data-stu-id="bc75f-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="bc75f-109">em que `<folder>` é um de `all` , `http-cache` , `packages-cache` *(3,5 e anterior)*, `global-packages` , `temp` *(3.4 +)* e `plugins-cache` *(4.8 +)*.</span><span class="sxs-lookup"><span data-stu-id="bc75f-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="bc75f-110">Opções</span><span class="sxs-lookup"><span data-stu-id="bc75f-110">Options</span></span>

- **`-Clear`**

  <span data-ttu-id="bc75f-111">Limpa a pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="bc75f-111">Clears the specified folder.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="bc75f-112">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="bc75f-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="bc75f-113">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="bc75f-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="bc75f-114">*(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="bc75f-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="bc75f-115">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="bc75f-115">Displays help information for the command.</span></span>

- **`-List`**

  <span data-ttu-id="bc75f-116">Lista o local da pasta especificada ou os locais de todas as pastas quando usados com *todos*.</span><span class="sxs-lookup"><span data-stu-id="bc75f-116">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="bc75f-117">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="bc75f-117">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="bc75f-118">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="bc75f-118">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="bc75f-119">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="bc75f-119">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="bc75f-120">Exemplos</span><span class="sxs-lookup"><span data-stu-id="bc75f-120">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="bc75f-121">Para obter exemplos adicionais, consulte [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="bc75f-121">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
