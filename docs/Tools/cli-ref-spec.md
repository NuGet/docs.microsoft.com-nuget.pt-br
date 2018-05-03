---
title: Comando spec NuGet CLI
description: Referência para o comando spec nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68d661030ce7bcff7d7a3a1c96c07e149ad4ffea
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="6d121-103">comando spec (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6d121-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="6d121-104">**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="6d121-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="6d121-105">Gera um `.nuspec` arquivo para um novo pacote.</span><span class="sxs-lookup"><span data-stu-id="6d121-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="6d121-106">Se executar na mesma pasta como um arquivo de projeto (`.csproj`, `.vbproj`, `.fsproj`), `spec` cria um editáveis `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="6d121-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="6d121-107">Para obter mais informações, consulte [criando um pacote](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="6d121-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="6d121-108">Uso</span><span class="sxs-lookup"><span data-stu-id="6d121-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="6d121-109">onde `<packageID>` é um identificador de pacote opcional para salvar no `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="6d121-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="6d121-110">Opções</span><span class="sxs-lookup"><span data-stu-id="6d121-110">Options</span></span>

| <span data-ttu-id="6d121-111">Opção</span><span class="sxs-lookup"><span data-stu-id="6d121-111">Option</span></span> | <span data-ttu-id="6d121-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="6d121-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6d121-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="6d121-113">AssemblyPath</span></span> | <span data-ttu-id="6d121-114">Especifica o caminho para o assembly a ser usado para metadados.</span><span class="sxs-lookup"><span data-stu-id="6d121-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="6d121-115">Force</span><span class="sxs-lookup"><span data-stu-id="6d121-115">Force</span></span> | <span data-ttu-id="6d121-116">Substitui qualquer existente `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="6d121-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="6d121-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6d121-117">ForceEnglishOutput</span></span> | <span data-ttu-id="6d121-118">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="6d121-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6d121-119">Ajuda</span><span class="sxs-lookup"><span data-stu-id="6d121-119">Help</span></span> | <span data-ttu-id="6d121-120">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="6d121-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="6d121-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="6d121-121">NonInteractive</span></span> | <span data-ttu-id="6d121-122">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="6d121-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="6d121-123">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="6d121-123">Verbosity</span></span> | <span data-ttu-id="6d121-124">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="6d121-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="6d121-125">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6d121-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6d121-126">Exemplos</span><span class="sxs-lookup"><span data-stu-id="6d121-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
