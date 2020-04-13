---
title: Criar pacotes do NuGet para a Plataforma Universal do Windows
description: Um passo a passo completo da criação de pacotes NuGet usando um componente de tempo de execução do Windows para a Plataforma Universal windows em C#.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231801"
---
# <a name="create-uwp-packages-c"></a><span data-ttu-id="a37be-103">Criar pacotes UWP (C#)</span><span class="sxs-lookup"><span data-stu-id="a37be-103">Create UWP packages (C#)</span></span>

<span data-ttu-id="a37be-104">A [UWP (Plataforma Universal do Windows)](/windows/uwp) fornece uma plataforma de aplicativo comum para todos os dispositivos que são executados no Windows 10.</span><span class="sxs-lookup"><span data-stu-id="a37be-104">The [Universal Windows Platform (UWP)](/windows/uwp) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="a37be-105">Nesse modelo, os aplicativos UWP podem chamar APIs do WinRT que são comuns a todos os dispositivos e APIs (incluindo Win32 e .NET) que são específicas para a família do dispositivo no qual o aplicativo está em execução.</span><span class="sxs-lookup"><span data-stu-id="a37be-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="a37be-106">Neste passo a passo, você cria um pacote NuGet com um componente C# UWP (incluindo um controle XAML) que pode ser usado em projetos gerenciados e nativos.</span><span class="sxs-lookup"><span data-stu-id="a37be-106">In this walkthrough you create a NuGet package with a C# UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a37be-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a37be-107">Prerequisites</span></span>

1. <span data-ttu-id="a37be-108">Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="a37be-108">Visual Studio 2019.</span></span> <span data-ttu-id="a37be-109">Instale a edição comunitária 2019 gratuitamente a partir de [visualstudio.com;](https://www.visualstudio.com/) você pode usar as edições Profissional e Empresarial também.</span><span class="sxs-lookup"><span data-stu-id="a37be-109">Install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="a37be-110">CLI do NuGet.</span><span class="sxs-lookup"><span data-stu-id="a37be-110">NuGet CLI.</span></span> <span data-ttu-id="a37be-111">Baixe a versão mais recente do `nuget.exe` de [nuget.org/downloads](https://nuget.org/downloads) e salve-a em um local de sua escolha (o download é o `.exe` diretamente).</span><span class="sxs-lookup"><span data-stu-id="a37be-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="a37be-112">Em seguida, adicione tal local à sua variável de ambiente PATH, se ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="a37be-112">Then add that location to your PATH environment variable if it isn't already.</span></span> <span data-ttu-id="a37be-113">[Mais detalhes](/nuget/reference/nuget-exe-cli-reference#windows).</span><span class="sxs-lookup"><span data-stu-id="a37be-113">[More details](/nuget/reference/nuget-exe-cli-reference#windows).</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="a37be-114">Criar um componente do Windows Runtime da UWP</span><span class="sxs-lookup"><span data-stu-id="a37be-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="a37be-115">No Visual Studio, escolha **Arquivo > Novo Projeto >**, procure por "uwp c#", selecione o modelo do Componente de tempo de **execução do Windows (Universal Windows),** clique em seguir, altere o nome para ImageEnhancer e clique em Criar.</span><span class="sxs-lookup"><span data-stu-id="a37be-115">In Visual Studio, choose **File > New > Project**, search for "uwp c#", select the **Windows Runtime Component (Universal Windows)** template, click next, change the name to ImageEnhancer, and click Create.</span></span> <span data-ttu-id="a37be-116">Aceite os valores padrão para a Versão de Destino e a Versão Mínima quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="a37be-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Criar um projeto de componente do Windows Runtime UWP](media/UWP-NewProject-CS.png)

1. <span data-ttu-id="a37be-118">Clique com o botão direito do mouse no projeto no Solution Explorer, **selecione Adicionar > Novo Item,** **selecione Controle de modelos,** altere o nome para AwesomeImageControl.cs e clique em **Adicionar**:</span><span class="sxs-lookup"><span data-stu-id="a37be-118">Right click the project in Solution Explorer, select **Add > New Item**, select **Templated Control**, change the name to AwesomeImageControl.cs, and click **Add**:</span></span>

    ![Adicionar um novo item de Controle Modelo XAML ao projeto](media/UWP-NewXAMLControl-CS.png)

1. <span data-ttu-id="a37be-120">Clique com o botão direito do mouse no projeto no Solution Explorer e selecione **Propriedades.**</span><span class="sxs-lookup"><span data-stu-id="a37be-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="a37be-121">Na página Propriedades, escolha a guia **Construir** e habilitar **o Arquivo de Documentação XML**:</span><span class="sxs-lookup"><span data-stu-id="a37be-121">In the Properties page, choose **Build** tab and enable **XML Documentation File**:</span></span>

    ![Definindo a geração de arquivos de documentação XML para Sim](media/UWP-GenerateXMLDocFiles-CS.png)

1. <span data-ttu-id="a37be-123">Clique com o botão direito do mouse na *solução* agora, selecione **Batch Build**, verifique as cinco caixas de compilação na caixa de diálogo como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a37be-123">Right click the *solution* now, select **Batch Build**, check the five build boxes in the dialog as shown below.</span></span> <span data-ttu-id="a37be-124">Isso garante que, quando você fizer uma compilação, gerará um conjunto completo de artefatos para cada um dos sistemas de destino com os quais o Windows é compatível.</span><span class="sxs-lookup"><span data-stu-id="a37be-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Build em Lotes](media/UWP-BatchBuild-CS.png)

