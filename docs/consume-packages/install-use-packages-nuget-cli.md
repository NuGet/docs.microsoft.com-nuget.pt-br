---
title: Gerenciar pacotes NuGet usando a CLI do nuget.exe
description: Instruções sobre como usar a CLI do nuget.exe para trabalhar com pacotes NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 9ef990c16cca62a1fbad25ff1582bfa543135fab
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860578"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="bc726-103">Gerenciar pacotes usando a CLI do nuget.exe</span><span class="sxs-lookup"><span data-stu-id="bc726-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="bc726-104">A ferramenta CLI permite que você atualize e restaure pacotes NuGet com facilidade em projetos e soluções.</span><span class="sxs-lookup"><span data-stu-id="bc726-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="bc726-105">Essa ferramenta fornece todas as funcionalidades do NuGet no Windows e também fornece a maioria dos recursos no Mac e no Linux durante a execução no Mono.</span><span class="sxs-lookup"><span data-stu-id="bc726-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="bc726-106">A CLI `nuget.exe` destina-se a seu projeto .NET Framework e a projetos no estilo não SDK (por exemplo, um projeto de estilo não SDK direcionado a bibliotecas .NET Standard).</span><span class="sxs-lookup"><span data-stu-id="bc726-106">The `nuget.exe` CLI is for your .NET Framework project and non-SDK-style projects (for example, a non-SDK style project that targets .NET Standard libraries).</span></span> <span data-ttu-id="bc726-107">Caso esteja usando um projeto no estilo não SDK que foi migrado para `PackageReference`, use a CLI `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="bc726-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the `dotnet` CLI instead.</span></span> <span data-ttu-id="bc726-108">A CLI `nuget.exe` exige um arquivo [packages.config](../reference/packages-config.md) para referências de pacote.</span><span class="sxs-lookup"><span data-stu-id="bc726-108">The `nuget.exe` CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="bc726-109">Na maioria dos cenários, recomendamos [migrar os projetos no estilo não SDK](../reference/migrate-packages-config-to-package-reference.md) que usam `packages.config` para PackageReference, assim é possível usar a CLI `dotnet` ao invés da CLI `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="bc726-109">In most scenarios, we recommend [migrating non-SDK-style projects](../reference/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the `dotnet` CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="bc726-110">Atualmente, a migração não está disponível para projetos C++ e ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="bc726-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="bc726-111">Este artigo mostra o uso básico de alguns dos comandos mais comuns da CLI `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="bc726-111">This article shows you basic usage for a few of the most common `nuget.exe` CLI commands.</span></span> <span data-ttu-id="bc726-112">Para a maioria desses comandos, a ferramenta CLI procura um arquivo de projeto no diretório atual, a menos que um arquivo de projeto seja especificado no comando.</span><span class="sxs-lookup"><span data-stu-id="bc726-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="bc726-113">Para obter uma lista completa de comandos e os argumentos que podem ser usados, confira [Referência da CLI do nuget.exe](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="bc726-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc726-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bc726-114">Prerequisites</span></span>

- <span data-ttu-id="bc726-115">Instale a CLI do `nuget.exe` baixando-a de [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), salvando o arquivo `.exe` em uma pasta adequada e adicionando pasta a variável de ambiente PATH.</span><span class="sxs-lookup"><span data-stu-id="bc726-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="bc726-116">Instalar um pacote</span><span class="sxs-lookup"><span data-stu-id="bc726-116">Install a package</span></span>

<span data-ttu-id="bc726-117">O comando [install](../reference/cli-reference/cli-ref-install.md) baixa e instala um pacote em um projeto, usando como padrão a pasta atual, com as origens do pacote especificadas.</span><span class="sxs-lookup"><span data-stu-id="bc726-117">The [install](../reference/cli-reference/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="bc726-118">Instale novos pacotes na pasta *packages* no diretório raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="bc726-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc726-119">O `install`comando não modifica um arquivo de projeto nem *packages.config*; dessa forma, ele é semelhante a `restore`, pois apenas adiciona pacotes ao disco, mas não altera as dependências de um projeto.</span><span class="sxs-lookup"><span data-stu-id="bc726-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="bc726-120">Para adicionar uma dependência, adicione um pacote por meio da interface do usuário do Gerenciador de Pacotes ou do Console no Visual Studio ou modifique *packages.config* e, em seguida, execute `install` ou `restore`.</span><span class="sxs-lookup"><span data-stu-id="bc726-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="bc726-121">Abra uma linha de comando e alterne para o diretório que contém o arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="bc726-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="bc726-122">Use o comando a seguir para instalar um pacote NuGet na pasta *packages*.</span><span class="sxs-lookup"><span data-stu-id="bc726-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="bc726-123">Para instalar o pacote `Newtonsoft.json` na pasta *packages*, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="bc726-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="bc726-124">Como alternativa, você pode usar o comando a seguir para instalar um pacote NuGet usando um arquivo `packages.config` existente na pasta *packages*.</span><span class="sxs-lookup"><span data-stu-id="bc726-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="bc726-125">Isso não adiciona o pacote às dependências do projeto, mas o instala localmente.</span><span class="sxs-lookup"><span data-stu-id="bc726-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="bc726-126">Instalar uma versão específica de um pacote</span><span class="sxs-lookup"><span data-stu-id="bc726-126">Install a specific version of a package</span></span>

<span data-ttu-id="bc726-127">Se a versão não for especificada quando você usar o comando [install](../reference/cli-reference/cli-ref-install.md), o NuGet instalará a última versão do pacote.</span><span class="sxs-lookup"><span data-stu-id="bc726-127">If the version is not specified when you use the [install](../reference/cli-reference/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="bc726-128">Instale também uma versão específica de um pacote NuGet:</span><span class="sxs-lookup"><span data-stu-id="bc726-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="bc726-129">Por exemplo, para adicionar a versão 12.0.1 do pacote `Newtonsoft.json`, use este comando:</span><span class="sxs-lookup"><span data-stu-id="bc726-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="bc726-130">Para obter mais informações sobre as limitações e o comportamento de `install`, confira [Instalar um pacote](#install-a-package).</span><span class="sxs-lookup"><span data-stu-id="bc726-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="bc726-131">Remover um pacote</span><span class="sxs-lookup"><span data-stu-id="bc726-131">Remove a package</span></span>

<span data-ttu-id="bc726-132">Para excluir um ou mais pacotes, exclua os pacotes que deseja remover da pasta *packages*.</span><span class="sxs-lookup"><span data-stu-id="bc726-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="bc726-133">Caso deseje reinstalar pacotes, use o comando `restore` ou `install`.</span><span class="sxs-lookup"><span data-stu-id="bc726-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="bc726-134">Listar pacotes</span><span class="sxs-lookup"><span data-stu-id="bc726-134">List packages</span></span>

<span data-ttu-id="bc726-135">Você pode exibir uma lista de pacotes de determinada fonte usando o comando [list](../reference/cli-reference/cli-ref-list.md).</span><span class="sxs-lookup"><span data-stu-id="bc726-135">You can display a list of packages from a given source using the [list](../reference/cli-reference/cli-ref-list.md) command.</span></span> <span data-ttu-id="bc726-136">Use a opção `-Source` para restringir a pesquisa.</span><span class="sxs-lookup"><span data-stu-id="bc726-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="bc726-137">Por exemplo, liste os pacotes da pasta *packages*.</span><span class="sxs-lookup"><span data-stu-id="bc726-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="bc726-138">Se você usar um termo de pesquisa, a pesquisa incluirá os nomes dos pacotes, as marcas e as descrições dos pacotes.</span><span class="sxs-lookup"><span data-stu-id="bc726-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="bc726-139">Atualizar um pacote individual</span><span class="sxs-lookup"><span data-stu-id="bc726-139">Update an individual package</span></span>

<span data-ttu-id="bc726-140">O NuGet instala a última versão do pacote quando você usa o comando `install`, a menos que você especifique a versão do pacote.</span><span class="sxs-lookup"><span data-stu-id="bc726-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="bc726-141">Atualizar todos os pacotes</span><span class="sxs-lookup"><span data-stu-id="bc726-141">Update all packages</span></span>

<span data-ttu-id="bc726-142">Use o comando [update](../reference/cli-reference/cli-ref-update.md) para atualizar todos os pacotes.</span><span class="sxs-lookup"><span data-stu-id="bc726-142">Use the [update](../reference/cli-reference/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="bc726-143">Atualiza todos os pacotes de um projeto (usando `packages.config`) para as últimas versões disponíveis.</span><span class="sxs-lookup"><span data-stu-id="bc726-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="bc726-144">É recomendável executar `restore` antes de executar `update`.</span><span class="sxs-lookup"><span data-stu-id="bc726-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="bc726-145">Restaurar pacotes</span><span class="sxs-lookup"><span data-stu-id="bc726-145">Restore packages</span></span>

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]