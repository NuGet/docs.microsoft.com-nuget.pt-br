---
title: Criar pacotes do NuGet para a Plataforma Universal do Windows
description: Uma explicação passo a passo de ponta a ponta da criação de pacotes do NuGet usando um componente do Windows Runtime para a Plataforma Universal do Windows.
author: JonDouglas
ms.author: jodou
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: c077645508cb10e86b3ed1e1f2bf61adcd2013d9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774238"
---
# <a name="create-uwp-packages"></a><span data-ttu-id="acc11-103">Criar pacotes UWP</span><span class="sxs-lookup"><span data-stu-id="acc11-103">Create UWP packages</span></span>

<span data-ttu-id="acc11-104">A [UWP (Plataforma Universal do Windows)](https://developer.microsoft.com/windows) fornece uma plataforma de aplicativo comum para todos os dispositivos que são executados no Windows 10.</span><span class="sxs-lookup"><span data-stu-id="acc11-104">The [Universal Windows Platform (UWP)](https://developer.microsoft.com/windows) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="acc11-105">Nesse modelo, os aplicativos UWP podem chamar APIs do WinRT que são comuns a todos os dispositivos e APIs (incluindo Win32 e .NET) que são específicas para a família do dispositivo no qual o aplicativo está em execução.</span><span class="sxs-lookup"><span data-stu-id="acc11-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="acc11-106">Neste passo a passo, você cria um pacote NuGet com um componente UWP nativo (incluindo um controle XAML) que pode ser usado em projetos nativos e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="acc11-106">In this walkthrough you create a NuGet package with a native UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acc11-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="acc11-107">Prerequisites</span></span>

1. <span data-ttu-id="acc11-108">Visual Studio 2017 ou 2015.</span><span class="sxs-lookup"><span data-stu-id="acc11-108">Visual Studio 2017 or Visual Studio 2015.</span></span> <span data-ttu-id="acc11-109">Instale a edição Community 2017 gratuitamente no [visualstudio.com](https://www.visualstudio.com/); você também pode usar as edições Professional e Enterprise.</span><span class="sxs-lookup"><span data-stu-id="acc11-109">Install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="acc11-110">CLI do NuGet.</span><span class="sxs-lookup"><span data-stu-id="acc11-110">NuGet CLI.</span></span> <span data-ttu-id="acc11-111">Baixe a versão mais recente do `nuget.exe` de [nuget.org/downloads](https://nuget.org/downloads) e salve-a em um local de sua escolha (o download é o `.exe` diretamente).</span><span class="sxs-lookup"><span data-stu-id="acc11-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="acc11-112">Em seguida, adicione tal local à sua variável de ambiente PATH, se ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="acc11-112">Then add that location to your PATH environment variable if it isn't already.</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="acc11-113">Criar um componente do Windows Runtime da UWP</span><span class="sxs-lookup"><span data-stu-id="acc11-113">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="acc11-114">No Visual Studio, escolha **Arquivo &gt; Novo &gt; Projeto**, expanda o nó **Visual C++ &gt; Windows &gt; Universal**, selecione o modelo **componente do Windows Runtime (Universal do Windows)**, altere o nome para ImageEnhancer e clique em OK.</span><span class="sxs-lookup"><span data-stu-id="acc11-114">In Visual Studio, choose **File > New > Project**, expand the **Visual C++ > Windows > Universal** node, select the **Windows Runtime Component (Universal Windows)** template, change the name to ImageEnhancer, and click OK.</span></span> <span data-ttu-id="acc11-115">Aceite os valores padrão para a Versão de Destino e a Versão Mínima quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="acc11-115">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Criar um projeto de componente do Windows Runtime UWP](media/UWP-NewProject.png)

1. <span data-ttu-id="acc11-117">Clique com botão direito do mouse no projeto no Gerenciador de Soluções, selecione **Adicionar > Novo Item**, clique no nó **Visual C++ > XAML**, selecione **Controle modelo**, altere o nome para AwesomeImageControl.cpp e clique em **Adicionar**:</span><span class="sxs-lookup"><span data-stu-id="acc11-117">Right click the project in Solution Explorer, select **Add > New Item**, click the **Visual C++ > XAML** node, select **Templated Control**, change the name to AwesomeImageControl.cpp, and click **Add**:</span></span>

    ![Adicionar um novo item de Controle Modelo XAML ao projeto](media/UWP-NewXAMLControl.png)

1. <span data-ttu-id="acc11-119">Clique com o botão direito do mouse no projeto em Gerenciador de Soluções e selecione **Propriedades.**</span><span class="sxs-lookup"><span data-stu-id="acc11-119">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="acc11-120">Na página Propriedades, expanda **Propriedades de configuração > C/C++** e clique em **Arquivos de saída**.</span><span class="sxs-lookup"><span data-stu-id="acc11-120">In the Properties page, expand **Configuration Properties > C/C++** and click **Output Files**.</span></span> <span data-ttu-id="acc11-121">No painel à direita, altere o valor para **Gerar arquivos de documentação XML** para Sim:</span><span class="sxs-lookup"><span data-stu-id="acc11-121">In the pane on the right, change the value for **Generate XML Documentation Files** to Yes:</span></span>

    ![Definindo a geração de arquivos de documentação XML para Sim](media/UWP-GenerateXMLDocFiles.png)

1. <span data-ttu-id="acc11-123">Clique com botão direito do mouse na *solução* agora, selecione **Build em Lotes** e marque as três caixas de Depuração na caixa de diálogo, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="acc11-123">Right click the *solution* now, select **Batch Build**, check the three Debug boxes in the dialog as shown below.</span></span> <span data-ttu-id="acc11-124">Isso garante que, quando você fizer uma compilação, gerará um conjunto completo de artefatos para cada um dos sistemas de destino com os quais o Windows é compatível.</span><span class="sxs-lookup"><span data-stu-id="acc11-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Build em Lotes](media/UWP-BatchBuild.png)

1. <span data-ttu-id="acc11-126">Na caixa de diálogo Compilação em Lotes, clique em **Compilar** para confirmar o projeto e criar os arquivos de saída que você precisa para o pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="acc11-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="acc11-127">Neste passo a passo, você usará os artefatos de Depuração para o pacote.</span><span class="sxs-lookup"><span data-stu-id="acc11-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="acc11-128">Para o pacote sem depuração, marque as opções de Versão na caixa de diálogo de Build em Lotes e consulte as pastas de Versão resultantes nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="acc11-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="acc11-129">Criar e atualizar o arquivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="acc11-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="acc11-130">Para criar o arquivo `.nuspec` inicial, execute as três etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="acc11-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="acc11-131">As seções a seguir, em seguida, guiarão você pelas outras atualizações necessárias.</span><span class="sxs-lookup"><span data-stu-id="acc11-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="acc11-132">Abra um prompt de comando e navegue até a pasta que contém `ImageEnhancer.vcxproj` (essa será uma subpasta abaixo onde está o arquivo da solução).</span><span class="sxs-lookup"><span data-stu-id="acc11-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.vcxproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="acc11-133">Execute o comando `spec` do NuGet para gerar `ImageEnhancer.nuspec` (o nome do arquivo é obtido do nome do arquivo `.vcxproj`):</span><span class="sxs-lookup"><span data-stu-id="acc11-133">Run the NuGet `spec` command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.vcxproj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="acc11-134">Abra o `ImageEnhancer.nuspec` em um editor e atualize-o para corresponder ao seguinte, substituindo YOUR_NAME por um valor apropriado.</span><span class="sxs-lookup"><span data-stu-id="acc11-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="acc11-135">O valor `<id>`, especificamente, precisa ser exclusivo no nuget.org (consulte as convenções de nomenclatura descritas em [Criando um pacote](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="acc11-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="acc11-136">Observe que você também precisa atualizar as marcas de autor e descrição ou um erro é mostrado durante a etapa de empacotamento.</span><span class="sxs-lookup"><span data-stu-id="acc11-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="acc11-137">Para pacotes compilados para consumo público, preste atenção especial ao elemento `<tags>`, visto que essas marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.</span><span class="sxs-lookup"><span data-stu-id="acc11-137">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="acc11-138">Adicionar metadados do Windows ao pacote</span><span class="sxs-lookup"><span data-stu-id="acc11-138">Adding Windows metadata to the package</span></span>

<span data-ttu-id="acc11-139">Um componente do Windows Runtime requer metadados que descrevem todos os seus tipos disponíveis publicamente, o que possibilita outros aplicativos e bibliotecas a consumirem o componente.</span><span class="sxs-lookup"><span data-stu-id="acc11-139">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="acc11-140">Esses metadados estão contidos em um arquivo .winmd, que é criado quando você compila o projeto e precisa ser incluído em seu pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="acc11-140">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="acc11-141">Um arquivo XML com os dados do IntelliSense também é criado ao mesmo tempo e também deve ser incluído.</span><span class="sxs-lookup"><span data-stu-id="acc11-141">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="acc11-142">Adicione o nó `<files>` a seguir ao arquivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="acc11-142">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="acc11-143">Adicionar conteúdo XAML</span><span class="sxs-lookup"><span data-stu-id="acc11-143">Adding XAML content</span></span>

<span data-ttu-id="acc11-144">Para incluir um controle XAML no seu componente, você precisa adicionar o arquivo XAML que tem o modelo padrão para o controle (conforme gerado pelo modelo de projeto).</span><span class="sxs-lookup"><span data-stu-id="acc11-144">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="acc11-145">Isso também vai para a seção `<files>`:</span><span class="sxs-lookup"><span data-stu-id="acc11-145">This also goes in the `<files>` section:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="acc11-146">Adicionar as bibliotecas de implementação nativa</span><span class="sxs-lookup"><span data-stu-id="acc11-146">Adding the native implementation libraries</span></span>

<span data-ttu-id="acc11-147">No seu componente, a lógica principal do tipo ImageEnhancer está no código nativo, que está contido nos vários assemblies `ImageEnhancer.dll` que são gerados para cada runtime de destino(ARM, x86 e x64).</span><span class="sxs-lookup"><span data-stu-id="acc11-147">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.dll` assemblies that are generated for each target runtime (ARM, x86, and x64).</span></span> <span data-ttu-id="acc11-148">Para incluí-los no pacote, faça referência a eles na seção `<files>` juntamente com seus arquivos de recurso .pri associado:</span><span class="sxs-lookup"><span data-stu-id="acc11-148">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a><span data-ttu-id="acc11-149">Adicionar .targets</span><span class="sxs-lookup"><span data-stu-id="acc11-149">Adding .targets</span></span>

<span data-ttu-id="acc11-150">Em seguida, projetos C++ e JavaScript que podem consumir seu pacote do NuGet precisam de um arquivo .targets para identificar os arquivos de assembly e winmd necessários.</span><span class="sxs-lookup"><span data-stu-id="acc11-150">Next, C++ and JavaScript projects that might consume your NuGet package need a .targets file to identify the necessary assembly and winmd files.</span></span> <span data-ttu-id="acc11-151">(Os projetos do C# e do Visual Basic fazem isso automaticamente.) Crie esse arquivo copiando o texto abaixo para `ImageEnhancer.targets` e salve-o na mesma pasta que o `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="acc11-151">(C# and Visual Basic projects do this automatically.) Create this file by copying the text below into `ImageEnhancer.targets` and save it in the same folder as the `.nuspec` file.</span></span> <span data-ttu-id="acc11-152">_Observação_: esse arquivo `.targets` precisa ter o mesmo nome que a ID do pacote (por exemplo, o elemento `<Id>` no arquivo `.nupspec`):</span><span class="sxs-lookup"><span data-stu-id="acc11-152">_Note_: This `.targets` file needs to be the same name as the package ID (e.g. the `<Id>` element in the `.nupspec` file):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

<span data-ttu-id="acc11-153">Em seguida, consulte `ImageEnhancer.targets` no seu arquivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="acc11-153">Then refer to `ImageEnhancer.targets` in your `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="acc11-154">.nuspec final</span><span class="sxs-lookup"><span data-stu-id="acc11-154">Final .nuspec</span></span>

<span data-ttu-id="acc11-155">O arquivo `.nuspec` final agora deve ser semelhante ao seguinte, em que novamente YOUR_NAME deve ser substituído por um valor apropriado:</span><span class="sxs-lookup"><span data-stu-id="acc11-155">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>     
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="acc11-156">Empacotar o componente</span><span class="sxs-lookup"><span data-stu-id="acc11-156">Package the component</span></span>

<span data-ttu-id="acc11-157">Depois do `.nuspec` terminar de referenciar todos os arquivos que você precisa incluir no pacote, você estará pronto para executar o comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="acc11-157">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="acc11-158">Isso gera `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="acc11-158">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="acc11-159">Ao abrir este arquivo em uma ferramenta como o [Explorador de Pacotes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) e expandir todos os nós, você verá o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="acc11-159">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![O Explorador de Pacotes do NuGet mostrando o pacote ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="acc11-161">O arquivo `.nupkg` é apenas um arquivo ZIP com uma extensão diferente.</span><span class="sxs-lookup"><span data-stu-id="acc11-161">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="acc11-162">Também é possível examinar o conteúdo do pacote alterando `.nupkg` para `.zip`, mas lembre-se de restaurar a extensão antes de carregar um pacote para o nuget.org.</span><span class="sxs-lookup"><span data-stu-id="acc11-162">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="acc11-163">Para disponibilizar seu pacote para outros desenvolvedores, siga as instruções em [Publicar um pacote](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="acc11-163">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="acc11-164">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="acc11-164">Related topics</span></span>

- [<span data-ttu-id="acc11-165">Referência de. nuspec</span><span class="sxs-lookup"><span data-stu-id="acc11-165">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="acc11-166">Pacotes de símbolo</span><span class="sxs-lookup"><span data-stu-id="acc11-166">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="acc11-167">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="acc11-167">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="acc11-168">Suporte a Várias Versões do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="acc11-168">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="acc11-169">Incluir objetivos e destinos de MSBuild em um pacote</span><span class="sxs-lookup"><span data-stu-id="acc11-169">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="acc11-170">Criando pacotes localizados</span><span class="sxs-lookup"><span data-stu-id="acc11-170">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
