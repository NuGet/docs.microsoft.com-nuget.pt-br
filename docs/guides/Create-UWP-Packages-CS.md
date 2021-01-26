---
title: Criar pacotes NuGet para a plataforma UWP (C#)
description: Uma explicação de ponta a ponta da criação de pacotes NuGet usando um componente Windows Runtime para o Plataforma Universal do Windows em C#.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 22df2cd6dc374ba265c79a019747191e797b774c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774284"
---
# <a name="create-uwp-packages-c"></a><span data-ttu-id="45a85-103">Criar pacotes UWP (C#)</span><span class="sxs-lookup"><span data-stu-id="45a85-103">Create UWP packages (C#)</span></span>

<span data-ttu-id="45a85-104">A [UWP (Plataforma Universal do Windows)](/windows/uwp) fornece uma plataforma de aplicativo comum para todos os dispositivos que são executados no Windows 10.</span><span class="sxs-lookup"><span data-stu-id="45a85-104">The [Universal Windows Platform (UWP)](/windows/uwp) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="45a85-105">Nesse modelo, os aplicativos UWP podem chamar APIs do WinRT que são comuns a todos os dispositivos e APIs (incluindo Win32 e .NET) que são específicas para a família do dispositivo no qual o aplicativo está em execução.</span><span class="sxs-lookup"><span data-stu-id="45a85-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="45a85-106">Neste tutorial, você cria um pacote NuGet com um componente UWP do C# (incluindo um controle XAML) que pode ser usado em projetos gerenciados e nativos.</span><span class="sxs-lookup"><span data-stu-id="45a85-106">In this walkthrough you create a NuGet package with a C# UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45a85-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="45a85-107">Prerequisites</span></span>

1. <span data-ttu-id="45a85-108">Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="45a85-108">Visual Studio 2019.</span></span> <span data-ttu-id="45a85-109">Instale o 2019 Community Edition gratuitamente do [VisualStudio.com](https://www.visualstudio.com/); Você também pode usar as edições Professional e Enterprise.</span><span class="sxs-lookup"><span data-stu-id="45a85-109">Install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="45a85-110">CLI do NuGet.</span><span class="sxs-lookup"><span data-stu-id="45a85-110">NuGet CLI.</span></span> <span data-ttu-id="45a85-111">Baixe a versão mais recente do `nuget.exe` de [nuget.org/downloads](https://nuget.org/downloads) e salve-a em um local de sua escolha (o download é o `.exe` diretamente).</span><span class="sxs-lookup"><span data-stu-id="45a85-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="45a85-112">Em seguida, adicione tal local à sua variável de ambiente PATH, se ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="45a85-112">Then add that location to your PATH environment variable if it isn't already.</span></span> <span data-ttu-id="45a85-113">[Mais detalhes](../reference/nuget-exe-cli-reference.md#windows).</span><span class="sxs-lookup"><span data-stu-id="45a85-113">[More details](../reference/nuget-exe-cli-reference.md#windows).</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="45a85-114">Criar um componente do Windows Runtime da UWP</span><span class="sxs-lookup"><span data-stu-id="45a85-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="45a85-115">No Visual Studio, escolha **arquivo > novo projeto de >**, pesquise "UWP c#", selecione o modelo **componente do Windows Runtime (universal do Windows)** , clique em avançar, altere o nome para ImageEnhancer e clique em criar.</span><span class="sxs-lookup"><span data-stu-id="45a85-115">In Visual Studio, choose **File > New > Project**, search for "uwp c#", select the **Windows Runtime Component (Universal Windows)** template, click next, change the name to ImageEnhancer, and click Create.</span></span> <span data-ttu-id="45a85-116">Aceite os valores padrão para a Versão de Destino e a Versão Mínima quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="45a85-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Criar um projeto de componente do Windows Runtime UWP](media/UWP-NewProject-CS.png)

1. <span data-ttu-id="45a85-118">Clique com o botão direito do mouse no projeto em Gerenciador de Soluções, selecione **adicionar > novo item**, selecione **controle modelo**, altere o nome para AwesomeImageControl.cs e clique em **Adicionar**:</span><span class="sxs-lookup"><span data-stu-id="45a85-118">Right click the project in Solution Explorer, select **Add > New Item**, select **Templated Control**, change the name to AwesomeImageControl.cs, and click **Add**:</span></span>

    ![Adicionar um novo item de Controle Modelo XAML ao projeto](media/UWP-NewXAMLControl-CS.png)

1. <span data-ttu-id="45a85-120">Clique com o botão direito do mouse no projeto em Gerenciador de Soluções e selecione **Propriedades.**</span><span class="sxs-lookup"><span data-stu-id="45a85-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="45a85-121">Na página Propriedades, escolha a guia **Compilar** e habilite o **arquivo de documentação XML**:</span><span class="sxs-lookup"><span data-stu-id="45a85-121">In the Properties page, choose **Build** tab and enable **XML Documentation File**:</span></span>

    ![Definindo a geração de arquivos de documentação XML para Sim](media/UWP-GenerateXMLDocFiles-CS.png)

1. <span data-ttu-id="45a85-123">Clique com o botão direito do mouse na *solução* agora, selecione **Build do lote**, marque as cinco caixas de Build na caixa de diálogo, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="45a85-123">Right click the *solution* now, select **Batch Build**, check the five build boxes in the dialog as shown below.</span></span> <span data-ttu-id="45a85-124">Isso garante que, quando você fizer uma compilação, gerará um conjunto completo de artefatos para cada um dos sistemas de destino com os quais o Windows é compatível.</span><span class="sxs-lookup"><span data-stu-id="45a85-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Build em Lotes](media/UWP-BatchBuild-CS.png)

1. <span data-ttu-id="45a85-126">Na caixa de diálogo Compilação em Lotes, clique em **Compilar** para confirmar o projeto e criar os arquivos de saída que você precisa para o pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="45a85-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="45a85-127">Neste passo a passo, você usará os artefatos de Depuração para o pacote.</span><span class="sxs-lookup"><span data-stu-id="45a85-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="45a85-128">Para o pacote sem depuração, marque as opções de Versão na caixa de diálogo de Build em Lotes e consulte as pastas de Versão resultantes nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="45a85-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="45a85-129">Criar e atualizar o arquivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="45a85-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="45a85-130">Para criar o arquivo `.nuspec` inicial, execute as três etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="45a85-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="45a85-131">As seções a seguir, em seguida, guiarão você pelas outras atualizações necessárias.</span><span class="sxs-lookup"><span data-stu-id="45a85-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="45a85-132">Abra um prompt de comando e navegue até a pasta que contém `ImageEnhancer.csproj` (essa será uma subpasta abaixo onde está o arquivo da solução).</span><span class="sxs-lookup"><span data-stu-id="45a85-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.csproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="45a85-133">Execute o [`NuGet spec`](../reference/cli-reference/cli-ref-spec.md) comando a ser gerado `ImageEnhancer.nuspec` (o nome do arquivo é obtido do nome do `.csroj` arquivo):</span><span class="sxs-lookup"><span data-stu-id="45a85-133">Run the [`NuGet spec`](../reference/cli-reference/cli-ref-spec.md) command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.csroj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="45a85-134">Abra o `ImageEnhancer.nuspec` em um editor e atualize-o para corresponder ao seguinte, substituindo YOUR_NAME por um valor apropriado.</span><span class="sxs-lookup"><span data-stu-id="45a85-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="45a85-135">Não deixe nenhum dos $propertyName valores $.</span><span class="sxs-lookup"><span data-stu-id="45a85-135">Do not leave any of the $propertyName$ values.</span></span> <span data-ttu-id="45a85-136">O valor `<id>`, especificamente, precisa ser exclusivo no nuget.org (consulte as convenções de nomenclatura descritas em [Criando um pacote](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="45a85-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="45a85-137">Observe que você também precisa atualizar as marcas de autor e descrição ou um erro é mostrado durante a etapa de empacotamento.</span><span class="sxs-lookup"><span data-stu-id="45a85-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2020</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="45a85-138">Para pacotes compilados para consumo público, preste atenção especial ao elemento `<tags>`, visto que essas marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.</span><span class="sxs-lookup"><span data-stu-id="45a85-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="45a85-139">Adicionar metadados do Windows ao pacote</span><span class="sxs-lookup"><span data-stu-id="45a85-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="45a85-140">Um componente do Windows Runtime requer metadados que descrevem todos os seus tipos disponíveis publicamente, o que possibilita outros aplicativos e bibliotecas a consumirem o componente.</span><span class="sxs-lookup"><span data-stu-id="45a85-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="45a85-141">Esses metadados estão contidos em um arquivo .winmd, que é criado quando você compila o projeto e precisa ser incluído em seu pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="45a85-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="45a85-142">Um arquivo XML com os dados do IntelliSense também é criado ao mesmo tempo e também deve ser incluído.</span><span class="sxs-lookup"><span data-stu-id="45a85-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="45a85-143">Adicione o nó `<files>` a seguir ao arquivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="45a85-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="45a85-144">Adicionar conteúdo XAML</span><span class="sxs-lookup"><span data-stu-id="45a85-144">Adding XAML content</span></span>

<span data-ttu-id="45a85-145">Para incluir um controle XAML no seu componente, você precisa adicionar o arquivo XAML que tem o modelo padrão para o controle (conforme gerado pelo modelo de projeto).</span><span class="sxs-lookup"><span data-stu-id="45a85-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="45a85-146">Isso também vai para a seção `<files>`:</span><span class="sxs-lookup"><span data-stu-id="45a85-146">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="45a85-147">Adicionar as bibliotecas de implementação nativa</span><span class="sxs-lookup"><span data-stu-id="45a85-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="45a85-148">Dentro de seu componente, a lógica principal do tipo ImageEnhancer está no código nativo, que está contido nos vários `ImageEnhancer.winmd` assemblies que são gerados para cada tempo de execução de destino (ARM, ARM64, x86 e x64).</span><span class="sxs-lookup"><span data-stu-id="45a85-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.winmd` assemblies that are generated for each target runtime (ARM, ARM64, x86, and x64).</span></span> <span data-ttu-id="45a85-149">Para incluí-los no pacote, faça referência a eles na seção `<files>` juntamente com seus arquivos de recurso .pri associado:</span><span class="sxs-lookup"><span data-stu-id="45a85-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="45a85-150">.nuspec final</span><span class="sxs-lookup"><span data-stu-id="45a85-150">Final .nuspec</span></span>

<span data-ttu-id="45a85-151">O arquivo `.nuspec` final agora deve ser semelhante ao seguinte, em que novamente YOUR_NAME deve ser substituído por um valor apropriado:</span><span class="sxs-lookup"><span data-stu-id="45a85-151">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="45a85-152">Empacotar o componente</span><span class="sxs-lookup"><span data-stu-id="45a85-152">Package the component</span></span>

<span data-ttu-id="45a85-153">Com o concluindo a `.nuspec` referência a todos os arquivos que você precisa incluir no pacote, você está pronto para executar o [`nuget pack`](../reference/cli-reference/cli-ref-pack.md) comando:</span><span class="sxs-lookup"><span data-stu-id="45a85-153">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the [`nuget pack`](../reference/cli-reference/cli-ref-pack.md) command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="45a85-154">Isso gera `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="45a85-154">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="45a85-155">Ao abrir este arquivo em uma ferramenta como o [Explorador de Pacotes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) e expandir todos os nós, você verá o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="45a85-155">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![O Explorador de Pacotes do NuGet mostrando o pacote ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="45a85-157">O arquivo `.nupkg` é apenas um arquivo ZIP com uma extensão diferente.</span><span class="sxs-lookup"><span data-stu-id="45a85-157">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="45a85-158">Também é possível examinar o conteúdo do pacote alterando `.nupkg` para `.zip`, mas lembre-se de restaurar a extensão antes de carregar um pacote para o nuget.org.</span><span class="sxs-lookup"><span data-stu-id="45a85-158">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="45a85-159">Para disponibilizar seu pacote para outros desenvolvedores, siga as instruções em [Publicar um pacote](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="45a85-159">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="45a85-160">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="45a85-160">Related topics</span></span>

- [<span data-ttu-id="45a85-161">Referência de. nuspec</span><span class="sxs-lookup"><span data-stu-id="45a85-161">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="45a85-162">Pacotes de símbolo</span><span class="sxs-lookup"><span data-stu-id="45a85-162">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="45a85-163">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="45a85-163">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="45a85-164">Suporte a Várias Versões do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="45a85-164">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="45a85-165">Incluir objetivos e destinos de MSBuild em um pacote</span><span class="sxs-lookup"><span data-stu-id="45a85-165">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="45a85-166">Criando pacotes localizados</span><span class="sxs-lookup"><span data-stu-id="45a85-166">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)