1. <span data-ttu-id="a37be-126">Na caixa de diálogo Compilação em Lotes, clique em **Compilar** para confirmar o projeto e criar os arquivos de saída que você precisa para o pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="a37be-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="a37be-127">Neste passo a passo, você usará os artefatos de Depuração para o pacote.</span><span class="sxs-lookup"><span data-stu-id="a37be-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="a37be-128">Para o pacote sem depuração, marque as opções de Versão na caixa de diálogo de Build em Lotes e consulte as pastas de Versão resultantes nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="a37be-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="a37be-129">Criar e atualizar o arquivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="a37be-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="a37be-130">Para criar o arquivo `.nuspec` inicial, execute as três etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="a37be-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="a37be-131">As seções a seguir, em seguida, guiarão você pelas outras atualizações necessárias.</span><span class="sxs-lookup"><span data-stu-id="a37be-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="a37be-132">Abra um prompt de comando e navegue até a pasta que contém `ImageEnhancer.csproj` (essa será uma subpasta abaixo onde está o arquivo da solução).</span><span class="sxs-lookup"><span data-stu-id="a37be-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.csproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="a37be-133">Execute [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) o comando `ImageEnhancer.nuspec` para gerar (o nome do arquivo `.csroj` é retirado do nome do arquivo):</span><span class="sxs-lookup"><span data-stu-id="a37be-133">Run the [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.csroj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="a37be-134">Abra o `ImageEnhancer.nuspec` em um editor e atualize-o para corresponder ao seguinte, substituindo YOUR_NAME por um valor apropriado.</span><span class="sxs-lookup"><span data-stu-id="a37be-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="a37be-135">Não deixe nenhum dos valores $propertyName$ .</span><span class="sxs-lookup"><span data-stu-id="a37be-135">Do not leave any of the $propertyName$ values.</span></span> <span data-ttu-id="a37be-136">O valor `<id>`, especificamente, precisa ser exclusivo no nuget.org (consulte as convenções de nomenclatura descritas em [Criando um pacote](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="a37be-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="a37be-137">Observe que você também precisa atualizar as marcas de autor e descrição ou um erro é mostrado durante a etapa de empacotamento.</span><span class="sxs-lookup"><span data-stu-id="a37be-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="a37be-138">Para pacotes compilados para consumo público, preste atenção especial ao elemento `<tags>`, visto que essas marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.</span><span class="sxs-lookup"><span data-stu-id="a37be-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="a37be-139">Adicionar metadados do Windows ao pacote</span><span class="sxs-lookup"><span data-stu-id="a37be-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="a37be-140">Um componente do Windows Runtime requer metadados que descrevem todos os seus tipos disponíveis publicamente, o que possibilita outros aplicativos e bibliotecas a consumirem o componente.</span><span class="sxs-lookup"><span data-stu-id="a37be-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="a37be-141">Esses metadados estão contidos em um arquivo .winmd, que é criado quando você compila o projeto e precisa ser incluído em seu pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="a37be-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="a37be-142">Um arquivo XML com os dados do IntelliSense também é criado ao mesmo tempo e também deve ser incluído.</span><span class="sxs-lookup"><span data-stu-id="a37be-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="a37be-143">Adicione o nó `<files>` a seguir ao arquivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="a37be-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

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

### <a name="adding-xaml-content"></a><span data-ttu-id="a37be-144">Adicionar conteúdo XAML</span><span class="sxs-lookup"><span data-stu-id="a37be-144">Adding XAML content</span></span>

<span data-ttu-id="a37be-145">Para incluir um controle XAML no seu componente, você precisa adicionar o arquivo XAML que tem o modelo padrão para o controle (conforme gerado pelo modelo de projeto).</span><span class="sxs-lookup"><span data-stu-id="a37be-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="a37be-146">Isso também vai para a seção `<files>`:</span><span class="sxs-lookup"><span data-stu-id="a37be-146">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="a37be-147">Adicionar as bibliotecas de implementação nativa</span><span class="sxs-lookup"><span data-stu-id="a37be-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="a37be-148">Dentro do seu componente, a lógica central do tipo ImageEnhancer está `ImageEnhancer.winmd` no código nativo, que está contido nos vários conjuntos gerados para cada tempo de execução de destino (ARM, ARM64, x86 e x64).</span><span class="sxs-lookup"><span data-stu-id="a37be-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.winmd` assemblies that are generated for each target runtime (ARM, ARM64, x86, and x64).</span></span> <span data-ttu-id="a37be-149">Para incluí-los no pacote, faça referência a eles na seção `<files>` juntamente com seus arquivos de recurso .pri associado:</span><span class="sxs-lookup"><span data-stu-id="a37be-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

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

### <a name="final-nuspec"></a><span data-ttu-id="a37be-150">.nuspec final</span><span class="sxs-lookup"><span data-stu-id="a37be-150">Final .nuspec</span></span>

<span data-ttu-id="a37be-151">O arquivo `.nuspec` final agora deve ser semelhante ao seguinte, em que novamente YOUR_NAME deve ser substituído por um valor apropriado:</span><span class="sxs-lookup"><span data-stu-id="a37be-151">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="a37be-152">Empacotar o componente</span><span class="sxs-lookup"><span data-stu-id="a37be-152">Package the component</span></span>

<span data-ttu-id="a37be-153">Com a `.nuspec` referência completa a todos os arquivos que você precisa incluir [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) no pacote, você está pronto para executar o comando:</span><span class="sxs-lookup"><span data-stu-id="a37be-153">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="a37be-154">Isso gera `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="a37be-154">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="a37be-155">Ao abrir este arquivo em uma ferramenta como o [Explorador de Pacotes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) e expandir todos os nós, você verá o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="a37be-155">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![O Explorador de Pacotes do NuGet mostrando o pacote ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="a37be-157">O arquivo `.nupkg` é apenas um arquivo ZIP com uma extensão diferente.</span><span class="sxs-lookup"><span data-stu-id="a37be-157">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="a37be-158">Também é possível examinar o conteúdo do pacote alterando `.nupkg` para `.zip`, mas lembre-se de restaurar a extensão antes de carregar um pacote para o nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a37be-158">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="a37be-159">Para disponibilizar seu pacote para outros desenvolvedores, siga as instruções em [Publicar um pacote](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="a37be-159">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="a37be-160">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="a37be-160">Related topics</span></span>

- [<span data-ttu-id="a37be-161">Referência .nuspec</span><span class="sxs-lookup"><span data-stu-id="a37be-161">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="a37be-162">Pacotes de símbolo</span><span class="sxs-lookup"><span data-stu-id="a37be-162">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="a37be-163">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="a37be-163">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="a37be-164">Suporte a Várias Versões do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="a37be-164">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="a37be-165">Incluir objetivos e destinos de MSBuild em um pacote</span><span class="sxs-lookup"><span data-stu-id="a37be-165">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="a37be-166">Criando pacotes localizados</span><span class="sxs-lookup"><span data-stu-id="a37be-166">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
