---
title: Criar pacotes do NuGet do .NET Standard com o Visual Studio 2015 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Uma explicação passo a passo de ponta a ponta da criação de pacotes do NuGet do .NET Standard usando o NuGet 3.x e o Visual Studio 2015."
keywords: criar um pacote, pacotes do .NET Standard, tabela de mapeamento do .NET Standard
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: abf6a56cbc84bdd066e31e77c7883825a8456144
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="205b5-104">Criar pacotes do .NET Standard com o Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="205b5-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="205b5-105">*Aplica-se ao NuGet 3.x. Veja [Criar e publicar um pacote com o Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) para trabalhar com o NuGet 4.x+.*</span><span class="sxs-lookup"><span data-stu-id="205b5-105">*Applies to NuGet 3.x. See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="205b5-106">A [Biblioteca do .NET Standard](/dotnet/articles/standard/library) é uma especificação formal de APIs .NET que devem estar disponíveis em todos os tempos de execução do .NET, estabelecendo dessa forma uma maior uniformidade no ecossistema do .NET.</span><span class="sxs-lookup"><span data-stu-id="205b5-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="205b5-107">A Biblioteca do .NET Standard define um conjunto uniforme de APIs de BCL (Biblioteca de Classes Base) para implementação em todas as plataformas do .NET, independentemente da carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="205b5-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="205b5-108">Ele permite que os desenvolvedores produzam código que podem ser usados em todos os tempos de execução do .NET e reduz ou elimina as diretivas de compilação condicional específicas da plataforma em código compartilhado.</span><span class="sxs-lookup"><span data-stu-id="205b5-108">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="205b5-109">Este guia orientará você durante a criação de um pacote NuGet direcionado para a Biblioteca do .NET Standard 1.4.</span><span class="sxs-lookup"><span data-stu-id="205b5-109">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="205b5-110">Essa biblioteca funcionará no .NET Framework 4.6.1, na Plataforma Universal do Windows 10, no .NET Core e no Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="205b5-110">Such a library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="205b5-111">Para obter detalhes, consulte a [tabela de mapeamento do .NET Standard](#net-standard-mapping-table) mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="205b5-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="205b5-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="205b5-112">Prerequisites</span></span>

