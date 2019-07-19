---
title: Referência do PowerShell open-PackagePage do NuGet
description: Referência para o comando Open-PackagePage do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0237c23d81000a1d58264cc0ab48c73d819d0e5a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327373"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="1a103-103">Open-PackagePage (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="1a103-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="1a103-104">*Preterido em 3.0 +; disponível somente dentro do [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="1a103-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="1a103-105">Inicia o navegador padrão com o projeto, a licença ou a URL de abuso de relatório para o pacote especificado.</span><span class="sxs-lookup"><span data-stu-id="1a103-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="1a103-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="1a103-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="1a103-107">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a103-107">Parameters</span></span>

| <span data-ttu-id="1a103-108">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a103-108">Parameter</span></span> | <span data-ttu-id="1a103-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a103-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1a103-110">Id</span><span class="sxs-lookup"><span data-stu-id="1a103-110">Id</span></span> | <span data-ttu-id="1a103-111">A ID do pacote desejado.</span><span class="sxs-lookup"><span data-stu-id="1a103-111">The package ID of the desired package.</span></span> <span data-ttu-id="1a103-112">A opção-ID em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="1a103-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="1a103-113">Versão</span><span class="sxs-lookup"><span data-stu-id="1a103-113">Version</span></span> | <span data-ttu-id="1a103-114">A versão do pacote, padronizando para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="1a103-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="1a103-115">Origem</span><span class="sxs-lookup"><span data-stu-id="1a103-115">Source</span></span> | <span data-ttu-id="1a103-116">A origem do pacote, padronizando para a origem selecionada na lista suspensa origem.</span><span class="sxs-lookup"><span data-stu-id="1a103-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="1a103-117">Licença</span><span class="sxs-lookup"><span data-stu-id="1a103-117">License</span></span> | <span data-ttu-id="1a103-118">Abre o navegador para a URL de licença do pacote.</span><span class="sxs-lookup"><span data-stu-id="1a103-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="1a103-119">Se nem-License nem-ReportAbuse for especificado, o navegador abrirá a URL do projeto do pacote.</span><span class="sxs-lookup"><span data-stu-id="1a103-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="1a103-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="1a103-120">ReportAbuse</span></span> | <span data-ttu-id="1a103-121">Abre o navegador para a URL de abuso de relatório do pacote.</span><span class="sxs-lookup"><span data-stu-id="1a103-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="1a103-122">Se nem-License nem-ReportAbuse for especificado, o navegador abrirá a URL do projeto do pacote.</span><span class="sxs-lookup"><span data-stu-id="1a103-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="1a103-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="1a103-123">PassThru</span></span> | <span data-ttu-id="1a103-124">Exibe a URL; Use com-WhatIf para suprimir a abertura do navegador.</span><span class="sxs-lookup"><span data-stu-id="1a103-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="1a103-125">Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="1a103-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="1a103-126">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="1a103-126">Common Parameters</span></span>

<span data-ttu-id="1a103-127">`Open-PackagePage`o oferece suporte aos seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="1a103-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="1a103-128">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a103-128">Examples</span></span>

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