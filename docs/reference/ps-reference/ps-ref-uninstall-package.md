---
title: Desinstalação do NuGet-referência do PowerShell do pacote
description: Referência para o comando Uninstall-Package do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5c963588d28cab42e5fb6a43b31a17e26e49d0d2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327273"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="13c2e-103">Uninstall-Package (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="13c2e-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="13c2e-104">*Este tópico descreve o comando no [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows. Para o comando genérico do PowerShell Uninstall-Package, consulte a [referência do PackageManagement do PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="13c2e-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="13c2e-105">Remove um pacote de um projeto, removendo opcionalmente suas dependências.</span><span class="sxs-lookup"><span data-stu-id="13c2e-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="13c2e-106">Se outros pacotes dependerem desse pacote, o comando falhará, a menos que a opção – Force seja especificada.</span><span class="sxs-lookup"><span data-stu-id="13c2e-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="13c2e-107">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="13c2e-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="13c2e-108">Se outros pacotes dependerem desse pacote, o comando falhará, a menos que a opção – Force seja especificada.</span><span class="sxs-lookup"><span data-stu-id="13c2e-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="13c2e-109">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="13c2e-109">Parameters</span></span>

| <span data-ttu-id="13c2e-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="13c2e-110">Parameter</span></span> | <span data-ttu-id="13c2e-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="13c2e-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="13c2e-112">Id</span><span class="sxs-lookup"><span data-stu-id="13c2e-112">Id</span></span> | <span data-ttu-id="13c2e-113">Necessária O identificador do pacote a ser desinstalado.</span><span class="sxs-lookup"><span data-stu-id="13c2e-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="13c2e-114">A opção-ID em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="13c2e-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="13c2e-115">Versão</span><span class="sxs-lookup"><span data-stu-id="13c2e-115">Version</span></span> | <span data-ttu-id="13c2e-116">A versão do pacote a ser desinstalado, padronizando para a versão instalada no momento.</span><span class="sxs-lookup"><span data-stu-id="13c2e-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="13c2e-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="13c2e-117">RemoveDependencies</span></span> | <span data-ttu-id="13c2e-118">Desinstale o pacote e suas dependências não utilizadas.</span><span class="sxs-lookup"><span data-stu-id="13c2e-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="13c2e-119">Ou seja, se alguma dependência tiver outro pacote que dependa dele, ela será ignorada.</span><span class="sxs-lookup"><span data-stu-id="13c2e-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="13c2e-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="13c2e-120">ProjectName</span></span> | <span data-ttu-id="13c2e-121">O projeto do qual o pacote será desinstalado, padronizando para o projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="13c2e-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="13c2e-122">Aplicação</span><span class="sxs-lookup"><span data-stu-id="13c2e-122">Force</span></span> | <span data-ttu-id="13c2e-123">Força a desinstalação de um pacote, mesmo que outros pacotes dependam dele.</span><span class="sxs-lookup"><span data-stu-id="13c2e-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="13c2e-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="13c2e-124">WhatIf</span></span> | <span data-ttu-id="13c2e-125">Mostra o que aconteceria ao executar o comando sem realmente executar a desinstalação.</span><span class="sxs-lookup"><span data-stu-id="13c2e-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="13c2e-126">Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="13c2e-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="13c2e-127">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="13c2e-127">Common Parameters</span></span>

<span data-ttu-id="13c2e-128">`Uninstall-Package`o oferece suporte aos seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="13c2e-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="13c2e-129">Exemplos</span><span class="sxs-lookup"><span data-stu-id="13c2e-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
