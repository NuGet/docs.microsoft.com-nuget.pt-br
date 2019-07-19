---
title: Comando init da CLI do NuGet
description: Referência para o comando init NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327773"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="89ec7-103">comando init (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="89ec7-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="89ec7-104">**Aplica-se a:** &bullet; **versões com suporte** para criação de pacote: 3.3+</span><span class="sxs-lookup"><span data-stu-id="89ec7-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="89ec7-105">Copia todos os pacotes de uma pasta simples para uma pasta de destino usando um layout hierárquico, conforme descrito para o [comando Add](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="89ec7-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="89ec7-106">Ou seja, o `init` uso do é equivalente ao `add` uso do comando em cada pacote na pasta.</span><span class="sxs-lookup"><span data-stu-id="89ec7-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="89ec7-107">Assim como `add`acontece com o, o destino deve ser uma pasta local ou um caminho UNC; Não há suporte para repositórios de pacotes HTTP, como nuget.org ou servidores privados.</span><span class="sxs-lookup"><span data-stu-id="89ec7-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="89ec7-108">Uso</span><span class="sxs-lookup"><span data-stu-id="89ec7-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="89ec7-109">em `<source>` que é a pasta que contém `<destination>` pacotes e é a pasta local ou o nome do caminho UNC para o qual os pacotes são copiados.</span><span class="sxs-lookup"><span data-stu-id="89ec7-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="89ec7-110">Opções</span><span class="sxs-lookup"><span data-stu-id="89ec7-110">Options</span></span>

| <span data-ttu-id="89ec7-111">Opção</span><span class="sxs-lookup"><span data-stu-id="89ec7-111">Option</span></span> | <span data-ttu-id="89ec7-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="89ec7-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="89ec7-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="89ec7-113">ConfigFile</span></span> | <span data-ttu-id="89ec7-114">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="89ec7-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="89ec7-115">Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="89ec7-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="89ec7-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="89ec7-116">ForceEnglishOutput</span></span> | <span data-ttu-id="89ec7-117">*(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="89ec7-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="89ec7-118">Expandir</span><span class="sxs-lookup"><span data-stu-id="89ec7-118">Expand</span></span> | <span data-ttu-id="89ec7-119">Adiciona todos os arquivos em cada pacote que é adicionado à origem do pacote; o mesmo `-Expand` que com `add` o comando.</span><span class="sxs-lookup"><span data-stu-id="89ec7-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="89ec7-120">Ajuda</span><span class="sxs-lookup"><span data-stu-id="89ec7-120">Help</span></span> | <span data-ttu-id="89ec7-121">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="89ec7-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="89ec7-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="89ec7-122">NonInteractive</span></span> | <span data-ttu-id="89ec7-123">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="89ec7-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="89ec7-124">Verbosity</span><span class="sxs-lookup"><span data-stu-id="89ec7-124">Verbosity</span></span> | <span data-ttu-id="89ec7-125">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="89ec7-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="89ec7-126">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="89ec7-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="89ec7-127">Exemplos</span><span class="sxs-lookup"><span data-stu-id="89ec7-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
