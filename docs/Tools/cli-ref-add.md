---
title: NuGet CLI adicionar comando | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 4f68a016-ad4e-41fc-b869-88910fc5121e
description: "Comando de adicionar a referência para o nuget.exe"
keywords: "NuGet adicionar referência, adicione o comando de pacote"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bf9a6e51dfbf1716ba40273487b76ae04c18e948
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="69b12-104">Adicionar um comando NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="69b12-104">add command (NuGet CLI)</span></span>

<span data-ttu-id="69b12-105">**Aplica-se a**: a publicação do pacote &bullet; **versões com suporte**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="69b12-105">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="69b12-106">Adiciona um pacote especificado para uma origem de pacote não HTTP (uma pasta ou caminho UNC) em um layout hierárquico, no qual as pastas são criadas para o número de ID e a versão do pacote.</span><span class="sxs-lookup"><span data-stu-id="69b12-106">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="69b12-107">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="69b12-107">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="69b12-108">Ao restaurar ou atualizar em relação a origem do pacote, o layout hierárquico fornece um desempenho significativamente melhor.</span><span class="sxs-lookup"><span data-stu-id="69b12-108">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="69b12-109">Para expandir todos os arquivos no pacote de origem do pacote de destino, use o `-Expand` alternar.</span><span class="sxs-lookup"><span data-stu-id="69b12-109">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="69b12-110">Isso normalmente resulta em subpastas adicionais que aparecem no destino, como `tools` e `lib`.</span><span class="sxs-lookup"><span data-stu-id="69b12-110">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="69b12-111">Uso</span><span class="sxs-lookup"><span data-stu-id="69b12-111">Usage</span></span>

```
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="69b12-112">onde `<packagePath>` é o nome do caminho para o pacote a ser adicionado e `<sourcePath>` Especifica a origem de pacote com base em pasta à qual o pacote será adicionado.</span><span class="sxs-lookup"><span data-stu-id="69b12-112">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="69b12-113">Não há suporte para fontes HTTP.</span><span class="sxs-lookup"><span data-stu-id="69b12-113">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="69b12-114">Opções</span><span class="sxs-lookup"><span data-stu-id="69b12-114">Options</span></span>

| <span data-ttu-id="69b12-115">Opção</span><span class="sxs-lookup"><span data-stu-id="69b12-115">Option</span></span> | <span data-ttu-id="69b12-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="69b12-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="69b12-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="69b12-117">ConfigFile</span></span> | <span data-ttu-id="69b12-118">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="69b12-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="69b12-119">Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado.</span><span class="sxs-lookup"><span data-stu-id="69b12-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span>| 
| <span data-ttu-id="69b12-120">Expandir</span><span class="sxs-lookup"><span data-stu-id="69b12-120">Expand</span></span> | <span data-ttu-id="69b12-121">Adiciona todos os arquivos no pacote de origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="69b12-121">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="69b12-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="69b12-122">ForceEnglishOutput</span></span> | <span data-ttu-id="69b12-123">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="69b12-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="69b12-124">Ajuda</span><span class="sxs-lookup"><span data-stu-id="69b12-124">Help</span></span> | <span data-ttu-id="69b12-125">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="69b12-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="69b12-126">Não interativo</span><span class="sxs-lookup"><span data-stu-id="69b12-126">NonInteractive</span></span> | <span data-ttu-id="69b12-127">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="69b12-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="69b12-128">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="69b12-128">Verbosity</span></span> | <span data-ttu-id="69b12-129">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="69b12-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="69b12-130">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="69b12-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="69b12-131">Exemplos</span><span class="sxs-lookup"><span data-stu-id="69b12-131">Examples</span></span>

```
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
