---
title: "Guia de introdução para a criação e publicação de um pacote do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/03/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: Um tutorial passo a passo sobre como criar e publicar um pacote do NuGet usando a interface de linha de comando nuget.exe e o Visual Studio.
keywords: "Criação de pacote do NuGet, publicação de pacote do NuGet, tutorial do NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53d29283c9e786fc27e9a608d7d251d8d0b5b0b2
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2018
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="bc686-104">Criar e publicar um pacote</span><span class="sxs-lookup"><span data-stu-id="bc686-104">Create and publish a package</span></span>

<span data-ttu-id="bc686-105">É um processo simples para criar um pacote do NuGet de uma Biblioteca de Classes do .NET e publique-o em nuget.org. Este artigo orienta você pelo processo usando a CLI (Interface de Linha de Comando) do NuGet e o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc686-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org. This article walks you through the process using the NuGet command-line interface (CLI) and Visual Studio.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="bc686-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bc686-106">Pre-requisites</span></span>

1. <span data-ttu-id="bc686-107">Instale qualquer edição do Visual Studio 2017 de [visualstudio.com](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="bc686-107">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/).</span></span>

1. <span data-ttu-id="bc686-108">Instale a ferramenta CLI do NuGet, `nuget.exe` baixando a versão mais recente do `nuget.exe` de [nuget.org/downloads](https://nuget.org/downloads) e salvando o `.exe` em um local no seu PATH.</span><span class="sxs-lookup"><span data-stu-id="bc686-108">Install the NuGet CLI tool, `nuget.exe`, by downloading the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), and saving the `.exe` to a location in your PATH.</span></span> <span data-ttu-id="bc686-109">Observe que o download *é* a ferramenta em si, não um instalador.</span><span class="sxs-lookup"><span data-stu-id="bc686-109">Note that the download *is* the tool itself, not an installer.</span></span>

1. <span data-ttu-id="bc686-110">Crie um projeto da Biblioteca de Classes .NET adequado para o código que você deseja empacotar.</span><span class="sxs-lookup"><span data-stu-id="bc686-110">Create a suitable .NET Class Library project for the code you want to package.</span></span> <span data-ttu-id="bc686-111">Se você ainda não tiver um projeto, poderá criar um simples da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="bc686-111">If you don't already have a project, you can create a simple one as follows:</span></span>
    1. <span data-ttu-id="bc686-112">No Visual Studio, escolha **Arquivo > Novo > Projeto**, expanda o nó **Visual C# > Windows**, selecione o modelo de “Biblioteca de Classes”, nomeie o projeto como AppLogger e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="bc686-112">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > Windows** node, select the "Class Library" template, name the project AppLogger, and click **OK**.</span></span>
    1. <span data-ttu-id="bc686-113">Clique com botão direito do mouse no arquivo de projeto resultante e selecione **Build** para verificar se o projeto foi criado corretamente.</span><span class="sxs-lookup"><span data-stu-id="bc686-113">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="bc686-114">A DLL é encontrada dentro da pasta de Depuração (ou Versão, se você compilar essa configuração).</span><span class="sxs-lookup"><span data-stu-id="bc686-114">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

    <span data-ttu-id="bc686-115">Dentro de um pacote do NuGet real, obviamente, você implementará muitos recursos úteis com os quais outras pessoas podem compilar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="bc686-115">Within a real NuGet package, of course, you'll implement many useful features upon which others can build applications.</span></span> <span data-ttu-id="bc686-116">Para este passo a passo, no entanto, você não escreverá nenhum código adicional porque uma biblioteca de classes do modelo é suficiente para criar um pacote.</span><span class="sxs-lookup"><span data-stu-id="bc686-116">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span>

## <a name="create-the-nuspec-package-manifest-file"></a><span data-ttu-id="bc686-117">Criar o arquivo de manifesto do pacote .nuspec</span><span class="sxs-lookup"><span data-stu-id="bc686-117">Create the .nuspec package manifest file</span></span>

<span data-ttu-id="bc686-118">Todos os pacotes do NuGet precisam de um arquivo de manifesto&mdash;`.nuspec`&mdash; para descrever seu conteúdo e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="bc686-118">Every NuGet package needs a manifest&mdash;a `.nuspec` file&mdash;to describe its contents and its dependencies.</span></span> <span data-ttu-id="bc686-119">O comando `nuget spec` cria esse arquivo para você, o qual você pode personalizar.</span><span class="sxs-lookup"><span data-stu-id="bc686-119">The `nuget spec` command creates this file for you, which you then customize.</span></span> <span data-ttu-id="bc686-120">Neste exemplo, você cria o `.nuspec` de um arquivo de projeto; você também pode criar o manifesto por outros meios conforme descrito em [Criar um pacote](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="bc686-120">In this example you create the `.nuspec` from a project file; you can also create the manifest through other means as described on [Create a Package](../create-packages/creating-a-package.md).</span></span>

1. <span data-ttu-id="bc686-121">Abra um prompt de comando e navegue até a pasta que contém o arquivo de projeto (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="bc686-121">Open a command prompt and navigate to the folder containing your project file (`.csproj`).</span></span>

1. <span data-ttu-id="bc686-122">Execute o comando `spec` da CLI do NuGet para gerar o manifesto, que tem o nome do seu projeto, como `AppLogger.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="bc686-122">Run the NuGet CLI `spec` command to generate the manifest, which is named after your project, such as `AppLogger.nuspec`:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="bc686-123">Abra o arquivo em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="bc686-123">Open the file in a text editor.</span></span> <span data-ttu-id="bc686-124">O manifesto se parece com o código abaixo, em que os tokens no formato `<token>`(como `$id$`) são substituídos durante o processo de empacotamento pelos valores do arquivo Properties/AssemblyInfo.cs do projeto.</span><span class="sxs-lookup"><span data-stu-id="bc686-124">The manifest looks something like the code below, where tokens in the form `<token>` (such as `$id$`) are be replaced during the packaging process with values from the project's Properties/AssemblyInfo.cs file.</span></span> <span data-ttu-id="bc686-125">Para obter mais detalhes sobre tokens, consulte [Criando um arquivo .nuspec](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="bc686-125">For more details on tokens, see [Creating a .nuspec file](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="bc686-126">Selecione uma ID de pacote que é exclusiva ao nuget.org. É recomendável usar as convenções de nomenclatura descritas em [Criando um pacote](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="bc686-126">Select a package ID that is unique across nuget.org. We recommend using the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="bc686-127">Atualize as marcas de autor e de descrição, caso contrário, você receberá um erro na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="bc686-127">Be sure to update the author and description tags or you get an error in the next step.</span></span> <span data-ttu-id="bc686-128">Aqui está um arquivo `.nuspec` atualizado como exemplo:</span><span class="sxs-lookup"><span data-stu-id="bc686-128">Here's an updated `.nuspec` file as an example:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="bc686-129">Para pacotes compilados para consumo público, preste atenção especial ao elemento `<tags>`, visto que essas marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.</span><span class="sxs-lookup"><span data-stu-id="bc686-129">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="bc686-130">Executar o comando pack</span><span class="sxs-lookup"><span data-stu-id="bc686-130">Run the pack command</span></span>

<span data-ttu-id="bc686-131">Para compilar um pacote do NuGet (um arquivo `.nupkg`) de um projeto, execute o comando `pack`:</span><span class="sxs-lookup"><span data-stu-id="bc686-131">To build a NuGet package (a `.nupkg` file) from a project, run the `pack` command:</span></span>

```cli
nuget pack AppLogger.csproj
```

<span data-ttu-id="bc686-132">Este comando cria `AppLogger.1.0.0.0.nupkg` usando o nome do pacote e o número de versão do arquivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="bc686-132">This command creates `AppLogger.1.0.0.0.nupkg` using the package name and version number from the `.nuspec` file.</span></span> <span data-ttu-id="bc686-133">O comando emite avisos se você não tiver atualizado vários campos no arquivo `.nuspec` de seus valores padrão.</span><span class="sxs-lookup"><span data-stu-id="bc686-133">The command issues warnings if you haven't updated various fields in the `.nuspec` file from their default values.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="bc686-134">Publicar o pacote</span><span class="sxs-lookup"><span data-stu-id="bc686-134">Publish the package</span></span>

<span data-ttu-id="bc686-135">Depois que você tiver um arquivo `.nupkg`, ele é publicado em nuget.org usando o comando `push`.</span><span class="sxs-lookup"><span data-stu-id="bc686-135">Once you have a `.nupkg` file, you publish it to nuget.org using the `push` command.</span></span> <span data-ttu-id="bc686-136">(Como alternativa, você pode usar o [Fluxo de trabalho de publicação do nuget.org](../create-packages/publish-a-package.md#publish-to-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="bc686-136">(Alternately, you can use the [nuget.org publishing workflow](../create-packages/publish-a-package.md#publish-to-nugetorg).</span></span>

> [!Warning]
> <span data-ttu-id="bc686-137">Os pacotes que você publica em nuget.org ficam visíveis publicamente para outros desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="bc686-137">The packages you publish to nuget.org are publicly visible to other developers.</span></span> <span data-ttu-id="bc686-138">Para hospedar pacotes de forma privada, consulte [Hospedando pacotes](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="bc686-138">To host packages privately, see [Hosting packages](../hosting-packages/overview.md).</span></span>

1. <span data-ttu-id="bc686-139">Crie uma conta gratuita em [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) ou faça logon se você já tiver uma.</span><span class="sxs-lookup"><span data-stu-id="bc686-139">Create a free account on [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), or log in if you already have one.</span></span> <span data-ttu-id="bc686-140">Criar uma nova conta envia um email de confirmação.</span><span class="sxs-lookup"><span data-stu-id="bc686-140">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="bc686-141">Você deve confirmar a conta antes de poder carregar um pacote.</span><span class="sxs-lookup"><span data-stu-id="bc686-141">You must confirm the account before you can upload a package.</span></span>

1. <span data-ttu-id="bc686-142">Depois de conectado, selecione seu nome de usuário (no canto superior direito) e selecione **Chaves de API**.</span><span class="sxs-lookup"><span data-stu-id="bc686-142">Once logged in, select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="bc686-143">Selecione **Criar**, forneça um nome para sua chave, selecione **Selecionar escopos > Push** em **Chave de API**, insira \* para **Padrão glob** e selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="bc686-143">Select **Create**, provide a name for your key, select **Select Scopes > Push** under **API Key**, enter \* for **Glob pattern**, then select **Create**.</span></span>

1. <span data-ttu-id="bc686-144">Depois que a chave é criada, selecione **Copiar** para recuperar a chave de acesso que você precisará na CLI:</span><span class="sxs-lookup"><span data-stu-id="bc686-144">Once the key is created, select **Copy** to retrieve the access key you'll need in the CLI:</span></span>

    ![Copiando a chave de API para a área de transferência](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > <span data-ttu-id="bc686-146">Salve sua chave em um local seguro e mantenha-a em segredo.</span><span class="sxs-lookup"><span data-stu-id="bc686-146">Save your key in a secure location and keep it secret.</span></span> <span data-ttu-id="bc686-147">Se a chave for revelada acidentalmente, você poderá recriá-la a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="bc686-147">If your key is accidentally revealed, you can regenerate it at any time.</span></span> <span data-ttu-id="bc686-148">Também é possível remover a chave de API, se você não quiser mais efetuar push de pacotes por meio da CLI.</span><span class="sxs-lookup"><span data-stu-id="bc686-148">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

1. <span data-ttu-id="bc686-149">Em um prompt de comando, execute o seguinte comando, especificando o nome do pacote e substituindo a chave pelo valor copiado na etapa 4:</span><span class="sxs-lookup"><span data-stu-id="bc686-149">At a command prompt, run the following command, specifying your package name and replacing the key with the value copied in step 4:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="bc686-150">O nuget.exe exibe os resultados do processo de publicação:</span><span class="sxs-lookup"><span data-stu-id="bc686-150">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. <span data-ttu-id="bc686-151">Do seu perfil no nuget.org, selecione **Gerenciar Pacotes** para ver o que você acabou de publicar.</span><span class="sxs-lookup"><span data-stu-id="bc686-151">From your profile on nuget.org, Select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="bc686-152">Você também receberá um email de confirmação.</span><span class="sxs-lookup"><span data-stu-id="bc686-152">You also receive a confirmation email.</span></span> <span data-ttu-id="bc686-153">Observe que pode levar algum tempo para o pacote ser indexado e aparecer nos resultados da pesquisa, onde outras pessoas podem encontrá-lo.</span><span class="sxs-lookup"><span data-stu-id="bc686-153">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="bc686-154">Durante esse momento, sua página do pacote mostra a mensagem abaixo:</span><span class="sxs-lookup"><span data-stu-id="bc686-154">During that time your package page shows the message below:</span></span>

    ![Esse pacote ainda não foi indexado.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> <span data-ttu-id="bc686-157">**Verificação de vírus**: todos os pacotes carregados para o nuget.org são examinados em busca de vírus e rejeitados caso algum vírus seja encontrado.</span><span class="sxs-lookup"><span data-stu-id="bc686-157">**Virus scanning**: All packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="bc686-158">Todos os pacotes listados em nuget.org também são examinados periodicamente.</span><span class="sxs-lookup"><span data-stu-id="bc686-158">All packages listed on nuget.org are also scanned periodically.</span></span>

<span data-ttu-id="bc686-159">E pronto.</span><span class="sxs-lookup"><span data-stu-id="bc686-159">And that's it!</span></span> <span data-ttu-id="bc686-160">Você acabou de publicar seu primeiro pacote do NuGet no [nuget.org](https://www.nuget.org/), o qual desenvolvedores podem usar em seus próprios projetos.</span><span class="sxs-lookup"><span data-stu-id="bc686-160">You've just published your first NuGet package to [nuget.org](https://www.nuget.org/), that other developers can use in their own projects.</span></span>

## <a name="related-topics"></a><span data-ttu-id="bc686-161">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="bc686-161">Related topics</span></span>

- [<span data-ttu-id="bc686-162">Criar um pacote</span><span class="sxs-lookup"><span data-stu-id="bc686-162">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="bc686-163">Publicar um pacote</span><span class="sxs-lookup"><span data-stu-id="bc686-163">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="bc686-164">Suporte a várias estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="bc686-164">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="bc686-165">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="bc686-165">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="bc686-166">Criando pacotes localizados</span><span class="sxs-lookup"><span data-stu-id="bc686-166">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
