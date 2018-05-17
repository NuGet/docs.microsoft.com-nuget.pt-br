---
title: Referência do PowerShell de pacote do NuGet sincronização
description: Referência de comando do PowerShell do pacote de sincronização no Console do Gerenciador de pacotes do NuGet no Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 424c4fbe3ff4b61c665bf7353976d4fb09268185
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="e2d55-103">Sync-Package (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e2d55-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e2d55-104">*Versão 3.0 +; disponível apenas dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="e2d55-104">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e2d55-105">Obtém a versão do pacote instalado a partir de especificado (ou padrão) do projeto e sincroniza a versão para o restante dos projetos na solução.</span><span class="sxs-lookup"><span data-stu-id="e2d55-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="e2d55-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="e2d55-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="e2d55-107">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="e2d55-107">Parameters</span></span>

| <span data-ttu-id="e2d55-108">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e2d55-108">Parameter</span></span> | <span data-ttu-id="e2d55-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="e2d55-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e2d55-110">Id</span><span class="sxs-lookup"><span data-stu-id="e2d55-110">Id</span></span> | <span data-ttu-id="e2d55-111">(Obrigatório) O identificador do pacote para sincronizar. -Id switch é opcional.</span><span class="sxs-lookup"><span data-stu-id="e2d55-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="e2d55-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="e2d55-112">IgnoreDependencies</span></span> | <span data-ttu-id="e2d55-113">Instale apenas esse pacote e não suas dependências.</span><span class="sxs-lookup"><span data-stu-id="e2d55-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="e2d55-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="e2d55-114">ProjectName</span></span> | <span data-ttu-id="e2d55-115">O projeto a ser sincronizados com o pacote, o padrão para o projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="e2d55-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="e2d55-116">Versão</span><span class="sxs-lookup"><span data-stu-id="e2d55-116">Version</span></span> | <span data-ttu-id="e2d55-117">A versão do pacote para sincronizar, padronizando para a versão atualmente instalada.</span><span class="sxs-lookup"><span data-stu-id="e2d55-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="e2d55-118">Origem</span><span class="sxs-lookup"><span data-stu-id="e2d55-118">Source</span></span> | <span data-ttu-id="e2d55-119">O caminho de URL ou pasta para a origem do pacote a ser pesquisado.</span><span class="sxs-lookup"><span data-stu-id="e2d55-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="e2d55-120">Caminhos de pasta local podem ser absoluto ou relativo para a pasta atual.</span><span class="sxs-lookup"><span data-stu-id="e2d55-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="e2d55-121">Se omitido, `Sync-Package` procura a origem de pacote selecionada atualmente.</span><span class="sxs-lookup"><span data-stu-id="e2d55-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="e2d55-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="e2d55-122">IncludePrerelease</span></span> | <span data-ttu-id="e2d55-123">Inclui pacotes pré-lançados a sincronização.</span><span class="sxs-lookup"><span data-stu-id="e2d55-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="e2d55-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="e2d55-124">FileConflictAction</span></span> | <span data-ttu-id="e2d55-125">A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes, referenciados pelo projeto.</span><span class="sxs-lookup"><span data-stu-id="e2d55-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="e2d55-126">Os valores possíveis são *substituir, ignorar, None, OverwriteAll*, e *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="e2d55-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="e2d55-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="e2d55-127">DependencyVersion</span></span> | <span data-ttu-id="e2d55-128">A versão dos pacotes de dependência a usar, que pode ser um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="e2d55-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="e2d55-129">*Menor* (padrão): a versão mais antiga</span><span class="sxs-lookup"><span data-stu-id="e2d55-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="e2d55-130">*HighestPatch*: a versão com o patch mais baixo principal, secundária menor, mais alto</span><span class="sxs-lookup"><span data-stu-id="e2d55-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="e2d55-131">*HighestMinor*: a versão com o menor principais, mais alto patch menor, mais alto</span><span class="sxs-lookup"><span data-stu-id="e2d55-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="e2d55-132">*Mais alto* (padrão para o pacote de atualização sem parâmetros): a versão mais recente</span><span class="sxs-lookup"><span data-stu-id="e2d55-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="e2d55-133">Você pode definir o valor padrão usando o [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) definindo no `Nuget.Config` arquivo.</span><span class="sxs-lookup"><span data-stu-id="e2d55-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="e2d55-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="e2d55-134">WhatIf</span></span> | <span data-ttu-id="e2d55-135">Mostra o que aconteceria quando a execução do comando sem realmente executar a sincronização.</span><span class="sxs-lookup"><span data-stu-id="e2d55-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="e2d55-136">Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="e2d55-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e2d55-137">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="e2d55-137">Common Parameters</span></span>

<span data-ttu-id="e2d55-138">`Sync-Package` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e2d55-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e2d55-139">Exemplos</span><span class="sxs-lookup"><span data-stu-id="e2d55-139">Examples</span></span>

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
