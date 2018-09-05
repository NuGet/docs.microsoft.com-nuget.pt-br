---
title: Referência do PowerShell NuGet Uninstall-Package
description: Referência de comando do PowerShell de pacote de desinstalação no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ae60473fbb716b23f40b0605be8aaa8515802315
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551637"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f7492-103">Uninstall-Package (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f7492-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f7492-104">*Este tópico descreve o comando dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows. Para o comando genérico do pacote de desinstalação do PowerShell, consulte o [referência do PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="f7492-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="f7492-105">Remove um pacote de um projeto, opcionalmente, removendo suas dependências.</span><span class="sxs-lookup"><span data-stu-id="f7492-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="f7492-106">Se outros pacotes dependem deste pacote, o comando falhará a menos que – Force a opção for especificada.</span><span class="sxs-lookup"><span data-stu-id="f7492-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="f7492-107">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="f7492-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="f7492-108">Se outros pacotes dependem deste pacote, o comando falhará a menos que – Force a opção for especificada.</span><span class="sxs-lookup"><span data-stu-id="f7492-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="f7492-109">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="f7492-109">Parameters</span></span>

| <span data-ttu-id="f7492-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="f7492-110">Parameter</span></span> | <span data-ttu-id="f7492-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="f7492-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f7492-112">Id</span><span class="sxs-lookup"><span data-stu-id="f7492-112">Id</span></span> | <span data-ttu-id="f7492-113">(Obrigatório) O identificador do pacote a desinstalar.</span><span class="sxs-lookup"><span data-stu-id="f7492-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="f7492-114">-Id do comutador em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="f7492-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="f7492-115">Versão</span><span class="sxs-lookup"><span data-stu-id="f7492-115">Version</span></span> | <span data-ttu-id="f7492-116">A versão do pacote para desinstalar, padronizando para a versão atualmente instalada.</span><span class="sxs-lookup"><span data-stu-id="f7492-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="f7492-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="f7492-117">RemoveDependencies</span></span> | <span data-ttu-id="f7492-118">Desinstale o pacote e suas dependências não utilizadas.</span><span class="sxs-lookup"><span data-stu-id="f7492-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="f7492-119">Ou seja, se qualquer dependência tiver outro pacote que depende dele, ele será ignorado.</span><span class="sxs-lookup"><span data-stu-id="f7492-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="f7492-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="f7492-120">ProjectName</span></span> | <span data-ttu-id="f7492-121">O projeto do qual deseja desinstalar o pacote, padronizando para o projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="f7492-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="f7492-122">Force</span><span class="sxs-lookup"><span data-stu-id="f7492-122">Force</span></span> | <span data-ttu-id="f7492-123">Força um pacote a ser desinstalado, mesmo se outros pacotes dependem dele.</span><span class="sxs-lookup"><span data-stu-id="f7492-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="f7492-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="f7492-124">WhatIf</span></span> | <span data-ttu-id="f7492-125">Mostra o que aconteceria ao executar o comando sem realmente executar a desinstalação.</span><span class="sxs-lookup"><span data-stu-id="f7492-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="f7492-126">Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="f7492-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f7492-127">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="f7492-127">Common Parameters</span></span>

<span data-ttu-id="f7492-128">`Uninstall-Package` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f7492-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f7492-129">Exemplos</span><span class="sxs-lookup"><span data-stu-id="f7492-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
