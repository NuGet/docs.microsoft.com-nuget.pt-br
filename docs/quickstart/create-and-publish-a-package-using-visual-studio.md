---
title: Criar e publicar um pacote .NET Standard usando o Visual Studio no Windows
description: Um tutorial passo a passo sobre como criar e publicar um pacote NuGet do .NET Standard usando o Visual Studio 2017 no Windows.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: d30e89473b5f00895136b75a90d8d95b7645a100
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812984"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Início Rápido: Criar e publicar um pacote do NuGet usando o Visual Studio (.NET Standard somente no Windows)

Criar um pacote NuGet de uma Biblioteca de Classes .NET Standard no Visual Studio no Windows e, em seguida, publicá-lo no nuget.org usando uma ferramenta de CLI é um processo simples.

> [!Note]
> Este Início Rápido se aplica somente ao Visual Studio 2017 para Windows. O Visual Studio para Mac não inclui os recursos descritos aqui. Em vez disso, use as [ferramentas CLI do dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Pré-requisitos

1. Instale qualquer edição do Visual Studio 2017 de [visualstudio.com](https://www.visualstudio.com/) usando qualquer carga de trabalho relacionada ao .NET. O Visual Studio 2017 inclui automaticamente os recursos do NuGet quando uma carga de trabalho do .NET é instalada.

1. Clique em uma das ferramentas de CLI.

   * Para a CLI do `dotnet`, instale o [SDK do .NET Core](https://www.microsoft.com/net/download/). A CLI dotnet é necessária para projetos do .NET Standard que usam o formato de estilo do SDK (atributo do SDK).

   * Instale a CLI do `nuget.exe`, baixe-a em [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), salve o arquivo `.exe` em uma pasta adequada e adicione essa pasta na sua variável de ambiente PATH. A CLI do nuget.exe é usada nas bibliotecas do .NET Standard no formato de estilo não SDK.

1. [Registre-se em uma conta gratuita em nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), se ainda não tiver uma. Criar uma nova conta envia um email de confirmação. Você deve confirmar a conta antes de poder carregar um pacote.

## <a name="create-a-class-library-project"></a>Criar um projeto de biblioteca de classes

Você pode usar um projeto existente da Biblioteca de Classes .NET Standard para o código que você deseja empacotar ou criar um simples da seguinte maneira:

1. No Visual Studio, escolha **Arquivo > Novo > Projeto**, expanda o nó **Visual C# > .NET Standard**, selecione o modelo de "Biblioteca de Classes (.NET Standard)", nomeie o projeto como AppLogger e clique em **OK**.

1. Clique com botão direito do mouse no arquivo de projeto resultante e selecione **Build** para verificar se o projeto foi criado corretamente. A DLL é encontrada dentro da pasta de Depuração (ou Versão, se você compilar essa configuração).

Em um pacote NuGet real, obviamente, você implementa muitos recursos úteis com os quais outras pessoas podem compilar aplicativos. Para este passo a passo, no entanto, você não escreverá nenhum código adicional porque uma biblioteca de classes do modelo é suficiente para criar um pacote. Ainda assim, se você desejar algum código funcional para o pacote, use o seguinte:

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

> [!Tip]
> A menos que você tenha um motivo para a escolha de outro jeito, o .NET Standard é o destino preferencial para pacotes NuGet, pois fornece compatibilidade com a mais ampla variedade de projetos de consumo.

## <a name="configure-package-properties"></a>Configurar propriedades do pacote

1. Selecione o comando de menu **Projeto > Propriedades** e, em seguida, selecione a guia **Pacote**. (A guia **Pacote** é exibida apenas para projetos da biblioteca de classes do .NET Standard. Se você estiver direcionando ao .NET Framework, veja [Criar e publicar um pacote do .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md). Se ela não for exibida para um projeto do .NET Standard, você precisará atualizar o Visual Studio 2017 para a versão mais recente.)

    ![Propriedades do pacote NuGet em um projeto do Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Para pacotes compilados para consumo público, preste atenção especial à propriedade **Tags**, à medida que as marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.

1. Dê ao seu pacote um identificador exclusivo e preencha as outras propriedades desejadas. Para obter uma descrição das propriedades diferentes, veja [referência de arquivo .nuspec](../reference/nuspec.md). Todas essas propriedades vão para o manifesto `.nuspec` que o Visual Studio cria para o projeto.

    > [!Important]
    > Você precisa dar ao pacote um identificador exclusivo em nuget.org ou qualquer host que você esteja usando. Para este passo a passo, recomendamos incluir o "Sample" ou "Test" no nome, pois a etapa de publicação posterior torna o pacote publicamente visível (embora seja improvável que alguém possa usá-lo).
    >
    > Se você tentar publicar um pacote com um nome que já existe, você verá um erro.

1. Opcional: para ver as propriedades diretamente no arquivo de projeto, clique com o botão direito do mouse no projeto no Gerenciador de Soluções e selecione **Editar AppLogger.csproj**.

## <a name="run-the-pack-command"></a>Executar o comando pack

1. Defina a configuração da solução como **Release**.

1. Clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e selecione o comando **Pack**:

    ![Comando pack do NuGet no menu de contexto de projeto do Visual Studio](media/qs_create-vs-02-pack-command.png)

1. O Visual Studio compila o projeto e cria o arquivo `.nupkg`. Examine a janela **Saída** para obter detalhes (semelhante ao seguinte), que contém o caminho até o arquivo de pacote. Observe também que o assembly criado está em `bin\Release\netstandard2.0`, como convém ao destino do .NET Standard 2.0.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a>Opção alternativa: empacotar com o MSBuild

Como uma alternativa ao uso do comando de menu **Pack**, o NuGet 4.x+ e o MSBuild 15.1+ são compatíveis com um destino `pack` quando o projeto contém os dados do pacote necessários. Abra um prompt de comando, navegue até a pasta do projeto e execute o seguinte comando. (Você normalmente deseja iniciar o "Prompt de Comando do Desenvolvedor para Visual Studio" por meio do menu Iniciar, pois ele estará configurado com todos os caminhos necessários para o MSBuild.)

```cli
msbuild -t:pack -p:Configuration=Release
```

O pacote pode então ser encontrado na pasta `bin\Release`.

Para opções adicionais com `msbuild -t:pack`, consulte [Empacotamento e restauração do NuGet como destinos do MSBuild](../reference/msbuild-targets.md#pack-target).

## <a name="publish-the-package"></a>Publicar o pacote

Depois que você tiver um arquivo `.nupkg`, publique-o em nuget.org usando a CLI do `nuget.exe` ou a CLI do `dotnet.exe` juntamente com uma chave de API adquirida em nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Adquirir a chave de sua API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a>Publicar com dotnet nuget push (CLI do dotnet)

Esta etapa é uma alternativa ao uso de `nuget.exe`.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a>Publicar com nuget push (CLI do nuget.exe)

Esta etapa é uma alternativa ao uso de `dotnet.exe`.

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

## <a name="adding-a-readme-and-other-files"></a>Adicionar um Leiame e outros arquivos

Para especificar diretamente os arquivos a serem incluídos no pacote, edite o arquivo de projeto e use a propriedade `content`:

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

Isso incluirá um arquivo chamado `readme.txt` na raiz do pacote. O Visual Studio exibe o conteúdo do arquivo como texto sem formatação imediatamente depois de instalar o pacote diretamente. (Arquivos Leiame não são exibidos para pacotes instalados como dependências). Por exemplo, mostramos aqui como o arquivo Leiame para o pacote HtmlAgilityPack é exibido:

![A exibição de um arquivo Leiame para um pacote do NuGet na instalação](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> Somente adicionar o readme.txt na raiz do projeto não resultará na inclusão dele no pacote resultante.

## <a name="related-topics"></a>Tópicos relacionados

- [Criar um pacote](../create-packages/creating-a-package.md)
- [Publicar um pacote](../create-packages/publish-a-package.md)
- [Pacotes de pré-lançamento](../create-packages/Prerelease-Packages.md)
- [Suporte a várias estruturas de destino](../create-packages/supporting-multiple-target-frameworks.md)
- [Controle de versão do pacote](../reference/package-versioning.md)
- [Criando pacotes localizados](../create-packages/creating-localized-packages.md)
- [Documentação da Biblioteca do .NET Standard](/dotnet/articles/standard/library)
- [Portabilidade para o .NET Core do .NET Framework](/dotnet/articles/core/porting/index)
