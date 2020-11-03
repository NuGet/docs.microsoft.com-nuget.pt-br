---
title: Referência do NuGet Add-BindingRedirect PowerShell
description: Referência para Add-BindingRedirect comando do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 382ba9b179428c70e3eb16db86a363e095207d61
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237251"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="01698-103">Add-BindingRedirect (console do Gerenciador de pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="01698-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="01698-104">*Disponível somente dentro do [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="01698-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="01698-105">Examina todos os assemblies no caminho de saída de um projeto e adiciona redirecionamentos de associação ao aplicativo ou ao arquivo de configuração da Web, quando necessário.</span><span class="sxs-lookup"><span data-stu-id="01698-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="01698-106">Esse comando é executado automaticamente ao instalar um pacote.</span><span class="sxs-lookup"><span data-stu-id="01698-106">This command is run automatically when installing a package.</span></span>

> [!NOTE]
> <span data-ttu-id="01698-107">Isso se aplica somente a cenários que usam um arquivo packages.config.</span><span class="sxs-lookup"><span data-stu-id="01698-107">This only applies to scenarios using a packages.config file.</span></span> <span data-ttu-id="01698-108">Para obter mais informações, consulte [referência de arquivo NuGet packages.config](~/reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="01698-108">For more information, see [NuGet packages.config file reference](~/reference/packages-config.md).</span></span>

<span data-ttu-id="01698-109">Para obter detalhes sobre redirecionamentos de associação e por que eles são usados, consulte [Redirecionando versões de assembly](/dotnet/framework/configure-apps/redirect-assembly-versions) na documentação do .net.</span><span class="sxs-lookup"><span data-stu-id="01698-109">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="01698-110">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="01698-110">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="01698-111">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="01698-111">Parameters</span></span>

| <span data-ttu-id="01698-112">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="01698-112">Parameter</span></span> | <span data-ttu-id="01698-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="01698-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="01698-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="01698-114">ProjectName</span></span> | <span data-ttu-id="01698-115">Necessária O projeto ao qual adicionar redirecionamentos de associação.</span><span class="sxs-lookup"><span data-stu-id="01698-115">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="01698-116">A opção-ProjectName em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="01698-116">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="01698-117">Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="01698-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="01698-118">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="01698-118">Common Parameters</span></span>

<span data-ttu-id="01698-119">`Add-BindingRedirect` o oferece suporte aos seguintes [parâmetros comuns do PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="01698-119">`Add-BindingRedirect` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="01698-120">Exemplos</span><span class="sxs-lookup"><span data-stu-id="01698-120">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```