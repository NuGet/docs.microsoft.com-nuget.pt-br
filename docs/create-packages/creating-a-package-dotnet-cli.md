---
title: Criar um pacote do NuGet usando a CLI dotnet
description: Um guia detalhado para o processo de design e criação de um pacote do NuGet, incluindo os principais pontos de decisão como arquivos e controle de versão.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 535d5a16a559cde065ee0277471edfbaf1aea084
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825277"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="17dd6-103">Criar um pacote do NuGet usando a CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="17dd6-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="17dd6-104">Independentemente do pacote ou do código que ele contém, use uma das ferramentas de CLI, seja `nuget.exe` ou `dotnet.exe`, para empacotar essa funcionalidade em um componente que possa ser compartilhado e usado por diversos desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="17dd6-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="17dd6-105">Este artigo descreve como criar um pacote usando a CLI dotnet.</span><span class="sxs-lookup"><span data-stu-id="17dd6-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="17dd6-106">Para instalar a CLI `dotnet`, confira [Instalar as ferramentas de cliente do NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="17dd6-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="17dd6-107">A partir do Visual Studio 2017, a CLI dotnet está inclusa nas cargas de trabalho do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="17dd6-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="17dd6-108">Para projetos .NET Core e .NET Standard que usam projetos no [formato de estilo SDK](../resources/check-project-format.md) e quaisquer outros estilos SDK, o NuGet usa as informações do arquivo de projeto diretamente para criar um pacote.</span><span class="sxs-lookup"><span data-stu-id="17dd6-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="17dd6-109">Para ver tutoriais passo a passo, confira [Criar pacotes .NET Standard com a CLI dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) e [Criar pacotes .NET Standard com o Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="17dd6-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) or [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="17dd6-110">`msbuild -t:pack` é uma funcionalidade equivalente a `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="17dd6-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="17dd6-111">Para compilar com MSBuild, consulte [Criar um pacote NuGet usando MSBuild](creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="17dd6-111">To build with MSBuild, see [Create a NuGet package using MSBuild](creating-a-package-msbuild.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17dd6-112">Este tópico aplica-se a projetos no [estilo SDK](../resources/check-project-format.md), normalmente projetos .NET Core e .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="17dd6-112">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="17dd6-113">Definir propriedades</span><span class="sxs-lookup"><span data-stu-id="17dd6-113">Set properties</span></span>

<span data-ttu-id="17dd6-114">As propriedades a seguir são necessárias para criar um pacote.</span><span class="sxs-lookup"><span data-stu-id="17dd6-114">The following properties are required to create a package.</span></span>

- <span data-ttu-id="17dd6-115">`PackageId`, o identificador de pacotes, que deve ser exclusivo na galeria que hospeda o pacote.</span><span class="sxs-lookup"><span data-stu-id="17dd6-115">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="17dd6-116">Se esse campo não for especificado, o valor padrão será `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="17dd6-116">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="17dd6-117">`Version`, um número de versão específico na forma *Principal.Secundário.Patch[-Sufixo]* em que *-Sufixo* identifica as [versões de pré-lançamento](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="17dd6-117">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="17dd6-118">Se esse campo não for especificado, o valor padrão será 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="17dd6-118">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="17dd6-119">O título do pacote como ele deve aparecer no host (como nuget.org)</span><span class="sxs-lookup"><span data-stu-id="17dd6-119">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="17dd6-120">`Authors`, informações de autor e proprietário.</span><span class="sxs-lookup"><span data-stu-id="17dd6-120">`Authors`, author and owner information.</span></span> <span data-ttu-id="17dd6-121">Se esse campo não for especificado, o valor padrão será `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="17dd6-121">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="17dd6-122">`Company`, o nome da empresa.</span><span class="sxs-lookup"><span data-stu-id="17dd6-122">`Company`, your company name.</span></span> <span data-ttu-id="17dd6-123">Se esse campo não for especificado, o valor padrão será `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="17dd6-123">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="17dd6-124">No Visual Studio, é possível definir esses valores nas propriedades do projeto (clique com o botão direito do mouse no projeto no Gerenciador de Soluções, escolha **Propriedades** e selecione a guia **Pacote**).</span><span class="sxs-lookup"><span data-stu-id="17dd6-124">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="17dd6-125">Você também pode definir essas propriedades diretamente nos arquivos do projeto (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="17dd6-125">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="17dd6-126">Dê ao pacote um identificador exclusivo em nuget.org ou qualquer origem de pacote que estiver usando.</span><span class="sxs-lookup"><span data-stu-id="17dd6-126">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="17dd6-127">O exemplo a seguir mostra um arquivo de projeto simples e completo com essas propriedades incluídas.</span><span class="sxs-lookup"><span data-stu-id="17dd6-127">The following example shows a simple, complete project file with these properties included.</span></span> <span data-ttu-id="17dd6-128">(Você pode criar um novo projeto padrão usando o comando `dotnet new classlib`.)</span><span class="sxs-lookup"><span data-stu-id="17dd6-128">(You can create a new default project using the `dotnet new classlib` command.)</span></span>

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

<span data-ttu-id="17dd6-129">Defina também as propriedades opcionais, como `Title`, `PackageDescription` e `PackageTags`, conforme descrito em [Destinos do pacote MSBuild](../reference/msbuild-targets.md#pack-target), [Controlar ativos de dependência](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) e [Propriedades de metadados do NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="17dd6-129">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="17dd6-130">Para pacotes compilados para consumo público, preste atenção especial à propriedade **PackageTags**, à medida que as marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.</span><span class="sxs-lookup"><span data-stu-id="17dd6-130">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="17dd6-131">Para obter detalhes sobre como declarar dependências e especificar números de versão, consulte [Referências de pacote em arquivos de projeto](../consume-packages/package-references-in-project-files.md) e [Controle de versão do pacote](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="17dd6-131">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="17dd6-132">Também é possível extrair ativos de dependências diretamente no pacote usando os atributos `<IncludeAssets>` e `<ExcludeAssets>`.</span><span class="sxs-lookup"><span data-stu-id="17dd6-132">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="17dd6-133">Para saber mais, confira [Controlar ativos de dependência](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="17dd6-133">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="17dd6-134">Escolher um identificador de pacote exclusivo e definir o número de versão</span><span class="sxs-lookup"><span data-stu-id="17dd6-134">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a><span data-ttu-id="17dd6-135">Executar o comando pack</span><span class="sxs-lookup"><span data-stu-id="17dd6-135">Run the pack command</span></span>

<span data-ttu-id="17dd6-136">Para compilar um pacote do NuGet (um arquivo `.nupkg`) do projeto, execute o comando `dotnet pack`, que também compila o projeto automaticamente:</span><span class="sxs-lookup"><span data-stu-id="17dd6-136">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="17dd6-137">A saída mostra o caminho até o arquivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="17dd6-137">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="17dd6-138">Gerar pacote automaticamente no build</span><span class="sxs-lookup"><span data-stu-id="17dd6-138">Automatically generate package on build</span></span>

<span data-ttu-id="17dd6-139">Para executar `dotnet pack` automaticamente ao executar `dotnet build`, adicione a seguinte linha ao arquivo de projeto em `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="17dd6-139">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="17dd6-140">Ao executar `dotnet pack` em uma solução, isso empacota todos os projetos na solução que são empacotáveis (a propriedade [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) é definida como `true`).</span><span class="sxs-lookup"><span data-stu-id="17dd6-140">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="17dd6-141">Ao gerar automaticamente o pacote, o tempo de empacotamento aumenta o tempo de compilação do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="17dd6-141">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="17dd6-142">Instalação do pacote de teste</span><span class="sxs-lookup"><span data-stu-id="17dd6-142">Test package installation</span></span>

<span data-ttu-id="17dd6-143">Antes de publicar um pacote, geralmente é recomendável testar o processo de instalação de um pacote em um projeto.</span><span class="sxs-lookup"><span data-stu-id="17dd6-143">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="17dd6-144">Os testes garantem que os arquivos todos terminem em seus lugares corretos no projeto.</span><span class="sxs-lookup"><span data-stu-id="17dd6-144">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="17dd6-145">Você pode testar instalações manualmente no Visual Studio ou na linha de comando usando as [etapas de instalação do pacote](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package) normais.</span><span class="sxs-lookup"><span data-stu-id="17dd6-145">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17dd6-146">Os pacotes são imutáveis.</span><span class="sxs-lookup"><span data-stu-id="17dd6-146">Packages are immutable.</span></span> <span data-ttu-id="17dd6-147">Se corrigir um problema, altere o conteúdo do pacote e empacote novamente. Quando você testar novamente, ainda estará usando a versão antiga do pacote até que [limpe sua pasta de pacotes globais](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders).</span><span class="sxs-lookup"><span data-stu-id="17dd6-147">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="17dd6-148">Isso é especialmente relevante ao testar pacotes que não usam um rótulo de pré-lançamento exclusivo em cada compilação.</span><span class="sxs-lookup"><span data-stu-id="17dd6-148">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17dd6-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="17dd6-149">Next Steps</span></span>

<span data-ttu-id="17dd6-150">Depois de criar um pacote, que é um arquivo `.nupkg`, você pode publicá-lo na galeria de sua escolha conforme descrito em [Publicar um pacote](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="17dd6-150">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="17dd6-151">Você também poderá estender os recursos do seu pacote ou dar suporte a outros cenários conforme descrito nos tópicos a seguir:</span><span class="sxs-lookup"><span data-stu-id="17dd6-151">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="17dd6-152">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="17dd6-152">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="17dd6-153">Suporte a várias estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="17dd6-153">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="17dd6-154">Transformações dos arquivos de configuração e de origem</span><span class="sxs-lookup"><span data-stu-id="17dd6-154">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="17dd6-155">Localização</span><span class="sxs-lookup"><span data-stu-id="17dd6-155">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="17dd6-156">Versões de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="17dd6-156">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="17dd6-157">Definir tipo de pacote</span><span class="sxs-lookup"><span data-stu-id="17dd6-157">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="17dd6-158">Criar pacotes com assemblies de interoperabilidade COM</span><span class="sxs-lookup"><span data-stu-id="17dd6-158">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="17dd6-159">Por fim, há tipos de pacote adicionais a serem considerados:</span><span class="sxs-lookup"><span data-stu-id="17dd6-159">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="17dd6-160">Pacotes nativos</span><span class="sxs-lookup"><span data-stu-id="17dd6-160">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="17dd6-161">Pacotes de Símbolo</span><span class="sxs-lookup"><span data-stu-id="17dd6-161">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
