---
title: Como empacotar controles UWP com o NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/14/2018
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: Como criar pacotes do NuGet que contêm controles UWP, incluindo os metadados e os arquivos de suporte necessários para os designers do Visual Studio e do Blend.
keywords: Controles UWP do NuGet, designer XAML do Visual Studio, designer do Blend, controles personalizados
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f024fd1823c77d57d30c4f841bf03494194c8339
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a>Criando controles UWP como pacotes do NuGet

Com o Visual Studio 2017, você pode aproveitar os recursos adicionados para os controles UWP que você fornecer em pacotes do NuGet. Este guia orientará você quanto a esses recursos usando o [exemplo ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). 

## <a name="prerequisites"></a>Pré-requisitos

1. Visual Studio 2017
1. Noções básicas sobre como [Criar pacotes UWP](create-uwp-packages.md)

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Adicionar suporte para o painel da caixa de ferramentas/ativos a controles XAML

Para que um controle XAML apareça na caixa de ferramentas do designer XAML no Visual Studio e no painel de Ativos do Blend, crie um arquivo `VisualStudioToolsManifest.xml` na raiz da pasta `tools` do seu projeto de pacote. Esse arquivo não é necessário se você não precisar que o controle apareça na caixa de ferramentas ou no painel Ativos.

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

A estrutura do arquivo é a seguinte:

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

em que:

- *your_package_file*: o nome do arquivo do seu controle, como `ManagedPackage.winmd` (“ManagedPackage” é um nome arbitrário usado para este exemplo e não tem nenhum outro significado).
- *vs_category*: o rótulo para o grupo no qual o controle deve aparecer na caixa de ferramentas do designer do Visual Studio. Um `VSCategory` é necessário para o controle apareça na caixa de ferramentas.
- *blend_category*: o rótulo para o grupo no qual o controle deve aparecer no painel Ativos do designer do Blend. Um `BlendCategory` é necessário para o controle apareça em Ativos.
- *type_full_name_n*: o nome totalmente qualificado para cada controle, incluindo o namespace, como `ManagedPackage.MyCustomControl`. Observe que o formato de ponto é usado tanto para tipos gerenciados quanto para tipos nativos.

Em cenários mais avançados, também é possível incluir vários elementos `<File>` dentro de `<FileList>` quando um único pacote contém vários assemblies de controle. Também é possível ter vários nós `<ToolboxItems>` dentro de um único `<File>` se você quiser organizar os controles em categorias separadas.

No exemplo a seguir, o controle implementado em `ManagedPackage.winmd` aparecerá no Visual Studio e no Blend em um grupo denominado “Managed Package” e “MyCustomControl” será exibido nesse grupo. Todos esses nomes são arbitrários.

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
> Você precisa especificar explicitamente cada controle deve ser exibido no painel de caixa de ferramentas/ativos. Verifique se você os especificou no formato `Namespace.ControlName`.

## <a name="add-custom-icons-to-your-controls"></a>Adicionar ícones personalizados aos seus controles

Para exibir um ícone personalizado no painel de caixa de ferramentas/ativos, adicione uma imagem ao seu projeto ou ao projeto `design.dll` correspondente com o nome “Namespace.ControlName.extension” e defina a ação de build como “Recurso Inserido”. Os formatos compatíveis são `.png`, `.jpg`, `.jpeg`, `.gif` e `.bmp`. O tamanho da imagem recomendado é 64 pixels por 64 pixels.

No exemplo a seguir, o projeto contém um arquivo de imagem denominado “ManagedPackage.MyCustomControl.png”.

![Definir um ícone personalizado em um projeto](media/UWP-control-custom-icon.png)

> [!Note]
> Para controles nativos, você deve colocar o ícone como um recurso do projeto `design.dll`.

## <a name="support-specific-windows-platform-versions"></a>Suporte a versões específicas de plataformas Windows

Pacotes UWP têm um TPV (TargetPlatformVersion) e TPMinV (TargetPlatformMinVersion) que definem os limites superior e inferior da versão do sistema operacional em que o aplicativo pode ser instalado. O TPV especifica ainda a versão do SDK na qual o aplicativo é compilado. Preste atenção a essas propriedades ao criar um pacote UWP: usar APIs fora dos limites das versões de plataforma definidas no aplicativo fará com que a compilação falhe ou o aplicativo falhe no tempo de execução.

Por exemplo, digamos que você definiu o TPMinV para o pacote de controles para o Windows 10 Anniversary Edition (10.0; Build 14393), por isso pode ser útil garantir que o pacote seja consumido somente por projetos UWP que correspondem ao limite inferior. Para permitir que o pacote seja consumido por projetos UWP você precisa empacotar os controles com os seguintes nomes de pasta:

    \lib\uap10.0\*
    \ref\uap10.0\*

Para impor a verificação de TPMinV apropriada, crie um [arquivo de destino do MSBuild](/visualstudio/msbuild/msbuild-targets) e empacote-o em `build\uap10.0" folder as `<nome_do_assembly>.targets`, replacing `<nome_do_assembly>` com o nome do assembly específico.

Veja este exemplo de como o arquivo de destino deve parecer:

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

## <a name="add-design-time-support"></a>Adicionar suporte no tempo de design

Para configurar onde as propriedades do controle aparecem na Inspeção de propriedade, adicionar adornos personalizados, etc., coloque o arquivo `design.dll` dentro da pasta `lib\uap10.0\Design` conforme apropriado para a plataforma de destino. Além disso, para garantir que o recurso **[Editar Modelo > Editar uma Cópia](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funcione, você precisará incluir o `Generic.xaml` e os dicionários de recursos aos quais ele é mesclado na pasta `<your_assembly_name>\Themes` (novamente, usando o nome real do assembly). (Este arquivo não tem nenhum impacto sobre o comportamento de tempo de execução de um controle.) A estrutura de pastas, portanto, seria exibida da seguinte maneira:

    \lib
      \uap10.0
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> Por padrão, as propriedades de controle aparecerão na categoria Diversos na Inspeção de propriedade.

## <a name="use-strings-and-resources"></a>Usar cadeias de caracteres e recursos

Você pode inserir recursos de cadeia de caracteres (`.resw`) no pacote, as quais podem ser usadas pelo controle ou o projeto UWP consumidor, defina a propriedade **Ação de Build** do arquivo `.resw` para **PRIResource**.

Para obter um exemplo, consulte [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) no exemplo ExtensionSDKasNuGetPackage.

## <a name="package-content-such-as-images"></a>Conteúdo do pacote como imagens

Para conteúdo do pacote como imagens que podem ser usadas para controle ou o projeto do UWP de consumidor, coloque os arquivos na pasta `lib\uap10.0`.

Você também pode criar um [arquivo de destino do MSBuild](/visualstudio/msbuild/msbuild-targets) para assegurar que o ativo seja copiado para a pasta de saída do projeto consumidor:

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

## <a name="see-also"></a>Consulte também

- [Criar Pacotes UWP](create-uwp-packages.md)
- [Exemplo de ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
