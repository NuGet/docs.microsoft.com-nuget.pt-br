---
title: Criar e publicar um pacote .NET Framework usando o Visual Studio no Windows
description: Um tutorial passo a passo sobre como criar e publicar um pacote NuGet do .NET Framework usando o Visual Studio no Windows.
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: efdaa0128d47f948c86c3cc83d6a332410cbf99f
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426334"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a>Início Rápido: Criar e publicar um pacote usando o Visual Studio (.NET Framework, Windows)

Para criar um pacote NuGet em uma Biblioteca de Classes .NET Framework, é necessário criar a DLL no Visual Studio no Windows e, em seguida, usar a ferramenta de linha de comando nuget.exe para criar e publicar o pacote.

> [!Note]
> Este Início Rápido se aplica somente ao Visual Studio 2017 para Windows. O Visual Studio para Mac não inclui os recursos descritos aqui. Em vez disso, use as [ferramentas CLI do dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Pré-requisitos

1. Instale qualquer edição do Visual Studio 2017 de [visualstudio.com](https://www.visualstudio.com/) usando qualquer carga de trabalho relacionada ao .NET. O Visual Studio 2017 inclui automaticamente os recursos do NuGet quando uma carga de trabalho do .NET é instalada.

1. Instale a CLI do `nuget.exe` baixando-a de [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), salvando o arquivo `.exe` em uma pasta adequada e adicionando pasta a variável de ambiente PATH.

1. [Registre-se em uma conta gratuita em nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), se ainda não tiver uma. Criar uma nova conta envia um email de confirmação. Você deve confirmar a conta antes de poder carregar um pacote.

## <a name="create-a-class-library-project"></a>Criar um projeto de biblioteca de classes

Você pode usar um projeto existente da Biblioteca de Classes .NET Framework para o código que desejar empacotar ou criar um projeto simples da seguinte maneira:

1. No Visual Studio, escolha **Arquivo > Novo > Projeto**, selecione o nó **Visual C#** , selecione o modelo “Biblioteca de Classes (.NET Framework)”, nomeie o projeto como AppLogger e clique em **OK**.

1. Clique com botão direito do mouse no arquivo de projeto resultante e selecione **Build** para verificar se o projeto foi criado corretamente. A DLL é encontrada dentro da pasta de Depuração (ou Versão, se você compilar essa configuração).

Em um pacote NuGet real, obviamente, você implementa muitos recursos úteis com os quais outras pessoas podem compilar aplicativos. Você também poderá definir as estruturas de destino da maneira que desejar. Por exemplo, veja os guias para a [UWP](../guides/create-uwp-packages.md) e para o [Xamarin](../guides/create-packages-for-xamarin.md).

Para este passo a passo, no entanto, você não escreverá nenhum código adicional porque uma biblioteca de classes do modelo é suficiente para criar um pacote. Ainda assim, se você desejar algum código funcional para o pacote, use o seguinte:

```cs
using System;

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

> [!Tip]
> A menos que você tenha um motivo para a escolha de outro jeito, o .NET Standard é o destino preferencial para pacotes NuGet, pois fornece compatibilidade com a mais ampla variedade de projetos de consumo. Veja [Criar e publicar um pacote usando o Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).

## <a name="configure-project-properties-for-the-package"></a>Configurar propriedades do projeto para o pacote

Um pacote NuGet contém um manifesto (um arquivo `.nuspec`), que contém metadados relevantes, como o identificador do pacote, o número de versão, a descrição e muito mais. Alguns deles podem ser obtidos diretamente das propriedades do projeto, o que evita a necessidade de atualizá-los separadamente no projeto e no manifesto. Esta seção descreve onde definir as propriedades aplicáveis.

1. Selecione o comando de menu **Projeto > Propriedades** e, em seguida, selecione a guia **Aplicativo**.

1. No campo **Nome do assembly**, dê um identificador exclusivo ao pacote.

    > [!Important]
    > Você precisa dar ao pacote um identificador exclusivo em nuget.org ou qualquer host que você esteja usando. Para este passo a passo, recomendamos incluir o "Sample" ou "Test" no nome, pois a etapa de publicação posterior torna o pacote publicamente visível (embora seja improvável que alguém possa usá-lo).
    >
    > Se você tentar publicar um pacote com um nome que já existe, você verá um erro.

1. Selecione o botão **Informações do Assembly...** , que abrirá uma caixa de diálogo na qual será possível inserir outras propriedades contidas no manifesto (veja [Referência do arquivo .nuspec – tokens de substituição](../reference/nuspec.md#replacement-tokens)). Os campos mais usados são **Título**, **Descrição**, **Empresa**, **Direitos autorais** e **Versão do assembly**. Essas propriedades aparecem, por fim, com o pacote em um host, como o nuget.org, portanto deixe-os totalmente descritivos.

    ![Informações do assembly em um projeto do .NET Framework no Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. Opcional: para ver e editar as propriedades diretamente, abra o arquivo `Properties/AssemblyInfo.cs` no projeto.

1. Quando as propriedades forem definidas, defina a configuração do projeto como **Versão** e recompile o projeto para gerar a DLL atualizada.

## <a name="generate-the-initial-manifest"></a>Gerar o manifesto inicial

Com uma DLL disponível e as propriedades do projeto definidas, use o comando `nuget spec` para gerar um arquivo `.nuspec` inicial do projeto. Essa etapa inclui os tokens de substituição correspondentes para obter informações do arquivo de projeto.

Execute `nuget spec` apenas uma vez para gerar o manifesto inicial. Ao atualizar o pacote, altere os valores no projeto ou edite o manifesto diretamente.

1. Abra um prompt de comando e navegue até a pasta que contém o arquivo de projeto `AppLogger.csproj`.

1. Execute o seguinte comando: `nuget spec AppLogger.csproj`. Ao especificar um projeto, o NuGet cria um manifesto que corresponde ao nome do projeto, nesse caso `AppLogger.nuspec`. Ele também inclui os tokens de substituição no manifesto.

1. Abra `AppLogger.nuspec` em um editor de texto para examinar o conteúdo, que deverá ter a seguinte aparência:

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a>Editar o manifesto

1. O NuGet gerará erro se você tentar criar um pacote com os valores padrão no arquivo `.nuspec`, portanto edite os campos a seguir antes de continuar. Veja a [Referência do arquivo .nuspec – elementos de metadados opcionais](../reference/nuspec.md#optional-metadata-elements) para uma descrição de como eles são usados.

    - licenseUrl
    - projectUrl
    - iconUrl
    - releaseNotes
    - marcações

1. Para pacotes compilados para consumo público, preste atenção especial à propriedade **Tags**, uma vez que as marcações ajudam outras pessoas a encontrar o pacote em fontes como o nuget.org e a entender o que ele faz.

1. Você também pode adicionar outros elementos ao manifesto nesse momento, conforme descrito em [Referência do arquivo .nuspec](../reference/nuspec.md).

1. Salve o arquivo antes de continuar.

## <a name="run-the-pack-command"></a>Executar o comando pack

1. Em um prompt de comando na pasta contendo o arquivo `.nuspec`, execute o comando `nuget pack`.

1. O NuGet gera um arquivo `.nupkg` na forma de *identifier-version.nupkg*, que você encontrará na pasta atual.

## <a name="publish-the-package"></a>Publicar o pacote

Depois de ter um arquivo `.nupkg`, publique-o no nuget.org usando `nuget.exe` juntamente com uma chave de API adquirida no nuget.org. Para o nuget.org, você deverá usar o `nuget.exe` 4.1.0 ou superior.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Adquirir a chave de sua API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Publicar com nuget push

1. Altere para a pasta que contém o arquivo `.nupkg`.

1. Execute o seguinte comando, especificando o nome do pacote e substituindo o valor da chave pela chave da API:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. O nuget.exe exibe os resultados do processo de publicação:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Confira [nuget push](../tools/cli-ref-push.md).

### <a name="publish-errors"></a>Erros de publicação

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Gerenciar o pacote publicado

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Tópicos relacionados

- [Criar um pacote](../create-packages/creating-a-package.md)
- [Publicar um pacote](../nuget-org/publish-a-package.md)
- [Pacotes de pré-lançamento](../create-packages/Prerelease-Packages.md)
- [Suporte a várias estruturas de destino](../create-packages/supporting-multiple-target-frameworks.md)
- [Controle de versão do pacote](../reference/package-versioning.md)
- [Criando pacotes localizados](../create-packages/creating-localized-packages.md)
