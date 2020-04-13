---
title: Instalar e usar um pacote do NuGet no Visual Studio
description: Um tutorial passo a passo sobre o processo de instalação e uso de um pacote NuGet em um projeto do Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 10bc34653d294cf70b5c91ce79a79cf6532fba1b
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80147481"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a>Quickstart: Instale e use um pacote no Visual Studio (somente para Windows)

Os pacotes NuGet contém código reutilizável que outros desenvolvedores disponibilizam para uso em seus projetos. Consulte [O que há de novo no NuGet](../What-is-NuGet.md) para obter mais informações. Os pacotes são instalados em um projeto do Visual Studio usando o NuGet Package Manager, o [Package Manager Console](../consume-packages/install-use-packages-powershell)ou o [dotnet CLI](install-and-use-a-package-using-the-dotnet-cli.md). Este artigo demonstra o processo usando o conhecido pacote [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) e um projeto da WPF (Windows Presentation Foundation). O mesmo processo se aplica a qualquer outro projeto .NET ou .NET Core.

Depois de instalado, consulte o pacote no código com `using <namespace>` em que \<namespace\> é específico para o pacote que você está usando. Depois que a referência é feita, você pode chamar o pacote por meio de sua API.

> [!Tip]
> **Comece com nuget.org**: Navegar *nuget.org* é como os desenvolvedores do .NET normalmente encontram componentes que podem reutilizar em seus próprios aplicativos. Você pode pesquisar no *nuget.org* diretamente ou localizar e instalar pacotes de dentro do Visual Studio, conforme mostrado neste artigo. Para saber mais, confira [Localizar e avaliar pacotes do NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Pré-requisitos

- Visual Studio 2019 com a carga de trabalho do desenvolvimento para área de trabalho .NET.

É possível instalar a edição Community 2019 gratuitamente em [visualstudio.com](https://www.visualstudio.com/) ou usar as edições Professional ou Enterprise.

Se você estiver usando o Visual Studio para Mac, consulte [Instalar e usar um pacote no Visual Studio para Mac](install-and-use-a-package-in-visual-studio-mac.md).

## <a name="create-a-project"></a>Criar um projeto

É possível instalar pacotes do NuGet em qualquer projeto .NET, desde que o pacote ofereça suporte à mesma estrutura de destino do projeto.

Para esta explicação, use um aplicativo WPF simples. Crie um projeto no Visual Studio usando **file** > **new project,** digitando **.NET** na caixa de pesquisa e, em seguida, selecionando o **aplicativo WPF (.NET Framework)**. Clique em **Próximo**. Aceite os valores padrão para **Estrutura** quando solicitado.

O Visual Studio criará o projeto, que será aberto no Gerenciador de Soluções.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Adicionar o pacote do NuGet Newtonsoft.Json

Para instalar o pacote, use o Gerenciador de pacotes do NuGet ou o Console do Gerenciador de Pacotes. Ao instalar um pacote, o NuGet registra a dependência no arquivo de projeto ou em um arquivo `packages.config` (dependendo do formato do projeto). Para obter mais informações, veja [Visão geral e fluxo de trabalho do consumo de pacote](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Gerenciador de Pacotes NuGet

1. No Gerenciador de Soluções, clique com botão direito do mouse em **Referências** e escolha **Gerenciar pacotes do NuGet**.

    ![Gerenciar o comando de pacotes do NuGet para referências de projeto](media/QS_Use-02-ManageNuGetPackages.png)

1. Escolha “nuget.org” como a **Origem do pacote**, selecione a guia **Procurar**, pesquise por **Newtonsoft.Json**, selecione o pacote na lista e escolha **Instalar**:

    ![Localizando o pacote Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

    Se quiser saber mais sobre o Gerenciador de pacotes do NuGet, confira [Instalar e gerenciar pacotes usando o Visual Studio](../consume-packages/install-use-packages-visual-studio.md).

1. Aceite quaisquer avisos de licença.

1. (Somente no Visual Studio 2017) Se receber uma solicitação para selecionar um formato de gerenciamento de pacote, selecione **PackageReference no arquivo de projeto**:

    ![Como selecionar um formato de gerenciamento de pacote](media/QS_Use-03b-SelectFormat.png)

1. Se for solicitado para examinar as alterações, selecione **OK**.

### <a name="package-manager-console"></a>Console do Gerenciador de Pacotes

1. Selecione o comando **Derdo** > do console do**Gerenciador de pacotes NuGet Package** > **Manager.**

1. Após a abertura do console, verifique se a lista suspensa **Projeto padrão** mostra o projeto no qual você deseja instalar o pacote. Se você tiver um único projeto na solução, ele já estará selecionado.

    ![Localizando o pacote Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. Insira o comando `Install-Package Newtonsoft.Json` (veja [Install-Package](../reference/ps-reference/ps-ref-install-package.md)). A janela do console mostra a saída do comando. Os erros indicam que o pacote não é compatível com a estrutura de destino do projeto.

   Se quiser saber mais sobre o Console do Gerenciador de Pacotes, confira [Instalar e gerenciar pacotes usando o Console do Gerenciador de Pacotes](../consume-packages/install-use-packages-powershell.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Use a API Newtonsoft.Json no aplicativo

Com o pacote Newtonsoft.Json no projeto, você pode chamar seu método `JsonConvert.SerializeObject` para converter um objeto em uma cadeia de caracteres legível.

1. Abra `MainWindow.xaml` e substitua o elemento `Grid` existente pelo seguinte:

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Abra o arquivo `MainWindow.xaml.cs` (localizado no Gerenciador de Soluções sob o nó `MainWindow.xaml`) e insira o seguinte código dentro da classe `MainWindow`:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. Mesmo que você tenha adicionado o pacote Newtonsoft.Json ao projeto, o sublinhado vermelho aparecerá sob `JsonConvert` porque você precisa de uma instrução `using` no topo do arquivo de código:

    ```cs
    using Newtonsoft.Json;
    ```

1. Construa e execute o aplicativo pressionando F5 ou selecionando **Depuração** > Iniciar**de depuração:**

    ![Saída inicial do aplicativo WPF](media/QS_Use-06-AppStart.png)

1. Selecione o botão para ver o conteúdo do TextBlock substituído com algum texto JSON:

    ![Saída do aplicativo WPF após selecionar o botão](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a>Vídeo relacionado

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

Encontre mais vídeos do NuGet no [Canal 9](https://channel9.msdn.com/Series/NuGet-101) e [no YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="next-steps"></a>Próximas etapas

Parabéns por instalar e usar seu primeiro pacote do NuGet!

> [!div class="nextstepaction"]
> [Instalar e gerenciar pacotes usando o Visual Studio](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [Instalar e gerenciar pacotes usando o Console do gerenciador de pacote](../consume-packages/install-use-packages-powershell.md)

Para ver o que mais o NuGet tem a oferecer, selecione os links abaixo.

- [Visão geral e fluxo de trabalho do consumo de pacote](../consume-packages/overview-and-workflow.md)
- [Localizando e escolhendo pacotes](../consume-packages/finding-and-choosing-packages.md)
- [Referências de pacotes em arquivos de projeto](../consume-packages/package-references-in-project-files.md)
