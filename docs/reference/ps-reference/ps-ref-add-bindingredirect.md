---
title: Referência do PowerShell para Add-BindingRedirect do NuGet
description: Referência para o comando Add-BindingRedirect PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d3d156cf882229260e8cf55f8ece2804aec36dc9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384978"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="84fdf-103">Add-BindingRedirect (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="84fdf-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="84fdf-104">*Disponível somente dentro do [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="84fdf-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="84fdf-105">Examina todos os assemblies no caminho de saída de um projeto e adiciona redirecionamentos de associação ao aplicativo ou ao arquivo de configuração da Web, quando necessário.</span><span class="sxs-lookup"><span data-stu-id="84fdf-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="84fdf-106">Esse comando é executado automaticamente ao instalar um pacote.</span><span class="sxs-lookup"><span data-stu-id="84fdf-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="84fdf-107">Para obter detalhes sobre redirecionamentos de associação e por que eles são usados, consulte [Redirecionando versões de assembly](/dotnet/framework/configure-apps/redirect-assembly-versions) na documentação do .net.</span><span class="sxs-lookup"><span data-stu-id="84fdf-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="84fdf-108">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="84fdf-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="84fdf-109">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="84fdf-109">Parameters</span></span>

| <span data-ttu-id="84fdf-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="84fdf-110">Parameter</span></span> | <span data-ttu-id="84fdf-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="84fdf-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="84fdf-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="84fdf-112">ProjectName</span></span> | <span data-ttu-id="84fdf-113">Necessária O projeto ao qual adicionar redirecionamentos de associação.</span><span class="sxs-lookup"><span data-stu-id="84fdf-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="84fdf-114">A opção-ProjectName em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="84fdf-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="84fdf-115">Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="84fdf-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="84fdf-116">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="84fdf-116">Common Parameters</span></span>

<span data-ttu-id="84fdf-117">o `Add-BindingRedirect` dá suporte aos seguintes [parâmetros comuns do PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="84fdf-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="84fdf-118">Exemplos</span><span class="sxs-lookup"><span data-stu-id="84fdf-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```