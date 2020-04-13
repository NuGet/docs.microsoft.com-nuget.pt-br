---
title: Crie pacotes NuGet para Xamarin (para iOS, Android e Windows) com visual studio 2017 ou 2019
description: Uma explicação passo a passo de ponta a ponta da criação de pacotes do NuGet para Xamarin que usam APIs nativas no iOS, Android e Windows.
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: 0cb653bad9e853d908039b3f7a94e1dd7eefdde5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230896"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a><span data-ttu-id="f6382-103">Crie pacotes para Xamarin com visual studio 2017 ou 2019</span><span class="sxs-lookup"><span data-stu-id="f6382-103">Create packages for Xamarin with Visual Studio 2017 or 2019</span></span>

<span data-ttu-id="f6382-104">Um pacote para Xamarin contém código que usa APIs nativas no iOS, Android e Windows, dependendo do sistema operacional de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="f6382-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="f6382-105">Embora seja simples fazer isso, é preferível para permitir que os desenvolvedores consumam o pacote de um PCL ou de bibliotecas do .NET Standard por meio de uma área de superfície de API comum.</span><span class="sxs-lookup"><span data-stu-id="f6382-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="f6382-106">Neste passo a passo você usa o Visual Studio 2017 ou 2019 para criar um pacote NuGet multiplataforma que pode ser usado em projetos móveis no iOS, Android e Windows.</span><span class="sxs-lookup"><span data-stu-id="f6382-106">In this walkthrough you use Visual Studio 2017 or 2019 to create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="f6382-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f6382-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="f6382-108">Criar a estrutura do projeto e o código de abstração</span><span class="sxs-lookup"><span data-stu-id="f6382-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="f6382-109">Escreva o código específico para sua plataforma</span><span class="sxs-lookup"><span data-stu-id="f6382-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="f6382-110">Criar e atualizar o arquivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="f6382-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="f6382-111">Empacotar o componente</span><span class="sxs-lookup"><span data-stu-id="f6382-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="f6382-112">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="f6382-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="f6382-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f6382-113">Prerequisites</span></span>

