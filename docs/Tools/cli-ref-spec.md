---
title: Comando spec NuGet CLI | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência para o comando spec nuget.exe"
keywords: "referência de especificação do NuGet, especificações de comando"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc7e772e737a0f74929d13e2b126f7796b6d0dc7
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="75dcf-104">comando spec (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="75dcf-104">spec command (NuGet CLI)</span></span>

<span data-ttu-id="75dcf-105">**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="75dcf-105">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="75dcf-106">Gera um `.nuspec` arquivo para um novo pacote.</span><span class="sxs-lookup"><span data-stu-id="75dcf-106">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="75dcf-107">Se executar na mesma pasta como um arquivo de projeto (`.csproj`, `.vbproj`, `.fsproj`), `spec` cria um editáveis `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="75dcf-107">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="75dcf-108">Para obter mais informações, consulte [criando um pacote](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="75dcf-108">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="75dcf-109">Uso</span><span class="sxs-lookup"><span data-stu-id="75dcf-109">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="75dcf-110">onde `<packageID>` é um identificador de pacote opcional para salvar no `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="75dcf-110">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="75dcf-111">Opções</span><span class="sxs-lookup"><span data-stu-id="75dcf-111">Options</span></span>

| <span data-ttu-id="75dcf-112">Opção</span><span class="sxs-lookup"><span data-stu-id="75dcf-112">Option</span></span> | <span data-ttu-id="75dcf-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="75dcf-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="75dcf-114">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="75dcf-114">AssemblyPath</span></span> | <span data-ttu-id="75dcf-115">Especifica o caminho para o assembly a ser usado para metadados.</span><span class="sxs-lookup"><span data-stu-id="75dcf-115">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="75dcf-116">Force</span><span class="sxs-lookup"><span data-stu-id="75dcf-116">Force</span></span> | <span data-ttu-id="75dcf-117">Substitui qualquer existente `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="75dcf-117">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="75dcf-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="75dcf-118">ForceEnglishOutput</span></span> | <span data-ttu-id="75dcf-119">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="75dcf-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="75dcf-120">Ajuda</span><span class="sxs-lookup"><span data-stu-id="75dcf-120">Help</span></span> | <span data-ttu-id="75dcf-121">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="75dcf-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="75dcf-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="75dcf-122">NonInteractive</span></span> | <span data-ttu-id="75dcf-123">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="75dcf-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="75dcf-124">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="75dcf-124">Verbosity</span></span> | <span data-ttu-id="75dcf-125">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="75dcf-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="75dcf-126">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="75dcf-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="75dcf-127">Exemplos</span><span class="sxs-lookup"><span data-stu-id="75dcf-127">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
