---
title: Usando NuGet.Server para hospedar feeds do NuGet
description: Como criar e hospedar um feed de pacote do NuGet em qualquer servidor que executa o IIS usando NuGet.Server, tornando os pacotes disponíveis por meio de HTTP e OData.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: b1ef1764b28631c3032ac23a250dedece7803ae6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817961"
---
# <a name="nugetserver"></a><span data-ttu-id="a6115-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="a6115-103">NuGet.Server</span></span>

<span data-ttu-id="a6115-104">O NuGet.Server é um pacote fornecido pelo .NET Foundation que cria um aplicativo ASP.NET que pode hospedar um feed de pacote em qualquer servidor que executa o IIS.</span><span class="sxs-lookup"><span data-stu-id="a6115-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="a6115-105">Em poucas palavras, o NuGet.Server disponibiliza uma pasta no servidor por meio de HTTP(S) (especificamente OData).</span><span class="sxs-lookup"><span data-stu-id="a6115-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="a6115-106">É fácil de configurar e é melhor para cenários simples.</span><span class="sxs-lookup"><span data-stu-id="a6115-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="a6115-107">Crie um aplicativo Web ASP.NET vazio no Visual Studio e adicione o pacote do NuGet.Server a ele.</span><span class="sxs-lookup"><span data-stu-id="a6115-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="a6115-108">Configure a pasta `Packages` no aplicativo e adicione pacotes.</span><span class="sxs-lookup"><span data-stu-id="a6115-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="a6115-109">Implantar o aplicativo em um servidor adequado.</span><span class="sxs-lookup"><span data-stu-id="a6115-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="a6115-110">As seções a seguir abordam esse processo em detalhes usando o C#.</span><span class="sxs-lookup"><span data-stu-id="a6115-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="a6115-111">Caso tenha outras dúvidas sobre o NuGet.Server, crie um problema no [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="a6115-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="a6115-112">Criar e implantar um aplicativo Web ASP.NET com o NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="a6115-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="a6115-113">No Visual Studio, selecione **Arquivo > Novo > Projeto**, pesquise "ASP.NET", selecione o modelo de C# **Aplicativo Web ASP.NET (.NET Framework)** e defina **Estrutura** como ".NET Framework 4.6":</span><span class="sxs-lookup"><span data-stu-id="a6115-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET", select the **ASP.NET Web Application (.NET Framework)** template for C#, and set **Framework** to ".NET Framework 4.6":</span></span>

    ![Definindo a estrutura de destino para um novo projeto](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="a6115-115">Dê um nome adequado ao aplicativo *diferente* de NuGet.Server, selecione OK e, na próxima caixa de diálogo, selecione o modelo **Vazio** e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="a6115-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

1. <span data-ttu-id="a6115-116">Clique com o botão direito do mouse no projeto e escolha **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a6115-116">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="a6115-117">Na interface do usuário do Gerenciador de Pacotes, selecione a guia **Procurar** e, em seguida, pesquise e instale a versão mais recente do pacote NuGet.Server se você estiver direcionando para o .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="a6115-117">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="a6115-118">(Também é possível instalá-lo do Console do Gerenciador de Pacotes com `Install-Package NuGet.Server`.) Se solicitado, aceite os termos de licença.</span><span class="sxs-lookup"><span data-stu-id="a6115-118">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Instalando o pacote do NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

1. <span data-ttu-id="a6115-120">Instalar o NuGet.Server converte o aplicativo Web vazio em uma origem de pacote.</span><span class="sxs-lookup"><span data-stu-id="a6115-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="a6115-121">Ele instala uma variedade de outros pacotes, cria uma pasta `Packages` no aplicativo e modifica `web.config` para incluir as configurações adicionais (veja os comentários no arquivo para obter detalhes).</span><span class="sxs-lookup"><span data-stu-id="a6115-121">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="a6115-122">Inspecione cuidadosamente `web.config` depois que o pacote NuGet.Server tiver concluído as modificações desse arquivo.</span><span class="sxs-lookup"><span data-stu-id="a6115-122">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="a6115-123">O NuGet.Server talvez não substituirá os elementos existentes, mas criará elementos duplicados.</span><span class="sxs-lookup"><span data-stu-id="a6115-123">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="a6115-124">Essas duplicatas provocarão um "Erro Interno do Servidor" quando você tentar executar o projeto mais tarde.</span><span class="sxs-lookup"><span data-stu-id="a6115-124">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="a6115-125">Por exemplo, se o seu `web.config` contiver `<compilation debug="true" targetFramework="4.5.2" />` antes de instalar o NuGet.Server, o pacote não o substituirá, mas sim inserirá um segundo `<compilation debug="true" targetFramework="4.6" />`.</span><span class="sxs-lookup"><span data-stu-id="a6115-125">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="a6115-126">Nesse caso, exclua o elemento com a versão mais antiga da estrutura.</span><span class="sxs-lookup"><span data-stu-id="a6115-126">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="a6115-127">Para disponibilizar esses pacotes no feed quando você publicar o aplicativo em um servidor, adicione os arquivos `.nupkg` à pasta `Packages` no Visual Studio e, em seguida, defina a **Ação de Build** deles como **Conteúdo** e **Copiar para Diretório de Saída** como **Sempre copiar**:</span><span class="sxs-lookup"><span data-stu-id="a6115-127">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Copiando pacotes para a pasta Pacotes no projeto](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="a6115-129">Execute o site localmente no Visual Studio (usando **Depurar > Iniciar sem Depurar** ou Ctrl + F5).</span><span class="sxs-lookup"><span data-stu-id="a6115-129">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="a6115-130">A home page fornece as URLs do feed do pacote, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="a6115-130">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="a6115-131">Se você encontrar erros, inspecione cuidadosamente o `web.config` para verificar se há elementos duplicados, conforme observado anteriormente na etapa 5.</span><span class="sxs-lookup"><span data-stu-id="a6115-131">If you see errors, carefully inspect your `web.config` for duplicate elements are noted earlier with step 5.</span></span>

    ![A página inicial padrão de um aplicativo com NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="a6115-133">Clique em **aqui** na área descrita acima para ver o feed OData de pacotes.</span><span class="sxs-lookup"><span data-stu-id="a6115-133">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="a6115-134">Na primeira vez que você executar o aplicativo, o NuGet.Server reestrutura a pasta `Packages` para conter uma pasta para cada pacote.</span><span class="sxs-lookup"><span data-stu-id="a6115-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="a6115-135">Isso corresponde ao [layout de armazenamento local](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduzido no NuGet 3.3 para melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="a6115-135">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="a6115-136">Ao adicionar mais pacotes, continue seguindo esta estrutura.</span><span class="sxs-lookup"><span data-stu-id="a6115-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="a6115-137">Depois de testar sua implantação local, implante o aplicativo para qualquer outro site interno ou externo, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="a6115-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="a6115-138">Uma vez implantado no `http://<domain>`, a URL que você usa para a origem do pacote será `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="a6115-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="a6115-139">Configurar a pasta Pacotes</span><span class="sxs-lookup"><span data-stu-id="a6115-139">Configuring the Packages folder</span></span>

<span data-ttu-id="a6115-140">Com o `NuGet.Server` 1.5 e posterior, é possível configurar a pasta de pacote mais especificamente usando o valor `appSetting/packagesPath` em `web.config`:</span><span class="sxs-lookup"><span data-stu-id="a6115-140">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="a6115-141">`packagesPath` pode ser um caminho absoluto ou virtual.</span><span class="sxs-lookup"><span data-stu-id="a6115-141">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="a6115-142">Quando o `packagesPath` for omitido ou deixado em branco, a pasta de pacotes é o `~/Packages` padrão.</span><span class="sxs-lookup"><span data-stu-id="a6115-142">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="a6115-143">Adicionar pacotes ao feed externamente</span><span class="sxs-lookup"><span data-stu-id="a6115-143">Adding packages to the feed externally</span></span>

<span data-ttu-id="a6115-144">Quando um site do NuGet.Server está em execução, você pode adicionar pacotes usando o comando [nuget push](../tools/cli-ref-push.md), desde que você defina um valor de chave de API em `web.config`.</span><span class="sxs-lookup"><span data-stu-id="a6115-144">Once a NuGet.Server site is running, you can add packages using [nuget push](../tools/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="a6115-145">Depois de instalar o pacote do NuGet.Server, o `web.config` contém um valor `appSetting/apiKey` vazio:</span><span class="sxs-lookup"><span data-stu-id="a6115-145">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="a6115-146">Quando `apiKey` for omitido ou estiver em branco, o push de pacotes para o feed está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="a6115-146">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="a6115-147">Para habilitar essa capacidade, defina o `apiKey` para um valor (o ideal é uma senha forte) e adicione uma chave denominada `appSettings/requireApiKey` com o valor de `true`:</span><span class="sxs-lookup"><span data-stu-id="a6115-147">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="a6115-148">Se o servidor já está protegido ou você não exige uma chave de API (por exemplo, ao usar um servidor privado em uma rede de equipe local), é possível definir `requireApiKey` para `false`.</span><span class="sxs-lookup"><span data-stu-id="a6115-148">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="a6115-149">Todos os usuários com acesso ao servidor poderão efetuar push dos pacotes.</span><span class="sxs-lookup"><span data-stu-id="a6115-149">All users with access to the server can then push packages.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="a6115-150">Removendo pacotes do feed</span><span class="sxs-lookup"><span data-stu-id="a6115-150">Removing packages from the feed</span></span>

<span data-ttu-id="a6115-151">Com o NuGet.Server, o comando [nuget delete](../tools/cli-ref-delete.md) remove um pacote do repositório, desde que você inclua a chave de API com o comentário.</span><span class="sxs-lookup"><span data-stu-id="a6115-151">With NuGet.Server, the [nuget delete](../tools/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="a6115-152">Se, em vez disso, você desejar alterar o comportamento para remover o pacote da lista (deixando-o disponível para a restauração de pacote), altere a chave `enableDelisting` em `web.config` para true.</span><span class="sxs-lookup"><span data-stu-id="a6115-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="a6115-153">Suporte do NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="a6115-153">NuGet.Server support</span></span>

<span data-ttu-id="a6115-154">Para obter ajuda adicional sobre o uso do NuGet.Server, crie um problema no [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="a6115-154">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>