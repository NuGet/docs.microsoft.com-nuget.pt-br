---
title: Instalar e usar um pacote do NuGet no Visual Studio
description: Um tutorial passo a passo sobre o processo de instalação e uso de um pacote NuGet em um projeto do Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 55f6a64d90ce8ca628d1ac5c68f8133872a214e0
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775528"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a><span data-ttu-id="af20a-103">Início rápido: instalar e usar um pacote no Visual Studio (somente Windows)</span><span class="sxs-lookup"><span data-stu-id="af20a-103">Quickstart: Install and use a package in Visual Studio (Windows only)</span></span>

<span data-ttu-id="af20a-104">Os pacotes NuGet contém código reutilizável que outros desenvolvedores disponibilizam para uso em seus projetos.</span><span class="sxs-lookup"><span data-stu-id="af20a-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="af20a-105">Consulte [O que há de novo no NuGet](../What-is-NuGet.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="af20a-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="af20a-106">Os pacotes são instalados em um projeto do Visual Studio usando o Gerenciador de pacotes NuGet, o [console do Gerenciador de pacotes](../consume-packages/install-use-packages-powershell.md)ou a CLI do [dotnet](install-and-use-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="af20a-106">Packages are installed into a Visual Studio project using the NuGet Package Manager, the [Package Manager Console](../consume-packages/install-use-packages-powershell.md), or the [dotnet CLI](install-and-use-a-package-using-the-dotnet-cli.md).</span></span> <span data-ttu-id="af20a-107">Este artigo demonstra o processo usando o conhecido pacote [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) e um projeto da WPF (Windows Presentation Foundation).</span><span class="sxs-lookup"><span data-stu-id="af20a-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Windows Presentation Foundation (WPF) project.</span></span> <span data-ttu-id="af20a-108">O mesmo processo se aplica a qualquer outro projeto .NET ou .NET Core.</span><span class="sxs-lookup"><span data-stu-id="af20a-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="af20a-109">Uma vez instalado, consulte o pacote em código com `using <namespace>` onde \<namespace\> é específico para o pacote que você está usando.</span><span class="sxs-lookup"><span data-stu-id="af20a-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="af20a-110">Depois que a referência é feita, você pode chamar o pacote por meio de sua API.</span><span class="sxs-lookup"><span data-stu-id="af20a-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="af20a-111">**Comece com NuGet.org**: navegar *NuGet.org* é como os desenvolvedores do .net normalmente localizam componentes que podem ser reutilizados em seus próprios aplicativos.</span><span class="sxs-lookup"><span data-stu-id="af20a-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="af20a-112">Você pode pesquisar no *nuget.org* diretamente ou localizar e instalar pacotes de dentro do Visual Studio, conforme mostrado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="af20a-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="af20a-113">Para saber mais, confira [Localizar e avaliar pacotes do NuGet](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="af20a-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af20a-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="af20a-114">Prerequisites</span></span>

- <span data-ttu-id="af20a-115">Visual Studio 2019 com a carga de trabalho do desenvolvimento para área de trabalho .NET.</span><span class="sxs-lookup"><span data-stu-id="af20a-115">Visual Studio 2019 with the .NET Desktop Development workload.</span></span>

<span data-ttu-id="af20a-116">É possível instalar a edição Community 2019 gratuitamente em [visualstudio.com](https://www.visualstudio.com/) ou usar as edições Professional ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="af20a-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="af20a-117">Se você estiver usando Visual Studio para Mac, consulte [instalar e usar um pacote no Visual Studio para Mac](install-and-use-a-package-in-visual-studio-mac.md).</span><span class="sxs-lookup"><span data-stu-id="af20a-117">If you're using Visual Studio for Mac, see [Install and use a package in Visual Studio for Mac](install-and-use-a-package-in-visual-studio-mac.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="af20a-118">Criar um projeto</span><span class="sxs-lookup"><span data-stu-id="af20a-118">Create a project</span></span>

<span data-ttu-id="af20a-119">É possível instalar pacotes do NuGet em qualquer projeto .NET, desde que o pacote ofereça suporte à mesma estrutura de destino do projeto.</span><span class="sxs-lookup"><span data-stu-id="af20a-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="af20a-120">Para esta explicação, use um aplicativo WPF simples.</span><span class="sxs-lookup"><span data-stu-id="af20a-120">For this walkthrough, use a simple WPF app.</span></span> <span data-ttu-id="af20a-121">Crie um projeto no Visual Studio usando **arquivo**  >  **novo projeto**, digitando **.net** na caixa de pesquisa e, em seguida, selecionando o **aplicativo do WPF (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="af20a-121">Create a project in Visual Studio using **File** > **New Project**, typing **.NET** in the search box, and then selecting the **WPF App (.NET Framework)**.</span></span> <span data-ttu-id="af20a-122">Clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="af20a-122">Click **Next**.</span></span> <span data-ttu-id="af20a-123">Aceite os valores padrão para **Estrutura** quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="af20a-123">Accept the default values for **Framework** when prompted.</span></span>

<span data-ttu-id="af20a-124">O Visual Studio criará o projeto, que será aberto no Gerenciador de Soluções.</span><span class="sxs-lookup"><span data-stu-id="af20a-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="af20a-125">Adicionar o pacote do NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="af20a-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="af20a-126">Para instalar o pacote, use o Gerenciador de pacotes do NuGet ou o Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="af20a-126">To install the package, you can use either the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="af20a-127">Ao instalar um pacote, o NuGet registra a dependência no arquivo de projeto ou em um arquivo `packages.config` (dependendo do formato do projeto).</span><span class="sxs-lookup"><span data-stu-id="af20a-127">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="af20a-128">Para obter mais informações, veja [Visão geral e fluxo de trabalho do consumo de pacote](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="af20a-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="af20a-129">Gerenciador de Pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="af20a-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="af20a-130">No Gerenciador de Soluções, clique com botão direito do mouse em **Referências** e escolha **Gerenciar pacotes do NuGet**.</span><span class="sxs-lookup"><span data-stu-id="af20a-130">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Gerenciar o comando de pacotes do NuGet para referências de projeto](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="af20a-132">Escolha “nuget.org” como a **Origem do pacote**, selecione a guia **Procurar**, pesquise por **Newtonsoft.Json**, selecione o pacote na lista e escolha **Instalar**:</span><span class="sxs-lookup"><span data-stu-id="af20a-132">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Localizando o pacote Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

    <span data-ttu-id="af20a-134">Se quiser saber mais sobre o Gerenciador de pacotes do NuGet, confira [Instalar e gerenciar pacotes usando o Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="af20a-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span></span>

1. <span data-ttu-id="af20a-135">Aceite quaisquer avisos de licença.</span><span class="sxs-lookup"><span data-stu-id="af20a-135">Accept any license prompts.</span></span>

1. <span data-ttu-id="af20a-136">(Somente no Visual Studio 2017) Se receber uma solicitação para selecionar um formato de gerenciamento de pacote, selecione **PackageReference no arquivo de projeto**:</span><span class="sxs-lookup"><span data-stu-id="af20a-136">(Visual Studio 2017 only) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Como selecionar um formato de gerenciamento de pacote](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="af20a-138">Se for solicitado para examinar as alterações, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="af20a-138">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="af20a-139">Console do Gerenciador de Pacotes</span><span class="sxs-lookup"><span data-stu-id="af20a-139">Package Manager Console</span></span>

1. <span data-ttu-id="af20a-140">Selecione o comando **ferramentas** Gerenciador de  >  **pacotes do NuGet**  >  **console do Gerenciador de pacotes** .</span><span class="sxs-lookup"><span data-stu-id="af20a-140">Select the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="af20a-141">Após a abertura do console, verifique se a lista suspensa **Projeto padrão** mostra o projeto no qual você deseja instalar o pacote.</span><span class="sxs-lookup"><span data-stu-id="af20a-141">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="af20a-142">Se você tiver um único projeto na solução, ele já estará selecionado.</span><span class="sxs-lookup"><span data-stu-id="af20a-142">If you have a single project in the solution, it is already selected.</span></span>

    ![Selecione um projeto para o pacote](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="af20a-144">Insira o comando `Install-Package Newtonsoft.Json` (veja [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="af20a-144">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="af20a-145">A janela do console mostra a saída do comando.</span><span class="sxs-lookup"><span data-stu-id="af20a-145">The console window shows output for the command.</span></span> <span data-ttu-id="af20a-146">Os erros indicam que o pacote não é compatível com a estrutura de destino do projeto.</span><span class="sxs-lookup"><span data-stu-id="af20a-146">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

   <span data-ttu-id="af20a-147">Se quiser saber mais sobre o Console do Gerenciador de Pacotes, confira [Instalar e gerenciar pacotes usando o Console do Gerenciador de Pacotes](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="af20a-147">If you want more information on the Package Manager Console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="af20a-148">Use a API Newtonsoft.Json no aplicativo</span><span class="sxs-lookup"><span data-stu-id="af20a-148">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="af20a-149">Com o pacote Newtonsoft.Json no projeto, você pode chamar seu método `JsonConvert.SerializeObject` para converter um objeto em uma cadeia de caracteres legível.</span><span class="sxs-lookup"><span data-stu-id="af20a-149">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="af20a-150">Abra `MainWindow.xaml` e substitua o elemento `Grid` existente pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="af20a-150">Open `MainWindow.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="af20a-151">Abra o arquivo `MainWindow.xaml.cs` (localizado no Gerenciador de Soluções sob o nó `MainWindow.xaml`) e insira o seguinte código dentro da classe `MainWindow`:</span><span class="sxs-lookup"><span data-stu-id="af20a-151">Open the `MainWindow.xaml.cs` file (located in Solution Explorer under the `MainWindow.xaml` node), and insert the following code inside the `MainWindow` class:</span></span>

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

1. <span data-ttu-id="af20a-152">Mesmo que você tenha adicionado o pacote Newtonsoft.Json ao projeto, o sublinhado vermelho aparecerá sob `JsonConvert` porque você precisa de uma instrução `using` no topo do arquivo de código:</span><span class="sxs-lookup"><span data-stu-id="af20a-152">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="af20a-153">Crie e execute o aplicativo pressionando F5 ou selecionando **depurar**  >  **Iniciar Depuração**:</span><span class="sxs-lookup"><span data-stu-id="af20a-153">Build and run the app by pressing F5 or selecting **Debug** > **Start Debugging**:</span></span>

    ![Saída inicial do aplicativo WPF](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="af20a-155">Selecione o botão para ver o conteúdo do TextBlock substituído com algum texto JSON:</span><span class="sxs-lookup"><span data-stu-id="af20a-155">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Saída do aplicativo WPF após selecionar o botão](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a><span data-ttu-id="af20a-157">Vídeo relacionado</span><span class="sxs-lookup"><span data-stu-id="af20a-157">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

<span data-ttu-id="af20a-158">Encontre mais vídeos sobre o NuGet no [Channel 9](https://channel9.msdn.com/Series/NuGet-101) e no [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="af20a-158">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="af20a-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="af20a-159">Next steps</span></span>

<span data-ttu-id="af20a-160">Parabéns por instalar e usar seu primeiro pacote do NuGet!</span><span class="sxs-lookup"><span data-stu-id="af20a-160">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="af20a-161">Instalar e gerenciar pacotes usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="af20a-161">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="af20a-162">Instalar e gerenciar pacotes usando o Console do gerenciador de pacote</span><span class="sxs-lookup"><span data-stu-id="af20a-162">Install and manage packages using Package Manager Console</span></span>](../consume-packages/install-use-packages-powershell.md)

<span data-ttu-id="af20a-163">Para ver o que mais o NuGet tem a oferecer, selecione os links abaixo.</span><span class="sxs-lookup"><span data-stu-id="af20a-163">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="af20a-164">Visão geral e fluxo de trabalho do consumo de pacote</span><span class="sxs-lookup"><span data-stu-id="af20a-164">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="af20a-165">Localizando e escolhendo pacotes</span><span class="sxs-lookup"><span data-stu-id="af20a-165">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="af20a-166">Referências de pacotes em arquivos de projeto</span><span class="sxs-lookup"><span data-stu-id="af20a-166">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
