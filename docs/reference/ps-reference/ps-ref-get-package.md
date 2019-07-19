---
title: Referência do PowerShell Get-Package do NuGet
description: Referência para o comando Get-Package do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 431e5f292f069ad5eb0c9f7f511d6b06810c8760
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327343"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="4d88b-103">Get-Package (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4d88b-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4d88b-104">*Este tópico descreve o comando no [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows. Para o comando genérico Get-Package do PowerShell, consulte a [referência do PackageManagement do PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="4d88b-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="4d88b-105">Recupera a lista de pacotes instalados no repositório local, lista os pacotes disponíveis de uma origem de pacote quando usados com a opção-ListAvailable ou lista as atualizações disponíveis quando usadas com a opção-Update.</span><span class="sxs-lookup"><span data-stu-id="4d88b-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="4d88b-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="4d88b-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="4d88b-107">Sem parâmetros, `Get-Package` exibe a lista de pacotes instalados no projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="4d88b-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="4d88b-108">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="4d88b-108">Parameters</span></span>

| <span data-ttu-id="4d88b-109">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="4d88b-109">Parameter</span></span> | <span data-ttu-id="4d88b-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="4d88b-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4d88b-111">Origem</span><span class="sxs-lookup"><span data-stu-id="4d88b-111">Source</span></span> | <span data-ttu-id="4d88b-112">A URL ou o caminho da pasta do pacote.</span><span class="sxs-lookup"><span data-stu-id="4d88b-112">The URL or folder path for the package .</span></span> <span data-ttu-id="4d88b-113">Os caminhos de pasta local podem ser absolutos ou relativos à pasta atual.</span><span class="sxs-lookup"><span data-stu-id="4d88b-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="4d88b-114">Se omitido `Get-Package` , pesquisa a origem do pacote selecionada no momento.</span><span class="sxs-lookup"><span data-stu-id="4d88b-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="4d88b-115">Quando usado com-ListAvailable, o padrão é nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4d88b-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="4d88b-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="4d88b-116">ListAvailable</span></span> | <span data-ttu-id="4d88b-117">Lista os pacotes disponíveis de uma origem de pacote, padronizando para nuget.org. Mostra um padrão de pacotes 50 a menos que-PageSize e/ou-First sejam especificados.</span><span class="sxs-lookup"><span data-stu-id="4d88b-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="4d88b-118">Atualizações</span><span class="sxs-lookup"><span data-stu-id="4d88b-118">Updates</span></span> | <span data-ttu-id="4d88b-119">Lista os pacotes que têm uma atualização disponível na origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="4d88b-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="4d88b-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="4d88b-120">ProjectName</span></span> | <span data-ttu-id="4d88b-121">O projeto do qual obter os pacotes instalados.</span><span class="sxs-lookup"><span data-stu-id="4d88b-121">The project from which to get installed packages.</span></span> <span data-ttu-id="4d88b-122">Se omitido, retorna projetos instalados para a solução inteira.</span><span class="sxs-lookup"><span data-stu-id="4d88b-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="4d88b-123">Filtro</span><span class="sxs-lookup"><span data-stu-id="4d88b-123">Filter</span></span> | <span data-ttu-id="4d88b-124">Uma cadeia de caracteres de filtro usada para restringir a lista de pacotes aplicando-o à ID, descrição e marcas do pacote.</span><span class="sxs-lookup"><span data-stu-id="4d88b-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="4d88b-125">First</span><span class="sxs-lookup"><span data-stu-id="4d88b-125">First</span></span> | <span data-ttu-id="4d88b-126">O número de pacotes a serem retornados do início da lista.</span><span class="sxs-lookup"><span data-stu-id="4d88b-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="4d88b-127">Se não for especificado, o padrão será 50.</span><span class="sxs-lookup"><span data-stu-id="4d88b-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="4d88b-128">Skip</span><span class="sxs-lookup"><span data-stu-id="4d88b-128">Skip</span></span> | <span data-ttu-id="4d88b-129">Omite os primeiros &lt;pacotes int&gt; da lista exibida.</span><span class="sxs-lookup"><span data-stu-id="4d88b-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="4d88b-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="4d88b-130">AllVersions</span></span> | <span data-ttu-id="4d88b-131">Exibe todas as versões disponíveis de cada pacote, em vez de apenas a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="4d88b-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="4d88b-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="4d88b-132">IncludePrerelease</span></span> | <span data-ttu-id="4d88b-133">Inclui pacotes de pré-lançamento nos resultados.</span><span class="sxs-lookup"><span data-stu-id="4d88b-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="4d88b-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="4d88b-134">PageSize</span></span> | <span data-ttu-id="4d88b-135">*(3.0 +)* Quando usado com-ListAvailable (obrigatório), o número de pacotes a serem listados antes de dar um aviso para continuar.</span><span class="sxs-lookup"><span data-stu-id="4d88b-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="4d88b-136">Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="4d88b-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4d88b-137">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="4d88b-137">Common Parameters</span></span>

<span data-ttu-id="4d88b-138">`Get-Package`o oferece suporte aos seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="4d88b-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4d88b-139">Exemplos</span><span class="sxs-lookup"><span data-stu-id="4d88b-139">Examples</span></span>

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
