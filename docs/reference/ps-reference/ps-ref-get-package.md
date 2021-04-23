---
title: Referência do NuGet Get-Package PowerShell
description: Referência para Get-Package comando do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7c91faecaac2967c7a01dd81e72b9097e7bd6cae
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901727"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="d5480-103">Get-Package (console do Gerenciador de pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d5480-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d5480-104">*Este tópico descreve o comando no [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows. Para o comando genérico Get-Package do PowerShell, consulte a [referência do PackageManagement do PowerShell](/powershell/module/packagemanagement).*</span><span class="sxs-lookup"><span data-stu-id="d5480-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="d5480-105">Recupera a lista de pacotes instalados no repositório local, lista os pacotes disponíveis de uma origem de pacote quando usados com a opção-ListAvailable ou lista as atualizações disponíveis quando usadas com a opção-Update.</span><span class="sxs-lookup"><span data-stu-id="d5480-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="d5480-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="d5480-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="d5480-107">Sem parâmetros, `Get-Package` exibe a lista de pacotes instalados no projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="d5480-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="d5480-108">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="d5480-108">Parameters</span></span>

| <span data-ttu-id="d5480-109">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d5480-109">Parameter</span></span> | <span data-ttu-id="d5480-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="d5480-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d5480-111">Fonte</span><span class="sxs-lookup"><span data-stu-id="d5480-111">Source</span></span> | <span data-ttu-id="d5480-112">A URL ou o caminho da pasta do pacote.</span><span class="sxs-lookup"><span data-stu-id="d5480-112">The URL or folder path for the package .</span></span> <span data-ttu-id="d5480-113">Os caminhos de pasta local podem ser absolutos ou relativos à pasta atual.</span><span class="sxs-lookup"><span data-stu-id="d5480-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="d5480-114">Se omitido, `Get-Package` pesquisa a origem do pacote selecionada no momento.</span><span class="sxs-lookup"><span data-stu-id="d5480-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="d5480-115">Quando usado com-ListAvailable, o padrão é nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d5480-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="d5480-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="d5480-116">ListAvailable</span></span> | <span data-ttu-id="d5480-117">Lista os pacotes disponíveis de uma origem de pacote, padronizando para nuget.org. Mostra um padrão de pacotes 50 a menos que-PageSize e/ou-First sejam especificados.</span><span class="sxs-lookup"><span data-stu-id="d5480-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="d5480-118">Atualizações</span><span class="sxs-lookup"><span data-stu-id="d5480-118">Updates</span></span> | <span data-ttu-id="d5480-119">Lista os pacotes que têm uma atualização disponível na origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="d5480-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="d5480-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="d5480-120">ProjectName</span></span> | <span data-ttu-id="d5480-121">O projeto do qual obter os pacotes instalados.</span><span class="sxs-lookup"><span data-stu-id="d5480-121">The project from which to get installed packages.</span></span> <span data-ttu-id="d5480-122">Se omitido, retorna projetos instalados para a solução inteira.</span><span class="sxs-lookup"><span data-stu-id="d5480-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="d5480-123">Filtrar</span><span class="sxs-lookup"><span data-stu-id="d5480-123">Filter</span></span> | <span data-ttu-id="d5480-124">Uma cadeia de caracteres de filtro usada para restringir a lista de pacotes aplicando-o à ID, descrição e marcas do pacote.</span><span class="sxs-lookup"><span data-stu-id="d5480-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="d5480-125">Primeiro</span><span class="sxs-lookup"><span data-stu-id="d5480-125">First</span></span> | <span data-ttu-id="d5480-126">O número de pacotes a serem retornados do início da lista.</span><span class="sxs-lookup"><span data-stu-id="d5480-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="d5480-127">Se não for especificado, o padrão será 50.</span><span class="sxs-lookup"><span data-stu-id="d5480-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="d5480-128">Ignorar</span><span class="sxs-lookup"><span data-stu-id="d5480-128">Skip</span></span> | <span data-ttu-id="d5480-129">Omite os primeiros &lt; pacotes int &gt; da lista exibida.</span><span class="sxs-lookup"><span data-stu-id="d5480-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="d5480-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="d5480-130">AllVersions</span></span> | <span data-ttu-id="d5480-131">Exibe todas as versões disponíveis de cada pacote, em vez de apenas a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="d5480-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="d5480-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="d5480-132">IncludePrerelease</span></span> | <span data-ttu-id="d5480-133">Inclui pacotes de pré-lançamento nos resultados.</span><span class="sxs-lookup"><span data-stu-id="d5480-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="d5480-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="d5480-134">PageSize</span></span> | <span data-ttu-id="d5480-135">*(3.0 +)* Quando usado com-ListAvailable (obrigatório), o número de pacotes a serem listados antes de dar um aviso para continuar.</span><span class="sxs-lookup"><span data-stu-id="d5480-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="d5480-136">Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="d5480-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d5480-137">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="d5480-137">Common Parameters</span></span>

<span data-ttu-id="d5480-138">`Get-Package` o oferece suporte aos seguintes [parâmetros comuns do PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d5480-138">`Get-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d5480-139">Exemplos</span><span class="sxs-lookup"><span data-stu-id="d5480-139">Examples</span></span>

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