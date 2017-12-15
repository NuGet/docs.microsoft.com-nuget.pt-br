---
title: "Referência do PowerShell do NuGet Open-PackagePage | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: e9f84530-6b3d-43b0-a832-0acb2997f6fc
description: "Referência de comando do PowerShell PackagePage abrir no Console do Gerenciador de pacotes do NuGet no Visual Studio."
keywords: "Pacote de NuGet manager console, comandos do Powershell do NuGet, referência do Powershell do NuGet, abrir PackagePage"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ec4310ea9d13926b1cb3b227b17016742a70bc16
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="d43cd-104">Abra-PackagePage (Console de Gerenciador de pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d43cd-104">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d43cd-105">*Preterido no 3.0 +; disponível apenas dentro de [NuGet Package Manager Console](Package-Manager-Console.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="d43cd-105">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="d43cd-106">Inicia o navegador padrão com o projeto, a licença ou a URL para o pacote especificado abuso.</span><span class="sxs-lookup"><span data-stu-id="d43cd-106">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="d43cd-107">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="d43cd-107">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="d43cd-108">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="d43cd-108">Parameters</span></span>

| <span data-ttu-id="d43cd-109">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d43cd-109">Parameter</span></span> | <span data-ttu-id="d43cd-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="d43cd-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d43cd-111">Id</span><span class="sxs-lookup"><span data-stu-id="d43cd-111">Id</span></span> | <span data-ttu-id="d43cd-112">A ID do pacote do pacote desejado.</span><span class="sxs-lookup"><span data-stu-id="d43cd-112">The package ID of the desired package.</span></span> <span data-ttu-id="d43cd-113">-Id switch é opcional.</span><span class="sxs-lookup"><span data-stu-id="d43cd-113">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="d43cd-114">Versão</span><span class="sxs-lookup"><span data-stu-id="d43cd-114">Version</span></span> | <span data-ttu-id="d43cd-115">A versão do pacote, o padrão para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="d43cd-115">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="d43cd-116">Origem</span><span class="sxs-lookup"><span data-stu-id="d43cd-116">Source</span></span> | <span data-ttu-id="d43cd-117">A origem do pacote, o padrão para a fonte selecionada na fonte de lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="d43cd-117">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="d43cd-118">Licença</span><span class="sxs-lookup"><span data-stu-id="d43cd-118">License</span></span> | <span data-ttu-id="d43cd-119">Abre o navegador a URL de licença do pacote.</span><span class="sxs-lookup"><span data-stu-id="d43cd-119">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="d43cd-120">Se - licença nem - ReportAbuse for especificado, o navegador abre a URL do projeto do pacote.</span><span class="sxs-lookup"><span data-stu-id="d43cd-120">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="d43cd-121">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="d43cd-121">ReportAbuse</span></span> | <span data-ttu-id="d43cd-122">Abre o navegador a URL de abuso de relatório do pacote.</span><span class="sxs-lookup"><span data-stu-id="d43cd-122">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="d43cd-123">Se - licença nem - ReportAbuse for especificado, o navegador abre a URL do projeto do pacote.</span><span class="sxs-lookup"><span data-stu-id="d43cd-123">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="d43cd-124">Passagem</span><span class="sxs-lookup"><span data-stu-id="d43cd-124">PassThru</span></span> | <span data-ttu-id="d43cd-125">Exibe a URL; Use com - WhatIf para suprimir a abrir o navegador.</span><span class="sxs-lookup"><span data-stu-id="d43cd-125">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="d43cd-126">Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="d43cd-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d43cd-127">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="d43cd-127">Common Parameters</span></span>

<span data-ttu-id="d43cd-128">`Open-PackagePage`suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d43cd-128">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d43cd-129">Exemplos</span><span class="sxs-lookup"><span data-stu-id="d43cd-129">Examples</span></span>

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