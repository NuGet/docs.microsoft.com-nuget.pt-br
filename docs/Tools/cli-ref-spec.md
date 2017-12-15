---
title: Comando spec NuGet CLI | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: "Referência para o comando spec nuget.exe"
keywords: "referência de especificação do NuGet, especificações de comando"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="a8be9-104">comando spec (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a8be9-104">spec command (NuGet CLI)</span></span>

<span data-ttu-id="a8be9-105">**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="a8be9-105">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a8be9-106">Gera um `.nuspec` arquivo para um novo pacote.</span><span class="sxs-lookup"><span data-stu-id="a8be9-106">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="a8be9-107">Se executar na mesma pasta como um arquivo de projeto (`.csproj`, `.vbproj`, `.fsproj`), `spec` cria um editáveis `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="a8be9-107">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="a8be9-108">Para obter mais informações, consulte [criando um pacote](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="a8be9-108">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a8be9-109">Uso</span><span class="sxs-lookup"><span data-stu-id="a8be9-109">Usage</span></span>

```
nuget spec [<packageID>] [options]
```

<span data-ttu-id="a8be9-110">onde `<packageID>` é um identificador de pacote opcional para salvar no `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="a8be9-110">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="a8be9-111">Opções</span><span class="sxs-lookup"><span data-stu-id="a8be9-111">Options</span></span>

| <span data-ttu-id="a8be9-112">Opção</span><span class="sxs-lookup"><span data-stu-id="a8be9-112">Option</span></span> | <span data-ttu-id="a8be9-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="a8be9-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a8be9-114">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="a8be9-114">AssemblyPath</span></span> | <span data-ttu-id="a8be9-115">Especifica o caminho para o assembly a ser usado para metadados.</span><span class="sxs-lookup"><span data-stu-id="a8be9-115">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="a8be9-116">Force</span><span class="sxs-lookup"><span data-stu-id="a8be9-116">Force</span></span> | <span data-ttu-id="a8be9-117">Substitui qualquer existente `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="a8be9-117">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="a8be9-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a8be9-118">ForceEnglishOutput</span></span> | <span data-ttu-id="a8be9-119">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="a8be9-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a8be9-120">Ajuda</span><span class="sxs-lookup"><span data-stu-id="a8be9-120">Help</span></span> | <span data-ttu-id="a8be9-121">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="a8be9-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="a8be9-122">Não interativo</span><span class="sxs-lookup"><span data-stu-id="a8be9-122">NonInteractive</span></span> | <span data-ttu-id="a8be9-123">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="a8be9-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a8be9-124">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="a8be9-124">Verbosity</span></span> | <span data-ttu-id="a8be9-125">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="a8be9-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="a8be9-126">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a8be9-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a8be9-127">Exemplos</span><span class="sxs-lookup"><span data-stu-id="a8be9-127">Examples</span></span>

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
