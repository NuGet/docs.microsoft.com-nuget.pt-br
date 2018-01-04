---
title: "Referência de PowerShell do NuGet Uninstall-Package | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: f4f5dc79-8e8e-4012-8986-873a5d9283d9
description: "Referência de comando do PowerShell do pacote de desinstalação no Console do Gerenciador de pacotes do NuGet no Visual Studio."
keywords: "Console do Gerenciador, comandos do Powershell do NuGet, referência do Powershell do NuGet, pacote de desinstalação do pacote NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 679e89e9cfb16dbe484f133b0b6431313b9d87ac
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="1f4cd-104">Uninstall-Package (Console de Gerenciador de pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="1f4cd-104">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="1f4cd-105">*Este tópico descreve o comando dentro de [NuGet Package Manager Console](Package-Manager-Console.md) no Visual Studio no Windows. Para o comando genérico do pacote de desinstalação do PowerShell, consulte o [referência do PowerShell PackageManagement](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="1f4cd-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="1f4cd-106">Remove um pacote de um projeto, opcionalmente, a remoção de suas dependências.</span><span class="sxs-lookup"><span data-stu-id="1f4cd-106">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="1f4cd-107">Se outros pacotes dependerem deste pacote, o comando falhará, a menos que – Force opção é especificada.</span><span class="sxs-lookup"><span data-stu-id="1f4cd-107">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="1f4cd-108">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="1f4cd-108">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="1f4cd-109">Se outros pacotes dependerem deste pacote, o comando falhará, a menos que – Force opção é especificada.</span><span class="sxs-lookup"><span data-stu-id="1f4cd-109">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="1f4cd-110">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="1f4cd-110">Parameters</span></span>

| <span data-ttu-id="1f4cd-111">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1f4cd-111">Parameter</span></span> | <span data-ttu-id="1f4cd-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="1f4cd-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1f4cd-113">Id</span><span class="sxs-lookup"><span data-stu-id="1f4cd-113">Id</span></span> | <span data-ttu-id="1f4cd-114">(Obrigatório) O identificador do pacote a ser desinstalado.</span><span class="sxs-lookup"><span data-stu-id="1f4cd-114">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="1f4cd-115">-Id switch é opcional.</span><span class="sxs-lookup"><span data-stu-id="1f4cd-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="1f4cd-116">Versão</span><span class="sxs-lookup"><span data-stu-id="1f4cd-116">Version</span></span> | <span data-ttu-id="1f4cd-117">A versão do pacote para desinstalar, padronizando para a versão atualmente instalada.</span><span class="sxs-lookup"><span data-stu-id="1f4cd-117">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="1f4cd-118">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="1f4cd-118">RemoveDependencies</span></span> | <span data-ttu-id="1f4cd-119">Desinstale o pacote e suas dependências não usadas.</span><span class="sxs-lookup"><span data-stu-id="1f4cd-119">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="1f4cd-120">Ou seja, se qualquer dependência tiver outro pacote que depende dele, ele é ignorado.</span><span class="sxs-lookup"><span data-stu-id="1f4cd-120">That is, if any dependency has another package that depends on it, it is skipped.</span></span> |
| <span data-ttu-id="1f4cd-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="1f4cd-121">ProjectName</span></span> | <span data-ttu-id="1f4cd-122">O projeto do qual deseja desinstalar o pacote, o padrão para o projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="1f4cd-122">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="1f4cd-123">Force</span><span class="sxs-lookup"><span data-stu-id="1f4cd-123">Force</span></span> | <span data-ttu-id="1f4cd-124">Força um pacote a ser desinstalado, mesmo se outros pacotes dependem dele.</span><span class="sxs-lookup"><span data-stu-id="1f4cd-124">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="1f4cd-125">WhatIf</span><span class="sxs-lookup"><span data-stu-id="1f4cd-125">WhatIf</span></span> | <span data-ttu-id="1f4cd-126">Mostra o que aconteceria quando a execução do comando sem realmente executar a desinstalação.</span><span class="sxs-lookup"><span data-stu-id="1f4cd-126">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="1f4cd-127">Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="1f4cd-127">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="1f4cd-128">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="1f4cd-128">Common Parameters</span></span>

<span data-ttu-id="1f4cd-129">`Uninstall-Package`suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="1f4cd-129">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="1f4cd-130">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1f4cd-130">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```