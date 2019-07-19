---
title: Comando de especificação da CLI do NuGet
description: Referência para o comando de especificação NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327563"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="f30bd-103">comando spec (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f30bd-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="f30bd-104">**Aplica-se a:** &bullet; **versões com suporte** para criação de pacote: todas</span><span class="sxs-lookup"><span data-stu-id="f30bd-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f30bd-105">Gera um `.nuspec` arquivo para um novo pacote.</span><span class="sxs-lookup"><span data-stu-id="f30bd-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="f30bd-106">Se for executado na mesma pasta que um arquivo de projeto`.csproj`( `.vbproj`, `.fsproj`,) `spec` , o criará `.nuspec` um arquivo com tokens.</span><span class="sxs-lookup"><span data-stu-id="f30bd-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="f30bd-107">Para obter informações adicionais, consulte [criando um pacote](../../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="f30bd-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="f30bd-108">Uso</span><span class="sxs-lookup"><span data-stu-id="f30bd-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="f30bd-109">em `<packageID>` que é um identificador de pacote opcional para salvar `.nuspec` no arquivo.</span><span class="sxs-lookup"><span data-stu-id="f30bd-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="f30bd-110">Opções</span><span class="sxs-lookup"><span data-stu-id="f30bd-110">Options</span></span>

| <span data-ttu-id="f30bd-111">Opção</span><span class="sxs-lookup"><span data-stu-id="f30bd-111">Option</span></span> | <span data-ttu-id="f30bd-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="f30bd-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f30bd-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="f30bd-113">AssemblyPath</span></span> | <span data-ttu-id="f30bd-114">Especifica o caminho para o assembly a ser usado para metadados.</span><span class="sxs-lookup"><span data-stu-id="f30bd-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="f30bd-115">Aplicação</span><span class="sxs-lookup"><span data-stu-id="f30bd-115">Force</span></span> | <span data-ttu-id="f30bd-116">Substitui qualquer arquivo existente `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="f30bd-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="f30bd-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f30bd-117">ForceEnglishOutput</span></span> | <span data-ttu-id="f30bd-118">*(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="f30bd-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f30bd-119">Help</span><span class="sxs-lookup"><span data-stu-id="f30bd-119">Help</span></span> | <span data-ttu-id="f30bd-120">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="f30bd-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="f30bd-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f30bd-121">NonInteractive</span></span> | <span data-ttu-id="f30bd-122">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="f30bd-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f30bd-123">Verbosity</span><span class="sxs-lookup"><span data-stu-id="f30bd-123">Verbosity</span></span> | <span data-ttu-id="f30bd-124">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="f30bd-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f30bd-125">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f30bd-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f30bd-126">Exemplos</span><span class="sxs-lookup"><span data-stu-id="f30bd-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
