---
title: Instalar as ferramentas de cliente do NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: Diretrizes sobre como instalar as ferramentas de cliente, a CLI (interface de linha de comando) e o Gerenciador de Pacotes para o Visual Studio.
keywords: CLI do nuget.exe, ferramentas de cliente do NuGet, gerenciador de pacotes do NuGet, console do gerenciador de pacotes do NuGet, NuGet para Visual Studio, canal beta do NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2f67c298d269149bba9f36ad9e026d5443c39b6a
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="installing-nuget-client-tools"></a><span data-ttu-id="79c2b-104">Instalar as ferramentas de cliente do NuGet</span><span class="sxs-lookup"><span data-stu-id="79c2b-104">Installing NuGet client tools</span></span>

> [!Tip]
> <span data-ttu-id="79c2b-105">**Deseja instalar um pacote? Consulte [Guia de início rápido – Usar um pacote](../Quickstart/Use-a-Package.md).**</span><span class="sxs-lookup"><span data-stu-id="79c2b-105">**Looking to install a package? See [Quickstart - Use a package](../Quickstart/Use-a-Package.md).**</span></span>

<span data-ttu-id="79c2b-106">Há duas ferramentas primárias disponíveis para ajudar você a compilar, publicar e consumir pacotes do NuGet:</span><span class="sxs-lookup"><span data-stu-id="79c2b-106">There are two primary tools available to help you build, publish and consume NuGet packages:</span></span>

