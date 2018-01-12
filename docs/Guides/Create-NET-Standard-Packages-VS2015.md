---
title: Criar pacotes do NuGet do .NET Standard com o Visual Studio 2015 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: "Uma explicação passo a passo de ponta a ponta da criação de pacotes do NuGet do .NET Standard usando o NuGet 3.x e o Visual Studio 2015."
keywords: criar um pacote, pacotes do .NET Standard, tabela de mapeamento do .NET Standard
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e02888bf552997afe25e967f13e021e78e40d48d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a>Criar pacotes do .NET Standard com o Visual Studio 2015

*Aplica-se ao NuGet 3.x. Consulte [Criar pacotes do .NET Standard com o Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) para trabalhar com o NuGet 4.x ou superior.*

A [Biblioteca do .NET Standard](/dotnet/articles/standard/library) é uma especificação formal de APIs .NET que devem estar disponíveis em todos os tempos de execução do .NET, estabelecendo dessa forma uma maior uniformidade no ecossistema do .NET. A Biblioteca do .NET Standard define um conjunto uniforme de APIs de BCL (Biblioteca de Classes Base) para implementação em todas as plataformas do .NET, independentemente da carga de trabalho. Ele permite que os desenvolvedores produzam PCLs que podem ser usados em todos os tempos de execução do .NET e reduz ou elimina as diretivas de compilação condicional específicas da plataforma em código compartilhado.