1. <span data-ttu-id="f6382-114">Visual Studio 2017 ou 2019 com Universal Windows Platform (UWP) e Xamarin.</span><span class="sxs-lookup"><span data-stu-id="f6382-114">Visual Studio 2017 or 2019 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="f6382-115">Instale a edição Community gratuitamente no [visualstudio.com](https://www.visualstudio.com/) e, claro, você também pode usar as edições Professional e Enterprise.</span><span class="sxs-lookup"><span data-stu-id="f6382-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="f6382-116">Para incluir as ferramentas UWP e Xamarin, selecione uma instalação Personalizada e verifique as opções apropriadas.</span><span class="sxs-lookup"><span data-stu-id="f6382-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="f6382-117">CLI do NuGet.</span><span class="sxs-lookup"><span data-stu-id="f6382-117">NuGet CLI.</span></span> <span data-ttu-id="f6382-118">Baixe a versão mais recente do nuget.exe de [nuget.org/downloads](https://nuget.org/downloads) e salve-a em um local de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="f6382-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="f6382-119">Em seguida, adicione tal local à sua variável de ambiente PATH, se ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="f6382-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="f6382-120">O nuget.exe é a própria ferramenta CLI e não um instalador, por isso não se esqueça de salvar o arquivo baixado do navegador em vez de executá-lo.</span><span class="sxs-lookup"><span data-stu-id="f6382-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="f6382-121">Criar a estrutura do projeto e o código de abstração</span><span class="sxs-lookup"><span data-stu-id="f6382-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="f6382-122">Baixe e execute a [extensão Cross-Platform .NET Standard Plugin Templates](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f6382-122">Download and run the [Cross-Platform .NET Standard Plugin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="f6382-123">Esses modelos facilitarão a criação da estrutura de projeto necessária para este passo a passo.</span><span class="sxs-lookup"><span data-stu-id="f6382-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="f6382-124">No Visual Studio 2017, File > `Plugin`New > **Project**, procure, selecione o modelo de **plugin de biblioteca padrão .NET,** altere o nome para LoggingLibrary e clique em OK.</span><span class="sxs-lookup"><span data-stu-id="f6382-124">In Visual Studio 2017, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Novo projeto de aplicativo em branco (Xamarin.Forms Portable) em VS 2017](media/CrossPlatform-NewProject.png)

    <span data-ttu-id="f6382-126">No Visual Studio 2019, File > `Plugin`New > **Project**, procure, selecione o modelo de **plugin de biblioteca padrão .NET e** clique em Next.</span><span class="sxs-lookup"><span data-stu-id="f6382-126">In Visual Studio 2019, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, and click Next.</span></span>

    ![Novo projeto de aplicativo em branco (Xamarin.Forms Portable) em VS 2019](media/CrossPlatform-NewProject19-Part1.png)

    <span data-ttu-id="f6382-128">Altere o nome para Biblioteca de Registro e clique em Criar.</span><span class="sxs-lookup"><span data-stu-id="f6382-128">Change the name to LoggingLibrary, and click Create.</span></span>

    ![Nova configuração do App Em Branco (Xamarin.Forms Portable) no VS 2019](media/CrossPlatform-NewProject19-Part2.png)

<span data-ttu-id="f6382-130">A solução resultante contém dois projetos compartilhados, juntamente com uma variedade de projetos específicos da plataforma:</span><span class="sxs-lookup"><span data-stu-id="f6382-130">The resulting solution contains two Shared projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="f6382-131">O `ILoggingLibrary` projeto, que está `ILoggingLibrary.shared.cs` contido no arquivo, define a interface pública (a área de superfície da API) do componente.</span><span class="sxs-lookup"><span data-stu-id="f6382-131">The `ILoggingLibrary` project, which is contained in the `ILoggingLibrary.shared.cs` file, defines the public interface (the API surface area) of the component.</span></span> <span data-ttu-id="f6382-132">É aqui que você define a interface para a biblioteca.</span><span class="sxs-lookup"><span data-stu-id="f6382-132">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="f6382-133">O outro projeto compartilhado `CrossLoggingLibrary.shared.cs` contém código que localizará uma implementação específica da interface abstrata em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="f6382-133">The other Shared project contains code in `CrossLoggingLibrary.shared.cs` that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="f6382-134">Normalmente não é necessário modificar esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="f6382-134">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="f6382-135">Os projetos específicos da `LoggingLibrary.android.cs`plataforma, como , cada um contém `LoggingLibraryImplementation.cs` uma implementação nativa `LoggingLibrary.<PLATFORM>.cs` da interface em seus respectivos arquivos (VS 2017) ou (VS 2019).</span><span class="sxs-lookup"><span data-stu-id="f6382-135">The platform-specific projects, such as `LoggingLibrary.android.cs`, each contain a native implementation of the interface in their respective `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) files.</span></span> <span data-ttu-id="f6382-136">É aqui que você compila o código da biblioteca.</span><span class="sxs-lookup"><span data-stu-id="f6382-136">This is where you build out your library's code.</span></span>

<span data-ttu-id="f6382-137">Por padrão, o arquivo `ILoggingLibrary` ILoggingLibrary.shared.cs do projeto contém uma definição de interface, mas sem métodos.</span><span class="sxs-lookup"><span data-stu-id="f6382-137">By default, the ILoggingLibrary.shared.cs file of the `ILoggingLibrary` project contains an interface definition, but no methods.</span></span> <span data-ttu-id="f6382-138">Para os fins deste passo a passo, adicione um método `Log` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f6382-138">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace Plugin.LoggingLibrary
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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="f6382-139">Escreva o código específico para sua plataforma</span><span class="sxs-lookup"><span data-stu-id="f6382-139">Write your platform-specific code</span></span>

<span data-ttu-id="f6382-140">Para implementar uma implementação específica da plataforma `ILoggingLibrary` e seus métodos, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f6382-140">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="f6382-141">Abra `LoggingLibraryImplementation.cs` o arquivo (VS 2017) ou `LoggingLibrary.<PLATFORM>.cs` (VS 2019) de cada projeto de plataforma e adicione o código necessário.</span><span class="sxs-lookup"><span data-stu-id="f6382-141">Open the `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) file of each platform project and add the necessary code.</span></span> <span data-ttu-id="f6382-142">Por exemplo (usando o projeto da `Android` plataforma):</span><span class="sxs-lookup"><span data-stu-id="f6382-142">For example (using the `Android` platform project):</span></span>

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Text;

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

