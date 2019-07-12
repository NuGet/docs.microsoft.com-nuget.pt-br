---
title: Referência do PowerShell NuGet Uninstall-Package
description: Referência de comando do PowerShell de pacote de desinstalação no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: c95479103be2cba3b4eb6964ea761870477863bd
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842467"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="517fd-103">Uninstall-Package (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="517fd-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="517fd-104">*Este tópico descreve o comando dentro de [Package Manager Console](package-manager-console.md) no Visual Studio no Windows. Para o comando genérico do pacote de desinstalação do PowerShell, consulte o [referência do PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="517fd-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="517fd-105">Remove um pacote de um projeto, opcionalmente, removendo suas dependências.</span><span class="sxs-lookup"><span data-stu-id="517fd-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="517fd-106">Se outros pacotes dependem deste pacote, o comando falhará a menos que – Force a opção for especificada.</span><span class="sxs-lookup"><span data-stu-id="517fd-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="517fd-107">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="517fd-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="517fd-108">Se outros pacotes dependem deste pacote, o comando falhará a menos que – Force a opção for especificada.</span><span class="sxs-lookup"><span data-stu-id="517fd-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="517fd-109">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="517fd-109">Parameters</span></span>

| <span data-ttu-id="517fd-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="517fd-110">Parameter</span></span> | <span data-ttu-id="517fd-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="517fd-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="517fd-112">Id</span><span class="sxs-lookup"><span data-stu-id="517fd-112">Id</span></span> | <span data-ttu-id="517fd-113">(Obrigatório) O identificador do pacote a desinstalar.</span><span class="sxs-lookup"><span data-stu-id="517fd-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="517fd-114">-Id do comutador em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="517fd-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="517fd-115">Versão</span><span class="sxs-lookup"><span data-stu-id="517fd-115">Version</span></span> | <span data-ttu-id="517fd-116">A versão do pacote para desinstalar, padronizando para a versão atualmente instalada.</span><span class="sxs-lookup"><span data-stu-id="517fd-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="517fd-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="517fd-117">RemoveDependencies</span></span> | <span data-ttu-id="517fd-118">Desinstale o pacote e suas dependências não utilizadas.</span><span class="sxs-lookup"><span data-stu-id="517fd-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="517fd-119">Ou seja, se qualquer dependência tiver outro pacote que depende dele, ele será ignorado.</span><span class="sxs-lookup"><span data-stu-id="517fd-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="517fd-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="517fd-120">ProjectName</span></span> | <span data-ttu-id="517fd-121">O projeto do qual deseja desinstalar o pacote, padronizando para o projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="517fd-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="517fd-122">Force</span><span class="sxs-lookup"><span data-stu-id="517fd-122">Force</span></span> | <span data-ttu-id="517fd-123">Força um pacote a ser desinstalado, mesmo se outros pacotes dependem dele.</span><span class="sxs-lookup"><span data-stu-id="517fd-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="517fd-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="517fd-124">WhatIf</span></span> | <span data-ttu-id="517fd-125">Mostra o que aconteceria ao executar o comando sem realmente executar a desinstalação.</span><span class="sxs-lookup"><span data-stu-id="517fd-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="517fd-126">Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="517fd-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="517fd-127">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="517fd-127">Common Parameters</span></span>

<span data-ttu-id="517fd-128">`Uninstall-Package` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="517fd-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="517fd-129">Exemplos</span><span class="sxs-lookup"><span data-stu-id="517fd-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
