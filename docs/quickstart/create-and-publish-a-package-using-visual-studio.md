---
title: Guia de introdução para a criação e a publicação de um pacote do NuGet do .NET Standard usando o Visual Studio
description: Um tutorial passo a passo sobre como criar e publicar um pacote NuGet do .NET Standard usando o Visual Studio 2017.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/18/2018
ms.topic: quickstart
ms.openlocfilehash: c5d58aa6312eae801607ca44a81bc092a7a7c15f
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2018
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard"></a><span data-ttu-id="92faa-103">Início Rápido: Criar e publicar um pacote do NuGet usando o Visual Studio (.NET Standard)</span><span class="sxs-lookup"><span data-stu-id="92faa-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard)</span></span>

<span data-ttu-id="92faa-104">É um processo simples criar um pacote NuGet de uma Biblioteca de Classes .NET Standard no Visual Studio e, em seguida, publicá-lo no nuget.org usando uma ferramenta de CLI.</span><span class="sxs-lookup"><span data-stu-id="92faa-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio, and then publish it to nuget.org using a CLI tool.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92faa-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="92faa-105">Prerequisites</span></span>

1. <span data-ttu-id="92faa-106">Instale qualquer edição do Visual Studio 2017 de [visualstudio.com](https://www.visualstudio.com/) usando qualquer carga de trabalho relacionada ao .NET.</span><span class="sxs-lookup"><span data-stu-id="92faa-106">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="92faa-107">O Visual Studio 2017 inclui automaticamente os recursos do NuGet quando uma carga de trabalho do .NET é instalada.</span><span class="sxs-lookup"><span data-stu-id="92faa-107">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="92faa-108">Instale a CLI do `nuget.exe` baixando-a de [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), salvando o arquivo `.exe` em uma pasta adequada e adicionando pasta a variável de ambiente PATH.</span><span class="sxs-lookup"><span data-stu-id="92faa-108">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="92faa-109">Como alternativa, se você tiver o [SDK do .NET Core](https://www.microsoft.com/net/download/) instalado, use a CLI do `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="92faa-109">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="92faa-110">[Registre-se em uma conta gratuita em nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), se ainda não tiver uma.</span><span class="sxs-lookup"><span data-stu-id="92faa-110">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="92faa-111">Criar uma nova conta envia um email de confirmação.</span><span class="sxs-lookup"><span data-stu-id="92faa-111">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="92faa-112">Você deve confirmar a conta antes de poder carregar um pacote.</span><span class="sxs-lookup"><span data-stu-id="92faa-112">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="92faa-113">Criar um projeto de biblioteca de classes</span><span class="sxs-lookup"><span data-stu-id="92faa-113">Create a class library project</span></span>

<span data-ttu-id="92faa-114">Você pode usar um projeto existente da Biblioteca de Classes .NET Standard para o código que você deseja empacotar ou criar um simples da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="92faa-114">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="92faa-115">No Visual Studio, escolha **Arquivo > Novo > Projeto**, expanda o nó **Visual C# > .NET Standard**, selecione o modelo de "Biblioteca de Classes (.NET Standard)", nomeie o projeto como AppLogger e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="92faa-115">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="92faa-116">Clique com botão direito do mouse no arquivo de projeto resultante e selecione **Build** para verificar se o projeto foi criado corretamente.</span><span class="sxs-lookup"><span data-stu-id="92faa-116">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="92faa-117">A DLL é encontrada dentro da pasta de Depuração (ou Versão, se você compilar essa configuração).</span><span class="sxs-lookup"><span data-stu-id="92faa-117">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="92faa-118">Em um pacote NuGet real, obviamente, você implementa muitos recursos úteis com os quais outras pessoas podem compilar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="92faa-118">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="92faa-119">Para este passo a passo, no entanto, você não escreverá nenhum código adicional porque uma biblioteca de classes do modelo é suficiente para criar um pacote.</span><span class="sxs-lookup"><span data-stu-id="92faa-119">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="92faa-120">Ainda assim, se você desejar algum código funcional para o pacote, use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="92faa-120">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="92faa-121">A menos que você tenha um motivo para a escolha de outro jeito, o .NET Standard é o destino preferencial para pacotes NuGet, pois fornece compatibilidade com a mais ampla variedade de projetos de consumo.</span><span class="sxs-lookup"><span data-stu-id="92faa-121">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="92faa-122">Configurar propriedades do pacote</span><span class="sxs-lookup"><span data-stu-id="92faa-122">Configure package properties</span></span>

1. <span data-ttu-id="92faa-123">Selecione o comando de menu **Projeto > Propriedades** e, em seguida, selecione a guia **Pacote**. (A guia **Pacote** é exibida apenas para projetos da biblioteca de classes do .NET Standard. Se você estiver direcionando ao .NET Framework, veja [Criar e publicar um pacote do .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="92faa-123">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="92faa-124">Se ela não for exibida para um projeto do .NET Standard, você precisará atualizar o Visual Studio 2017 para a versão mais recente.)</span><span class="sxs-lookup"><span data-stu-id="92faa-124">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![Propriedades do pacote NuGet em um projeto do Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="92faa-126">Para pacotes compilados para consumo público, preste atenção especial à propriedade **Tags**, à medida que as marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.</span><span class="sxs-lookup"><span data-stu-id="92faa-126">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="92faa-127">Dê ao seu pacote um identificador exclusivo e preencha as outras propriedades desejadas.</span><span class="sxs-lookup"><span data-stu-id="92faa-127">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="92faa-128">Para obter uma descrição das propriedades diferentes, veja [referência de arquivo .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="92faa-128">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="92faa-129">Todas essas propriedades vão para o manifesto `.nuspec` que o Visual Studio cria para o projeto.</span><span class="sxs-lookup"><span data-stu-id="92faa-129">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="92faa-130">Você precisa dar ao pacote um identificador exclusivo em nuget.org ou qualquer host que você esteja usando.</span><span class="sxs-lookup"><span data-stu-id="92faa-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="92faa-131">Para este passo a passo, recomendamos incluir o "Sample" ou "Test" no nome, pois a etapa de publicação posterior torna o pacote publicamente visível (embora seja improvável que alguém possa usá-lo).</span><span class="sxs-lookup"><span data-stu-id="92faa-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="92faa-132">Se você tentar publicar um pacote com um nome que já existe, você verá um erro.</span><span class="sxs-lookup"><span data-stu-id="92faa-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="92faa-133">Opcional: para ver as propriedades diretamente no arquivo de projeto, clique com o botão direito do mouse no projeto no Gerenciador de Soluções e selecione **Editar AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="92faa-133">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="92faa-134">Executar o comando pack</span><span class="sxs-lookup"><span data-stu-id="92faa-134">Run the pack command</span></span>

1. <span data-ttu-id="92faa-135">Defina a configuração como **Versão**.</span><span class="sxs-lookup"><span data-stu-id="92faa-135">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="92faa-136">Clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e selecione o comando **Pack**:</span><span class="sxs-lookup"><span data-stu-id="92faa-136">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Comando pack do NuGet no menu de contexto de projeto do Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="92faa-138">O Visual Studio compila o projeto e cria o arquivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="92faa-138">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="92faa-139">Examine a janela **Saída** para obter detalhes (semelhante ao seguinte), que contém o caminho até o arquivo de pacote.</span><span class="sxs-lookup"><span data-stu-id="92faa-139">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="92faa-140">Observe também que o assembly criado está em `bin\Release\netstandard2.0`, como convém ao destino do .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="92faa-140">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="92faa-141">Opção alternativa: empacotar com o MSBuild</span><span class="sxs-lookup"><span data-stu-id="92faa-141">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="92faa-142">Como uma alternativa ao uso do comando de menu **Pack**, o NuGet 4.x+ e o MSBuild 15.1+ são compatíveis com um destino `pack` quando o projeto contém os dados do pacote necessários.</span><span class="sxs-lookup"><span data-stu-id="92faa-142">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="92faa-143">Abra um prompt de comando, navegue até a pasta do projeto e execute o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="92faa-143">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="92faa-144">(Você normalmente deseja iniciar o "Prompt de Comando do Desenvolvedor para Visual Studio" por meio do menu Iniciar, pois ele estará configurado com todos os caminhos necessários para o MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="92faa-144">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="92faa-145">O pacote pode então ser encontrado na pasta `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="92faa-145">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="92faa-146">Para opções adicionais com `msbuild /t:pack`, consulte [Empacotamento e restauração do NuGet como destinos do MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="92faa-146">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="92faa-147">Publicar o pacote</span><span class="sxs-lookup"><span data-stu-id="92faa-147">Publish the package</span></span>

<span data-ttu-id="92faa-148">Depois que você tiver um arquivo `.nupkg`, publique-o em nuget.org usando a CLI do `nuget.exe` ou a CLI do `dotnet.exe` juntamente com uma chave de API adquirida em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="92faa-148">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="92faa-149">Adquirir a chave de sua API</span><span class="sxs-lookup"><span data-stu-id="92faa-149">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="92faa-150">Publicar com nuget push</span><span class="sxs-lookup"><span data-stu-id="92faa-150">Publish with nuget push</span></span>

<span data-ttu-id="92faa-151">Esta etapa é uma alternativa ao uso de `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="92faa-151">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="92faa-152">Altere para a pasta que contém o arquivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="92faa-152">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="92faa-153">Execute o seguinte comando, especificando o nome do pacote e substituindo o valor da chave pela chave da API:</span><span class="sxs-lookup"><span data-stu-id="92faa-153">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="92faa-154">O nuget.exe exibe os resultados do processo de publicação:</span><span class="sxs-lookup"><span data-stu-id="92faa-154">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="92faa-155">Confira [nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="92faa-155">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="92faa-156">Publicar com dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="92faa-156">Publish with dotnet nuget push</span></span>

<span data-ttu-id="92faa-157">Esta etapa é uma alternativa ao uso de `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="92faa-157">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="92faa-158">Erros de publicação</span><span class="sxs-lookup"><span data-stu-id="92faa-158">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="92faa-159">Gerenciar o pacote publicado</span><span class="sxs-lookup"><span data-stu-id="92faa-159">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="92faa-160">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="92faa-160">Related topics</span></span>

- [<span data-ttu-id="92faa-161">Criar um pacote</span><span class="sxs-lookup"><span data-stu-id="92faa-161">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="92faa-162">Publicar um pacote</span><span class="sxs-lookup"><span data-stu-id="92faa-162">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="92faa-163">Pacotes de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="92faa-163">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="92faa-164">Suporte a várias estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="92faa-164">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="92faa-165">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="92faa-165">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="92faa-166">Criando pacotes localizados</span><span class="sxs-lookup"><span data-stu-id="92faa-166">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="92faa-167">Documentação da Biblioteca do .NET Standard</span><span class="sxs-lookup"><span data-stu-id="92faa-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="92faa-168">Portabilidade para o .NET Core do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="92faa-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
