---
title: Comando Add da CLI do NuGet
description: Referência para o nuget.exe Adicionar comando
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 096d2f7a61a3c861ce2084368500ab8e8b21f212
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776096"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="3d6e1-103">Adicionar comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3d6e1-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="3d6e1-104">**Aplica-se a**: &bullet; **versões com suporte** para publicação de pacotes: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="3d6e1-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="3d6e1-105">Adiciona um pacote especificado a uma origem de pacote não HTTP (uma pasta ou caminho UNC) em um layout hierárquico, onde as pastas são criadas para a ID do pacote e o número de versão.</span><span class="sxs-lookup"><span data-stu-id="3d6e1-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="3d6e1-106">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3d6e1-106">For example:</span></span>

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

<span data-ttu-id="3d6e1-107">Ao restaurar ou atualizar na origem do pacote, o layout hierárquico fornece um desempenho significativamente melhor.</span><span class="sxs-lookup"><span data-stu-id="3d6e1-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="3d6e1-108">Para expandir todos os arquivos no pacote para a origem do pacote de destino, use a `-Expand` opção.</span><span class="sxs-lookup"><span data-stu-id="3d6e1-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="3d6e1-109">Isso normalmente resulta em subpastas adicionais que aparecem no destino, como `tools` e `lib` .</span><span class="sxs-lookup"><span data-stu-id="3d6e1-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="3d6e1-110">Uso</span><span class="sxs-lookup"><span data-stu-id="3d6e1-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="3d6e1-111">em que `<packagePath>` é o nome do caminho para o pacote a ser adicionado e `<sourcePath>` especifica a origem do pacote baseado em pasta à qual o pacote será adicionado.</span><span class="sxs-lookup"><span data-stu-id="3d6e1-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="3d6e1-112">Não há suporte para fontes HTTP.</span><span class="sxs-lookup"><span data-stu-id="3d6e1-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="3d6e1-113">Opções</span><span class="sxs-lookup"><span data-stu-id="3d6e1-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="3d6e1-114">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="3d6e1-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3d6e1-115">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="3d6e1-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="3d6e1-116">Adiciona todos os arquivos no pacote à origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="3d6e1-116">Adds all the files in the package to the package source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="3d6e1-117">*(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="3d6e1-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>
<span data-ttu-id="3d6e1-118">Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="3d6e1-118">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="3d6e1-119">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="3d6e1-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="3d6e1-120">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="3d6e1-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

   <span data-ttu-id="3d6e1-121">Especifica a origem do pacote, que é uma pasta ou compartilhamento UNC, ao qual o nupkg será adicionado.</span><span class="sxs-lookup"><span data-stu-id="3d6e1-121">Specifies the package source, which is a folder or UNC share, to which the nupkg will be added.</span></span> <span data-ttu-id="3d6e1-122">Não há suporte para fontes http.</span><span class="sxs-lookup"><span data-stu-id="3d6e1-122">Http sources are not supported.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="3d6e1-123">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="3d6e1-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="3d6e1-124">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3d6e1-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3d6e1-125">Exemplos</span><span class="sxs-lookup"><span data-stu-id="3d6e1-125">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
