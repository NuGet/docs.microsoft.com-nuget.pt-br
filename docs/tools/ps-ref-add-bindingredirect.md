---
title: Referência do PowerShell do NuGet BindingRedirect adicionar
description: Referência de comando do PowerShell Add-BindingRedirect no Console do Gerenciador de pacotes do NuGet no Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7f1f2ef23e54ee48b577a2796b7f7b5f4c7eb284
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="78f7a-103">Add-BindingRedirect (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="78f7a-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="78f7a-104">*Disponível apenas dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="78f7a-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="78f7a-105">Examina todos os assemblies no caminho de saída para um projeto e adiciona redirecionamentos de associação para o arquivo de configuração do aplicativo ou da web, quando necessário.</span><span class="sxs-lookup"><span data-stu-id="78f7a-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="78f7a-106">Esse comando é executado automaticamente quando a instalação de um pacote.</span><span class="sxs-lookup"><span data-stu-id="78f7a-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="78f7a-107">Para obter detalhes sobre associação redirecionamentos e por que eles são usados, consulte [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) na documentação do .NET.</span><span class="sxs-lookup"><span data-stu-id="78f7a-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="78f7a-108">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="78f7a-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="78f7a-109">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="78f7a-109">Parameters</span></span>

| <span data-ttu-id="78f7a-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="78f7a-110">Parameter</span></span> | <span data-ttu-id="78f7a-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="78f7a-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="78f7a-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="78f7a-112">ProjectName</span></span> | <span data-ttu-id="78f7a-113">(Obrigatório) O projeto ao qual adicionar redirecionamentos de associação.</span><span class="sxs-lookup"><span data-stu-id="78f7a-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="78f7a-114">A opção - ProjectName em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="78f7a-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="78f7a-115">Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="78f7a-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="78f7a-116">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="78f7a-116">Common Parameters</span></span>

<span data-ttu-id="78f7a-117">`Add-BindingRedirect` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="78f7a-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="78f7a-118">Exemplos</span><span class="sxs-lookup"><span data-stu-id="78f7a-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```