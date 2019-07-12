---
title: Referência do PowerShell NuGet Find-Package
description: Referência de comando do PowerShell de Find-Package no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: fee0ad0496f27d0796eddf177edc235bcb10da70
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842528"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="eab07-103">Find-Package (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="eab07-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="eab07-104">*Versão 3.0 ou superior; Este tópico descreve o comando dentro de [Package Manager Console](package-manager-console.md) no Visual Studio no Windows. Para o comando Find-Package PowerShell genérico, consulte o [referência do PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="eab07-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="eab07-105">Obtém o conjunto de pacotes remotos com o ID ou palavras-chave especificada da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="eab07-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="eab07-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="eab07-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="eab07-107">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="eab07-107">Parameters</span></span>

| <span data-ttu-id="eab07-108">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="eab07-108">Parameter</span></span> | <span data-ttu-id="eab07-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="eab07-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eab07-110">ID &lt;palavras-chave&gt;</span><span class="sxs-lookup"><span data-stu-id="eab07-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="eab07-111">(Obrigatório) Palavras-chave a ser usado ao procurar a origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="eab07-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="eab07-112">Use - ExactMatch para retornar somente os pacotes cuja ID de pacote corresponde as palavras-chave.</span><span class="sxs-lookup"><span data-stu-id="eab07-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="eab07-113">Se nenhuma palavra-chave é fornecidas, `Find-Package` retorna uma lista dos pacotes 20 principais downloads, ou o número especificada pelo - primeiro.</span><span class="sxs-lookup"><span data-stu-id="eab07-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="eab07-114">Observe que - Id é opcional e não operacional.</span><span class="sxs-lookup"><span data-stu-id="eab07-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="eab07-115">Origem</span><span class="sxs-lookup"><span data-stu-id="eab07-115">Source</span></span> | <span data-ttu-id="eab07-116">O caminho de URL ou pasta para a origem do pacote a pesquisar.</span><span class="sxs-lookup"><span data-stu-id="eab07-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="eab07-117">Caminhos de pasta local podem ser absoluto ou relativo à pasta atual.</span><span class="sxs-lookup"><span data-stu-id="eab07-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="eab07-118">Se omitido, `Find-Package` procura a origem do pacote selecionado no momento.</span><span class="sxs-lookup"><span data-stu-id="eab07-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="eab07-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="eab07-119">AllVersions</span></span> | <span data-ttu-id="eab07-120">Exibe todas as versões disponíveis de cada pacote em vez de apenas a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="eab07-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="eab07-121">First</span><span class="sxs-lookup"><span data-stu-id="eab07-121">First</span></span> | <span data-ttu-id="eab07-122">O número de pacotes para retornar do início da lista; o padrão é 20.</span><span class="sxs-lookup"><span data-stu-id="eab07-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="eab07-123">Skip</span><span class="sxs-lookup"><span data-stu-id="eab07-123">Skip</span></span> | <span data-ttu-id="eab07-124">Omite o primeiro &lt;int&gt; pacotes na lista exibida.</span><span class="sxs-lookup"><span data-stu-id="eab07-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="eab07-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="eab07-125">IncludePrerelease</span></span> | <span data-ttu-id="eab07-126">Inclui pacotes pré-lançados nos resultados.</span><span class="sxs-lookup"><span data-stu-id="eab07-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="eab07-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="eab07-127">ExactMatch</span></span> | <span data-ttu-id="eab07-128">Especificado para usar &lt;palavras-chave&gt; como uma ID do pacote diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="eab07-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="eab07-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="eab07-129">StartWith</span></span> | <span data-ttu-id="eab07-130">Retorna pacotes cujo começa com a ID de pacote &lt;palavras-chave&gt;.</span><span class="sxs-lookup"><span data-stu-id="eab07-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="eab07-131">Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="eab07-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="eab07-132">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="eab07-132">Common Parameters</span></span>

<span data-ttu-id="eab07-133">`Find-Package` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="eab07-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="eab07-134">Exemplos</span><span class="sxs-lookup"><span data-stu-id="eab07-134">Examples</span></span>

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