Este guia orientará você durante a criação de um pacote do nuget direcionado para a Biblioteca do .NET Standard 1.4. Isso funcionará em .NET Framework 4.6.1, Plataforma Universal do Windows 10, .NET Core e Mono/Xamarin. Para obter detalhes, consulte a [tabela de mapeamento do .NET Standard](#net-standard-mapping-table) mais adiante neste tópico.

1. [Pré-requisitos](#pre-requisites)
1. [Criar o projeto da biblioteca de classes](#create-the-class-library-project)
1. [Criar e atualizar o arquivo .nuspec](#create-and-update-the-nuspec-file)
1. [Empacotar o componente](#package-the-component)
1. [Opções adicionais](#additional-options)
1. [Tabela de mapeamento do .NET Standard](#net-standard-mapping-table)
1. [Tópicos relacionados](#related-topics)


## <a name="pre-requisites"></a>Pré-requisitos

1. Visual Studio 2015. Instale a edição Community gratuitamente no [visualstudio.com](https://www.visualstudio.com/) e, claro, você também pode usar as edições Professional e Enterprise.
1. .NET Core: instale o .NET Core junto com modelos e outras ferramentas para o Visual Studio 2015 de [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).
1. CLI do NuGet. Baixe a versão mais recente do nuget.exe de [nuget.org/downloads](https://nuget.org/downloads) e salve-a em um local de sua escolha. Em seguida, adicione tal local à sua variável de ambiente PATH, se ainda não tiver feito isso.

> [!Note]
> O nuget.exe é a própria ferramenta CLI e não um instalador, por isso não se esqueça de salvar o arquivo baixado do navegador em vez de executá-lo.



## <a name="create-the-class-library-project"></a>Criar o projeto da biblioteca de classes

1. No Visual Studio, **Arquivo > Novo > Projeto**, expanda o nó **Visual C# > Windows**, selecione **Biblioteca de Classes (Portátil)**, altere o nome para AppLogger e clique em OK.

    ![Criar um novo projeto de biblioteca de classes](media/NetStandard-NewProject.png)

1. Na caixa de diálogo **Adicionar biblioteca de classes portátil** exibida, selecione as opções `.NET Framework 4.6` e `ASP.NET Core 1.0`.
1. Clique com o botão direito do mouse no `AppLogger (Portable)` no Gerenciador de Soluções, selecione **Propriedades**, escolha a guia **Biblioteca** e, em seguida, clique em **Destinado ao .NET Platform Standard** na seção **Direcionamento**. Isso solicitará a confirmação, quando então é possível selecionar `.NET Standard 1.4` na lista suspensa:

    ![Definir o destino como .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. Clique na guia **Build**, altere a **Configuração** para `Release` e marque a caixa para **Arquivo de documentação XML**.
1. Adicione seu código ao componente, como por exemplo:

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. Compile o projeto (com a configuração de Versão) e verifique se os arquivos DLL e XML são produzidos dentro da pasta bin\Release.

## <a name="create-and-update-the-nuspec-file"></a>Criar e atualizar o arquivo .nuspec

1. Abra um prompt de comando, navegue até a pasta que contém a pasta `AppLogg.csproj` (um nível abaixo de onde o arquivo `.sln` está) e execute o comando `spec` do NuGet para criar o arquivo `AppLogger.nuspec` inicial:

```
nuget spec
```

1. Abra o `AppLogger.nuspec` em um editor e atualize-o para corresponder ao seguinte, substituindo YOUR_NAME por um valor apropriado. O valor `<id>`, especificamente, precisa ser exclusivo no nuget.org (consulte as convenções de nomenclatura descritas em [Criando um pacote](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)). Observe que você também precisa atualizar as marcas de autor e descrição ou um erro será mostrado durante a etapa de empacotamento.

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>AppLogger.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>AppLogger</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. Adicionar assemblies de referência ao arquivo `.nuspec`, especificamente a DLL da biblioteca e o arquivo XML do IntelliSense:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. Clique com o botão direito do mouse na solução e selecione **Compilar solução** para gerar todos os arquivos de pacote.


## <a name="package-the-component"></a>Empacotar o componente

Depois do `.nuspec` terminar de referenciar todos os arquivos que você precisa incluir no pacote, você estará pronto para executar o comando `pack`:

```
nuget pack AppLogger.nuspec
```

Isso gerará `AppLogger.YOUR_NAME.1.0.0.nupkg`. Ao abrir este arquivo em uma ferramenta como o [Explorador de Pacotes do NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) e expandir todos os nós, você verá o seguinte conteúdo:

![O Explorador de Pacotes do NuGet mostrando o pacote AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> O arquivo `.nupkg` é apenas um arquivo ZIP com uma extensão diferente. Também é possível examinar o conteúdo do pacote alterando `.nupkg` para `.zip`, mas lembre-se de restaurar a extensão antes de carregar um pacote para o nuget.org.

Para disponibilizar seu pacote para outros desenvolvedores, siga as instruções em [Publicar um pacote](../create-packages/publish-a-package.md).

Observe que `pack` requer o Mono 4.4.2 no Mac OS X e não funciona em sistemas Linux. Em um Mac, você também precisa converter os nomes de caminho do Windows no arquivo `.nuspec` em caminhos no estilo Unix.

## <a name="additional-options"></a>Opções adicionais

As seções a seguir abordam opções adicionais para criação de pacotes do NuGet:

- [Declarando dependências](#declaring-dependencies)
- [Suporte a várias estruturas de destino](#supporting-multiple-target-frameworks)
- [Adicionar destinos e objetos ao MSBuild](#adding-targets-and-props-for-msbuild)
- [Criando pacotes localizados](#creating-localized-packages)
- [Adicionar um Leiame](#adding-a-readme)

### <a name="declaring-dependencies"></a>Declarando dependências

Se você tiver dependências em outros pacotes do NuGet, liste-os no elemento `<dependencies>` com elementos `<group>`. Por exemplo, para declarar uma dependência no NewtonSoft.Json 8.0.3 ou superior, adicione o seguinte:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

A sintaxe do atributo *version* aqui indica que a versão 8.0.3 ou superior é aceitável. Para especificar intervalos de versão diferentes, consulte [Controle de versão do pacote](../reference/package-versioning.md).

### <a name="supporting-multiple-target-frameworks"></a>Suporte a várias estruturas de destino

Suponha que você gostaria de aproveitar uma API no .NET Framework 4.6.2 não está disponível no .NET Standard 1.4. Para fazer isso, primeiro você precisará verificar se a biblioteca é compilada para o .NET 4.6.2 usando a compilação condicional ou projetos compartilhados. (No Visual Studio, você pode criar um projeto NetCore, adicionar a estrutura de sua escolha à seção de várias estruturas e, em seguida, compilar.) Em seguida, crie o pacote usando a técnica simples de diretório de trabalho baseado em convenção da seguinte maneira:

1. Na pasta raiz do projeto que contém seu arquivo `.nuspec`, crie uma pasta chamada `lib`.
1. Dentro de `lib`, crie pastas para cada plataforma às quais você deseja dar suporte:

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. No arquivo `.nuspec`, adicione um nó `files` sob o nó `package` e consulte os arquivos em `lib` usando curingas. **Observação:** substituições de Token não são compatíveis com a abordagem do diretório de trabalho baseado em convenção, portanto, substitua-as por valores literais:

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. Crie o pacote novamente usando `nuget pack AppLogger.spec`.

Para obter mais detalhes sobre como usar essa técnica, consulte [Suporte a várias versões do .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)

### <a name="adding-targets-and-props-for-msbuild"></a>Adicionar destinos e objetos ao MSBuild

Em alguns casos, convém adicionar destinos ou propriedades de build personalizados a projetos que consomem o pacote, como a execução de uma ferramenta personalizada ou um processo durante o build. Faça isso adicionando arquivos a uma pasta `\build` conforme descrito nas etapas abaixo. Quando o NuGet instala um pacote com arquivos \build, ele adiciona um elemento de MSBuild ao arquivo de projeto que aponta para arquivos .targets e .props.

> [!Note]
> Ao usar `project.json`, os destinos não são adicionados ao projeto, mas são disponibilizados por meio do `project.lock.json`.


1. Na pasta de projeto que contém seu arquivo `.nuspec`, crie uma pasta chamada `build`.
1. Dentro do `build`, crie pastas para cada um que for compatível e coloque nelas seus arquivos `.targets` e `.props`:

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. No arquivo `.nuspec`, adicione um nó `files` sob o nó `package` e consulte os arquivos em `build` usando curingas.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. Crie o pacote novamente usando `nuget pack AppLogger.nuspec`.

Para ver detalhes adicionais, consulte [Incluir objetos e destinos do MSBuild em um pacote](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).


### <a name="creating-localized-packages"></a>Criando pacotes localizados

Para criar versões localizadas da biblioteca, crie pacotes separados para localidades diferentes ou inclua assemblies de recursos localizados em um único pacote. Aqui está como realizar a segunda abordagem para alemão e italiano:

1. Dentro de cada pasta de estrutura de destino, em `lib`, crie pastas para cada idioma compatível além do inglês padrão. Nessas pastas, você pode colocar assemblies de recursos e arquivos XML do IntelliSense localizados. Por exemplo:

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. No arquivo `.nuspec`, faça referência desses arquivos no nó `<files>`:

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. Crie o pacote novamente usando `nuget pack AppLogger.nuspec`.


### <a name="adding-a-readme"></a>Adicionar um Leiame

Quando você inclui um arquivo `readme.txt` na raiz do pacote, o Visual Studio será exibido quando o pacote for instalado diretamente.

> [!Note]
> Os arquivos Leiame não são mostrados para pacotes que são instalados como uma dependência ou para projetos do .NET Core.


Para fazer isso, crie o arquivo `readme.txt`, coloque-o na pasta raiz do projeto e faça referência a ele no arquivo `.nuspec`:

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```


## <a name="net-standard-mapping-table"></a>Tabela de mapeamento do .NET Standard

|Nome da plataforma |Alias|
|--------------|-----|
|.NET Standard | netstandard| 1.0| 1.1| 1.2| 1.3| 1.4| 1.5| 1.6|
|.NET Core | netcoreapp| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| 1.0|
|.NET Framework| net| 4.5| 4.5.1| 4.6| 4.6.1| 4.6.2| 4.6.3|
|Plataformas Mono/Xamarin| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;|
|Plataforma Universal do Windows| uap| &#x2192;| &#x2192;| &#x2192;| &#x2192;|10.0|
|Windows| win| &#x2192;| 8.0| 8.1|
|Windows Phone| wpa| &#x2192;| &#x2192;|8.1|
|Windows Phone Silverlight| wp| 8.0|



## <a name="related-topics"></a>Tópicos relacionados

- [Referência de Nuspec](../schema/nuspec.md)
- [Pacotes de símbolo](../create-packages/symbol-packages.md)
- [Controle de versão do pacote](../reference/package-versioning.md)
- [Suporte a Várias Versões do .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Incluir objetivos e destinos de MSBuild em um pacote](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Criando Pacotes Localizados](../create-packages/creating-localized-packages.md)
- [Documentação da Biblioteca do .NET Standard](/dotnet/articles/standard/library)
- [Portabilidade para o .NET Core do .NET Framework](/dotnet/articles/core/porting/index)
