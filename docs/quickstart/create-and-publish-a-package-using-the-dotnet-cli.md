---
title: Criar e publicar um pacote do NuGet usando a CLI dotnet
description: Um tutorial passo a passo sobre como criar e publicar um pacote NuGet usando a CLI do .NET Core, dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 30a77b427fe0a33b41262c5784045e5a6b10852f
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419988"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="d333b-103">Início Rápido: Criar e publicar um pacote (CLI do dotnet)</span><span class="sxs-lookup"><span data-stu-id="d333b-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="d333b-104">É um processo simples para criar um pacote NuGet de uma Biblioteca de Classes do .NET e publique-o em nuget.org usando a CLI (interface de linha de comando) `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="d333b-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d333b-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d333b-105">Prerequisites</span></span>

1. <span data-ttu-id="d333b-106">Instale o [SDK do .NET Core](https://www.microsoft.com/net/download/), que inclui a CLI do `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="d333b-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="d333b-107">No Visual Studio 2017 em diante, a CLI do dotnet é instalada automaticamente com qualquer carga de trabalho relacionada ao .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d333b-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="d333b-108">[Registre-se em uma conta gratuita em nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), se ainda não tiver uma.</span><span class="sxs-lookup"><span data-stu-id="d333b-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="d333b-109">Criar uma nova conta envia um email de confirmação.</span><span class="sxs-lookup"><span data-stu-id="d333b-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="d333b-110">Você deve confirmar a conta antes de poder carregar um pacote.</span><span class="sxs-lookup"><span data-stu-id="d333b-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="d333b-111">Criar um projeto de biblioteca de classes</span><span class="sxs-lookup"><span data-stu-id="d333b-111">Create a class library project</span></span>

<span data-ttu-id="d333b-112">Você pode usar um projeto existente da Biblioteca de Classes .NET para o código que você deseja empacotar, ou criar um simples da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d333b-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="d333b-113">Crie uma pasta chamada `AppLogger` e altere para ela.</span><span class="sxs-lookup"><span data-stu-id="d333b-113">Create a folder called `AppLogger` and change into it.</span></span>

1. <span data-ttu-id="d333b-114">Crie o projeto usando `dotnet new classlib`, que usa o nome da pasta atual para o projeto.</span><span class="sxs-lookup"><span data-stu-id="d333b-114">Create the project using `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="d333b-115">Adicionar metadados de pacote ao arquivo de projeto</span><span class="sxs-lookup"><span data-stu-id="d333b-115">Add package metadata to the project file</span></span>

<span data-ttu-id="d333b-116">Todos os pacotes NuGet precisam de um manifesto que descreve seu conteúdo e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="d333b-116">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="d333b-117">Em um pacote final, o manifesto é um arquivo `.nuspec` gerado das propriedades de metadados do NuGet que você inclui no arquivo do projeto.</span><span class="sxs-lookup"><span data-stu-id="d333b-117">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="d333b-118">Abra o arquivo de projeto (`.csproj`) e adicione as seguintes propriedades mínimas dentro da marca `<PropertyGroup>` existente, alterando os valores conforme apropriado:</span><span class="sxs-lookup"><span data-stu-id="d333b-118">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="d333b-119">Dê ao pacote um identificador exclusivo em nuget.org ou qualquer host que você esteja usando.</span><span class="sxs-lookup"><span data-stu-id="d333b-119">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="d333b-120">Para este passo a passo, recomendamos incluir o "Sample" ou "Test" no nome, pois a etapa de publicação posterior torna o pacote publicamente visível (embora seja improvável que alguém possa usá-lo).</span><span class="sxs-lookup"><span data-stu-id="d333b-120">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="d333b-121">Adicione propriedades opcionais descritas em [Propriedades de metadados do NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="d333b-121">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="d333b-122">Para pacotes compilados para consumo público, preste atenção especial à propriedade **PackageTags**, à medida que as marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.</span><span class="sxs-lookup"><span data-stu-id="d333b-122">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="d333b-123">Executar o comando pack</span><span class="sxs-lookup"><span data-stu-id="d333b-123">Run the pack command</span></span>

<span data-ttu-id="d333b-124">Para compilar um pacote do NuGet (um arquivo `.nupkg`) do projeto, execute o comando `dotnet pack`, que também compila o projeto automaticamente:</span><span class="sxs-lookup"><span data-stu-id="d333b-124">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="d333b-125">A saída mostra o caminho até o arquivo `.nupkg`:</span><span class="sxs-lookup"><span data-stu-id="d333b-125">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="d333b-126">Gerar pacote automaticamente no build</span><span class="sxs-lookup"><span data-stu-id="d333b-126">Automatically generate package on build</span></span>

<span data-ttu-id="d333b-127">Para executar `dotnet pack` automaticamente ao executar `dotnet build`, adicione a seguinte linha ao arquivo de projeto em `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="d333b-127">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="d333b-128">Publicar o pacote</span><span class="sxs-lookup"><span data-stu-id="d333b-128">Publish the package</span></span>

<span data-ttu-id="d333b-129">Depois que você tiver um arquivo `.nupkg`, publique-o em nuget.org usando o comando `dotnet nuget push` juntamente com uma chave de API adquirida em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d333b-129">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="d333b-130">Adquirir a chave de sua API</span><span class="sxs-lookup"><span data-stu-id="d333b-130">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="d333b-131">Publicar com dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="d333b-131">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="d333b-132">Erros de publicação</span><span class="sxs-lookup"><span data-stu-id="d333b-132">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="d333b-133">Gerenciar o pacote publicado</span><span class="sxs-lookup"><span data-stu-id="d333b-133">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a><span data-ttu-id="d333b-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d333b-134">Next steps</span></span>

<span data-ttu-id="d333b-135">Parabéns por criar seu primeiro pacote do NuGet!</span><span class="sxs-lookup"><span data-stu-id="d333b-135">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d333b-136">Criar um pacote</span><span class="sxs-lookup"><span data-stu-id="d333b-136">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)

<span data-ttu-id="d333b-137">Para ver o que mais o NuGet tem a oferecer, selecione os links abaixo.</span><span class="sxs-lookup"><span data-stu-id="d333b-137">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="d333b-138">Publicar um pacote</span><span class="sxs-lookup"><span data-stu-id="d333b-138">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="d333b-139">Pacotes de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="d333b-139">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="d333b-140">Suporte a várias estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="d333b-140">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="d333b-141">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="d333b-141">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="d333b-142">Criando pacotes localizados</span><span class="sxs-lookup"><span data-stu-id="d333b-142">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="d333b-143">Criando pacotes de símbolos</span><span class="sxs-lookup"><span data-stu-id="d333b-143">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="d333b-144">Assinando pacotes</span><span class="sxs-lookup"><span data-stu-id="d333b-144">Signing packages</span></span>](../create-packages/Sign-a-package.md)
