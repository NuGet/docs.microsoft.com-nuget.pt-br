---
title: Referência do PowerShell de sincronização-pacote do NuGet
description: Referência de comando do PowerShell de sincronização de pacote no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: de0b612e1335cafdcd6a0b802d54f2182d27ad22
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842258"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="daf10-103">Sync-Package (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="daf10-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="daf10-104">*Versão 3.0 ou superior; disponível somente dentro de [Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="daf10-104">*Version 3.0+; available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="daf10-105">Obtém a versão do pacote instalado do especificado (ou padrão) do projeto e sincroniza a versão para o restante dos projetos na solução.</span><span class="sxs-lookup"><span data-stu-id="daf10-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="daf10-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="daf10-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="daf10-107">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="daf10-107">Parameters</span></span>

| <span data-ttu-id="daf10-108">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="daf10-108">Parameter</span></span> | <span data-ttu-id="daf10-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="daf10-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="daf10-110">Id</span><span class="sxs-lookup"><span data-stu-id="daf10-110">Id</span></span> | <span data-ttu-id="daf10-111">(Obrigatório) O identificador do pacote para sincronizar. -Id do comutador em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="daf10-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="daf10-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="daf10-112">IgnoreDependencies</span></span> | <span data-ttu-id="daf10-113">Instale apenas esse pacote e não as suas dependências.</span><span class="sxs-lookup"><span data-stu-id="daf10-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="daf10-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="daf10-114">ProjectName</span></span> | <span data-ttu-id="daf10-115">O projeto para sincronizar o pacote, padronizando para o projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="daf10-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="daf10-116">Versão</span><span class="sxs-lookup"><span data-stu-id="daf10-116">Version</span></span> | <span data-ttu-id="daf10-117">A versão do pacote para sincronizar, padronizando para a versão atualmente instalada.</span><span class="sxs-lookup"><span data-stu-id="daf10-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="daf10-118">Origem</span><span class="sxs-lookup"><span data-stu-id="daf10-118">Source</span></span> | <span data-ttu-id="daf10-119">O caminho de URL ou pasta para a origem do pacote a pesquisar.</span><span class="sxs-lookup"><span data-stu-id="daf10-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="daf10-120">Caminhos de pasta local podem ser absoluto ou relativo à pasta atual.</span><span class="sxs-lookup"><span data-stu-id="daf10-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="daf10-121">Se omitido, `Sync-Package` procura a origem do pacote selecionado no momento.</span><span class="sxs-lookup"><span data-stu-id="daf10-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="daf10-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="daf10-122">IncludePrerelease</span></span> | <span data-ttu-id="daf10-123">Inclui pacotes de pré-lançamento na sincronização.</span><span class="sxs-lookup"><span data-stu-id="daf10-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="daf10-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="daf10-124">FileConflictAction</span></span> | <span data-ttu-id="daf10-125">A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes, referenciados pelo projeto.</span><span class="sxs-lookup"><span data-stu-id="daf10-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="daf10-126">Os valores possíveis são *substituir, ignorar, None, OverwriteAll*, e *(3.0 ou superior)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="daf10-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="daf10-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="daf10-127">DependencyVersion</span></span> | <span data-ttu-id="daf10-128">A versão dos pacotes de dependência a ser usado, que pode ser um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="daf10-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="daf10-129">*Mais baixo* (padrão): a versão mais antiga</span><span class="sxs-lookup"><span data-stu-id="daf10-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="daf10-130">*HighestPatch*: a versão com o patch mais baixa principal, secundária menor, mais alto</span><span class="sxs-lookup"><span data-stu-id="daf10-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="daf10-131">*HighestMinor*: a versão com menor principais, o patch mais alto de pequena, mais alto</span><span class="sxs-lookup"><span data-stu-id="daf10-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="daf10-132">*Mais alto* (padrão para o pacote de atualização sem parâmetros): a versão mais recente</span><span class="sxs-lookup"><span data-stu-id="daf10-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="daf10-133">Você pode definir o valor padrão usando o [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) definindo no `Nuget.Config` arquivo.</span><span class="sxs-lookup"><span data-stu-id="daf10-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="daf10-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="daf10-134">WhatIf</span></span> | <span data-ttu-id="daf10-135">Mostra o que aconteceria ao executar o comando sem realmente executar a sincronização.</span><span class="sxs-lookup"><span data-stu-id="daf10-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="daf10-136">Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="daf10-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="daf10-137">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="daf10-137">Common Parameters</span></span>

<span data-ttu-id="daf10-138">`Sync-Package` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="daf10-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="daf10-139">Exemplos</span><span class="sxs-lookup"><span data-stu-id="daf10-139">Examples</span></span>

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
