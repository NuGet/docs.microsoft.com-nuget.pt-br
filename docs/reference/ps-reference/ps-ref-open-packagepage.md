---
title: Referência do PowerShell open-PackagePage do NuGet
description: Referência para o comando Open-PackagePage do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 39199ebfc37756ed40158a1c07afca7709067350
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384422"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="1c973-103">Open-PackagePage (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="1c973-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="1c973-104">*Preterido em 3.0 +; disponível somente dentro do [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="1c973-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="1c973-105">Inicia o navegador padrão com o projeto, a licença ou a URL de abuso de relatório para o pacote especificado.</span><span class="sxs-lookup"><span data-stu-id="1c973-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="1c973-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="1c973-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="1c973-107">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="1c973-107">Parameters</span></span>

| <span data-ttu-id="1c973-108">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1c973-108">Parameter</span></span> | <span data-ttu-id="1c973-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="1c973-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1c973-110">Id</span><span class="sxs-lookup"><span data-stu-id="1c973-110">Id</span></span> | <span data-ttu-id="1c973-111">A ID do pacote desejado.</span><span class="sxs-lookup"><span data-stu-id="1c973-111">The package ID of the desired package.</span></span> <span data-ttu-id="1c973-112">A opção-ID em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="1c973-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="1c973-113">Versão do</span><span class="sxs-lookup"><span data-stu-id="1c973-113">Version</span></span> | <span data-ttu-id="1c973-114">A versão do pacote, padronizando para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="1c973-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="1c973-115">Source</span><span class="sxs-lookup"><span data-stu-id="1c973-115">Source</span></span> | <span data-ttu-id="1c973-116">A origem do pacote, padronizando para a origem selecionada na lista suspensa origem.</span><span class="sxs-lookup"><span data-stu-id="1c973-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="1c973-117">Licença</span><span class="sxs-lookup"><span data-stu-id="1c973-117">License</span></span> | <span data-ttu-id="1c973-118">Abre o navegador para a URL de licença do pacote.</span><span class="sxs-lookup"><span data-stu-id="1c973-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="1c973-119">Se nem-License nem-ReportAbuse for especificado, o navegador abrirá a URL do projeto do pacote.</span><span class="sxs-lookup"><span data-stu-id="1c973-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="1c973-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="1c973-120">ReportAbuse</span></span> | <span data-ttu-id="1c973-121">Abre o navegador para a URL de abuso de relatório do pacote.</span><span class="sxs-lookup"><span data-stu-id="1c973-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="1c973-122">Se nem-License nem-ReportAbuse for especificado, o navegador abrirá a URL do projeto do pacote.</span><span class="sxs-lookup"><span data-stu-id="1c973-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="1c973-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="1c973-123">PassThru</span></span> | <span data-ttu-id="1c973-124">Exibe a URL; Use com-WhatIf para suprimir a abertura do navegador.</span><span class="sxs-lookup"><span data-stu-id="1c973-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="1c973-125">Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="1c973-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="1c973-126">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="1c973-126">Common Parameters</span></span>

<span data-ttu-id="1c973-127">o `Open-PackagePage` dá suporte aos seguintes [parâmetros comuns do PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="1c973-127">`Open-PackagePage` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="1c973-128">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1c973-128">Examples</span></span>

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