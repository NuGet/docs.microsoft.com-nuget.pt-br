---
title: Instalar e gerenciar pacotes do NuGet usando o console no Visual Studio
description: Instruções para usar o Console do Gerenciador de pacotes do NuGet no Visual Studio para trabalhar com pacotes.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 42031f7b5fe4d3c1b4dbe5e1bfbf9197014e0e88
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428950"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="73c6b-103">Instalar e gerenciar pacotes com o Console do Gerenciador de Pacotes no Visual Studio (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="73c6b-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="73c6b-104">O Console do Gerenciador de pacotes do NuGet possibilita usar os [comandos do PowerShell para NuGet](../reference/powershell-reference.md) para localizar, instalar, desinstalar e atualizar os pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="73c6b-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../reference/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="73c6b-105">O uso do console é necessário nos casos em que a interface do usuário do Gerenciador de Pacotes não fornece uma maneira de executar uma operação.</span><span class="sxs-lookup"><span data-stu-id="73c6b-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="73c6b-106">Para usar os comandos da CLI `nuget.exe` no console, confira [Usar a CLI nuget.exe no console](#use-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="73c6b-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#use-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="73c6b-107">O console é integrado ao Visual Studio no Windows.</span><span class="sxs-lookup"><span data-stu-id="73c6b-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="73c6b-108">Ele não está incluído no Visual Studio para Mac ou no Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="73c6b-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="73c6b-109">Encontrar e instalar um pacote</span><span class="sxs-lookup"><span data-stu-id="73c6b-109">Find and install a package</span></span>

<span data-ttu-id="73c6b-110">Por exemplo, encontrar e instalar um pacote é feito com três etapas fáceis:</span><span class="sxs-lookup"><span data-stu-id="73c6b-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="73c6b-111">Abra o projeto/solução no Visual Studio e abra o console usando o comando **Ferramentas > Gerenciador de pacotes do NuGet > Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="73c6b-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="73c6b-112">Localize o pacote que você deseja instalar.</span><span class="sxs-lookup"><span data-stu-id="73c6b-112">Find the package you want to install.</span></span> <span data-ttu-id="73c6b-113">Se já sabe qual é, pule para a etapa 3.</span><span class="sxs-lookup"><span data-stu-id="73c6b-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="73c6b-114">Execute o comando de instalação:</span><span class="sxs-lookup"><span data-stu-id="73c6b-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="73c6b-115">Todas as operações que estão disponíveis no console também podem ser feitas com a [CLI NuGet](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="73c6b-115">All operations that are available in the console can also be done with the [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="73c6b-116">No entanto, os comandos do console operam dentro do contexto do Visual Studio e de um projeto/solução salvo e, muitas vezes, executam mais do que seus comandos equivalentes de CLI.</span><span class="sxs-lookup"><span data-stu-id="73c6b-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="73c6b-117">Por exemplo, a instalação de um pacote por meio do console adiciona uma referência ao projeto, enquanto o comando da CLI, não.</span><span class="sxs-lookup"><span data-stu-id="73c6b-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="73c6b-118">Por esse motivo, os desenvolvedores que trabalham no Visual Studio normalmente preferem usar o console ao invés da CLI.</span><span class="sxs-lookup"><span data-stu-id="73c6b-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="73c6b-119">Muitas operações de console dependem de ter uma solução aberta no Visual Studio com um nome de caminho conhecido.</span><span class="sxs-lookup"><span data-stu-id="73c6b-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="73c6b-120">Se uma solução não está salva, ou se não há uma solução, ocorrerá o erro "A solução não está aberta ou não foi salva.</span><span class="sxs-lookup"><span data-stu-id="73c6b-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="73c6b-121">Verifique se tem uma solução aberta e salva".</span><span class="sxs-lookup"><span data-stu-id="73c6b-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="73c6b-122">Isso indica que o console não pode determinar a pasta da solução.</span><span class="sxs-lookup"><span data-stu-id="73c6b-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="73c6b-123">Salvar uma solução que não foi salva, ou criar e salvar uma solução se uma não estiver aberta, deve corrigir o erro.</span><span class="sxs-lookup"><span data-stu-id="73c6b-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="73c6b-124">Abrir o console e os controles do console</span><span class="sxs-lookup"><span data-stu-id="73c6b-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="73c6b-125">Abra o console no Visual Studio usando o comando **Ferramentas > Gerenciador de pacotes do NuGet > Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="73c6b-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="73c6b-126">O console é uma janela do Visual Studio que pode ser organizada e posicionada como você desejar (confira [Personalizar layouts de janela no Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="73c6b-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="73c6b-127">Por padrão, os comandos do console operam em relação a um projeto e origem de pacote específicos, como definido no controle na parte superior da janela:</span><span class="sxs-lookup"><span data-stu-id="73c6b-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Controles do Console do Gerenciador de Pacotes para o projeto e a origem do pacote](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="73c6b-129">A seleção de um projeto e/ou origem de pacote diferente altera esses padrões para os comandos subsequentes.</span><span class="sxs-lookup"><span data-stu-id="73c6b-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="73c6b-130">Para substituir essas configurações sem alterar os padrões, a maioria dos comandos é compatível com as opções `-Source` e `-ProjectName`.</span><span class="sxs-lookup"><span data-stu-id="73c6b-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="73c6b-131">Para gerenciar as origens dos pacote, selecione o ícone de engrenagem.</span><span class="sxs-lookup"><span data-stu-id="73c6b-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="73c6b-132">Este é um atalho para a caixa de diálogo **Ferramentas > Opções > Gerenciador de pacotes do NuGet > Origens do Pacote**, como descrito na página [Interface do usuário do Gerenciador de Pacotes](install-use-packages-visual-studio.md#package-sources).</span><span class="sxs-lookup"><span data-stu-id="73c6b-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](install-use-packages-visual-studio.md#package-sources) page.</span></span> <span data-ttu-id="73c6b-133">Além disso, o controle à direita do seletor de projeto limpa o conteúdo do console:</span><span class="sxs-lookup"><span data-stu-id="73c6b-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Configurações do Console do Gerenciador de pacotes e controles desmarcados](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="73c6b-135">O botão mais à direita interrompe um comando de execução longa.</span><span class="sxs-lookup"><span data-stu-id="73c6b-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="73c6b-136">Por exemplo, a execução de `Get-Package -ListAvailable -PageSize 500` lista os primeiros 500 pacotes na origem padrão (como nuget.org), o que pode demorar vários minutos para executar.</span><span class="sxs-lookup"><span data-stu-id="73c6b-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Controle de interrupção do Console do Gerenciador de Pacotes](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a><span data-ttu-id="73c6b-138">Instalar um pacote</span><span class="sxs-lookup"><span data-stu-id="73c6b-138">Install a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="73c6b-139">Confira [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="73c6b-139">See [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span></span>

<span data-ttu-id="73c6b-140">A instalação de um pacote no console executa as mesmas etapas, como descrito em [O que acontece quando um pacote é instalado](../concepts/package-installation-process.md), com as seguintes adições:</span><span class="sxs-lookup"><span data-stu-id="73c6b-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="73c6b-141">O console exibe os termos de licenças aplicáveis em sua janela com o contrato implícito.</span><span class="sxs-lookup"><span data-stu-id="73c6b-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="73c6b-142">Se você não concordar com os termos, deverá desinstalar o pacote imediatamente.</span><span class="sxs-lookup"><span data-stu-id="73c6b-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="73c6b-143">Além disso, uma referência ao pacote é adicionada ao arquivo de projeto e aparece no **Gerenciador de Soluções** sob o nó **Referências**; é preciso salvar o projeto para ver as alterações diretamente no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="73c6b-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="73c6b-144">Desinstalar um pacote</span><span class="sxs-lookup"><span data-stu-id="73c6b-144">Uninstall a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="73c6b-145">Confira [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="73c6b-145">See [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="73c6b-146">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) para ver todos os pacotes atualmente instalados no projeto padrão, caso precise encontrar um identificador.</span><span class="sxs-lookup"><span data-stu-id="73c6b-146">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="73c6b-147">A desinstalação de um pacote executa as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="73c6b-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="73c6b-148">Remove as referências ao pacote do projeto (e qualquer formato de gerenciamento em uso).</span><span class="sxs-lookup"><span data-stu-id="73c6b-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="73c6b-149">As referências não aparecem mais no **Gerenciador de Soluções**.</span><span class="sxs-lookup"><span data-stu-id="73c6b-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="73c6b-150">(Talvez seja necessário recompilar o projeto para vê-lo removido da pasta **Bin**.)</span><span class="sxs-lookup"><span data-stu-id="73c6b-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="73c6b-151">Reverte todas as alterações feitas em `app.config` ou `web.config` quando o pacote foi instalado.</span><span class="sxs-lookup"><span data-stu-id="73c6b-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="73c6b-152">Remove as dependências instaladas anteriormente se nenhum pacote restante usa essas dependências.</span><span class="sxs-lookup"><span data-stu-id="73c6b-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="73c6b-153">Atualizar um pacote</span><span class="sxs-lookup"><span data-stu-id="73c6b-153">Update a package</span></span>

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

<span data-ttu-id="73c6b-154">Confira [Get-Package](../reference/ps-reference/ps-ref-get-package.md) e [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="73c6b-154">See [Get-Package](../reference/ps-reference/ps-ref-get-package.md) and [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span></span>

## <a name="find-a-package"></a><span data-ttu-id="73c6b-155">Localizar um pacote</span><span class="sxs-lookup"><span data-stu-id="73c6b-155">Find a package</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

<span data-ttu-id="73c6b-156">Confira [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="73c6b-156">See [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span></span> <span data-ttu-id="73c6b-157">No Visual Studio 2013 e anteriores, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md).</span><span class="sxs-lookup"><span data-stu-id="73c6b-157">In Visual Studio 2013 and earlier, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="73c6b-158">Disponibilidade do console</span><span class="sxs-lookup"><span data-stu-id="73c6b-158">Availability of the console</span></span>

<span data-ttu-id="73c6b-159">A partir do Visual Studio 2017, o NuGet e o Gerenciador de pacotes do NuGet são instalados automaticamente ao seleciona qualquer carga de trabalho relacionada a .NET. Também é possível instalá-los individualmente marcando a opção **Componentes individuais > Ferramentas de código > Gerenciador de pacotes do NuGet** no instalador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="73c6b-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="73c6b-160">Além disso, se você não tem o Gerenciador de pacotes do NuGet no Visual Studio 2015 e anteriores, marque **Ferramentas > Extensões e Atualizações...** e pesquise pela extensão Gerenciador de pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="73c6b-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="73c6b-161">Se você não puder usar o instalador de extensões no Visual [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)Studio, você pode baixar a extensão diretamente de .</span><span class="sxs-lookup"><span data-stu-id="73c6b-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="73c6b-162">O Console do Gerenciador de Pacotes não está disponível atualmente no Visual Studio para Mac.</span><span class="sxs-lookup"><span data-stu-id="73c6b-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="73c6b-163">No entanto, os comandos equivalentes estão disponíveis por meio da [CLI NuGet](../reference/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="73c6b-163">The equivalent commands, however, are available through the [NuGet CLI](../reference/nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="73c6b-164">O Visual Studio para Mac tem uma interface do usuário para gerenciar pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="73c6b-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="73c6b-165">Confira [Incluindo um pacote do NuGet no projeto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="73c6b-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="73c6b-166">O Console do Gerenciador de Pacotes não está incluso no Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="73c6b-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extend-the-package-manager-console"></a><span data-ttu-id="73c6b-167">Estender o Console do Gerenciador de Pacotes</span><span class="sxs-lookup"><span data-stu-id="73c6b-167">Extend the Package Manager Console</span></span>

<span data-ttu-id="73c6b-168">Alguns pacotes instalam novos comandos no console.</span><span class="sxs-lookup"><span data-stu-id="73c6b-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="73c6b-169">Por exemplo, `MvcScaffolding` cria comandos como `Scaffold`, como mostrado abaixo, que gera os controladores e exibições do ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="73c6b-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Instalar e usar MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a><span data-ttu-id="73c6b-171">Configurar um perfil do PowerShell do NuGet</span><span class="sxs-lookup"><span data-stu-id="73c6b-171">Set up a NuGet PowerShell profile</span></span>

<span data-ttu-id="73c6b-172">Um perfil do PowerShell possibilita disponibilizar os comandos usados com frequência sempre que usar o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="73c6b-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="73c6b-173">O NuGet é compatível com um perfil específico do NuGet, normalmente encontrado no seguinte local:</span><span class="sxs-lookup"><span data-stu-id="73c6b-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="73c6b-174">Para localizar o perfil, digite `$profile` no console:</span><span class="sxs-lookup"><span data-stu-id="73c6b-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="73c6b-175">Para saber mais, confira [Perfis do Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="73c6b-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="use-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="73c6b-176">Usar a CLI nuget.exe no console</span><span class="sxs-lookup"><span data-stu-id="73c6b-176">Use the nuget.exe CLI in the console</span></span>

<span data-ttu-id="73c6b-177">Para disponibilizar [ `nuget.exe` ](../reference/nuget-exe-cli-reference.md) a CLI no console do gerenciador de pacotes, instale o pacote [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) no console:</span><span class="sxs-lookup"><span data-stu-id="73c6b-177">To make the [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
