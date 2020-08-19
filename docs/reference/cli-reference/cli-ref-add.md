---
title: Comando Add da CLI do NuGet
description: Referência para o nuget.exe Adicionar comando
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 89d268946243e8eae07e482db48e809a15260c38
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622896"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="03535-103">Adicionar comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="03535-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="03535-104">**Aplica-se a**: &bullet; **versões com suporte**para publicação de pacotes: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="03535-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="03535-105">Adiciona um pacote especificado a uma origem de pacote não HTTP (uma pasta ou caminho UNC) em um layout hierárquico, onde as pastas são criadas para a ID do pacote e o número de versão.</span><span class="sxs-lookup"><span data-stu-id="03535-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="03535-106">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="03535-106">For example:</span></span>

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

<span data-ttu-id="03535-107">Ao restaurar ou atualizar na origem do pacote, o layout hierárquico fornece um desempenho significativamente melhor.</span><span class="sxs-lookup"><span data-stu-id="03535-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="03535-108">Para expandir todos os arquivos no pacote para a origem do pacote de destino, use a `-Expand` opção.</span><span class="sxs-lookup"><span data-stu-id="03535-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="03535-109">Isso normalmente resulta em subpastas adicionais que aparecem no destino, como `tools` e `lib` .</span><span class="sxs-lookup"><span data-stu-id="03535-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="03535-110">Uso</span><span class="sxs-lookup"><span data-stu-id="03535-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="03535-111">em que `<packagePath>` é o nome do caminho para o pacote a ser adicionado e `<sourcePath>` especifica a origem do pacote baseado em pasta à qual o pacote será adicionado.</span><span class="sxs-lookup"><span data-stu-id="03535-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="03535-112">Não há suporte para fontes HTTP.</span><span class="sxs-lookup"><span data-stu-id="03535-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="03535-113">Opções</span><span class="sxs-lookup"><span data-stu-id="03535-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="03535-114">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="03535-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="03535-115">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="03535-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="03535-116">Adiciona todos os arquivos no pacote à origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="03535-116">Adds all the files in the package to the package source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="03535-117">*(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="03535-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>
<span data-ttu-id="03535-118">Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="03535-118">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="03535-119">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="03535-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="03535-120">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="03535-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

   <span data-ttu-id="03535-121">Especifica a origem do pacote, que é uma pasta ou compartilhamento UNC, ao qual o nupkg será adicionado.</span><span class="sxs-lookup"><span data-stu-id="03535-121">Specifies the package source, which is a folder or UNC share, to which the nupkg will be added.</span></span> <span data-ttu-id="03535-122">Não há suporte para fontes http.</span><span class="sxs-lookup"><span data-stu-id="03535-122">Http sources are not supported.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="03535-123">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="03535-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="03535-124">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="03535-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="03535-125">Exemplos</span><span class="sxs-lookup"><span data-stu-id="03535-125">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