1. <span data-ttu-id="205b5-113">Visual Studio 2015 Atualização 3</span><span class="sxs-lookup"><span data-stu-id="205b5-113">Visual Studio 2015 Update 3</span></span>
1. [<span data-ttu-id="205b5-114">SDK do .NET Core</span><span class="sxs-lookup"><span data-stu-id="205b5-114">.NET Core SDK</span></span>](https://www.microsoft.com/net/download/)
1. <span data-ttu-id="205b5-115">CLI do NuGet.</span><span class="sxs-lookup"><span data-stu-id="205b5-115">NuGet CLI.</span></span> <span data-ttu-id="205b5-116">Baixe a versão mais recente do nuget.exe de [nuget.org/downloads](https://nuget.org/downloads) e salve-a em um local de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="205b5-116">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="205b5-117">Em seguida, adicione tal local à sua variável de ambiente PATH, se ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="205b5-117">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="205b5-118">O nuget.exe é a própria ferramenta CLI e não um instalador, por isso não se esqueça de salvar o arquivo baixado do navegador em vez de executá-lo.</span><span class="sxs-lookup"><span data-stu-id="205b5-118">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="205b5-119">Criar o projeto da biblioteca de classes</span><span class="sxs-lookup"><span data-stu-id="205b5-119">Create the class library project</span></span>

1. <span data-ttu-id="205b5-120">No Visual Studio, **Arquivo > Novo > Projeto**, expanda o nó **Visual C# > Windows**, selecione **Biblioteca de Classes (Portátil)**, altere o nome para AppLogger e clique em OK.</span><span class="sxs-lookup"><span data-stu-id="205b5-120">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![Criar um novo projeto de biblioteca de classes](media/NetStandard-NewProject.png)

1. <span data-ttu-id="205b5-122">Na caixa de diálogo **Adicionar biblioteca de classes portátil** exibida, selecione as opções `.NET Framework 4.6` e `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="205b5-122">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>

1. <span data-ttu-id="205b5-123">Clique com o botão direito do mouse no `AppLogger (Portable)` no Gerenciador de Soluções, selecione **Propriedades**, escolha a guia **Biblioteca** e, em seguida, clique em **Destinado ao .NET Platform Standard** na seção **Direcionamento**.</span><span class="sxs-lookup"><span data-stu-id="205b5-123">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="205b5-124">Isso solicitará a confirmação, quando então é possível selecionar `.NET Standard 1.4` na lista suspensa:</span><span class="sxs-lookup"><span data-stu-id="205b5-124">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![Definir o destino como .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="205b5-126">Clique na guia **Build**, altere a **Configuração** para `Release` e marque a caixa para **Arquivo de documentação XML**.</span><span class="sxs-lookup"><span data-stu-id="205b5-126">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="205b5-127">Adicione seu código ao componente, como por exemplo:</span><span class="sxs-lookup"><span data-stu-id="205b5-127">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. <span data-ttu-id="205b5-128">Defina a configuração para Versão, compile o projeto e verifique se os arquivos DLL e XML são produzidos na pasta `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="205b5-128">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="205b5-129">Criar e atualizar o arquivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="205b5-129">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="205b5-130">Abra um prompt de comando, navegue até a pasta que contém a pasta `AppLogger.csproj` (um nível abaixo de onde o arquivo `.sln` está) e execute o comando `spec` do NuGet para criar o arquivo `AppLogger.nuspec` inicial:</span><span class="sxs-lookup"><span data-stu-id="205b5-130">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="205b5-131">Abra o `AppLogger.nuspec` em um editor e atualize-o para corresponder ao seguinte, substituindo YOUR_NAME por um valor apropriado.</span><span class="sxs-lookup"><span data-stu-id="205b5-131">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="205b5-132">O valor `<id>`, especificamente, precisa ser exclusivo no nuget.org (consulte as convenções de nomenclatura descritas em [Criando um pacote](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="205b5-132">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="205b5-133">Observe que você também precisa atualizar as marcas de autor e descrição ou um erro é mostrado durante a etapa de empacotamento.</span><span class="sxs-lookup"><span data-stu-id="205b5-133">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="205b5-134">Adicionar assemblies de referência ao arquivo `.nuspec`, especificamente a DLL da biblioteca e o arquivo XML do IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="205b5-134">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="205b5-135">Clique com o botão direito do mouse na solução e selecione **Compilar solução** para gerar todos os arquivos de pacote.</span><span class="sxs-lookup"><span data-stu-id="205b5-135">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="205b5-136">Declarando dependências</span><span class="sxs-lookup"><span data-stu-id="205b5-136">Declaring dependencies</span></span>

<span data-ttu-id="205b5-137">Se você tiver dependências em outros pacotes NuGet, liste-as no elemento `<dependencies>` do manifesto com os elementos `<group>`.</span><span class="sxs-lookup"><span data-stu-id="205b5-137">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="205b5-138">Por exemplo, para declarar uma dependência no NewtonSoft.Json 8.0.3 ou superior, adicione o seguinte:</span><span class="sxs-lookup"><span data-stu-id="205b5-138">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="205b5-139">A sintaxe do atributo *version* aqui indica que a versão 8.0.3 ou superior é aceitável.</span><span class="sxs-lookup"><span data-stu-id="205b5-139">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="205b5-140">Para especificar intervalos de versão diferentes, consulte [Controle de versão do pacote](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="205b5-140">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="205b5-141">Adicionar um Leiame</span><span class="sxs-lookup"><span data-stu-id="205b5-141">Adding a readme</span></span>

<span data-ttu-id="205b5-142">Crie o arquivo `readme.txt`, coloque-o na pasta raiz do projeto e faça referência a ele no arquivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="205b5-142">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="205b5-143">O Visual Studio exibe `readme.txt` quando o pacote está instalado em um projeto.</span><span class="sxs-lookup"><span data-stu-id="205b5-143">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="205b5-144">O arquivo não é mostrado quando instalado em projetos do .NET Core ou para pacotes instalados como uma dependência.</span><span class="sxs-lookup"><span data-stu-id="205b5-144">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="205b5-145">Empacotar o componente</span><span class="sxs-lookup"><span data-stu-id="205b5-145">Package the component</span></span>

<span data-ttu-id="205b5-146">Depois do `.nuspec` terminar de referenciar todos os arquivos que você precisa incluir no pacote, você estará pronto para executar o comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="205b5-146">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="205b5-147">Isso gerará `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="205b5-147">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="205b5-148">Ao abrir este arquivo em uma ferramenta como o [Explorador de Pacotes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) e expandir todos os nós, você verá o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="205b5-148">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![O Explorador de Pacotes do NuGet mostrando o pacote AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="205b5-150">O arquivo `.nupkg` é apenas um arquivo ZIP com uma extensão diferente.</span><span class="sxs-lookup"><span data-stu-id="205b5-150">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="205b5-151">Também é possível examinar o conteúdo do pacote alterando `.nupkg` para `.zip`, mas lembre-se de restaurar a extensão antes de carregar um pacote para o nuget.org.</span><span class="sxs-lookup"><span data-stu-id="205b5-151">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="205b5-152">Para disponibilizar o pacote para outros desenvolvedores, siga as instruções em [Publicar um pacote](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="205b5-152">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="205b5-153">Observe que `pack` requer o Mono 4.4.2 no Mac OS X e não funciona em sistemas Linux.</span><span class="sxs-lookup"><span data-stu-id="205b5-153">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="205b5-154">Em um Mac, você também precisa converter os nomes de caminho do Windows no arquivo `.nuspec` em caminhos no estilo Unix.</span><span class="sxs-lookup"><span data-stu-id="205b5-154">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="net-standard-mapping-table"></a><span data-ttu-id="205b5-155">Tabela de mapeamento do .NET Standard</span><span class="sxs-lookup"><span data-stu-id="205b5-155">.NET Standard mapping table</span></span>

| <span data-ttu-id="205b5-156">Nome da plataforma</span><span class="sxs-lookup"><span data-stu-id="205b5-156">Platform Name</span></span> | <span data-ttu-id="205b5-157">Alias</span><span class="sxs-lookup"><span data-stu-id="205b5-157">Alias</span></span> |
| --- | --- |
| <span data-ttu-id="205b5-158">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="205b5-158">.NET Standard</span></span> | <span data-ttu-id="205b5-159">netstandard</span><span class="sxs-lookup"><span data-stu-id="205b5-159">netstandard</span></span> | <span data-ttu-id="205b5-160">1.0</span><span class="sxs-lookup"><span data-stu-id="205b5-160">1.0</span></span> | <span data-ttu-id="205b5-161">1.1</span><span class="sxs-lookup"><span data-stu-id="205b5-161">1.1</span></span> | <span data-ttu-id="205b5-162">1.2</span><span class="sxs-lookup"><span data-stu-id="205b5-162">1.2</span></span> | <span data-ttu-id="205b5-163">1.3</span><span class="sxs-lookup"><span data-stu-id="205b5-163">1.3</span></span> | <span data-ttu-id="205b5-164">1.4</span><span class="sxs-lookup"><span data-stu-id="205b5-164">1.4</span></span> | <span data-ttu-id="205b5-165">1.5</span><span class="sxs-lookup"><span data-stu-id="205b5-165">1.5</span></span> | <span data-ttu-id="205b5-166">1.6</span><span class="sxs-lookup"><span data-stu-id="205b5-166">1.6</span></span> |
| <span data-ttu-id="205b5-167">.NET Core</span><span class="sxs-lookup"><span data-stu-id="205b5-167">.NET Core</span></span> | <span data-ttu-id="205b5-168">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="205b5-168">netcoreapp</span></span> | <span data-ttu-id="205b5-169">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-169">&#x2192;</span></span> | <span data-ttu-id="205b5-170">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-170">&#x2192;</span></span> | <span data-ttu-id="205b5-171">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-171">&#x2192;</span></span> | <span data-ttu-id="205b5-172">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-172">&#x2192;</span></span> | <span data-ttu-id="205b5-173">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-173">&#x2192;</span></span> | <span data-ttu-id="205b5-174">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-174">&#x2192;</span></span> | <span data-ttu-id="205b5-175">1.0</span><span class="sxs-lookup"><span data-stu-id="205b5-175">1.0</span></span> |
| <span data-ttu-id="205b5-176">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="205b5-176">.NET Framework</span></span> | <span data-ttu-id="205b5-177">net</span><span class="sxs-lookup"><span data-stu-id="205b5-177">net</span></span> | <span data-ttu-id="205b5-178">4.5</span><span class="sxs-lookup"><span data-stu-id="205b5-178">4.5</span></span> | <span data-ttu-id="205b5-179">4.5.1</span><span class="sxs-lookup"><span data-stu-id="205b5-179">4.5.1</span></span> | <span data-ttu-id="205b5-180">4.6</span><span class="sxs-lookup"><span data-stu-id="205b5-180">4.6</span></span> | <span data-ttu-id="205b5-181">4.6.1</span><span class="sxs-lookup"><span data-stu-id="205b5-181">4.6.1</span></span> | <span data-ttu-id="205b5-182">4.6.2</span><span class="sxs-lookup"><span data-stu-id="205b5-182">4.6.2</span></span> | <span data-ttu-id="205b5-183">4.6.3</span><span class="sxs-lookup"><span data-stu-id="205b5-183">4.6.3</span></span> |
| <span data-ttu-id="205b5-184">Plataformas Mono/Xamarin</span><span class="sxs-lookup"><span data-stu-id="205b5-184">Mono/Xamarin Platforms</span></span> | <span data-ttu-id="205b5-185">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-185">&#x2192;</span></span> | <span data-ttu-id="205b5-186">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-186">&#x2192;</span></span> | <span data-ttu-id="205b5-187">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-187">&#x2192;</span></span> | <span data-ttu-id="205b5-188">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-188">&#x2192;</span></span> | <span data-ttu-id="205b5-189">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-189">&#x2192;</span></span> | <span data-ttu-id="205b5-190">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-190">&#x2192;</span></span> |
| <span data-ttu-id="205b5-191">Plataforma Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="205b5-191">Universal Windows Platform</span></span> | <span data-ttu-id="205b5-192">uap</span><span class="sxs-lookup"><span data-stu-id="205b5-192">uap</span></span> | <span data-ttu-id="205b5-193">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-193">&#x2192;</span></span> | <span data-ttu-id="205b5-194">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-194">&#x2192;</span></span> | <span data-ttu-id="205b5-195">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-195">&#x2192;</span></span> | <span data-ttu-id="205b5-196">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-196">&#x2192;</span></span> |<span data-ttu-id="205b5-197">10.0</span><span class="sxs-lookup"><span data-stu-id="205b5-197">10.0</span></span> |
| <span data-ttu-id="205b5-198">Windows</span><span class="sxs-lookup"><span data-stu-id="205b5-198">Windows</span></span> | <span data-ttu-id="205b5-199">win</span><span class="sxs-lookup"><span data-stu-id="205b5-199">win</span></span>| <span data-ttu-id="205b5-200">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-200">&#x2192;</span></span> | <span data-ttu-id="205b5-201">8.0</span><span class="sxs-lookup"><span data-stu-id="205b5-201">8.0</span></span> | <span data-ttu-id="205b5-202">8.1</span><span class="sxs-lookup"><span data-stu-id="205b5-202">8.1</span></span> |
| <span data-ttu-id="205b5-203">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="205b5-203">Windows Phone</span></span> | <span data-ttu-id="205b5-204">wpa</span><span class="sxs-lookup"><span data-stu-id="205b5-204">wpa</span></span>| <span data-ttu-id="205b5-205">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-205">&#x2192;</span></span>| <span data-ttu-id="205b5-206">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="205b5-206">&#x2192;</span></span> | <span data-ttu-id="205b5-207">8.1</span><span class="sxs-lookup"><span data-stu-id="205b5-207">8.1</span></span> |
| <span data-ttu-id="205b5-208">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="205b5-208">Windows Phone Silverlight</span></span> | <span data-ttu-id="205b5-209">wp</span><span class="sxs-lookup"><span data-stu-id="205b5-209">wp</span></span> | <span data-ttu-id="205b5-210">8.0</span><span class="sxs-lookup"><span data-stu-id="205b5-210">8.0</span></span> |

## <a name="related-topics"></a><span data-ttu-id="205b5-211">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="205b5-211">Related topics</span></span>

- [<span data-ttu-id="205b5-212">Referência do .nuspec</span><span class="sxs-lookup"><span data-stu-id="205b5-212">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="205b5-213">Compatibilidade com várias versões do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="205b5-213">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="205b5-214">Incluir objetivos e destinos de MSBuild em um pacote</span><span class="sxs-lookup"><span data-stu-id="205b5-214">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="205b5-215">Criando pacotes localizados</span><span class="sxs-lookup"><span data-stu-id="205b5-215">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="205b5-216">Pacotes de símbolo</span><span class="sxs-lookup"><span data-stu-id="205b5-216">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="205b5-217">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="205b5-217">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="205b5-218">Documentação da Biblioteca do .NET Standard</span><span class="sxs-lookup"><span data-stu-id="205b5-218">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="205b5-219">Portabilidade para o .NET Core do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="205b5-219">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
