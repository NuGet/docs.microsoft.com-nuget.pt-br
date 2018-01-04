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
# <a name="install-and-use-a-package"></a><span data-ttu-id="2df44-104">Instalar e usar um pacote</span><span class="sxs-lookup"><span data-stu-id="2df44-104">Install and use a package</span></span>

[!INCLUDE [install-methods](../includes/install-methods.md)]

<span data-ttu-id="2df44-105">Depois de instalado, consulte o pacote no código com `using <namespace>` em que \<namespace\> é específico para o pacote que você está usando.</span><span class="sxs-lookup"><span data-stu-id="2df44-105">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="2df44-106">Depois que a referência é feita, você pode chamar o pacote por meio de sua API.</span><span class="sxs-lookup"><span data-stu-id="2df44-106">Once the reference is made, you can call the package through its API.</span></span>

<span data-ttu-id="2df44-107">O restante deste tópico explica o processo de usar a interface do usuário do Gerenciador de Pacotes para instalar o popular pacote [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) em um projeto da UWP (Plataforma Universal do Windows).</span><span class="sxs-lookup"><span data-stu-id="2df44-107">The remainder of this topic walks through the process of using the Package Manager UI to install the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package in a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="2df44-108">Ele mostra um exemplo de como usar o pacote.</span><span class="sxs-lookup"><span data-stu-id="2df44-108">It then shows an example of using the package.</span></span> <span data-ttu-id="2df44-109">Você pode usar um fluxo de trabalho semelhante para praticamente todos os pacotes do NuGet usados em um projeto.</span><span class="sxs-lookup"><span data-stu-id="2df44-109">You use a similar same workflow for virtually every NuGet package you use in a project.</span></span>

