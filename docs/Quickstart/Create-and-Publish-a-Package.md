---
title: "Guia de introdução para a criação e publicação de um pacote do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/03/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: Um tutorial passo a passo sobre como criar e publicar um pacote do NuGet usando a interface de linha de comando nuget.exe e o Visual Studio.
keywords: "Criação de pacote do NuGet, publicação de pacote do NuGet, tutorial do NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53d29283c9e786fc27e9a608d7d251d8d0b5b0b2
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2018
---
# <a name="create-and-publish-a-package"></a>Criar e publicar um pacote

É um processo simples para criar um pacote do NuGet de uma Biblioteca de Classes do .NET e publique-o em nuget.org. Este artigo orienta você pelo processo usando a CLI (Interface de Linha de Comando) do NuGet e o Visual Studio.

## <a name="pre-requisites"></a>Pré-requisitos

1. Instale qualquer edição do Visual Studio 2017 de [visualstudio.com](https://www.visualstudio.com/).

1. Instale a ferramenta CLI do NuGet, `nuget.exe` baixando a versão mais recente do `nuget.exe` de [nuget.org/downloads](https://nuget.org/downloads) e salvando o `.exe` em um local no seu PATH. Observe que o download *é* a ferramenta em si, não um instalador.

1. Crie um projeto da Biblioteca de Classes .NET adequado para o código que você deseja empacotar. Se você ainda não tiver um projeto, poderá criar um simples da seguinte maneira:
    1. No Visual Studio, escolha **Arquivo > Novo > Projeto**, expanda o nó **Visual C# > Windows**, selecione o modelo de “Biblioteca de Classes”, nomeie o projeto como AppLogger e clique em **OK**.
    1. Clique com botão direito do mouse no arquivo de projeto resultante e selecione **Build** para verificar se o projeto foi criado corretamente. A DLL é encontrada dentro da pasta de Depuração (ou Versão, se você compilar essa configuração).

    Dentro de um pacote do NuGet real, obviamente, você implementará muitos recursos úteis com os quais outras pessoas podem compilar aplicativos. Para este passo a passo, no entanto, você não escreverá nenhum código adicional porque uma biblioteca de classes do modelo é suficiente para criar um pacote.

## <a name="create-the-nuspec-package-manifest-file"></a>Criar o arquivo de manifesto do pacote .nuspec

Todos os pacotes do NuGet precisam de um arquivo de manifesto&mdash;`.nuspec`&mdash; para descrever seu conteúdo e suas dependências. O comando `nuget spec` cria esse arquivo para você, o qual você pode personalizar. Neste exemplo, você cria o `.nuspec` de um arquivo de projeto; você também pode criar o manifesto por outros meios conforme descrito em [Criar um pacote](../create-packages/creating-a-package.md).

1. Abra um prompt de comando e navegue até a pasta que contém o arquivo de projeto (`.csproj`).

1. Execute o comando `spec` da CLI do NuGet para gerar o manifesto, que tem o nome do seu projeto, como `AppLogger.nuspec`:

    ```cli
    nuget spec
    ```

1. Abra o arquivo em um editor de texto. O manifesto se parece com o código abaixo, em que os tokens no formato `<token>`(como `$id$`) são substituídos durante o processo de empacotamento pelos valores do arquivo Properties/AssemblyInfo.cs do projeto. Para obter mais detalhes sobre tokens, consulte [Criando um arquivo .nuspec](../create-packages/creating-a-package.md#creating-the-nuspec-file).

    ```xml
    <?xml version="1.0"?>
    <package>
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
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. Selecione uma ID de pacote que é exclusiva ao nuget.org. É recomendável usar as convenções de nomenclatura descritas em [Criando um pacote](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Atualize as marcas de autor e de descrição, caso contrário, você receberá um erro na próxima etapa. Aqui está um arquivo `.nuspec` atualizado como exemplo:

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> Para pacotes compilados para consumo público, preste atenção especial ao elemento `<tags>`, visto que essas marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.

## <a name="run-the-pack-command"></a>Executar o comando pack

Para compilar um pacote do NuGet (um arquivo `.nupkg`) de um projeto, execute o comando `pack`:

```cli
nuget pack AppLogger.csproj
```

Este comando cria `AppLogger.1.0.0.0.nupkg` usando o nome do pacote e o número de versão do arquivo `.nuspec`. O comando emite avisos se você não tiver atualizado vários campos no arquivo `.nuspec` de seus valores padrão.

## <a name="publish-the-package"></a>Publicar o pacote

Depois que você tiver um arquivo `.nupkg`, ele é publicado em nuget.org usando o comando `push`. (Como alternativa, você pode usar o [Fluxo de trabalho de publicação do nuget.org](../create-packages/publish-a-package.md#publish-to-nugetorg).

> [!Warning]
> Os pacotes que você publica em nuget.org ficam visíveis publicamente para outros desenvolvedores. Para hospedar pacotes de forma privada, consulte [Hospedando pacotes](../hosting-packages/overview.md).

1. Crie uma conta gratuita em [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) ou faça logon se você já tiver uma. Criar uma nova conta envia um email de confirmação. Você deve confirmar a conta antes de poder carregar um pacote.

1. Depois de conectado, selecione seu nome de usuário (no canto superior direito) e selecione **Chaves de API**.

1. Selecione **Criar**, forneça um nome para sua chave, selecione **Selecionar escopos > Push** em **Chave de API**, insira * para **Padrão glob** e selecione **Criar**.

1. Depois que a chave é criada, selecione **Copiar** para recuperar a chave de acesso que você precisará na CLI:

    ![Copiando a chave de API para a área de transferência](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > Salve sua chave em um local seguro e mantenha-a em segredo. Se a chave for revelada acidentalmente, você poderá recriá-la a qualquer momento. Também é possível remover a chave de API, se você não quiser mais efetuar push de pacotes por meio da CLI.

1. Em um prompt de comando, execute o seguinte comando, especificando o nome do pacote e substituindo a chave pelo valor copiado na etapa 4:

    ```cli
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. O nuget.exe exibe os resultados do processo de publicação:

    ```output
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. Do seu perfil no nuget.org, selecione **Gerenciar Pacotes** para ver o que você acabou de publicar. Você também receberá um email de confirmação. Observe que pode levar algum tempo para o pacote ser indexado e aparecer nos resultados da pesquisa, onde outras pessoas podem encontrá-lo. Durante esse momento, sua página do pacote mostra a mensagem abaixo:

    ![Esse pacote ainda não foi indexado. Ele aparecerá nos resultados da pesquisa e estará disponível para instalação/restauração após a conclusão da indexação.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> **Verificação de vírus**: todos os pacotes carregados para o nuget.org são examinados em busca de vírus e rejeitados caso algum vírus seja encontrado. Todos os pacotes listados em nuget.org também são examinados periodicamente.

E pronto. Você acabou de publicar seu primeiro pacote do NuGet no [nuget.org](https://www.nuget.org/), o qual desenvolvedores podem usar em seus próprios projetos.

## <a name="related-topics"></a>Tópicos relacionados

- [Criar um pacote](../create-packages/creating-a-package.md)
- [Publicar um pacote](../create-packages/publish-a-package.md)
- [Suporte a várias estruturas de destino](../create-packages/supporting-multiple-target-frameworks.md)
- [Controle de versão do pacote](../reference/package-versioning.md)
- [Criando pacotes localizados](../create-packages/creating-localized-packages.md)
