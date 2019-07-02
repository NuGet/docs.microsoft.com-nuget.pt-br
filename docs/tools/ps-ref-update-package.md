---
title: Referência de pacote de atualização do NuGet do PowerShell
description: Referência de comando do PowerShell do pacote de atualização no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5b5a11ee11d9e2cf6a90d56ac63b1f7bad750ea
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496485"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="24b34-103">Update-Package (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="24b34-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="24b34-104">*Disponível somente dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="24b34-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="24b34-105">Atualiza um pacote e suas dependências ou todos os pacotes em um projeto, para uma versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="24b34-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="24b34-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="24b34-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="24b34-107">No NuGet 2.8 ou superior, `Update-Package` pode ser usado para fazer o downgrade de um pacote existente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="24b34-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="24b34-108">Por exemplo, se você tiver 5.1.0-rc1 ASPNET instalado, o comando a seguir seria fazer o downgrade para 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="24b34-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="24b34-109">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="24b34-109">Parameters</span></span>

|  <span data-ttu-id="24b34-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="24b34-110">Parameter</span></span> | <span data-ttu-id="24b34-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="24b34-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="24b34-112">Id</span><span class="sxs-lookup"><span data-stu-id="24b34-112">Id</span></span> | <span data-ttu-id="24b34-113">O identificador do pacote a atualizar.</span><span class="sxs-lookup"><span data-stu-id="24b34-113">The identifier of the package to update.</span></span> <span data-ttu-id="24b34-114">Se omitido, todos os pacotes de atualizações.</span><span class="sxs-lookup"><span data-stu-id="24b34-114">If omitted, updates all packages.</span></span> <span data-ttu-id="24b34-115">-Id do comutador em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="24b34-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="24b34-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="24b34-116">IgnoreDependencies</span></span> | <span data-ttu-id="24b34-117">Ignora atualizando dependências do pacote.</span><span class="sxs-lookup"><span data-stu-id="24b34-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="24b34-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="24b34-118">ProjectName</span></span> | <span data-ttu-id="24b34-119">O nome do projeto que contém os pacotes para atualizar, padronizando para todos os projetos.</span><span class="sxs-lookup"><span data-stu-id="24b34-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="24b34-120">Versão</span><span class="sxs-lookup"><span data-stu-id="24b34-120">Version</span></span> | <span data-ttu-id="24b34-121">A versão a ser usado para a atualização, padronizando para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="24b34-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="24b34-122">No NuGet 3.0 ou superior, o valor de versão deve ser um dos *menor, mais alto, HighestMinor*, ou *HighestPatch* (equivalente ao - Safe).</span><span class="sxs-lookup"><span data-stu-id="24b34-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="24b34-123">Safe</span><span class="sxs-lookup"><span data-stu-id="24b34-123">Safe</span></span> | <span data-ttu-id="24b34-124">Restringe atualizações para versões somente com a mesma versão principal e secundária do pacote atualmente instalado.</span><span class="sxs-lookup"><span data-stu-id="24b34-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="24b34-125">Origem</span><span class="sxs-lookup"><span data-stu-id="24b34-125">Source</span></span> | <span data-ttu-id="24b34-126">O caminho de URL ou pasta para a origem do pacote a pesquisar.</span><span class="sxs-lookup"><span data-stu-id="24b34-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="24b34-127">Caminhos de pasta local podem ser absoluto ou relativo à pasta atual.</span><span class="sxs-lookup"><span data-stu-id="24b34-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="24b34-128">Se omitido, `Update-Package` procura a origem do pacote selecionado no momento.</span><span class="sxs-lookup"><span data-stu-id="24b34-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="24b34-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="24b34-129">IncludePrerelease</span></span> | <span data-ttu-id="24b34-130">Inclui pacotes de pré-lançamento de atualizações.</span><span class="sxs-lookup"><span data-stu-id="24b34-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="24b34-131">Reinstalar</span><span class="sxs-lookup"><span data-stu-id="24b34-131">Reinstall</span></span> | <span data-ttu-id="24b34-132">Pacotes de Resintalls usando suas versões atualmente instaladas.</span><span class="sxs-lookup"><span data-stu-id="24b34-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="24b34-133">Confira [Reinstalando e atualizando pacotes](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="24b34-133">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="24b34-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="24b34-134">FileConflictAction</span></span> | <span data-ttu-id="24b34-135">A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes, referenciados pelo projeto.</span><span class="sxs-lookup"><span data-stu-id="24b34-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="24b34-136">Os valores possíveis são *substituir, ignorar, None, OverwriteAll*, e *IgnoreAll* (3.0 ou superior).</span><span class="sxs-lookup"><span data-stu-id="24b34-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="24b34-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="24b34-137">DependencyVersion</span></span> | <span data-ttu-id="24b34-138">A versão dos pacotes de dependência a ser usado, que pode ser um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="24b34-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="24b34-139">*Mais baixo* (padrão): a versão mais antiga</span><span class="sxs-lookup"><span data-stu-id="24b34-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="24b34-140">*HighestPatch*: a versão com o patch mais baixa principal, secundária menor, mais alto</span><span class="sxs-lookup"><span data-stu-id="24b34-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="24b34-141">*HighestMinor*: a versão com menor principais, o patch mais alto de pequena, mais alto</span><span class="sxs-lookup"><span data-stu-id="24b34-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="24b34-142">*Mais alto* (padrão para o pacote de atualização sem parâmetros): a versão mais recente</span><span class="sxs-lookup"><span data-stu-id="24b34-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="24b34-143">Você pode definir o valor padrão usando o [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) definindo no `Nuget.Config` arquivo.</span><span class="sxs-lookup"><span data-stu-id="24b34-143">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="24b34-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="24b34-144">ToHighestPatch</span></span> | <span data-ttu-id="24b34-145">equivalente ao - Safe.</span><span class="sxs-lookup"><span data-stu-id="24b34-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="24b34-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="24b34-146">ToHighestMinor</span></span> | <span data-ttu-id="24b34-147">Restringe atualizações para apenas as versões com a mesma versão principal que o pacote atualmente instalado.</span><span class="sxs-lookup"><span data-stu-id="24b34-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="24b34-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="24b34-148">WhatIf</span></span> | <span data-ttu-id="24b34-149">Mostra o que aconteceria ao executar o comando sem realmente executar a atualização.</span><span class="sxs-lookup"><span data-stu-id="24b34-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="24b34-150">Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="24b34-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="24b34-151">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="24b34-151">Common Parameters</span></span>

<span data-ttu-id="24b34-152">`Update-Package` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="24b34-152">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="24b34-153">Exemplos</span><span class="sxs-lookup"><span data-stu-id="24b34-153">Examples</span></span>

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
