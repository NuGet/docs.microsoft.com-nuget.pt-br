---
title: Criar e publicar um pacote NuGet do .NET Standard - Visual Studio no Windows
description: Um tutorial passo a passo sobre como criar e publicar um pacote NuGet do .NET Standard usando o Visual Studio no Windows.
author: karann-msft
ms.author: karann
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 32dcc1d233154463e2950b1ce46554b1cb89956e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237491"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Início Rápido: Criar e publicar um pacote do NuGet usando o Visual Studio (.NET Standard somente no Windows)

Criar um pacote NuGet de uma Biblioteca de Classes .NET Standard no Visual Studio no Windows e, em seguida, publicá-lo no nuget.org usando uma ferramenta de CLI é um processo simples.

> [!Note]
> Se você estiver usando o Visual Studio para Mac, confira [essas informações](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) sobre como criar um pacote NuGet ou use as [ferramentas de CLI do dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Pré-requisitos

1. Instale qualquer edição do Visual Studio 2019 de [visualstudio.com](https://www.visualstudio.com/) com uma carga de trabalho relacionada ao .NET Core.

1. Instale a CLI `dotnet`, se ainda não estiver instalada.

   Para a CLI do `dotnet`, a partir do Visual Studio 2017, a CLI do `dotnet` é instalada automaticamente com qualquer carga de trabalho relacionada ao .NET Core. Caso contrário, instale o [SDK do .NET Core](https://www.microsoft.com/net/download/) para ter a CLI do `dotnet`. A CLI `dotnet` é necessária para projetos do .NET Standard que usam o [formato de estilo SDK](../resources/check-project-format.md) (atributo do SDK). O modelo padrão de biblioteca de classes .NET Standard no Visual Studio 2017 e posterior, que é usado neste artigo, usa o atributo SDK.
   
   > [!Important]
   > Se você estiver trabalhando com um projeto de estilo não SDK, siga os procedimentos em [Criar e publicar um pacote de .NET Framework (Visual Studio](create-and-publish-a-package-using-visual-studio-net-framework.md)) para criar e publicar o pacote. Para este artigo, a CLI do `dotnet` recomendada. Embora você possa publicar qualquer pacote NuGet usando a CLI do `nuget.exe`, algumas das etapas neste artigo são específicas para projetos no estilo SDK e a CLI do dotnet. A CLI do nuget.exe é usada para [projetos de estilo não SDK](../resources/check-project-format.md) (normalmente .NET Framework).

1. [Registre-se em uma conta gratuita em nuget.org](../nuget-org/individual-accounts.md#add-a-new-individual-account), se ainda não tiver uma. Criar uma nova conta envia um email de confirmação. Você deve confirmar a conta antes de poder carregar um pacote.

## <a name="create-a-class-library-project"></a>Criar um projeto de biblioteca de classes

Você pode usar um projeto existente da Biblioteca de Classes .NET Standard para o código que você deseja empacotar ou criar um simples da seguinte maneira:

1. No Visual Studio, escolha **Arquivo > Novo > Projeto** , expanda o nó **Visual C# > .NET Standard** , selecione o modelo de "Biblioteca de Classes (.NET Standard)", nomeie o projeto como AppLogger e clique em **OK** .

   > [!Tip]
   > A menos que você tenha um motivo para a escolha de outro jeito, o .NET Standard é o destino preferencial para pacotes NuGet, pois fornece compatibilidade com a mais ampla variedade de projetos de consumo.

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

## <a name="configure-package-properties"></a>Configurar as propriedades do pacote

1. Clique com o botão direito do mouse no projeto no Gerenciador de Soluções e escolha o comando de menu **Propriedades** e selecione a guia **Pacote** .

   A guia **Pacote** é exibida apenas para projetos no estilo SDK no Visual Studio, normalmente .NET Standard ou projetos de biblioteca de classes do .NET Core; se você estiver direcionando para um projeto de estilo não SDK (normalmente, .NET Framework), [migre o projeto](../consume-packages/migrate-packages-config-to-package-reference.md) ou confira [Criar e publicar um pacote do .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) para ver as instruções passo a passo.

    ![Propriedades do pacote NuGet em um projeto do Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Para pacotes compilados para consumo público, preste atenção especial à propriedade **Tags** , à medida que as marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.

1. Dê ao seu pacote um identificador exclusivo e preencha as outras propriedades desejadas. Para ver um mapeamento das propriedades do MSBuild (projeto no estilo SDK) para propriedades em um *.nuspec* , confira [alvos de pacote](../reference/msbuild-targets.md#pack-target). Para obter descrições de propriedades, confira a [referência do arquivo .nuspec](../reference/nuspec.md). Todas essas propriedades vão para o manifesto `.nuspec` que o Visual Studio cria para o projeto.

    > [!Important]
    > Você precisa dar ao pacote um identificador exclusivo em nuget.org ou qualquer host que você esteja usando. Para este passo a passo, recomendamos incluir o "Sample" ou "Test" no nome, pois a etapa de publicação posterior torna o pacote publicamente visível (embora seja improvável que alguém possa usá-lo).
    >
    > Se você tentar publicar um pacote com um nome que já existe, você verá um erro.

1. (Opcional) Para ver as propriedades diretamente no arquivo de projeto, clique com o botão direito do mouse no projeto no Gerenciador de Soluções e selecione **Editar AppLogger.csproj** .

   Essa opção só está disponível a partir do Visual Studio 2017 para projetos que usam o atributo de estilo SDK. Caso contrário, clique com o botão direito do mouse no projeto e escolha **Descarregar Projeto** . Em seguida, clique com o botão direito do mouse no projeto descarregado e escolha **Editar AppLogger.csproj** .

## <a name="run-the-pack-command"></a>Executar o comando pack

1. Defina a configuração como **Versão** .

1. Clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e selecione o comando **Pack** :

    ![Comando pack do NuGet no menu de contexto de projeto do Visual Studio](media/qs_create-vs-02-pack-command.png)

    Se você não vir o comando **Pack** , seu projeto provavelmente não será um projeto no estilo SDK e você precisará usar a CLI do `nuget.exe`. Ou [migre o projeto](../consume-packages/migrate-packages-config-to-package-reference.md) e use `dotnet` a CLI, ou confira [Criar e publicar um pacote do .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) para ver instruções passo a passo.

1. O Visual Studio compila o projeto e cria o arquivo `.nupkg`. Examine a janela **Saída** para obter detalhes (semelhante ao seguinte), que contém o caminho até o arquivo de pacote. Observe também que o assembly criado está em `bin\Release\netstandard2.0`, como convém ao destino do .NET Standard 2.0.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a>(Opcional) Gerar pacote ao compilar

Você pode configurar o Visual Studio para gerar automaticamente o pacote NuGet ao compilar o projeto.

1. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e escolha **Propriedades** .

2. Na guia **Pacote** , selecione **Gerar pacote NuGet no build** .

   ![Gerar pacote automaticamente no build](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> Ao gerar automaticamente o pacote, o tempo de empacotamento aumenta o tempo de compilação do seu projeto.

### <a name="optional-pack-with-msbuild"></a>(Opcional) Empacotar com MSBuild

Como alternativa ao uso do comando do menu **Pack** , o NuGet 4. x + e o MSBuild 15.1 + dão suporte a um `pack` destino quando o projeto contém os dados de pacote necessários. Abra um prompt de comando, navegue até a pasta do projeto e execute o seguinte comando. (Você normalmente deseja iniciar o "Prompt de Comando do Desenvolvedor para Visual Studio" por meio do menu Iniciar, pois ele estará configurado com todos os caminhos necessários para o MSBuild.)

Para saber mais, confira [Criar um pacote usando MSBuild](../create-packages/creating-a-package-msbuild.md).

## <a name="publish-the-package"></a>Publicar o pacote

Depois que você tiver um arquivo `.nupkg`, publique-o em nuget.org usando a CLI do `nuget.exe` ou a CLI do `dotnet.exe` juntamente com uma chave de API adquirida em nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Adquirir a chave de sua API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a>Publicar com a CLI do dotnet ou a CLI do nuget.exe

Selecione a guia para sua ferramenta CLI, **CLI do .NET Core** (CLI do dotnet) ou **NuGet** (CLI do nuget.exe).

# <a name="net-core-cli"></a>[CLI do .NET Core](#tab/netcore-cli)

Esta etapa é a alternativa recomendada para usar o `nuget.exe`.

Antes de publicar o pacote, você deverá primeiro abrir uma linha de comando.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nuget"></a>[NuGet](#tab/nuget)

Esta etapa é uma alternativa ao uso de `dotnet.exe`.

1. Abra uma linha de comando e altere para a pasta que contém o arquivo `.nupkg`.

1. Execute o seguinte comando, especificando o nome do pacote (ID de pacote exclusiva) e substituindo o valor da chave pela chave da API:

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

Confira [nuget push](../reference/cli-reference/cli-ref-push.md).

---

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

## <a name="related-video"></a>Vídeo relacionado

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-Visual-Studio-4-of-5/player]

Encontre mais vídeos sobre o NuGet no [Channel 9](https://channel9.msdn.com/Series/NuGet-101) e no [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="related-topics"></a>Tópicos relacionados

- [Criar um pacote](../create-packages/creating-a-package-dotnet-cli.md)
- [Publicar um pacote](../nuget-org/publish-a-package.md)
- [Pacotes de pré-lançamento](../create-packages/Prerelease-Packages.md)
- [Suporte a várias estruturas de destino](../create-packages/multiple-target-frameworks-project-file.md)
- [Controle de versão do pacote](../concepts/package-versioning.md)
- [Criando pacotes localizados](../create-packages/creating-localized-packages.md)
- [Documentação da Biblioteca do .NET Standard](/dotnet/articles/standard/library)
- [Portabilidade para o .NET Core do .NET Framework](/dotnet/articles/core/porting/index)
