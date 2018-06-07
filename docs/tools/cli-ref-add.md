---
title: Comando Adicionar do NuGet CLI
description: Comando de adicionar a referência para o nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f229ca100463c556f9c4cefc49f52724a9c4ba77
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817604"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="7eda3-103">Commando add (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7eda3-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="7eda3-104">**Aplica-se a**: a publicação do pacote &bullet; **versões com suporte**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="7eda3-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="7eda3-105">Adiciona um pacote especificado para uma origem de pacote não HTTP (uma pasta ou caminho UNC) em um layout hierárquico, no qual as pastas são criadas para o número de ID e a versão do pacote.</span><span class="sxs-lookup"><span data-stu-id="7eda3-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="7eda3-106">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7eda3-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="7eda3-107">Ao restaurar ou atualizar em relação a origem do pacote, o layout hierárquico fornece um desempenho significativamente melhor.</span><span class="sxs-lookup"><span data-stu-id="7eda3-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="7eda3-108">Para expandir todos os arquivos no pacote de origem do pacote de destino, use o `-Expand` alternar.</span><span class="sxs-lookup"><span data-stu-id="7eda3-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="7eda3-109">Isso normalmente resulta em subpastas adicionais que aparecem no destino, como `tools` e `lib`.</span><span class="sxs-lookup"><span data-stu-id="7eda3-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="7eda3-110">Uso</span><span class="sxs-lookup"><span data-stu-id="7eda3-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="7eda3-111">onde `<packagePath>` é o nome do caminho para o pacote a ser adicionado e `<sourcePath>` Especifica a origem de pacote com base em pasta à qual o pacote será adicionado.</span><span class="sxs-lookup"><span data-stu-id="7eda3-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="7eda3-112">Não há suporte para fontes HTTP.</span><span class="sxs-lookup"><span data-stu-id="7eda3-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="7eda3-113">Opções</span><span class="sxs-lookup"><span data-stu-id="7eda3-113">Options</span></span>

| <span data-ttu-id="7eda3-114">Opção</span><span class="sxs-lookup"><span data-stu-id="7eda3-114">Option</span></span> | <span data-ttu-id="7eda3-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="7eda3-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7eda3-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7eda3-116">ConfigFile</span></span> | <span data-ttu-id="7eda3-117">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="7eda3-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7eda3-118">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="7eda3-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7eda3-119">Expandir</span><span class="sxs-lookup"><span data-stu-id="7eda3-119">Expand</span></span> | <span data-ttu-id="7eda3-120">Adiciona todos os arquivos no pacote de origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="7eda3-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="7eda3-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7eda3-121">ForceEnglishOutput</span></span> | <span data-ttu-id="7eda3-122">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="7eda3-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7eda3-123">Ajuda</span><span class="sxs-lookup"><span data-stu-id="7eda3-123">Help</span></span> | <span data-ttu-id="7eda3-124">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="7eda3-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="7eda3-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="7eda3-125">NonInteractive</span></span> | <span data-ttu-id="7eda3-126">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="7eda3-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7eda3-127">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="7eda3-127">Verbosity</span></span> | <span data-ttu-id="7eda3-128">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="7eda3-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7eda3-129">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7eda3-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7eda3-130">Exemplos</span><span class="sxs-lookup"><span data-stu-id="7eda3-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
