---
title: Referência de PowerShell do NuGet Uninstall-Package | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referência de comando do PowerShell do pacote de desinstalação no Console do Gerenciador de pacotes do NuGet no Visual Studio.
keywords: Console do Gerenciador, comandos do Powershell do NuGet, referência do Powershell do NuGet, pacote de desinstalação do pacote NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: b53a36a6456522aa0d9d0d7cdf412de464ba9e08
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="e53f8-104">Uninstall-Package (Console de Gerenciador de pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e53f8-104">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e53f8-105">*Este tópico descreve o comando dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows. Para o comando genérico do pacote de desinstalação do PowerShell, consulte o [referência do PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="e53f8-105">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="e53f8-106">Remove um pacote de um projeto, opcionalmente, a remoção de suas dependências.</span><span class="sxs-lookup"><span data-stu-id="e53f8-106">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="e53f8-107">Se outros pacotes dependerem deste pacote, o comando falhará, a menos que – Force opção é especificada.</span><span class="sxs-lookup"><span data-stu-id="e53f8-107">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="e53f8-108">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="e53f8-108">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="e53f8-109">Se outros pacotes dependerem deste pacote, o comando falhará, a menos que – Force opção é especificada.</span><span class="sxs-lookup"><span data-stu-id="e53f8-109">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="e53f8-110">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="e53f8-110">Parameters</span></span>

| <span data-ttu-id="e53f8-111">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e53f8-111">Parameter</span></span> | <span data-ttu-id="e53f8-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="e53f8-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e53f8-113">Id</span><span class="sxs-lookup"><span data-stu-id="e53f8-113">Id</span></span> | <span data-ttu-id="e53f8-114">(Obrigatório) O identificador do pacote a ser desinstalado.</span><span class="sxs-lookup"><span data-stu-id="e53f8-114">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="e53f8-115">-Id switch é opcional.</span><span class="sxs-lookup"><span data-stu-id="e53f8-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="e53f8-116">Versão</span><span class="sxs-lookup"><span data-stu-id="e53f8-116">Version</span></span> | <span data-ttu-id="e53f8-117">A versão do pacote para desinstalar, padronizando para a versão atualmente instalada.</span><span class="sxs-lookup"><span data-stu-id="e53f8-117">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="e53f8-118">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="e53f8-118">RemoveDependencies</span></span> | <span data-ttu-id="e53f8-119">Desinstale o pacote e suas dependências não usadas.</span><span class="sxs-lookup"><span data-stu-id="e53f8-119">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="e53f8-120">Ou seja, se qualquer dependência tiver outro pacote que depende dele, ele é ignorado.</span><span class="sxs-lookup"><span data-stu-id="e53f8-120">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="e53f8-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="e53f8-121">ProjectName</span></span> | <span data-ttu-id="e53f8-122">O projeto do qual deseja desinstalar o pacote, o padrão para o projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="e53f8-122">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="e53f8-123">Force</span><span class="sxs-lookup"><span data-stu-id="e53f8-123">Force</span></span> | <span data-ttu-id="e53f8-124">Força um pacote a ser desinstalado, mesmo se outros pacotes dependem dele.</span><span class="sxs-lookup"><span data-stu-id="e53f8-124">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="e53f8-125">WhatIf</span><span class="sxs-lookup"><span data-stu-id="e53f8-125">WhatIf</span></span> | <span data-ttu-id="e53f8-126">Mostra o que aconteceria quando a execução do comando sem realmente executar a desinstalação.</span><span class="sxs-lookup"><span data-stu-id="e53f8-126">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="e53f8-127">Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="e53f8-127">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e53f8-128">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="e53f8-128">Common Parameters</span></span>

<span data-ttu-id="e53f8-129">`Uninstall-Package` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e53f8-129">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e53f8-130">Exemplos</span><span class="sxs-lookup"><span data-stu-id="e53f8-130">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
