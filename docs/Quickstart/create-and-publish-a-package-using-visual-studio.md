---
title: "Guia de introdução para a criação e publicação de um pacote NuGet usando o Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: Um tutorial passo a passo sobre como criar e publicar um pacote NuGet usando o Visual Studio 2017.
keywords: "Criação de pacote NuGet, publicação de pacote NuGet, tutorial do NuGet, criação de pacote NuGet no Visual Studio, pacote msbuild"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a4d60fdc0f27f9c4080266e212ac1cfe470ba925
ms.sourcegitcommit: eabd401616a98dda2ae6293612acb3b81b584967
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="create-and-publish-a-package-using-visual-studio"></a><span data-ttu-id="52b26-104">Criar e publicar um pacote usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="52b26-104">Create and publish a package using Visual Studio</span></span>

<span data-ttu-id="52b26-105">É um processo simples criar um pacote NuGet de uma Biblioteca de Classes do .NET no Visual Studio e publicá-lo em nuget.org usando uma ferramenta de CLI.</span><span class="sxs-lookup"><span data-stu-id="52b26-105">It's a simple process to create a NuGet package from a .NET Class Library in Visual Studio, and then publish it to nuget.org using a CLI tool.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="52b26-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="52b26-106">Pre-requisites</span></span>

1. <span data-ttu-id="52b26-107">Instale qualquer edição do Visual Studio 2017 de [visualstudio.com](https://www.visualstudio.com/) usando qualquer carga de trabalho relacionada ao .NET.</span><span class="sxs-lookup"><span data-stu-id="52b26-107">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="52b26-108">O Visual Studio 2017 inclui automaticamente os recursos do NuGet quando uma carga de trabalho do .NET é instalada.</span><span class="sxs-lookup"><span data-stu-id="52b26-108">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="52b26-109">Instale a CLI do `nuget.exe` baixando-a de [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), salvando o arquivo `.exe` em uma pasta adequada e adicionando pasta a variável de ambiente PATH.</span><span class="sxs-lookup"><span data-stu-id="52b26-109">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="52b26-110">Como alternativa, se você tiver o [SDK do .NET Core](https://www.microsoft.com/net/download/) instalado, use a CLI do `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="52b26-110">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="52b26-111">[Registre-se em uma conta gratuita em nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), se ainda não tiver uma.</span><span class="sxs-lookup"><span data-stu-id="52b26-111">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="52b26-112">Criar uma nova conta envia um email de confirmação.</span><span class="sxs-lookup"><span data-stu-id="52b26-112">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="52b26-113">Você deve confirmar a conta antes de poder carregar um pacote.</span><span class="sxs-lookup"><span data-stu-id="52b26-113">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="52b26-114">Criar um projeto de biblioteca de classes</span><span class="sxs-lookup"><span data-stu-id="52b26-114">Create a class library project</span></span>

<span data-ttu-id="52b26-115">Você pode usar um projeto existente da Biblioteca de Classes .NET para o código que você deseja empacotar, ou criar um simples da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="52b26-115">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="52b26-116">No Visual Studio, escolha **Arquivo > Novo > Projeto**, expanda o nó **Visual C# > .NET Standard**, selecione o modelo de "Biblioteca de Classes (.NET Standard)", nomeie o projeto como AppLogger e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="52b26-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="52b26-117">Clique com botão direito do mouse no arquivo de projeto resultante e selecione **Build** para verificar se o projeto foi criado corretamente.</span><span class="sxs-lookup"><span data-stu-id="52b26-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="52b26-118">A DLL é encontrada dentro da pasta de Depuração (ou Versão, se você compilar essa configuração).</span><span class="sxs-lookup"><span data-stu-id="52b26-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="52b26-119">Em um pacote NuGet real, obviamente, você implementa muitos recursos úteis com os quais outras pessoas podem compilar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="52b26-119">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="52b26-120">Para este passo a passo, no entanto, você não escreverá nenhum código adicional porque uma biblioteca de classes do modelo é suficiente para criar um pacote.</span><span class="sxs-lookup"><span data-stu-id="52b26-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="52b26-121">Ainda assim, se você desejar algum código funcional para o pacote, use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="52b26-121">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="52b26-122">A menos que você tenha um motivo para a escolha de outro jeito, o .NET Standard é o destino preferencial para pacotes NuGet, pois fornece compatibilidade com a mais ampla variedade de projetos de consumo.</span><span class="sxs-lookup"><span data-stu-id="52b26-122">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="52b26-123">Configurar propriedades do pacote</span><span class="sxs-lookup"><span data-stu-id="52b26-123">Configure package properties</span></span>

1. <span data-ttu-id="52b26-124">Selecione o comando de menu **Projeto > Propriedades** e, em seguida, selecione a guia **Pacote**:</span><span class="sxs-lookup"><span data-stu-id="52b26-124">Select the **Project > Properties** menu command, then select the **Package** tab:</span></span>

    ![Propriedades do pacote NuGet em um projeto do Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="52b26-126">Para pacotes compilados para consumo público, preste atenção especial à propriedade **Tags**, à medida que as marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.</span><span class="sxs-lookup"><span data-stu-id="52b26-126">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="52b26-127">Dê ao seu pacote um identificador exclusivo e preencha as outras propriedades desejadas.</span><span class="sxs-lookup"><span data-stu-id="52b26-127">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="52b26-128">Para obter uma descrição das propriedades diferentes, veja [referência de arquivo .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="52b26-128">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="52b26-129">Todas essas propriedades vão para o manifesto `.nuspec` que o Visual Studio cria para o projeto.</span><span class="sxs-lookup"><span data-stu-id="52b26-129">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="52b26-130">Você precisa dar ao pacote um identificador exclusivo em nuget.org ou qualquer host que você esteja usando.</span><span class="sxs-lookup"><span data-stu-id="52b26-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="52b26-131">Para este passo a passo, recomendamos incluir o "Sample" ou "Test" no nome, pois a etapa de publicação posterior torna o pacote publicamente visível (embora seja improvável que alguém possa usá-lo).</span><span class="sxs-lookup"><span data-stu-id="52b26-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="52b26-132">Se você tentar publicar um pacote com um nome que já existe, você verá um erro.</span><span class="sxs-lookup"><span data-stu-id="52b26-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="52b26-133">Opcional: para ver as propriedades diretamente no arquivo de projeto, clique com o botão direito do mouse no projeto no Gerenciador de Soluções e selecione **Editar AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="52b26-133">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="52b26-134">Executar o comando pack</span><span class="sxs-lookup"><span data-stu-id="52b26-134">Run the pack command</span></span>

1. <span data-ttu-id="52b26-135">Defina a configuração como **Versão**.</span><span class="sxs-lookup"><span data-stu-id="52b26-135">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="52b26-136">Clique com o botão direito do mouse no projeto no **Gerenciador de Soluções** e selecione o comando **Pack**:</span><span class="sxs-lookup"><span data-stu-id="52b26-136">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Comando pack do NuGet no menu de contexto de projeto do Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="52b26-138">O Visual Studio compila o projeto e cria o arquivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="52b26-138">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="52b26-139">Examine a janela **Saída** para obter detalhes (semelhante ao seguinte), que contém o caminho até o arquivo de pacote.</span><span class="sxs-lookup"><span data-stu-id="52b26-139">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="52b26-140">Observe também que o assembly criado está em `bin\Release\netstandard2.0`, como convém ao destino do .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="52b26-140">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="52b26-141">Opção alternativa: empacotar com o MSBuild</span><span class="sxs-lookup"><span data-stu-id="52b26-141">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="52b26-142">Como uma alternativa ao uso do comando de menu **Pack**, o NuGet 4.x+ e o MSBuild 15.1+ são compatíveis com um destino `pack` quando o projeto contém os dados do pacote necessários:</span><span class="sxs-lookup"><span data-stu-id="52b26-142">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data:</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="52b26-143">O pacote pode então ser encontrado na pasta `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="52b26-143">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="52b26-144">Para opções adicionais com `msbuild /t:pack`, consulte [Empacotamento e restauração do NuGet como destinos do MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="52b26-144">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="52b26-145">Publicar o pacote</span><span class="sxs-lookup"><span data-stu-id="52b26-145">Publish the package</span></span>

<span data-ttu-id="52b26-146">Depois que você tiver um arquivo `.nupkg`, publique-o em nuget.org usando a CLI do `nuget.exe` ou a CLI do `dotnet.exe` juntamente com uma chave de API adquirida em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="52b26-146">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="52b26-147">Adquirir a chave de sua API</span><span class="sxs-lookup"><span data-stu-id="52b26-147">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="52b26-148">Publicar com nuget push</span><span class="sxs-lookup"><span data-stu-id="52b26-148">Publish with nuget push</span></span>

<span data-ttu-id="52b26-149">Esta etapa é uma alternativa ao uso de `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="52b26-149">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="52b26-150">Altere para a pasta que contém o arquivo `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="52b26-150">Change to the folder containing the `.nupkg` file..</span></span>

1. <span data-ttu-id="52b26-151">Execute o seguinte comando, especificando o nome do pacote e substituindo o valor da chave pela chave da API:</span><span class="sxs-lookup"><span data-stu-id="52b26-151">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="52b26-152">O nuget.exe exibe os resultados do processo de publicação:</span><span class="sxs-lookup"><span data-stu-id="52b26-152">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="52b26-153">Confira [nuget push](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="52b26-153">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="52b26-154">Publicar com dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="52b26-154">Publish with dotnet nuget push</span></span>

<span data-ttu-id="52b26-155">Esta etapa é uma alternativa ao uso de `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="52b26-155">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="52b26-156">Erros de publicação</span><span class="sxs-lookup"><span data-stu-id="52b26-156">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="52b26-157">Gerenciar o pacote publicado</span><span class="sxs-lookup"><span data-stu-id="52b26-157">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="52b26-158">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="52b26-158">Related topics</span></span>

- [<span data-ttu-id="52b26-159">Criar um pacote</span><span class="sxs-lookup"><span data-stu-id="52b26-159">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="52b26-160">Publicar um pacote</span><span class="sxs-lookup"><span data-stu-id="52b26-160">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="52b26-161">Suporte a várias estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="52b26-161">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="52b26-162">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="52b26-162">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="52b26-163">Criando pacotes localizados</span><span class="sxs-lookup"><span data-stu-id="52b26-163">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="52b26-164">Documentação da Biblioteca do .NET Standard</span><span class="sxs-lookup"><span data-stu-id="52b26-164">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="52b26-165">Portabilidade para o .NET Core do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="52b26-165">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)