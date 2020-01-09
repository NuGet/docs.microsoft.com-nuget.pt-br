---
title: Atualização do NuGet-referência do PowerShell do pacote
description: Referência para o comando Update-Package do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e1bff9d4b7391d8be87afa4b8f2fbd51ae922140
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384850"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="43891-103">Update-Package (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="43891-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="43891-104">*Disponível somente no [console do Gerenciador de pacotes NuGet](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows.*</span><span class="sxs-lookup"><span data-stu-id="43891-104">*Available only within the [NuGet Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="43891-105">Atualiza um pacote e suas dependências, ou todos os pacotes em um projeto, para uma versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="43891-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="43891-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="43891-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="43891-107">No NuGet 2.8 +, `Update-Package` pode ser usado para fazer downgrade de um pacote existente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="43891-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="43891-108">Por exemplo, se você tiver o Microsoft. AspNet. MVC 5.1.0-RC1 instalado, o comando a seguir o desfazeria para 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="43891-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="43891-109">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="43891-109">Parameters</span></span>

|  <span data-ttu-id="43891-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="43891-110">Parameter</span></span> | <span data-ttu-id="43891-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="43891-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="43891-112">Id</span><span class="sxs-lookup"><span data-stu-id="43891-112">Id</span></span> | <span data-ttu-id="43891-113">O identificador do pacote a ser atualizado.</span><span class="sxs-lookup"><span data-stu-id="43891-113">The identifier of the package to update.</span></span> <span data-ttu-id="43891-114">Se omitido, atualiza todos os pacotes.</span><span class="sxs-lookup"><span data-stu-id="43891-114">If omitted, updates all packages.</span></span> <span data-ttu-id="43891-115">A opção-ID em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="43891-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="43891-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="43891-116">IgnoreDependencies</span></span> | <span data-ttu-id="43891-117">Ignora a atualização das dependências do pacote.</span><span class="sxs-lookup"><span data-stu-id="43891-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="43891-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="43891-118">ProjectName</span></span> | <span data-ttu-id="43891-119">O nome do projeto que contém os pacotes a serem atualizados, padronizando para todos os projetos.</span><span class="sxs-lookup"><span data-stu-id="43891-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="43891-120">Versão do</span><span class="sxs-lookup"><span data-stu-id="43891-120">Version</span></span> | <span data-ttu-id="43891-121">A versão a ser usada para a atualização, padronizando para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="43891-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="43891-122">No NuGet 3.0 +, o valor da versão deve ser um dos *mais baixo, mais alto, HighestMinor*ou *HighestPatch* (equivalente a seguro).</span><span class="sxs-lookup"><span data-stu-id="43891-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="43891-123">Safe</span><span class="sxs-lookup"><span data-stu-id="43891-123">Safe</span></span> | <span data-ttu-id="43891-124">Restringe atualizações para apenas versões com a mesma versão principal e secundária do pacote atualmente instalado.</span><span class="sxs-lookup"><span data-stu-id="43891-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="43891-125">Source</span><span class="sxs-lookup"><span data-stu-id="43891-125">Source</span></span> | <span data-ttu-id="43891-126">O caminho da URL ou da pasta para a origem do pacote a ser pesquisado.</span><span class="sxs-lookup"><span data-stu-id="43891-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="43891-127">Os caminhos de pasta local podem ser absolutos ou relativos à pasta atual.</span><span class="sxs-lookup"><span data-stu-id="43891-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="43891-128">Se for omitido, `Update-Package` pesquisará a origem do pacote selecionada no momento.</span><span class="sxs-lookup"><span data-stu-id="43891-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="43891-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="43891-129">IncludePrerelease</span></span> | <span data-ttu-id="43891-130">Inclui pacotes de pré-lançamento para atualizações.</span><span class="sxs-lookup"><span data-stu-id="43891-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="43891-131">Reinstalar</span><span class="sxs-lookup"><span data-stu-id="43891-131">Reinstall</span></span> | <span data-ttu-id="43891-132">Pacotes Resintalls usando suas versões atualmente instaladas.</span><span class="sxs-lookup"><span data-stu-id="43891-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="43891-133">Confira [Reinstalando e atualizando pacotes](../../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="43891-133">See [Reinstalling and updating packages](../../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="43891-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="43891-134">FileConflictAction</span></span> | <span data-ttu-id="43891-135">A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes referenciados pelo projeto.</span><span class="sxs-lookup"><span data-stu-id="43891-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="43891-136">Os valores possíveis são *overwrite, ignore, None, OverwriteAll*e *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="43891-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="43891-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="43891-137">DependencyVersion</span></span> | <span data-ttu-id="43891-138">A versão dos pacotes de dependência a serem usados, que pode ser uma das seguintes:</span><span class="sxs-lookup"><span data-stu-id="43891-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="43891-139">*Mais baixo* (padrão): a versão mais baixa</span><span class="sxs-lookup"><span data-stu-id="43891-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="43891-140">*HighestPatch*: a versão com o menor principal, menor o mais baixo, patch mais alto</span><span class="sxs-lookup"><span data-stu-id="43891-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="43891-141">*HighestMinor*: a versão com o menor principal, o mais baixo, o patch mais alto</span><span class="sxs-lookup"><span data-stu-id="43891-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="43891-142">*Mais alto* (padrão para update-package sem parâmetros): a versão mais recente</span><span class="sxs-lookup"><span data-stu-id="43891-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="43891-143">Você pode definir o valor padrão usando a configuração de [`dependencyVersion`](../nuget-config-file.md#config-section) no arquivo de `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="43891-143">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="43891-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="43891-144">ToHighestPatch</span></span> | <span data-ttu-id="43891-145">equivalente a-Safe.</span><span class="sxs-lookup"><span data-stu-id="43891-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="43891-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="43891-146">ToHighestMinor</span></span> | <span data-ttu-id="43891-147">Restringe atualizações para apenas versões com a mesma versão principal do pacote atualmente instalado.</span><span class="sxs-lookup"><span data-stu-id="43891-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="43891-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="43891-148">WhatIf</span></span> | <span data-ttu-id="43891-149">Mostra o que aconteceria ao executar o comando sem realmente executar a atualização.</span><span class="sxs-lookup"><span data-stu-id="43891-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="43891-150">Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="43891-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="43891-151">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="43891-151">Common Parameters</span></span>

<span data-ttu-id="43891-152">o `Update-Package` dá suporte aos seguintes [parâmetros comuns do PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="43891-152">`Update-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="43891-153">Exemplos</span><span class="sxs-lookup"><span data-stu-id="43891-153">Examples</span></span>

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
