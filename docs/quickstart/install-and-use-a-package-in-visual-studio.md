---
title: Guia de introdução ao uso de pacotes do NuGet no Visual Studio
description: Um tutorial passo a passo sobre o processo de instalação e uso de um pacote NuGet em um projeto do Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 014b316ea03b45584406c313d46b96ad36340124
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426225"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="0c8b2-103">Início Rápido: Instalar e usar um pacote no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0c8b2-103">Quickstart: Install and use a package in Visual Studio</span></span>

<span data-ttu-id="0c8b2-104">Os pacotes NuGet contém código reutilizável que outros desenvolvedores disponibilizam para uso em seus projetos.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="0c8b2-105">Consulte [O que há de novo no NuGet](../What-is-NuGet.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="0c8b2-106">Os pacotes são instalados em um projeto do Visual Studio usando a interface do usuário do Gerenciador de Pacotes ou o Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-106">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="0c8b2-107">Este artigo demonstra o processo usando o conhecido pacote [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) e um projeto da UWP (Plataforma Universal do Windows).</span><span class="sxs-lookup"><span data-stu-id="0c8b2-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="0c8b2-108">O mesmo processo se aplica a qualquer outro projeto .NET ou .NET Core.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="0c8b2-109">Depois de instalado, consulte o pacote no código com `using <namespace>` em que \<namespace\> é específico para o pacote que você está usando.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="0c8b2-110">Depois que a referência é feita, você pode chamar o pacote por meio de sua API.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="0c8b2-111">**Começar no nuget.org**: normalmente, os desenvolvedores em .NET encontram componentes que podem reutilizar em seus próprios aplicativos procurando no nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-111">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="0c8b2-112">Você pode pesquisar no nuget.org diretamente ou localizar e instalar pacotes de dentro do Visual Studio, conforme mostrado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-112">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c8b2-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0c8b2-113">Prerequisites</span></span>

- <span data-ttu-id="0c8b2-114">Visual Studio 2017 com a carga de trabalho de desenvolvimento da Plataforma Universal do Windows, ou</span><span class="sxs-lookup"><span data-stu-id="0c8b2-114">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="0c8b2-115">Visual Studio 2015 Atualização 3 com Ferramentas para Aplicativos Universais do Windows.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-115">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="0c8b2-116">Você pode instalar a edição Community 2017 gratuitamente no [visualstudio.com](https://www.visualstudio.com/) ou usar as edições Professional ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-116">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="0c8b2-117">Se você estiver usando o Visual Studio para Mac, confira [Incluir um pacote do NuGet em seu projeto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="0c8b2-117">If you're using Visual Studio for Mac, see [Include a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="0c8b2-118">Criar um projeto</span><span class="sxs-lookup"><span data-stu-id="0c8b2-118">Create a project</span></span>

<span data-ttu-id="0c8b2-119">É possível instalar pacotes do NuGet em qualquer projeto .NET, desde que o pacote ofereça suporte à mesma estrutura de destino do projeto.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="0c8b2-120">Para este passo a passo, use um aplicativo da UWP (Plataforma Universal do Windows).</span><span class="sxs-lookup"><span data-stu-id="0c8b2-120">For this walkthrough, use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="0c8b2-121">Crie um projeto no Visual Studio usando **Arquivo > Novo Projeto...** e selecionando **Universal do Windows > Aplicativo em Branco (Universal do Windows)** .</span><span class="sxs-lookup"><span data-stu-id="0c8b2-121">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="0c8b2-122">Aceite os valores padrão para a Versão de Destino e a Versão Mínima quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-122">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="0c8b2-123">Adicionar o pacote do NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="0c8b2-123">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="0c8b2-124">Para instalar o pacote, use a IU do Gerenciador de Pacotes ou o Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-124">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="0c8b2-125">Ao instalar um pacote, o NuGet registrará a dependência no arquivo de projeto ou em um arquivo `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-125">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="0c8b2-126">Para obter mais informações, veja [Visão geral e fluxo de trabalho do consumo de pacote](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="0c8b2-126">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="0c8b2-127">Interface do usuário do Gerenciador de Pacotes</span><span class="sxs-lookup"><span data-stu-id="0c8b2-127">Package Manager UI</span></span>

1. <span data-ttu-id="0c8b2-128">No Gerenciador de Soluções, clique com botão direito do mouse em **Referências** e escolha **Gerenciar pacotes do NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-128">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Gerenciar o comando de pacotes do NuGet para referências de projeto](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="0c8b2-130">Escolha “nuget.org” como a **Origem do pacote**, selecione a guia **Procurar**, pesquise por **Newtonsoft.Json**, selecione o pacote na lista e escolha **Instalar**:</span><span class="sxs-lookup"><span data-stu-id="0c8b2-130">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Localizando o pacote Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="0c8b2-132">Aceite quaisquer avisos de licença.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-132">Accept any license prompts.</span></span>

1. <span data-ttu-id="0c8b2-133">(Visual Studio 2017) Se receber uma solicitação para selecionar um formato de gerenciamento de pacote, selecione **PackageReference no arquivo de projeto**:</span><span class="sxs-lookup"><span data-stu-id="0c8b2-133">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Como selecionar um formato de gerenciamento de pacote](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="0c8b2-135">Se for solicitado para examinar as alterações, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-135">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="0c8b2-136">Console do Gerenciador de Pacotes</span><span class="sxs-lookup"><span data-stu-id="0c8b2-136">Package Manager Console</span></span>

1. <span data-ttu-id="0c8b2-137">Selecione o comando do menu **Ferramentas > Gerenciador de Pacotes NuGet > Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-137">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="0c8b2-138">Após a abertura do console, verifique se a lista suspensa **Projeto padrão** mostra o projeto no qual você deseja instalar o pacote.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-138">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="0c8b2-139">Se você tiver um único projeto na solução, ele já estará selecionado.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-139">If you have a single project in the solution, it is already selected.</span></span>

    ![Localizando o pacote Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="0c8b2-141">Insira o comando `Install-Package Newtonsoft.Json` (veja [Install-Package](../tools/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="0c8b2-141">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../tools/ps-ref-install-package.md)).</span></span> <span data-ttu-id="0c8b2-142">A janela do console mostra a saída do comando.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-142">The console window shows output for the command.</span></span> <span data-ttu-id="0c8b2-143">Os erros indicam que o pacote não é compatível com a estrutura de destino do projeto.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-143">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="0c8b2-144">Use a API Newtonsoft.Json no aplicativo</span><span class="sxs-lookup"><span data-stu-id="0c8b2-144">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="0c8b2-145">Com o pacote Newtonsoft.Json no projeto, você pode chamar seu método `JsonConvert.SerializeObject` para converter um objeto em uma cadeia de caracteres legível.</span><span class="sxs-lookup"><span data-stu-id="0c8b2-145">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="0c8b2-146">Abra `MainPage.xaml` e substitua o elemento `Grid` existente pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="0c8b2-146">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="0c8b2-147">Abra o arquivo `MainPage.xaml.cs` (localizado no Gerenciador de Soluções no nó `MainPage.xaml`) e insira o seguinte código dentro do construtor `MainPage`:</span><span class="sxs-lookup"><span data-stu-id="0c8b2-147">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

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

1. <span data-ttu-id="0c8b2-148">Mesmo que você tenha adicionado o pacote Newtonsoft.Json ao projeto, o sublinhado vermelho aparecerá sob `JsonConvert` porque você precisa de uma instrução `using` no topo do arquivo de código:</span><span class="sxs-lookup"><span data-stu-id="0c8b2-148">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="0c8b2-149">Compile e execute o aplicativo pressionando F5 ou selecionando **Depurar > Iniciar a Depuração**:</span><span class="sxs-lookup"><span data-stu-id="0c8b2-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![Saída inicial do aplicativo UWP](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="0c8b2-151">Selecione o botão para ver o conteúdo do TextBlock substituído com algum texto JSON:</span><span class="sxs-lookup"><span data-stu-id="0c8b2-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Saída do aplicativo UWP depois de selecionar o botão](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="0c8b2-153">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="0c8b2-153">Related articles</span></span>

- [<span data-ttu-id="0c8b2-154">Visão geral e fluxo de trabalho do consumo de pacote</span><span class="sxs-lookup"><span data-stu-id="0c8b2-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="0c8b2-155">Instalar e gerenciar pacotes usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0c8b2-155">Install and manage packages using Visual Studio</span></span>](../tools/package-manager-ui.md)
- [<span data-ttu-id="0c8b2-156">Localizando e escolhendo pacotes</span><span class="sxs-lookup"><span data-stu-id="0c8b2-156">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="0c8b2-157">Configurações comuns do NuGet</span><span class="sxs-lookup"><span data-stu-id="0c8b2-157">Common NuGet configurations</span></span>](../consume-packages/configuring-nuget-behavior.md)
