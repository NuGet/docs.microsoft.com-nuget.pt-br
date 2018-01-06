---
title: "Referência do PowerShell do NuGet BindingRedirect adicionar | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 90f4dcb0-6e5a-4948-8ea9-62e0d061d95a
description: "Referência de comando do PowerShell Add-BindingRedirect no Console do Gerenciador de pacotes do NuGet no Visual Studio."
keywords: "Pacote de NuGet manager console, comandos do Powershell do NuGet, referência do Powershell do NuGet, adicionar BindingRedirect"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6a3232af925f75713168421e68f2773060c5ebaa
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="ad6b2-104">Adicionar-BindingRedirect (Console de Gerenciador de pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="ad6b2-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ad6b2-105">*Disponível apenas dentro de [NuGet Package Manager Console](Package-Manager-Console.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="ad6b2-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="ad6b2-106">Examina todos os assemblies no caminho de saída para um projeto e adiciona redirecionamentos de associação para o arquivo de configuração do aplicativo ou da web, quando necessário.</span><span class="sxs-lookup"><span data-stu-id="ad6b2-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="ad6b2-107">Esse comando é executado automaticamente quando a instalação de um pacote.</span><span class="sxs-lookup"><span data-stu-id="ad6b2-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="ad6b2-108">Para obter detalhes sobre associação redirecionamentos e por que eles são usados, consulte [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) na documentação do .NET.</span><span class="sxs-lookup"><span data-stu-id="ad6b2-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="ad6b2-109">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="ad6b2-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="ad6b2-110">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="ad6b2-110">Parameters</span></span>

| <span data-ttu-id="ad6b2-111">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="ad6b2-111">Parameter</span></span> | <span data-ttu-id="ad6b2-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="ad6b2-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ad6b2-113">ProjectName</span><span class="sxs-lookup"><span data-stu-id="ad6b2-113">ProjectName</span></span> | <span data-ttu-id="ad6b2-114">(Obrigatório) O projeto ao qual adicionar redirecionamentos de associação.</span><span class="sxs-lookup"><span data-stu-id="ad6b2-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="ad6b2-115">A opção - ProjectName em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="ad6b2-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="ad6b2-116">Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="ad6b2-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ad6b2-117">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="ad6b2-117">Common Parameters</span></span>

<span data-ttu-id="ad6b2-118">`Add-BindingRedirect`suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="ad6b2-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ad6b2-119">Exemplos</span><span class="sxs-lookup"><span data-stu-id="ad6b2-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```