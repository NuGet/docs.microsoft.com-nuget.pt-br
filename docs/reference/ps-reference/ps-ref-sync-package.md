---
title: Sincronização do NuGet – referência do PowerShell do pacote
description: Referência para o comando sync-Package do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a48a09a27b6db9b774e59b9a10652067179e2c27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327303"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="e2eab-103">Sync-Package (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="e2eab-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e2eab-104">*Versão 3.0 +; disponível somente dentro do [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="e2eab-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e2eab-105">Obtém a versão do pacote instalado do projeto especificado (ou padrão) e sincroniza a versão para o restante dos projetos na solução.</span><span class="sxs-lookup"><span data-stu-id="e2eab-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="e2eab-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="e2eab-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="e2eab-107">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="e2eab-107">Parameters</span></span>

| <span data-ttu-id="e2eab-108">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e2eab-108">Parameter</span></span> | <span data-ttu-id="e2eab-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="e2eab-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e2eab-110">Id</span><span class="sxs-lookup"><span data-stu-id="e2eab-110">Id</span></span> | <span data-ttu-id="e2eab-111">Necessária O identificador do pacote a ser sincronizado. A opção-ID em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="e2eab-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="e2eab-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="e2eab-112">IgnoreDependencies</span></span> | <span data-ttu-id="e2eab-113">Instale somente este pacote e não suas dependências.</span><span class="sxs-lookup"><span data-stu-id="e2eab-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="e2eab-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="e2eab-114">ProjectName</span></span> | <span data-ttu-id="e2eab-115">O projeto do qual sincronizar o pacote, padronizando para o projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="e2eab-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="e2eab-116">Versão</span><span class="sxs-lookup"><span data-stu-id="e2eab-116">Version</span></span> | <span data-ttu-id="e2eab-117">A versão do pacote a ser sincronizado, padronizando para a versão instalada no momento.</span><span class="sxs-lookup"><span data-stu-id="e2eab-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="e2eab-118">Origem</span><span class="sxs-lookup"><span data-stu-id="e2eab-118">Source</span></span> | <span data-ttu-id="e2eab-119">O caminho da URL ou da pasta para a origem do pacote a ser pesquisado.</span><span class="sxs-lookup"><span data-stu-id="e2eab-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="e2eab-120">Os caminhos de pasta local podem ser absolutos ou relativos à pasta atual.</span><span class="sxs-lookup"><span data-stu-id="e2eab-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="e2eab-121">Se omitido `Sync-Package` , pesquisa a origem do pacote selecionada no momento.</span><span class="sxs-lookup"><span data-stu-id="e2eab-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="e2eab-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="e2eab-122">IncludePrerelease</span></span> | <span data-ttu-id="e2eab-123">Inclui pacotes de pré-lançamento na sincronização.</span><span class="sxs-lookup"><span data-stu-id="e2eab-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="e2eab-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="e2eab-124">FileConflictAction</span></span> | <span data-ttu-id="e2eab-125">A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes referenciados pelo projeto.</span><span class="sxs-lookup"><span data-stu-id="e2eab-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="e2eab-126">Os valores possíveis são *overwrite, ignore, None, OverwriteAll*e *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="e2eab-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="e2eab-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="e2eab-127">DependencyVersion</span></span> | <span data-ttu-id="e2eab-128">A versão dos pacotes de dependência a serem usados, que pode ser uma das seguintes:</span><span class="sxs-lookup"><span data-stu-id="e2eab-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="e2eab-129">*Mais baixo* (padrão): a versão mais baixa</span><span class="sxs-lookup"><span data-stu-id="e2eab-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="e2eab-130">*HighestPatch*: a versão com o menor principal, menor o mais baixo, patch mais alto</span><span class="sxs-lookup"><span data-stu-id="e2eab-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="e2eab-131">*HighestMinor*: a versão com o menor principal, o mais baixo, o patch mais alto</span><span class="sxs-lookup"><span data-stu-id="e2eab-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="e2eab-132">*Mais alto* (padrão para update-package sem parâmetros): a versão mais recente</span><span class="sxs-lookup"><span data-stu-id="e2eab-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="e2eab-133">Você pode definir o valor padrão usando a [`dependencyVersion`](../nuget-config-file.md#config-section) configuração `Nuget.Config` no arquivo.</span><span class="sxs-lookup"><span data-stu-id="e2eab-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="e2eab-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="e2eab-134">WhatIf</span></span> | <span data-ttu-id="e2eab-135">Mostra o que aconteceria ao executar o comando sem realmente executar a sincronização.</span><span class="sxs-lookup"><span data-stu-id="e2eab-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="e2eab-136">Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="e2eab-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e2eab-137">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="e2eab-137">Common Parameters</span></span>

<span data-ttu-id="e2eab-138">`Sync-Package`o oferece suporte aos seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e2eab-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e2eab-139">Exemplos</span><span class="sxs-lookup"><span data-stu-id="e2eab-139">Examples</span></span>

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
