---
title: Comando spec NuGet CLI
description: Referência para o comando spec nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17d3c5fc083f52fd9ab4a854ad358995bc55293b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817080"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="f658e-103">comando spec (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f658e-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="f658e-104">**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="f658e-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f658e-105">Gera um `.nuspec` arquivo para um novo pacote.</span><span class="sxs-lookup"><span data-stu-id="f658e-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="f658e-106">Se executar na mesma pasta como um arquivo de projeto (`.csproj`, `.vbproj`, `.fsproj`), `spec` cria um editáveis `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="f658e-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="f658e-107">Para obter mais informações, consulte [criando um pacote](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="f658e-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="f658e-108">Uso</span><span class="sxs-lookup"><span data-stu-id="f658e-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="f658e-109">onde `<packageID>` é um identificador de pacote opcional para salvar no `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="f658e-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="f658e-110">Opções</span><span class="sxs-lookup"><span data-stu-id="f658e-110">Options</span></span>

| <span data-ttu-id="f658e-111">Opção</span><span class="sxs-lookup"><span data-stu-id="f658e-111">Option</span></span> | <span data-ttu-id="f658e-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="f658e-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f658e-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="f658e-113">AssemblyPath</span></span> | <span data-ttu-id="f658e-114">Especifica o caminho para o assembly a ser usado para metadados.</span><span class="sxs-lookup"><span data-stu-id="f658e-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="f658e-115">Force</span><span class="sxs-lookup"><span data-stu-id="f658e-115">Force</span></span> | <span data-ttu-id="f658e-116">Substitui qualquer existente `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="f658e-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="f658e-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f658e-117">ForceEnglishOutput</span></span> | <span data-ttu-id="f658e-118">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="f658e-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f658e-119">Ajuda</span><span class="sxs-lookup"><span data-stu-id="f658e-119">Help</span></span> | <span data-ttu-id="f658e-120">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="f658e-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="f658e-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f658e-121">NonInteractive</span></span> | <span data-ttu-id="f658e-122">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="f658e-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f658e-123">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="f658e-123">Verbosity</span></span> | <span data-ttu-id="f658e-124">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="f658e-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f658e-125">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f658e-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f658e-126">Exemplos</span><span class="sxs-lookup"><span data-stu-id="f658e-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
