---
title: Referência do NuGet Get-Package PowerShell
description: Referência para Get-Package comando do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8394f888ec3d5e57eacd351a4867173da1070ead
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777490"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="39951-103">Get-Package (console do Gerenciador de pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="39951-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="39951-104">*Este tópico descreve o comando no [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows. Para o comando genérico Get-Package do PowerShell, consulte a [referência do PackageManagement do PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="39951-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="39951-105">Recupera a lista de pacotes instalados no repositório local, lista os pacotes disponíveis de uma origem de pacote quando usados com a opção-ListAvailable ou lista as atualizações disponíveis quando usadas com a opção-Update.</span><span class="sxs-lookup"><span data-stu-id="39951-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="39951-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="39951-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="39951-107">Sem parâmetros, `Get-Package` exibe a lista de pacotes instalados no projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="39951-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="39951-108">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="39951-108">Parameters</span></span>

| <span data-ttu-id="39951-109">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="39951-109">Parameter</span></span> | <span data-ttu-id="39951-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="39951-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="39951-111">Fonte</span><span class="sxs-lookup"><span data-stu-id="39951-111">Source</span></span> | <span data-ttu-id="39951-112">A URL ou o caminho da pasta do pacote.</span><span class="sxs-lookup"><span data-stu-id="39951-112">The URL or folder path for the package .</span></span> <span data-ttu-id="39951-113">Os caminhos de pasta local podem ser absolutos ou relativos à pasta atual.</span><span class="sxs-lookup"><span data-stu-id="39951-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="39951-114">Se omitido, `Get-Package` pesquisa a origem do pacote selecionada no momento.</span><span class="sxs-lookup"><span data-stu-id="39951-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="39951-115">Quando usado com-ListAvailable, o padrão é nuget.org.</span><span class="sxs-lookup"><span data-stu-id="39951-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="39951-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="39951-116">ListAvailable</span></span> | <span data-ttu-id="39951-117">Lista os pacotes disponíveis de uma origem de pacote, padronizando para nuget.org. Mostra um padrão de pacotes 50 a menos que-PageSize e/ou-First sejam especificados.</span><span class="sxs-lookup"><span data-stu-id="39951-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="39951-118">Atualizações</span><span class="sxs-lookup"><span data-stu-id="39951-118">Updates</span></span> | <span data-ttu-id="39951-119">Lista os pacotes que têm uma atualização disponível na origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="39951-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="39951-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="39951-120">ProjectName</span></span> | <span data-ttu-id="39951-121">O projeto do qual obter os pacotes instalados.</span><span class="sxs-lookup"><span data-stu-id="39951-121">The project from which to get installed packages.</span></span> <span data-ttu-id="39951-122">Se omitido, retorna projetos instalados para a solução inteira.</span><span class="sxs-lookup"><span data-stu-id="39951-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="39951-123">Filtrar</span><span class="sxs-lookup"><span data-stu-id="39951-123">Filter</span></span> | <span data-ttu-id="39951-124">Uma cadeia de caracteres de filtro usada para restringir a lista de pacotes aplicando-o à ID, descrição e marcas do pacote.</span><span class="sxs-lookup"><span data-stu-id="39951-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="39951-125">Primeiro</span><span class="sxs-lookup"><span data-stu-id="39951-125">First</span></span> | <span data-ttu-id="39951-126">O número de pacotes a serem retornados do início da lista.</span><span class="sxs-lookup"><span data-stu-id="39951-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="39951-127">Se não for especificado, o padrão será 50.</span><span class="sxs-lookup"><span data-stu-id="39951-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="39951-128">Ignorar</span><span class="sxs-lookup"><span data-stu-id="39951-128">Skip</span></span> | <span data-ttu-id="39951-129">Omite os primeiros &lt; pacotes int &gt; da lista exibida.</span><span class="sxs-lookup"><span data-stu-id="39951-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="39951-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="39951-130">AllVersions</span></span> | <span data-ttu-id="39951-131">Exibe todas as versões disponíveis de cada pacote, em vez de apenas a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="39951-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="39951-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="39951-132">IncludePrerelease</span></span> | <span data-ttu-id="39951-133">Inclui pacotes de pré-lançamento nos resultados.</span><span class="sxs-lookup"><span data-stu-id="39951-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="39951-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="39951-134">PageSize</span></span> | <span data-ttu-id="39951-135">*(3.0 +)* Quando usado com-ListAvailable (obrigatório), o número de pacotes a serem listados antes de dar um aviso para continuar.</span><span class="sxs-lookup"><span data-stu-id="39951-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="39951-136">Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="39951-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="39951-137">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="39951-137">Common Parameters</span></span>

<span data-ttu-id="39951-138">`Get-Package` o oferece suporte aos seguintes [parâmetros comuns do PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="39951-138">`Get-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="39951-139">Exemplos</span><span class="sxs-lookup"><span data-stu-id="39951-139">Examples</span></span>

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```