1. <span data-ttu-id="f6382-143">Repita essa implementação nos projetos para cada plataforma às quais você deseja dar suporte.</span><span class="sxs-lookup"><span data-stu-id="f6382-143">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="f6382-144">Clique com o botão direito do mouse e selecione **Compilar solução** para verificar seu trabalho e produzir os artefatos que são empacotados em seguida.</span><span class="sxs-lookup"><span data-stu-id="f6382-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="f6382-145">Se você receber erros sobre referências ausentes, clique com o botão direito do mouse na solução, selecione **Restaurar pacotes do NuGet** para instalar as dependências e recompile.</span><span class="sxs-lookup"><span data-stu-id="f6382-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="f6382-146">Se você estiver usando o Visual Studio 2019, antes de selecionar **Restaurar pacotes NuGet** e tentar reconstruir, você precisa alterar a versão de `MSBuild.Sdk.Extras` para `2.0.54` dentro `LoggingLibrary.csproj`.</span><span class="sxs-lookup"><span data-stu-id="f6382-146">If you are using Visual Studio 2019, before selecting **Restore NuGet Packages** and trying to rebuild, you need to change the version of `MSBuild.Sdk.Extras` to `2.0.54` in `LoggingLibrary.csproj`.</span></span> <span data-ttu-id="f6382-147">Este arquivo só pode ser acessado primeiro clicando com o botão `Unload Project`direito do mouse no projeto (abaixo da `Edit LoggingLibrary.csproj`solução) e selecionando , após o qual você clica com o botão direito do mouse no projeto descarregado e seleciona .</span><span class="sxs-lookup"><span data-stu-id="f6382-147">This file can only be accessed by first right-clicking the project (below the solution) and selecting `Unload Project`, after which you right-click on the unloaded project and select `Edit LoggingLibrary.csproj`.</span></span>

