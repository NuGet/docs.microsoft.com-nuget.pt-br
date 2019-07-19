---
title: Referência do PowerShell Get-Project do NuGet
description: Referência para o comando GetProject PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 830746f032bb4eb916508ef320c5b3d0486b89a4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327353"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="4751d-103">Get-Project (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4751d-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4751d-104">*Disponível somente dentro do [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="4751d-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="4751d-105">Exibe informações sobre o projeto padrão ou especificado.</span><span class="sxs-lookup"><span data-stu-id="4751d-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="4751d-106">`Get-Project`especificamente retorna um referent para o objeto DTE (ambiente de ferramentas de desenvolvimento) do Visual Studio para o projeto.</span><span class="sxs-lookup"><span data-stu-id="4751d-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="4751d-107">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="4751d-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="4751d-108">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="4751d-108">Parameters</span></span>

| <span data-ttu-id="4751d-109">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="4751d-109">Parameter</span></span> | <span data-ttu-id="4751d-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="4751d-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4751d-111">Nome</span><span class="sxs-lookup"><span data-stu-id="4751d-111">Name</span></span> | <span data-ttu-id="4751d-112">Especifica o projeto a ser exibido, padronizando para o projeto padrão selecionado no console do Gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="4751d-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="4751d-113">A opção-Name é opcional.</span><span class="sxs-lookup"><span data-stu-id="4751d-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="4751d-114">Todos</span><span class="sxs-lookup"><span data-stu-id="4751d-114">All</span></span> | <span data-ttu-id="4751d-115">Exibe informações para cada projeto na solução; a ordem dos projetos não é determinística.</span><span class="sxs-lookup"><span data-stu-id="4751d-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="4751d-116">Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="4751d-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4751d-117">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="4751d-117">Common Parameters</span></span>

<span data-ttu-id="4751d-118">`Get-Project`o oferece suporte aos seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="4751d-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4751d-119">Exemplos</span><span class="sxs-lookup"><span data-stu-id="4751d-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```