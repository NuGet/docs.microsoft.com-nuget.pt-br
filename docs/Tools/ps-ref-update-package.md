---
title: "Referência do pacote de atualização do NuGet PowerShell | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência de comando do PowerShell do pacote de atualização no Console do Gerenciador de pacotes do NuGet no Visual Studio."
keywords: "Console do Gerenciador, comandos do Powershell do NuGet, referência do Powershell do NuGet, pacote de atualização do pacote NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 768fdb4d7c785b4f3ed9e70958390676ea965794
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="d1868-104">Pacote de atualização (Console de Gerenciador de pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d1868-104">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d1868-105">*Disponível apenas dentro de [NuGet Package Manager Console](Package-Manager-Console.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="d1868-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="d1868-106">Atualiza um pacote e suas dependências ou todos os pacotes em um projeto, para uma versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="d1868-106">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="d1868-107">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="d1868-107">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="d1868-108">No NuGet 2.8 + `Update-Package` pode ser usado para fazer o downgrade de um pacote existente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="d1868-108">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="d1868-109">Por exemplo, se você tiver 5.1.0-rc1 Microsoft.AspNet.MVC instalado, o comando a seguir seria o downgrade dele para 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="d1868-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

<span data-ttu-id="d1868-110">NuGet 2.7 e anterior fornece uma mensagem de erro informando que uma versão mais recente já está instalada.</span><span class="sxs-lookup"><span data-stu-id="d1868-110">NuGet 2.7 and earlier gives an error saying that a newer version is already installed.</span></span>

## <a name="parameters"></a><span data-ttu-id="d1868-111">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="d1868-111">Parameters</span></span>

|  <span data-ttu-id="d1868-112">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d1868-112">Parameter</span></span> | <span data-ttu-id="d1868-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="d1868-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1868-114">Id</span><span class="sxs-lookup"><span data-stu-id="d1868-114">Id</span></span> | <span data-ttu-id="d1868-115">O identificador do pacote para atualizar.</span><span class="sxs-lookup"><span data-stu-id="d1868-115">The identifier of the package to update.</span></span> <span data-ttu-id="d1868-116">Se omitido, todos os pacotes de atualizações.</span><span class="sxs-lookup"><span data-stu-id="d1868-116">If omitted, updates all packages.</span></span> <span data-ttu-id="d1868-117">-Id switch é opcional.</span><span class="sxs-lookup"><span data-stu-id="d1868-117">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="d1868-118">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="d1868-118">IgnoreDependencies</span></span> | <span data-ttu-id="d1868-119">Ignora a dependências do pacote de atualização.</span><span class="sxs-lookup"><span data-stu-id="d1868-119">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="d1868-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="d1868-120">ProjectName</span></span> | <span data-ttu-id="d1868-121">O nome do projeto que contém os pacotes para atualizar, padronizando para todos os projetos.</span><span class="sxs-lookup"><span data-stu-id="d1868-121">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="d1868-122">Versão</span><span class="sxs-lookup"><span data-stu-id="d1868-122">Version</span></span> | <span data-ttu-id="d1868-123">A versão a ser usado para a atualização, o padrão para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="d1868-123">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="d1868-124">No NuGet 3.0 +, o valor de versão deve ser um dos *menor, mais alta, HighestMinor*, ou *HighestPatch* (equivalente a - Safe).</span><span class="sxs-lookup"><span data-stu-id="d1868-124">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="d1868-125">Safe</span><span class="sxs-lookup"><span data-stu-id="d1868-125">Safe</span></span> | <span data-ttu-id="d1868-126">Restringe as atualizações para versões somente com a mesma versão principal e secundária do pacote instalado atualmente.</span><span class="sxs-lookup"><span data-stu-id="d1868-126">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="d1868-127">Origem</span><span class="sxs-lookup"><span data-stu-id="d1868-127">Source</span></span> | <span data-ttu-id="d1868-128">O caminho de URL ou pasta para a origem do pacote a ser pesquisado.</span><span class="sxs-lookup"><span data-stu-id="d1868-128">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="d1868-129">Caminhos de pasta local podem ser absoluto ou relativo para a pasta atual.</span><span class="sxs-lookup"><span data-stu-id="d1868-129">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="d1868-130">Se omitido, `Uninstall-Package` procura a origem de pacote selecionada atualmente.</span><span class="sxs-lookup"><span data-stu-id="d1868-130">If omitted, `Uninstall-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="d1868-131">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="d1868-131">IncludePrerelease</span></span> | <span data-ttu-id="d1868-132">Inclui pacotes de pré-lançamento de atualizações.</span><span class="sxs-lookup"><span data-stu-id="d1868-132">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="d1868-133">Reinstalar</span><span class="sxs-lookup"><span data-stu-id="d1868-133">Reinstall</span></span> | <span data-ttu-id="d1868-134">Pacotes de Resintalls usando as versões atualmente instaladas.</span><span class="sxs-lookup"><span data-stu-id="d1868-134">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="d1868-135">Consulte [reinstalação e atualização de pacotes](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="d1868-135">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="d1868-136">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="d1868-136">FileConflictAction</span></span> | <span data-ttu-id="d1868-137">A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes, referenciados pelo projeto.</span><span class="sxs-lookup"><span data-stu-id="d1868-137">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="d1868-138">Os valores possíveis são *substituir, ignorar, None, OverwriteAll*, e *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="d1868-138">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="d1868-139">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="d1868-139">DependencyVersion</span></span> | <span data-ttu-id="d1868-140">A versão dos pacotes de dependência a usar, que pode ser um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="d1868-140">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="d1868-141">*Menor* (padrão): a versão mais antiga</span><span class="sxs-lookup"><span data-stu-id="d1868-141">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="d1868-142">*HighestPatch*: a versão com o patch mais baixo principal, secundária menor, mais alto</span><span class="sxs-lookup"><span data-stu-id="d1868-142">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="d1868-143">*HighestMinor*: a versão com o menor principais, mais alto patch menor, mais alto</span><span class="sxs-lookup"><span data-stu-id="d1868-143">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="d1868-144">*Mais alto* (padrão para o pacote de atualização sem parâmetros): a versão mais recente</span><span class="sxs-lookup"><span data-stu-id="d1868-144">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="d1868-145">Você pode definir o valor padrão usando o [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) definindo no `Nuget.Config` arquivo.</span><span class="sxs-lookup"><span data-stu-id="d1868-145">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="d1868-146">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="d1868-146">ToHighestPatch</span></span> | <span data-ttu-id="d1868-147">Restringe as atualizações para somente versões com a mesma versão secundária do pacote instalado atualmente.</span><span class="sxs-lookup"><span data-stu-id="d1868-147">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="d1868-148">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="d1868-148">ToHighestMinor</span></span> | <span data-ttu-id="d1868-149">Restringe as atualizações para somente versões com a mesma versão principal do pacote instalado atualmente.</span><span class="sxs-lookup"><span data-stu-id="d1868-149">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="d1868-150">WhatIf</span><span class="sxs-lookup"><span data-stu-id="d1868-150">WhatIf</span></span> | <span data-ttu-id="d1868-151">Mostra o que aconteceria quando a execução do comando sem realmente executar a atualização.</span><span class="sxs-lookup"><span data-stu-id="d1868-151">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="d1868-152">Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="d1868-152">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="d1868-153">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="d1868-153">Common Parameters</span></span>

<span data-ttu-id="d1868-154">`Update-Package`suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d1868-154">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="d1868-155">Exemplos</span><span class="sxs-lookup"><span data-stu-id="d1868-155">Examples</span></span>

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