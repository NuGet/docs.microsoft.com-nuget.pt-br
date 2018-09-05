---
title: Referência do PowerShell aberta-PackagePage do NuGet
description: Referência de comando do PowerShell de PackagePage aberto no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0325aa4ddd718a901dd6a09cdf86cae260e326ab
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547162"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="46c9d-103">Open-PackagePage (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="46c9d-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="46c9d-104">*Preterido no 3.0 ou superior; disponível somente dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="46c9d-104">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="46c9d-105">Inicia o navegador padrão com o projeto, a licença ou a URL para relatar abuso para o pacote especificado.</span><span class="sxs-lookup"><span data-stu-id="46c9d-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="46c9d-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="46c9d-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="46c9d-107">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="46c9d-107">Parameters</span></span>

| <span data-ttu-id="46c9d-108">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="46c9d-108">Parameter</span></span> | <span data-ttu-id="46c9d-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="46c9d-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="46c9d-110">Id</span><span class="sxs-lookup"><span data-stu-id="46c9d-110">Id</span></span> | <span data-ttu-id="46c9d-111">A ID do pacote do pacote desejado.</span><span class="sxs-lookup"><span data-stu-id="46c9d-111">The package ID of the desired package.</span></span> <span data-ttu-id="46c9d-112">-Id do comutador em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="46c9d-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="46c9d-113">Versão</span><span class="sxs-lookup"><span data-stu-id="46c9d-113">Version</span></span> | <span data-ttu-id="46c9d-114">A versão do pacote, padronizando para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="46c9d-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="46c9d-115">Origem</span><span class="sxs-lookup"><span data-stu-id="46c9d-115">Source</span></span> | <span data-ttu-id="46c9d-116">A origem do pacote, padronizando para a fonte selecionada na lista suspensa origem.</span><span class="sxs-lookup"><span data-stu-id="46c9d-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="46c9d-117">Licença</span><span class="sxs-lookup"><span data-stu-id="46c9d-117">License</span></span> | <span data-ttu-id="46c9d-118">Abre o navegador a URL de licença do pacote.</span><span class="sxs-lookup"><span data-stu-id="46c9d-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="46c9d-119">Se nem - licença nem - ReportAbuse for especificado, o navegador abre a URL do projeto do pacote.</span><span class="sxs-lookup"><span data-stu-id="46c9d-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="46c9d-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="46c9d-120">ReportAbuse</span></span> | <span data-ttu-id="46c9d-121">Abre o navegador a URL para relatar abuso do pacote.</span><span class="sxs-lookup"><span data-stu-id="46c9d-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="46c9d-122">Se nem - licença nem - ReportAbuse for especificado, o navegador abre a URL do projeto do pacote.</span><span class="sxs-lookup"><span data-stu-id="46c9d-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="46c9d-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="46c9d-123">PassThru</span></span> | <span data-ttu-id="46c9d-124">Exibe a URL; Use com - WhatIf para suprimir abrindo o navegador.</span><span class="sxs-lookup"><span data-stu-id="46c9d-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="46c9d-125">Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="46c9d-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="46c9d-126">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="46c9d-126">Common Parameters</span></span>

<span data-ttu-id="46c9d-127">`Open-PackagePage` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="46c9d-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="46c9d-128">Exemplos</span><span class="sxs-lookup"><span data-stu-id="46c9d-128">Examples</span></span>

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```