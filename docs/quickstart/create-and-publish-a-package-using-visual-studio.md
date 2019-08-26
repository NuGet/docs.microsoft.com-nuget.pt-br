---
title: Criar e publicar um pacote NuGet do .NET Standard - Visual Studio no Windows
description: Um tutorial passo a passo sobre como criar e publicar um pacote NuGet do .NET Standard usando o Visual Studio no Windows.
author: karann-msft
ms.author: karann
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 9552f6c5291f950430bfb723cb713bf76a79ea66
ms.sourcegitcommit: 80cf99f40759911324468be1ec815c96aebf376d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2019
ms.locfileid: "69564598"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="97227-103">Início Rápido: Criar e publicar um pacote do NuGet usando o Visual Studio (.NET Standard somente no Windows)</span><span class="sxs-lookup"><span data-stu-id="97227-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="97227-104">Criar um pacote NuGet de uma Biblioteca de Classes .NET Standard no Visual Studio no Windows e, em seguida, publicá-lo no nuget.org usando uma ferramenta de CLI é um processo simples.</span><span class="sxs-lookup"><span data-stu-id="97227-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="97227-105">Se você estiver usando o Visual Studio para Mac, confira [essas informações](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) sobre como criar um pacote NuGet ou use as [ferramentas de CLI do dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="97227-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97227-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="97227-106">Prerequisites</span></span>

1. <span data-ttu-id="97227-107">Instale qualquer edição do Visual Studio 2019 de [visualstudio.com](https://www.visualstudio.com/) com uma carga de trabalho relacionada ao .NET Core.</span><span class="sxs-lookup"><span data-stu-id="97227-107">Install any edition of Visual Studio 2019 from [visualstudio.com](https://www.visualstudio.com/) with a .NET Core related workload.</span></span>

1. <span data-ttu-id="97227-108">Instale a CLI `dotnet`, se ainda não estiver instalada.</span><span class="sxs-lookup"><span data-stu-id="97227-108">If it's not already installed, install the `dotnet` CLI.</span></span>

   <span data-ttu-id="97227-109">Para a CLI do `dotnet`, a partir do Visual Studio 2017, a CLI do `dotnet` é instalada automaticamente com qualquer carga de trabalho relacionada ao .NET Core.</span><span class="sxs-lookup"><span data-stu-id="97227-109">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="97227-110">Caso contrário, instale o [SDK do .NET Core](https://www.microsoft.com/net/download/) para ter a CLI do `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="97227-110">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="97227-111">A CLI `dotnet` é necessária para projetos do .NET Standard que usam o [formato de estilo SDK](../resources/check-project-format.md) (atributo do SDK).</span><span class="sxs-lookup"><span data-stu-id="97227-111">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="97227-112">O modelo padrão de biblioteca de classes .NET Standard no Visual Studio 2017 e posterior, que é usado neste artigo, usa o atributo SDK.</span><span class="sxs-lookup"><span data-stu-id="97227-112">The default .NET Standard class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="97227-113">Se você estiver trabalhando com um projeto de estilo não SDK, siga os procedimentos em [Criar e publicar um pacote de .NET Framework (Visual Studio](create-and-publish-a-package-using-visual-studio-net-framework.md)) para criar e publicar o pacote.</span><span class="sxs-lookup"><span data-stu-id="97227-113">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package instead.</span></span> <span data-ttu-id="97227-114">Para este artigo, a CLI do `dotnet` recomendada.</span><span class="sxs-lookup"><span data-stu-id="97227-114">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="97227-115">Embora você possa publicar qualquer pacote NuGet usando a CLI do `nuget.exe`, algumas das etapas neste artigo são específicas para projetos no estilo SDK e a CLI do dotnet.</span><span class="sxs-lookup"><span data-stu-id="97227-115">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="97227-116">A CLI do nuget.exe é usada para [projetos de estilo não SDK](../resources/check-project-format.md) (normalmente .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="97227-116">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span>

1. <span data-ttu-id="97227-117">[Registre-se em uma conta gratuita em nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account), se ainda não tiver uma.</span><span class="sxs-lookup"><span data-stu-id="97227-117">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="97227-118">Criar uma nova conta envia um email de confirmação.</span><span class="sxs-lookup"><span data-stu-id="97227-118">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="97227-119">Você deve confirmar a conta antes de poder carregar um pacote.</span><span class="sxs-lookup"><span data-stu-id="97227-119">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="97227-120">Criar um projeto de biblioteca de classes</span><span class="sxs-lookup"><span data-stu-id="97227-120">Create a class library project</span></span>

<span data-ttu-id="97227-121">Você pode usar um projeto existente da Biblioteca de Classes .NET Standard para o código que você deseja empacotar ou criar um simples da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="97227-121">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="97227-122">No Visual Studio, escolha **Arquivo > Novo > Projeto**, expanda o nó **Visual C# > .NET Standard**, selecione o modelo de "Biblioteca de Classes (.NET Standard)", nomeie o projeto como AppLogger e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="97227-122">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

   > [!Tip]
   > <span data-ttu-id="97227-123">A menos que você tenha um motivo para a escolha de outro jeito, o .NET Standard é o destino preferencial para pacotes NuGet, pois fornece compatibilidade com a mais ampla variedade de projetos de consumo.</span><span class="sxs-lookup"><span data-stu-id="97227-123">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

1. <span data-ttu-id="97227-124">Clique com botão direito do mouse no arquivo de projeto resultante e selecione **Build** para verificar se o projeto foi criado corretamente.</span><span class="sxs-lookup"><span data-stu-id="97227-124">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="97227-125">A DLL é encontrada dentro da pasta de Depuração (ou Versão, se você compilar essa configuração).</span><span class="sxs-lookup"><span data-stu-id="97227-125">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="97227-126">Em um pacote NuGet real, obviamente, você implementa muitos recursos úteis com os quais outras pessoas podem compilar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="97227-126">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="97227-127">Para este passo a passo, no entanto, você não escreverá nenhum código adicional porque uma biblioteca de classes do modelo é suficiente para criar um pacote.</span><span class="sxs-lookup"><span data-stu-id="97227-127">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="97227-128">Ainda assim, se você desejar algum código funcional para o pacote, use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="97227-128">Still, if you'd like some functional code for the package, use the following:</span></span>

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

## <a name="configure-package-properties"></a><span data-ttu-id="97227-129">Configurar propriedades do pacote</span><span class="sxs-lookup"><span data-stu-id="97227-129">Configure package properties</span></span>

1. <span data-ttu-id="97227-130">Clique com o botão direito do mouse no projeto no Gerenciador de Soluções e escolha o comando de menu **Propriedades** e selecione a guia **Pacote**.</span><span class="sxs-lookup"><span data-stu-id="97227-130">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="97227-131">A guia **Pacote** é exibida apenas para projetos no estilo SDK no Visual Studio, normalmente .NET Standard ou projetos de biblioteca de classes do .NET Core; se você estiver direcionando para um projeto de estilo não SDK (normalmente, .NET Framework), [migre o projeto](../consume-packages/migrate-packages-config-to-package-reference.md) ou confira [Criar e publicar um pacote do .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) para ver as instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="97227-131">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../consume-packages/migrate-packages-config-to-package-reference.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Propriedades do pacote NuGet em um projeto do Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="97227-133">Para pacotes compilados para consumo público, preste atenção especial à propriedade **Tags**, à medida que as marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.</span><span class="sxs-lookup"><span data-stu-id="97227-133">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="97227-134">Dê ao seu pacote um identificador exclusivo e preencha as outras propriedades desejadas.</span><span class="sxs-lookup"><span data-stu-id="97227-134">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="97227-135">Para ver um mapeamento das propriedades do MSBuild (projeto no estilo SDK) para propriedades em um *.nuspec*, confira [alvos de pacote](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="97227-135">For a mapping of MSBuild properties (SDK-style project) to properties in a *.nuspec*, see [pack targets](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="97227-136">Para obter descrições de propriedades, confira a [referência do arquivo .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="97227-136">For descriptions of properties, see the [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="97227-137">Todas essas propriedades vão para o manifesto `.nuspec` que o Visual Studio cria para o projeto.</span><span class="sxs-lookup"><span data-stu-id="97227-137">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="97227-138">Você precisa dar ao pacote um identificador exclusivo em nuget.org ou qualquer host que você esteja usando.</span><span class="sxs-lookup"><span data-stu-id="97227-138">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="97227-139">Para este passo a passo, recomendamos incluir o "Sample" ou "Test" no nome, pois a etapa de publicação posterior torna o pacote publicamente visível (embora seja improvável que alguém possa usá-lo).</span><span class="sxs-lookup"><span data-stu-id="97227-139">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="97227-140">Se você tentar publicar um pacote com um nome que já existe, você verá um erro.</span><span class="sxs-lookup"><span data-stu-id="97227-140">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="97227-141">(Opcional) Para ver as propriedades diretamente no arquivo de projeto, clique com o botão direito do mouse no projeto no Gerenciador de Soluções e selecione **Editar AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="97227-141">(Optional) To see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="97227-142">Essa opção só está disponível a partir do Visual Studio 2017 para projetos que usam o atributo de estilo SDK.</span><span class="sxs-lookup"><span data-stu-id="97227-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="97227-143">Caso contrário, clique com o botão direito do mouse no projeto e escolha **Descarregar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="97227-143">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="97227-144">Em seguida, clique com o botão direito do mouse no projeto descarregado e escolha **Editar AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="97227-144">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="97227-145">Executar o comando pack</span><span class="sxs-lookup"><span data-stu-id="97227-145">Run the pack command</span></span>

1. <span data-ttu-id="97227-146">Defina a configuração da solução como **Release**.</span><span class="sxs-lookup"><span data-stu-id="97227-146">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="97227-147">Clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e selecione o comando **Pack**:</span><span class="sxs-lookup"><span data-stu-id="97227-147">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Comando pack do NuGet no menu de contexto de projeto do Visual Studio](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="97227-149">Se você não vir o comando **Pack**, seu projeto provavelmente não será um projeto no estilo SDK e você precisará usar a CLI do `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="97227-149">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="97227-150">Ou [migre o projeto](../consume-packages/migrate-packages-config-to-package-reference.md) e use `dotnet` a CLI, ou confira [Criar e publicar um pacote do .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) para ver instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="97227-150">Either [migrate the project](../consume-packages/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="97227-151">O Visual Studio compila o projeto e cria o arquivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="97227-151">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="97227-152">Examine a janela **Saída** para obter detalhes (semelhante ao seguinte), que contém o caminho até o arquivo de pacote.</span><span class="sxs-lookup"><span data-stu-id="97227-152">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="97227-153">Observe também que o assembly criado está em `bin\Release\netstandard2.0`, como convém ao destino do .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="97227-153">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a><span data-ttu-id="97227-154">(Opcional) Gerar pacote ao compilar</span><span class="sxs-lookup"><span data-stu-id="97227-154">(Optional) Generate package on build</span></span>

<span data-ttu-id="97227-155">Você pode configurar o Visual Studio para gerar automaticamente o pacote NuGet ao compilar o projeto.</span><span class="sxs-lookup"><span data-stu-id="97227-155">You can configure Visual Studio to automatically generate the NuGet package when you build the project.</span></span>

1. <span data-ttu-id="97227-156">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e escolha **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="97227-156">In Solution Explorer, right-click the project and choose **Properties**.</span></span>

2. <span data-ttu-id="97227-157">Na guia **Pacote**, selecione **Gerar pacote NuGet no build**.</span><span class="sxs-lookup"><span data-stu-id="97227-157">In the **Package** tab, select **Generate NuGet package on build**.</span></span>

   ![Gerar pacote automaticamente no build](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> <span data-ttu-id="97227-159">Ao gerar automaticamente o pacote, o tempo de empacotamento aumenta o tempo de compilação do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="97227-159">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="optional-pack-with-msbuild"></a><span data-ttu-id="97227-160">(Opcional) Empacotar com MSBuild</span><span class="sxs-lookup"><span data-stu-id="97227-160">(Optional) pack with MSBuild</span></span>

<span data-ttu-id="97227-161">Como uma alternativa ao uso do comando de menu **Pack**, o NuGet 4.x+ e o MSBuild 15.1+ são compatíveis com um destino `pack` quando o projeto contém os dados do pacote necessários.</span><span class="sxs-lookup"><span data-stu-id="97227-161">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="97227-162">Abra um prompt de comando, navegue até a pasta do projeto e execute o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="97227-162">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="97227-163">(Você normalmente deseja iniciar o "Prompt de Comando do Desenvolvedor para Visual Studio" por meio do menu Iniciar, pois ele estará configurado com todos os caminhos necessários para o MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="97227-163">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

<span data-ttu-id="97227-164">Para saber mais, confira [Criar um pacote usando MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="97227-164">For more information, see [Create a package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="97227-165">Publicar o pacote</span><span class="sxs-lookup"><span data-stu-id="97227-165">Publish the package</span></span>

<span data-ttu-id="97227-166">Depois que você tiver um arquivo `.nupkg`, publique-o em nuget.org usando a CLI do `nuget.exe` ou a CLI do `dotnet.exe` juntamente com uma chave de API adquirida em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="97227-166">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="97227-167">Adquirir a chave de sua API</span><span class="sxs-lookup"><span data-stu-id="97227-167">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a><span data-ttu-id="97227-168">Publicar com a CLI do dotnet ou a CLI do nuget.exe</span><span class="sxs-lookup"><span data-stu-id="97227-168">Publish with the dotnet CLI or nuget.exe CLI</span></span>

<span data-ttu-id="97227-169">Selecione a guia para sua ferramenta CLI, **CLI do .NET Core** (CLI do dotnet) ou **NuGet** (CLI do nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="97227-169">Select the tab for your CLI tool, either **.NET Core CLI** (dotnet CLI) or **NuGet** (nuget.exe CLI).</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="97227-170">CLI do .NET Core</span><span class="sxs-lookup"><span data-stu-id="97227-170">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="97227-171">Esta etapa é a alternativa recomendada para usar o `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="97227-171">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="97227-172">Antes de publicar o pacote, você deverá primeiro abrir uma linha de comando.</span><span class="sxs-lookup"><span data-stu-id="97227-172">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nugettabnuget"></a>[<span data-ttu-id="97227-173">NuGet</span><span class="sxs-lookup"><span data-stu-id="97227-173">NuGet</span></span>](#tab/nuget)

<span data-ttu-id="97227-174">Esta etapa é uma alternativa ao uso de `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="97227-174">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="97227-175">Abra uma linha de comando e altere para a pasta que contém o arquivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="97227-175">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="97227-176">Execute o seguinte comando, especificando o nome do pacote (ID de pacote exclusiva) e substituindo o valor da chave pela chave da API:</span><span class="sxs-lookup"><span data-stu-id="97227-176">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="97227-177">O nuget.exe exibe os resultados do processo de publicação:</span><span class="sxs-lookup"><span data-stu-id="97227-177">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="97227-178">Confira [nuget push](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="97227-178">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

---

### <a name="publish-errors"></a><span data-ttu-id="97227-179">Erros de publicação</span><span class="sxs-lookup"><span data-stu-id="97227-179">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="97227-180">Gerenciar o pacote publicado</span><span class="sxs-lookup"><span data-stu-id="97227-180">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="97227-181">Adicionar um Leiame e outros arquivos</span><span class="sxs-lookup"><span data-stu-id="97227-181">Adding a readme and other files</span></span>

<span data-ttu-id="97227-182">Para especificar diretamente os arquivos a serem incluídos no pacote, edite o arquivo de projeto e use a propriedade `content`:</span><span class="sxs-lookup"><span data-stu-id="97227-182">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="97227-183">Isso incluirá um arquivo chamado `readme.txt` na raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="97227-183">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="97227-184">O Visual Studio exibe o conteúdo do arquivo como texto sem formatação imediatamente depois de instalar o pacote diretamente.</span><span class="sxs-lookup"><span data-stu-id="97227-184">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="97227-185">(Arquivos Leiame não são exibidos para pacotes instalados como dependências).</span><span class="sxs-lookup"><span data-stu-id="97227-185">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="97227-186">Por exemplo, mostramos aqui como o arquivo Leiame para o pacote HtmlAgilityPack é exibido:</span><span class="sxs-lookup"><span data-stu-id="97227-186">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![A exibição de um arquivo Leiame para um pacote do NuGet na instalação](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="97227-188">Somente adicionar o readme.txt na raiz do projeto não resultará na inclusão dele no pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="97227-188">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="97227-189">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="97227-189">Related topics</span></span>

- [<span data-ttu-id="97227-190">Criar um pacote</span><span class="sxs-lookup"><span data-stu-id="97227-190">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)
- [<span data-ttu-id="97227-191">Publicar um pacote</span><span class="sxs-lookup"><span data-stu-id="97227-191">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="97227-192">Pacotes de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="97227-192">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="97227-193">Suporte a várias estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="97227-193">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="97227-194">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="97227-194">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="97227-195">Criando pacotes localizados</span><span class="sxs-lookup"><span data-stu-id="97227-195">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="97227-196">Documentação da Biblioteca do .NET Standard</span><span class="sxs-lookup"><span data-stu-id="97227-196">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="97227-197">Portabilidade para o .NET Core do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="97227-197">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
