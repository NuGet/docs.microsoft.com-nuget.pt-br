---
title: Criar pacotes NuGet para o Xamarin (para iOS, Android e Windows) com o Visual Studio 2017 ou 2019
description: Uma explicação passo a passo de ponta a ponta da criação de pacotes do NuGet para Xamarin que usam APIs nativas no iOS, Android e Windows.
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: fce3c9a92dfee325f9e914bf3d6444601fb38b6c
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385659"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a>Criar pacotes para o Xamarin com Visual Studio 2017 ou 2019

Um pacote para Xamarin contém código que usa APIs nativas no iOS, Android e Windows, dependendo do sistema operacional de tempo de execução. Embora seja simples fazer isso, é preferível para permitir que os desenvolvedores consumam o pacote de um PCL ou de bibliotecas do .NET Standard por meio de uma área de superfície de API comum.

Neste tutorial, você usa o Visual Studio 2017 ou 2019 para criar um pacote NuGet de plataforma cruzada que pode ser usado em projetos móveis no iOS, no Android e no Windows.

1. [Pré-requisitos](#prerequisites)
1. [Criar a estrutura do projeto e o código de abstração](#create-the-project-structure-and-abstraction-code)
1. [Escreva o código específico para sua plataforma](#write-your-platform-specific-code)
1. [Criar e atualizar o arquivo .nuspec](#create-and-update-the-nuspec-file)
1. [Empacotar o componente](#package-the-component)
1. [Tópicos relacionados](#related-topics)

## <a name="prerequisites"></a>{1&gt;{2&gt;Pré-requisitos&lt;2}&lt;1}

1. Visual Studio 2017 ou 2019 com Plataforma Universal do Windows (UWP) e Xamarin. Instale a edição Community gratuitamente no [visualstudio.com](https://www.visualstudio.com/) e, claro, você também pode usar as edições Professional e Enterprise. Para incluir as ferramentas UWP e Xamarin, selecione uma instalação Personalizada e verifique as opções apropriadas.
1. CLI do NuGet. Baixe a versão mais recente do nuget.exe de [nuget.org/downloads](https://nuget.org/downloads) e salve-a em um local de sua escolha. Em seguida, adicione tal local à sua variável de ambiente PATH, se ainda não tiver feito isso.

> [!Note]
> O nuget.exe é a própria ferramenta CLI e não um instalador, por isso não se esqueça de salvar o arquivo baixado do navegador em vez de executá-lo.

## <a name="create-the-project-structure-and-abstraction-code"></a>Criar a estrutura do projeto e o código de abstração

1. Baixe e execute a [extensão de modelos de plug-in de .net Standard de plataforma cruzada](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) para o Visual Studio. Esses modelos facilitarão a criação da estrutura de projeto necessária para este passo a passo.
1. No Visual Studio 2017, **arquivo > novo projeto de >** , procure `Plugin`, selecione o modelo de **plug-in biblioteca de .net Standard de plataforma cruzada** , altere o nome para LoggingLibrary e clique em OK.

    ![Novo projeto de aplicativo em branco (aplicativos Xamarin. Forms portátil) no VS 2017](media/CrossPlatform-NewProject.png)

    No Visual Studio 2019, **arquivo > novo > projeto**, procure `Plugin`, selecione o modelo de **plug-in biblioteca de .net Standard de plataforma cruzada** e clique em Avançar.

    ![Novo projeto de aplicativo em branco (aplicativos Xamarin. Forms portátil) no VS 2019](media/CrossPlatform-NewProject19-Part1.png)

    Altere o nome para LoggingLibrary e clique em criar.

    ![Nova configuração de aplicativo em branco (aplicativos Xamarin. Forms portáteis) no VS 2019](media/CrossPlatform-NewProject19-Part2.png)

A solução resultante contém dois projetos compartilhados, juntamente com uma variedade de projetos específicos da plataforma:

- O projeto `ILoggingLibrary`, que está contido no arquivo `ILoggingLibrary.shared.cs`, define a interface pública (a área de superfície da API) do componente. É aqui que você define a interface para a biblioteca.
- O outro projeto compartilhado contém código em `CrossLoggingLibrary.shared.cs` que localizará uma implementação específica da plataforma da interface abstrata em tempo de execução. Normalmente não é necessário modificar esse arquivo.
- Os projetos específicos da plataforma, como `LoggingLibrary.android.cs`, cada um contém uma implementação nativa da interface em seus respectivos arquivos de `LoggingLibraryImplementation.cs` (VS 2017) ou `LoggingLibrary.<PLATFORM>.cs` (VS 2019). É aqui que você compila o código da biblioteca.

Por padrão, o arquivo ILoggingLibrary.shared.cs do projeto `ILoggingLibrary` contém uma definição de interface, mas nenhum método. Para os fins deste passo a passo, adicione um método `Log` da seguinte maneira:

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace Plugin.LoggingLibrary
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a>Escreva o código específico para sua plataforma

Para implementar uma implementação específica da plataforma `ILoggingLibrary` e seus métodos, faça o seguinte:

1. Abra o arquivo `LoggingLibraryImplementation.cs` (VS 2017) ou `LoggingLibrary.<PLATFORM>.cs` (VS 2019) de cada projeto de plataforma e adicione o código necessário. Por exemplo (usando o projeto de plataforma `Android`):

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Text;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. Repita essa implementação nos projetos para cada plataforma às quais você deseja dar suporte.
1. Clique com o botão direito do mouse e selecione **Compilar solução** para verificar seu trabalho e produzir os artefatos que são empacotados em seguida. Se você receber erros sobre referências ausentes, clique com o botão direito do mouse na solução, selecione **Restaurar pacotes do NuGet** para instalar as dependências e recompile.

> [!Note]
> Se você estiver usando o Visual Studio 2019, antes de selecionar **restaurar pacotes NuGet** e tentar recompilar, será necessário alterar a versão do `MSBuild.Sdk.Extras` para `2.0.54` no `LoggingLibrary.csproj`. Esse arquivo só pode ser acessado clicando-se primeiro com o botão direito do mouse no projeto (abaixo da solução) e selecionando `Unload Project`, depois que você clica com o botão direito do mouse no projeto descarregado e seleciona `Edit LoggingLibrary.csproj`.

> [!Note]
> Para compilar para iOS, é necessário ter um Mac em rede conectado ao Visual Studio, conforme descrito em [Introdução ao Xamarin.iOS para Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/). Se você não tiver um Mac disponível, apague o projeto iOS no Gerenciador de Configuração (etapa 3 acima).

## <a name="create-and-update-the-nuspec-file"></a>Criar e atualizar o arquivo .nuspec

1. Abra um prompt de comando, navegue até a pasta `LoggingLibrary` que está um nível abaixo do qual o arquivo `.sln` está e execute o comando `spec` do NuGet para criar o arquivo `Package.nuspec` inicial:

    ```cli
    nuget spec
    ```

1. Renomeie este arquivo para `LoggingLibrary.nuspec` e abra-o em um editor.
1. Atualize o arquivo para corresponder ao seguinte, substituindo YOUR_NAME por um valor apropriado. O valor `<id>`, especificamente, precisa ser exclusivo no nuget.org (consulte as convenções de nomenclatura descritas em [Criando um pacote](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)). Observe que você também precisa atualizar as marcas de autor e descrição ou um erro é mostrado durante a etapa de empacotamento.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> Você pode acrescentar o sufixo à sua versão de pacote com `-alpha`, `-beta` ou `-rc` para marcar o pacote como versão de pré-lançamento, consulte [Versões de pré-lançamento](../create-packages/prerelease-packages.md) para obter mais informações sobre as versões de pré-lançamento.

### <a name="add-reference-assemblies"></a>Adicionar assemblies de referência

Para incluir os assemblies de referência específicos de plataforma, adicione o seguinte ao elemento `<files>` de `LoggingLibrary.nuspec` conforme apropriado para as plataformas compatíveis:

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> Para encurtar os nomes dos arquivos DLL e XML, clique com o botão direito do mouse em qualquer projeto, selecione a guia **Biblioteca** e altere os nomes de assembly.

### <a name="add-dependencies"></a>Adicionar dependências

Se você tiver dependências específicas para implementações nativas, use o elemento `<dependencies>` com elementos `<group>` especificá-los, por exemplo:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

Por exemplo, o seguinte definiria iTextSharp como uma dependência para o destino UAP:

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>.nuspec final

O arquivo `.nuspec` final agora deve ser semelhante ao seguinte, em que novamente YOUR_NAME deve ser substituído por um valor apropriado:

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2018</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a>Empacotar o componente

Depois do `.nuspec` terminar de referenciar todos os arquivos que você precisa incluir no pacote, você estará pronto para executar o comando `pack`:

```cli
nuget pack LoggingLibrary.nuspec
```

Isso gerará `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`. Ao abrir este arquivo em uma ferramenta como o [Explorador de Pacotes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) e expandir todos os nós, você verá o seguinte conteúdo:

![O Explorador de Pacotes do NuGet mostrando o pacote LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> O arquivo `.nupkg` é apenas um arquivo ZIP com uma extensão diferente. Também é possível examinar o conteúdo do pacote alterando `.nupkg` para `.zip`, mas lembre-se de restaurar a extensão antes de carregar um pacote para o nuget.org.

Para disponibilizar seu pacote para outros desenvolvedores, siga as instruções em [Publicar um pacote](../nuget-org/publish-a-package.md).

## <a name="related-topics"></a>Tópicos relacionados

- [Referência de Nuspec](../reference/nuspec.md)
- [Pacotes de símbolo](../create-packages/symbol-packages.md)
- [Controle de versão do pacote](../concepts/package-versioning.md)
- [Suporte a Várias Versões do .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Incluir objetivos e destinos de MSBuild em um pacote](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Criando Pacotes Localizados](../create-packages/creating-localized-packages.md)