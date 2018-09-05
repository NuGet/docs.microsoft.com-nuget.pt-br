---
title: Comando spec da CLI do NuGet
description: Referência do comando spec nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68b165751ab6794d2a01d7e466619b1ce4d7ed72
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546443"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="f8bdb-103">comando spec (CLI do NuGet)</span><span class="sxs-lookup"><span data-stu-id="f8bdb-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="f8bdb-104">**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** todos os</span><span class="sxs-lookup"><span data-stu-id="f8bdb-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f8bdb-105">Gera um `.nuspec` arquivo para um novo pacote.</span><span class="sxs-lookup"><span data-stu-id="f8bdb-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="f8bdb-106">Se executado na mesma pasta como um arquivo de projeto (`.csproj`, `.vbproj`, `.fsproj`), `spec` cria com um token `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="f8bdb-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="f8bdb-107">Para obter mais informações, consulte [criando um pacote](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="f8bdb-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="f8bdb-108">Uso</span><span class="sxs-lookup"><span data-stu-id="f8bdb-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="f8bdb-109">em que `<packageID>` é um identificador de pacote opcional para salvar no `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="f8bdb-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="f8bdb-110">Opções</span><span class="sxs-lookup"><span data-stu-id="f8bdb-110">Options</span></span>

| <span data-ttu-id="f8bdb-111">Opção</span><span class="sxs-lookup"><span data-stu-id="f8bdb-111">Option</span></span> | <span data-ttu-id="f8bdb-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="f8bdb-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f8bdb-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="f8bdb-113">AssemblyPath</span></span> | <span data-ttu-id="f8bdb-114">Especifica o caminho para o assembly a ser usado para metadados.</span><span class="sxs-lookup"><span data-stu-id="f8bdb-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="f8bdb-115">Force</span><span class="sxs-lookup"><span data-stu-id="f8bdb-115">Force</span></span> | <span data-ttu-id="f8bdb-116">Substitui todos os existentes `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="f8bdb-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="f8bdb-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f8bdb-117">ForceEnglishOutput</span></span> | <span data-ttu-id="f8bdb-118">*(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="f8bdb-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f8bdb-119">Ajuda</span><span class="sxs-lookup"><span data-stu-id="f8bdb-119">Help</span></span> | <span data-ttu-id="f8bdb-120">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="f8bdb-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="f8bdb-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f8bdb-121">NonInteractive</span></span> | <span data-ttu-id="f8bdb-122">Suprime a solicitações de entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="f8bdb-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f8bdb-123">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="f8bdb-123">Verbosity</span></span> | <span data-ttu-id="f8bdb-124">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="f8bdb-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f8bdb-125">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f8bdb-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f8bdb-126">Exemplos</span><span class="sxs-lookup"><span data-stu-id="f8bdb-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
