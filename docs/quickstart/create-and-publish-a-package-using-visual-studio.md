---
title: Criar e publicar um pacote .NET Standard usando o Visual Studio no Windows
description: Um tutorial passo a passo sobre como criar e publicar um pacote NuGet do .NET Standard usando o Visual Studio 2017 no Windows.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: c75785d361f25564c8a59d7a2d85924c570a7b9a
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467807"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="d0d9f-103">Início Rápido: Criar e publicar um pacote do NuGet usando o Visual Studio (.NET Standard somente no Windows)</span><span class="sxs-lookup"><span data-stu-id="d0d9f-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="d0d9f-104">Criar um pacote NuGet de uma Biblioteca de Classes .NET Standard no Visual Studio no Windows e, em seguida, publicá-lo no nuget.org usando uma ferramenta de CLI é um processo simples.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="d0d9f-105">Este Início Rápido se aplica somente ao Visual Studio 2017 para Windows.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="d0d9f-106">O Visual Studio para Mac não inclui os recursos descritos aqui.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="d0d9f-107">Em vez disso, use as [ferramentas CLI do dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d0d9f-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0d9f-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d0d9f-108">Prerequisites</span></span>

1. <span data-ttu-id="d0d9f-109">Instale qualquer edição do Visual Studio 2017 de [visualstudio.com](https://www.visualstudio.com/) usando qualquer carga de trabalho relacionada ao .NET.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="d0d9f-110">O Visual Studio 2017 inclui automaticamente os recursos do NuGet quando uma carga de trabalho do .NET é instalada.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="d0d9f-111">Clique em uma das ferramentas de CLI.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-111">Install one of the CLI tools.</span></span>

   * <span data-ttu-id="d0d9f-112">Para a CLI do `dotnet`, instale o [SDK do .NET Core](https://www.microsoft.com/net/download/).</span><span class="sxs-lookup"><span data-stu-id="d0d9f-112">For the `dotnet` CLI, install the [.NET Core SDK](https://www.microsoft.com/net/download/).</span></span> <span data-ttu-id="d0d9f-113">A CLI dotnet é necessária para projetos do .NET Standard que usam o formato de estilo do SDK (atributo do SDK).</span><span class="sxs-lookup"><span data-stu-id="d0d9f-113">The dotnet CLI is required for .NET Standard projects that use the SDK-style format (SDK attribute).</span></span>

   * <span data-ttu-id="d0d9f-114">Instale a CLI do `nuget.exe`, baixe-a em [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), salve o arquivo `.exe` em uma pasta adequada e adicione essa pasta na sua variável de ambiente PATH.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-114">For the `nuget.exe` CLI, download it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving the `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span> <span data-ttu-id="d0d9f-115">A CLI do nuget.exe é usada nas bibliotecas do .NET Standard no formato de estilo não SDK.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-115">The nuget.exe CLI is used for .NET Standard libraries in the non-SDK-style format.</span></span>

1. <span data-ttu-id="d0d9f-116">[Registre-se em uma conta gratuita em nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account), se ainda não tiver uma.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-116">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="d0d9f-117">Criar uma nova conta envia um email de confirmação.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-117">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="d0d9f-118">Você deve confirmar a conta antes de poder carregar um pacote.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-118">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="d0d9f-119">Criar um projeto de biblioteca de classes</span><span class="sxs-lookup"><span data-stu-id="d0d9f-119">Create a class library project</span></span>

<span data-ttu-id="d0d9f-120">Você pode usar um projeto existente da Biblioteca de Classes .NET Standard para o código que você deseja empacotar ou criar um simples da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d0d9f-120">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="d0d9f-121">No Visual Studio, escolha **Arquivo > Novo > Projeto**, expanda o nó **Visual C# > .NET Standard**, selecione o modelo de "Biblioteca de Classes (.NET Standard)", nomeie o projeto como AppLogger e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-121">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="d0d9f-122">Clique com botão direito do mouse no arquivo de projeto resultante e selecione **Build** para verificar se o projeto foi criado corretamente.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-122">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="d0d9f-123">A DLL é encontrada dentro da pasta de Depuração (ou Versão, se você compilar essa configuração).</span><span class="sxs-lookup"><span data-stu-id="d0d9f-123">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="d0d9f-124">Em um pacote NuGet real, obviamente, você implementa muitos recursos úteis com os quais outras pessoas podem compilar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-124">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="d0d9f-125">Para este passo a passo, no entanto, você não escreverá nenhum código adicional porque uma biblioteca de classes do modelo é suficiente para criar um pacote.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-125">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="d0d9f-126">Ainda assim, se você desejar algum código funcional para o pacote, use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d0d9f-126">Still, if you'd like some functional code for the package, use the following:</span></span>

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

> [!Tip]
> <span data-ttu-id="d0d9f-127">A menos que você tenha um motivo para a escolha de outro jeito, o .NET Standard é o destino preferencial para pacotes NuGet, pois fornece compatibilidade com a mais ampla variedade de projetos de consumo.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-127">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="d0d9f-128">Configurar propriedades do pacote</span><span class="sxs-lookup"><span data-stu-id="d0d9f-128">Configure package properties</span></span>

1. <span data-ttu-id="d0d9f-129">Selecione o comando de menu **Projeto > Propriedades** e, em seguida, selecione a guia **Pacote**. (A guia **Pacote** é exibida apenas para projetos da biblioteca de classes do .NET Standard. Se você estiver direcionando ao .NET Framework, veja [Criar e publicar um pacote do .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="d0d9f-129">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="d0d9f-130">Se ela não for exibida para um projeto do .NET Standard, você precisará atualizar o Visual Studio 2017 para a versão mais recente.)</span><span class="sxs-lookup"><span data-stu-id="d0d9f-130">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![Propriedades do pacote NuGet em um projeto do Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="d0d9f-132">Para pacotes compilados para consumo público, preste atenção especial à propriedade **Tags**, à medida que as marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-132">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="d0d9f-133">Dê ao seu pacote um identificador exclusivo e preencha as outras propriedades desejadas.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-133">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="d0d9f-134">Para obter uma descrição das propriedades diferentes, veja [referência de arquivo .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="d0d9f-134">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="d0d9f-135">Todas essas propriedades vão para o manifesto `.nuspec` que o Visual Studio cria para o projeto.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-135">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="d0d9f-136">Você precisa dar ao pacote um identificador exclusivo em nuget.org ou qualquer host que você esteja usando.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-136">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="d0d9f-137">Para este passo a passo, recomendamos incluir o "Sample" ou "Test" no nome, pois a etapa de publicação posterior torna o pacote publicamente visível (embora seja improvável que alguém possa usá-lo).</span><span class="sxs-lookup"><span data-stu-id="d0d9f-137">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="d0d9f-138">Se você tentar publicar um pacote com um nome que já existe, você verá um erro.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-138">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="d0d9f-139">Opcional: para ver as propriedades diretamente no arquivo de projeto, clique com o botão direito do mouse no projeto no Gerenciador de Soluções e selecione **Editar AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-139">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="d0d9f-140">Executar o comando pack</span><span class="sxs-lookup"><span data-stu-id="d0d9f-140">Run the pack command</span></span>

1. <span data-ttu-id="d0d9f-141">Defina a configuração da solução como **Release**.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-141">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="d0d9f-142">Clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e selecione o comando **Pack**:</span><span class="sxs-lookup"><span data-stu-id="d0d9f-142">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Comando pack do NuGet no menu de contexto de projeto do Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="d0d9f-144">O Visual Studio compila o projeto e cria o arquivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-144">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="d0d9f-145">Examine a janela **Saída** para obter detalhes (semelhante ao seguinte), que contém o caminho até o arquivo de pacote.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-145">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="d0d9f-146">Observe também que o assembly criado está em `bin\Release\netstandard2.0`, como convém ao destino do .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-146">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="d0d9f-147">Opção alternativa: empacotar com o MSBuild</span><span class="sxs-lookup"><span data-stu-id="d0d9f-147">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="d0d9f-148">Como uma alternativa ao uso do comando de menu **Pack**, o NuGet 4.x+ e o MSBuild 15.1+ são compatíveis com um destino `pack` quando o projeto contém os dados do pacote necessários.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-148">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="d0d9f-149">Abra um prompt de comando, navegue até a pasta do projeto e execute o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-149">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="d0d9f-150">(Você normalmente deseja iniciar o "Prompt de Comando do Desenvolvedor para Visual Studio" por meio do menu Iniciar, pois ele estará configurado com todos os caminhos necessários para o MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="d0d9f-150">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="d0d9f-151">O pacote pode então ser encontrado na pasta `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-151">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="d0d9f-152">Para opções adicionais com `msbuild -t:pack`, consulte [Empacotamento e restauração do NuGet como destinos do MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="d0d9f-152">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="d0d9f-153">Publicar o pacote</span><span class="sxs-lookup"><span data-stu-id="d0d9f-153">Publish the package</span></span>

<span data-ttu-id="d0d9f-154">Depois que você tiver um arquivo `.nupkg`, publique-o em nuget.org usando a CLI do `nuget.exe` ou a CLI do `dotnet.exe` juntamente com uma chave de API adquirida em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-154">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="d0d9f-155">Adquirir a chave de sua API</span><span class="sxs-lookup"><span data-stu-id="d0d9f-155">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="d0d9f-156">Publicar com dotnet nuget push (CLI do dotnet)</span><span class="sxs-lookup"><span data-stu-id="d0d9f-156">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="d0d9f-157">Esta etapa é uma alternativa ao uso de `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-157">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="d0d9f-158">Publicar com nuget push (CLI do nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="d0d9f-158">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="d0d9f-159">Esta etapa é uma alternativa ao uso de `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-159">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="d0d9f-160">Altere para a pasta que contém o arquivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-160">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="d0d9f-161">Execute o seguinte comando, especificando o nome do pacote e substituindo o valor da chave pela chave da API:</span><span class="sxs-lookup"><span data-stu-id="d0d9f-161">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="d0d9f-162">O nuget.exe exibe os resultados do processo de publicação:</span><span class="sxs-lookup"><span data-stu-id="d0d9f-162">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="d0d9f-163">Confira [nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="d0d9f-163">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="d0d9f-164">Erros de publicação</span><span class="sxs-lookup"><span data-stu-id="d0d9f-164">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="d0d9f-165">Gerenciar o pacote publicado</span><span class="sxs-lookup"><span data-stu-id="d0d9f-165">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="d0d9f-166">Adicionar um Leiame e outros arquivos</span><span class="sxs-lookup"><span data-stu-id="d0d9f-166">Adding a readme and other files</span></span>

<span data-ttu-id="d0d9f-167">Para especificar diretamente os arquivos a serem incluídos no pacote, edite o arquivo de projeto e use a propriedade `content`:</span><span class="sxs-lookup"><span data-stu-id="d0d9f-167">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="d0d9f-168">Isso incluirá um arquivo chamado `readme.txt` na raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-168">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="d0d9f-169">O Visual Studio exibe o conteúdo do arquivo como texto sem formatação imediatamente depois de instalar o pacote diretamente.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-169">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="d0d9f-170">(Arquivos Leiame não são exibidos para pacotes instalados como dependências).</span><span class="sxs-lookup"><span data-stu-id="d0d9f-170">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="d0d9f-171">Por exemplo, mostramos aqui como o arquivo Leiame para o pacote HtmlAgilityPack é exibido:</span><span class="sxs-lookup"><span data-stu-id="d0d9f-171">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![A exibição de um arquivo Leiame para um pacote do NuGet na instalação](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="d0d9f-173">Somente adicionar o readme.txt na raiz do projeto não resultará na inclusão dele no pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="d0d9f-173">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="d0d9f-174">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="d0d9f-174">Related topics</span></span>

- [<span data-ttu-id="d0d9f-175">Criar um pacote</span><span class="sxs-lookup"><span data-stu-id="d0d9f-175">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="d0d9f-176">Publicar um pacote</span><span class="sxs-lookup"><span data-stu-id="d0d9f-176">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="d0d9f-177">Pacotes de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="d0d9f-177">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="d0d9f-178">Suporte a várias estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="d0d9f-178">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="d0d9f-179">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="d0d9f-179">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="d0d9f-180">Criando pacotes localizados</span><span class="sxs-lookup"><span data-stu-id="d0d9f-180">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="d0d9f-181">Documentação da Biblioteca do .NET Standard</span><span class="sxs-lookup"><span data-stu-id="d0d9f-181">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="d0d9f-182">Portabilidade para o .NET Core do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="d0d9f-182">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
