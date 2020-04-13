---
title: Criar pacotes do NuGet do .NET Standard e do .NET Framework com o Visual Studio 2015
description: Uma explicação passo a passo completa da criação de pacotes do NuGet do .NET Standard e .NET Framework usando o NuGet 3.x e o Visual Studio 2015.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: b16bf422e2627be3b8516a875d749639734064a9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380717"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>Criar pacotes do .NET Standard e .NET Framework com o Visual Studio 2015

**Observação:** é recomendável usar Visual Studio 2017 para o desenvolvimento de bibliotecas .NET Standard. O Visual Studio 2015 pode funcionar, mas as ferramentas do .NET Core ficam somente no estado de versão prévia. Confira [Criar e publicar um pacote com o Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) para trabalhar com o NuGet 4.x ou posterior e Visual Studio 2017.

A [Biblioteca do .NET Standard](/dotnet/articles/standard/library) é uma especificação formal de APIs .NET que devem estar disponíveis em todos os runtimes do .NET, estabelecendo dessa forma uma maior uniformidade no ecossistema do .NET. A Biblioteca do .NET Standard define um conjunto uniforme de APIs de BCL (Biblioteca de Classes Base) para implementação em todas as plataformas do .NET, independentemente da carga de trabalho. Ele permite que os desenvolvedores produzam código que podem ser usados em todos os runtimes do .NET e reduz ou elimina as diretivas de compilação condicional específicas da plataforma em código compartilhado.

