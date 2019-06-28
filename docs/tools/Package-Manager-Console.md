---
title: Instalar e gerenciar pacotes NuGet no Visual Studio usando o PowerShell
description: Instruções sobre como usar o Console do Gerenciador de pacotes NuGet no Visual Studio para trabalhar com pacotes.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 11ec25598d3110ba84dec5044642e205e13346af
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426213"
---
# <a name="install-and-manage-packages-using-powershell-in-visual-studio"></a><span data-ttu-id="7d68f-103">Instalar e gerenciar pacotes no Visual Studio usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d68f-103">Install and manage packages using PowerShell in Visual Studio</span></span>

<span data-ttu-id="7d68f-104">O NuGet Package Manager Console permite que você use [comandos do PowerShell do NuGet](../tools/powershell-reference.md) para localizar, instalar, desinstalar e atualizar pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="7d68f-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="7d68f-105">Usando o console é necessário em casos em que o Gerenciador de pacotes UI não fornece uma maneira de executar uma operação.</span><span class="sxs-lookup"><span data-stu-id="7d68f-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="7d68f-106">Para usar `nuget.exe` comandos da CLI no console do, consulte [usando a CLI nuget.exe no console do](#using-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="7d68f-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="7d68f-107">O console é criado no Visual Studio no Windows.</span><span class="sxs-lookup"><span data-stu-id="7d68f-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="7d68f-108">Não é incluído no Visual Studio para Mac ou Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7d68f-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="7d68f-109">Localizar e instalar um pacote</span><span class="sxs-lookup"><span data-stu-id="7d68f-109">Find and install a package</span></span>

<span data-ttu-id="7d68f-110">Por exemplo, localizar e instalar um pacote é feito com três etapas fáceis:</span><span class="sxs-lookup"><span data-stu-id="7d68f-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="7d68f-111">Abra o projeto/solução no Visual Studio e abra o console usando o **Ferramentas > Gerenciador de pacotes NuGet > Console do Gerenciador de pacotes** comando.</span><span class="sxs-lookup"><span data-stu-id="7d68f-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="7d68f-112">Encontre o pacote que você deseja instalar.</span><span class="sxs-lookup"><span data-stu-id="7d68f-112">Find the package you want to install.</span></span> <span data-ttu-id="7d68f-113">Se você já sabe que isso, vá para a etapa 3.</span><span class="sxs-lookup"><span data-stu-id="7d68f-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="7d68f-114">Execute o comando de instalação:</span><span class="sxs-lookup"><span data-stu-id="7d68f-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="7d68f-115">Todas as operações que estão disponíveis no console também podem ser feitas com o [CLI do NuGet](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="7d68f-115">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="7d68f-116">No entanto, os comandos do console operam dentro do contexto do Visual Studio e uma projeto/solução salva e geralmente realizar mais de seus comandos CLI equivalentes.</span><span class="sxs-lookup"><span data-stu-id="7d68f-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="7d68f-117">Por exemplo, instalação de um pacote por meio do console adiciona uma referência ao projeto enquanto o comando da CLI não.</span><span class="sxs-lookup"><span data-stu-id="7d68f-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="7d68f-118">Por esse motivo, os desenvolvedores que trabalham no Visual Studio geralmente preferem usando o console da CLI.</span><span class="sxs-lookup"><span data-stu-id="7d68f-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="7d68f-119">Muitas operações de console dependem de você ter uma solução aberta no Visual Studio com um nome de caminho conhecido.</span><span class="sxs-lookup"><span data-stu-id="7d68f-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="7d68f-120">Se você tiver uma solução não salva ou nenhuma solução, você pode ver o erro, "solução não é aberta ou não salvas.</span><span class="sxs-lookup"><span data-stu-id="7d68f-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="7d68f-121">Verifique se que você tiver uma solução aberta e salva."</span><span class="sxs-lookup"><span data-stu-id="7d68f-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="7d68f-122">Isso indica que o console não é possível determinar a pasta da solução.</span><span class="sxs-lookup"><span data-stu-id="7d68f-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="7d68f-123">Salvando uma solução não salva, ou criando e salvando uma solução se você não tiver uma aberta, deverá corrigir o erro.</span><span class="sxs-lookup"><span data-stu-id="7d68f-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="7d68f-124">Abrindo o console e os controles de console</span><span class="sxs-lookup"><span data-stu-id="7d68f-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="7d68f-125">Abra o console no Visual Studio usando o **Ferramentas > Gerenciador de pacotes NuGet > Console do Gerenciador de pacotes** comando.</span><span class="sxs-lookup"><span data-stu-id="7d68f-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="7d68f-126">O console é uma janela do Visual Studio que pode ser organizada e posicionada no entanto, como (consulte [Personalizar layouts de janela no Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="7d68f-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="7d68f-127">Por padrão, os comandos do console operam em relação a uma origem de pacote específico e um projeto conforme definido no controle na parte superior da janela:</span><span class="sxs-lookup"><span data-stu-id="7d68f-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Controles do Package Manager Console para a origem do pacote e projeto](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="7d68f-129">A seleção de uma origem de pacote diferente e/ou projeto altera esses padrões para comandos subsequentes.</span><span class="sxs-lookup"><span data-stu-id="7d68f-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="7d68f-130">Para ignorar essas configurações sem alterar os padrões, a maioria dos comandos de suporte `-Source` e `-ProjectName` opções.</span><span class="sxs-lookup"><span data-stu-id="7d68f-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="7d68f-131">Para gerenciar fontes de pacote, selecione o ícone de engrenagem.</span><span class="sxs-lookup"><span data-stu-id="7d68f-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="7d68f-132">Esse é um atalho para o **Ferramentas > Opções > Gerenciador de pacotes NuGet > origens de pacote** caixa de diálogo, conforme descrito no [Gerenciador de pacotes UI](package-manager-ui.md#package-sources) página.</span><span class="sxs-lookup"><span data-stu-id="7d68f-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="7d68f-133">Além disso, o controle à direita do seletor de projeto limpa o conteúdo do console:</span><span class="sxs-lookup"><span data-stu-id="7d68f-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![As configurações do Console do Gerenciador de pacotes e limpar controles](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="7d68f-135">O botão mais à direita interrupções de um comando de execução longa.</span><span class="sxs-lookup"><span data-stu-id="7d68f-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="7d68f-136">Por exemplo, executando `Get-Package -ListAvailable -PageSize 500` lista os pacotes superior a 500 na fonte de padrão (como nuget.org), que pode levar vários minutos para ser executado.</span><span class="sxs-lookup"><span data-stu-id="7d68f-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Controle de parada do Package Manager Console](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="7d68f-138">Instalação de um pacote</span><span class="sxs-lookup"><span data-stu-id="7d68f-138">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="7d68f-139">Ver [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="7d68f-139">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="7d68f-140">Instalação de um pacote no console executa as mesmas etapas conforme descrito em [o que acontece quando um pacote é instalado](../concepts/package-installation-process.md), com as seguintes adições:</span><span class="sxs-lookup"><span data-stu-id="7d68f-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="7d68f-141">O Console exibe os termos de licença aplicáveis em sua janela com o contrato implícito.</span><span class="sxs-lookup"><span data-stu-id="7d68f-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="7d68f-142">Se você não concordar com os termos, você deve desinstalar o pacote imediatamente.</span><span class="sxs-lookup"><span data-stu-id="7d68f-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="7d68f-143">Também uma referência para o pacote é adicionada ao arquivo de projeto e aparece na **Gerenciador de soluções** sob o **referências** nó, você precisa salvar o projeto para ver as alterações no arquivo de projeto diretamente.</span><span class="sxs-lookup"><span data-stu-id="7d68f-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="7d68f-144">Desinstalar um pacote</span><span class="sxs-lookup"><span data-stu-id="7d68f-144">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="7d68f-145">Ver [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="7d68f-145">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="7d68f-146">Use [Get-Package](../tools/ps-ref-get-package.md) para ver todos os pacotes instalados no momento no projeto padrão, se você precisar localizar um identificador.</span><span class="sxs-lookup"><span data-stu-id="7d68f-146">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="7d68f-147">Desinstalar um pacote executa as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="7d68f-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="7d68f-148">Remove as referências ao pacote do projeto (e qualquer formato de gerenciamento está em uso).</span><span class="sxs-lookup"><span data-stu-id="7d68f-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="7d68f-149">Referências não aparecem mais na **Gerenciador de soluções**.</span><span class="sxs-lookup"><span data-stu-id="7d68f-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="7d68f-150">(Talvez seja necessário recompilar o projeto para vê-lo removido do **Bin** pasta.)</span><span class="sxs-lookup"><span data-stu-id="7d68f-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="7d68f-151">Reverte todas as alterações feitas `app.config` ou `web.config` quando o pacote foi instalado.</span><span class="sxs-lookup"><span data-stu-id="7d68f-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="7d68f-152">Remove instalado anteriormente dependências se não há pacotes restantes usam essas dependências.</span><span class="sxs-lookup"><span data-stu-id="7d68f-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="7d68f-153">Atualizar um pacote</span><span class="sxs-lookup"><span data-stu-id="7d68f-153">Updating a package</span></span>

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

<span data-ttu-id="7d68f-154">Ver [Get-Package](../tools/ps-ref-get-package.md) e [Update-Package](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="7d68f-154">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="7d68f-155">Localizar um pacote</span><span class="sxs-lookup"><span data-stu-id="7d68f-155">Finding a package</span></span>

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

<span data-ttu-id="7d68f-156">Ver [Find-Package](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="7d68f-156">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="7d68f-157">No Visual Studio 2013 e anteriores, use [Get-Package](../tools/ps-ref-get-package.md) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="7d68f-157">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="7d68f-158">Disponibilidade do console</span><span class="sxs-lookup"><span data-stu-id="7d68f-158">Availability of the console</span></span>

<span data-ttu-id="7d68f-159">A partir do Visual Studio 2017, NuGet e o Gerenciador de pacotes do NuGet são instalados automaticamente quando você seleciona qualquer um. Cargas de trabalho relacionados à rede; Você também pode instalar individualmente, marcando a **componentes individuais > Ferramentas de código > Gerenciador de pacotes NuGet** opção no instalador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7d68f-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="7d68f-160">Além disso, se estiver faltando o Gerenciador de pacotes do NuGet no Visual Studio 2015 e anteriores, verifique **Ferramentas > extensões e atualizações...**  e pesquise a extensão do Gerenciador de pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="7d68f-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="7d68f-161">Se você não puder usar o instalador de extensões no Visual Studio, você pode baixar a extensão diretamente [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="7d68f-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="7d68f-162">O Console do Gerenciador de pacote não está disponível atualmente com o Visual Studio para Mac.</span><span class="sxs-lookup"><span data-stu-id="7d68f-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="7d68f-163">No entanto, os comandos equivalentes, estão disponíveis por meio de [CLI do NuGet](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="7d68f-163">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="7d68f-164">O Visual Studio para Mac tem uma interface do usuário para o gerenciamento de pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="7d68f-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="7d68f-165">Ver [incluindo um pacote do NuGet em seu projeto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="7d68f-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="7d68f-166">O Console do Gerenciador de pacote não está incluído com o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7d68f-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="7d68f-167">Estendendo o Package Manager Console</span><span class="sxs-lookup"><span data-stu-id="7d68f-167">Extending the Package Manager Console</span></span>

<span data-ttu-id="7d68f-168">Alguns pacotes instalados novos comandos para o console.</span><span class="sxs-lookup"><span data-stu-id="7d68f-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="7d68f-169">Por exemplo, `MvcScaffolding` cria comandos como `Scaffold` mostrado abaixo, que gera a controladores e exibições MVC do ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="7d68f-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Instalar e usar MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="7d68f-171">Como configurar um perfil do NuGet PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d68f-171">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="7d68f-172">Um perfil do PowerShell permite disponibilizar comandos usados sempre que você usar o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7d68f-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="7d68f-173">O NuGet dá suporte a um perfil específico do NuGet normalmente encontrado no seguinte local:</span><span class="sxs-lookup"><span data-stu-id="7d68f-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="7d68f-174">Para localizar o perfil, digite `$profile` no console:</span><span class="sxs-lookup"><span data-stu-id="7d68f-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="7d68f-175">Para obter mais detalhes, consulte [perfis do Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d68f-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="7d68f-176">Usando a CLI nuget.exe no console do</span><span class="sxs-lookup"><span data-stu-id="7d68f-176">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="7d68f-177">Para tornar o [ `nuget.exe` CLI](nuget-exe-cli-reference.md) disponível no Console do Gerenciador de pacotes, instalar o [CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) pacote no console:</span><span class="sxs-lookup"><span data-stu-id="7d68f-177">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
