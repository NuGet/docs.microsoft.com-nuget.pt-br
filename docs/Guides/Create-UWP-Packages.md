---
title: Criar pacotes do NuGet para a Plataforma Universal do Windows | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/21/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Uma explicação passo a passo de ponta a ponta da criação de pacotes do NuGet usando um componente do Tempo de Execução do Windows para a Plataforma Universal do Windows."
keywords: criar um pacote, pacotes para UWP, Componentes do Windows Runtime
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: af650b6cd67855a67d0f49cdbd9f510bf90a60f6
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="create-uwp-packages"></a>Criar pacotes UWP

A [UWP (Plataforma Universal do Windows)](https://developer.microsoft.com/windows) fornece uma plataforma de aplicativo comum para todos os dispositivos que são executados no Windows 10. Nesse modelo, os aplicativos UWP podem chamar APIs do WinRT que são comuns a todos os dispositivos e APIs (incluindo Win32 e .NET) que são específicas para a família do dispositivo no qual o aplicativo está em execução.

Neste passo a passo, você cria um pacote NuGet com um componente UWP nativo (incluindo um controle XAML) que pode ser usado em projetos nativos e gerenciados.

## <a name="prerequisites"></a>Pré-requisitos

1. Visual Studio 2017 ou 2015. Instale a edição Community 2017 gratuitamente no [visualstudio.com](https://www.visualstudio.com/); você também pode usar as edições Professional e Enterprise.

1. CLI do NuGet. Baixe a versão mais recente do `nuget.exe` de [nuget.org/downloads](https://nuget.org/downloads) e salve-a em um local de sua escolha (o download é o `.exe` diretamente). Em seguida, adicione tal local à sua variável de ambiente PATH, se ainda não tiver feito isso.

## <a name="create-a-uwp-windows-runtime-component"></a>Criar um componente do Tempo de Execução do Windows da UWP

1. No Visual Studio, escolha **Arquivo > Novo > Projeto**, expanda o nó **Visual C++ > Windows > Universal**, selecione o modelo **Componente do Tempo de Execução do Windows (Universal do Windows)**, altere o nome para ImageEnhancer e clique em OK. Aceite os valores padrão para a Versão de Destino e a Versão Mínima quando solicitado.

    ![Criar um projeto de componente do Tempo de Execução do Windows UWP](media/UWP-NewProject.png)

1. Clique com botão direito do mouse no projeto no Gerenciador de Soluções, selecione **Adicionar > Novo Item**, clique no nó **Visual C++ > XAML**, selecione **Controle modelo**, altere o nome para AwesomeImageControl.cpp e clique em **Adicionar**:

    ![Adicionar um novo item de Controle Modelo XAML ao projeto](media/UWP-NewXAMLControl.png)

1. Clique com o botão direito do mouse no projeto no Gerenciador de Soluções e selecione **Propriedades**. Na página Propriedades, expanda **Propriedades de configuração > C/C++** e clique em **Arquivos de saída**. No painel à direita, altere o valor para **Gerar arquivos de documentação XML** para Sim:

    ![Definindo a geração de arquivos de documentação XML para Sim](media/UWP-GenerateXMLDocFiles.png)

1. Clique com botão direito do mouse na *solução* agora, selecione **Build em Lotes** e marque as três caixas de Depuração na caixa de diálogo, conforme mostrado abaixo. Isso garante que, quando você fizer uma compilação, gerará um conjunto completo de artefatos para cada um dos sistemas de destino com os quais o Windows é compatível.

    ![Build em Lotes](media/UWP-BatchBuild.png)

1. Na caixa de diálogo Compilação em Lotes, clique em **Compilar** para confirmar o projeto e criar os arquivos de saída que você precisa para o pacote NuGet.

> [!Note]
> Neste passo a passo, você usará os artefatos de Depuração para o pacote. Para o pacote sem depuração, marque as opções de Versão na caixa de diálogo de Build em Lotes e consulte as pastas de Versão resultantes nas etapas a seguir.

## <a name="create-and-update-the-nuspec-file"></a>Criar e atualizar o arquivo .nuspec

Para criar o arquivo `.nuspec` inicial, execute as três etapas abaixo. As seções a seguir, em seguida, guiarão você pelas outras atualizações necessárias.

1. Abra um prompt de comando e navegue até a pasta que contém `ImageEnhancer.vcxproj` (essa será uma subpasta abaixo onde está o arquivo da solução).
1. Execute o comando `spec` do NuGet para gerar `ImageEnhancer.nuspec` (o nome do arquivo é obtido do nome do arquivo `.vcxproj`):

    ```cli
    nuget spec
    ```

1. Abra o `ImageEnhancer.nuspec` em um editor e atualize-o para corresponder ao seguinte, substituindo YOUR_NAME por um valor apropriado. O valor `<id>`, especificamente, precisa ser exclusivo no nuget.org (consulte as convenções de nomenclatura descritas em [Criando um pacote](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)). Observe que você também precisa atualizar as marcas de autor e descrição ou um erro é mostrado durante a etapa de empacotamento.

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
> Para pacotes compilados para consumo público, preste atenção especial ao elemento `<tags>`, visto que essas marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.

### <a name="adding-windows-metadata-to-the-package"></a>Adicionar metadados do Windows ao pacote

Um componente do Tempo de Execução do Windows requer metadados que descrevem todos os seus tipos disponíveis publicamente, o que possibilita outros aplicativos e bibliotecas a consumirem o componente. Esses metadados estão contidos em um arquivo .winmd, que é criado quando você compila o projeto e precisa ser incluído em seu pacote do NuGet. Um arquivo XML com os dados do IntelliSense também é criado ao mesmo tempo e também deve ser incluído.

Adicione o nó `<files>` a seguir ao arquivo `.nuspec`:

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

No seu componente, a lógica principal do tipo ImageEnhancer está no código nativo, que está contido nos vários assemblies `ImageEnhancer.dll` que são gerados para cada tempo de execução de destino(ARM, x86 e x64). Para incluí-los no pacote, faça referência a eles na seção `<files>` juntamente com seus arquivos de recurso .pri associado:

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

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a>Adicionar .targets

Em seguida, projetos C++ e JavaScript que podem consumir seu pacote do NuGet precisam de um arquivo .targets para identificar os arquivos de assembly e winmd necessários. (Projetos C# e Visual Basic fazem isso automaticamente.) Crie esse arquivo copiando o texto abaixo em `ImageEnhancer.targets` e salve-o na mesma pasta que o arquivo `.nuspec`. _Observação_: esse arquivo `.targets` precisa ter o mesmo nome que a ID do pacote (por exemplo, o elemento `<Id>` no arquivo `.nupspec`):

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

Em seguida, consulte `ImageEnhancer.targets` no seu arquivo `.nuspec`:

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
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a>Empacotar o componente

Depois do `.nuspec` terminar de referenciar todos os arquivos que você precisa incluir no pacote, você estará pronto para executar o comando `pack`:

```cli
nuget pack ImageEnhancer.nuspec
```

Isso gera `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`. Ao abrir este arquivo em uma ferramenta como o [Explorador de Pacotes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) e expandir todos os nós, você verá o seguinte conteúdo:

![O Explorador de Pacotes do NuGet mostrando o pacote ImageEnhancer](media/UWP-PackageExplorer.png)

> [!Tip]
> O arquivo `.nupkg` é apenas um arquivo ZIP com uma extensão diferente. Também é possível examinar o conteúdo do pacote alterando `.nupkg` para `.zip`, mas lembre-se de restaurar a extensão antes de carregar um pacote para o nuget.org.

Para disponibilizar seu pacote para outros desenvolvedores, siga as instruções em [Publicar um pacote](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>Tópicos relacionados

- [Referência do .nuspec](../reference/nuspec.md)
- [Pacotes de símbolo](../create-packages/symbol-packages.md)
- [Controle de versão do pacote](../reference/package-versioning.md)
- [Suporte a Várias Versões do .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Incluir objetivos e destinos de MSBuild em um pacote](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Criando Pacotes Localizados](../create-packages/creating-localized-packages.md)
