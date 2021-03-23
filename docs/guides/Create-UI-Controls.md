---
title: Como empacotar os controles da Interface do Usuário com o NuGet
description: Como criar pacotes do NuGet que contêm controles UWP ou WPF, incluindo os metadados e os arquivos de suporte necessários para os designers do Visual Studio e do Blend.
author: JonDouglas
ms.author: jodou
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: 7660203ec44db75b7764767b519c9ff10dd1122e
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859077"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="aeb2c-103">Como criar controles de interface do usuário como pacotes do NuGet</span><span class="sxs-lookup"><span data-stu-id="aeb2c-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="aeb2c-104">No Visual Studio 2017 em diante, você pode aproveitar as funcionalidades adicionadas dos controles UWP e WPF entregues em pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-104">Starting with Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="aeb2c-105">Este guia orientará você quanto a esses recursos no contexto dos controles UWP usando o [exemplo ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/main/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="aeb2c-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/main/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="aeb2c-106">O mesmo se aplica aos controles WPF, salvo indicação em contrário.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aeb2c-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="aeb2c-107">Prerequisites</span></span>

1. <span data-ttu-id="aeb2c-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="aeb2c-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="aeb2c-109">Noções básicas sobre como [Criar pacotes UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="aeb2c-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="aeb2c-110">Gerar Layout da Biblioteca</span><span class="sxs-lookup"><span data-stu-id="aeb2c-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="aeb2c-111">Isso só se aplica aos controles UWP.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="aeb2c-112">Configurar a propriedade `GenerateLibraryLayout` garante que a saída de build do projeto é gerada em um layout que está pronto para ser empacotado, sem a necessidade de entradas de arquivos individuais no nuspec.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="aeb2c-113">Nas propriedades do projeto, acesse a guia build e marque a caixa de seleção "Gerar Layout da Biblioteca".</span><span class="sxs-lookup"><span data-stu-id="aeb2c-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="aeb2c-114">Isso modificará o arquivo de projeto e definirá o sinalizador `GenerateLibraryLayout` como verdadeiro para a plataforma e a configuração de build selecionadas no momento.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="aeb2c-115">Como alternativa, edite o arquivo de projeto para adicionar `<GenerateLibraryLayout>true</GenerateLibraryLayout>` no primeiro grupo de propriedade incondicional.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="aeb2c-116">Isso aplicaria a propriedade independentemente da plataforma e da configuração de build.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="aeb2c-117">Adicionar suporte para o painel da caixa de ferramentas/ativos a controles XAML</span><span class="sxs-lookup"><span data-stu-id="aeb2c-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="aeb2c-118">Para que um controle XAML apareça na caixa de ferramentas do designer XAML no Visual Studio e no painel de Ativos do Blend, crie um arquivo `VisualStudioToolsManifest.xml` na raiz da pasta `tools` do seu projeto de pacote.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="aeb2c-119">Esse arquivo não é necessário se você não precisar que o controle apareça na caixa de ferramentas ou no painel Ativos.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

```
\build
\lib
\tools
    VisualStudioToolsManifest.xml
```

<span data-ttu-id="aeb2c-120">A estrutura do arquivo é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="aeb2c-120">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems UIFramework="WPF" VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="aeb2c-121">em que:</span><span class="sxs-lookup"><span data-stu-id="aeb2c-121">where:</span></span>

- <span data-ttu-id="aeb2c-122">*your_package_file*: o nome do arquivo do seu controle, como `ManagedPackage.winmd` (“ManagedPackage” é um nome arbitrário usado para este exemplo e não tem nenhum outro significado).</span><span class="sxs-lookup"><span data-stu-id="aeb2c-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="aeb2c-123">*vs_category*: o rótulo para o grupo no qual o controle deve aparecer na caixa de ferramentas do designer do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="aeb2c-124">Um `VSCategory` é necessário para o controle apareça na caixa de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
<span data-ttu-id="aeb2c-125">*ui_framework*: o nome da estrutura, como ' WPF ', observe que `UIFramework` o atributo é necessário em nós ToolboxItems no Visual Studio 16,7 Preview 3 ou superior para que o controle apareça na caixa de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-125">*ui_framework*: The name of the Framework, such as 'WPF', note that `UIFramework` attribute is required on ToolboxItems nodes on Visual Studio 16.7 Preview 3 or above for the control to appear in toolbox.</span></span>
- <span data-ttu-id="aeb2c-126">*blend_category*: o rótulo para o grupo no qual o controle deve aparecer no painel Ativos do designer do Blend.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-126">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="aeb2c-127">Um `BlendCategory` é necessário para o controle apareça em Ativos.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-127">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="aeb2c-128">*type_full_name_n*: o nome totalmente qualificado para cada controle, incluindo o namespace, como `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-128">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="aeb2c-129">Observe que o formato de ponto é usado tanto para tipos gerenciados quanto para tipos nativos.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-129">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="aeb2c-130">Em cenários mais avançados, também é possível incluir vários elementos `<File>` dentro de `<FileList>` quando um único pacote contém vários assemblies de controle.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-130">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="aeb2c-131">Também é possível ter vários nós `<ToolboxItems>` dentro de um único `<File>` se você quiser organizar os controles em categorias separadas.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-131">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="aeb2c-132">No exemplo a seguir, o controle implementado em `ManagedPackage.winmd` aparecerá no Visual Studio e no Blend em um grupo denominado “Managed Package” e “MyCustomControl” será exibido nesse grupo.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-132">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="aeb2c-133">Todos esses nomes são arbitrários.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-133">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems UIFramework="WPF" VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Um controle de exemplo como ele aparece no Visual Studio](media/UWP-control-vs-toolbox.png)

![Um controle de exemplo como ele aparece no Blend](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="aeb2c-136">Você precisa especificar explicitamente cada controle deve ser exibido no painel de caixa de ferramentas/ativos.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-136">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="aeb2c-137">Verifique se você os especificou no formato `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-137">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="aeb2c-138">Adicionar ícones personalizados aos seus controles</span><span class="sxs-lookup"><span data-stu-id="aeb2c-138">Add custom icons to your controls</span></span>

<span data-ttu-id="aeb2c-139">Para exibir um ícone personalizado no painel de caixa de ferramentas/ativos, adicione uma imagem ao seu projeto ou ao projeto `design.dll` correspondente com o nome “Namespace.ControlName.extension” e defina a ação de build como “Recurso Inserido”.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-139">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="aeb2c-140">Você também deve garantir que o `AssemblyInfo.cs` associado especifique o atributo ProvideMetadata - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-140">You must also ensure that the associated `AssemblyInfo.cs` specifies the ProvideMetadata attribute - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span></span> <span data-ttu-id="aeb2c-141">Veja este [exemplo](https://github.com/NuGet/Samples/blob/main/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span><span class="sxs-lookup"><span data-stu-id="aeb2c-141">See this [sample](https://github.com/NuGet/Samples/blob/main/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span></span>

<span data-ttu-id="aeb2c-142">Os formatos compatíveis são `.png`, `.jpg`, `.jpeg`, `.gif` e `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-142">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="aeb2c-143">O formato recomendado é BMP24 em 16 x 16 pixels.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-143">The recommended format is BMP24 in 16 pixels by 16 pixels.</span></span>

![Exemplo de ícone da caixa de ferramentas](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

<span data-ttu-id="aeb2c-145">A tela de fundo rosa é substituída em runtime.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-145">The pink background is replaced at runtime.</span></span> <span data-ttu-id="aeb2c-146">Os ícones são recoloridos quando o tema do Visual Studio é alterado e essa cor da tela de fundo é esperada.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-146">The icons are recolored when the Visual Studio theme is changed and that background color is expected.</span></span> <span data-ttu-id="aeb2c-147">Para obter mais informações, veja [Imagens e ícones para o Visual Studio](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="aeb2c-147">For more information, please reference [Images and Icons for Visual Studio](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span></span>

<span data-ttu-id="aeb2c-148">No exemplo a seguir, o projeto contém um arquivo de imagem denominado “ManagedPackage.MyCustomControl.png”.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-148">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Definir um ícone personalizado em um projeto](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="aeb2c-150">Para controles nativos, você deve colocar o ícone como um recurso do projeto `design.dll`.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-150">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="aeb2c-151">Suporte a versões específicas de plataformas Windows</span><span class="sxs-lookup"><span data-stu-id="aeb2c-151">Support specific Windows platform versions</span></span>

<span data-ttu-id="aeb2c-152">Pacotes UWP têm um TPV (TargetPlatformVersion) e TPMinV (TargetPlatformMinVersion) que definem os limites superior e inferior da versão do sistema operacional em que o aplicativo pode ser instalado.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-152">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="aeb2c-153">O TPV especifica ainda a versão do SDK na qual o aplicativo é compilado.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-153">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="aeb2c-154">Preste atenção a essas propriedades ao criar um pacote UWP: usar APIs fora dos limites das versões de plataforma definidas no aplicativo fará com que a compilação falhe ou o aplicativo falhe no runtime.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-154">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="aeb2c-155">Por exemplo, digamos que você tenha definido o TPMinV para o pacote de controles para o Windows 10 Anniversary Edition (10.0; Build 14393), por isso pode ser útil garantir que o pacote seja consumido somente por projetos UWP que correspondam ao limite inferior.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-155">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="aeb2c-156">Para permitir que o pacote seja consumido por projetos UWP você precisa empacotar os controles com os seguintes nomes de pasta:</span><span class="sxs-lookup"><span data-stu-id="aeb2c-156">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

```
\lib\uap10.0.14393\*
\ref\uap10.0.14393\*
```

<span data-ttu-id="aeb2c-157">O NuGet verificará automaticamente o TPMinV do projeto consumidor e falhará na instalação se for inferior ao Windows 10 Anniversary Edition (10.0; build 14393)</span><span class="sxs-lookup"><span data-stu-id="aeb2c-157">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="aeb2c-158">No caso do WPF, digamos que você queira que seu pacote de controles WPF seja consumido por projetos utilizando o .NET Framework v4.6.1 ou superior.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-158">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="aeb2c-159">Para impor isso, você deve empacotar os controles com os seguintes nomes de pastas:</span><span class="sxs-lookup"><span data-stu-id="aeb2c-159">To enforce that, you must package your controls with the following folder names:</span></span>

```
\lib\net461\*
\ref\net461\*
```

## <a name="add-design-time-support"></a><span data-ttu-id="aeb2c-160">Adicionar suporte no tempo de design</span><span class="sxs-lookup"><span data-stu-id="aeb2c-160">Add design-time support</span></span>

<span data-ttu-id="aeb2c-161">Para configurar onde as propriedades do controle aparecem na Inspeção de propriedade, adicionar adornos personalizados, etc., coloque o arquivo `design.dll` dentro da pasta `lib\uap10.0.14393\Design` conforme apropriado para a plataforma de destino.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-161">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="aeb2c-162">Além disso, para garantir que o recurso **[Editar Modelo > Editar uma Cópia](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funcione, você precisará incluir o `Generic.xaml` e os dicionários de recursos aos quais ele é mesclado na pasta `<your_assembly_name>\Themes` (novamente, usando o nome real do assembly).</span><span class="sxs-lookup"><span data-stu-id="aeb2c-162">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="aeb2c-163">(Esse arquivo não tem impacto sobre o comportamento de tempo de execução de um controle.) A estrutura de pastas, portanto, seria exibida da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="aeb2c-163">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

```
\lib
  \uap10.0.14393
    \Design
      \MyControl.design.dll
    \your_assembly_name
      \Themes
        Generic.xaml
```

<span data-ttu-id="aeb2c-164">Para WPF, continuando com o exemplo em que você deseja que o pacote de controles WPF fosse consumido por projetos utilizando o .NET Framework v4.6.1 ou superior:</span><span class="sxs-lookup"><span data-stu-id="aeb2c-164">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

```
\lib
  \net461
    \Design
      \MyControl.design.dll
    \your_assembly_name
      \Themes
        Generic.xaml
```

> [!Note]
> <span data-ttu-id="aeb2c-165">Por padrão, as propriedades de controle aparecerão na categoria Diversos na Inspeção de propriedade.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-165">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="aeb2c-166">Usar cadeias de caracteres e recursos</span><span class="sxs-lookup"><span data-stu-id="aeb2c-166">Use strings and resources</span></span>

<span data-ttu-id="aeb2c-167">Você pode inserir recursos de cadeia de caracteres (`.resw`) no pacote, as quais podem ser usadas pelo controle ou o projeto UWP consumidor, defina a propriedade **Ação de Build** do arquivo `.resw` para **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-167">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="aeb2c-168">Para obter um exemplo, consulte [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/main/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) no exemplo ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-168">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/main/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="aeb2c-169">Isso só se aplica aos controles UWP.</span><span class="sxs-lookup"><span data-stu-id="aeb2c-169">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="aeb2c-170">Veja também</span><span class="sxs-lookup"><span data-stu-id="aeb2c-170">See also</span></span>

- [<span data-ttu-id="aeb2c-171">Criar Pacotes UWP</span><span class="sxs-lookup"><span data-stu-id="aeb2c-171">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="aeb2c-172">Exemplo de ExtensionSDKasNuGetPackage</span><span class="sxs-lookup"><span data-stu-id="aeb2c-172">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/main/ExtensionSDKasNuGetPackage)