Este guia orienta você durante a criação de um pacote do NuGet direcionado para a Biblioteca do .NET Standard 1.4 ou um pacote direcionado para .NET Framework 4.6. Uma biblioteca do .NET Standard 1.4 funciona no .NET Framework 4.6.1, na Plataforma Universal do Windows 10, no .NET Core e no Mono/Xamarin. Para obter detalhes, consulte a [tabela de mapeamento do .NET Standard](/dotnet/standard/net-standard#net-implementation-support) (documentação do .NET). Se desejar, você poderá escolher outra versão da Biblioteca do .NET Standard.

## <a name="prerequisites"></a>Pré-requisitos

1. Visual Studio 2015 Atualização 3
1. (Apenas .NET Standard) [SDK do .NET Core](https://www.microsoft.com/net/download/)
1. CLI do NuGet. Baixe a versão mais recente do nuget.exe de [nuget.org/downloads](https://nuget.org/downloads) e salve-a em um local de sua escolha. Em seguida, adicione tal local à sua variável de ambiente PATH, se ainda não tiver feito isso.

    > [!Note]
    > O nuget.exe é a própria ferramenta CLI e não um instalador, por isso não se esqueça de salvar o arquivo baixado do navegador em vez de executá-lo.

## <a name="create-the-class-library-project"></a>Criar o projeto da biblioteca de classes

1. No Visual Studio, **Arquivo > Novo > Projeto**, expanda o nó **Visual C# > Windows**, selecione **Biblioteca de Classes (Portátil)**, altere o nome para AppLogger e clique em **OK**.

    ![Criar um novo projeto de biblioteca de classes](media/NetStandard-NewProject.png)

1. Na caixa de diálogo **Adicionar biblioteca de classes portátil** exibida, selecione as opções para `.NET Framework 4.6` e `ASP.NET Core 1.0`. (Se estiver direcionando para .NET Framework, você poderá selecionar qualquer opção apropriada).

1. Se estiver direcionando para .NET Standard, clique com o botão direito do mouse em `AppLogger (Portable)` no Gerenciador de Soluções, selecione **Propriedades**, escolha a guia **Biblioteca** e, em seguida, selecione **Direcionar a .NET Platform Standard** na seção **Direcionamento**. Essa ação solicita confirmação e, em seguida, é possível selecionar `.NET Standard 1.4` (ou outra versão disponível) na lista suspensa:

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
                Console.WriteLine(text);
            }
        }
    }
    ```

1. Defina a configuração para Versão, compile o projeto e verifique se os arquivos DLL e XML são produzidos na pasta `bin\Release`.

## <a name="create-and-update-the-nuspec-file"></a>Criar e atualizar o arquivo .nuspec

1. Abra um prompt de comando, navegue até a pasta que contém a pasta `AppLogger.csproj` (um nível abaixo de onde o arquivo `.sln` está) e execute o comando `spec` do NuGet para criar o arquivo `AppLogger.nuspec` inicial:

    ```cli
    nuget spec
    ```

1. Abra o `AppLogger.nuspec` em um editor e atualize-o para corresponder ao seguinte, substituindo YOUR_NAME por um valor apropriado. O `<id>` valor, especificamente, deve ser único em todo nuget.org (veja as convenções de nomeação descritas na [Criação de um pacote](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number). Observe que você também precisa atualizar as marcas de autor e descrição ou um erro é mostrado durante a etapa de empacotamento.

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
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. Adicionar assemblies de referência ao arquivo `.nuspec`, especificamente a DLL da biblioteca e o arquivo XML do IntelliSense:

    Se estiver direcionando para .NET Standard, as entradas exibidas serão semelhantes a estas:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    Se estiver direcionando para .NET Framework, as entradas exibidas serão semelhantes a estas:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. Clique com o botão direito do mouse na solução e selecione **Compilar solução** para gerar todos os arquivos de pacote.

### <a name="declaring-dependencies"></a>Declarando dependências

Se você tiver dependências em outros pacotes NuGet, liste-as no elemento `<dependencies>` do manifesto com os elementos `<group>`. Por exemplo, para declarar uma dependência no NewtonSoft.Json 8.0.3 ou superior, adicione o seguinte:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

A sintaxe do atributo *version* aqui indica que a versão 8.0.3 ou superior é aceitável. Para especificar intervalos de versão diferentes, consulte [Controle de versão do pacote](../concepts/package-versioning.md).

### <a name="adding-a-readme"></a>Adicionar um Leiame

Crie o arquivo `readme.txt`, coloque-o na pasta raiz do projeto e faça referência a ele no arquivo `.nuspec`:

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

O Visual Studio exibe `readme.txt` quando o pacote está instalado em um projeto. O arquivo não é mostrado quando instalado em projetos do .NET Core ou para pacotes instalados como uma dependência.

## <a name="package-the-component"></a>Empacotar o componente

Depois do `.nuspec` terminar de referenciar todos os arquivos que você precisa incluir no pacote, você estará pronto para executar o comando `pack`:

```cli
nuget pack AppLogger.nuspec
```

Isso gera `AppLogger.YOUR_NAME.1.0.0.nupkg`. Ao abrir este arquivo em uma ferramenta como o [Explorador de Pacotes do NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) e expandir todos os nós, você verá o seguinte conteúdo (mostrado para .NET Standard):

![O Explorador de Pacotes do NuGet mostrando o pacote AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> O arquivo `.nupkg` é apenas um arquivo ZIP com uma extensão diferente. Também é possível examinar o conteúdo do pacote alterando `.nupkg` para `.zip`, mas lembre-se de restaurar a extensão antes de carregar um pacote para o nuget.org.

Para disponibilizar seu pacote para outros desenvolvedores, siga as instruções sobre [Publicar um pacote](../nuget-org/publish-a-package.md).

Observe que `pack` requer o Mono 4.4.2 no Mac OS X e não funciona em sistemas Linux. Em um Mac, você também precisa converter os nomes de caminho do Windows no arquivo `.nuspec` em caminhos no estilo Unix.

## <a name="related-topics"></a>Tópicos relacionados

- [Referência do .nuspec](../reference/nuspec.md)
- [Suporte a várias versões de framework .NET](../create-packages/supporting-multiple-target-frameworks.md)
- [Incluir objetivos e destinos de MSBuild em um pacote](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [Criando pacotes localizados](../create-packages/creating-localized-packages.md)
- [Pacotes de símbolo](../create-packages/symbol-packages-snupkg.md)
- [Controle de versão do pacote](../concepts/package-versioning.md)
- [Documentação da Biblioteca do .NET Standard](/dotnet/articles/standard/library)
- [Portabilidade para o .NET Core do .NET Framework](/dotnet/articles/core/porting/index)
