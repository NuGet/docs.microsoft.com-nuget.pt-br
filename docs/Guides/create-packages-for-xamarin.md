---
title: Criar pacotes NuGet para Xamarin (para iOS, Android e Windows) com Visual Studio 2015 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: Uma explicação passo a passo de ponta a ponta da criação de pacotes do NuGet para Xamarin que usam APIs nativas no iOS, Android e Windows.
keywords: criar um pacote, pacotes para Xamarin, pacotes de multiplataforma
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e101ca2d124a19d2cf758776717b3680aa5bbdd8
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="create-packages-for-xamarin-with-visual-studio-2015"></a><span data-ttu-id="0e08e-104">Criar pacotes para Xamarin com o Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="0e08e-104">Create packages for Xamarin with Visual Studio 2015</span></span>

<span data-ttu-id="0e08e-105">Um pacote para Xamarin contém código que usa APIs nativas no iOS, Android e Windows, dependendo do sistema operacional de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="0e08e-105">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="0e08e-106">Embora seja simples fazer isso, é preferível para permitir que os desenvolvedores consumam o pacote de um PCL ou de bibliotecas do .NET Standard por meio de uma área de superfície de API comum.</span><span class="sxs-lookup"><span data-stu-id="0e08e-106">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="0e08e-107">Neste passo a passo, use Visual Studio 2015 para criar um pacote do NuGet de plataforma cruzada que pode ser usado em projetos móveis no iOS, Android e Windows.</span><span class="sxs-lookup"><span data-stu-id="0e08e-107">In this walkthrough you use Visual Studio 2015 create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="0e08e-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0e08e-108">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="0e08e-109">Criar a estrutura do projeto e o código de abstração</span><span class="sxs-lookup"><span data-stu-id="0e08e-109">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="0e08e-110">Escreva o código específico para sua plataforma</span><span class="sxs-lookup"><span data-stu-id="0e08e-110">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="0e08e-111">Criar e atualizar o arquivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="0e08e-111">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="0e08e-112">Empacotar o componente</span><span class="sxs-lookup"><span data-stu-id="0e08e-112">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="0e08e-113">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="0e08e-113">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="0e08e-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0e08e-114">Prerequisites</span></span>

