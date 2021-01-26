---
title: Referência do NuGet Uninstall-Package PowerShell
description: Referência para Uninstall-Package comando do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 961a9d68e5cba09030401fc871a93bf1145b23a3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777396"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="10ac8-103">Uninstall-Package (console do Gerenciador de pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="10ac8-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="10ac8-104">*Este tópico descreve o comando no [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows. Para o comando genérico Uninstall-Package do PowerShell, consulte a [referência do PackageManagement do PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="10ac8-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="10ac8-105">Remove um pacote de um projeto, removendo opcionalmente suas dependências.</span><span class="sxs-lookup"><span data-stu-id="10ac8-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="10ac8-106">Se outros pacotes dependem deste pacote, o comando irá falhar, a não ser que a opção –Force esteja especificada.</span><span class="sxs-lookup"><span data-stu-id="10ac8-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="10ac8-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="10ac8-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="10ac8-108">Se outros pacotes dependem deste pacote, o comando irá falhar, a não ser que a opção –Force esteja especificada.</span><span class="sxs-lookup"><span data-stu-id="10ac8-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="10ac8-109">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="10ac8-109">Parameters</span></span>

| <span data-ttu-id="10ac8-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="10ac8-110">Parameter</span></span> | <span data-ttu-id="10ac8-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="10ac8-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="10ac8-112">Id</span><span class="sxs-lookup"><span data-stu-id="10ac8-112">Id</span></span> | <span data-ttu-id="10ac8-113">Necessária O identificador do pacote a ser desinstalado.</span><span class="sxs-lookup"><span data-stu-id="10ac8-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="10ac8-114">A opção-ID em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="10ac8-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="10ac8-115">Versão</span><span class="sxs-lookup"><span data-stu-id="10ac8-115">Version</span></span> | <span data-ttu-id="10ac8-116">A versão do pacote a ser desinstalado, padronizando para a versão instalada no momento.</span><span class="sxs-lookup"><span data-stu-id="10ac8-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="10ac8-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="10ac8-117">RemoveDependencies</span></span> | <span data-ttu-id="10ac8-118">Desinstale o pacote e suas dependências não utilizadas.</span><span class="sxs-lookup"><span data-stu-id="10ac8-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="10ac8-119">Ou seja, se alguma dependência tiver outro pacote que dependa dele, ela será ignorada.</span><span class="sxs-lookup"><span data-stu-id="10ac8-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="10ac8-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="10ac8-120">ProjectName</span></span> | <span data-ttu-id="10ac8-121">O projeto do qual o pacote será desinstalado, padronizando para o projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="10ac8-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="10ac8-122">Force</span><span class="sxs-lookup"><span data-stu-id="10ac8-122">Force</span></span> | <span data-ttu-id="10ac8-123">Força a desinstalação de um pacote, mesmo que outros pacotes dependam dele.</span><span class="sxs-lookup"><span data-stu-id="10ac8-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="10ac8-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="10ac8-124">WhatIf</span></span> | <span data-ttu-id="10ac8-125">Mostra o que aconteceria ao executar o comando sem realmente executar a desinstalação.</span><span class="sxs-lookup"><span data-stu-id="10ac8-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="10ac8-126">Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="10ac8-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="10ac8-127">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="10ac8-127">Common Parameters</span></span>

<span data-ttu-id="10ac8-128">`Uninstall-Package` o oferece suporte aos seguintes [parâmetros comuns do PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="10ac8-128">`Uninstall-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="10ac8-129">Exemplos</span><span class="sxs-lookup"><span data-stu-id="10ac8-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```