1. <span data-ttu-id="79c2b-107">A [**CLI do NuGet**](#nuget-cli) é o utilitário de linha de comando do Windows que fornece todos os recursos do NuGet; ele também pode ser executado no Mac OSX e Linux usando Mono ou por meio da CLI do .NET Core (`dotnet`).</span><span class="sxs-lookup"><span data-stu-id="79c2b-107">The [**NuGet CLI**](#nuget-cli) is the command-line utility for Windows that provides all NuGet capabilities; it can also be run on Mac OSX and Linux using Mono, or through the .NET Core CLI (`dotnet`).</span></span>
1. <span data-ttu-id="79c2b-108">O [**Gerenciador de Pacotes do NuGet no Visual Studio**](#nuget-package-manager-in-visual-studio) (somente Windows) é uma ferramenta de GUI para gerenciar pacotes e inclui um console do PowerShell por meio do qual você pode usar alguns comandos do NuGet diretamente no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="79c2b-108">The [**NuGet Package Manager in Visual Studio**](#nuget-package-manager-in-visual-studio) (Windows only) is a GUI tool for managing packages and includes a PowerShell console through which you can use certain NuGet commands directly within Visual Studio.</span></span> <span data-ttu-id="79c2b-109">A Interface do usuário e o Console do Gerenciador de Pacotes são incluídos no Visual Studio (no Windows) 2012 e posterior e podem ser instalados manualmente para versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="79c2b-109">The Package Manager UI and Console are both included with Visual Studio (on Windows) 2012 and later and can be installed manually for earlier versions.</span></span>

    <span data-ttu-id="79c2b-110">Com o Visual Studio para Mac, os recursos NuGet são incorporados diretamente.</span><span class="sxs-lookup"><span data-stu-id="79c2b-110">With Visual Studio for Mac, NuGet capabilities are built in directly.</span></span> <span data-ttu-id="79c2b-111">Consulte [Incluindo um pacote do NuGet no seu projeto](/visualstudio/mac/nuget-walkthrough) para ver uma explicação passo a passo.</span><span class="sxs-lookup"><span data-stu-id="79c2b-111">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough) for a walkthrough.</span></span>

    <span data-ttu-id="79c2b-112">No momento, o Visual Studio Code não tem suporte interno para o NuGet.</span><span class="sxs-lookup"><span data-stu-id="79c2b-112">Visual Studio Code at present does not have any built-in NuGet support.</span></span> <span data-ttu-id="79c2b-113">Usar a CLI do NuGet ou a [CLI do dotnet](../Tools/dotnet-Commands.md).</span><span class="sxs-lookup"><span data-stu-id="79c2b-113">Use the NuGet CLI or the [dotnet CLI](../Tools/dotnet-Commands.md).</span></span>

<span data-ttu-id="79c2b-114">A CLI do NuGet e o Gerenciador de Pacotes são compatíveis com as seguintes operações:</span><span class="sxs-lookup"><span data-stu-id="79c2b-114">The NuGet CLI and Package Manager both support the following operations:</span></span>

- <span data-ttu-id="79c2b-115">Pesquisar pacotes</span><span class="sxs-lookup"><span data-stu-id="79c2b-115">Search packages</span></span>
- <span data-ttu-id="79c2b-116">Instalar pacotes</span><span class="sxs-lookup"><span data-stu-id="79c2b-116">Install packages</span></span>
- <span data-ttu-id="79c2b-117">Atualizar pacotes</span><span class="sxs-lookup"><span data-stu-id="79c2b-117">Update packages</span></span>
- <span data-ttu-id="79c2b-118">Desinstalar pacotes</span><span class="sxs-lookup"><span data-stu-id="79c2b-118">Uninstall packages</span></span>
- <span data-ttu-id="79c2b-119">Restaurar os pacotes (interface do usuário somente no Gerenciador de Pacotes)</span><span class="sxs-lookup"><span data-stu-id="79c2b-119">Restore packages (UI only in the Package Manager)</span></span>
- <span data-ttu-id="79c2b-120">Gerenciar as origens do NuGet</span><span class="sxs-lookup"><span data-stu-id="79c2b-120">Manage NuGet sources</span></span>

<span data-ttu-id="79c2b-121">Os seguintes recursos são compatíveis somente com a CLI do NuGet:</span><span class="sxs-lookup"><span data-stu-id="79c2b-121">The following capabilities are supported only in the NuGet CLI:</span></span>

- <span data-ttu-id="79c2b-122">Gerenciar pacotes (nuget.org ou feed privado)</span><span class="sxs-lookup"><span data-stu-id="79c2b-122">Manage packages (nuget.org or private feed)</span></span>
- <span data-ttu-id="79c2b-123">Criar pacotes</span><span class="sxs-lookup"><span data-stu-id="79c2b-123">Create packages</span></span> 
- <span data-ttu-id="79c2b-124">Publicar pacotes</span><span class="sxs-lookup"><span data-stu-id="79c2b-124">Publish packages</span></span>
- <span data-ttu-id="79c2b-125">Gerenciar o Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="79c2b-125">Manage Nuget.Config</span></span>
- <span data-ttu-id="79c2b-126">Gerenciar o cache do NuGet</span><span class="sxs-lookup"><span data-stu-id="79c2b-126">Manage the NuGet cache</span></span>
- <span data-ttu-id="79c2b-127">Replicando um pacote</span><span class="sxs-lookup"><span data-stu-id="79c2b-127">Replicating a package</span></span>

> [!Note]
> <span data-ttu-id="79c2b-128">Outra boa ferramenta é o [Explorador de Pacotes do NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), uma ferramenta autônoma e de software livre para explorar, criar e editar visualmente os pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="79c2b-128">Another good tool is the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), an open-source, stand-alone tool to visually explore, create, and edit NuGet packages.</span></span> <span data-ttu-id="79c2b-129">Por exemplo, é muito útil fazer alterações experimentais em uma estrutura de pacote sem a necessidade de recompilar o pacote a cada vez.</span><span class="sxs-lookup"><span data-stu-id="79c2b-129">It's very helpful, for example, to make experimental changes to a package structure without having to rebuild the package each time.</span></span>
> <span data-ttu-id="79c2b-130">A cadeia de ferramentas da [CLI do .NET Core](/dotnet/articles/core/tools/index#installation) de multiplataforma, usada para desenvolver aplicativos do .NET Core, compatível com vários comandos do NuGet, como delete, locals, push, pack e restore.</span><span class="sxs-lookup"><span data-stu-id="79c2b-130">The cross-platform [.NET Core CLI](/dotnet/articles/core/tools/index#installation) toolchain, used for developing .NET Core applications, supports several NuGet commands, such as delete, locals, push, pack, and restore.</span></span> 

## <a name="nuget-cli"></a><span data-ttu-id="79c2b-131">CLI do NuGet</span><span class="sxs-lookup"><span data-stu-id="79c2b-131">NuGet CLI</span></span>

<span data-ttu-id="79c2b-132">A interface de linha de comando do NuGet fornece acesso a todos os recursos do NuGet e pode ser executada no Windows, Mac OSX e Linux, conforme descrito nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="79c2b-132">The NuGet command-line interface provides access to all NuGet capabilities, and can be run on Windows, Mac OSX, and Linux as described in the following sections.</span></span>

### <a name="windows"></a><span data-ttu-id="79c2b-133">Windows</span><span class="sxs-lookup"><span data-stu-id="79c2b-133">Windows</span></span>

<span data-ttu-id="79c2b-134">**Download direto:**</span><span class="sxs-lookup"><span data-stu-id="79c2b-134">**Direct download:**</span></span>

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> <span data-ttu-id="79c2b-135">Com o NuGet 1.4 ou superior, você pode usar `nuget update -self` para atualizar seu nuget.exe existente para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="79c2b-135">With NuGet 1.4+, you can use `nuget update -self` to update your existing nuget.exe to the latest version.</span></span>

<span data-ttu-id="79c2b-136">**Outros métodos:**</span><span class="sxs-lookup"><span data-stu-id="79c2b-136">**Other methods:**</span></span>

- <span data-ttu-id="79c2b-137">**Chocolatey**: instale o pacote [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) do Chocolatey usando o cliente do [Chocolatey](http://chocolatey.org).</span><span class="sxs-lookup"><span data-stu-id="79c2b-137">**Chocolatey**: Install the [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey package using the [Chocolatey](http://chocolatey.org) client.</span></span> 

    ```ps
    choco install nuget.commandline
    ```

- <span data-ttu-id="79c2b-138">**Visual Studio**: instale o pacote [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) do Console do Gerenciador de Pacotes no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="79c2b-138">**Visual Studio**: Install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the Package Manager Console in Visual Studio.</span></span>

    > [!Note]
    > <span data-ttu-id="79c2b-139">**Para usuários do NuGet 2.x**: devido a alterações significativas introduzidas no NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) aponta para a versão NuGet 2.x estável mais recente, a fim de impedir que os sistemas de integração contínua sejam potencialmente interrompidos.</span><span class="sxs-lookup"><span data-stu-id="79c2b-139">**For NuGet 2.x users**: Because of breaking changes introduced in NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) points to the latest stable NuGet 2.x release to prevent continuous integration systems from potentially breaking.</span></span>

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a><span data-ttu-id="79c2b-140">Mac OSX e Linux</span><span class="sxs-lookup"><span data-stu-id="79c2b-140">Mac OSX and Linux</span></span>

