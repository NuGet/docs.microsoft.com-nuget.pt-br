---
title: Referência do PowerShell NuGet Install-Package
description: Referência de comando do PowerShell de Install-Package no Console do Gerenciador de pacotes NuGet no Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 755c87bbc68d3b688c81e16edbc1faabdc9e0520
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842495"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="d9083-103">Install-Package (Console do Gerenciador de Pacotes no Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d9083-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d9083-104">*Este tópico descreve o comando dentro de [Package Manager Console](package-manager-console.md) no Visual Studio no Windows. Para o comando do PowerShell Install-Package genérico, consulte o [referência do PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="d9083-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="d9083-105">Instala um pacote e suas dependências em um projeto.</span><span class="sxs-lookup"><span data-stu-id="d9083-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="d9083-106">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="d9083-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="d9083-107">No NuGet 2.8 ou superior, `Install-Package` pode fazer downgrade de um pacote existente em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="d9083-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="d9083-108">Por exemplo, se você tiver 5.1.0-rc1 ASPNET instalado, o comando a seguir seria fazer o downgrade para 5.0.0:</span><span class="sxs-lookup"><span data-stu-id="d9083-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="d9083-109">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="d9083-109">Parameters</span></span>

| <span data-ttu-id="d9083-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d9083-110">Parameter</span></span> | <span data-ttu-id="d9083-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="d9083-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d9083-112">Id</span><span class="sxs-lookup"><span data-stu-id="d9083-112">Id</span></span> | <span data-ttu-id="d9083-113">(Obrigatório) O identificador do pacote a instalar.</span><span class="sxs-lookup"><span data-stu-id="d9083-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="d9083-114">(*3.0 ou superior*) o identificador pode ser um caminho ou URL de um `packages.config` arquivo ou um `.nupkg` arquivo.</span><span class="sxs-lookup"><span data-stu-id="d9083-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="d9083-115">-Id do comutador em si é opcional.</span><span class="sxs-lookup"><span data-stu-id="d9083-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="d9083-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="d9083-116">IgnoreDependencies</span></span> | <span data-ttu-id="d9083-117">Instale apenas esse pacote e não as suas dependências.</span><span class="sxs-lookup"><span data-stu-id="d9083-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="d9083-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="d9083-118">ProjectName</span></span> | <span data-ttu-id="d9083-119">O projeto no qual instalar o pacote, padronizando para o projeto padrão.</span><span class="sxs-lookup"><span data-stu-id="d9083-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="d9083-120">Origem</span><span class="sxs-lookup"><span data-stu-id="d9083-120">Source</span></span> | <span data-ttu-id="d9083-121">O caminho de URL ou pasta para a origem do pacote a pesquisar.</span><span class="sxs-lookup"><span data-stu-id="d9083-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="d9083-122">Caminhos de pasta local podem ser absoluto ou relativo à pasta atual.</span><span class="sxs-lookup"><span data-stu-id="d9083-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="d9083-123">Se omitido, `Install-Package` procura a origem do pacote selecionado no momento.</span><span class="sxs-lookup"><span data-stu-id="d9083-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="d9083-124">Versão</span><span class="sxs-lookup"><span data-stu-id="d9083-124">Version</span></span> | <span data-ttu-id="d9083-125">A versão do pacote a instalar, padronizando para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="d9083-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="d9083-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="d9083-126">IncludePrerelease</span></span> | <span data-ttu-id="d9083-127">Considera os pacotes de pré-lançamento para a instalação.</span><span class="sxs-lookup"><span data-stu-id="d9083-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="d9083-128">Se omitido, apenas os pacotes estáveis são considerados.</span><span class="sxs-lookup"><span data-stu-id="d9083-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="d9083-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="d9083-129">FileConflictAction</span></span> | <span data-ttu-id="d9083-130">A ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes, referenciados pelo projeto.</span><span class="sxs-lookup"><span data-stu-id="d9083-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="d9083-131">Os valores possíveis são *substituir, ignorar, None, OverwriteAll*, e *(3.0 ou superior)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="d9083-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="d9083-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="d9083-132">DependencyVersion</span></span> | <span data-ttu-id="d9083-133">A versão dos pacotes de dependência a ser usado, que pode ser um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="d9083-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="d9083-134">*Mais baixo* (padrão): a versão mais antiga</span><span class="sxs-lookup"><span data-stu-id="d9083-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="d9083-135">*HighestPatch*: a versão com o patch mais baixa principal, secundária menor, mais alto</span><span class="sxs-lookup"><span data-stu-id="d9083-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="d9083-136">*HighestMinor*: a versão com menor principais, o patch mais alto de pequena, mais alto</span><span class="sxs-lookup"><span data-stu-id="d9083-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="d9083-137">*Mais alto* (padrão para o pacote de atualização sem parâmetros): a versão mais recente</span><span class="sxs-lookup"><span data-stu-id="d9083-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="d9083-138">Você pode definir o valor padrão usando o [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) definindo no `Nuget.Config` arquivo.</span><span class="sxs-lookup"><span data-stu-id="d9083-138">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="d9083-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="d9083-139">WhatIf</span></span> | <span data-ttu-id="d9083-140">Mostra o que aconteceria ao executar o comando sem realmente executar a instalação.</span><span class="sxs-lookup"><span data-stu-id="d9083-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="d9083-141">Nenhum desses parâmetros aceitam caracteres curinga ou de entrada do pipeline.</span><span class="sxs-lookup"><span data-stu-id="d9083-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d9083-142">Parâmetros comuns</span><span class="sxs-lookup"><span data-stu-id="d9083-142">Common Parameters</span></span>

<span data-ttu-id="d9083-143">`Install-Package` suporta as seguintes [parâmetros comuns do PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Depuração, ação de erro, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, detalhado, WarningAction e WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d9083-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d9083-144">Exemplos</span><span class="sxs-lookup"><span data-stu-id="d9083-144">Examples</span></span>

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