> [!Note]
> <span data-ttu-id="f6382-148">Para compilar para iOS, é necessário ter um Mac em rede conectado ao Visual Studio, conforme descrito em [Introdução ao Xamarin.iOS para Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span><span class="sxs-lookup"><span data-stu-id="f6382-148">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="f6382-149">Se você não tiver um Mac disponível, apague o projeto iOS no Gerenciador de Configuração (etapa 3 acima).</span><span class="sxs-lookup"><span data-stu-id="f6382-149">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="f6382-150">Criar e atualizar o arquivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="f6382-150">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="f6382-151">Abra um prompt de comando, navegue até a pasta `LoggingLibrary` que está um nível abaixo do qual o arquivo `.sln` está e execute o comando `spec` do NuGet para criar o arquivo `Package.nuspec` inicial:</span><span class="sxs-lookup"><span data-stu-id="f6382-151">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="f6382-152">Renomeie este arquivo para `LoggingLibrary.nuspec` e abra-o em um editor.</span><span class="sxs-lookup"><span data-stu-id="f6382-152">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="f6382-153">Atualize o arquivo para corresponder ao seguinte, substituindo YOUR_NAME por um valor apropriado.</span><span class="sxs-lookup"><span data-stu-id="f6382-153">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="f6382-154">O valor `<id>`, especificamente, precisa ser exclusivo no nuget.org (consulte as convenções de nomenclatura descritas em [Criando um pacote](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="f6382-154">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="f6382-155">Observe que você também precisa atualizar as marcas de autor e descrição ou um erro é mostrado durante a etapa de empacotamento.</span><span class="sxs-lookup"><span data-stu-id="f6382-155">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2018</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="f6382-156">Você pode acrescentar o sufixo à sua versão de pacote com `-alpha`, `-beta` ou `-rc` para marcar o pacote como versão de pré-lançamento, consulte [Versões de pré-lançamento](../create-packages/prerelease-packages.md) para obter mais informações sobre as versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="f6382-156">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="f6382-157">Adicionar assemblies de referência</span><span class="sxs-lookup"><span data-stu-id="f6382-157">Add reference assemblies</span></span>

<span data-ttu-id="f6382-158">Para incluir os assemblies de referência específicos de plataforma, adicione o seguinte ao elemento `<files>` de `LoggingLibrary.nuspec` conforme apropriado para as plataformas compatíveis:</span><span class="sxs-lookup"><span data-stu-id="f6382-158">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="f6382-159">Para encurtar os nomes dos arquivos DLL e XML, clique com o botão direito do mouse em qualquer projeto, selecione a guia **Biblioteca** e altere os nomes de assembly.</span><span class="sxs-lookup"><span data-stu-id="f6382-159">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="f6382-160">Adicionar dependências</span><span class="sxs-lookup"><span data-stu-id="f6382-160">Add dependencies</span></span>

<span data-ttu-id="f6382-161">Se você tiver dependências específicas para implementações nativas, use o elemento `<dependencies>` com elementos `<group>` especificá-los, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f6382-161">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="f6382-162">Por exemplo, o seguinte definiria iTextSharp como uma dependência para o destino UAP:</span><span class="sxs-lookup"><span data-stu-id="f6382-162">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="f6382-163">.nuspec final</span><span class="sxs-lookup"><span data-stu-id="f6382-163">Final .nuspec</span></span>

<span data-ttu-id="f6382-164">O arquivo `.nuspec` final agora deve ser semelhante ao seguinte, em que novamente YOUR_NAME deve ser substituído por um valor apropriado:</span><span class="sxs-lookup"><span data-stu-id="f6382-164">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2018</copyright>
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

## <a name="package-the-component"></a><span data-ttu-id="f6382-165">Empacotar o componente</span><span class="sxs-lookup"><span data-stu-id="f6382-165">Package the component</span></span>

<span data-ttu-id="f6382-166">Depois do `.nuspec` terminar de referenciar todos os arquivos que você precisa incluir no pacote, você estará pronto para executar o comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="f6382-166">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="f6382-167">Isso gerará `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="f6382-167">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="f6382-168">Ao abrir este arquivo em uma ferramenta como o [Explorador de Pacotes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) e expandir todos os nós, você verá o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="f6382-168">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![O Explorador de Pacotes do NuGet mostrando o pacote LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="f6382-170">O arquivo `.nupkg` é apenas um arquivo ZIP com uma extensão diferente.</span><span class="sxs-lookup"><span data-stu-id="f6382-170">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="f6382-171">Também é possível examinar o conteúdo do pacote alterando `.nupkg` para `.zip`, mas lembre-se de restaurar a extensão antes de carregar um pacote para o nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f6382-171">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="f6382-172">Para disponibilizar seu pacote para outros desenvolvedores, siga as instruções em [Publicar um pacote](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="f6382-172">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="f6382-173">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="f6382-173">Related topics</span></span>

- [<span data-ttu-id="f6382-174">Referência nuspec</span><span class="sxs-lookup"><span data-stu-id="f6382-174">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="f6382-175">Pacotes de símbolo</span><span class="sxs-lookup"><span data-stu-id="f6382-175">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="f6382-176">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="f6382-176">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="f6382-177">Suporte a Várias Versões do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="f6382-177">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="f6382-178">Incluir objetivos e destinos de MSBuild em um pacote</span><span class="sxs-lookup"><span data-stu-id="f6382-178">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="f6382-179">Criando pacotes localizados</span><span class="sxs-lookup"><span data-stu-id="f6382-179">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
