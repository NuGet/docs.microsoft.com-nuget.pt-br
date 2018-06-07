---
title: Comando de inicialização do NuGet CLI
description: Referência para o comando de inicialização de nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4fda33aabd51fbbf0e5559baaa42af065366ba4
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817812"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="ad3ea-103">comando init (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ad3ea-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="ad3ea-104">**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="ad3ea-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="ad3ea-105">Copia todos os pacotes de uma pasta simples em uma pasta de destino usando um layout hierárquico, conforme descrito para o [adicionar comando](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="ad3ea-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="ad3ea-106">Ou seja, usando `init` é equivalente a usar o `add` comando em cada pacote na pasta.</span><span class="sxs-lookup"><span data-stu-id="ad3ea-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="ad3ea-107">Assim como acontece com `add`, o destino deve ser uma pasta local ou um caminho UNC; Não há suporte para os repositórios de pacote HTTP como nuget.org ou servidores privadas.</span><span class="sxs-lookup"><span data-stu-id="ad3ea-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="ad3ea-108">Uso</span><span class="sxs-lookup"><span data-stu-id="ad3ea-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="ad3ea-109">onde `<source>` é a pasta que contém pacotes e `<destination>` é a pasta local ou caminho UNC para o qual os pacotes são copiados.</span><span class="sxs-lookup"><span data-stu-id="ad3ea-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="ad3ea-110">Opções</span><span class="sxs-lookup"><span data-stu-id="ad3ea-110">Options</span></span>

| <span data-ttu-id="ad3ea-111">Opção</span><span class="sxs-lookup"><span data-stu-id="ad3ea-111">Option</span></span> | <span data-ttu-id="ad3ea-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="ad3ea-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ad3ea-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ad3ea-113">ConfigFile</span></span> | <span data-ttu-id="ad3ea-114">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="ad3ea-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ad3ea-115">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="ad3ea-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ad3ea-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ad3ea-116">ForceEnglishOutput</span></span> | <span data-ttu-id="ad3ea-117">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="ad3ea-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ad3ea-118">Expandir</span><span class="sxs-lookup"><span data-stu-id="ad3ea-118">Expand</span></span> | <span data-ttu-id="ad3ea-119">Adiciona todos os arquivos em cada pacote que é adicionado à origem do pacote; mesmo que `-Expand` com o `add` comando.</span><span class="sxs-lookup"><span data-stu-id="ad3ea-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="ad3ea-120">Ajuda</span><span class="sxs-lookup"><span data-stu-id="ad3ea-120">Help</span></span> | <span data-ttu-id="ad3ea-121">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="ad3ea-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="ad3ea-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ad3ea-122">NonInteractive</span></span> | <span data-ttu-id="ad3ea-123">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="ad3ea-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ad3ea-124">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="ad3ea-124">Verbosity</span></span> | <span data-ttu-id="ad3ea-125">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="ad3ea-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ad3ea-126">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ad3ea-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ad3ea-127">Exemplos</span><span class="sxs-lookup"><span data-stu-id="ad3ea-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
