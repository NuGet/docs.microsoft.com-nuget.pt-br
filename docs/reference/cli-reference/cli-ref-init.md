---
title: Comando init da CLI do NuGet
description: Referência para o comando nuget.exe init
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3b830d678a473c917b70bd46900bdb0206d3652e
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623078"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="2fd58-103">comando init (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2fd58-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="2fd58-104">**Aplica-se a:** &bullet; **versões com suporte** para criação de pacote: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="2fd58-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="2fd58-105">Copia todos os pacotes de uma pasta simples para uma pasta de destino usando um layout hierárquico, conforme descrito para o [comando Add](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="2fd58-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="2fd58-106">Ou seja, `init` o uso do é equivalente ao uso do `add` comando em cada pacote na pasta.</span><span class="sxs-lookup"><span data-stu-id="2fd58-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="2fd58-107">Assim como acontece com `add` o, o destino deve ser uma pasta local ou um caminho UNC; Não há suporte para repositórios de pacotes HTTP, como nuget.org ou servidores privados.</span><span class="sxs-lookup"><span data-stu-id="2fd58-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="2fd58-108">Uso</span><span class="sxs-lookup"><span data-stu-id="2fd58-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="2fd58-109">em que `<source>` é a pasta que contém pacotes e `<destination>` é a pasta local ou o nome do caminho UNC para o qual os pacotes são copiados.</span><span class="sxs-lookup"><span data-stu-id="2fd58-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="2fd58-110">Opções</span><span class="sxs-lookup"><span data-stu-id="2fd58-110">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="2fd58-111">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="2fd58-111">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2fd58-112">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="2fd58-112">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="2fd58-113">Adiciona todos os arquivos em cada pacote que é adicionado à origem do pacote; o mesmo que `-Expand` com o `add` comando.</span><span class="sxs-lookup"><span data-stu-id="2fd58-113">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="2fd58-114">*(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="2fd58-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="2fd58-115">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="2fd58-115">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="2fd58-116">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="2fd58-116">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="2fd58-117">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="2fd58-117">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="2fd58-118">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2fd58-118">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2fd58-119">Exemplos</span><span class="sxs-lookup"><span data-stu-id="2fd58-119">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
