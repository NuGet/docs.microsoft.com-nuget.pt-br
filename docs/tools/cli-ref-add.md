---
title: CLI do NuGet adicionar comando
description: Referência para o nuget.exe adicionar comando
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545828"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="9edf8-103">Commando add (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9edf8-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="9edf8-104">**Aplica-se ao**: a publicação do pacote &bullet; **versões com suporte**: 3.3 ou superior</span><span class="sxs-lookup"><span data-stu-id="9edf8-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="9edf8-105">Adiciona um pacote especificado para uma origem de pacote não HTTP (uma pasta ou caminho UNC) em um layout hierárquico, no qual as pastas são criadas para o número de ID e a versão do pacote.</span><span class="sxs-lookup"><span data-stu-id="9edf8-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="9edf8-106">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9edf8-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="9edf8-107">Ao restaurar ou atualizar em relação a origem do pacote, o layout hierárquico fornece um desempenho significativamente melhor.</span><span class="sxs-lookup"><span data-stu-id="9edf8-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="9edf8-108">Para expandir todos os arquivos no pacote para a origem do pacote de destino, use o `-Expand` alternar.</span><span class="sxs-lookup"><span data-stu-id="9edf8-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="9edf8-109">Isso normalmente resulta em subpastas adicionais que aparecem no destino, como `tools` e `lib`.</span><span class="sxs-lookup"><span data-stu-id="9edf8-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="9edf8-110">Uso</span><span class="sxs-lookup"><span data-stu-id="9edf8-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="9edf8-111">em que `<packagePath>` é o nome do caminho para o pacote para adicionar, e `<sourcePath>` Especifica a origem de pacote com base em pasta à qual o pacote será adicionado.</span><span class="sxs-lookup"><span data-stu-id="9edf8-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="9edf8-112">Não há suporte para fontes de HTTP.</span><span class="sxs-lookup"><span data-stu-id="9edf8-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="9edf8-113">Opções</span><span class="sxs-lookup"><span data-stu-id="9edf8-113">Options</span></span>

| <span data-ttu-id="9edf8-114">Opção</span><span class="sxs-lookup"><span data-stu-id="9edf8-114">Option</span></span> | <span data-ttu-id="9edf8-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="9edf8-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9edf8-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="9edf8-116">ConfigFile</span></span> | <span data-ttu-id="9edf8-117">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="9edf8-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9edf8-118">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="9edf8-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="9edf8-119">Expandir</span><span class="sxs-lookup"><span data-stu-id="9edf8-119">Expand</span></span> | <span data-ttu-id="9edf8-120">Adiciona todos os arquivos no pacote de origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="9edf8-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="9edf8-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9edf8-121">ForceEnglishOutput</span></span> | <span data-ttu-id="9edf8-122">*(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="9edf8-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9edf8-123">Ajuda</span><span class="sxs-lookup"><span data-stu-id="9edf8-123">Help</span></span> | <span data-ttu-id="9edf8-124">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="9edf8-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="9edf8-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="9edf8-125">NonInteractive</span></span> | <span data-ttu-id="9edf8-126">Suprime a solicitações de entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="9edf8-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="9edf8-127">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="9edf8-127">Verbosity</span></span> | <span data-ttu-id="9edf8-128">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="9edf8-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="9edf8-129">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9edf8-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9edf8-130">Exemplos</span><span class="sxs-lookup"><span data-stu-id="9edf8-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
