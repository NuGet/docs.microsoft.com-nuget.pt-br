---
title: "Referência do PowerShell Get-pacote de NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 42476008-64b3-480e-a966-98b2fa38b681
description: "Referência de comando do PowerShell Get-Package no Console do Gerenciador de pacotes do NuGet no Visual Studio."
keywords: "Pacote de NuGet manager console, comandos do Powershell do NuGet, referência do Powershell do NuGet, Get-Package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 632936fe4dd9736f7c3740a2f763173dc725424a
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="c81a8-104">Get-Package (Console de Gerenciador de pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="c81a8-104">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="c81a8-105">*Este tópico descreve o comando dentro de [NuGet Package Manager Console](Package-Manager-Console.md) no Visual Studio no Windows. Para o comando do PowerShell Get-Package genérico, consulte o [referência do PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="c81a8-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="c81a8-106">Recupera a lista de pacotes instalados no repositório local, lista de pacotes disponíveis a partir de uma origem de pacote quando usado com a opção - ListAvailable ou lista de atualizações disponíveis quando usado com a opção-Update.</span><span class="sxs-lookup"><span data-stu-id="c81a8-106">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="c81a8-107">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="c81a8-107">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="c81a8-108">Sem parâmetros, `Get-Package` exibe a lista de pacotes instalados no projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="c81a8-108">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="c81a8-109">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="c81a8-109">Parameters</span></span>

| <span data-ttu-id="c81a8-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c81a8-110">Parameter</span></span> | <span data-ttu-id="c81a8-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="c81a8-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c81a8-112">Origem</span><span class="sxs-lookup"><span data-stu-id="c81a8-112">Source</span></span> | <span data-ttu-id="c81a8-113">O caminho de URL ou pasta para o pacote.</span><span class="sxs-lookup"><span data-stu-id="c81a8-113">The URL or folder path for the package .</span></span> <span data-ttu-id="c81a8-114">Caminhos de pasta local podem ser absoluto ou relativo para a pasta atual.</span><span class="sxs-lookup"><span data-stu-id="c81a8-114">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="c81a8-115">Se omitido, `Get-Package` procura a origem de pacote selecionada atualmente.</span><span class="sxs-lookup"><span data-stu-id="c81a8-115">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="c81a8-116">Quando usado com - ListAvailable, o padrão é nuget.org.</span><span class="sxs-lookup"><span data-stu-id="c81a8-116">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="c81a8-117">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="c81a8-117">ListAvailable</span></span> | <span data-ttu-id="c81a8-118">Lista de pacotes disponíveis a partir de uma origem do pacote, padronizando para nuget.org. Mostra um padrão de 50 pacotes, a menos que - PageSize e/ou - primeiro é especificado.</span><span class="sxs-lookup"><span data-stu-id="c81a8-118">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="c81a8-119">Atualizações</span><span class="sxs-lookup"><span data-stu-id="c81a8-119">Updates</span></span> | <span data-ttu-id="c81a8-120">Lista os pacotes que tenham uma atualização disponível da origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="c81a8-120">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="c81a8-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="c81a8-121">ProjectName</span></span> | <span data-ttu-id="c81a8-122">O projeto do qual obter os pacotes instalados.</span><span class="sxs-lookup"><span data-stu-id="c81a8-122">The project from which to get installed packages.</span></span> <span data-ttu-id="c81a8-123">Se omitido, retorna instalados projetos da solução inteira.</span><span class="sxs-lookup"><span data-stu-id="c81a8-123">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="c81a8-124">Filtro</span><span class="sxs-lookup"><span data-stu-id="c81a8-124">Filter</span></span> | <span data-ttu-id="c81a8-125">Uma cadeia de caracteres de filtro usada para restringir a lista de pacotes por aplicá-la para a ID do pacote, descrição e marcas.</span><span class="sxs-lookup"><span data-stu-id="c81a8-125">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="c81a8-126">Primeiro</span><span class="sxs-lookup"><span data-stu-id="c81a8-126">First</span></span> | <span data-ttu-id="c81a8-127">O número de pacotes a serem retornados desde o início da lista.</span><span class="sxs-lookup"><span data-stu-id="c81a8-127">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="c81a8-128">Se não for especificado, padrão é 50.</span><span class="sxs-lookup"><span data-stu-id="c81a8-128">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="c81a8-129">Skip</span><span class="sxs-lookup"><span data-stu-id="c81a8-129">Skip</span></span> | <span data-ttu-id="c81a8-130">Omite o primeiro &lt;int&gt; pacotes na lista exibida.</span><span class="sxs-lookup"><span data-stu-id="c81a8-130">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="c81a8-131">Todasas versões</span><span class="sxs-lookup"><span data-stu-id="c81a8-131">AllVersions</span></span> | <span data-ttu-id="c81a8-132">Exibe todas as versões disponíveis de cada pacote em vez de apenas a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="c81a8-132">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="c81a8-133">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="c81a8-133">IncludePrerelease</span></span> | <span data-ttu-id="c81a8-134">Inclui pacotes pré-lançados nos resultados.</span><span class="sxs-lookup"><span data-stu-id="c81a8-134">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="c81a8-135">PageSize</span><span class="sxs-lookup"><span data-stu-id="c81a8-135">PageSize</span></span> | <span data-ttu-id="c81a8-136">*(3.0 +)*  Quando usado com - ListAvailable (obrigatório), o número de pacotes para a lista antes de fazer uma solicitação para continuar.</span><span class="sxs-lookup"><span data-stu-id="c81a8-136">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="c81a8-137">Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="c81a8-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="c81a8-138">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="c81a8-138">Common Parameters</span></span>

<span data-ttu-id="c81a8-139">`Get-Package`suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c81a8-139">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="c81a8-140">Exemplos</span><span class="sxs-lookup"><span data-stu-id="c81a8-140">Examples</span></span>

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

