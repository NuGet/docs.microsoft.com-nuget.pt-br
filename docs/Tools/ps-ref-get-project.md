---
title: "Referência do PowerShell Get-projeto NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência de comando do GetProject PowerShell no Console do Gerenciador de pacotes do NuGet no Visual Studio."
keywords: "Pacote de NuGet manager console, comandos do Powershell do NuGet, referência do Powershell do NuGet, Get-projeto"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c347a6104d89bb29626ad7c2f33bec150eb38cd2
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="c3525-104">Get-projeto (Console de Gerenciador de pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="c3525-104">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="c3525-105">*Disponível apenas dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="c3525-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="c3525-106">Exibe informações sobre o padrão ou o projeto especificado.</span><span class="sxs-lookup"><span data-stu-id="c3525-106">Displays information about the default or specified project.</span></span> <span data-ttu-id="c3525-107">`Get-Project` Especificamente, retorna um referente ao objeto DTE (ambiente de ferramentas de desenvolvimento) do Visual Studio para o projeto.</span><span class="sxs-lookup"><span data-stu-id="c3525-107">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="c3525-108">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="c3525-108">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="c3525-109">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="c3525-109">Parameters</span></span>

| <span data-ttu-id="c3525-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c3525-110">Parameter</span></span> | <span data-ttu-id="c3525-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="c3525-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c3525-112">Nome</span><span class="sxs-lookup"><span data-stu-id="c3525-112">Name</span></span> | <span data-ttu-id="c3525-113">Especifica o projeto a ser exibido, padronizando para o projeto padrão selecionado no Console do Gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="c3525-113">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="c3525-114">-Nome do comutador é opcional.</span><span class="sxs-lookup"><span data-stu-id="c3525-114">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="c3525-115">Todos</span><span class="sxs-lookup"><span data-stu-id="c3525-115">All</span></span> | <span data-ttu-id="c3525-116">Exibe as informações de todos os projetos na solução. a ordem dos projetos não é determinística.</span><span class="sxs-lookup"><span data-stu-id="c3525-116">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="c3525-117">Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="c3525-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="c3525-118">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="c3525-118">Common Parameters</span></span>

<span data-ttu-id="c3525-119">`Get-Project` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c3525-119">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="c3525-120">Exemplos</span><span class="sxs-lookup"><span data-stu-id="c3525-120">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```