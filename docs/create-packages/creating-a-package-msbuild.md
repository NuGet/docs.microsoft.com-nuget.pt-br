---
title: Criar um pacote NuGet usando MSBuild
description: Um guia detalhado para o processo de design e criação de um pacote do NuGet, incluindo os principais pontos de decisão como arquivos e controle de versão.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9512899a4086d17d2584f16833aba33efb321eae
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380699"
---
# <a name="create-a-nuget-package-using-msbuild"></a><span data-ttu-id="25c80-103">Criar um pacote NuGet usando MSBuild</span><span class="sxs-lookup"><span data-stu-id="25c80-103">Create a NuGet package using MSBuild</span></span>

<span data-ttu-id="25c80-104">Ao criar um pacote NuGet de seu criar, você empacota essa funcionalidade em um componente que pode ser compartilhado e usado por uma infinidade de outros desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="25c80-104">When you create a NuGet package from your code, you package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="25c80-105">Este artigo descreve como criar um pacote usando MSBuild.</span><span class="sxs-lookup"><span data-stu-id="25c80-105">This article describes how to create a package using MSBuild.</span></span> <span data-ttu-id="25c80-106">O MSBuild vem pré-instalado com todas as cargas de trabalho do Visual Studio que contêm o NuGet.</span><span class="sxs-lookup"><span data-stu-id="25c80-106">MSBuild comes preinstalled with every Visual Studio workload that contains NuGet.</span></span> <span data-ttu-id="25c80-107">Além disso, você também pode usar o MSBuild por meio da CLI do dotnet com [dotnet msbuild](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild)</span><span class="sxs-lookup"><span data-stu-id="25c80-107">Additionally you can also use MSBuild through the dotnet CLI with [dotnet msbuild](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild)</span></span>

<span data-ttu-id="25c80-108">Para projetos .NET Core e .NET Standard que usam projetos no [formato de estilo SDK](../resources/check-project-format.md) e quaisquer outros estilos SDK, o NuGet usa as informações do arquivo de projeto diretamente para criar um pacote.</span><span class="sxs-lookup"><span data-stu-id="25c80-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span>  <span data-ttu-id="25c80-109">Para projetos que não são de estilo SDK e que usam `<PackageReference>`, o NuGet também usa o arquivo de projeto para criar um pacote.</span><span class="sxs-lookup"><span data-stu-id="25c80-109">For a non-SDK-style project that uses `<PackageReference>`, NuGet also uses the project file to create a package.</span></span>

