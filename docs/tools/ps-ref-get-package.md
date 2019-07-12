---
title: Referência do PowerShell Get-pacote do NuGet
description: Referência de comando do PowerShell Get-Package no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d0d25cb6e21f6d0d42389e08340b6f1e1baf8a64
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842511"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="a5581-103">Get-Package (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="a5581-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a5581-104">*Este tópico descreve o comando dentro de [Package Manager Console](package-manager-console.md) no Visual Studio no Windows. Para o comando do PowerShell Get-Package genérico, consulte o [referência do PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="a5581-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="a5581-105">Recupera a lista de pacotes instalados no repositório local, lista de pacotes disponíveis a partir de uma origem de pacote quando usado com a opção - ListAvailable ou lista de atualizações disponíveis quando usado com a opção - opção de atualização.</span><span class="sxs-lookup"><span data-stu-id="a5581-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="a5581-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="a5581-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="a5581-107">Sem parâmetros, `Get-Package` exibe a lista de pacotes instalados no projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="a5581-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="a5581-108">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="a5581-108">Parameters</span></span>

| <span data-ttu-id="a5581-109">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="a5581-109">Parameter</span></span> | <span data-ttu-id="a5581-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="a5581-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a5581-111">Origem</span><span class="sxs-lookup"><span data-stu-id="a5581-111">Source</span></span> | <span data-ttu-id="a5581-112">O caminho de URL ou pasta para o pacote.</span><span class="sxs-lookup"><span data-stu-id="a5581-112">The URL or folder path for the package .</span></span> <span data-ttu-id="a5581-113">Caminhos de pasta local podem ser absoluto ou relativo à pasta atual.</span><span class="sxs-lookup"><span data-stu-id="a5581-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="a5581-114">Se omitido, `Get-Package` procura a origem do pacote selecionado no momento.</span><span class="sxs-lookup"><span data-stu-id="a5581-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="a5581-115">Quando usado com - ListAvailable, assume como padrão para o nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a5581-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="a5581-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="a5581-116">ListAvailable</span></span> | <span data-ttu-id="a5581-117">Lista os pacotes disponíveis a partir de uma origem de pacote, padronizando para nuget.org. Mostra um padrão de 50 pacotes, a menos que - PageSize e/ou - primeiro é especificado.</span><span class="sxs-lookup"><span data-stu-id="a5581-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="a5581-118">Atualizações</span><span class="sxs-lookup"><span data-stu-id="a5581-118">Updates</span></span> | <span data-ttu-id="a5581-119">Lista os pacotes que têm uma atualização disponível da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="a5581-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="a5581-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="a5581-120">ProjectName</span></span> | <span data-ttu-id="a5581-121">O projeto do qual obter os pacotes instalados.</span><span class="sxs-lookup"><span data-stu-id="a5581-121">The project from which to get installed packages.</span></span> <span data-ttu-id="a5581-122">Se omitido, retorna instalados projetos da solução inteira.</span><span class="sxs-lookup"><span data-stu-id="a5581-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="a5581-123">Filtro</span><span class="sxs-lookup"><span data-stu-id="a5581-123">Filter</span></span> | <span data-ttu-id="a5581-124">Uma cadeia de caracteres de filtro usada para restringir a lista de pacotes aplicando-o para a ID do pacote, descrição e marcas.</span><span class="sxs-lookup"><span data-stu-id="a5581-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="a5581-125">First</span><span class="sxs-lookup"><span data-stu-id="a5581-125">First</span></span> | <span data-ttu-id="a5581-126">O número de pacotes para retornar do início da lista.</span><span class="sxs-lookup"><span data-stu-id="a5581-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="a5581-127">Se não for especificado, padrão é 50.</span><span class="sxs-lookup"><span data-stu-id="a5581-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="a5581-128">Skip</span><span class="sxs-lookup"><span data-stu-id="a5581-128">Skip</span></span> | <span data-ttu-id="a5581-129">Omite o primeiro &lt;int&gt; pacotes na lista exibida.</span><span class="sxs-lookup"><span data-stu-id="a5581-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="a5581-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="a5581-130">AllVersions</span></span> | <span data-ttu-id="a5581-131">Exibe todas as versões disponíveis de cada pacote em vez de apenas a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="a5581-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="a5581-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="a5581-132">IncludePrerelease</span></span> | <span data-ttu-id="a5581-133">Inclui pacotes pré-lançados nos resultados.</span><span class="sxs-lookup"><span data-stu-id="a5581-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="a5581-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="a5581-134">PageSize</span></span> | <span data-ttu-id="a5581-135">*(3.0 ou superior)*  Quando usado com - ListAvailable (obrigatório), o número de pacotes para a lista antes de entregar um prompt para continuar.</span><span class="sxs-lookup"><span data-stu-id="a5581-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="a5581-136">Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="a5581-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a5581-137">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="a5581-137">Common Parameters</span></span>

<span data-ttu-id="a5581-138">`Get-Package` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="a5581-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a5581-139">Exemplos</span><span class="sxs-lookup"><span data-stu-id="a5581-139">Examples</span></span>

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
