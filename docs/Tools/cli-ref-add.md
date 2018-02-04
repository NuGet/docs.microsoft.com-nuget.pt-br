---
title: NuGet CLI adicionar comando | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Comando de adicionar a referência para o nuget.exe"
keywords: "NuGet adicionar referência, adicione o comando de pacote"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 70c86f8d240bd308224f6b7887b630cc1e953bf8
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="cb35d-104">Adicionar um comando NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cb35d-104">add command (NuGet CLI)</span></span>

<span data-ttu-id="cb35d-105">**Aplica-se a**: a publicação do pacote &bullet; **versões com suporte**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="cb35d-105">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="cb35d-106">Adiciona um pacote especificado para uma origem de pacote não HTTP (uma pasta ou caminho UNC) em um layout hierárquico, no qual as pastas são criadas para o número de ID e a versão do pacote.</span><span class="sxs-lookup"><span data-stu-id="cb35d-106">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="cb35d-107">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="cb35d-107">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="cb35d-108">Ao restaurar ou atualizar em relação a origem do pacote, o layout hierárquico fornece um desempenho significativamente melhor.</span><span class="sxs-lookup"><span data-stu-id="cb35d-108">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="cb35d-109">Para expandir todos os arquivos no pacote de origem do pacote de destino, use o `-Expand` alternar.</span><span class="sxs-lookup"><span data-stu-id="cb35d-109">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="cb35d-110">Isso normalmente resulta em subpastas adicionais que aparecem no destino, como `tools` e `lib`.</span><span class="sxs-lookup"><span data-stu-id="cb35d-110">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="cb35d-111">Uso</span><span class="sxs-lookup"><span data-stu-id="cb35d-111">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="cb35d-112">onde `<packagePath>` é o nome do caminho para o pacote a ser adicionado e `<sourcePath>` Especifica a origem de pacote com base em pasta à qual o pacote será adicionado.</span><span class="sxs-lookup"><span data-stu-id="cb35d-112">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="cb35d-113">Não há suporte para fontes HTTP.</span><span class="sxs-lookup"><span data-stu-id="cb35d-113">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="cb35d-114">Opções</span><span class="sxs-lookup"><span data-stu-id="cb35d-114">Options</span></span>

| <span data-ttu-id="cb35d-115">Opção</span><span class="sxs-lookup"><span data-stu-id="cb35d-115">Option</span></span> | <span data-ttu-id="cb35d-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="cb35d-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cb35d-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="cb35d-117">ConfigFile</span></span> | <span data-ttu-id="cb35d-118">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="cb35d-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cb35d-119">Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado.</span><span class="sxs-lookup"><span data-stu-id="cb35d-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span>| 
| <span data-ttu-id="cb35d-120">Expandir</span><span class="sxs-lookup"><span data-stu-id="cb35d-120">Expand</span></span> | <span data-ttu-id="cb35d-121">Adiciona todos os arquivos no pacote de origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="cb35d-121">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="cb35d-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cb35d-122">ForceEnglishOutput</span></span> | <span data-ttu-id="cb35d-123">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="cb35d-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cb35d-124">Ajuda</span><span class="sxs-lookup"><span data-stu-id="cb35d-124">Help</span></span> | <span data-ttu-id="cb35d-125">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="cb35d-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="cb35d-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="cb35d-126">NonInteractive</span></span> | <span data-ttu-id="cb35d-127">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="cb35d-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="cb35d-128">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="cb35d-128">Verbosity</span></span> | <span data-ttu-id="cb35d-129">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="cb35d-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="cb35d-130">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cb35d-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cb35d-131">Exemplos</span><span class="sxs-lookup"><span data-stu-id="cb35d-131">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
