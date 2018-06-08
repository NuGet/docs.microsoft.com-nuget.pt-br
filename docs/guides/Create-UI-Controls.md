---
title: Como empacotar os controles da Interface do Usuário com o NuGet
description: Como criar pacotes do NuGet que contêm controles UWP ou WPF, incluindo os metadados e os arquivos de suporte necessários para os designers do Visual Studio e do Blend.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: ab7499c415f63319fd314f33607f74d400b5f957
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818651"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>Como criar controles de interface do usuário como pacotes do NuGet

Com o Visual Studio 2017, você pode aproveitar os recursos adicionados para os controles UWP e WPF que você fornecer em pacotes do NuGet. Este guia orientará você quanto a esses recursos no contexto dos controles UWP usando o [exemplo ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). O mesmo se aplica aos controles WPF, salvo indicação em contrário.

## <a name="prerequisites"></a>Pré-requisitos

1. Visual Studio 2017
1. Noções básicas sobre como [Criar pacotes UWP](create-uwp-packages.md)

## <a name="generate-library-layout"></a>Gerar Layout da Biblioteca

> [!Note]
> Isso só se aplica aos controles UWP.

Configurar a propriedade `GenerateLibraryLayout` garante que a saída de build do projeto é gerada em um layout que está pronto para ser empacotado, sem a necessidade de entradas de arquivos individuais no nuspec.

Nas propriedades do projeto, acesse a guia build e marque a caixa de seleção "Gerar Layout da Biblioteca". Isso modificará o arquivo de projeto e definirá o sinalizador `GenerateLibraryLayout` como verdadeiro para a plataforma e a configuração de build selecionadas no momento.

Como alternativa, edite o arquivo de projeto para adicionar `<GenerateLibraryLayout>true</GenerateLibraryLayout>` no primeiro grupo de propriedade incondicional. Isso aplicaria a propriedade independentemente da plataforma e da configuração de build.

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

Por exemplo, digamos que você tenha definido o TPMinV para o pacote de controles para o Windows 10 Anniversary Edition (10.0; Build 14393), por isso pode ser útil garantir que o pacote seja consumido somente por projetos UWP que correspondam ao limite inferior. Para permitir que o pacote seja consumido por projetos UWP você precisa empacotar os controles com os seguintes nomes de pasta:

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

O NuGet verificará automaticamente o TPMinV do projeto consumidor e falhará na instalação se for inferior ao Windows 10 Anniversary Edition (10.0; build 14393)

No caso do WPF, digamos que você queira que seu pacote de controles WPF seja consumido por projetos utilizando o .NET Framework v4.6.1 ou superior. Para impor isso, você deve empacotar os controles com os seguintes nomes de pastas:

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>Adicionar suporte no tempo de design

Para configurar onde as propriedades do controle aparecem na Inspeção de propriedade, adicionar adornos personalizados, etc., coloque o arquivo `design.dll` dentro da pasta `lib\uap10.0.14393\Design` conforme apropriado para a plataforma de destino. Além disso, para garantir que o recurso **[Editar Modelo > Editar uma Cópia](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** funcione, você precisará incluir o `Generic.xaml` e os dicionários de recursos aos quais ele é mesclado na pasta `<your_assembly_name>\Themes` (novamente, usando o nome real do assembly). (Este arquivo não tem nenhum impacto sobre o comportamento de tempo de execução de um controle.) A estrutura de pastas, portanto, seria exibida da seguinte maneira:

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


Para WPF, continuando com o exemplo em que você deseja que o pacote de controles WPF fosse consumido por projetos utilizando o .NET Framework v4.6.1 ou superior:

    \lib
      \net461
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

> [!Note]
> Isso só se aplica aos controles UWP.

## <a name="see-also"></a>Consulte também

- [Criar Pacotes UWP](create-uwp-packages.md)
- [Exemplo de ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
