---
title: Instalar e gerenciar pacotes NuGet usando a CLI do dotnet
description: Instruções de uso da CLI do dotnet para trabalhar com pacotes NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 38455e61bd91f115df9f27df090ba47a029f6877
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622935"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="a635e-103">Instalar e gerenciar pacotes usando a CLI do dotnet</span><span class="sxs-lookup"><span data-stu-id="a635e-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="a635e-104">A ferramenta CLI permite que você instale, desinstale e atualize pacotes NuGet com facilidade em projetos e soluções.</span><span class="sxs-lookup"><span data-stu-id="a635e-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="a635e-105">Ela é executada no Windows, no Mac OS X e no Linux.</span><span class="sxs-lookup"><span data-stu-id="a635e-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="a635e-106">A CLI do dotnet destina-se ao uso em seu projeto .NET Core e .NET Standard (tipos de projeto no estilo SDK) e a todos os outros projetos no estilo SDK (por exemplo, um projeto no estilo SDK direcionado ao .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="a635e-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="a635e-107">Para obter mais informações, confira [Atributo SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="a635e-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="a635e-108">Este artigo mostra o uso básico de alguns dos comandos mais comuns da CLI do dotnet.</span><span class="sxs-lookup"><span data-stu-id="a635e-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="a635e-109">Para a maioria desses comandos, a ferramenta CLI procura um arquivo de projeto no diretório atual, a menos que um arquivo de projeto seja especificado no comando (o arquivo de projeto é uma opção facultativa).</span><span class="sxs-lookup"><span data-stu-id="a635e-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="a635e-110">Para obter uma lista completa de comandos e os argumentos que podem ser usados, confira [Ferramentas da CLI (interface de linha de comando) do .NET Core](../reference/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="a635e-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../reference/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a635e-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a635e-111">Prerequisites</span></span>

- <span data-ttu-id="a635e-112">O [SDK do .NET Core](https://www.microsoft.com/net/download/), que fornece a ferramenta de linha de comando `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="a635e-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="a635e-113">No Visual Studio 2017 em diante, a CLI do dotnet é instalada automaticamente com qualquer carga de trabalho relacionada ao .NET Core.</span><span class="sxs-lookup"><span data-stu-id="a635e-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="a635e-114">Instalar um pacote</span><span class="sxs-lookup"><span data-stu-id="a635e-114">Install a package</span></span>

<span data-ttu-id="a635e-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adiciona uma referência de pacote ao arquivo de projeto e, em seguida, executa `dotnet restore` para instalar o pacote.</span><span class="sxs-lookup"><span data-stu-id="a635e-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="a635e-116">Abra uma linha de comando e alterne para o diretório que contém o arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="a635e-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="a635e-117">Use o seguinte comando para instalar um pacote NuGet:</span><span class="sxs-lookup"><span data-stu-id="a635e-117">Use the following command to install a Nuget package:</span></span>

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="a635e-118">Por exemplo, para instalar o pacote `Newtonsoft.Json`, use o comando a seguir</span><span class="sxs-lookup"><span data-stu-id="a635e-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="a635e-119">Após a conclusão do comando, examine o arquivo de projeto para verificar se o pacote foi instalado.</span><span class="sxs-lookup"><span data-stu-id="a635e-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="a635e-120">Abra o arquivo `.csproj` para ver a referência adicionada:</span><span class="sxs-lookup"><span data-stu-id="a635e-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="a635e-121">Instalar uma versão específica de um pacote</span><span class="sxs-lookup"><span data-stu-id="a635e-121">Install a specific version of a package</span></span>

<span data-ttu-id="a635e-122">Se a versão não for especificada, o NuGet instalará a última versão do pacote.</span><span class="sxs-lookup"><span data-stu-id="a635e-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="a635e-123">Use também o comando [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) para instalar uma versão específica de um pacote NuGet:</span><span class="sxs-lookup"><span data-stu-id="a635e-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```dotnetcli
dotnet add package <PACKAGE_NAME> --version <VERSION>
```

<span data-ttu-id="a635e-124">Por exemplo, para adicionar a versão 12.0.1 do pacote `Newtonsoft.Json`, use este comando:</span><span class="sxs-lookup"><span data-stu-id="a635e-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```dotnetcli
dotnet add package Newtonsoft.Json --version 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="a635e-125">Listar as referências de pacote</span><span class="sxs-lookup"><span data-stu-id="a635e-125">List package references</span></span>

<span data-ttu-id="a635e-126">Liste as referências de pacote para o projeto usando o comando [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="a635e-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="a635e-127">Remover um pacote</span><span class="sxs-lookup"><span data-stu-id="a635e-127">Remove a package</span></span>

<span data-ttu-id="a635e-128">Use o comando [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) para remover uma referência de pacote do arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="a635e-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="a635e-129">Por exemplo, para remover o pacote `Newtonsoft.Json`, use o comando a seguir</span><span class="sxs-lookup"><span data-stu-id="a635e-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="a635e-130">Atualizar um pacote</span><span class="sxs-lookup"><span data-stu-id="a635e-130">Update a package</span></span>

<span data-ttu-id="a635e-131">O NuGet instala a última versão do pacote quando você usa o comando `dotnet add package`, a menos que você especifique a versão do pacote (opção `-v`).</span><span class="sxs-lookup"><span data-stu-id="a635e-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="a635e-132">Restaurar pacotes</span><span class="sxs-lookup"><span data-stu-id="a635e-132">Restore packages</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
