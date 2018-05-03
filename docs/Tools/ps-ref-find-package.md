---
title: Referência de PowerShell do NuGet Find-Package
description: Referência de comando do PowerShell de Find-Package no Console do Gerenciador de pacotes do NuGet no Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 0faf5c5cf9ae99105e3d76a4f5e37f164c4f4ff3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="2776b-103">Find-Package (Console de Gerenciador de pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="2776b-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="2776b-104">*Versão 3.0 +; Este tópico descreve o comando dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows. Para o comando PowerShell Find-Package genérico, consulte o [referência do PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="2776b-104">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="2776b-105">Obtém o conjunto de pacotes remotos com a ID ou palavras-chave especificada da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="2776b-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="2776b-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="2776b-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="2776b-107">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="2776b-107">Parameters</span></span>

| <span data-ttu-id="2776b-108">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="2776b-108">Parameter</span></span> | <span data-ttu-id="2776b-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="2776b-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2776b-110">ID &lt;palavras-chave&gt;</span><span class="sxs-lookup"><span data-stu-id="2776b-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="2776b-111">(Obrigatório) Palavras-chave a ser usado ao procurar a origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="2776b-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="2776b-112">Use - ExactMatch para retornar somente os pacotes cuja ID de pacote coincide com as palavras-chave.</span><span class="sxs-lookup"><span data-stu-id="2776b-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="2776b-113">Se nenhuma palavra-chave for fornecido, `Find-Package` retorna uma lista dos pacotes 20 principais downloads ou o número especificada por - primeiro.</span><span class="sxs-lookup"><span data-stu-id="2776b-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="2776b-114">Observe que - Id é opcional e não operacional.</span><span class="sxs-lookup"><span data-stu-id="2776b-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="2776b-115">Origem</span><span class="sxs-lookup"><span data-stu-id="2776b-115">Source</span></span> | <span data-ttu-id="2776b-116">O caminho de URL ou pasta para a origem do pacote a ser pesquisado.</span><span class="sxs-lookup"><span data-stu-id="2776b-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="2776b-117">Caminhos de pasta local podem ser absoluto ou relativo para a pasta atual.</span><span class="sxs-lookup"><span data-stu-id="2776b-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="2776b-118">Se omitido, `Find-Package` procura a origem de pacote selecionada atualmente.</span><span class="sxs-lookup"><span data-stu-id="2776b-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="2776b-119">Todasas versões</span><span class="sxs-lookup"><span data-stu-id="2776b-119">AllVersions</span></span> | <span data-ttu-id="2776b-120">Exibe todas as versões disponíveis de cada pacote em vez de apenas a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="2776b-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="2776b-121">Primeiro</span><span class="sxs-lookup"><span data-stu-id="2776b-121">First</span></span> | <span data-ttu-id="2776b-122">O número de pacotes a serem retornados desde o início da lista; o padrão é 20.</span><span class="sxs-lookup"><span data-stu-id="2776b-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="2776b-123">Skip</span><span class="sxs-lookup"><span data-stu-id="2776b-123">Skip</span></span> | <span data-ttu-id="2776b-124">Omite o primeiro &lt;int&gt; pacotes na lista exibida.</span><span class="sxs-lookup"><span data-stu-id="2776b-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="2776b-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="2776b-125">IncludePrerelease</span></span> | <span data-ttu-id="2776b-126">Inclui pacotes pré-lançados nos resultados.</span><span class="sxs-lookup"><span data-stu-id="2776b-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="2776b-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="2776b-127">ExactMatch</span></span> | <span data-ttu-id="2776b-128">Especificado para usar &lt;palavras-chave&gt; como uma ID de pacote diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2776b-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="2776b-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="2776b-129">StartWith</span></span> | <span data-ttu-id="2776b-130">Retorna pacotes cujo começa com a ID de pacote &lt;palavras-chave&gt;.</span><span class="sxs-lookup"><span data-stu-id="2776b-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="2776b-131">Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="2776b-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="2776b-132">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="2776b-132">Common Parameters</span></span>

<span data-ttu-id="2776b-133">`Find-Package` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="2776b-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="2776b-134">Exemplos</span><span class="sxs-lookup"><span data-stu-id="2776b-134">Examples</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```
