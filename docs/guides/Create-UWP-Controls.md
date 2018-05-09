---
title: Como empacotar os controles da UWP com o NuGet
description: Como criar pacotes do NuGet que contêm controles UWP, incluindo os metadados e os arquivos de suporte necessários para os designers do Visual Studio e do Blend.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/14/2018
ms.topic: tutorial
ms.openlocfilehash: 963846e857c8757176e4fbe1cd60c92a7397ba01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a><span data-ttu-id="bb617-103">Criando controles UWP como pacotes do NuGet</span><span class="sxs-lookup"><span data-stu-id="bb617-103">Creating UWP controls as NuGet packages</span></span>

<span data-ttu-id="bb617-104">Com o Visual Studio 2017, você pode aproveitar os recursos adicionados para os controles UWP que você fornecer em pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="bb617-104">With Visual Studio 2017, you can take advantage of added capabilities for UWP controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="bb617-105">Este guia orientará você quanto a esses recursos usando o [exemplo ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="bb617-105">This guide walks you through these capabilities using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bb617-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bb617-106">Prerequisites</span></span>

1. <span data-ttu-id="bb617-107">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="bb617-107">Visual Studio 2017</span></span>
1. <span data-ttu-id="bb617-108">Noções básicas sobre como [Criar pacotes UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="bb617-108">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="bb617-109">Adicionar suporte para o painel da caixa de ferramentas/ativos a controles XAML</span><span class="sxs-lookup"><span data-stu-id="bb617-109">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="bb617-110">Para que um controle XAML apareça na caixa de ferramentas do designer XAML no Visual Studio e no painel de Ativos do Blend, crie um arquivo `VisualStudioToolsManifest.xml` na raiz da pasta `tools` do seu projeto de pacote.</span><span class="sxs-lookup"><span data-stu-id="bb617-110">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="bb617-111">Esse arquivo não é necessário se você não precisar que o controle apareça na caixa de ferramentas ou no painel Ativos.</span><span class="sxs-lookup"><span data-stu-id="bb617-111">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="bb617-112">A estrutura do arquivo é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="bb617-112">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="bb617-113">em que:</span><span class="sxs-lookup"><span data-stu-id="bb617-113">where:</span></span>

- <span data-ttu-id="bb617-114">*your_package_file*: o nome do arquivo do seu controle, como `ManagedPackage.winmd` (“ManagedPackage” é um nome arbitrário usado para este exemplo e não tem nenhum outro significado).</span><span class="sxs-lookup"><span data-stu-id="bb617-114">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="bb617-115">*vs_category*: o rótulo para o grupo no qual o controle deve aparecer na caixa de ferramentas do designer do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb617-115">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="bb617-116">Um `VSCategory` é necessário para o controle apareça na caixa de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="bb617-116">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="bb617-117">*blend_category*: o rótulo para o grupo no qual o controle deve aparecer no painel Ativos do designer do Blend.</span><span class="sxs-lookup"><span data-stu-id="bb617-117">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="bb617-118">Um `BlendCategory` é necessário para o controle apareça em Ativos.</span><span class="sxs-lookup"><span data-stu-id="bb617-118">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="bb617-119">*type_full_name_n*: o nome totalmente qualificado para cada controle, incluindo o namespace, como `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="bb617-119">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="bb617-120">Observe que o formato de ponto é usado tanto para tipos gerenciados quanto para tipos nativos.</span><span class="sxs-lookup"><span data-stu-id="bb617-120">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="bb617-121">Em cenários mais avançados, também é possível incluir vários elementos `<File>` dentro de `<FileList>` quando um único pacote contém vários assemblies de controle.</span><span class="sxs-lookup"><span data-stu-id="bb617-121">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="bb617-122">Também é possível ter vários nós `<ToolboxItems>` dentro de um único `<File>` se você quiser organizar os controles em categorias separadas.</span><span class="sxs-lookup"><span data-stu-id="bb617-122">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="bb617-123">No exemplo a seguir, o controle implementado em `ManagedPackage.winmd` aparecerá no Visual Studio e no Blend em um grupo denominado “Managed Package” e “MyCustomControl” será exibido nesse grupo.</span><span class="sxs-lookup"><span data-stu-id="bb617-123">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="bb617-124">Todos esses nomes são arbitrários.</span><span class="sxs-lookup"><span data-stu-id="bb617-124">All these names are arbitrary.</span></span>

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
> <span data-ttu-id="bb617-127">Você precisa especificar explicitamente cada controle deve ser exibido no painel de caixa de ferramentas/ativos.</span><span class="sxs-lookup"><span data-stu-id="bb617-127">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="bb617-128">Verifique se você os especificou no formato `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="bb617-128">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="bb617-129">Adicionar ícones personalizados aos seus controles</span><span class="sxs-lookup"><span data-stu-id="bb617-129">Add custom icons to your controls</span></span>

<span data-ttu-id="bb617-130">Para exibir um ícone personalizado no painel de caixa de ferramentas/ativos, adicione uma imagem ao seu projeto ou ao projeto `design.dll` correspondente com o nome “Namespace.ControlName.extension” e defina a ação de build como “Recurso Inserido”.</span><span class="sxs-lookup"><span data-stu-id="bb617-130">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="bb617-131">Os formatos compatíveis são `.png`, `.jpg`, `.jpeg`, `.gif` e `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="bb617-131">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="bb617-132">O tamanho da imagem recomendado é 64 pixels por 64 pixels.</span><span class="sxs-lookup"><span data-stu-id="bb617-132">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="bb617-133">No exemplo a seguir, o projeto contém um arquivo de imagem denominado “ManagedPackage.MyCustomControl.png”.</span><span class="sxs-lookup"><span data-stu-id="bb617-133">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Definir um ícone personalizado em um projeto](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="bb617-135">Para controles nativos, você deve colocar o ícone como um recurso do projeto `design.dll`.</span><span class="sxs-lookup"><span data-stu-id="bb617-135">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="bb617-136">Suporte a versões específicas de plataformas Windows</span><span class="sxs-lookup"><span data-stu-id="bb617-136">Support specific Windows platform versions</span></span>

<span data-ttu-id="bb617-137">Pacotes UWP têm um TPV (TargetPlatformVersion) e TPMinV (TargetPlatformMinVersion) que definem os limites superior e inferior da versão do sistema operacional em que o aplicativo pode ser instalado.</span><span class="sxs-lookup"><span data-stu-id="bb617-137">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="bb617-138">O TPV especifica ainda a versão do SDK na qual o aplicativo é compilado.</span><span class="sxs-lookup"><span data-stu-id="bb617-138">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="bb617-139">Preste atenção a essas propriedades ao criar um pacote UWP: usar APIs fora dos limites das versões de plataforma definidas no aplicativo fará com que a compilação falhe ou o aplicativo falhe no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="bb617-139">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="bb617-140">Por exemplo, digamos que você definiu o TPMinV para o pacote de controles para o Windows 10 Anniversary Edition (10.0; Build 14393), por isso pode ser útil garantir que o pacote seja consumido somente por projetos UWP que correspondem ao limite inferior.</span><span class="sxs-lookup"><span data-stu-id="bb617-140">For example, let’s say you’ve set the TPMinV for you controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="bb617-141">Para permitir que o pacote seja consumido por projetos UWP você precisa empacotar os controles com os seguintes nomes de pasta:</span><span class="sxs-lookup"><span data-stu-id="bb617-141">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0\*
    \ref\uap10.0\*

<span data-ttu-id="bb617-142">Para impor a verificação de TPMinV apropriada, crie um [arquivo de destino do MSBuild](/visualstudio/msbuild/msbuild-targets) e empacote-o em `build\uap10.0" folder as `<nome_do_assembly>.targets`, replacing `<nome_do_assembly>\` com o nome do assembly específico.</span><span class="sxs-lookup"><span data-stu-id="bb617-142">To enforce the appropriate TPMinV check, create an [MSBuild targets file](/visualstudio/msbuild/msbuild-targets) and package it under the `build\uap10.0" folder as `<your_assembly_name>.targets`, replacing `<your_assembly_name>\` with the name of your specific assembly.</span></span>

<span data-ttu-id="bb617-143">Veja este exemplo de como o arquivo de destino deve parecer:</span><span class="sxs-lookup"><span data-stu-id="bb617-143">Here is an example of what the targets file should look like:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="ResolveAssemblyReferences" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a><span data-ttu-id="bb617-144">Adicionar suporte no tempo de design</span><span class="sxs-lookup"><span data-stu-id="bb617-144">Add design-time support</span></span>

<span data-ttu-id="bb617-145">Para configurar onde as propriedades do controle aparecem na Inspeção de propriedade, adicionar adornos personalizados, etc., coloque o arquivo `design.dll` dentro da pasta `lib\uap10.0\Design` conforme apropriado para a plataforma de destino.</span><span class="sxs-lookup"><span data-stu-id="bb617-145">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="bb617-146">Além disso, para garantir que o recurso **[Editar Modelo > Editar uma Cópia](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funcione, você precisará incluir o `Generic.xaml` e os dicionários de recursos aos quais ele é mesclado na pasta `<your_assembly_name>\Themes` (novamente, usando o nome real do assembly).</span><span class="sxs-lookup"><span data-stu-id="bb617-146">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="bb617-147">(Este arquivo não tem nenhum impacto sobre o comportamento de tempo de execução de um controle.) A estrutura de pastas, portanto, seria exibida da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="bb617-147">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="bb617-148">Por padrão, as propriedades de controle aparecerão na categoria Diversos na Inspeção de propriedade.</span><span class="sxs-lookup"><span data-stu-id="bb617-148">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="bb617-149">Usar cadeias de caracteres e recursos</span><span class="sxs-lookup"><span data-stu-id="bb617-149">Use strings and resources</span></span>

<span data-ttu-id="bb617-150">Você pode inserir recursos de cadeia de caracteres (`.resw`) no pacote, as quais podem ser usadas pelo controle ou o projeto UWP consumidor, defina a propriedade **Ação de Build** do arquivo `.resw` para **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="bb617-150">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="bb617-151">Para obter um exemplo, consulte [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) no exemplo ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="bb617-151">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

## <a name="package-content-such-as-images"></a><span data-ttu-id="bb617-152">Conteúdo do pacote como imagens</span><span class="sxs-lookup"><span data-stu-id="bb617-152">Package content such as images</span></span>

<span data-ttu-id="bb617-153">Para conteúdo do pacote como imagens que podem ser usadas para controle ou o projeto do UWP de consumidor, coloque os arquivos na pasta `lib\uap10.0`.</span><span class="sxs-lookup"><span data-stu-id="bb617-153">To package content such as images that can be used by your control or the consuming UWP project, place those files within the `lib\uap10.0` folder.</span></span>

<span data-ttu-id="bb617-154">Você também pode criar um [arquivo de destino do MSBuild](/visualstudio/msbuild/msbuild-targets) para assegurar que o ativo seja copiado para a pasta de saída do projeto consumidor:</span><span class="sxs-lookup"><span data-stu-id="bb617-154">You may also author an [MSBuild targets file](/visualstudio/msbuild/msbuild-targets) to ensure the asset is copied to the consuming project’s output folder:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a><span data-ttu-id="bb617-155">Consulte também</span><span class="sxs-lookup"><span data-stu-id="bb617-155">See also</span></span>

- [<span data-ttu-id="bb617-156">Criar Pacotes UWP</span><span class="sxs-lookup"><span data-stu-id="bb617-156">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="bb617-157">Exemplo de ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="bb617-157">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
