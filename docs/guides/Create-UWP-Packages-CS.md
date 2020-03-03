---
title: Criar pacotes do NuGet para a Plataforma Universal do Windows
description: Uma explicação de ponta a ponta da criação de pacotes NuGet usando um componente Windows Runtime para o Plataforma Universal do Windows no C#.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231801"
---
# <a name="create-uwp-packages-c"></a>Criar pacotes UWP (C#)

A [UWP (Plataforma Universal do Windows)](/windows/uwp) fornece uma plataforma de aplicativo comum para todos os dispositivos que são executados no Windows 10. Nesse modelo, os aplicativos UWP podem chamar APIs do WinRT que são comuns a todos os dispositivos e APIs (incluindo Win32 e .NET) que são específicas para a família do dispositivo no qual o aplicativo está em execução.

Neste tutorial, você cria um pacote NuGet com um C# componente UWP (incluindo um controle XAML) que pode ser usado em projetos gerenciados e nativos.

## <a name="prerequisites"></a>Prerequisites

1. Visual Studio 2019. Instale o 2019 Community Edition gratuitamente do [VisualStudio.com](https://www.visualstudio.com/); Você também pode usar as edições Professional e Enterprise.

1. CLI do NuGet. Baixe a versão mais recente do `nuget.exe` de [nuget.org/downloads](https://nuget.org/downloads) e salve-a em um local de sua escolha (o download é o `.exe` diretamente). Em seguida, adicione tal local à sua variável de ambiente PATH, se ainda não tiver feito isso. [Mais detalhes](/nuget/reference/nuget-exe-cli-reference#windows).

## <a name="create-a-uwp-windows-runtime-component"></a>Criar um componente do Windows Runtime da UWP

1. No Visual Studio, escolha **arquivo > novo projeto de >**, pesquise "UWP c#", selecione o modelo **componente do Windows Runtime (universal do Windows)** , clique em avançar, altere o nome para ImageEnhancer e clique em criar. Aceite os valores padrão para a Versão de Destino e a Versão Mínima quando solicitado.

    ![Criar um projeto de componente do Windows Runtime UWP](media/UWP-NewProject-CS.png)

1. Clique com o botão direito do mouse no projeto em Gerenciador de Soluções, selecione **adicionar > novo item**, selecione **controle modelo**, altere o nome para AwesomeImageControl.cs e clique em **Adicionar**:

    ![Adicionar um novo item de Controle Modelo XAML ao projeto](media/UWP-NewXAMLControl-CS.png)

1. Clique com o botão direito do mouse no projeto no Gerenciador de Soluções e selecione **Propriedades**. Na página Propriedades, escolha a guia **Compilar** e habilite o **arquivo de documentação XML**:

    ![Definindo a geração de arquivos de documentação XML para Sim](media/UWP-GenerateXMLDocFiles-CS.png)

1. Clique com o botão direito do mouse na *solução* agora, selecione **Build do lote**, marque as cinco caixas de Build na caixa de diálogo, conforme mostrado abaixo. Isso garante que, quando você fizer uma compilação, gerará um conjunto completo de artefatos para cada um dos sistemas de destino com os quais o Windows é compatível.

    ![Build em Lotes](media/UWP-BatchBuild-CS.png)

1. Na caixa de diálogo Compilação em Lotes, clique em **Compilar** para confirmar o projeto e criar os arquivos de saída que você precisa para o pacote NuGet.

> [!Note]
> Neste passo a passo, você usará os artefatos de Depuração para o pacote. Para o pacote sem depuração, marque as opções de Versão na caixa de diálogo de Build em Lotes e consulte as pastas de Versão resultantes nas etapas a seguir.

## <a name="create-and-update-the-nuspec-file"></a>Criar e atualizar o arquivo .nuspec

Para criar o arquivo `.nuspec` inicial, execute as três etapas abaixo. As seções a seguir, em seguida, guiarão você pelas outras atualizações necessárias.

1. Abra um prompt de comando e navegue até a pasta que contém `ImageEnhancer.csproj` (essa será uma subpasta abaixo onde está o arquivo da solução).
1. Execute o comando [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) para gerar `ImageEnhancer.nuspec` (o nome do arquivo é obtido do nome do arquivo `.csroj`):

    ```cli
    nuget spec
    ```

1. Abra o `ImageEnhancer.nuspec` em um editor e atualize-o para corresponder ao seguinte, substituindo YOUR_NAME por um valor apropriado. Não deixe nenhum dos $propertyName valores $. O valor `<id>`, especificamente, precisa ser exclusivo no nuget.org (consulte as convenções de nomenclatura descritas em [Criando um pacote](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). Observe que você também precisa atualizar as marcas de autor e descrição ou um erro é mostrado durante a etapa de empacotamento.

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
> Para pacotes compilados para consumo público, preste atenção especial ao elemento `<tags>`, visto que essas marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.

### <a name="adding-windows-metadata-to-the-package"></a>Adicionar metadados do Windows ao pacote

Um componente do Windows Runtime requer metadados que descrevem todos os seus tipos disponíveis publicamente, o que possibilita outros aplicativos e bibliotecas a consumirem o componente. Esses metadados estão contidos em um arquivo .winmd, que é criado quando você compila o projeto e precisa ser incluído em seu pacote do NuGet. Um arquivo XML com os dados do IntelliSense também é criado ao mesmo tempo e também deve ser incluído.

Adicione o nó `<files>` a seguir ao arquivo `.nuspec`:

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

### <a name="adding-xaml-content"></a>Adicionar conteúdo XAML

Para incluir um controle XAML no seu componente, você precisa adicionar o arquivo XAML que tem o modelo padrão para o controle (conforme gerado pelo modelo de projeto). Isso também vai para a seção `<files>`:

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

### <a name="adding-the-native-implementation-libraries"></a>Adicionar as bibliotecas de implementação nativa

Dentro de seu componente, a lógica principal do tipo ImageEnhancer está no código nativo, que está contido nos vários assemblies `ImageEnhancer.winmd` que são gerados para cada tempo de execução de destino (ARM, ARM64, x86 e x64). Para incluí-los no pacote, faça referência a eles na seção `<files>` juntamente com seus arquivos de recurso .pri associado:

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

### <a name="final-nuspec"></a>.nuspec final

O arquivo `.nuspec` final agora deve ser semelhante ao seguinte, em que novamente YOUR_NAME deve ser substituído por um valor apropriado:

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

## <a name="package-the-component"></a>Empacotar o componente

Com o `.nuspec` concluído referenciando todos os arquivos que você precisa incluir no pacote, você está pronto para executar o comando [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) :

```cli
nuget pack ImageEnhancer.nuspec
```

Isso gera `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Ao abrir este arquivo em uma ferramenta como o [Explorador de Pacotes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) e expandir todos os nós, você verá o seguinte conteúdo:

![O Explorador de Pacotes do NuGet mostrando o pacote ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> O arquivo `.nupkg` é apenas um arquivo ZIP com uma extensão diferente. Também é possível examinar o conteúdo do pacote alterando `.nupkg` para `.zip`, mas lembre-se de restaurar a extensão antes de carregar um pacote para o nuget.org.

Para disponibilizar seu pacote para outros desenvolvedores, siga as instruções em [Publicar um pacote](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Tópicos relacionados

- [Referência do .nuspec](../reference/nuspec.md)
- [Pacotes de símbolo](../create-packages/symbol-packages-snupkg.md)
- [Controle de versão do pacote](../concepts/package-versioning.md)
- [Suporte a Várias Versões do .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Incluir objetivos e destinos de MSBuild em um pacote](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Criando pacotes localizados](../create-packages/creating-localized-packages.md)
