---
title: Instale e use um pacote NuGet no Visual Studio para Mac
description: Um tutorial passo a passo sobre o processo de instalação e uso de um pacote NuGet em um projeto do Visual Studio for Mac.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238472"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a><span data-ttu-id="aaf3c-103">Quickstart: Instale e use um pacote no Visual Studio para Mac</span><span class="sxs-lookup"><span data-stu-id="aaf3c-103">Quickstart: Install and use a package in Visual Studio for Mac</span></span>

<span data-ttu-id="aaf3c-104">Os pacotes NuGet contém código reutilizável que outros desenvolvedores disponibilizam para uso em seus projetos.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="aaf3c-105">Consulte [O que há de novo no NuGet](../What-is-NuGet.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="aaf3c-106">Os pacotes são instalados em um projeto do Visual Studio for Mac usando o NuGet Package Manager.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-106">Packages are installed into a Visual Studio for Mac project using the NuGet Package Manager.</span></span> <span data-ttu-id="aaf3c-107">Este artigo demonstra o processo usando o popular pacote [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) e um projeto de console .NET Core.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a .NET Core console project.</span></span> <span data-ttu-id="aaf3c-108">O mesmo processo se aplica a qualquer outro projeto Xamarin ou .NET Core.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-108">The same process applies to any other Xamarin or .NET Core project.</span></span>

<span data-ttu-id="aaf3c-109">Depois de instalado, consulte o pacote no código com `using <namespace>` em que \<namespace\> é específico para o pacote que você está usando.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="aaf3c-110">Depois que a referência é feita, você pode chamar o pacote por meio de sua API.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="aaf3c-111">**Comece com nuget.org**: Navegar *nuget.org* é como os desenvolvedores do .NET normalmente encontram componentes que podem reutilizar em seus próprios aplicativos.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="aaf3c-112">Você pode pesquisar no *nuget.org* diretamente ou localizar e instalar pacotes de dentro do Visual Studio, conforme mostrado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="aaf3c-113">Para saber mais, confira [Localizar e avaliar pacotes do NuGet](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="aaf3c-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aaf3c-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="aaf3c-114">Prerequisites</span></span>

- <span data-ttu-id="aaf3c-115">Visual Studio 2019 para Mac.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-115">Visual Studio 2019 for Mac.</span></span>

<span data-ttu-id="aaf3c-116">É possível instalar a edição Community 2019 gratuitamente em [visualstudio.com](https://www.visualstudio.com/) ou usar as edições Professional ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="aaf3c-117">Se você estiver usando o Visual Studio no Windows, consulte [Instalar e usar um pacote no Visual Studio (Somente windows)](install-and-use-a-package-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="aaf3c-117">If you're using Visual Studio on Windows, see [Install and use a package in Visual Studio (Windows Only)](install-and-use-a-package-in-visual-studio.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="aaf3c-118">Criar um projeto</span><span class="sxs-lookup"><span data-stu-id="aaf3c-118">Create a project</span></span>

<span data-ttu-id="aaf3c-119">É possível instalar pacotes do NuGet em qualquer projeto .NET, desde que o pacote ofereça suporte à mesma estrutura de destino do projeto.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="aaf3c-120">Para este passo a passo, use um aplicativo simples .NET Core Console.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-120">For this walkthrough, use a simple .NET Core Console app.</span></span> <span data-ttu-id="aaf3c-121">Crie um projeto no Visual Studio para Mac usando **file > New Solution...**, selecione o modelo **de aplicativo > de > console do .NET Core.**</span><span class="sxs-lookup"><span data-stu-id="aaf3c-121">Create a project in Visual Studio for Mac using **File > New Solution...**, select the **.NET Core > App > Console Application** template.</span></span> <span data-ttu-id="aaf3c-122">Clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-122">Click **Next**.</span></span> <span data-ttu-id="aaf3c-123">Aceite os valores padrão para **O Quadro de destino** quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-123">Accept the default values for **Target Framework** when prompted.</span></span>

<span data-ttu-id="aaf3c-124">O Visual Studio criará o projeto, que será aberto no Gerenciador de Soluções.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="aaf3c-125">Adicionar o pacote do NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="aaf3c-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="aaf3c-126">Para instalar o pacote, use o NuGet Package Manager.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-126">To install the package, you use the NuGet Package Manager.</span></span> <span data-ttu-id="aaf3c-127">Quando você instala um pacote, o NuGet registra a `packages.config` dependência no arquivo do projeto ou em um arquivo (dependendo do formato do projeto).</span><span class="sxs-lookup"><span data-stu-id="aaf3c-127">When you install a package, NuGet records the dependency in  either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="aaf3c-128">Para obter mais informações, veja [Visão geral e fluxo de trabalho do consumo de pacote](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="aaf3c-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="aaf3c-129">Gerenciador de Pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="aaf3c-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="aaf3c-130">No Solution Explorer, clique com o botão direito do mouse **em Dependências** e escolha **Adicionar pacotes...**.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-130">In Solution Explorer, right-click **Dependencies** and choose **Add Packages...**.</span></span>

    ![Gerenciar o comando de pacotes do NuGet para referências de projeto](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. <span data-ttu-id="aaf3c-132">Escolha "nuget.org" como a **fonte do Pacote** no canto superior esquerdo da caixa de diálogo e procure por **Newtonsoft.Json**, selecione esse pacote na lista e selecione **Adicionar pacotes...**:</span><span class="sxs-lookup"><span data-stu-id="aaf3c-132">Choose "nuget.org" as the **Package source** in the top left corner of the dialog, and search for **Newtonsoft.Json**, select that package in the list, and select **Add Packages...**:</span></span>

    ![Localizando o pacote Newtonsoft.Json](media/QS_Use_Mac-03-NewtonsoftJson.png)

    <span data-ttu-id="aaf3c-134">Se você quiser mais informações sobre o NuGet Package Manager, consulte [Instalar e gerenciar pacotes usando o Visual Studio para Mac](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="aaf3c-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="aaf3c-135">Use a API Newtonsoft.Json no aplicativo</span><span class="sxs-lookup"><span data-stu-id="aaf3c-135">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="aaf3c-136">Com o pacote Newtonsoft.Json no projeto, você pode chamar seu método `JsonConvert.SerializeObject` para converter um objeto em uma cadeia de caracteres legível.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-136">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="aaf3c-137">Abra `Program.cs` o arquivo (localizado no Bloco de solução) e substitua o conteúdo do arquivo pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="aaf3c-137">Open the `Program.cs` file (located in the Solution Pad) and replace the file contents with the following code:</span></span>

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. <span data-ttu-id="aaf3c-138">Construa e execute o aplicativo selecionando **Executar > Iniciar depuração**:</span><span class="sxs-lookup"><span data-stu-id="aaf3c-138">Build and run the app by selecting **Run > Start Debugging**:</span></span>

1. <span data-ttu-id="aaf3c-139">Uma vez que o aplicativo seja executado, você verá a saída JSON serializada aparecer no console:</span><span class="sxs-lookup"><span data-stu-id="aaf3c-139">Once the app runs, you'll see the serialized JSON output appear in the console:</span></span>

  ![Saída do aplicativo Console](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a><span data-ttu-id="aaf3c-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aaf3c-141">Next steps</span></span>
<span data-ttu-id="aaf3c-142">Parabéns por instalar e usar seu primeiro pacote do NuGet!</span><span class="sxs-lookup"><span data-stu-id="aaf3c-142">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aaf3c-143">Instale e gerencie pacotes usando o Visual Studio para Mac</span><span class="sxs-lookup"><span data-stu-id="aaf3c-143">Install and manage packages using Visual Studio for Mac</span></span>](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

<span data-ttu-id="aaf3c-144">Para ver o que mais o NuGet tem a oferecer, selecione os links abaixo.</span><span class="sxs-lookup"><span data-stu-id="aaf3c-144">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="aaf3c-145">Visão geral e fluxo de trabalho do consumo de pacote</span><span class="sxs-lookup"><span data-stu-id="aaf3c-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="aaf3c-146">Referências de pacotes em arquivos de projeto</span><span class="sxs-lookup"><span data-stu-id="aaf3c-146">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
