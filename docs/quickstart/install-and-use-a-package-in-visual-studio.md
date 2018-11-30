---
title: Guia de introdução ao uso de pacotes do NuGet no Visual Studio
description: Um tutorial passo a passo sobre o processo de instalação e uso de um pacote NuGet em um projeto do Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 15268ae33d56042a765420e5076dac49db6cce04
ms.sourcegitcommit: 1591bb230e106b94162a87dd1d86fe427366730a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52671169"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a>Início Rápido: Instalar e usar um pacote no Visual Studio

Os pacotes NuGet contém código reutilizável que outros desenvolvedores disponibilizam para uso em seus projetos. Consulte [O que há de novo no NuGet](../What-is-NuGet.md) para obter mais informações. Os pacotes são instalados em um projeto do Visual Studio usando a interface do usuário do Gerenciador de Pacotes ou o Console do Gerenciador de Pacotes. Este artigo demonstra o processo usando o conhecido pacote [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) e um projeto da UWP (Plataforma Universal do Windows). O mesmo processo se aplica a qualquer outro projeto .NET ou .NET Core.

Depois de instalado, consulte o pacote no código com `using <namespace>` em que \<namespace\> é específico para o pacote que você está usando. Depois que a referência é feita, você pode chamar o pacote por meio de sua API.

> [!Tip]
> **Começar com nuget.org**: normalmente, os desenvolvedores em .NET encontram os componentes que podem reutilizar em seus próprios aplicativos procurando no nuget.org. Você pode pesquisar no nuget.org diretamente ou localizar e instalar pacotes de dentro do Visual Studio, conforme mostrado neste artigo.

## <a name="prerequisites"></a>Pré-requisitos

- Visual Studio 2017 com a carga de trabalho de desenvolvimento da Plataforma Universal do Windows, ou
- Visual Studio 2015 Atualização 3 com Ferramentas para Aplicativos Universais do Windows.

Você pode instalar a edição Community 2017 gratuitamente no [visualstudio.com](https://www.visualstudio.com/) ou usar as edições Professional ou Enterprise.

## <a name="create-a-project"></a>Criar um projeto

É possível instalar pacotes do NuGet em qualquer projeto .NET, desde que o pacote ofereça suporte à mesma estrutura de destino do projeto.

Para este passo a passo, use um aplicativo da UWP (Plataforma Universal do Windows). Crie um projeto no Visual Studio usando **Arquivo > Novo Projeto...** e selecionando **Universal do Windows > Aplicativo em Branco (Universal do Windows)**. Aceite os valores padrão para a Versão de Destino e a Versão Mínima quando solicitado.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Adicionar o pacote do NuGet Newtonsoft.Json

Para instalar o pacote, use a IU do Gerenciador de Pacotes ou o Console do Gerenciador de Pacotes. Ao instalar um pacote, o NuGet registrará a dependência no arquivo de projeto ou em um arquivo `packages.config`. Para obter mais informações, veja [Visão geral e fluxo de trabalho do consumo de pacote](../consume-packages/Overview-and-Workflow.md).

### <a name="package-manager-ui"></a>Interface do usuário do Gerenciador de Pacotes

1. No Gerenciador de Soluções, clique com botão direito do mouse em **Referências** e escolha **Gerenciar pacotes do NuGet**.

    ![Gerenciar o comando de pacotes do NuGet para referências de projeto](media/QS_Use-02-ManageNuGetPackages.png)

1. Escolha “nuget.org” como a **Origem do pacote**, selecione a guia **Procurar**, pesquise por **Newtonsoft.Json**, selecione o pacote na lista e escolha **Instalar**:

    ![Localizando o pacote Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. Aceite quaisquer avisos de licença.

1. (Visual Studio 2017) Se receber uma solicitação para selecionar um formato de gerenciamento de pacote, selecione **PackageReference no arquivo de projeto**:

    ![Como selecionar um formato de gerenciamento de pacote](media/QS_Use-03b-SelectFormat.png)

1. Se for solicitado para examinar as alterações, selecione **OK**.

### <a name="package-manager-console"></a>Console do Gerenciador de Pacotes

1. Selecione o comando do menu **Ferramentas > Gerenciador de Pacotes NuGet > Console do Gerenciador de Pacotes**.

1. Após a abertura do console, verifique se a lista suspensa **Projeto padrão** mostra o projeto no qual você deseja instalar o pacote. Se você tiver um único projeto na solução, ele já estará selecionado.

    ![Localizando o pacote Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. Insira o comando `Install-Package Newtonsoft.Json` (veja [Install-Package](../tools/ps-ref-install-package.md)). A janela do console mostra a saída do comando. Os erros indicam que o pacote não é compatível com a estrutura de destino do projeto.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Use a API Newtonsoft.Json no aplicativo

Com o pacote Newtonsoft.Json no projeto, você pode chamar seu método `JsonConvert.SerializeObject` para converter um objeto em uma cadeia de caracteres legível.

1. Abra `MainPage.xaml` e substitua o elemento `Grid` existente pelo seguinte:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Abra o arquivo `MainPage.xaml.cs` (localizado no Gerenciador de Soluções no nó `MainPage.xaml`) e insira o seguinte código dentro do construtor `MainPage`:

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

1. Compile e execute o aplicativo pressionando F5 ou selecionando **Depurar > Iniciar a Depuração**:

    ![Saída inicial do aplicativo UWP](media/QS_Use-06-AppStart.png)

1. Selecione o botão para ver o conteúdo do TextBlock substituído com algum texto JSON:

    ![Saída do aplicativo UWP depois de selecionar o botão](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a>Artigos relacionados

- [Visão geral e fluxo de trabalho do consumo de pacote](../consume-packages/overview-and-workflow.md)
- [Localizando e escolhendo pacotes](../consume-packages/finding-and-choosing-packages.md)
- [Maneiras de instalar um pacote](../consume-packages/ways-to-install-a-package.md)
- [Configurando o Comportamento de NuGet](../consume-packages/configuring-nuget-behavior.md)
