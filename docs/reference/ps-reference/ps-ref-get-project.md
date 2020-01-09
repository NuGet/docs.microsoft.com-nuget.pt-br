---
title: Referência do PowerShell Get-Project do NuGet
description: Referência para o comando GetProject PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 3343952535c2d3c822f5cac24cb30c8f5bfa5be3
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384614"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="0ad8b-103">Get-Project (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="0ad8b-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="0ad8b-104">*Disponível somente dentro do [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="0ad8b-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="0ad8b-105">Exibe informações sobre o projeto padrão ou especificado.</span><span class="sxs-lookup"><span data-stu-id="0ad8b-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="0ad8b-106">`Get-Project` retorna especificamente um referent para o objeto DTE (ambiente de ferramentas de desenvolvimento) do Visual Studio para o projeto.</span><span class="sxs-lookup"><span data-stu-id="0ad8b-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="0ad8b-107">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="0ad8b-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="0ad8b-108">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="0ad8b-108">Parameters</span></span>

| <span data-ttu-id="0ad8b-109">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="0ad8b-109">Parameter</span></span> | <span data-ttu-id="0ad8b-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="0ad8b-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0ad8b-111">Name</span><span class="sxs-lookup"><span data-stu-id="0ad8b-111">Name</span></span> | <span data-ttu-id="0ad8b-112">Especifica o projeto a ser exibido, padronizando para o projeto padrão selecionado no console do Gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="0ad8b-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="0ad8b-113">A opção-Name é opcional.</span><span class="sxs-lookup"><span data-stu-id="0ad8b-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="0ad8b-114">{1&gt;Todos&lt;1}</span><span class="sxs-lookup"><span data-stu-id="0ad8b-114">All</span></span> | <span data-ttu-id="0ad8b-115">Exibe informações para cada projeto na solução; a ordem dos projetos não é determinística.</span><span class="sxs-lookup"><span data-stu-id="0ad8b-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="0ad8b-116">Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="0ad8b-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="0ad8b-117">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="0ad8b-117">Common Parameters</span></span>

<span data-ttu-id="0ad8b-118">o `Get-Project` dá suporte aos seguintes [parâmetros comuns do PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="0ad8b-118">`Get-Project` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="0ad8b-119">Exemplos</span><span class="sxs-lookup"><span data-stu-id="0ad8b-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```