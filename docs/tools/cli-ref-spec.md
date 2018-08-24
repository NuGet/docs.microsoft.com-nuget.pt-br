---
title: Comando spec da CLI do NuGet
description: Referência do comando spec nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: cd1dc66676898e2be1c64698886a5ba29a07f88f
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794145"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="2dee6-103">comando spec (CLI do NuGet)</span><span class="sxs-lookup"><span data-stu-id="2dee6-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="2dee6-104">**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** todos os</span><span class="sxs-lookup"><span data-stu-id="2dee6-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="2dee6-105">Gera um `.nuspec` arquivo para um novo pacote.</span><span class="sxs-lookup"><span data-stu-id="2dee6-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="2dee6-106">Se executado na mesma pasta como um arquivo de projeto (`.csproj`, `.vbproj`, `.fsproj`), `spec` cria com um token `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="2dee6-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="2dee6-107">Para obter mais informações, consulte [criando um pacote](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="2dee6-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="2dee6-108">Uso</span><span class="sxs-lookup"><span data-stu-id="2dee6-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="2dee6-109">em que `<packageID>` é um identificador de pacote opcional para salvar no `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="2dee6-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="2dee6-110">Opções</span><span class="sxs-lookup"><span data-stu-id="2dee6-110">Options</span></span>

| <span data-ttu-id="2dee6-111">Opção</span><span class="sxs-lookup"><span data-stu-id="2dee6-111">Option</span></span> | <span data-ttu-id="2dee6-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="2dee6-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2dee6-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="2dee6-113">AssemblyPath</span></span> | <span data-ttu-id="2dee6-114">Especifica o caminho para o assembly a ser usado para metadados.</span><span class="sxs-lookup"><span data-stu-id="2dee6-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="2dee6-115">Force</span><span class="sxs-lookup"><span data-stu-id="2dee6-115">Force</span></span> | <span data-ttu-id="2dee6-116">Substitui todos os existentes `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="2dee6-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="2dee6-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2dee6-117">ForceEnglishOutput</span></span> | <span data-ttu-id="2dee6-118">*(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="2dee6-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2dee6-119">Ajuda</span><span class="sxs-lookup"><span data-stu-id="2dee6-119">Help</span></span> | <span data-ttu-id="2dee6-120">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="2dee6-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="2dee6-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2dee6-121">NonInteractive</span></span> | <span data-ttu-id="2dee6-122">Suprime a solicitações de entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="2dee6-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2dee6-123">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="2dee6-123">Verbosity</span></span> | <span data-ttu-id="2dee6-124">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="2dee6-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2dee6-125">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2dee6-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2dee6-126">Exemplos</span><span class="sxs-lookup"><span data-stu-id="2dee6-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
