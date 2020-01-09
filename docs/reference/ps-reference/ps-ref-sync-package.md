---
title: Sincronização do NuGet – referência do PowerShell do pacote
description: Referência para o comando sync-Package do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 12a3d5f32056539a75da9e17b15d67e72a8a42c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384897"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="e9d8d-103">Sync-Package (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e9d8d-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e9d8d-104">*Versão 3.0 +; disponível somente dentro do [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="e9d8d-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e9d8d-105">Obtém a versão do pacote instalado do projeto especificado (ou padrão) e sincroniza a versão para o restante dos projetos na solução.</span><span class="sxs-lookup"><span data-stu-id="e9d8d-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="e9d8d-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="e9d8d-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="e9d8d-107">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="e9d8d-107">Parameters</span></span>

| <span data-ttu-id="e9d8d-108">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9d8d-108">Parameter</span></span> | <span data-ttu-id="e9d8d-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="e9d8d-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e9d8d-110">Id</span><span class="sxs-lookup"><span data-stu-id="e9d8d-110">Id</span></span> | <span data-ttu-id="e9d8d-111">Necessária O identificador do pacote a ser sincronizado. A opção-ID em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="e9d8d-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="e9d8d-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="e9d8d-112">IgnoreDependencies</span></span> | <span data-ttu-id="e9d8d-113">Instale somente este pacote e não suas dependências.</span><span class="sxs-lookup"><span data-stu-id="e9d8d-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="e9d8d-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="e9d8d-114">ProjectName</span></span> | <span data-ttu-id="e9d8d-115">O projeto do qual sincronizar o pacote, padronizando para o projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="e9d8d-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="e9d8d-116">Versão do</span><span class="sxs-lookup"><span data-stu-id="e9d8d-116">Version</span></span> | <span data-ttu-id="e9d8d-117">A versão do pacote a ser sincronizado, padronizando para a versão instalada no momento.</span><span class="sxs-lookup"><span data-stu-id="e9d8d-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="e9d8d-118">Source</span><span class="sxs-lookup"><span data-stu-id="e9d8d-118">Source</span></span> | <span data-ttu-id="e9d8d-119">O caminho da URL ou da pasta para a origem do pacote a ser pesquisado.</span><span class="sxs-lookup"><span data-stu-id="e9d8d-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="e9d8d-120">Os caminhos de pasta local podem ser absolutos ou relativos à pasta atual.</span><span class="sxs-lookup"><span data-stu-id="e9d8d-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="e9d8d-121">Se for omitido, `Sync-Package` pesquisará a origem do pacote selecionada no momento.</span><span class="sxs-lookup"><span data-stu-id="e9d8d-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="e9d8d-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="e9d8d-122">IncludePrerelease</span></span> | <span data-ttu-id="e9d8d-123">Inclui pacotes de pré-lançamento na sincronização.</span><span class="sxs-lookup"><span data-stu-id="e9d8d-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="e9d8d-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="e9d8d-124">FileConflictAction</span></span> | <span data-ttu-id="e9d8d-125">A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes referenciados pelo projeto.</span><span class="sxs-lookup"><span data-stu-id="e9d8d-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="e9d8d-126">Os valores possíveis são *overwrite, ignore, None, OverwriteAll*e *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="e9d8d-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="e9d8d-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="e9d8d-127">DependencyVersion</span></span> | <span data-ttu-id="e9d8d-128">A versão dos pacotes de dependência a serem usados, que pode ser uma das seguintes:</span><span class="sxs-lookup"><span data-stu-id="e9d8d-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="e9d8d-129">*Mais baixo* (padrão): a versão mais baixa</span><span class="sxs-lookup"><span data-stu-id="e9d8d-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="e9d8d-130">*HighestPatch*: a versão com o menor principal, menor o mais baixo, patch mais alto</span><span class="sxs-lookup"><span data-stu-id="e9d8d-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="e9d8d-131">*HighestMinor*: a versão com o menor principal, o mais baixo, o patch mais alto</span><span class="sxs-lookup"><span data-stu-id="e9d8d-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="e9d8d-132">*Mais alto* (padrão para update-package sem parâmetros): a versão mais recente</span><span class="sxs-lookup"><span data-stu-id="e9d8d-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="e9d8d-133">Você pode definir o valor padrão usando a configuração de [`dependencyVersion`](../nuget-config-file.md#config-section) no arquivo de `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="e9d8d-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="e9d8d-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="e9d8d-134">WhatIf</span></span> | <span data-ttu-id="e9d8d-135">Mostra o que aconteceria ao executar o comando sem realmente executar a sincronização.</span><span class="sxs-lookup"><span data-stu-id="e9d8d-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="e9d8d-136">Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="e9d8d-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e9d8d-137">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="e9d8d-137">Common Parameters</span></span>

<span data-ttu-id="e9d8d-138">o `Sync-Package` dá suporte aos seguintes [parâmetros comuns do PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e9d8d-138">`Sync-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e9d8d-139">Exemplos</span><span class="sxs-lookup"><span data-stu-id="e9d8d-139">Examples</span></span>

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
