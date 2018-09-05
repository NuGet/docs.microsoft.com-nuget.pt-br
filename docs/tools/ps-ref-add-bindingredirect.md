---
title: Referência do PowerShell BindingRedirect adicionar NuGet
description: Referência de comando do PowerShell Add-BindingRedirect no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: dec7db04c5cf239863b9c00e9f5bc0dde42c7e47
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551651"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="40e60-103">Add-BindingRedirect (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="40e60-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="40e60-104">*Disponível somente dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="40e60-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="40e60-105">Examina todos os assemblies no caminho de saída para um projeto e adiciona redirecionamentos de ligação ao arquivo de configuração da web ou aplicativo, onde for necessário.</span><span class="sxs-lookup"><span data-stu-id="40e60-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="40e60-106">Esse comando é executado automaticamente ao instalar um pacote.</span><span class="sxs-lookup"><span data-stu-id="40e60-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="40e60-107">Para obter detalhes sobre associação de redirecionamentos e por que eles são usados, consulte [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) na documentação do .NET.</span><span class="sxs-lookup"><span data-stu-id="40e60-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="40e60-108">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="40e60-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="40e60-109">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="40e60-109">Parameters</span></span>

| <span data-ttu-id="40e60-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="40e60-110">Parameter</span></span> | <span data-ttu-id="40e60-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="40e60-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="40e60-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="40e60-112">ProjectName</span></span> | <span data-ttu-id="40e60-113">(Obrigatório) O projeto ao qual adicionar redirecionamentos de associação.</span><span class="sxs-lookup"><span data-stu-id="40e60-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="40e60-114">O comutador - ProjectName em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="40e60-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="40e60-115">Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="40e60-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="40e60-116">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="40e60-116">Common Parameters</span></span>

<span data-ttu-id="40e60-117">`Add-BindingRedirect` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="40e60-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="40e60-118">Exemplos</span><span class="sxs-lookup"><span data-stu-id="40e60-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```