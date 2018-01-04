---
title: Criar pacotes do NuGet do .NET Standard com o Visual Studio 2015 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: "Uma explicação passo a passo de ponta a ponta da criação de pacotes do NuGet do .NET Standard usando o NuGet 3.x e o Visual Studio 2015."
keywords: criar um pacote, pacotes do .NET Standard, tabela de mapeamento do .NET Standard
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a912c27e1873d60426f2147995f69e2dcc433ca9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="0604e-104">Criar pacotes do .NET Standard com o Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="0604e-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="0604e-105">*Aplica-se ao NuGet 3.x. Consulte [Criar pacotes do .NET Standard com o Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) para trabalhar com o NuGet 4.x ou superior.*</span><span class="sxs-lookup"><span data-stu-id="0604e-105">*Applies to NuGet 3.x. See [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="0604e-106">A [Biblioteca do .NET Standard](https://docs.microsoft.com/dotnet/articles/standard/library) é uma especificação formal de APIs .NET que devem estar disponíveis em todos os tempos de execução do .NET, estabelecendo dessa forma uma maior uniformidade no ecossistema do .NET.</span><span class="sxs-lookup"><span data-stu-id="0604e-106">The [.NET Standard Library](https://docs.microsoft.com/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="0604e-107">A Biblioteca do .NET Standard define um conjunto uniforme de APIs de BCL (Biblioteca de Classes Base) para implementação em todas as plataformas do .NET, independentemente da carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0604e-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="0604e-108">Ele permite que os desenvolvedores produzam PCLs que podem ser usados em todos os tempos de execução do .NET e reduz ou elimina as diretivas de compilação condicional específicas da plataforma em código compartilhado.</span><span class="sxs-lookup"><span data-stu-id="0604e-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="0604e-109">Este guia orientará você durante a criação de um pacote do nuget direcionado para a Biblioteca do .NET Standard 1.4.</span><span class="sxs-lookup"><span data-stu-id="0604e-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="0604e-110">Isso funcionará em .NET Framework 4.6.1, Plataforma Universal do Windows 10, .NET Core e Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="0604e-110">This will work across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="0604e-111">Para obter detalhes, consulte a [tabela de mapeamento do .NET Standard](#net-standard-mapping-table) mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="0604e-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