<span data-ttu-id="79c2b-141">No Mac OSX e Linux, há duas maneiras de executar a CLI do NuGet:</span><span class="sxs-lookup"><span data-stu-id="79c2b-141">On Mac OSX and Linux, there are two ways to run the NuGet CLI:</span></span>

- <span data-ttu-id="79c2b-142">Instale o [SDK do .NET Core](https://www.microsoft.com/net/download/core), que inclui os principais recursos do NuGet.</span><span class="sxs-lookup"><span data-stu-id="79c2b-142">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core), which includes the core NuGet capabilities.</span></span> <span data-ttu-id="79c2b-143">Downloads também são listados em [github.com/dotnet/cli](https://github.com/dotnet/cli).</span><span class="sxs-lookup"><span data-stu-id="79c2b-143">Downloads are also listed on [github.com/dotnet/cli](https://github.com/dotnet/cli).</span></span> <span data-ttu-id="79c2b-144">Se você precisar de recursos mais completos, use a segunda opção abaixo para usar `nuget.exe` com o Mono.</span><span class="sxs-lookup"><span data-stu-id="79c2b-144">If you need fuller capabilities, then use the second option below to use `nuget.exe` with Mono.</span></span>

- <span data-ttu-id="79c2b-145">Instale [Mono](http://www.mono-project.com/docs/getting-started/install/) e, em seguida, use o executável `nuget.exe` de linha de comando do Windows (versão 3.2 e posterior) de [nuget.org/downloads](https://nuget.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="79c2b-145">Install [Mono](http://www.mono-project.com/docs/getting-started/install/) and then use the `nuget.exe` command-line executable for Windows (version 3.2 and later) from [nuget.org/downloads](https://nuget.org/downloads).</span></span> <span data-ttu-id="79c2b-146">Executar o NuGet em Mono está sujeito às seguintes limitações:</span><span class="sxs-lookup"><span data-stu-id="79c2b-146">Running NuGet on Mono is subject to the following limitations:</span></span>

    - <span data-ttu-id="79c2b-147">Comandos testados que funcionam:</span><span class="sxs-lookup"><span data-stu-id="79c2b-147">Commands tested to work:</span></span>
        - <span data-ttu-id="79c2b-148">config</span><span class="sxs-lookup"><span data-stu-id="79c2b-148">config</span></span>
        - <span data-ttu-id="79c2b-149">excluir</span><span class="sxs-lookup"><span data-stu-id="79c2b-149">delete</span></span>
        - <span data-ttu-id="79c2b-150">help</span><span class="sxs-lookup"><span data-stu-id="79c2b-150">help</span></span>
        - <span data-ttu-id="79c2b-151">install</span><span class="sxs-lookup"><span data-stu-id="79c2b-151">install</span></span>
        - <span data-ttu-id="79c2b-152">lista</span><span class="sxs-lookup"><span data-stu-id="79c2b-152">list</span></span>
        - <span data-ttu-id="79c2b-153">push</span><span class="sxs-lookup"><span data-stu-id="79c2b-153">push</span></span>
        - <span data-ttu-id="79c2b-154">setApiKey</span><span class="sxs-lookup"><span data-stu-id="79c2b-154">setApiKey</span></span>
        - <span data-ttu-id="79c2b-155">origens</span><span class="sxs-lookup"><span data-stu-id="79c2b-155">sources</span></span>
        - <span data-ttu-id="79c2b-156">spec</span><span class="sxs-lookup"><span data-stu-id="79c2b-156">spec</span></span>

    - <span data-ttu-id="79c2b-157">Comandos que funcionam parcialmente:</span><span class="sxs-lookup"><span data-stu-id="79c2b-157">Partially-working commands:</span></span>
        - <span data-ttu-id="79c2b-158">pack: funciona com arquivos `.nuspec`, mas não com arquivos de projeto.</span><span class="sxs-lookup"><span data-stu-id="79c2b-158">pack: works with `.nuspec` files but not with project files.</span></span>
        - <span data-ttu-id="79c2b-159">restore: funciona com arquivos `packages.config` e `project.json`, mas não com arquivos (`.sln`) da solução.</span><span class="sxs-lookup"><span data-stu-id="79c2b-159">restore: works with `packages.config` and `project.json` files but not with solution (`.sln`) files.</span></span>

    - <span data-ttu-id="79c2b-160">Comandos que não funcionam:</span><span class="sxs-lookup"><span data-stu-id="79c2b-160">Commands that do not work:</span></span>
        - <span data-ttu-id="79c2b-161">atualizar</span><span class="sxs-lookup"><span data-stu-id="79c2b-161">update</span></span>

### <a name="related-topics"></a><span data-ttu-id="79c2b-162">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="79c2b-162">Related topics</span></span>

- [<span data-ttu-id="79c2b-163">Referência da CLI do NuGet</span><span class="sxs-lookup"><span data-stu-id="79c2b-163">NuGet CLI reference</span></span>](../tools/nuget-exe-cli-reference.md)
- [<span data-ttu-id="79c2b-164">Criando um pacote</span><span class="sxs-lookup"><span data-stu-id="79c2b-164">Creating a package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="79c2b-165">Publicando um pacote</span><span class="sxs-lookup"><span data-stu-id="79c2b-165">Publishing a Package</span></span>](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a><span data-ttu-id="79c2b-166">Gerenciador de Pacotes do NuGet no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="79c2b-166">NuGet Package Manager in Visual Studio</span></span>

<span data-ttu-id="79c2b-167">O Gerenciador de Pacotes do NuGet está incluído em todas as edições do Visual Studio no Windows 2012 e posterior.</span><span class="sxs-lookup"><span data-stu-id="79c2b-167">The NuGet Package Manager is included in every edition of Visual Studio on Windows, 2012 and later.</span></span> <span data-ttu-id="79c2b-168">Ele inclui a interface do usuário do Gerenciador de Pacotes ([referência](../tools/package-manager-ui.md)) e o Console do Gerenciador de Pacotes por meio do qual você pode acessar as ferramentas que vêm com determinados pacotes ([referência](../tools/package-manager-console.md)).</span><span class="sxs-lookup"><span data-stu-id="79c2b-168">It includes the Package Manager UI ([reference](../tools/package-manager-ui.md)), and the Package Manager Console through which you can access tools that come with certain packages ([reference](../tools/package-manager-console.md)).</span></span>

<span data-ttu-id="79c2b-169">O instalador do Visual Studio 2017 inclui o Gerenciador de Pacotes do NuGet com qualquer carga de trabalho que utiliza o .NET.</span><span class="sxs-lookup"><span data-stu-id="79c2b-169">The Visual Studio 2017 installer includes the NuGet Package Manager with any workload that employs .NET.</span></span> <span data-ttu-id="79c2b-170">Para instalar separadamente ou para verificar se o Gerenciador de Pacotes está instalado, execute o instalador do Visual Studio 2017 e marque a opção em **Componentes individuais > Ferramentas de código > Gerenciador de pacotes do NuGet**.</span><span class="sxs-lookup"><span data-stu-id="79c2b-170">To install separately, or to verify that the Package Manager is installed, run the Visual Studio 2017 installer and check the option under **Individual Components > Code tools > NuGet package manager**.</span></span>

> [!Note]
> <span data-ttu-id="79c2b-171">O console requer o [PowerShell 2.0](http://support.microsoft.com/kb/968929), que já estará instalado no Windows 7 ou superior e Windows Server 2008 R2 ou superior.</span><span class="sxs-lookup"><span data-stu-id="79c2b-171">The console requires [PowerShell 2.0](http://support.microsoft.com/kb/968929), which will already be installed on Windows 7 or higher and Windows Server 2008 R2 or higher.</span></span>
>
> <span data-ttu-id="79c2b-172">Comandos do Console do Gerenciador de Pacotes também funcionam apenas dentro do Visual Studio no Windows.</span><span class="sxs-lookup"><span data-stu-id="79c2b-172">Package Manager Console commands also work only within Visual Studio on Windows.</span></span> <span data-ttu-id="79c2b-173">Use a CLI do NuGet fora do ambiente, incluindo com o Visual Studio para Mac e o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="79c2b-173">Use the NuGet CLI outside of that environment, including with Visual Studio for Mac and Visual Studio Code.</span></span>

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a><span data-ttu-id="79c2b-174">Instalação do Gerenciador de Pacotes para Visual Studio 2010 e anterior</span><span class="sxs-lookup"><span data-stu-id="79c2b-174">Package Manager installation for Visual Studio 2010 and earlier</span></span>

<span data-ttu-id="79c2b-175">*Essas etapas não são necessárias para o Visual Studio 2012 e versões posteriores, que já incluem o Gerenciador de Pacotes.*</span><span class="sxs-lookup"><span data-stu-id="79c2b-175">*These steps are not necessary for Visual Studio 2012 and later, which already include the Package Manager.*</span></span>

1. <span data-ttu-id="79c2b-176">No Visual Studio 2010 e versões anteriores, clique em **Ferramentas > Extensão e atualizações**.</span><span class="sxs-lookup"><span data-stu-id="79c2b-176">In Visual Studio 2010 and earlier, click **Tools > Extension and Updates**.</span></span>
1. <span data-ttu-id="79c2b-177">Navegue até **Online**, pesquise “Gerenciador de Pacotes do NuGet para Visual Studio” e clique em **Baixar**.</span><span class="sxs-lookup"><span data-stu-id="79c2b-177">Navigate to **Online**, then search for "NuGet Package Manager for Visual Studio" and click **Download**.</span></span>
1. <span data-ttu-id="79c2b-178">Na caixa de diálogo Instalador, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="79c2b-178">In the Installer dialog box, click **Install**.</span></span>
1. <span data-ttu-id="79c2b-179">Quando a instalação for concluída, reinicie o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="79c2b-179">When installation is complete, restart Visual Studio.</span></span>

> [!Tip]
> <span data-ttu-id="79c2b-180">Se você não conseguir usar a caixa de diálogo **Extensões e atualizações** no Visual Studio (por exemplo, se estiver bloqueado por um proxy), poderá baixar as extensões para o Visual Studio 2013 e 2015 diretamente no [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="79c2b-180">If you're unable to use the **Extensions and Updates** dialog in Visual Studio (for example, its blocked by a proxy), you can download extensions for Visual Studio 2013 and 2015 directly at [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

### <a name="updating-the-package-manager"></a><span data-ttu-id="79c2b-181">Atualizando o Gerenciador de Pacotes</span><span class="sxs-lookup"><span data-stu-id="79c2b-181">Updating the Package Manager</span></span>

<span data-ttu-id="79c2b-182">Para o Visual Studio 2015 Atualização 2 e posterior, o Gerenciador de Pacotes é atualizado automaticamente para a versão estável mais recente.</span><span class="sxs-lookup"><span data-stu-id="79c2b-182">For Visual Studio 2015 Update 2 and later, the Package Manager is automatically updated to the latest stable release.</span></span>

<span data-ttu-id="79c2b-183">Para o Visual Studio 2015 Atualização 1 e anterior, selecione o comando **Ferramentas > Extensões e Atualizações** e clique na guia **Atualizações** para ver se uma nova versão do Gerenciador de Pacotes está disponível.</span><span class="sxs-lookup"><span data-stu-id="79c2b-183">For Visual Studio 2015 Update 1 and earlier, select the **Tools > Extensions and Updates** command and click on the **Updates** tab to see if a new version of the Package Manager is available.</span></span>  

### <a name="nuget-previews"></a><span data-ttu-id="79c2b-184">Visualizações do NuGet</span><span class="sxs-lookup"><span data-stu-id="79c2b-184">NuGet previews</span></span>

<span data-ttu-id="79c2b-185">Se você quiser visualizar futuros recursos do NuGet, instale o [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), que funciona lado a lado com as versões estáveis do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="79c2b-185">If you'd like to preview upcoming NuGet features, install the [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), which works side-by-side with stable releases of Visual Studio.</span></span>

<span data-ttu-id="79c2b-186">Observe que o Canal Beta do NuGet anterior (`https://dotnet.myget.org/F/nuget-beta/vsix/`) para Visual Studio 2015 não é mais usado.</span><span class="sxs-lookup"><span data-stu-id="79c2b-186">Note that the previous NuGet Beta Channel (`https://dotnet.myget.org/F/nuget-beta/vsix/`) for Visual Studio 2015 is no longer used.</span></span>

<span data-ttu-id="79c2b-187">Para relatar problemas com qualquer versão do NuGet ou compartilhar ideias, abra um problema no [repositório GitHub do NuGet](https://github.com/Nuget/Home).</span><span class="sxs-lookup"><span data-stu-id="79c2b-187">To report problems with any release of NuGet or to share ideas, open an issue on the [NuGet GitHub repository](https://github.com/Nuget/Home).</span></span>

### <a name="related-topics"></a><span data-ttu-id="79c2b-188">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="79c2b-188">Related topics</span></span>

- [<span data-ttu-id="79c2b-189">Referência da interface do usuário do Gerenciador de Pacotes</span><span class="sxs-lookup"><span data-stu-id="79c2b-189">Package Manager UI reference</span></span>](../tools/package-manager-ui.md)
- [<span data-ttu-id="79c2b-190">Referência do Console do Gerenciador de Pacotes</span><span class="sxs-lookup"><span data-stu-id="79c2b-190">Package Manager Console reference</span></span>](../tools/package-manager-console.md)
- [<span data-ttu-id="79c2b-191">Referência do PowerShell do Console do Gerenciador de Pacotes</span><span class="sxs-lookup"><span data-stu-id="79c2b-191">Package Manager Console PowerShell reference</span></span>](../tools/powershell-reference.md)