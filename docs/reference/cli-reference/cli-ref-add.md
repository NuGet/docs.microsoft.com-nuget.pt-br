---
title: Comando Add da CLI do NuGet
description: Referência para o comando de adição NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327853"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="3f383-103">Commando add (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3f383-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="3f383-104">**Aplica-se a**: &bullet; **versões com suporte**para publicação de pacotes: 3.3+</span><span class="sxs-lookup"><span data-stu-id="3f383-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="3f383-105">Adiciona um pacote especificado a uma origem de pacote não HTTP (uma pasta ou caminho UNC) em um layout hierárquico, onde as pastas são criadas para a ID do pacote e o número de versão.</span><span class="sxs-lookup"><span data-stu-id="3f383-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="3f383-106">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3f383-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="3f383-107">Ao restaurar ou atualizar na origem do pacote, o layout hierárquico fornece um desempenho significativamente melhor.</span><span class="sxs-lookup"><span data-stu-id="3f383-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="3f383-108">Para expandir todos os arquivos no pacote para a origem do pacote de destino, use `-Expand` a opção.</span><span class="sxs-lookup"><span data-stu-id="3f383-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="3f383-109">Isso normalmente resulta em subpastas adicionais que aparecem no destino, como `tools` e. `lib`</span><span class="sxs-lookup"><span data-stu-id="3f383-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="3f383-110">Uso</span><span class="sxs-lookup"><span data-stu-id="3f383-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="3f383-111">em `<packagePath>` que é o nome do caminho para o pacote a `<sourcePath>` ser adicionado e especifica a origem do pacote baseado em pasta à qual o pacote será adicionado.</span><span class="sxs-lookup"><span data-stu-id="3f383-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="3f383-112">Não há suporte para fontes HTTP.</span><span class="sxs-lookup"><span data-stu-id="3f383-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="3f383-113">Opções</span><span class="sxs-lookup"><span data-stu-id="3f383-113">Options</span></span>

| <span data-ttu-id="3f383-114">Opção</span><span class="sxs-lookup"><span data-stu-id="3f383-114">Option</span></span> | <span data-ttu-id="3f383-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="3f383-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3f383-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3f383-116">ConfigFile</span></span> | <span data-ttu-id="3f383-117">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="3f383-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3f383-118">Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="3f383-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3f383-119">Expand</span><span class="sxs-lookup"><span data-stu-id="3f383-119">Expand</span></span> | <span data-ttu-id="3f383-120">Adiciona todos os arquivos no pacote à origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="3f383-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="3f383-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3f383-121">ForceEnglishOutput</span></span> | <span data-ttu-id="3f383-122">*(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="3f383-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3f383-123">Help</span><span class="sxs-lookup"><span data-stu-id="3f383-123">Help</span></span> | <span data-ttu-id="3f383-124">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="3f383-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="3f383-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3f383-125">NonInteractive</span></span> | <span data-ttu-id="3f383-126">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="3f383-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3f383-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="3f383-127">Verbosity</span></span> | <span data-ttu-id="3f383-128">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="3f383-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3f383-129">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3f383-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3f383-130">Exemplos</span><span class="sxs-lookup"><span data-stu-id="3f383-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
