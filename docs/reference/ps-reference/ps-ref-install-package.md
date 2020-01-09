---
title: Instalação do NuGet – referência do PowerShell do pacote
description: Referência do comando install-Package do PowerShell no console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: a65ba63ed070f40e82c43d12e5fad12d86f28112
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384435"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f6b6e-103">Install-Package (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="f6b6e-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f6b6e-104">*Este tópico descreve o comando no [console do Gerenciador de pacotes](../../consume-packages/install-use-packages-powershell.md) no Visual Studio no Windows. Para o comando genérico do PowerShell Install-Package, consulte a [referência do PackageManagement do PowerShell](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="f6b6e-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="f6b6e-105">Instala um pacote e suas dependências em um projeto.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="f6b6e-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="f6b6e-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="f6b6e-107">No NuGet 2.8 +, `Install-Package` pode fazer downgrade de um pacote existente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="f6b6e-108">Por exemplo, se você tiver o Microsoft. AspNet. MVC 5.1.0-RC1 instalado, o comando a seguir o desfazeria para 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="f6b6e-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="f6b6e-109">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="f6b6e-109">Parameters</span></span>

| <span data-ttu-id="f6b6e-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="f6b6e-110">Parameter</span></span> | <span data-ttu-id="f6b6e-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="f6b6e-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f6b6e-112">Id</span><span class="sxs-lookup"><span data-stu-id="f6b6e-112">Id</span></span> | <span data-ttu-id="f6b6e-113">Necessária O identificador do pacote a ser instalado.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="f6b6e-114">(*3.0 +* ) O identificador pode ser um caminho ou uma URL de um arquivo de `packages.config` ou um arquivo de `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="f6b6e-115">A opção-ID em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="f6b6e-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="f6b6e-116">IgnoreDependencies</span></span> | <span data-ttu-id="f6b6e-117">Instale somente este pacote e não suas dependências.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="f6b6e-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="f6b6e-118">ProjectName</span></span> | <span data-ttu-id="f6b6e-119">O projeto no qual instalar o pacote, padronizando para o projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="f6b6e-120">Source</span><span class="sxs-lookup"><span data-stu-id="f6b6e-120">Source</span></span> | <span data-ttu-id="f6b6e-121">O caminho da URL ou da pasta para a origem do pacote a ser pesquisado.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="f6b6e-122">Os caminhos de pasta local podem ser absolutos ou relativos à pasta atual.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="f6b6e-123">Se for omitido, `Install-Package` pesquisará a origem do pacote selecionada no momento.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="f6b6e-124">Versão do</span><span class="sxs-lookup"><span data-stu-id="f6b6e-124">Version</span></span> | <span data-ttu-id="f6b6e-125">A versão do pacote a ser instalada, padronizando para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="f6b6e-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="f6b6e-126">IncludePrerelease</span></span> | <span data-ttu-id="f6b6e-127">Considera os pacotes de pré-lançamento para a instalação.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="f6b6e-128">Se omitido, apenas os pacotes estáveis são considerados.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="f6b6e-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="f6b6e-129">FileConflictAction</span></span> | <span data-ttu-id="f6b6e-130">A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes referenciados pelo projeto.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="f6b6e-131">Os valores possíveis são *overwrite, ignore, None, OverwriteAll*e *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="f6b6e-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="f6b6e-132">DependencyVersion</span></span> | <span data-ttu-id="f6b6e-133">A versão dos pacotes de dependência a serem usados, que pode ser uma das seguintes:</span><span class="sxs-lookup"><span data-stu-id="f6b6e-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="f6b6e-134">*Mais baixo* (padrão): a versão mais baixa</span><span class="sxs-lookup"><span data-stu-id="f6b6e-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="f6b6e-135">*HighestPatch*: a versão com o menor principal, menor o mais baixo, patch mais alto</span><span class="sxs-lookup"><span data-stu-id="f6b6e-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="f6b6e-136">*HighestMinor*: a versão com o menor principal, o mais baixo, o patch mais alto</span><span class="sxs-lookup"><span data-stu-id="f6b6e-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="f6b6e-137">*Mais alto* (padrão para update-package sem parâmetros): a versão mais recente</span><span class="sxs-lookup"><span data-stu-id="f6b6e-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="f6b6e-138">Você pode definir o valor padrão usando a configuração de [`dependencyVersion`](../nuget-config-file.md#config-section) no arquivo de `Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-138">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="f6b6e-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="f6b6e-139">WhatIf</span></span> | <span data-ttu-id="f6b6e-140">Mostra o que aconteceria ao executar o comando sem realmente executar a instalação.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="f6b6e-141">Nenhum desses parâmetros aceita a entrada de pipeline ou caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f6b6e-142">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="f6b6e-142">Common Parameters</span></span>

<span data-ttu-id="f6b6e-143">o `Install-Package` dá suporte aos seguintes [parâmetros comuns do PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debug, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f6b6e-143">`Install-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f6b6e-144">Exemplos</span><span class="sxs-lookup"><span data-stu-id="f6b6e-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