- [<span data-ttu-id="2df44-110">Instalar os pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2df44-110">Install pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="2df44-111">Criar um projeto</span><span class="sxs-lookup"><span data-stu-id="2df44-111">Create a project</span></span>](#create-a-project)
- [<span data-ttu-id="2df44-112">Adicionar o pacote do NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="2df44-112">Add the Newtonsoft.Json NuGet package</span></span>](#add-the-newtonsoftjson-nuget-package)
- [<span data-ttu-id="2df44-113">Use a API Newtonsoft.Json no aplicativo</span><span class="sxs-lookup"><span data-stu-id="2df44-113">Use the Newtonsoft.Json API in the app</span></span>](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> <span data-ttu-id="2df44-114">**Iniciar com nuget.org**: a instalação de pacotes do nuget.org é um fluxo de trabalho comum que os desenvolvedores de .NET usam para encontrar componentes que podem ser reutilizados em seus próprios aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2df44-114">**Start with nuget.org**: Installing packages from nuget.org is a common workflow that .NET developers use to find components they can reuse in their own applications.</span></span> <span data-ttu-id="2df44-115">Você sempre pode pesquisar no nuget.org diretamente ou localizar e instalar pacotes de dentro do Visual Studio, conforme mostrado neste tópico.</span><span class="sxs-lookup"><span data-stu-id="2df44-115">You can always search nuget.org directly or find and install packages within Visual Studio as shown in this topic.</span></span>

## <a name="install-pre-requisites"></a><span data-ttu-id="2df44-116">Instalar os pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2df44-116">Install pre-requisites</span></span>

<span data-ttu-id="2df44-117">Este tutorial requer o Visual Studio 2015 Atualização 3 com as Ferramentas para Aplicativos Universais do Windows ou Visual Studio 2017 com a carga de trabalho de desenvolvimento da Plataforma Universal do Windows.</span><span class="sxs-lookup"><span data-stu-id="2df44-117">This tutorial requires Visual Studio 2015 Update 3 with Tools for Universal Windows Apps, or Visual Studio 2017 with the Universal Windows Platform development workload.</span></span> <span data-ttu-id="2df44-118">Se você já tiver o Visual Studio instalado, execute o instalador novamente para adicionar as ferramentas UWP.</span><span class="sxs-lookup"><span data-stu-id="2df44-118">If you already have Visual Studio installed, you can run the installer again to add the UWP tools.</span></span>

<span data-ttu-id="2df44-119">Você pode instalar a edição Community gratuitamente no [visualstudio.com](https://www.visualstudio.com/) ou usar as edições Professional ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="2df44-119">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span> 

## <a name="create-a-project"></a><span data-ttu-id="2df44-120">Criar um projeto</span><span class="sxs-lookup"><span data-stu-id="2df44-120">Create a project</span></span>

<span data-ttu-id="2df44-121">Para instalar um pacote do NuGet, você precisa alguns tipos de projetos baseados em .NET no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2df44-121">To install a NuGet package, you need some kind of .NET-based project in Visual Studio.</span></span> <span data-ttu-id="2df44-122">Para este passo a passo, você pode usar um aplicativo simples do WPF (Windows Presentation Foundation) ou UWP (Universal do Windows):</span><span class="sxs-lookup"><span data-stu-id="2df44-122">For this walkthrough, you can use use a simple Windows Presentation Foundation (WPF) or Universal Windows (UWP) app:</span></span>

- <span data-ttu-id="2df44-123">Para WPF (Windows 7 ou superior), escolha **Arquivo > Novo > Projeto**, expanda **Visual C#**, selecione **Área de Trabalho Clássica do Windows > Aplicativo WPF (.NET Framework)** e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="2df44-123">For WPF (Windows 7+), choose **File > New > Project**, expand **Visual C#**, select **Windows Classic Desktop > WPF App (.NET Framework)**, and select **OK**.</span></span>
- <span data-ttu-id="2df44-124">Para a UWP (Windows 10), use o **Universal do Windows > Aplicativo em Branco (Universal do Windows)** em vez disso.</span><span class="sxs-lookup"><span data-stu-id="2df44-124">For UWP (Windows 10), use the **Windows Universal > Blank App (Universal Windows)** instead.</span></span> <span data-ttu-id="2df44-125">Aceite os valores padrão para a Versão de Destino e a Versão Mínima quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="2df44-125">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="2df44-126">Adicionar o pacote do NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="2df44-126">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="2df44-127">No Gerenciador de Soluções, clique com botão direito do mouse em **Referências** e escolha **Gerenciar pacotes do NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2df44-127">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Gerenciar o comando de pacotes do NuGet para referências de projeto](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="2df44-129">Escolha “nuget.org” como a **Origem do pacote**, selecione a guia **Procurar**, pesquise por **Newtonsoft.Json**, selecione o pacote na lista e escolha **Instalar**:</span><span class="sxs-lookup"><span data-stu-id="2df44-129">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Localizando o pacote Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="2df44-131">Se solicitado para escolher um formato de gerenciamento de pacote, escolha entre PackageReference (recomendado) e `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="2df44-131">If prompted to select a package management format, choose between PackageReference (recommended) and `packages.config`:</span></span>

    ![Selecionando um formato de referência de pacote](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="2df44-133">Se for solicitado para examinar as alterações, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="2df44-133">If prompted to review changes, select **OK**.</span></span>

1. <span data-ttu-id="2df44-134">Clique com o botão direito do mouse na solução no Gerenciador de Soluções e selecione **Compilar Solução**.</span><span class="sxs-lookup"><span data-stu-id="2df44-134">Right-click the solution in Solution Explorer and select **Build Solution**.</span></span> <span data-ttu-id="2df44-135">Isso restaura todos os pacotes do NuGet listados em **Referências**.</span><span class="sxs-lookup"><span data-stu-id="2df44-135">This restores any NuGet packages listed under **References**.</span></span> <span data-ttu-id="2df44-136">Para obter mais detalhes, consulte [Restauração de pacotes](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="2df44-136">For more details, see [Package Restore](../consume-packages/package-restore.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="2df44-137">Use a API Newtonsoft.Json no aplicativo</span><span class="sxs-lookup"><span data-stu-id="2df44-137">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="2df44-138">Com o pacote Newtonsoft.Json no projeto, você pode chamar seu método `JsonConvert.SerializeObject` para converter um objeto em uma cadeia de caracteres legível.</span><span class="sxs-lookup"><span data-stu-id="2df44-138">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="2df44-139">Abra `MainWindow.xaml` (WPF) ou `MainPage.xaml` (UWP) e substitua o elemento `Grid` pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="2df44-139">Open `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="2df44-140">Expanda o nó `MainWindow.xaml` (WPF) ou `MainPage.xaml` (UWP) no Gerenciador de Soluções, abra o arquivo `.cs` e insira o seguinte código dentro da classe `MainWindow` ou `MainPage`, após o construtor:</span><span class="sxs-lookup"><span data-stu-id="2df44-140">Expand the `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) node in Solution Explorer, open the `.cs` file, and insert the following code inside the `MainWindow` or `MainPage` class, after the constructor:</span></span>

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

1. <span data-ttu-id="2df44-141">Mesmo que você tenha adicionado o pacote Newtonsoft.Json ao projeto, o sublinhado vermelho aparecerá sob `JsonConvert` porque você precisa de uma instrução `using`.</span><span class="sxs-lookup"><span data-stu-id="2df44-141">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement.</span></span> <span data-ttu-id="2df44-142">Passe o mouse sobre o `JsonConvert` sublinhado e você verá a Lâmpada e a opção para **Mostrar possíveis correções**:</span><span class="sxs-lookup"><span data-stu-id="2df44-142">Hover over the underlined `JsonConvert` and you'll see the Lightbulb and the option to **Show potential fixes**:</span></span>

    ![Lâmpada com comando exibir correções em potencial](media/QS_Use-04-ShowPotentialFixes.png)


1. <span data-ttu-id="2df44-144">Clique em **Mostrar possíveis correções** (ou na Lâmpada) e selecione a primeira correção sugerida, `using Newtonsoft.Json;`.</span><span class="sxs-lookup"><span data-stu-id="2df44-144">Click on **Show potential fixes** (or the Lightbulb) and select the first suggested fix, `using Newtonsoft.Json;`.</span></span> <span data-ttu-id="2df44-145">Isso adiciona a linha necessária na parte superior do arquivo.</span><span class="sxs-lookup"><span data-stu-id="2df44-145">This adds the necessary line to the top of the file.</span></span>

    ![Lâmpada oferecendo a opção de adicionar uma instrução using](media/QS_Use-05-AddUsing.png)

1. <span data-ttu-id="2df44-147">Build e execute o aplicativo pressionando F5 ou selecionando **Depurar > Iniciar a depuração** ( o UWP é mostrado aqui; o WPF é semelhante):</span><span class="sxs-lookup"><span data-stu-id="2df44-147">Build and run the app by pressing F5 or selecting **Debug > Start Debugging** (UWP shown here; WPF is similar):</span></span>

    ![Saída inicial do aplicativo UWP](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="2df44-149">Selecione o botão para ver o conteúdo do TextBlock substituído com algum texto JSON:</span><span class="sxs-lookup"><span data-stu-id="2df44-149">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Saída do aplicativo UWP depois de selecionar o botão](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a><span data-ttu-id="2df44-151">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="2df44-151">Related topics</span></span>

- [<span data-ttu-id="2df44-152">Visão geral e fluxo de trabalho do consumo de pacote</span><span class="sxs-lookup"><span data-stu-id="2df44-152">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="2df44-153">Localizando e escolhendo pacotes</span><span class="sxs-lookup"><span data-stu-id="2df44-153">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="2df44-154">Configurando o Comportamento de NuGet</span><span class="sxs-lookup"><span data-stu-id="2df44-154">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
