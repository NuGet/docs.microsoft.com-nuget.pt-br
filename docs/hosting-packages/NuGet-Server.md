---
title: Usando NuGet.Server para hospedar feeds do NuGet
description: Como criar e hospedar um feed de pacote do NuGet em qualquer servidor que executa o IIS usando NuGet.Server, tornando os pacotes disponíveis por meio de HTTP e OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 098375b2bba13675ba5d80a27e0226dc2ee39e77
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79059502"
---
# <a name="nugetserver"></a><span data-ttu-id="1bf3b-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="1bf3b-103">NuGet.Server</span></span>

<span data-ttu-id="1bf3b-104">O NuGet.Server é um pacote fornecido pelo .NET Foundation que cria um aplicativo ASP.NET que pode hospedar um feed de pacote em qualquer servidor que executa o IIS.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="1bf3b-105">Em poucas palavras, o NuGet.Server disponibiliza uma pasta no servidor por meio de HTTP(S) (especificamente OData).</span><span class="sxs-lookup"><span data-stu-id="1bf3b-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="1bf3b-106">É fácil de configurar e é melhor para cenários simples.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="1bf3b-107">Crie um aplicativo Web ASP.NET vazio no Visual Studio e adicione o pacote do NuGet.Server a ele.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="1bf3b-108">Configure a pasta `Packages` no aplicativo e adicione pacotes.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="1bf3b-109">Implantar o aplicativo em um servidor adequado.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="1bf3b-110">As seções a seguir abordam esse processo em detalhes usando o C#.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="1bf3b-111">Se você tiver mais perguntas sobre nuGet.server, crie um problema em [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="1bf3b-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="1bf3b-112">Criar e implantar um aplicativo Web ASP.NET com o NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="1bf3b-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="1bf3b-113">No Visual Studio, selecione **Arquivo > Novo Projeto >,** procure "ASP.NET Web Application (.NET Framework)", selecione o modelo correspondente para C#.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET Web Application (.NET Framework)", select the matching template for C#.</span></span>

    ![Selecione o modelo de projeto web do .NET Framework](media/Hosting_00-NuGet.Server-ProjectType.png)

