---
title: Criar pacotes do NuGet do .NET Standard e do .NET Framework com o Visual Studio 2015
description: Uma explicação passo a passo completa da criação de pacotes do NuGet do .NET Standard e .NET Framework usando o NuGet 3.x e o Visual Studio 2015.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: 1198a781543e581f55740cc0ae5a212d3f8a8b61
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842453"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="9fb5f-103">Criar pacotes do .NET Standard e .NET Framework com o Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="9fb5f-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="9fb5f-104">**Observação:** É recomendável usar o Visual Studio 2017 para o desenvolvimento de bibliotecas .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="9fb5f-105">O Visual Studio 2015 pode funcionar, mas as ferramentas do .NET Core ficam somente no estado de versão prévia.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="9fb5f-106">Confira [Criar e publicar um pacote com o Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) para trabalhar com o NuGet 4.x ou posterior e Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="9fb5f-107">A [Biblioteca do .NET Standard](/dotnet/articles/standard/library) é uma especificação formal de APIs .NET que devem estar disponíveis em todos os tempos de execução do .NET, estabelecendo dessa forma uma maior uniformidade no ecossistema do .NET.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="9fb5f-108">A Biblioteca do .NET Standard define um conjunto uniforme de APIs de BCL (Biblioteca de Classes Base) para implementação em todas as plataformas do .NET, independentemente da carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="9fb5f-109">Ele permite que os desenvolvedores produzam código que podem ser usados em todos os tempos de execução do .NET e reduz ou elimina as diretivas de compilação condicional específicas da plataforma em código compartilhado.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="9fb5f-110">Este guia orienta você durante a criação de um pacote do NuGet direcionado para a Biblioteca do .NET Standard 1.4 ou um pacote direcionado para .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="9fb5f-111">Uma biblioteca do .NET Standard 1.4 funciona no .NET Framework 4.6.1, na Plataforma Universal do Windows 10, no .NET Core e no Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="9fb5f-112">Para obter detalhes, consulte a [tabela de mapeamento do .NET Standard](/dotnet/standard/net-standard#net-implementation-support) (documentação do .NET).</span><span class="sxs-lookup"><span data-stu-id="9fb5f-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="9fb5f-113">Se desejar, você poderá escolher outra versão da Biblioteca do .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fb5f-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9fb5f-114">Prerequisites</span></span>

1. <span data-ttu-id="9fb5f-115">Visual Studio 2015 Atualização 3</span><span class="sxs-lookup"><span data-stu-id="9fb5f-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="9fb5f-116">(Apenas .NET Standard) [SDK do .NET Core](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="9fb5f-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="9fb5f-117">CLI do NuGet.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-117">NuGet CLI.</span></span> <span data-ttu-id="9fb5f-118">Baixe a versão mais recente do nuget.exe de [nuget.org/downloads](https://nuget.org/downloads) e salve-a em um local de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="9fb5f-119">Em seguida, adicione tal local à sua variável de ambiente PATH, se ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="9fb5f-120">O nuget.exe é a própria ferramenta CLI e não um instalador, por isso não se esqueça de salvar o arquivo baixado do navegador em vez de executá-lo.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="9fb5f-121">Criar o projeto da biblioteca de classes</span><span class="sxs-lookup"><span data-stu-id="9fb5f-121">Create the class library project</span></span>

1. <span data-ttu-id="9fb5f-122">No Visual Studio, **Arquivo > Novo > Projeto**, expanda o nó **Visual C# > Windows**, selecione **Biblioteca de Classes (Portátil)** , altere o nome para AppLogger e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Criar um novo projeto de biblioteca de classes](media/NetStandard-NewProject.png)

1. <span data-ttu-id="9fb5f-124">Na caixa de diálogo **Adicionar biblioteca de classes portátil** exibida, selecione as opções para `.NET Framework 4.6` e `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="9fb5f-125">(Se estiver direcionando para .NET Framework, você poderá selecionar qualquer opção apropriada).</span><span class="sxs-lookup"><span data-stu-id="9fb5f-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="9fb5f-126">Se estiver direcionando para .NET Standard, clique com o botão direito do mouse em `AppLogger (Portable)` no Gerenciador de Soluções, selecione **Propriedades**, escolha a guia **Biblioteca** e, em seguida, selecione **Direcionar a .NET Platform Standard** na seção **Direcionamento**.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="9fb5f-127">Essa ação solicita confirmação e, em seguida, é possível selecionar `.NET Standard 1.4` (ou outra versão disponível) na lista suspensa:</span><span class="sxs-lookup"><span data-stu-id="9fb5f-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Definir o destino como .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="9fb5f-129">Clique na guia **Build**, altere a **Configuração** para `Release` e marque a caixa para **Arquivo de documentação XML**.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="9fb5f-130">Adicione seu código ao componente, como por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9fb5f-130">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="9fb5f-131">Defina a configuração para Versão, compile o projeto e verifique se os arquivos DLL e XML são produzidos na pasta `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="9fb5f-132">Criar e atualizar o arquivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="9fb5f-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="9fb5f-133">Abra um prompt de comando, navegue até a pasta que contém a pasta `AppLogger.csproj` (um nível abaixo de onde o arquivo `.sln` está) e execute o comando `spec` do NuGet para criar o arquivo `AppLogger.nuspec` inicial:</span><span class="sxs-lookup"><span data-stu-id="9fb5f-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="9fb5f-134">Abra o `AppLogger.nuspec` em um editor e atualize-o para corresponder ao seguinte, substituindo YOUR_NAME por um valor apropriado.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="9fb5f-135">O valor `<id>`, especificamente, precisa ser exclusivo no nuget.org (consulte as convenções de nomenclatura descritas em [Criando um pacote](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="9fb5f-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="9fb5f-136">Observe que você também precisa atualizar as marcas de autor e descrição ou um erro é mostrado durante a etapa de empacotamento.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="9fb5f-137">Adicionar assemblies de referência ao arquivo `.nuspec`, especificamente a DLL da biblioteca e o arquivo XML do IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="9fb5f-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="9fb5f-138">Se estiver direcionando para .NET Standard, as entradas exibidas serão semelhantes a estas:</span><span class="sxs-lookup"><span data-stu-id="9fb5f-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="9fb5f-139">Se estiver direcionando para .NET Framework, as entradas exibidas serão semelhantes a estas:</span><span class="sxs-lookup"><span data-stu-id="9fb5f-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="9fb5f-140">Clique com o botão direito do mouse na solução e selecione **Compilar solução** para gerar todos os arquivos de pacote.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="9fb5f-141">Declarando dependências</span><span class="sxs-lookup"><span data-stu-id="9fb5f-141">Declaring dependencies</span></span>

<span data-ttu-id="9fb5f-142">Se você tiver dependências em outros pacotes NuGet, liste-as no elemento `<dependencies>` do manifesto com os elementos `<group>`.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="9fb5f-143">Por exemplo, para declarar uma dependência no NewtonSoft.Json 8.0.3 ou superior, adicione o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9fb5f-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="9fb5f-144">A sintaxe do atributo *version* aqui indica que a versão 8.0.3 ou superior é aceitável.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="9fb5f-145">Para especificar intervalos de versão diferentes, consulte [Controle de versão do pacote](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9fb5f-145">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="9fb5f-146">Adicionar um Leiame</span><span class="sxs-lookup"><span data-stu-id="9fb5f-146">Adding a readme</span></span>

<span data-ttu-id="9fb5f-147">Crie o arquivo `readme.txt`, coloque-o na pasta raiz do projeto e faça referência a ele no arquivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="9fb5f-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="9fb5f-148">O Visual Studio exibe `readme.txt` quando o pacote está instalado em um projeto.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="9fb5f-149">O arquivo não é mostrado quando instalado em projetos do .NET Core ou para pacotes instalados como uma dependência.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="9fb5f-150">Empacotar o componente</span><span class="sxs-lookup"><span data-stu-id="9fb5f-150">Package the component</span></span>

<span data-ttu-id="9fb5f-151">Depois do `.nuspec` terminar de referenciar todos os arquivos que você precisa incluir no pacote, você estará pronto para executar o comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="9fb5f-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="9fb5f-152">Isso gera `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="9fb5f-153">Ao abrir este arquivo em uma ferramenta como o [Explorador de Pacotes do NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) e expandir todos os nós, você verá o seguinte conteúdo (mostrado para .NET Standard):</span><span class="sxs-lookup"><span data-stu-id="9fb5f-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![O Explorador de Pacotes do NuGet mostrando o pacote AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="9fb5f-155">O arquivo `.nupkg` é apenas um arquivo ZIP com uma extensão diferente.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="9fb5f-156">Também é possível examinar o conteúdo do pacote alterando `.nupkg` para `.zip`, mas lembre-se de restaurar a extensão antes de carregar um pacote para o nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="9fb5f-157">Para disponibilizar o pacote para outros desenvolvedores, siga as instruções em [Publicar um pacote](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="9fb5f-157">To make your package available to other developers, follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="9fb5f-158">Observe que `pack` requer o Mono 4.4.2 no Mac OS X e não funciona em sistemas Linux.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="9fb5f-159">Em um Mac, você também precisa converter os nomes de caminho do Windows no arquivo `.nuspec` em caminhos no estilo Unix.</span><span class="sxs-lookup"><span data-stu-id="9fb5f-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="9fb5f-160">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="9fb5f-160">Related topics</span></span>

- [<span data-ttu-id="9fb5f-161">Referência do .nuspec</span><span class="sxs-lookup"><span data-stu-id="9fb5f-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="9fb5f-162">Compatibilidade com várias versões do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="9fb5f-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="9fb5f-163">Incluir objetivos e destinos de MSBuild em um pacote</span><span class="sxs-lookup"><span data-stu-id="9fb5f-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="9fb5f-164">Criando pacotes localizados</span><span class="sxs-lookup"><span data-stu-id="9fb5f-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="9fb5f-165">Pacotes de símbolo</span><span class="sxs-lookup"><span data-stu-id="9fb5f-165">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="9fb5f-166">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="9fb5f-166">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="9fb5f-167">Documentação da Biblioteca do .NET Standard</span><span class="sxs-lookup"><span data-stu-id="9fb5f-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="9fb5f-168">Portabilidade para o .NET Core do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="9fb5f-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
