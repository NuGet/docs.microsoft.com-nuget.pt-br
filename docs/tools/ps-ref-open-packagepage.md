---
title: Referência do PowerShell aberta-PackagePage do NuGet
description: Referência de comando do PowerShell de PackagePage aberto no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fd738f15b461051c4e9413b3035456c687979b97
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842260"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="f4ab0-103">Open-PackagePage (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f4ab0-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f4ab0-104">*Preterido no 3.0 ou superior; disponível somente dentro de [Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="f4ab0-104">*Deprecated in 3.0+; available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f4ab0-105">Inicia o navegador padrão com o projeto, a licença ou a URL para relatar abuso para o pacote especificado.</span><span class="sxs-lookup"><span data-stu-id="f4ab0-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="f4ab0-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="f4ab0-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f4ab0-107">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="f4ab0-107">Parameters</span></span>

| <span data-ttu-id="f4ab0-108">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="f4ab0-108">Parameter</span></span> | <span data-ttu-id="f4ab0-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="f4ab0-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f4ab0-110">Id</span><span class="sxs-lookup"><span data-stu-id="f4ab0-110">Id</span></span> | <span data-ttu-id="f4ab0-111">A ID do pacote do pacote desejado.</span><span class="sxs-lookup"><span data-stu-id="f4ab0-111">The package ID of the desired package.</span></span> <span data-ttu-id="f4ab0-112">-Id do comutador em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="f4ab0-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="f4ab0-113">Versão</span><span class="sxs-lookup"><span data-stu-id="f4ab0-113">Version</span></span> | <span data-ttu-id="f4ab0-114">A versão do pacote, padronizando para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="f4ab0-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="f4ab0-115">Origem</span><span class="sxs-lookup"><span data-stu-id="f4ab0-115">Source</span></span> | <span data-ttu-id="f4ab0-116">A origem do pacote, padronizando para a fonte selecionada na lista suspensa origem.</span><span class="sxs-lookup"><span data-stu-id="f4ab0-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="f4ab0-117">Licença</span><span class="sxs-lookup"><span data-stu-id="f4ab0-117">License</span></span> | <span data-ttu-id="f4ab0-118">Abre o navegador a URL de licença do pacote.</span><span class="sxs-lookup"><span data-stu-id="f4ab0-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="f4ab0-119">Se nem - licença nem - ReportAbuse for especificado, o navegador abre a URL do projeto do pacote.</span><span class="sxs-lookup"><span data-stu-id="f4ab0-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="f4ab0-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="f4ab0-120">ReportAbuse</span></span> | <span data-ttu-id="f4ab0-121">Abre o navegador a URL para relatar abuso do pacote.</span><span class="sxs-lookup"><span data-stu-id="f4ab0-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="f4ab0-122">Se nem - licença nem - ReportAbuse for especificado, o navegador abre a URL do projeto do pacote.</span><span class="sxs-lookup"><span data-stu-id="f4ab0-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="f4ab0-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="f4ab0-123">PassThru</span></span> | <span data-ttu-id="f4ab0-124">Exibe a URL; Use com - WhatIf para suprimir abrindo o navegador.</span><span class="sxs-lookup"><span data-stu-id="f4ab0-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="f4ab0-125">Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="f4ab0-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f4ab0-126">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="f4ab0-126">Common Parameters</span></span>

<span data-ttu-id="f4ab0-127">`Open-PackagePage` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f4ab0-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f4ab0-128">Exemplos</span><span class="sxs-lookup"><span data-stu-id="f4ab0-128">Examples</span></span>

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