<span data-ttu-id="25c80-110">Projetos de estilo SDK têm a funcionalidade de empacotamento disponível por padrão.</span><span class="sxs-lookup"><span data-stu-id="25c80-110">SDK-style projects have the pack functionality available by default.</span></span> <span data-ttu-id="25c80-111">Para projetos de PackageReference que não são de estilo SDK, você precisa adicionar o pacote NuGet.Build.Tasks.Pack às dependências do projeto.</span><span class="sxs-lookup"><span data-stu-id="25c80-111">For non SDK-style PackageReference projects, you need to add the NuGet.Build.Tasks.Pack package to the project dependencies.</span></span> <span data-ttu-id="25c80-112">Para obter informações detalhadas sobre os destinos de empacotamento do MSBuild, confira [Empacotamento e restauração do NuGet como destinos do MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="25c80-112">For detailed information about MSBuild pack targets, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

<span data-ttu-id="25c80-113">O comando que cria um pacote, `msbuild -t:pack`, é a funcionalidade equivalente a `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="25c80-113">The command that creates a package, `msbuild -t:pack`, is functionality equivalent to `dotnet pack`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25c80-114">Este tópico se aplica a projetos com [estilo SDK](../resources/check-project-format.md), normalmente projetos do .NET Core e do .NET Standard, e a projetos que não são de estilo SDK que usam PackageReference.</span><span class="sxs-lookup"><span data-stu-id="25c80-114">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects, and to non-SDK-style projects that use PackageReference.</span></span>

## <a name="set-properties"></a><span data-ttu-id="25c80-115">Definir propriedades</span><span class="sxs-lookup"><span data-stu-id="25c80-115">Set properties</span></span>

<span data-ttu-id="25c80-116">As propriedades a seguir são necessárias para criar um pacote.</span><span class="sxs-lookup"><span data-stu-id="25c80-116">The following properties are required to create a package.</span></span>

- <span data-ttu-id="25c80-117">`PackageId`, o identificador de pacotes, que deve ser exclusivo na galeria que hospeda o pacote.</span><span class="sxs-lookup"><span data-stu-id="25c80-117">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="25c80-118">Se não for especificado, o valor padrão será `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="25c80-118">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="25c80-119">`Version`, um número de versão específico na forma *Principal.Secundário.Patch[-Sufixo]* em que *-Sufixo* identifica as [versões de pré-lançamento](prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="25c80-119">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="25c80-120">Se esse campo não for especificado, o valor padrão será 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="25c80-120">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="25c80-121">O título do pacote como ele deve aparecer no host (como nuget.org)</span><span class="sxs-lookup"><span data-stu-id="25c80-121">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="25c80-122">`Authors`, informações de autor e proprietário.</span><span class="sxs-lookup"><span data-stu-id="25c80-122">`Authors`, author and owner information.</span></span> <span data-ttu-id="25c80-123">Se não for especificado, o valor padrão será `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="25c80-123">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="25c80-124">`Company`, o nome da empresa.</span><span class="sxs-lookup"><span data-stu-id="25c80-124">`Company`, your company name.</span></span> <span data-ttu-id="25c80-125">Se não for especificado, o valor padrão será `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="25c80-125">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="25c80-126">No Visual Studio, é possível definir esses valores nas propriedades do projeto (clique com o botão direito do mouse no projeto no Gerenciador de Soluções, escolha **Propriedades** e selecione a guia **Pacote**).</span><span class="sxs-lookup"><span data-stu-id="25c80-126">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="25c80-127">Você também pode definir essas propriedades diretamente nos arquivos do projeto ( *.csproj*).</span><span class="sxs-lookup"><span data-stu-id="25c80-127">You can also set these properties directly in the project files (*.csproj*).</span></span>

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="25c80-128">Dê ao pacote um identificador exclusivo em nuget.org ou qualquer origem de pacote que estiver usando.</span><span class="sxs-lookup"><span data-stu-id="25c80-128">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="25c80-129">O exemplo a seguir mostra um arquivo de projeto simples e completo com essas propriedades incluídas.</span><span class="sxs-lookup"><span data-stu-id="25c80-129">The following example shows a simple, complete project file with these properties included.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="25c80-130">Defina também as propriedades opcionais, como `Title`, `PackageDescription` e `PackageTags`, conforme descrito em [Destinos do pacote MSBuild](../reference/msbuild-targets.md#pack-target), [Controlar ativos de dependência](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) e [Propriedades de metadados do NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="25c80-130">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="25c80-131">Para pacotes compilados para consumo público, preste atenção especial à propriedade **PackageTags**, à medida que as marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.</span><span class="sxs-lookup"><span data-stu-id="25c80-131">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="25c80-132">Para obter detalhes sobre como declarar dependências e especificar números de versão, consulte [Referências de pacote em arquivos de projeto](../consume-packages/package-references-in-project-files.md) e [Controle de versão do pacote](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="25c80-132">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="25c80-133">Também é possível extrair ativos de dependências diretamente no pacote usando os atributos `<IncludeAssets>` e `<ExcludeAssets>`.</span><span class="sxs-lookup"><span data-stu-id="25c80-133">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="25c80-134">Para saber mais, confira [Controlar ativos de dependência](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="25c80-134">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="25c80-135">Escolher um identificador de pacote exclusivo e definir o número de versão</span><span class="sxs-lookup"><span data-stu-id="25c80-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a><span data-ttu-id="25c80-136">Adicionar o pacote NuGet.Build.Tasks.Pack</span><span class="sxs-lookup"><span data-stu-id="25c80-136">Add the NuGet.Build.Tasks.Pack package</span></span>

<span data-ttu-id="25c80-137">Se você estiver usando o MSBuild com um projeto que não é de estilo SDK e com PackageReference, adicione o pacote NuGet.Build.Tasks.Pack ao projeto.</span><span class="sxs-lookup"><span data-stu-id="25c80-137">If you are using MSBuild with a non-SDK-style project and PackageReference, add the NuGet.Build.Tasks.Pack package to your project.</span></span>

1. <span data-ttu-id="25c80-138">Abra o arquivo de projeto e adicione o seguinte após o elemento `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="25c80-138">Open the project file and add the following after the `<PropertyGroup>` element:</span></span>

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="25c80-139">Abra um prompt de comando do Desenvolvedor (na caixa **Pesquisar**, digite **Prompt de Comando do Desenvolvedor**).</span><span class="sxs-lookup"><span data-stu-id="25c80-139">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="25c80-140">Você normalmente deseja iniciar o Prompt de Comando do Desenvolvedor para Visual Studio usando o menu **Iniciar**, pois ele estará configurado com todos os caminhos necessários para o MSBuild.</span><span class="sxs-lookup"><span data-stu-id="25c80-140">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

3. <span data-ttu-id="25c80-141">Alterne para a pasta que contém o arquivo de projeto e digite o seguinte comando para instalar o pacote NuGet.Build.Tasks.Pack.</span><span class="sxs-lookup"><span data-stu-id="25c80-141">Switch to the folder containing the project file and type the following command to install the NuGet.Build.Tasks.Pack package.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   <span data-ttu-id="25c80-142">Verifique se a saída de MSBuild indica que a compilação foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="25c80-142">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="run-the-msbuild--tpack-command"></a><span data-ttu-id="25c80-143">Execute o comando msbuild -t:pack</span><span class="sxs-lookup"><span data-stu-id="25c80-143">Run the msbuild -t:pack command</span></span>

<span data-ttu-id="25c80-144">Para compilar um pacote do NuGet (um arquivo `.nupkg`) do projeto, execute o comando `msbuild -t:pack`, que também compila o projeto automaticamente:</span><span class="sxs-lookup"><span data-stu-id="25c80-144">To build a NuGet package (a `.nupkg` file) from the project, run the `msbuild -t:pack` command, which also builds the project automatically:</span></span>

<span data-ttu-id="25c80-145">No prompt de comando do Desenvolvedor para Visual Studio, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="25c80-145">In the Developer command prompt for Visual Studio, type the following command:</span></span>

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

<span data-ttu-id="25c80-146">A saída mostra o caminho até o arquivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="25c80-146">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="25c80-147">Gerar pacote automaticamente no build</span><span class="sxs-lookup"><span data-stu-id="25c80-147">Automatically generate package on build</span></span>

<span data-ttu-id="25c80-148">Para executar `msbuild -t:pack` automaticamente ao compilar ou restaurar o projeto, adicione a seguinte linha ao arquivo de projeto em `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="25c80-148">To automatically run `msbuild -t:pack` when you build or restore the project, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="25c80-149">Ao executar `msbuild -t:pack` em uma solução, isso empacota todos os projetos na solução que são empacotáveis (a propriedade [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) é definida como `true`).</span><span class="sxs-lookup"><span data-stu-id="25c80-149">When you run `msbuild -t:pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="25c80-150">Ao gerar automaticamente o pacote, o tempo de empacotamento aumenta o tempo de compilação do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="25c80-150">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="25c80-151">Instalação do pacote de teste</span><span class="sxs-lookup"><span data-stu-id="25c80-151">Test package installation</span></span>

<span data-ttu-id="25c80-152">Antes de publicar um pacote, geralmente é recomendável testar o processo de instalação de um pacote em um projeto.</span><span class="sxs-lookup"><span data-stu-id="25c80-152">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="25c80-153">Os testes garantem que os arquivos todos terminem em seus lugares corretos no projeto.</span><span class="sxs-lookup"><span data-stu-id="25c80-153">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="25c80-154">Você pode testar instalações manualmente no Visual Studio ou na linha de comando usando as [etapas de instalação do pacote](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package) normais.</span><span class="sxs-lookup"><span data-stu-id="25c80-154">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25c80-155">Os pacotes são imutáveis.</span><span class="sxs-lookup"><span data-stu-id="25c80-155">Packages are immutable.</span></span> <span data-ttu-id="25c80-156">Se corrigir um problema, altere o conteúdo do pacote e empacote novamente. Quando você testar novamente, ainda estará usando a versão antiga do pacote até que [limpe sua pasta de pacotes globais](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders).</span><span class="sxs-lookup"><span data-stu-id="25c80-156">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="25c80-157">Isso é especialmente relevante ao testar pacotes que não usam um rótulo de pré-lançamento exclusivo em cada compilação.</span><span class="sxs-lookup"><span data-stu-id="25c80-157">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25c80-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="25c80-158">Next Steps</span></span>

<span data-ttu-id="25c80-159">Depois de criar um pacote, que é um arquivo `.nupkg`, você pode publicá-lo na galeria de sua escolha conforme descrito em [Publicar um pacote](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="25c80-159">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="25c80-160">Você também poderá estender os recursos do seu pacote ou dar suporte a outros cenários conforme descrito nos tópicos a seguir:</span><span class="sxs-lookup"><span data-stu-id="25c80-160">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="25c80-161">Empacotamento e restauração do NuGet como destinos do MSBuild</span><span class="sxs-lookup"><span data-stu-id="25c80-161">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
- [<span data-ttu-id="25c80-162">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="25c80-162">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="25c80-163">Suporte a várias estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="25c80-163">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="25c80-164">Transformações dos arquivos de configuração e de origem</span><span class="sxs-lookup"><span data-stu-id="25c80-164">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="25c80-165">Localização</span><span class="sxs-lookup"><span data-stu-id="25c80-165">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="25c80-166">Versões de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="25c80-166">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="25c80-167">Definir tipo de pacote</span><span class="sxs-lookup"><span data-stu-id="25c80-167">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="25c80-168">Criar pacotes com assemblies de interoperabilidade COM</span><span class="sxs-lookup"><span data-stu-id="25c80-168">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="25c80-169">Por fim, há tipos de pacote adicionais a serem considerados:</span><span class="sxs-lookup"><span data-stu-id="25c80-169">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="25c80-170">Pacotes nativos</span><span class="sxs-lookup"><span data-stu-id="25c80-170">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="25c80-171">Pacotes de Símbolo</span><span class="sxs-lookup"><span data-stu-id="25c80-171">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
