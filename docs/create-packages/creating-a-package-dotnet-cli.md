---
title: Criar um pacote do NuGet usando a CLI dotnet
description: Um guia detalhado para o processo de design e criação de um pacote do NuGet, incluindo os principais pontos de decisão como arquivos e controle de versão.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 712e4c7159aa9719052330d8e45f63e18e390325
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230563"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="0ab86-103">Criar um pacote do NuGet usando a CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="0ab86-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="0ab86-104">Independentemente do pacote ou do código que ele contém, use uma das ferramentas de CLI, seja `nuget.exe` ou `dotnet.exe`, para empacotar essa funcionalidade em um componente que possa ser compartilhado e usado por diversos desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="0ab86-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="0ab86-105">Este artigo descreve como criar um pacote usando a CLI dotnet.</span><span class="sxs-lookup"><span data-stu-id="0ab86-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="0ab86-106">Para instalar a CLI `dotnet`, confira [Instalar as ferramentas de cliente do NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="0ab86-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="0ab86-107">A partir do Visual Studio 2017, a CLI dotnet está inclusa nas cargas de trabalho do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="0ab86-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="0ab86-108">Para projetos .NET Core e .NET Standard que usam projetos no [formato de estilo SDK](../resources/check-project-format.md) e quaisquer outros estilos SDK, o NuGet usa as informações do arquivo de projeto diretamente para criar um pacote.</span><span class="sxs-lookup"><span data-stu-id="0ab86-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="0ab86-109">Para ver tutoriais passo a passo, confira [Criar pacotes .NET Standard com a CLI dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) e [Criar pacotes .NET Standard com o Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="0ab86-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) or [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="0ab86-110">`msbuild -t:pack` é uma funcionalidade equivalente a `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="0ab86-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="0ab86-111">Para compilar com MSBuild, consulte [Criar um pacote NuGet usando MSBuild](creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="0ab86-111">To build with MSBuild, see [Create a NuGet package using MSBuild](creating-a-package-msbuild.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ab86-112">Este tópico aplica-se a projetos no [estilo SDK](../resources/check-project-format.md), normalmente projetos .NET Core e .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="0ab86-112">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="0ab86-113">Definir propriedades</span><span class="sxs-lookup"><span data-stu-id="0ab86-113">Set properties</span></span>

<span data-ttu-id="0ab86-114">As propriedades a seguir são necessárias para criar um pacote.</span><span class="sxs-lookup"><span data-stu-id="0ab86-114">The following properties are required to create a package.</span></span>

- <span data-ttu-id="0ab86-115">`PackageId`, o identificador de pacotes, que deve ser exclusivo na galeria que hospeda o pacote.</span><span class="sxs-lookup"><span data-stu-id="0ab86-115">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="0ab86-116">Se esse campo não for especificado, o valor padrão será `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="0ab86-116">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="0ab86-117">`Version`, um número de versão específico na forma *Principal.Secundário.Patch[-Sufixo]* em que *-Sufixo* identifica as [versões de pré-lançamento](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="0ab86-117">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="0ab86-118">Se esse campo não for especificado, o valor padrão será 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="0ab86-118">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="0ab86-119">O título do pacote como ele deve aparecer no host (como nuget.org)</span><span class="sxs-lookup"><span data-stu-id="0ab86-119">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="0ab86-120">`Authors`, informações de autor e proprietário.</span><span class="sxs-lookup"><span data-stu-id="0ab86-120">`Authors`, author and owner information.</span></span> <span data-ttu-id="0ab86-121">Se esse campo não for especificado, o valor padrão será `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="0ab86-121">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="0ab86-122">`Company`, o nome da empresa.</span><span class="sxs-lookup"><span data-stu-id="0ab86-122">`Company`, your company name.</span></span> <span data-ttu-id="0ab86-123">Se esse campo não for especificado, o valor padrão será `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="0ab86-123">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="0ab86-124">No Visual Studio, é possível definir esses valores nas propriedades do projeto (clique com o botão direito do mouse no projeto no Gerenciador de Soluções, escolha **Propriedades** e selecione a guia **Pacote**).</span><span class="sxs-lookup"><span data-stu-id="0ab86-124">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="0ab86-125">Você também pode definir essas propriedades diretamente nos arquivos do projeto (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="0ab86-125">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="0ab86-126">Dê ao pacote um identificador exclusivo em nuget.org ou qualquer origem de pacote que estiver usando.</span><span class="sxs-lookup"><span data-stu-id="0ab86-126">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="0ab86-127">O exemplo a seguir mostra um arquivo de projeto simples e completo com essas propriedades incluídas.</span><span class="sxs-lookup"><span data-stu-id="0ab86-127">The following example shows a simple, complete project file with these properties included.</span></span> <span data-ttu-id="0ab86-128">(Você pode criar um novo projeto padrão usando o comando `dotnet new classlib`.)</span><span class="sxs-lookup"><span data-stu-id="0ab86-128">(You can create a new default project using the `dotnet new classlib` command.)</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="0ab86-129">Defina também as propriedades opcionais, como `Title`, `PackageDescription` e `PackageTags`, conforme descrito em [Destinos do pacote MSBuild](../reference/msbuild-targets.md#pack-target), [Controlar ativos de dependência](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) e [Propriedades de metadados do NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="0ab86-129">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="0ab86-130">Para pacotes compilados para consumo público, preste atenção especial à propriedade **PackageTags**, à medida que as marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.</span><span class="sxs-lookup"><span data-stu-id="0ab86-130">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="0ab86-131">Para obter detalhes sobre como declarar dependências e especificar números de versão, consulte [Referências de pacote em arquivos de projeto](../consume-packages/package-references-in-project-files.md) e [Controle de versão do pacote](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="0ab86-131">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="0ab86-132">Também é possível extrair ativos de dependências diretamente no pacote usando os atributos `<IncludeAssets>` e `<ExcludeAssets>`.</span><span class="sxs-lookup"><span data-stu-id="0ab86-132">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="0ab86-133">Para saber mais, confira [Controlar ativos de dependência](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="0ab86-133">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="0ab86-134">Adicione um campo de descrição opcional</span><span class="sxs-lookup"><span data-stu-id="0ab86-134">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="0ab86-135">Escolher um identificador de pacote exclusivo e definir o número de versão</span><span class="sxs-lookup"><span data-stu-id="0ab86-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a><span data-ttu-id="0ab86-136">Executar o comando pack</span><span class="sxs-lookup"><span data-stu-id="0ab86-136">Run the pack command</span></span>

<span data-ttu-id="0ab86-137">Para compilar um pacote do NuGet (um arquivo `.nupkg`) do projeto, execute o comando `dotnet pack`, que também compila o projeto automaticamente:</span><span class="sxs-lookup"><span data-stu-id="0ab86-137">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="0ab86-138">A saída mostra o caminho até o arquivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="0ab86-138">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="0ab86-139">Gerar pacote automaticamente no build</span><span class="sxs-lookup"><span data-stu-id="0ab86-139">Automatically generate package on build</span></span>

<span data-ttu-id="0ab86-140">Para executar `dotnet pack` automaticamente ao executar `dotnet build`, adicione a seguinte linha ao arquivo de projeto em `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="0ab86-140">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="0ab86-141">Quando você `dotnet pack` executa em uma solução, isso embala todos[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) os projetos `true`na solução que são embalados (a propriedade está definida para ).</span><span class="sxs-lookup"><span data-stu-id="0ab86-141">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="0ab86-142">Ao gerar automaticamente o pacote, o tempo de empacotamento aumenta o tempo de compilação do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="0ab86-142">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="0ab86-143">Instalação do pacote de teste</span><span class="sxs-lookup"><span data-stu-id="0ab86-143">Test package installation</span></span>

<span data-ttu-id="0ab86-144">Antes de publicar um pacote, geralmente é recomendável testar o processo de instalação de um pacote em um projeto.</span><span class="sxs-lookup"><span data-stu-id="0ab86-144">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="0ab86-145">Os testes garantem que os arquivos todos terminem em seus lugares corretos no projeto.</span><span class="sxs-lookup"><span data-stu-id="0ab86-145">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="0ab86-146">Você pode testar instalações manualmente no Visual Studio ou na linha de comando usando as [etapas de instalação do pacote](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package) normais.</span><span class="sxs-lookup"><span data-stu-id="0ab86-146">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ab86-147">Os pacotes são imutáveis.</span><span class="sxs-lookup"><span data-stu-id="0ab86-147">Packages are immutable.</span></span> <span data-ttu-id="0ab86-148">Se corrigir um problema, altere o conteúdo do pacote e empacote novamente. Quando você testar novamente, ainda estará usando a versão antiga do pacote até que [limpe sua pasta de pacotes globais](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders).</span><span class="sxs-lookup"><span data-stu-id="0ab86-148">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="0ab86-149">Isso é especialmente relevante ao testar pacotes que não usam um rótulo de pré-lançamento exclusivo em cada compilação.</span><span class="sxs-lookup"><span data-stu-id="0ab86-149">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ab86-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0ab86-150">Next Steps</span></span>

<span data-ttu-id="0ab86-151">Depois de criar um pacote, que é um arquivo `.nupkg`, você pode publicá-lo na galeria de sua escolha conforme descrito em [Publicar um pacote](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="0ab86-151">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="0ab86-152">Você também poderá estender os recursos do seu pacote ou dar suporte a outros cenários conforme descrito nos tópicos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0ab86-152">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="0ab86-153">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="0ab86-153">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="0ab86-154">Suporte a várias estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="0ab86-154">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="0ab86-155">Adicionar um ícone de pacote</span><span class="sxs-lookup"><span data-stu-id="0ab86-155">Add a package icon</span></span>](../reference/nuspec.md#icon)
- [<span data-ttu-id="0ab86-156">Transformações dos arquivos de configuração e de origem</span><span class="sxs-lookup"><span data-stu-id="0ab86-156">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="0ab86-157">Localização</span><span class="sxs-lookup"><span data-stu-id="0ab86-157">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="0ab86-158">Versões de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="0ab86-158">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="0ab86-159">Definir tipo de pacote</span><span class="sxs-lookup"><span data-stu-id="0ab86-159">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="0ab86-160">Criar pacotes com assemblies de interoperabilidade COM</span><span class="sxs-lookup"><span data-stu-id="0ab86-160">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="0ab86-161">Por fim, há tipos de pacote adicionais a serem considerados:</span><span class="sxs-lookup"><span data-stu-id="0ab86-161">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="0ab86-162">Pacotes nativos</span><span class="sxs-lookup"><span data-stu-id="0ab86-162">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="0ab86-163">Pacotes de símbolos</span><span class="sxs-lookup"><span data-stu-id="0ab86-163">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
