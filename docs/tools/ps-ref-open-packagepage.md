---
title: Referência do PowerShell do NuGet Open-PackagePage
description: Referência de comando do PowerShell PackagePage abrir no Console do Gerenciador de pacotes do NuGet no Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: df4bea390105a7e3fc5d2abd476f2908d92bbcf8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="07835-103">Open-PackagePage (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="07835-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="07835-104">*Preterido no 3.0 +; disponível apenas dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="07835-104">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="07835-105">Inicia o navegador padrão com o projeto, a licença ou a URL para o pacote especificado abuso.</span><span class="sxs-lookup"><span data-stu-id="07835-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="07835-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="07835-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="07835-107">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="07835-107">Parameters</span></span>

| <span data-ttu-id="07835-108">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="07835-108">Parameter</span></span> | <span data-ttu-id="07835-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="07835-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="07835-110">Id</span><span class="sxs-lookup"><span data-stu-id="07835-110">Id</span></span> | <span data-ttu-id="07835-111">A ID do pacote do pacote desejado.</span><span class="sxs-lookup"><span data-stu-id="07835-111">The package ID of the desired package.</span></span> <span data-ttu-id="07835-112">-Id switch é opcional.</span><span class="sxs-lookup"><span data-stu-id="07835-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="07835-113">Versão</span><span class="sxs-lookup"><span data-stu-id="07835-113">Version</span></span> | <span data-ttu-id="07835-114">A versão do pacote, o padrão para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="07835-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="07835-115">Origem</span><span class="sxs-lookup"><span data-stu-id="07835-115">Source</span></span> | <span data-ttu-id="07835-116">A origem do pacote, o padrão para a fonte selecionada na fonte de lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="07835-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="07835-117">Licença</span><span class="sxs-lookup"><span data-stu-id="07835-117">License</span></span> | <span data-ttu-id="07835-118">Abre o navegador a URL de licença do pacote.</span><span class="sxs-lookup"><span data-stu-id="07835-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="07835-119">Se - licença nem - ReportAbuse for especificado, o navegador abre a URL do projeto do pacote.</span><span class="sxs-lookup"><span data-stu-id="07835-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="07835-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="07835-120">ReportAbuse</span></span> | <span data-ttu-id="07835-121">Abre o navegador a URL de abuso de relatório do pacote.</span><span class="sxs-lookup"><span data-stu-id="07835-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="07835-122">Se - licença nem - ReportAbuse for especificado, o navegador abre a URL do projeto do pacote.</span><span class="sxs-lookup"><span data-stu-id="07835-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="07835-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="07835-123">PassThru</span></span> | <span data-ttu-id="07835-124">Exibe a URL; Use com - WhatIf para suprimir a abrir o navegador.</span><span class="sxs-lookup"><span data-stu-id="07835-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="07835-125">Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="07835-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="07835-126">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="07835-126">Common Parameters</span></span>

<span data-ttu-id="07835-127">`Open-PackagePage` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="07835-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="07835-128">Exemplos</span><span class="sxs-lookup"><span data-stu-id="07835-128">Examples</span></span>

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