1. <span data-ttu-id="0e08e-115">Visual Studio 2015 com UWP (Plataforma Universal do Windows) e Xamarin.</span><span class="sxs-lookup"><span data-stu-id="0e08e-115">Visual Studio 2015 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="0e08e-116">Instale a edição Community gratuitamente no [visualstudio.com](https://www.visualstudio.com/) e, claro, você também pode usar as edições Professional e Enterprise.</span><span class="sxs-lookup"><span data-stu-id="0e08e-116">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="0e08e-117">Para incluir as ferramentas UWP e Xamarin, selecione uma instalação Personalizada e verifique as opções apropriadas.</span><span class="sxs-lookup"><span data-stu-id="0e08e-117">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="0e08e-118">CLI do NuGet.</span><span class="sxs-lookup"><span data-stu-id="0e08e-118">NuGet CLI.</span></span> <span data-ttu-id="0e08e-119">Baixe a versão mais recente do nuget.exe de [nuget.org/downloads](https://nuget.org/downloads) e salve-a em uma localização de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="0e08e-119">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="0e08e-120">Em seguida, adicione tal localização à sua variável de ambiente PATH, se ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="0e08e-120">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="0e08e-121">O nuget.exe é a própria ferramenta CLI e não um instalador, por isso não se esqueça de salvar o arquivo baixado do navegador em vez de executá-lo.</span><span class="sxs-lookup"><span data-stu-id="0e08e-121">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="0e08e-122">Criar a estrutura do projeto e o código de abstração</span><span class="sxs-lookup"><span data-stu-id="0e08e-122">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="0e08e-123">Baixe e execute o [Plug-in de extensão de modelos do Xamarin](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0e08e-123">Download and run the [Plugin for Xamarin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="0e08e-124">Esses modelos facilitarão a criação da estrutura de projeto necessária para este passo a passo.</span><span class="sxs-lookup"><span data-stu-id="0e08e-124">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="0e08e-125">No Visual Studio, **Arquivo > Novo > Projeto**, pesquise `Plugin`, selecione o modelo **Plug-in para Xamarin**, altere o nome para LoggingLibrary e clique em OK.</span><span class="sxs-lookup"><span data-stu-id="0e08e-125">In Visual Studio, **File > New > Project**, search for `Plugin`, select the **Plugin for Xamarin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Novo projeto de Aplicativo em branco (Xamarin.Forms portátil) no Visual Studio](media/CrossPlatform-NewProject.png)

<span data-ttu-id="0e08e-127">A solução resultante contém dois projetos PCL, juntamente com uma variedade de projetos específicos da plataforma:</span><span class="sxs-lookup"><span data-stu-id="0e08e-127">The resulting solution contains two PCL projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="0e08e-128">O PCL denominado `Plugin.LoggingLibrary.Abstractions (Portable)` define a interface pública (a área de superfície de API) do componente, nesse caso a interface `ILoggingLibrary` contida no arquivo ILoggingLibrary.cs.</span><span class="sxs-lookup"><span data-stu-id="0e08e-128">The PCL named `Plugin.LoggingLibrary.Abstractions (Portable)`, defines the public interface (the API surface area) of the component, in this case the `ILoggingLibrary` interface contained in the ILoggingLibrary.cs file.</span></span> <span data-ttu-id="0e08e-129">É aqui que você define a interface para a biblioteca.</span><span class="sxs-lookup"><span data-stu-id="0e08e-129">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="0e08e-130">O outro PCL, `Plugin.LoggingLibrary (Portable)`, contém o código em CrossLoggingLibrary.cs que localizará uma implementação específica de plataforma da interface abstrata no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="0e08e-130">The other PCL, `Plugin.LoggingLibrary (Portable)`, contains code in CrossLoggingLibrary.cs that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="0e08e-131">Normalmente não é necessário modificar esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="0e08e-131">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="0e08e-132">Os projetos específicos de plataforma, como `Plugin.LoggingLibrary.Android`, contêm uma implementação nativa da interface em seus respectivos arquivos LoggingLibraryImplementation.cs.</span><span class="sxs-lookup"><span data-stu-id="0e08e-132">The platform-specific projects, such as `Plugin.LoggingLibrary.Android`, each contain contain a native implementation of the interface in their respective LoggingLibraryImplementation.cs files.</span></span> <span data-ttu-id="0e08e-133">É aqui que você compila o código da biblioteca.</span><span class="sxs-lookup"><span data-stu-id="0e08e-133">This is where you build out your library's code.</span></span>

<span data-ttu-id="0e08e-134">Por padrão, o arquivo ILoggingLibrary.cs do projeto Abstractions contém uma definição de interface, mas nenhum método.</span><span class="sxs-lookup"><span data-stu-id="0e08e-134">By default, the ILoggingLibrary.cs file of the Abstractions project contains an interface definition, but no methods.</span></span> <span data-ttu-id="0e08e-135">Para os fins deste passo a passo, adicione um método `Log` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0e08e-135">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="0e08e-136">Escreva o código específico para sua plataforma</span><span class="sxs-lookup"><span data-stu-id="0e08e-136">Write your platform-specific code</span></span>

<span data-ttu-id="0e08e-137">Para implementar uma implementação específica da plataforma `ILoggingLibrary` e seus métodos, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0e08e-137">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="0e08e-138">Abra o arquivo `LoggingLibraryImplementation.cs` de cada plataforma do projeto e adicione o código necessário.</span><span class="sxs-lookup"><span data-stu-id="0e08e-138">Open the `LoggingLibraryImplementation.cs` file of each platform project and add the necessary code.</span></span> <span data-ttu-id="0e08e-139">Por exemplo (usando o projeto `Plugin.LoggingLibrary.Android`):</span><span class="sxs-lookup"><span data-stu-id="0e08e-139">For example (using the `Plugin.LoggingLibrary.Android` project):</span></span>

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. <span data-ttu-id="0e08e-140">Repita essa implementação nos projetos para cada plataforma às quais você deseja dar suporte.</span><span class="sxs-lookup"><span data-stu-id="0e08e-140">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="0e08e-141">Clique com botão direito do mouse no projeto do iOS, selecione **Propriedades**, clique na guia **Build** e remova “\iPhone” das configurações **Caminho de saída** e **Arquivo de documentação XML**.</span><span class="sxs-lookup"><span data-stu-id="0e08e-141">Right-click the iOS project, select **Properties**, click the **Build** tab, and remove "\iPhone" from the **Output path** and **XML documentation file** settings.</span></span> <span data-ttu-id="0e08e-142">Isso serve apenas para conveniência posterior neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="0e08e-142">This is just for later convenience in this walkthrough.</span></span> <span data-ttu-id="0e08e-143">Salve o arquivo quando terminar.</span><span class="sxs-lookup"><span data-stu-id="0e08e-143">Save the file when done.</span></span>
1. <span data-ttu-id="0e08e-144">Clique com o botão direito do mouse na solução, selecione **Configuration Manager...**e marque as caixas **Build** para as PCLs e cada plataforma que você deseja dar suporte.</span><span class="sxs-lookup"><span data-stu-id="0e08e-144">Right-click the solution, select **Configuration Manager...**, and check the **Build** boxes for the PCLs and each platform you're supporting.</span></span>
1. <span data-ttu-id="0e08e-145">Clique com o botão direito do mouse e selecione **Compilar solução** para verificar seu trabalho e produzir os artefatos que são empacotados em seguida.</span><span class="sxs-lookup"><span data-stu-id="0e08e-145">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="0e08e-146">Se você receber erros sobre referências ausentes, clique com o botão direito do mouse na solução, selecione **Restaurar pacotes do NuGet** para instalar as dependências e recompile.</span><span class="sxs-lookup"><span data-stu-id="0e08e-146">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="0e08e-147">Para compilar para iOS, é necessário ter um Mac em rede conectado ao Visual Studio, conforme descrito em [Introdução ao Xamarin.iOS para Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span><span class="sxs-lookup"><span data-stu-id="0e08e-147">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="0e08e-148">Se você não tiver um Mac disponível, apague o projeto iOS no Gerenciador de Configuração (etapa 3 acima).</span><span class="sxs-lookup"><span data-stu-id="0e08e-148">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="0e08e-149">Criar e atualizar o arquivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="0e08e-149">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="0e08e-150">Abra um prompt de comando, navegue até a pasta `LoggingLibrary` que está um nível abaixo do qual o arquivo `.sln` está e execute o comando `spec` do NuGet para criar o arquivo `Package.nuspec` inicial:</span><span class="sxs-lookup"><span data-stu-id="0e08e-150">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="0e08e-151">Renomeie este arquivo para `LoggingLibrary.nuspec` e abra-o em um editor.</span><span class="sxs-lookup"><span data-stu-id="0e08e-151">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="0e08e-152">Atualize o arquivo para corresponder ao seguinte, substituindo YOUR_NAME por um valor apropriado.</span><span class="sxs-lookup"><span data-stu-id="0e08e-152">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="0e08e-153">O valor `<id>`, especificamente, precisa ser exclusivo no nuget.org (consulte as convenções de nomenclatura descritas em [Criando um pacote](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="0e08e-153">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="0e08e-154">Observe que você também precisa atualizar as marcas de autor e descrição ou um erro é mostrado durante a etapa de empacotamento.</span><span class="sxs-lookup"><span data-stu-id="0e08e-154">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="0e08e-155">Você pode acrescentar o sufixo à sua versão de pacote com `-alpha`, `-beta` ou `-rc` para marcar o pacote como versão de pré-lançamento, consulte [Versões de pré-lançamento](../create-packages/prerelease-packages.md) para obter mais informações sobre as versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="0e08e-155">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="0e08e-156">Adicionar assemblies de referência</span><span class="sxs-lookup"><span data-stu-id="0e08e-156">Add reference assemblies</span></span>

<span data-ttu-id="0e08e-157">Para incluir os assemblies de referência específicos de plataforma, adicione o seguinte ao elemento `<files>` de `LoggingLibrary.nuspec` conforme apropriado para as plataformas compatíveis:</span><span class="sxs-lookup"><span data-stu-id="0e08e-157">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> <span data-ttu-id="0e08e-158">Para encurtar os nomes dos arquivos DLL e XML, clique com o botão direito do mouse em qualquer projeto, selecione a guia **Biblioteca** e altere os nomes de assembly.</span><span class="sxs-lookup"><span data-stu-id="0e08e-158">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="0e08e-159">Adicionar dependências</span><span class="sxs-lookup"><span data-stu-id="0e08e-159">Add dependencies</span></span>

<span data-ttu-id="0e08e-160">Se você tiver dependências específicas para implementações nativas, use o elemento `<dependencies>` com elementos `<group>` especificá-los, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0e08e-160">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

<span data-ttu-id="0e08e-161">Por exemplo, o seguinte definiria iTextSharp como uma dependência para o destino UAP:</span><span class="sxs-lookup"><span data-stu-id="0e08e-161">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="0e08e-162">.nuspec final</span><span class="sxs-lookup"><span data-stu-id="0e08e-162">Final .nuspec</span></span>

<span data-ttu-id="0e08e-163">O arquivo `.nuspec` final agora deve ser semelhante ao seguinte, em que novamente YOUR_NAME deve ser substituído por um valor apropriado:</span><span class="sxs-lookup"><span data-stu-id="0e08e-163">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="0e08e-164">Empacotar o componente</span><span class="sxs-lookup"><span data-stu-id="0e08e-164">Package the component</span></span>

<span data-ttu-id="0e08e-165">Depois do `.nuspec` terminar de referenciar todos os arquivos que você precisa incluir no pacote, você estará pronto para executar o comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="0e08e-165">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="0e08e-166">Isso gerará `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="0e08e-166">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="0e08e-167">Ao abrir este arquivo em uma ferramenta como o [Explorador de Pacotes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) e expandir todos os nós, você verá o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="0e08e-167">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![O Explorador de Pacotes do NuGet mostrando o pacote LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="0e08e-169">O arquivo `.nupkg` é apenas um arquivo ZIP com uma extensão diferente.</span><span class="sxs-lookup"><span data-stu-id="0e08e-169">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="0e08e-170">Também é possível examinar o conteúdo do pacote alterando `.nupkg` para `.zip`, mas lembre-se de restaurar a extensão antes de carregar um pacote para o nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0e08e-170">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="0e08e-171">Para disponibilizar seu pacote para outros desenvolvedores, siga as instruções em [Publicar um pacote](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="0e08e-171">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="0e08e-172">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="0e08e-172">Related topics</span></span>

- [<span data-ttu-id="0e08e-173">Referência de Nuspec</span><span class="sxs-lookup"><span data-stu-id="0e08e-173">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="0e08e-174">Pacotes de símbolo</span><span class="sxs-lookup"><span data-stu-id="0e08e-174">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="0e08e-175">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="0e08e-175">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="0e08e-176">Suporte a Várias Versões do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="0e08e-176">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="0e08e-177">Incluir objetos e destinos de MSBuild em um pacote</span><span class="sxs-lookup"><span data-stu-id="0e08e-177">Including MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="0e08e-178">Criando Pacotes Localizados</span><span class="sxs-lookup"><span data-stu-id="0e08e-178">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)