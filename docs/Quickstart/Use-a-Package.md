---
title: "Guia de introdução ao uso de pacotes do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: f31f8259-20a8-4617-880e-5819299372d2
description: "Um tutorial passo a passo sobre o processo de instalação e uso de um pacote do NuGet em um projeto."
keywords: "instalar o NuGet, consumo de pacote do NuGet, instalando pacotes do NuGet, referências de pacote do NuGet, usando pacotes do NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bcccc7139de31a8d07e9ed52abfd12fe9e6d687b
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="install-and-use-a-package"></a>Instalar e usar um pacote

[!INCLUDE [install-methods](../includes/install-methods.md)]

Depois de instalado, consulte o pacote no código com `using <namespace>` em que \<namespace\> é específico para o pacote que você está usando. Depois que a referência é feita, você pode chamar o pacote por meio de sua API.

O restante deste tópico explica o processo de usar a interface do usuário do Gerenciador de Pacotes para instalar o popular pacote [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) em um projeto da UWP (Plataforma Universal do Windows). Ele mostra um exemplo de como usar o pacote. Você pode usar um fluxo de trabalho semelhante para praticamente todos os pacotes do NuGet usados em um projeto.

- [Instalar os pré-requisitos](#install-pre-requisites)
- [Criar um projeto](#create-a-project)
- [Adicionar o pacote do NuGet Newtonsoft.Json](#add-the-newtonsoftjson-nuget-package)
- [Use a API Newtonsoft.Json no aplicativo](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> **Iniciar com nuget.org**: a instalação de pacotes do nuget.org é um fluxo de trabalho comum que os desenvolvedores de .NET usam para encontrar componentes que podem ser reutilizados em seus próprios aplicativos. Você sempre pode pesquisar no nuget.org diretamente ou localizar e instalar pacotes de dentro do Visual Studio, conforme mostrado neste tópico.

## <a name="install-pre-requisites"></a>Instalar os pré-requisitos

Este tutorial requer o Visual Studio 2015 Atualização 3 com as Ferramentas para Aplicativos Universais do Windows ou Visual Studio 2017 com a carga de trabalho de desenvolvimento da Plataforma Universal do Windows. Se você já tiver o Visual Studio instalado, execute o instalador novamente para adicionar as ferramentas UWP.

Você pode instalar a edição Community gratuitamente no [visualstudio.com](https://www.visualstudio.com/) ou usar as edições Professional ou Enterprise. 

## <a name="create-a-project"></a>Criar um projeto

Para instalar um pacote do NuGet, você precisa alguns tipos de projetos baseados em .NET no Visual Studio. Para este passo a passo, você pode usar um aplicativo simples do WPF (Windows Presentation Foundation) ou UWP (Universal do Windows):

- Para WPF (Windows 7 ou superior), escolha **Arquivo > Novo > Projeto**, expanda **Visual C#**, selecione **Área de Trabalho Clássica do Windows > Aplicativo WPF (.NET Framework)** e selecione **OK**.
- Para a UWP (Windows 10), use o **Universal do Windows > Aplicativo em Branco (Universal do Windows)** em vez disso. Aceite os valores padrão para a Versão de Destino e a Versão Mínima quando solicitado.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Adicionar o pacote do NuGet Newtonsoft.Json

1. No Gerenciador de Soluções, clique com botão direito do mouse em **Referências** e escolha **Gerenciar pacotes do NuGet**.

    ![Gerenciar o comando de pacotes do NuGet para referências de projeto](media/QS_Use-02-ManageNuGetPackages.png)

1. Escolha “nuget.org” como a **Origem do pacote**, selecione a guia **Procurar**, pesquise por **Newtonsoft.Json**, selecione o pacote na lista e escolha **Instalar**:

    ![Localizando o pacote Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. Se solicitado para escolher um formato de gerenciamento de pacote, escolha entre PackageReference (recomendado) e `packages.config`:

    ![Selecionando um formato de referência de pacote](media/QS_Use-03b-SelectFormat.png)

1. Se for solicitado para examinar as alterações, selecione **OK**.

1. Clique com o botão direito do mouse na solução no Gerenciador de Soluções e selecione **Compilar Solução**. Isso restaura todos os pacotes do NuGet listados em **Referências**. Para obter mais detalhes, consulte [Restauração de pacotes](../consume-packages/package-restore.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Use a API Newtonsoft.Json no aplicativo

Com o pacote Newtonsoft.Json no projeto, você pode chamar seu método `JsonConvert.SerializeObject` para converter um objeto em uma cadeia de caracteres legível.

1. Abra `MainWindow.xaml` (WPF) ou `MainPage.xaml` (UWP) e substitua o elemento `Grid` pelo seguinte:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Expanda o nó `MainWindow.xaml` (WPF) ou `MainPage.xaml` (UWP) no Gerenciador de Soluções, abra o arquivo `.cs` e insira o seguinte código dentro da classe `MainWindow` ou `MainPage`, após o construtor:

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

1. Mesmo que você tenha adicionado o pacote Newtonsoft.Json ao projeto, o sublinhado vermelho aparecerá sob `JsonConvert` porque você precisa de uma instrução `using`. Passe o mouse sobre o `JsonConvert` sublinhado e você verá a Lâmpada e a opção para **Mostrar possíveis correções**:

    ![Lâmpada com comando exibir correções em potencial](media/QS_Use-04-ShowPotentialFixes.png)


1. Clique em **Mostrar possíveis correções** (ou na Lâmpada) e selecione a primeira correção sugerida, `using Newtonsoft.Json;`. Isso adiciona a linha necessária na parte superior do arquivo.

    ![Lâmpada oferecendo a opção de adicionar uma instrução using](media/QS_Use-05-AddUsing.png)

1. Build e execute o aplicativo pressionando F5 ou selecionando **Depurar > Iniciar a depuração** ( o UWP é mostrado aqui; o WPF é semelhante):

    ![Saída inicial do aplicativo UWP](media/QS_Use-06-AppStart.png)

1. Selecione o botão para ver o conteúdo do TextBlock substituído com algum texto JSON:

    ![Saída do aplicativo UWP depois de selecionar o botão](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a>Tópicos relacionados

- [Visão geral e fluxo de trabalho do consumo de pacote](../consume-packages/overview-and-workflow.md)
- [Localizando e escolhendo pacotes](../consume-packages/finding-and-choosing-packages.md)
- [Configurando o Comportamento de NuGet](../consume-packages/configuring-nuget-behavior.md)
