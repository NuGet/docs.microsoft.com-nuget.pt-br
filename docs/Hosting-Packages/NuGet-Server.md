---
title: Usando NuGet.Server para hospedar feeds do NuGet Feeds | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Como criar e hospedar um feed de pacote do NuGet em qualquer servidor que executa o IIS usando NuGet.Server, tornando os pacotes disponíveis por meio de HTTP e OData."
keywords: Feed do NuGet, Galeria do NuGet, feed de pacote remoto, NuGet.Server
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4cb3f04954fac1b4a39284be187776ab4a19b364
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="nugetserver"></a><span data-ttu-id="305d2-104">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="305d2-104">NuGet.Server</span></span>

<span data-ttu-id="305d2-105">O NuGet.Server é um pacote fornecido pelo .NET Foundation que cria um aplicativo ASP.NET que pode hospedar um feed de pacote em qualquer servidor que executa o IIS.</span><span class="sxs-lookup"><span data-stu-id="305d2-105">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="305d2-106">Em poucas palavras, o NuGet.Server disponibiliza uma pasta no servidor por meio de HTTP(S) (especificamente OData).</span><span class="sxs-lookup"><span data-stu-id="305d2-106">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="305d2-107">É fácil de configurar e é melhor para cenários simples.</span><span class="sxs-lookup"><span data-stu-id="305d2-107">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="305d2-108">Crie um aplicativo Web ASP.NET vazio no Visual Studio e adicione o pacote do NuGet.Server a ele.</span><span class="sxs-lookup"><span data-stu-id="305d2-108">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="305d2-109">Configure a pasta `Packages` no aplicativo e adicione pacotes.</span><span class="sxs-lookup"><span data-stu-id="305d2-109">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="305d2-110">Implantar o aplicativo em um servidor adequado.</span><span class="sxs-lookup"><span data-stu-id="305d2-110">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="305d2-111">As seções a seguir abordam esse processo em detalhes usando o C#.</span><span class="sxs-lookup"><span data-stu-id="305d2-111">The following sections walk through this process in detail, using C#.</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="305d2-112">Criar e implantar um aplicativo Web ASP.NET com o NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="305d2-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="305d2-113">No Visual Studio, selecione **Arquivo > Novo > Projeto**, defina a estrutura de destino para o .NET Framework 4.6 (veja abaixo), pesquise por “ASP.NET” e selecione o modelo de C# **Aplicativo Web ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="305d2-113">In Visual Studio, select **File > New > Project**, set the target framework for .NET Framework 4.6 (see below), search for "ASP.NET", and select the **ASP.NET Web Application (.NET Framework)** template for C#.</span></span>

    ![Definindo o destino do .NET Framework 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="305d2-115">Dê um nome adequado para o aplicativo *diferente* do NuGet.Server, selecione OK e, na próxima caixa de diálogo, escolha o modelo **Vazio** e clique em OK.</span><span class="sxs-lookup"><span data-stu-id="305d2-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template and select OK.</span></span>

1. <span data-ttu-id="305d2-116">Clique com o botão direito do mouse no projeto, selecione **Gerenciar pacotes do NuGet** e, na interface do usuário do Gerenciador de Pacotes, pesquise e instale a versão mais recente do pacote do NuGet.Server se voltado para o .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="305d2-116">Right-click the project, select **Manage NuGet Packages**, and in the Package Manager UI search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="305d2-117">(Também é possível instalá-lo do Console do Gerenciador de Pacotes com `Install-Package NuGet.Server`.)</span><span class="sxs-lookup"><span data-stu-id="305d2-117">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.)</span></span>

    ![Instalando o pacote do NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > <span data-ttu-id="305d2-119">Se seu aplicativo Web destina-se ao .NET Framework 4.5.2, você precisa instalar o NuGet Server **2.10.3** em vez disso.</span><span class="sxs-lookup"><span data-stu-id="305d2-119">If your web application targets .NET Framework 4.5.2, you must install NuGet Server **2.10.3** instead.</span></span>

1. <span data-ttu-id="305d2-120">Instalar o NuGet.Server converte o aplicativo Web vazio em uma origem de pacote.</span><span class="sxs-lookup"><span data-stu-id="305d2-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="305d2-121">Ele cria uma pasta `Packages` no aplicativo e substitui `web.config` para incluir configurações adicionais (consulte os comentários no arquivo para obter detalhes).</span><span class="sxs-lookup"><span data-stu-id="305d2-121">It creates a `Packages` folder in the application and overwrites `web.config` to include additional settings (see the comments in that file for details).</span></span>

1. <span data-ttu-id="305d2-122">Para disponibilizar esses pacotes no feed quando você publicar o aplicativo em um servidor, adicione seus arquivos `.nupkg` para a pasta `Packages` no Visual Studio e, em seguida, defina sua **Ação de build** para **Conteúdo** e **Copiar para diretório de saída** para **Sempre copiar**:</span><span class="sxs-lookup"><span data-stu-id="305d2-122">To make packages available in the feed when you publish the application to a server, add their `.nupkg` files to the `Packages` folder in Visual Studio, then set their **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Copiando pacotes para a pasta Pacotes no projeto](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="305d2-124">Execute o site localmente no Visual Studio (sem depuração, que é Ctrl + F5).</span><span class="sxs-lookup"><span data-stu-id="305d2-124">Run the site locally in Visual Studio (without debugging, that is Ctrl+F5).</span></span> <span data-ttu-id="305d2-125">A página inicial fornece as URLs do feed do pacote:</span><span class="sxs-lookup"><span data-stu-id="305d2-125">The home page provides the package feed URLs:</span></span>

    ![A página inicial padrão de um aplicativo com NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="305d2-127">Clique em **aqui** na área descrita acima para ver o feed OData de pacotes.</span><span class="sxs-lookup"><span data-stu-id="305d2-127">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="305d2-128">Na primeira vez que você executar o aplicativo, o NuGet.Server reestrutura a pasta `Packages` para conter uma pasta para cada pacote.</span><span class="sxs-lookup"><span data-stu-id="305d2-128">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="305d2-129">Isso corresponde ao [layout de armazenamento local](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduzido no NuGet 3.3 para melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="305d2-129">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="305d2-130">Ao adicionar mais pacotes, continue seguindo esta estrutura.</span><span class="sxs-lookup"><span data-stu-id="305d2-130">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="305d2-131">Depois de testar sua implantação local, implante o aplicativo para qualquer outro site interno ou externo, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="305d2-131">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>
1. <span data-ttu-id="305d2-132">Uma vez implantado no `http://<domain>`, a URL que você usa para a origem do pacote será `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="305d2-132">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="305d2-133">Configurar a pasta Pacotes</span><span class="sxs-lookup"><span data-stu-id="305d2-133">Configuring the Packages folder</span></span>

<span data-ttu-id="305d2-134">Com o `NuGet.Server` 1.5 e posterior, é possível configurar a pasta de pacote mais especificamente usando o valor `appSetting/packagesPath` em `web.config`:</span><span class="sxs-lookup"><span data-stu-id="305d2-134">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="305d2-135">`packagesPath` pode ser um caminho absoluto ou virtual.</span><span class="sxs-lookup"><span data-stu-id="305d2-135">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="305d2-136">Quando o `packagesPath` for omitido ou deixado em branco, a pasta de pacotes é o `~/Packages` padrão.</span><span class="sxs-lookup"><span data-stu-id="305d2-136">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="305d2-137">Adicionar pacotes ao feed externamente</span><span class="sxs-lookup"><span data-stu-id="305d2-137">Adding packages to the feed externally</span></span>

<span data-ttu-id="305d2-138">Quando um site do NuGet.Server está em execução, você pode adicionar ou excluir pacotes usando o nuget.exe fornecido para os quais você definiu um valor de chave de API em `web.config`.</span><span class="sxs-lookup"><span data-stu-id="305d2-138">Once a NuGet.Server site is running, you can add or delete packages using nuget.exe provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="305d2-139">Depois de instalar o pacote do NuGet.Server, o `web.config` contém um valor `appSetting/apiKey` vazio:</span><span class="sxs-lookup"><span data-stu-id="305d2-139">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="305d2-140">Quando `apiKey` for omitido ou estiver em branco, o push de pacotes para o feed está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="305d2-140">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="305d2-141">Para habilitar essa capacidade, defina o `apiKey` para um valor (o ideal é uma senha forte) e adicione uma chave denominada `appSettings/requireApiKey` com o valor de `true`:</span><span class="sxs-lookup"><span data-stu-id="305d2-141">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="305d2-142">Se o servidor já está protegido ou você não exige uma chave de API (por exemplo, ao usar um servidor privado em uma rede de equipe local), é possível definir `requireApiKey` para `false`.</span><span class="sxs-lookup"><span data-stu-id="305d2-142">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="305d2-143">Todos os usuários com acesso ao servidor poderão, então, efetuar push ou excluir pacotes.</span><span class="sxs-lookup"><span data-stu-id="305d2-143">All users with access to the server can then push or delete packages.</span></span>