---
title: Referência do PowerShell Get-projeto NuGet
description: Referência de comando do GetProject PowerShell no Console do Gerenciador de pacotes do NuGet no Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: afdf9f762bbd34531f9d9093238a2fed27e3f4d3
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817750"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="a2bea-103">Get-Project (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="a2bea-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a2bea-104">*Disponível apenas dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="a2bea-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="a2bea-105">Exibe informações sobre o padrão ou o projeto especificado.</span><span class="sxs-lookup"><span data-stu-id="a2bea-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="a2bea-106">`Get-Project` Especificamente, retorna um referente ao objeto DTE (ambiente de ferramentas de desenvolvimento) do Visual Studio para o projeto.</span><span class="sxs-lookup"><span data-stu-id="a2bea-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="a2bea-107">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="a2bea-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a2bea-108">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="a2bea-108">Parameters</span></span>

| <span data-ttu-id="a2bea-109">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="a2bea-109">Parameter</span></span> | <span data-ttu-id="a2bea-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="a2bea-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a2bea-111">Nome</span><span class="sxs-lookup"><span data-stu-id="a2bea-111">Name</span></span> | <span data-ttu-id="a2bea-112">Especifica o projeto a ser exibido, padronizando para o projeto padrão selecionado no Console do Gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="a2bea-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="a2bea-113">-Nome do comutador é opcional.</span><span class="sxs-lookup"><span data-stu-id="a2bea-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="a2bea-114">Todos</span><span class="sxs-lookup"><span data-stu-id="a2bea-114">All</span></span> | <span data-ttu-id="a2bea-115">Exibe as informações de todos os projetos na solução. a ordem dos projetos não é determinística.</span><span class="sxs-lookup"><span data-stu-id="a2bea-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="a2bea-116">Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="a2bea-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a2bea-117">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="a2bea-117">Common Parameters</span></span>

<span data-ttu-id="a2bea-118">`Get-Project` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="a2bea-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a2bea-119">Exemplos</span><span class="sxs-lookup"><span data-stu-id="a2bea-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```