---
title: Referência do NuGet Find-Package PowerShell
description: Referência para Find-Package comando do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 267dd3eb501cae6e419386a5ca5e0c1ab659f807
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238082"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="3babe-103">Find-Package (console do Gerenciador de pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3babe-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3babe-104">*Versão 3.0 +; Este tópico descreve o comando no [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows. Para o comando genérico Find-Package do PowerShell, consulte a [referência do PackageManagement do PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="3babe-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="3babe-105">Obtém o conjunto de pacotes remotos com a ID ou palavras-chave especificadas da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="3babe-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="3babe-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="3babe-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="3babe-107">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="3babe-107">Parameters</span></span>

| <span data-ttu-id="3babe-108">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="3babe-108">Parameter</span></span> | <span data-ttu-id="3babe-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="3babe-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3babe-110">&lt;Palavras-chave de ID&gt;</span><span class="sxs-lookup"><span data-stu-id="3babe-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="3babe-111">Necessária Palavras-chave a serem usadas ao pesquisar a origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="3babe-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="3babe-112">Use-ExactMatch para retornar apenas os pacotes cuja ID de pacote corresponde às palavras-chave.</span><span class="sxs-lookup"><span data-stu-id="3babe-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="3babe-113">Se nenhuma palavra-chave for fornecida, `Find-Package` o retornará uma lista dos 20 primeiros pacotes por downloads ou o número especificado por-primeiro.</span><span class="sxs-lookup"><span data-stu-id="3babe-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="3babe-114">Observe que-ID é opcional e um não op.</span><span class="sxs-lookup"><span data-stu-id="3babe-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="3babe-115">Fonte</span><span class="sxs-lookup"><span data-stu-id="3babe-115">Source</span></span> | <span data-ttu-id="3babe-116">O caminho da URL ou da pasta para a origem do pacote a ser pesquisado.</span><span class="sxs-lookup"><span data-stu-id="3babe-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="3babe-117">Os caminhos de pasta local podem ser absolutos ou relativos à pasta atual.</span><span class="sxs-lookup"><span data-stu-id="3babe-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="3babe-118">Se omitido, `Find-Package` pesquisa a origem do pacote selecionada no momento.</span><span class="sxs-lookup"><span data-stu-id="3babe-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="3babe-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="3babe-119">AllVersions</span></span> | <span data-ttu-id="3babe-120">Exibe todas as versões disponíveis de cada pacote, em vez de apenas a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="3babe-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="3babe-121">Primeiro</span><span class="sxs-lookup"><span data-stu-id="3babe-121">First</span></span> | <span data-ttu-id="3babe-122">O número de pacotes a serem retornados do início da lista; o padrão é 20.</span><span class="sxs-lookup"><span data-stu-id="3babe-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="3babe-123">Ignorar</span><span class="sxs-lookup"><span data-stu-id="3babe-123">Skip</span></span> | <span data-ttu-id="3babe-124">Omite os primeiros &lt; pacotes int &gt; da lista exibida.</span><span class="sxs-lookup"><span data-stu-id="3babe-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="3babe-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="3babe-125">IncludePrerelease</span></span> | <span data-ttu-id="3babe-126">Inclui pacotes de pré-lançamento nos resultados.</span><span class="sxs-lookup"><span data-stu-id="3babe-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="3babe-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="3babe-127">ExactMatch</span></span> | <span data-ttu-id="3babe-128">Especificado para usar &lt; palavras-chave &gt; como uma ID de pacote que diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="3babe-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="3babe-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="3babe-129">StartWith</span></span> | <span data-ttu-id="3babe-130">Retorna os pacotes cuja ID de pacote começa com &lt; palavras-chave &gt; .</span><span class="sxs-lookup"><span data-stu-id="3babe-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="3babe-131">Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="3babe-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3babe-132">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="3babe-132">Common Parameters</span></span>

<span data-ttu-id="3babe-133">`Find-Package` o oferece suporte aos seguintes [parâmetros comuns do PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3babe-133">`Find-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3babe-134">Exemplos</span><span class="sxs-lookup"><span data-stu-id="3babe-134">Examples</span></span>

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