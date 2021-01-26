---
title: Comando de especificação da CLI do NuGet
description: Referência para o comando nuget.exe spec
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b7780ee5d2e722da5e1623f44709059dd9aa3d45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779150"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="8a78f-103">comando spec (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8a78f-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="8a78f-104">**Aplica-se a:** &bullet; **versões com suporte** para criação de pacote: todas</span><span class="sxs-lookup"><span data-stu-id="8a78f-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8a78f-105">Gera um `.nuspec` arquivo para um novo pacote.</span><span class="sxs-lookup"><span data-stu-id="8a78f-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="8a78f-106">Se for executado na mesma pasta que um arquivo de projeto ( `.csproj` , `.vbproj` , `.fsproj` ), `spec` o criará um arquivo com tokens `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="8a78f-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="8a78f-107">Para obter informações adicionais, consulte [criando um pacote](../../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="8a78f-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8a78f-108">Uso</span><span class="sxs-lookup"><span data-stu-id="8a78f-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="8a78f-109">em que `<packageID>` é um identificador de pacote opcional para salvar no `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="8a78f-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="8a78f-110">Opções</span><span class="sxs-lookup"><span data-stu-id="8a78f-110">Options</span></span>

- **`-AssemblyPath`**

  <span data-ttu-id="8a78f-111">Especifica o caminho para o assembly a ser usado para metadados.</span><span class="sxs-lookup"><span data-stu-id="8a78f-111">Specifies the path to the assembly to use for metadata.</span></span>

- **`-Force`**

  <span data-ttu-id="8a78f-112">Substitui qualquer `.nuspec` arquivo existente.</span><span class="sxs-lookup"><span data-stu-id="8a78f-112">Overwrites any existing `.nuspec` file.</span></span>


- **`-ForceEnglishOutput`**

  <span data-ttu-id="8a78f-113">*(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="8a78f-113">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="8a78f-114">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="8a78f-114">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="8a78f-115">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="8a78f-115">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="8a78f-116">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="8a78f-116">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="8a78f-117">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8a78f-117">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8a78f-118">Exemplos</span><span class="sxs-lookup"><span data-stu-id="8a78f-118">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