1. [<span data-ttu-id="0604e-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0604e-112">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="0604e-113">Criar o projeto da biblioteca de classes</span><span class="sxs-lookup"><span data-stu-id="0604e-113">Create the class library project</span></span>](#create-the-class-library-project)
1. [<span data-ttu-id="0604e-114">Criar e atualizar o arquivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="0604e-114">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="0604e-115">Empacotar o componente</span><span class="sxs-lookup"><span data-stu-id="0604e-115">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="0604e-116">Opções adicionais</span><span class="sxs-lookup"><span data-stu-id="0604e-116">Additional options</span></span>](#additional-options)
1. [<span data-ttu-id="0604e-117">Tabela de mapeamento do .NET Standard</span><span class="sxs-lookup"><span data-stu-id="0604e-117">.NET Standard mapping table</span></span>](#net-standard-mapping-table)
1. [<span data-ttu-id="0604e-118">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="0604e-118">Related topics</span></span>](#related-topics)


## <a name="pre-requisites"></a><span data-ttu-id="0604e-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0604e-119">Pre-requisites</span></span>

1. <span data-ttu-id="0604e-120">Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="0604e-120">Visual Studio 2015.</span></span> <span data-ttu-id="0604e-121">Instale a edição Community gratuitamente no [visualstudio.com](https://www.visualstudio.com/) e, claro, você também pode usar as edições Professional e Enterprise.</span><span class="sxs-lookup"><span data-stu-id="0604e-121">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span>
1. <span data-ttu-id="0604e-122">.NET Core: instale o .NET Core junto com modelos e outras ferramentas para o Visual Studio 2015 de [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span><span class="sxs-lookup"><span data-stu-id="0604e-122">.NET Core: Install .NET Core along with templates and other tools for Visual Studio 2015 from [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span></span>
1. <span data-ttu-id="0604e-123">CLI do NuGet.</span><span class="sxs-lookup"><span data-stu-id="0604e-123">NuGet CLI.</span></span> <span data-ttu-id="0604e-124">Baixe a versão mais recente do nuget.exe de [nuget.org/downloads](https://nuget.org/downloads) e salve-a em um local de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="0604e-124">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="0604e-125">Em seguida, adicione tal local à sua variável de ambiente PATH, se ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="0604e-125">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="0604e-126">O nuget.exe é a própria ferramenta CLI e não um instalador, por isso não se esqueça de salvar o arquivo baixado do navegador em vez de executá-lo.</span><span class="sxs-lookup"><span data-stu-id="0604e-126">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>



## <a name="create-the-class-library-project"></a><span data-ttu-id="0604e-127">Criar o projeto da biblioteca de classes</span><span class="sxs-lookup"><span data-stu-id="0604e-127">Create the class library project</span></span>

1. <span data-ttu-id="0604e-128">No Visual Studio, **Arquivo > Novo > Projeto**, expanda o nó **Visual C# > Windows**, selecione **Biblioteca de Classes (Portátil)**, altere o nome para AppLogger e clique em OK.</span><span class="sxs-lookup"><span data-stu-id="0604e-128">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![Criar um novo projeto de biblioteca de classes](media/NetStandard-NewProject.png)

1. <span data-ttu-id="0604e-130">Na caixa de diálogo **Adicionar biblioteca de classes portátil** exibida, selecione as opções `.NET Framework 4.6` e `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="0604e-130">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>
1. <span data-ttu-id="0604e-131">Clique com o botão direito do mouse no `AppLogger (Portable)` no Gerenciador de Soluções, selecione **Propriedades**, escolha a guia **Biblioteca** e, em seguida, clique em **Destinado ao .NET Platform Standard** na seção **Direcionamento**.</span><span class="sxs-lookup"><span data-stu-id="0604e-131">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="0604e-132">Isso solicitará a confirmação, quando então é possível selecionar `.NET Standard 1.4` na lista suspensa:</span><span class="sxs-lookup"><span data-stu-id="0604e-132">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![Definir o destino como .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="0604e-134">Clique na guia **Build**, altere a **Configuração** para `Release` e marque a caixa para **Arquivo de documentação XML**.</span><span class="sxs-lookup"><span data-stu-id="0604e-134">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>
1. <span data-ttu-id="0604e-135">Adicione seu código ao componente, como por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0604e-135">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. <span data-ttu-id="0604e-136">Compile o projeto (com a configuração de Versão) e verifique se os arquivos DLL e XML são produzidos dentro da pasta bin\Release.</span><span class="sxs-lookup"><span data-stu-id="0604e-136">Build the project (with the Release configuration) and check that DLL and XML files are produced within the bin\Release folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="0604e-137">Criar e atualizar o arquivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="0604e-137">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="0604e-138">Abra um prompt de comando, navegue até a pasta que contém a pasta `AppLogg.csproj` (um nível abaixo de onde o arquivo `.sln` está) e execute o comando `spec` do NuGet para criar o arquivo `AppLogger.nuspec` inicial:</span><span class="sxs-lookup"><span data-stu-id="0604e-138">Open a command prompt, navigate to the folder containing `AppLogg.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

```
nuget spec
```

1. <span data-ttu-id="0604e-139">Abra o `AppLogger.nuspec` em um editor e atualize-o para corresponder ao seguinte, substituindo YOUR_NAME por um valor apropriado.</span><span class="sxs-lookup"><span data-stu-id="0604e-139">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="0604e-140">O valor `<id>`, especificamente, precisa ser exclusivo no nuget.org (consulte as convenções de nomenclatura descritas em [Criando um pacote](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="0604e-140">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="0604e-141">Observe que você também precisa atualizar as marcas de autor e descrição ou um erro será mostrado durante a etapa de empacotamento.</span><span class="sxs-lookup"><span data-stu-id="0604e-141">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>AppLogger.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>AppLogger</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. <span data-ttu-id="0604e-142">Adicionar assemblies de referência ao arquivo `.nuspec`, especificamente a DLL da biblioteca e o arquivo XML do IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="0604e-142">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="0604e-143">Clique com o botão direito do mouse na solução e selecione **Compilar solução** para gerar todos os arquivos de pacote.</span><span class="sxs-lookup"><span data-stu-id="0604e-143">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="0604e-144">Empacotar o componente</span><span class="sxs-lookup"><span data-stu-id="0604e-144">Package the component</span></span>

<span data-ttu-id="0604e-145">Depois do `.nuspec` terminar de referenciar todos os arquivos que você precisa incluir no pacote, você estará pronto para executar o comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="0604e-145">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack AppLogger.nuspec
```

<span data-ttu-id="0604e-146">Isso gerará `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="0604e-146">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="0604e-147">Ao abrir este arquivo em uma ferramenta como o [Explorador de Pacotes do NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) e expandir todos os nós, você verá o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="0604e-147">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![O Explorador de Pacotes do NuGet mostrando o pacote AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="0604e-149">O arquivo `.nupkg` é apenas um arquivo ZIP com uma extensão diferente.</span><span class="sxs-lookup"><span data-stu-id="0604e-149">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="0604e-150">Também é possível examinar o conteúdo do pacote alterando `.nupkg` para `.zip`, mas lembre-se de restaurar a extensão antes de carregar um pacote para o nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0604e-150">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="0604e-151">Para disponibilizar seu pacote para outros desenvolvedores, siga as instruções em [Publicar um pacote](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="0604e-151">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="0604e-152">Observe que `pack` requer o Mono 4.4.2 no Mac OS X e não funciona em sistemas Linux.</span><span class="sxs-lookup"><span data-stu-id="0604e-152">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="0604e-153">Em um Mac, você também precisa converter os nomes de caminho do Windows no arquivo `.nuspec` em caminhos no estilo Unix.</span><span class="sxs-lookup"><span data-stu-id="0604e-153">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="additional-options"></a><span data-ttu-id="0604e-154">Opções adicionais</span><span class="sxs-lookup"><span data-stu-id="0604e-154">Additional options</span></span>

<span data-ttu-id="0604e-155">As seções a seguir abordam opções adicionais para criação de pacotes do NuGet:</span><span class="sxs-lookup"><span data-stu-id="0604e-155">The following sections go into additional options for NuGet package creation:</span></span>

- [<span data-ttu-id="0604e-156">Declarando dependências</span><span class="sxs-lookup"><span data-stu-id="0604e-156">Declaring dependencies</span></span>](#declaring-dependencies)
- [<span data-ttu-id="0604e-157">Suporte a várias estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="0604e-157">Supporting multiple target frameworks</span></span>](#supporting-multiple-target-frameworks)
- [<span data-ttu-id="0604e-158">Adicionar destinos e objetos ao MSBuild</span><span class="sxs-lookup"><span data-stu-id="0604e-158">Adding targets and props for MSBuild</span></span>](#adding-targets-and-props-for-msbuild)
- [<span data-ttu-id="0604e-159">Criando pacotes localizados</span><span class="sxs-lookup"><span data-stu-id="0604e-159">Creating localized packages</span></span>](#creating-localized-packages)
- [<span data-ttu-id="0604e-160">Adicionar um Leiame</span><span class="sxs-lookup"><span data-stu-id="0604e-160">Adding a readme</span></span>](#adding-a-readme)

### <a name="declaring-dependencies"></a><span data-ttu-id="0604e-161">Declarando dependências</span><span class="sxs-lookup"><span data-stu-id="0604e-161">Declaring dependencies</span></span>

<span data-ttu-id="0604e-162">Se você tiver dependências em outros pacotes do NuGet, liste-os no elemento `<dependencies>` com elementos `<group>`.</span><span class="sxs-lookup"><span data-stu-id="0604e-162">If you have any dependencies on other NuGet packages, list those in the `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="0604e-163">Por exemplo, para declarar uma dependência no NewtonSoft.Json 8.0.3 ou superior, adicione o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0604e-163">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="0604e-164">A sintaxe do atributo *version* aqui indica que a versão 8.0.3 ou superior é aceitável.</span><span class="sxs-lookup"><span data-stu-id="0604e-164">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="0604e-165">Para especificar intervalos de versão diferentes, consulte [Controle de versão do pacote](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="0604e-165">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="supporting-multiple-target-frameworks"></a><span data-ttu-id="0604e-166">Suporte a várias estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="0604e-166">Supporting multiple target frameworks</span></span>

<span data-ttu-id="0604e-167">Suponha que você gostaria de aproveitar uma API no .NET Framework 4.6.2 não está disponível no .NET Standard 1.4.</span><span class="sxs-lookup"><span data-stu-id="0604e-167">Suppose you'd like to take advantage of an API in .NET Framework 4.6.2 that is not available in .NET Standard 1.4.</span></span> <span data-ttu-id="0604e-168">Para fazer isso, primeiro você precisará verificar se a biblioteca é compilada para o .NET 4.6.2 usando a compilação condicional ou projetos compartilhados.</span><span class="sxs-lookup"><span data-stu-id="0604e-168">To do this, you'll first need to make sure the library compiles for .NET 4.6.2 by using conditional compilation or shared projects.</span></span> <span data-ttu-id="0604e-169">(No Visual Studio, você pode criar um projeto NetCore, adicionar a estrutura de sua escolha à seção de várias estruturas e, em seguida, compilar.) Em seguida, crie o pacote usando a técnica simples de diretório de trabalho baseado em convenção da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0604e-169">(In Visual Studio, you can create a NetCore project, add the framework of choice to the multiple framework section, and then build.) Then you create the package using the simple convention-based working directory technique as follows:</span></span>

1. <span data-ttu-id="0604e-170">Na pasta raiz do projeto que contém seu arquivo `.nuspec`, crie uma pasta chamada `lib`.</span><span class="sxs-lookup"><span data-stu-id="0604e-170">In the project's root folder containing your `.nuspec` file, create a folder named `lib`.</span></span>
1. <span data-ttu-id="0604e-171">Dentro de `lib`, crie pastas para cada plataforma às quais você deseja dar suporte:</span><span class="sxs-lookup"><span data-stu-id="0604e-171">Inside `lib`, create folders for each platform you want to support:</span></span>

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. <span data-ttu-id="0604e-172">No arquivo `.nuspec`, adicione um nó `files` sob o nó `package` e consulte os arquivos em `lib` usando curingas.</span><span class="sxs-lookup"><span data-stu-id="0604e-172">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `lib` using wildcards.</span></span> <span data-ttu-id="0604e-173">**Observação:** substituições de Token não são compatíveis com a abordagem do diretório de trabalho baseado em convenção, portanto, substitua-as por valores literais:</span><span class="sxs-lookup"><span data-stu-id="0604e-173">**Note:** Token replacements are not supported with the convention-based working directory approach, so replace them with literal values:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="0604e-174">Crie o pacote novamente usando `nuget pack AppLogger.spec`.</span><span class="sxs-lookup"><span data-stu-id="0604e-174">Create the package again using `nuget pack AppLogger.spec`.</span></span>

<span data-ttu-id="0604e-175">Para obter mais detalhes sobre como usar essa técnica, consulte [Suporte a várias versões do .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)</span><span class="sxs-lookup"><span data-stu-id="0604e-175">For more details on using this technique, see [Supporting Multiple .NET Framework Versions](../create-packages/supporting-multiple-target-frameworks.md)</span></span>

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="0604e-176">Adicionar destinos e objetos ao MSBuild</span><span class="sxs-lookup"><span data-stu-id="0604e-176">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="0604e-177">Em alguns casos, convém adicionar destinos ou propriedades de build personalizados a projetos que consomem o pacote, como a execução de uma ferramenta personalizada ou um processo durante o build.</span><span class="sxs-lookup"><span data-stu-id="0604e-177">In some cases you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="0604e-178">Faça isso adicionando arquivos a uma pasta `\build` conforme descrito nas etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="0604e-178">You do this by adding files in a `\build` folder as described in the steps below.</span></span> <span data-ttu-id="0604e-179">Quando o NuGet instala um pacote com arquivos \build, ele adiciona um elemento de MSBuild ao arquivo de projeto que aponta para arquivos .targets e .props.</span><span class="sxs-lookup"><span data-stu-id="0604e-179">When NuGet installs a package with \build files, it adds an MSBuild element in the project file pointing to the .targets and .props files.</span></span>

> [!Note]
> <span data-ttu-id="0604e-180">Ao usar `project.json`, os destinos não são adicionados ao projeto, mas são disponibilizados por meio do `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="0604e-180">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>


1. <span data-ttu-id="0604e-181">Na pasta de projeto que contém seu arquivo `.nuspec`, crie uma pasta chamada `build`.</span><span class="sxs-lookup"><span data-stu-id="0604e-181">In the project folder containing the your `.nuspec` file, create a folder named `build`.</span></span>
1. <span data-ttu-id="0604e-182">Dentro do `build`, crie pastas para cada um que for compatível e coloque nelas seus arquivos `.targets` e `.props`:</span><span class="sxs-lookup"><span data-stu-id="0604e-182">Inside `build`, create folders for each supported, and within those place your `.targets` and `.props` files:</span></span>

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. <span data-ttu-id="0604e-183">No arquivo `.nuspec`, adicione um nó `files` sob o nó `package` e consulte os arquivos em `build` usando curingas.</span><span class="sxs-lookup"><span data-stu-id="0604e-183">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `build` using wildcards.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. <span data-ttu-id="0604e-184">Crie o pacote novamente usando `nuget pack AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="0604e-184">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>

<span data-ttu-id="0604e-185">Para ver detalhes adicionais, consulte [Incluir objetos e destinos do MSBuild em um pacote](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="0604e-185">For additional details, refer to [Include MSBuild props and targets in a package](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span></span>


### <a name="creating-localized-packages"></a><span data-ttu-id="0604e-186">Criando pacotes localizados</span><span class="sxs-lookup"><span data-stu-id="0604e-186">Creating localized packages</span></span>

<span data-ttu-id="0604e-187">Para criar versões localizadas da biblioteca, crie pacotes separados para localidades diferentes ou inclua assemblies de recursos localizados em um único pacote.</span><span class="sxs-lookup"><span data-stu-id="0604e-187">To create localized versions of your library, you can either create separate packages for different locales, or include localized resource assemblies within a single package.</span></span> <span data-ttu-id="0604e-188">Aqui está como realizar a segunda abordagem para alemão e italiano:</span><span class="sxs-lookup"><span data-stu-id="0604e-188">Here's how to do the latter approach for German and Italian:</span></span>

1. <span data-ttu-id="0604e-189">Dentro de cada pasta de estrutura de destino, em `lib`, crie pastas para cada idioma compatível além do inglês padrão.</span><span class="sxs-lookup"><span data-stu-id="0604e-189">Within each target framework folder under `lib`, create folders for each supported language other than the English default.</span></span> <span data-ttu-id="0604e-190">Nessas pastas, você pode colocar assemblies de recursos e arquivos XML do IntelliSense localizados.</span><span class="sxs-lookup"><span data-stu-id="0604e-190">In these folders you can place resource assemblies  and localized IntelliSense XML files.</span></span> <span data-ttu-id="0604e-191">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0604e-191">For example:</span></span>

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. <span data-ttu-id="0604e-192">No arquivo `.nuspec`, faça referência desses arquivos no nó `<files>`:</span><span class="sxs-lookup"><span data-stu-id="0604e-192">In the `.nuspec` file, reference these files in the `<files>` node:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="0604e-193">Crie o pacote novamente usando `nuget pack AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="0604e-193">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>


### <a name="adding-a-readme"></a><span data-ttu-id="0604e-194">Adicionar um Leiame</span><span class="sxs-lookup"><span data-stu-id="0604e-194">Adding a readme</span></span>

<span data-ttu-id="0604e-195">Quando você inclui um arquivo `readme.txt` na raiz do pacote, o Visual Studio será exibido quando o pacote for instalado diretamente.</span><span class="sxs-lookup"><span data-stu-id="0604e-195">When you include a `readme.txt` file in the root of the package, Visual Studio will display it when the package is installed directly.</span></span>

> [!Note]
> <span data-ttu-id="0604e-196">Os arquivos Leiame não são mostrados para pacotes que são instalados como uma dependência ou para projetos do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="0604e-196">Readme files are not shown for packages that are installed as a dependency, or for .NET Core projects.</span></span>


<span data-ttu-id="0604e-197">Para fazer isso, crie o arquivo `readme.txt`, coloque-o na pasta raiz do projeto e faça referência a ele no arquivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="0604e-197">To do this, create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```


## <a name="net-standard-mapping-table"></a><span data-ttu-id="0604e-198">Tabela de mapeamento do .NET Standard</span><span class="sxs-lookup"><span data-stu-id="0604e-198">.NET Standard mapping table</span></span>

|<span data-ttu-id="0604e-199">Nome da Plataforma</span><span class="sxs-lookup"><span data-stu-id="0604e-199">Platform Name</span></span> |<span data-ttu-id="0604e-200">Alias</span><span class="sxs-lookup"><span data-stu-id="0604e-200">Alias</span></span>|
|--------------|-----|
|<span data-ttu-id="0604e-201">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="0604e-201">.NET Standard</span></span> | <span data-ttu-id="0604e-202">netstandard</span><span class="sxs-lookup"><span data-stu-id="0604e-202">netstandard</span></span>| <span data-ttu-id="0604e-203">1.0</span><span class="sxs-lookup"><span data-stu-id="0604e-203">1.0</span></span>| <span data-ttu-id="0604e-204">1.1</span><span class="sxs-lookup"><span data-stu-id="0604e-204">1.1</span></span>| <span data-ttu-id="0604e-205">1.2</span><span class="sxs-lookup"><span data-stu-id="0604e-205">1.2</span></span>| <span data-ttu-id="0604e-206">1.3</span><span class="sxs-lookup"><span data-stu-id="0604e-206">1.3</span></span>| <span data-ttu-id="0604e-207">1.4</span><span class="sxs-lookup"><span data-stu-id="0604e-207">1.4</span></span>| <span data-ttu-id="0604e-208">1.5</span><span class="sxs-lookup"><span data-stu-id="0604e-208">1.5</span></span>| <span data-ttu-id="0604e-209">1.6</span><span class="sxs-lookup"><span data-stu-id="0604e-209">1.6</span></span>|
|<span data-ttu-id="0604e-210">.NET Core</span><span class="sxs-lookup"><span data-stu-id="0604e-210">.NET Core</span></span> | <span data-ttu-id="0604e-211">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="0604e-211">netcoreapp</span></span>| <span data-ttu-id="0604e-212">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-212">&#x2192;</span></span>| <span data-ttu-id="0604e-213">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-213">&#x2192;</span></span>| <span data-ttu-id="0604e-214">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-214">&#x2192;</span></span>| <span data-ttu-id="0604e-215">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-215">&#x2192;</span></span>| <span data-ttu-id="0604e-216">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-216">&#x2192;</span></span>| <span data-ttu-id="0604e-217">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-217">&#x2192;</span></span>| <span data-ttu-id="0604e-218">1.0</span><span class="sxs-lookup"><span data-stu-id="0604e-218">1.0</span></span>|
|<span data-ttu-id="0604e-219">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="0604e-219">.NET Framework</span></span>| <span data-ttu-id="0604e-220">net</span><span class="sxs-lookup"><span data-stu-id="0604e-220">net</span></span>| <span data-ttu-id="0604e-221">4.5</span><span class="sxs-lookup"><span data-stu-id="0604e-221">4.5</span></span>| <span data-ttu-id="0604e-222">4.5.1</span><span class="sxs-lookup"><span data-stu-id="0604e-222">4.5.1</span></span>| <span data-ttu-id="0604e-223">4.6</span><span class="sxs-lookup"><span data-stu-id="0604e-223">4.6</span></span>| <span data-ttu-id="0604e-224">4.6.1</span><span class="sxs-lookup"><span data-stu-id="0604e-224">4.6.1</span></span>| <span data-ttu-id="0604e-225">4.6.2</span><span class="sxs-lookup"><span data-stu-id="0604e-225">4.6.2</span></span>| <span data-ttu-id="0604e-226">4.6.3</span><span class="sxs-lookup"><span data-stu-id="0604e-226">4.6.3</span></span>|
|<span data-ttu-id="0604e-227">Plataformas Mono/Xamarin</span><span class="sxs-lookup"><span data-stu-id="0604e-227">Mono/Xamarin Platforms</span></span>| <span data-ttu-id="0604e-228">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-228">&#x2192;</span></span>| <span data-ttu-id="0604e-229">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-229">&#x2192;</span></span>| <span data-ttu-id="0604e-230">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-230">&#x2192;</span></span>| <span data-ttu-id="0604e-231">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-231">&#x2192;</span></span>| <span data-ttu-id="0604e-232">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-232">&#x2192;</span></span>| <span data-ttu-id="0604e-233">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-233">&#x2192;</span></span>|
|<span data-ttu-id="0604e-234">Plataforma Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="0604e-234">Universal Windows Platform</span></span>| <span data-ttu-id="0604e-235">uap</span><span class="sxs-lookup"><span data-stu-id="0604e-235">uap</span></span>| <span data-ttu-id="0604e-236">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-236">&#x2192;</span></span>| <span data-ttu-id="0604e-237">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-237">&#x2192;</span></span>| <span data-ttu-id="0604e-238">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-238">&#x2192;</span></span>| <span data-ttu-id="0604e-239">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-239">&#x2192;</span></span>|<span data-ttu-id="0604e-240">10.0</span><span class="sxs-lookup"><span data-stu-id="0604e-240">10.0</span></span>|
|<span data-ttu-id="0604e-241">Windows</span><span class="sxs-lookup"><span data-stu-id="0604e-241">Windows</span></span>| <span data-ttu-id="0604e-242">win</span><span class="sxs-lookup"><span data-stu-id="0604e-242">win</span></span>| <span data-ttu-id="0604e-243">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-243">&#x2192;</span></span>| <span data-ttu-id="0604e-244">8.0</span><span class="sxs-lookup"><span data-stu-id="0604e-244">8.0</span></span>| <span data-ttu-id="0604e-245">8.1</span><span class="sxs-lookup"><span data-stu-id="0604e-245">8.1</span></span>|
|<span data-ttu-id="0604e-246">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="0604e-246">Windows Phone</span></span>| <span data-ttu-id="0604e-247">wpa</span><span class="sxs-lookup"><span data-stu-id="0604e-247">wpa</span></span>| <span data-ttu-id="0604e-248">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-248">&#x2192;</span></span>| <span data-ttu-id="0604e-249">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="0604e-249">&#x2192;</span></span>|<span data-ttu-id="0604e-250">8.1</span><span class="sxs-lookup"><span data-stu-id="0604e-250">8.1</span></span>|
|<span data-ttu-id="0604e-251">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="0604e-251">Windows Phone Silverlight</span></span>| <span data-ttu-id="0604e-252">wp</span><span class="sxs-lookup"><span data-stu-id="0604e-252">wp</span></span>| <span data-ttu-id="0604e-253">8.0</span><span class="sxs-lookup"><span data-stu-id="0604e-253">8.0</span></span>|



## <a name="related-topics"></a><span data-ttu-id="0604e-254">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="0604e-254">Related topics</span></span>

- [<span data-ttu-id="0604e-255">Referência de Nuspec</span><span class="sxs-lookup"><span data-stu-id="0604e-255">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="0604e-256">Pacotes de símbolo</span><span class="sxs-lookup"><span data-stu-id="0604e-256">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="0604e-257">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="0604e-257">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="0604e-258">Suporte a Várias Versões do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="0604e-258">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="0604e-259">Incluir objetivos e destinos de MSBuild em um pacote</span><span class="sxs-lookup"><span data-stu-id="0604e-259">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="0604e-260">Criando Pacotes Localizados</span><span class="sxs-lookup"><span data-stu-id="0604e-260">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="0604e-261">Documentação da Biblioteca do .NET Standard</span><span class="sxs-lookup"><span data-stu-id="0604e-261">.NET Standard Library documentation</span></span>](https://docs.microsoft.com/dotnet/articles/standard/library)
- [<span data-ttu-id="0604e-262">Portabilidade para o .NET Core do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="0604e-262">Porting to .NET Core from .NET Framework</span></span>](https://docs.microsoft.com/dotnet/articles/core/porting/index)
