---
title: "Guia de introdução ao uso de pacotes NuGet no Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Um tutorial passo a passo sobre o processo de instalação e uso de um pacote NuGet em um projeto do Visual Studio."
keywords: "instalar o NuGet, consumo de pacote do NuGet, instalando pacotes do NuGet, referências de pacote do NuGet, usando pacotes do NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ff905fec6d6af4fa40fd4331cb970121b6eb0879
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2018
---
# <a name="install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="2edc4-104">Instalar e usar um pacote no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2edc4-104">Install and use a package in Visual Studio</span></span>

<span data-ttu-id="2edc4-105">Os pacotes NuGet contém código reutilizável que outros desenvolvedores disponibilizam para uso em seus projetos.</span><span class="sxs-lookup"><span data-stu-id="2edc4-105">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="2edc4-106">Consulte [O que há de novo no NuGet](../What-is-NuGet.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="2edc4-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="2edc4-107">Pacotes são instalados em um projeto do Visual Studio usando a IU do Gerenciador de Pacotes ou o Console do Gerenciador de Pacotes, conforme descrito neste artigo para o pacote popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) e um projeto da UWP (Plataforma Universal do Windows).</span><span class="sxs-lookup"><span data-stu-id="2edc4-107">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console, as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span>

<span data-ttu-id="2edc4-108">Depois de instalado, consulte o pacote no código com `using <namespace>` em que \<namespace\> é específico para o pacote que você está usando.</span><span class="sxs-lookup"><span data-stu-id="2edc4-108">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="2edc4-109">Depois que a referência é feita, você pode chamar o pacote por meio de sua API.</span><span class="sxs-lookup"><span data-stu-id="2edc4-109">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="2edc4-110">**Começar com nuget.org**: normalmente, os desenvolvedores em .NET encontram os componentes que podem reutilizar em seus próprios aplicativos procurando no nuget.org.</span><span class="sxs-lookup"><span data-stu-id="2edc4-110">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="2edc4-111">Você pode pesquisar no nuget.org diretamente ou localizar e instalar pacotes de dentro do Visual Studio, conforme mostrado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2edc4-111">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2edc4-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2edc4-112">Prerequisites</span></span>

- <span data-ttu-id="2edc4-113">Visual Studio 2017 com a carga de trabalho de desenvolvimento da Plataforma Universal do Windows, ou</span><span class="sxs-lookup"><span data-stu-id="2edc4-113">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="2edc4-114">Visual Studio 2015 Atualização 3 com Ferramentas para Aplicativos Universais do Windows.</span><span class="sxs-lookup"><span data-stu-id="2edc4-114">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="2edc4-115">Você pode instalar a edição Community 2017 gratuitamente no [visualstudio.com](https://www.visualstudio.com/) ou usar as edições Professional ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="2edc4-115">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="2edc4-116">Criar um projeto</span><span class="sxs-lookup"><span data-stu-id="2edc4-116">Create a project</span></span>

<span data-ttu-id="2edc4-117">Os pacotes NuGet podem ser instalados em algum tipo de projeto do .NET.</span><span class="sxs-lookup"><span data-stu-id="2edc4-117">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="2edc4-118">Para este passo a passo, use um aplicativo UWP (Plataforma Universal do Windows).</span><span class="sxs-lookup"><span data-stu-id="2edc4-118">For this walkthrough, you use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="2edc4-119">Crie um projeto no Visual Studio usando **Arquivo > Novo Projeto...** e selecionando **Universal do Windows > Aplicativo em Branco (Universal do Windows)**.</span><span class="sxs-lookup"><span data-stu-id="2edc4-119">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="2edc4-120">Aceite os valores padrão para a Versão de Destino e a Versão Mínima quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="2edc4-120">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="2edc4-121">Adicionar o pacote do NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="2edc4-121">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="2edc4-122">Para instalar o pacote, use a IU do Gerenciador de Pacotes ou o Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="2edc4-122">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="2edc4-123">Ao instalar um pacote, o NuGet registrará a dependência no arquivo de projeto ou em um arquivo `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="2edc4-123">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="2edc4-124">Para obter mais informações, veja [Visão geral e fluxo de trabalho do consumo de pacote](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="2edc4-124">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="2edc4-125">Interface do usuário do Gerenciador de Pacotes</span><span class="sxs-lookup"><span data-stu-id="2edc4-125">Package Manager UI</span></span>

1. <span data-ttu-id="2edc4-126">No Gerenciador de Soluções, clique com botão direito do mouse em **Referências** e escolha **Gerenciar pacotes do NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2edc4-126">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Gerenciar o comando de pacotes do NuGet para referências de projeto](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="2edc4-128">Escolha “nuget.org” como a **Origem do pacote**, selecione a guia **Procurar**, pesquise por **Newtonsoft.Json**, selecione o pacote na lista e escolha **Instalar**:</span><span class="sxs-lookup"><span data-stu-id="2edc4-128">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Localizando o pacote Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="2edc4-130">Aceite quaisquer avisos de licença.</span><span class="sxs-lookup"><span data-stu-id="2edc4-130">Accept any license prompts.</span></span>

1. <span data-ttu-id="2edc4-131">(Visual Studio 2017) Se receber uma solicitação para selecionar um formato de gerenciamento de pacote, selecione **PackageReference no arquivo de projeto**:</span><span class="sxs-lookup"><span data-stu-id="2edc4-131">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Selecionando um formato de referência de pacote](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="2edc4-133">Se for solicitado para examinar as alterações, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="2edc4-133">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="2edc4-134">Console do Gerenciador de Pacotes</span><span class="sxs-lookup"><span data-stu-id="2edc4-134">Package Manager Console</span></span>

1. <span data-ttu-id="2edc4-135">Selecione o comando do menu **Ferramentas > Gerenciador de Pacotes NuGet > Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="2edc4-135">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="2edc4-136">Após a abertura do console, verifique se a lista suspensa **Projeto padrão** mostra o projeto no qual você deseja instalar o pacote.</span><span class="sxs-lookup"><span data-stu-id="2edc4-136">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="2edc4-137">Se você tiver um único projeto na solução, ele já estará selecionado.</span><span class="sxs-lookup"><span data-stu-id="2edc4-137">If you have a single project in the solution, it is already selected.</span></span>

    ![Localizando o pacote Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="2edc4-139">Insira o comando `Install-Package Newtonsoft.json` (veja [Install-Package](../tools/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="2edc4-139">Enter the command `Install-Package Newtonsoft.json` (see [Install-Package](../tools/ps-ref-install-package.md)).</span></span> <span data-ttu-id="2edc4-140">A janela do console mostra a saída do comando.</span><span class="sxs-lookup"><span data-stu-id="2edc4-140">The console window shows output for the command.</span></span> <span data-ttu-id="2edc4-141">Os erros indicam que o pacote não é compatível com a estrutura de destino do projeto.</span><span class="sxs-lookup"><span data-stu-id="2edc4-141">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="2edc4-142">Use a API Newtonsoft.Json no aplicativo</span><span class="sxs-lookup"><span data-stu-id="2edc4-142">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="2edc4-143">Com o pacote Newtonsoft.Json no projeto, você pode chamar seu método `JsonConvert.SerializeObject` para converter um objeto em uma cadeia de caracteres legível.</span><span class="sxs-lookup"><span data-stu-id="2edc4-143">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="2edc4-144">Abra `MainPage.xaml` e substitua o elemento `Grid` existente pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="2edc4-144">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="2edc4-145">Abra o arquivo `MainPage.xaml.cs` (localizado no Gerenciador de Soluções no nó `MainPage.xaml`) e insira o seguinte código dentro do construtor `MainPage`:</span><span class="sxs-lookup"><span data-stu-id="2edc4-145">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

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

1. <span data-ttu-id="2edc4-146">Mesmo que você tenha adicionado o pacote Newtonsoft.Json ao projeto, o sublinhado vermelho aparecerá sob `JsonConvert` porque você precisa de uma instrução `using` no topo do arquivo de código:</span><span class="sxs-lookup"><span data-stu-id="2edc4-146">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.json;
    ```

1. <span data-ttu-id="2edc4-147">Compile e execute o aplicativo pressionando F5 ou selecionando **Depurar > Iniciar a Depuração**:</span><span class="sxs-lookup"><span data-stu-id="2edc4-147">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![Saída inicial do aplicativo UWP](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="2edc4-149">Selecione o botão para ver o conteúdo do TextBlock substituído com algum texto JSON:</span><span class="sxs-lookup"><span data-stu-id="2edc4-149">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Saída do aplicativo UWP depois de selecionar o botão](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="2edc4-151">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="2edc4-151">Related articles</span></span>

- [<span data-ttu-id="2edc4-152">Visão geral e fluxo de trabalho do consumo de pacote</span><span class="sxs-lookup"><span data-stu-id="2edc4-152">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="2edc4-153">Localizando e escolhendo pacotes</span><span class="sxs-lookup"><span data-stu-id="2edc4-153">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="2edc4-154">Maneiras de instalar um pacote</span><span class="sxs-lookup"><span data-stu-id="2edc4-154">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="2edc4-155">Configurando o Comportamento de NuGet</span><span class="sxs-lookup"><span data-stu-id="2edc4-155">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
