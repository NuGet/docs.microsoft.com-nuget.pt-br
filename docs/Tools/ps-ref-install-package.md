---
title: Referência do pacote de instalação do NuGet PowerShell
description: Referência de comando do PowerShell do pacote de instalação no Console do Gerenciador de pacotes do NuGet no Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5adfbcae0affcaa402f7981c12e108490d546511
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="224bb-103">Pacote de instalação (Console de Gerenciador de pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="224bb-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="224bb-104">*Este tópico descreve o comando dentro de [NuGet Package Manager Console](package-manager-console.md) no Visual Studio no Windows. Para o comando PowerShell Install-Package genérico, consulte o [referência do PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="224bb-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="224bb-105">Instala um pacote e suas dependências em um projeto.</span><span class="sxs-lookup"><span data-stu-id="224bb-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="224bb-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="224bb-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="224bb-107">No NuGet 2.8 + `Install-Package` pode fazer downgrade de um pacote existente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="224bb-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="224bb-108">Por exemplo, se você tiver 5.1.0-rc1 Microsoft.AspNet.MVC instalado, o comando a seguir seria o downgrade dele para 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="224bb-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="224bb-109">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="224bb-109">Parameters</span></span>

| <span data-ttu-id="224bb-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="224bb-110">Parameter</span></span> | <span data-ttu-id="224bb-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="224bb-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="224bb-112">Id</span><span class="sxs-lookup"><span data-stu-id="224bb-112">Id</span></span> | <span data-ttu-id="224bb-113">(Obrigatório) O identificador do pacote para instalar.</span><span class="sxs-lookup"><span data-stu-id="224bb-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="224bb-114">(*3.0 +*) o identificador pode ser um caminho ou URL de um `packages.config` arquivo ou um `.nupkg` arquivo.</span><span class="sxs-lookup"><span data-stu-id="224bb-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="224bb-115">-Id switch é opcional.</span><span class="sxs-lookup"><span data-stu-id="224bb-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="224bb-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="224bb-116">IgnoreDependencies</span></span> | <span data-ttu-id="224bb-117">Instale apenas esse pacote e não suas dependências.</span><span class="sxs-lookup"><span data-stu-id="224bb-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="224bb-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="224bb-118">ProjectName</span></span> | <span data-ttu-id="224bb-119">O projeto no qual instalar o pacote, o padrão para o projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="224bb-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="224bb-120">Origem</span><span class="sxs-lookup"><span data-stu-id="224bb-120">Source</span></span> | <span data-ttu-id="224bb-121">O caminho de URL ou pasta para a origem do pacote a ser pesquisado.</span><span class="sxs-lookup"><span data-stu-id="224bb-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="224bb-122">Caminhos de pasta local podem ser absoluto ou relativo para a pasta atual.</span><span class="sxs-lookup"><span data-stu-id="224bb-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="224bb-123">Se omitido, `Install-Package` procura a origem de pacote selecionada atualmente.</span><span class="sxs-lookup"><span data-stu-id="224bb-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="224bb-124">Versão</span><span class="sxs-lookup"><span data-stu-id="224bb-124">Version</span></span> | <span data-ttu-id="224bb-125">A versão do pacote de instalação, o padrão para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="224bb-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="224bb-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="224bb-126">IncludePrerelease</span></span> | <span data-ttu-id="224bb-127">Considera os pacotes de pré-lançamento para a instalação.</span><span class="sxs-lookup"><span data-stu-id="224bb-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="224bb-128">Se omitido, apenas pacotes estáveis serão considerados.</span><span class="sxs-lookup"><span data-stu-id="224bb-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="224bb-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="224bb-129">FileConflictAction</span></span> | <span data-ttu-id="224bb-130">A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes, referenciados pelo projeto.</span><span class="sxs-lookup"><span data-stu-id="224bb-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="224bb-131">Os valores possíveis são *substituir, ignorar, None, OverwriteAll*, e *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="224bb-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="224bb-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="224bb-132">DependencyVersion</span></span> | <span data-ttu-id="224bb-133">A versão dos pacotes de dependência a usar, que pode ser um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="224bb-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="224bb-134">*Menor* (padrão): a versão mais antiga</span><span class="sxs-lookup"><span data-stu-id="224bb-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="224bb-135">*HighestPatch*: a versão com o patch mais baixo principal, secundária menor, mais alto</span><span class="sxs-lookup"><span data-stu-id="224bb-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="224bb-136">*HighestMinor*: a versão com o menor principais, mais alto patch menor, mais alto</span><span class="sxs-lookup"><span data-stu-id="224bb-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="224bb-137">*Mais alto* (padrão para o pacote de atualização sem parâmetros): a versão mais recente</span><span class="sxs-lookup"><span data-stu-id="224bb-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="224bb-138">Você pode definir o valor padrão usando o [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) definindo no `Nuget.Config` arquivo.</span><span class="sxs-lookup"><span data-stu-id="224bb-138">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="224bb-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="224bb-139">WhatIf</span></span> | <span data-ttu-id="224bb-140">Mostra o que aconteceria quando a execução do comando sem realmente executar a instalação.</span><span class="sxs-lookup"><span data-stu-id="224bb-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="224bb-141">Nenhum desses parâmetros aceitar caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="224bb-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="224bb-142">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="224bb-142">Common Parameters</span></span>

<span data-ttu-id="224bb-143">`Install-Package` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, WarningAction, detalhado e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="224bb-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="224bb-144">Exemplos</span><span class="sxs-lookup"><span data-stu-id="224bb-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
