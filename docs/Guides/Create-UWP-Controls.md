---
title: Como empacotar controles UWP com o NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/21/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Como criar pacotes do NuGet que contêm controles UWP, incluindo os metadados e os arquivos de suporte necessários para os designers do Visual Studio e do Blend."
keywords: Controles UWP do NuGet, designer XAML do Visual Studio, designer do Blend, controles personalizados
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3af17121f73b878decd5f0c933696fc1b0c786d7
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a><span data-ttu-id="4108c-104">Criando controles UWP como pacotes do NuGet</span><span class="sxs-lookup"><span data-stu-id="4108c-104">Creating UWP controls as NuGet packages</span></span>

<span data-ttu-id="4108c-105">Com o Visual Studio 2017, você pode aproveitar os recursos adicionados para os controles UWP que você fornecer em pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="4108c-105">With Visual Studio 2017, you can take advantage of added capabilities for UWP controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="4108c-106">Este guia orientará você quanto a esses recursos usando o [exemplo ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="4108c-106">This guide walks you through these capabilities using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> 

## <a name="pre-requisites"></a><span data-ttu-id="4108c-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4108c-107">Pre-requisites</span></span>

1. <span data-ttu-id="4108c-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="4108c-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="4108c-109">Noções básicas sobre como [Criar pacotes UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="4108c-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="4108c-110">Adicionar suporte para o painel da caixa de ferramentas/ativos a controles XAML</span><span class="sxs-lookup"><span data-stu-id="4108c-110">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="4108c-111">Para que um controle XAML apareça na caixa de ferramentas do designer XAML no Visual Studio e no painel de Ativos do Blend, crie um arquivo `VisualStudioToolsManifest.xml` na raiz da pasta `tools` do seu projeto de pacote.</span><span class="sxs-lookup"><span data-stu-id="4108c-111">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="4108c-112">Esse arquivo não é necessário se você não precisar que o controle apareça na caixa de ferramentas ou no painel Ativos.</span><span class="sxs-lookup"><span data-stu-id="4108c-112">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="4108c-113">A estrutura do arquivo é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="4108c-113">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="4108c-114">em que:</span><span class="sxs-lookup"><span data-stu-id="4108c-114">where:</span></span>

- <span data-ttu-id="4108c-115">*your_package_file*: o nome do arquivo do seu controle, como `ManagedPackage.winmd` (“ManagedPackage” é um nome arbitrário usado para este exemplo e não tem nenhum outro significado).</span><span class="sxs-lookup"><span data-stu-id="4108c-115">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="4108c-116">*vs_category*: o rótulo para o grupo no qual o controle deve aparecer na caixa de ferramentas do designer do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4108c-116">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="4108c-117">Um `VSCategory` é necessário para o controle apareça na caixa de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="4108c-117">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="4108c-118">*blend_category*: o rótulo para o grupo no qual o controle deve aparecer no painel Ativos do designer do Blend.</span><span class="sxs-lookup"><span data-stu-id="4108c-118">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="4108c-119">Um `BlendCategory` é necessário para o controle apareça em Ativos.</span><span class="sxs-lookup"><span data-stu-id="4108c-119">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="4108c-120">*type_full_name_n*: o nome totalmente qualificado para cada controle, incluindo o namespace, como `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="4108c-120">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="4108c-121">Observe que o formato de ponto é usado tanto para tipos gerenciados quanto para tipos nativos.</span><span class="sxs-lookup"><span data-stu-id="4108c-121">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="4108c-122">Em cenários mais avançados, também é possível incluir vários elementos `<File>` dentro de `<FileList>` quando um único pacote contém vários assemblies de controle.</span><span class="sxs-lookup"><span data-stu-id="4108c-122">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="4108c-123">Também é possível ter vários nós `<ToolboxItems>` dentro de um único `<File>` se você quiser organizar os controles em categorias separadas.</span><span class="sxs-lookup"><span data-stu-id="4108c-123">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="4108c-124">No exemplo a seguir, o controle implementado em `ManagedPackage.winmd` aparecerá no Visual Studio e no Blend em um grupo denominado “Managed Package” e “MyCustomControl” será exibido nesse grupo.</span><span class="sxs-lookup"><span data-stu-id="4108c-124">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="4108c-125">Todos esses nomes são arbitrários.</span><span class="sxs-lookup"><span data-stu-id="4108c-125">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Um controle de exemplo como ele aparece no Visual Studio](media/UWP-control-vs-toolbox.png)

![Um controle de exemplo como ele aparece no Blend](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="4108c-128">Você precisa especificar explicitamente cada controle deve ser exibido no painel de caixa de ferramentas/ativos.</span><span class="sxs-lookup"><span data-stu-id="4108c-128">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="4108c-129">Verifique se você os especificou no formato `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="4108c-129">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="4108c-130">Adicionar ícones personalizados aos seus controles</span><span class="sxs-lookup"><span data-stu-id="4108c-130">Add custom icons to your controls</span></span>

<span data-ttu-id="4108c-131">Para exibir um ícone personalizado no painel de caixa de ferramentas/ativos, adicione uma imagem ao seu projeto ou ao projeto `design.dll` correspondente com o nome “Namespace.ControlName.extension” e defina a ação de build como “Recurso Inserido”.</span><span class="sxs-lookup"><span data-stu-id="4108c-131">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="4108c-132">Os formatos compatíveis são `.png`, `.jpg`, `.jpeg`, `.gif` e `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="4108c-132">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="4108c-133">O tamanho da imagem recomendado é 64 pixels por 64 pixels.</span><span class="sxs-lookup"><span data-stu-id="4108c-133">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="4108c-134">No exemplo a seguir, o projeto contém um arquivo de imagem denominado “ManagedPackage.MyCustomControl.png”.</span><span class="sxs-lookup"><span data-stu-id="4108c-134">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Definir um ícone personalizado em um projeto](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="4108c-136">Para controles nativos, você deve colocar o ícone como um recurso do projeto `design.dll`.</span><span class="sxs-lookup"><span data-stu-id="4108c-136">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="4108c-137">Suporte a versões específicas de plataformas Windows</span><span class="sxs-lookup"><span data-stu-id="4108c-137">Support specific Windows platform versions</span></span>

<span data-ttu-id="4108c-138">Pacotes UWP têm um TPV (TargetPlatformVersion) e TPMinV (TargetPlatformMinVersion) que definem os limites superior e inferior da versão do sistema operacional em que o aplicativo pode ser instalado.</span><span class="sxs-lookup"><span data-stu-id="4108c-138">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="4108c-139">O TPV especifica ainda a versão do SDK na qual o aplicativo é compilado.</span><span class="sxs-lookup"><span data-stu-id="4108c-139">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="4108c-140">Preste atenção a essas propriedades ao criar um pacote UWP: usar APIs fora dos limites das versões de plataforma definidas no aplicativo fará com que a compilação falhe ou o aplicativo falhe no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="4108c-140">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="4108c-141">Por exemplo, digamos que você definiu o TPMinV para o pacote de controles para o Windows 10 Anniversary Edition (10.0; Build 14393), por isso pode ser útil garantir que o pacote seja consumido somente por projetos UWP que correspondem ao limite inferior.</span><span class="sxs-lookup"><span data-stu-id="4108c-141">For example, let’s say you’ve set the TPMinV for you controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="4108c-142">Para permitir que o pacote seja consumido por projetos UWP você precisa empacotar os controles com os seguintes nomes de pasta:</span><span class="sxs-lookup"><span data-stu-id="4108c-142">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0\*
    \ref\uap10.0\*

<span data-ttu-id="4108c-143">Para impor a verificação de TPMinV apropriada, crie um [arquivo de destino do MSBuild](/visualstudio/msbuild/msbuild-targets) e empacote-o na pasta de build (substituindo “your_assembly_name” pelo nome do seu assembly específico):</span><span class="sxs-lookup"><span data-stu-id="4108c-143">To enforce the appropriate TPMinV check, create an [MSBuild targets file](/visualstudio/msbuild/msbuild-targets) and package it under the build folder (replacing "your_assembly_name" with the name of your specific assembly):</span></span>

    \build
      \uap10.0
        your_assembly_name.targets
    \lib
    \tools

<span data-ttu-id="4108c-144">Veja este exemplo de como o arquivo de destino deve parecer:</span><span class="sxs-lookup"><span data-stu-id="4108c-144">Here is an example of what the targets file should look like:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="Build;ReBuild" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a><span data-ttu-id="4108c-145">Adicionar suporte no tempo de design</span><span class="sxs-lookup"><span data-stu-id="4108c-145">Add design-time support</span></span>

<span data-ttu-id="4108c-146">Para configurar onde as propriedades do controle aparecem na Inspeção de propriedade, adicionar adornos personalizados, etc., coloque o arquivo `design.dll` dentro da pasta `lib\<platform>\Design` conforme apropriado para a plataforma de destino.</span><span class="sxs-lookup"><span data-stu-id="4108c-146">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\<platform>\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="4108c-147">Além disso, para garantir que o recurso **[Editar modelo > Editar uma cópia](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funcione, você precisa incluir o `Generic.xaml` e os dicionários de recursos que ele mescla na pasta `<AssemblyName>\Themes`.</span><span class="sxs-lookup"><span data-stu-id="4108c-147">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<AssemblyName>\Themes` folder.</span></span> <span data-ttu-id="4108c-148">(Este arquivo não tem nenhum impacto sobre o comportamento de tempo de execução de um controle.)</span><span class="sxs-lookup"><span data-stu-id="4108c-148">(This file has no impact on the runtime behavior of a control.)</span></span>

    \build
    \lib
      \uap10.0.14393.0
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml
    \tools

> [!Note]
> <span data-ttu-id="4108c-149">Por padrão, as propriedades de controle aparecerão na categoria Diversos na Inspeção de propriedade.</span><span class="sxs-lookup"><span data-stu-id="4108c-149">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="4108c-150">Usar cadeias de caracteres e recursos</span><span class="sxs-lookup"><span data-stu-id="4108c-150">Use strings and resources</span></span>

<span data-ttu-id="4108c-151">Você pode inserir recursos de cadeia de caracteres (`.resw`) no pacote, as quais podem ser usadas pelo controle ou o projeto UWP consumidor, defina a propriedade **Ação de Build** do arquivo `.resw` para **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="4108c-151">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="4108c-152">Para obter um exemplo, consulte [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) no exemplo ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="4108c-152">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

## <a name="package-content-such-as-images"></a><span data-ttu-id="4108c-153">Conteúdo do pacote como imagens</span><span class="sxs-lookup"><span data-stu-id="4108c-153">Package content such as images</span></span>

<span data-ttu-id="4108c-154">Para conteúdo do pacote, como imagens que podem ser usadas por seu controle ou o projeto UWP consumidor.</span><span class="sxs-lookup"><span data-stu-id="4108c-154">To package content such as images that can be used by your control or the consuming UWP project.</span></span> <span data-ttu-id="4108c-155">adicione esses arquivos à pasta `lib\uap10.0.14393.0` da seguinte maneira (“your_assembly_name” deve corresponder novamente ao seu controle específico):</span><span class="sxs-lookup"><span data-stu-id="4108c-155">add those files `lib\uap10.0.14393.0` folder as follows ("your_assembly_name" should again match your particular control):</span></span>

    \build
    \lib
      \uap10.0.14393.0
        \Design
          \your_assembly_name
    \contosoSampleImage.jpg
    \tools

<span data-ttu-id="4108c-156">Você também pode criar um [arquivo de destino do MSBuild](/visualstudio/msbuild/msbuild-targets) para garantir que o ativo seja copiado para a pasta de saída do projeto consumidor:</span><span class="sxs-lookup"><span data-stu-id="4108c-156">You may also author an[MSBuild targets file](/visualstudio/msbuild/msbuild-targets) to ensure the asset is copied to the consuming project’s output folder:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0.14393.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a><span data-ttu-id="4108c-157">Consulte também</span><span class="sxs-lookup"><span data-stu-id="4108c-157">See also</span></span>

- [<span data-ttu-id="4108c-158">Criar Pacotes UWP</span><span class="sxs-lookup"><span data-stu-id="4108c-158">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="4108c-159">Exemplo de ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="4108c-159">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)