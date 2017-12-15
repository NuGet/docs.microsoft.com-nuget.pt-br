---
title: "Referência do pacote do NuGet Sync PowerShell | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 1b980b93-fa58-430c-b663-78ce069b1603
description: "Referência de comando do PowerShell do pacote de sincronização no Console do Gerenciador de pacotes do NuGet no Visual Studio."
keywords: "Console do Gerenciador, comandos do Powershell do NuGet, referência do Powershell do NuGet, sincronização do pacote do pacote NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4dc542714f14f0e6d3e827292f8fce06561fe270
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="98045-104">Pacote de sincronização (Console de Gerenciador de pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="98045-104">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="98045-105">*Versão 3.0 +; disponível apenas dentro de [NuGet Package Manager Console](Package-Manager-Console.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="98045-105">*Version 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="98045-106">Obtém a versão do pacote instalado a partir de especificado (ou padrão) do projeto e sincroniza a versão para o restante dos projetos na solução.</span><span class="sxs-lookup"><span data-stu-id="98045-106">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="98045-107">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="98045-107">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="98045-108">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="98045-108">Parameters</span></span>

| <span data-ttu-id="98045-109">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="98045-109">Parameter</span></span> | <span data-ttu-id="98045-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="98045-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="98045-111">Id</span><span class="sxs-lookup"><span data-stu-id="98045-111">Id</span></span> | <span data-ttu-id="98045-112">(Obrigatório) O identificador do pacote para sincronizar. -Id switch é opcional.</span><span class="sxs-lookup"><span data-stu-id="98045-112">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="98045-113">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="98045-113">IgnoreDependencies</span></span> | <span data-ttu-id="98045-114">Instale apenas esse pacote e não suas dependências.</span><span class="sxs-lookup"><span data-stu-id="98045-114">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="98045-115">ProjectName</span><span class="sxs-lookup"><span data-stu-id="98045-115">ProjectName</span></span> | <span data-ttu-id="98045-116">O projeto a ser sincronizados com o pacote, o padrão para o projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="98045-116">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="98045-117">Versão</span><span class="sxs-lookup"><span data-stu-id="98045-117">Version</span></span> | <span data-ttu-id="98045-118">A versão do pacote para sincronizar, padronizando para a versão atualmente instalada.</span><span class="sxs-lookup"><span data-stu-id="98045-118">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="98045-119">Origem</span><span class="sxs-lookup"><span data-stu-id="98045-119">Source</span></span> | <span data-ttu-id="98045-120">O caminho de URL ou pasta para a origem do pacote a ser pesquisado.</span><span class="sxs-lookup"><span data-stu-id="98045-120">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="98045-121">Caminhos de pasta local podem ser absoluto ou relativo para a pasta atual.</span><span class="sxs-lookup"><span data-stu-id="98045-121">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="98045-122">Se omitido, `Sync-Package` procura a origem de pacote selecionada atualmente.</span><span class="sxs-lookup"><span data-stu-id="98045-122">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="98045-123">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="98045-123">IncludePrerelease</span></span> | <span data-ttu-id="98045-124">Inclui pacotes pré-lançados a sincronização.</span><span class="sxs-lookup"><span data-stu-id="98045-124">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="98045-125">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="98045-125">FileConflictAction</span></span> | <span data-ttu-id="98045-126">A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes, referenciados pelo projeto.</span><span class="sxs-lookup"><span data-stu-id="98045-126">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="98045-127">Os valores possíveis são *substituir, ignorar, None, OverwriteAll*, e *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="98045-127">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="98045-128">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="98045-128">DependencyVersion</span></span> | <span data-ttu-id="98045-129">A versão dos pacotes de dependência a usar, que pode ser um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="98045-129">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="98045-130">*Menor* (padrão): a versão mais antiga</span><span class="sxs-lookup"><span data-stu-id="98045-130">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="98045-131">*HighestPatch*: a versão com o patch mais baixo principal, secundária menor, mais alto</span><span class="sxs-lookup"><span data-stu-id="98045-131">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="98045-132">*HighestMinor*: a versão com o menor principais, mais alto patch menor, mais alto</span><span class="sxs-lookup"><span data-stu-id="98045-132">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="98045-133">*Mais alto* (padrão para o pacote de atualização sem parâmetros): a versão mais recente</span><span class="sxs-lookup"><span data-stu-id="98045-133">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="98045-134">Você pode definir o valor padrão usando o [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) definindo no `Nuget.Config` arquivo.</span><span class="sxs-lookup"><span data-stu-id="98045-134">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="98045-135">WhatIf</span><span class="sxs-lookup"><span data-stu-id="98045-135">WhatIf</span></span> | <span data-ttu-id="98045-136">Mostra o que aconteceria quando a execução do comando sem realmente executar a sincronização.</span><span class="sxs-lookup"><span data-stu-id="98045-136">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="98045-137">Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="98045-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="98045-138">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="98045-138">Common Parameters</span></span>

<span data-ttu-id="98045-139">`Sync-Package`suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="98045-139">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="98045-140">Exemplos</span><span class="sxs-lookup"><span data-stu-id="98045-140">Examples</span></span>

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