1. <span data-ttu-id="1bf3b-115">Definir **framework** para ".NET Framework 4.6".</span><span class="sxs-lookup"><span data-stu-id="1bf3b-115">Set **Framework** to ".NET Framework 4.6".</span></span>

    ![Definindo a estrutura de destino para um novo projeto](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="1bf3b-117">Dê um nome adequado ao aplicativo *diferente* de NuGet.Server, selecione OK e, na próxima caixa de diálogo, selecione o modelo **Vazio** e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-117">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

    ![Selecione o projeto web vazio](media/Hosting_02-NuGet.Server-Empty.png)

1. <span data-ttu-id="1bf3b-119">Clique com o botão direito do mouse no projeto e escolha **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-119">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="1bf3b-120">Na interface do usuário do Gerenciador de Pacotes, selecione a guia **Procurar** e, em seguida, pesquise e instale a versão mais recente do pacote NuGet.Server se você estiver direcionando para o .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-120">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="1bf3b-121">(Você também pode instalá-lo `Install-Package NuGet.Server`no Console do Gerenciador de Pacotes com .) Aceite os termos da licença se solicitado.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-121">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Instalando o pacote do NuGet.Server](media/Hosting_03-NuGet.Server-Package.png)

1. <span data-ttu-id="1bf3b-123">Instalar o NuGet.Server converte o aplicativo Web vazio em uma origem de pacote.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-123">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="1bf3b-124">Ele instala uma variedade de outros pacotes, cria uma pasta `Packages` no aplicativo e modifica `web.config` para incluir as configurações adicionais (veja os comentários no arquivo para obter detalhes).</span><span class="sxs-lookup"><span data-stu-id="1bf3b-124">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="1bf3b-125">Inspecione cuidadosamente `web.config` depois que o pacote NuGet.Server tiver concluído as modificações desse arquivo.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-125">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="1bf3b-126">O NuGet.Server talvez não substituirá os elementos existentes, mas criará elementos duplicados.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-126">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="1bf3b-127">Essas duplicatas provocarão um "Erro Interno do Servidor" quando você tentar executar o projeto mais tarde.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-127">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="1bf3b-128">Por exemplo, se o seu `web.config` contiver `<compilation debug="true" targetFramework="4.5.2" />` antes de instalar o NuGet.Server, o pacote não o substituirá, mas sim inserirá um segundo `<compilation debug="true" targetFramework="4.6" />`.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-128">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="1bf3b-129">Nesse caso, exclua o elemento com a versão mais antiga da estrutura.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-129">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="1bf3b-130">Execute o site localmente no Visual Studio (usando **Depurar > Iniciar sem Depurar** ou Ctrl + F5).</span><span class="sxs-lookup"><span data-stu-id="1bf3b-130">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="1bf3b-131">A home page fornece as URLs do feed do pacote, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-131">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="1bf3b-132">Se você vir erros, `web.config` inspecione cuidadosamente os elementos duplicados, como observado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-132">If you see errors, carefully inspect your `web.config` for duplicate elements as noted earlier.</span></span>

    ![A página inicial padrão de um aplicativo com NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  <span data-ttu-id="1bf3b-134">Na primeira vez que você executar o aplicativo, o NuGet.Server reestrutura a pasta `Packages` para conter uma pasta para cada pacote.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="1bf3b-135">Isso corresponde ao [layout de armazenamento local](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduzido no NuGet 3.3 para melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-135">This matches the [local storage layout](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="1bf3b-136">Ao adicionar mais pacotes, continue seguindo esta estrutura.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="1bf3b-137">Depois de testar sua implantação local, implante o aplicativo para qualquer outro site interno ou externo, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="1bf3b-138">Uma vez implantado no `http://<domain>`, a URL que você usa para a origem do pacote será `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="1bf3b-139">Adicionar pacotes ao feed externamente</span><span class="sxs-lookup"><span data-stu-id="1bf3b-139">Adding packages to the feed externally</span></span>

<span data-ttu-id="1bf3b-140">Quando um site do NuGet.Server está em execução, você pode adicionar pacotes usando o comando [nuget push](../reference/cli-reference/cli-ref-push.md), desde que você defina um valor de chave de API em `web.config`.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-140">Once a NuGet.Server site is running, you can add packages using [nuget push](../reference/cli-reference/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="1bf3b-141">Depois de instalar o pacote do NuGet.Server, o `web.config` contém um valor `appSetting/apiKey` vazio:</span><span class="sxs-lookup"><span data-stu-id="1bf3b-141">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="1bf3b-142">Quando `apiKey` for omitido ou estiver em branco, o push de pacotes para o feed está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-142">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="1bf3b-143">Para habilitar essa capacidade, defina o `apiKey` para um valor (o ideal é uma senha forte) e adicione uma chave denominada `appSettings/requireApiKey` com o valor de `true`:</span><span class="sxs-lookup"><span data-stu-id="1bf3b-143">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="1bf3b-144">Se o servidor já está protegido ou você não exige uma chave de API (por exemplo, ao usar um servidor privado em uma rede de equipe local), é possível definir `requireApiKey` para `false`.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-144">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="1bf3b-145">Todos os usuários com acesso ao servidor poderão efetuar push dos pacotes.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-145">All users with access to the server can then push packages.</span></span>

<span data-ttu-id="1bf3b-146">Começando pelo NuGet.Server 3.0.0, a URL para `http://<domain>/nuget`empurrar pacotes foi mudada para .</span><span class="sxs-lookup"><span data-stu-id="1bf3b-146">Starting with NuGet.Server 3.0.0, the URL for pushing packages was change to `http://<domain>/nuget`.</span></span> <span data-ttu-id="1bf3b-147">Antes da versão 3.0.0, a `http://<domain>/api/v2/package`URL push era .</span><span class="sxs-lookup"><span data-stu-id="1bf3b-147">Prior to the 3.0.0 release, the push URL was `http://<domain>/api/v2/package`.</span></span>

<span data-ttu-id="1bf3b-148">Com o NuGet 3.2.1 e `/api/v2/package` mais novo, essa `/nuget` URL `enableLegacyPushRoute: true` herdada é habilitada, além de por padrão, via opção na configuração de inicialização (por`NuGetODataConfig.cs` padrão).</span><span class="sxs-lookup"><span data-stu-id="1bf3b-148">With NuGet 3.2.1 and newer, this legacy URL `/api/v2/package` is enabled in addition to `/nuget` by default via `enableLegacyPushRoute: true` option in your startup config (`NuGetODataConfig.cs` by default).</span></span> <span data-ttu-id="1bf3b-149">Observe que esse recurso não funciona quando vários feeds são hospedados no mesmo projeto.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-149">Note that this feature does not work when multiple feeds are hosted in the same project.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="1bf3b-150">Removendo pacotes do feed</span><span class="sxs-lookup"><span data-stu-id="1bf3b-150">Removing packages from the feed</span></span>

<span data-ttu-id="1bf3b-151">Com o NuGet.Server, o comando [nuget delete](../reference/cli-reference/cli-ref-delete.md) remove um pacote do repositório, desde que você inclua a chave de API com o comentário.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-151">With NuGet.Server, the [nuget delete](../reference/cli-reference/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="1bf3b-152">Se, em vez disso, você desejar alterar o comportamento para remover o pacote da lista (deixando-o disponível para a restauração de pacote), altere a chave `enableDelisting` em `web.config` para true.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="1bf3b-153">Configurar a pasta Pacotes</span><span class="sxs-lookup"><span data-stu-id="1bf3b-153">Configuring the Packages folder</span></span>

<span data-ttu-id="1bf3b-154">Com `NuGet.Server` 1,5 e posterior, você pode `appSettings/packagesPath` personalizar `web.config`a pasta do pacote usando o valor em :</span><span class="sxs-lookup"><span data-stu-id="1bf3b-154">With `NuGet.Server` 1.5 and later, you can customize the package folder using the `appSettings/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="1bf3b-155">`packagesPath` pode ser um caminho absoluto ou virtual.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-155">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="1bf3b-156">Quando o `packagesPath` for omitido ou deixado em branco, a pasta de pacotes é o `~/Packages` padrão.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-156">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="making-packages-available-when-you-publish-the-web-app"></a><span data-ttu-id="1bf3b-157">Disponibilizando pacotes quando você publica o aplicativo web</span><span class="sxs-lookup"><span data-stu-id="1bf3b-157">Making packages available when you publish the web app</span></span>

<span data-ttu-id="1bf3b-158">Para disponibilizar esses pacotes no feed quando você publicar o aplicativo em um servidor, adicione os arquivos `.nupkg` à pasta `Packages` no Visual Studio e, em seguida, defina a **Ação de Build** deles como **Conteúdo** e **Copiar para Diretório de Saída** como **Sempre copiar**:</span><span class="sxs-lookup"><span data-stu-id="1bf3b-158">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

![Copiando pacotes para a pasta Pacotes no projeto](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a><span data-ttu-id="1bf3b-160">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="1bf3b-160">Release Notes</span></span>

<span data-ttu-id="1bf3b-161">As notas de versão do NuGet.Server estão disponíveis na página de versão do [GitHub](https://github.com/NuGet/NuGet.Server/releases).</span><span class="sxs-lookup"><span data-stu-id="1bf3b-161">Release notes for NuGet.Server are available on the [GitHub release page](https://github.com/NuGet/NuGet.Server/releases).</span></span>
<span data-ttu-id="1bf3b-162">Isso inclui detalhes sobre correções de bugs e novos recursos que são adicionados.</span><span class="sxs-lookup"><span data-stu-id="1bf3b-162">This includes details about bug fixes and new features that are added.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="1bf3b-163">Suporte do NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="1bf3b-163">NuGet.Server support</span></span>

<span data-ttu-id="1bf3b-164">Para obter ajuda adicional usando nuGet.server, crie um problema em [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="1bf3b-164">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>
