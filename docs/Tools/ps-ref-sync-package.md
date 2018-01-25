---
title: "Referência do pacote do NuGet Sync PowerShell | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência de comando do PowerShell do pacote de sincronização no Console do Gerenciador de pacotes do NuGet no Visual Studio."
keywords: "Console do Gerenciador, comandos do Powershell do NuGet, referência do Powershell do NuGet, sincronização do pacote do pacote NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 02233cd0532fab2338e65e0d58b9afc3e2dab6af
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="1a74b-104">Pacote de sincronização (Console de Gerenciador de pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="1a74b-104">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="1a74b-105">*Versão 3.0 +; disponível apenas dentro de [NuGet Package Manager Console](Package-Manager-Console.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="1a74b-105">*Version 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="1a74b-106">Obtém a versão do pacote instalado a partir de especificado (ou padrão) do projeto e sincroniza a versão para o restante dos projetos na solução.</span><span class="sxs-lookup"><span data-stu-id="1a74b-106">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="1a74b-107">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="1a74b-107">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="1a74b-108">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="1a74b-108">Parameters</span></span>

| <span data-ttu-id="1a74b-109">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1a74b-109">Parameter</span></span> | <span data-ttu-id="1a74b-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a74b-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1a74b-111">Id</span><span class="sxs-lookup"><span data-stu-id="1a74b-111">Id</span></span> | <span data-ttu-id="1a74b-112">(Obrigatório) O identificador do pacote para sincronizar. -Id switch é opcional.</span><span class="sxs-lookup"><span data-stu-id="1a74b-112">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="1a74b-113">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="1a74b-113">IgnoreDependencies</span></span> | <span data-ttu-id="1a74b-114">Instale apenas esse pacote e não suas dependências.</span><span class="sxs-lookup"><span data-stu-id="1a74b-114">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="1a74b-115">ProjectName</span><span class="sxs-lookup"><span data-stu-id="1a74b-115">ProjectName</span></span> | <span data-ttu-id="1a74b-116">O projeto a ser sincronizados com o pacote, o padrão para o projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="1a74b-116">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="1a74b-117">Versão</span><span class="sxs-lookup"><span data-stu-id="1a74b-117">Version</span></span> | <span data-ttu-id="1a74b-118">A versão do pacote para sincronizar, padronizando para a versão atualmente instalada.</span><span class="sxs-lookup"><span data-stu-id="1a74b-118">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="1a74b-119">Origem</span><span class="sxs-lookup"><span data-stu-id="1a74b-119">Source</span></span> | <span data-ttu-id="1a74b-120">O caminho de URL ou pasta para a origem do pacote a ser pesquisado.</span><span class="sxs-lookup"><span data-stu-id="1a74b-120">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="1a74b-121">Caminhos de pasta local podem ser absoluto ou relativo para a pasta atual.</span><span class="sxs-lookup"><span data-stu-id="1a74b-121">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="1a74b-122">Se omitido, `Sync-Package` procura a origem de pacote selecionada atualmente.</span><span class="sxs-lookup"><span data-stu-id="1a74b-122">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="1a74b-123">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="1a74b-123">IncludePrerelease</span></span> | <span data-ttu-id="1a74b-124">Inclui pacotes pré-lançados a sincronização.</span><span class="sxs-lookup"><span data-stu-id="1a74b-124">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="1a74b-125">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="1a74b-125">FileConflictAction</span></span> | <span data-ttu-id="1a74b-126">A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes, referenciados pelo projeto.</span><span class="sxs-lookup"><span data-stu-id="1a74b-126">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="1a74b-127">Os valores possíveis são *substituir, ignorar, None, OverwriteAll*, e *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="1a74b-127">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="1a74b-128">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="1a74b-128">DependencyVersion</span></span> | <span data-ttu-id="1a74b-129">A versão dos pacotes de dependência a usar, que pode ser um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="1a74b-129">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="1a74b-130">*Menor* (padrão): a versão mais antiga</span><span class="sxs-lookup"><span data-stu-id="1a74b-130">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="1a74b-131">*HighestPatch*: a versão com o patch mais baixo principal, secundária menor, mais alto</span><span class="sxs-lookup"><span data-stu-id="1a74b-131">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="1a74b-132">*HighestMinor*: a versão com o menor principais, mais alto patch menor, mais alto</span><span class="sxs-lookup"><span data-stu-id="1a74b-132">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="1a74b-133">*Mais alto* (padrão para o pacote de atualização sem parâmetros): a versão mais recente</span><span class="sxs-lookup"><span data-stu-id="1a74b-133">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="1a74b-134">Você pode definir o valor padrão usando o [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) definindo no `Nuget.Config` arquivo.</span><span class="sxs-lookup"><span data-stu-id="1a74b-134">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="1a74b-135">WhatIf</span><span class="sxs-lookup"><span data-stu-id="1a74b-135">WhatIf</span></span> | <span data-ttu-id="1a74b-136">Mostra o que aconteceria quando a execução do comando sem realmente executar a sincronização.</span><span class="sxs-lookup"><span data-stu-id="1a74b-136">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="1a74b-137">Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="1a74b-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="1a74b-138">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="1a74b-138">Common Parameters</span></span>

<span data-ttu-id="1a74b-139">`Sync-Package`suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="1a74b-139">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="1a74b-140">Exemplos</span><span class="sxs-lookup"><span data-stu-id="1a74b-140">Examples</span></span>

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
