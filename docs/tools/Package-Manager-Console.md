---
title: Guia do Console de Gerenciador de pacotes NuGet
description: Instruções sobre como usar o Console do Gerenciador de pacotes NuGet no Visual Studio para trabalhar com pacotes.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 88979c67ea7f073f2ea5a02c445186642f77f210
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546872"
---
# <a name="package-manager-console"></a><span data-ttu-id="97502-103">Console do Gerenciador de Pacotes</span><span class="sxs-lookup"><span data-stu-id="97502-103">Package Manager Console</span></span>

<span data-ttu-id="97502-104">O NuGet Package Manager Console é criado no Visual Studio no Windows versão 2012 e posterior.</span><span class="sxs-lookup"><span data-stu-id="97502-104">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="97502-105">(Não é incluído no Visual Studio para Mac ou Visual Studio Code.)</span><span class="sxs-lookup"><span data-stu-id="97502-105">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="97502-106">O console permite que você use [comandos do PowerShell do NuGet](../tools/powershell-reference.md) para localizar, instalar, desinstalar e atualizar pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="97502-106">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="97502-107">Usando o console é necessário em casos em que o Gerenciador de pacotes UI não fornece uma maneira de executar uma operação.</span><span class="sxs-lookup"><span data-stu-id="97502-107">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="97502-108">Para usar `nuget.exe` comandos no console do, consulte [usando a CLI nuget.exe no console do](#using-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="97502-108">To use `nuget.exe` commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="97502-109">Por exemplo, localizar e instalar um pacote é feito com três etapas fáceis:</span><span class="sxs-lookup"><span data-stu-id="97502-109">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="97502-110">Abra o projeto/solução no Visual Studio e abra o console usando o **Ferramentas > Gerenciador de pacotes NuGet > Console do Gerenciador de pacotes** comando.</span><span class="sxs-lookup"><span data-stu-id="97502-110">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="97502-111">Encontre o pacote que você deseja instalar.</span><span class="sxs-lookup"><span data-stu-id="97502-111">Find the package you want to install.</span></span> <span data-ttu-id="97502-112">Se você já sabe que isso, vá para a etapa 3.</span><span class="sxs-lookup"><span data-stu-id="97502-112">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="97502-113">Execute o comando de instalação:</span><span class="sxs-lookup"><span data-stu-id="97502-113">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="97502-114">Todas as operações que estão disponíveis no console também podem ser feitas com o [CLI do NuGet](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="97502-114">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="97502-115">No entanto, os comandos do console operam dentro do contexto do Visual Studio e uma projeto/solução salva e geralmente realizar mais de seus comandos CLI equivalentes.</span><span class="sxs-lookup"><span data-stu-id="97502-115">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="97502-116">Por exemplo, instalação de um pacote por meio do console adiciona uma referência ao projeto enquanto o comando da CLI não.</span><span class="sxs-lookup"><span data-stu-id="97502-116">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="97502-117">Por esse motivo, os desenvolvedores que trabalham no Visual Studio geralmente preferem usando o console da CLI.</span><span class="sxs-lookup"><span data-stu-id="97502-117">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="97502-118">Muitas operações de console dependem de você ter uma solução aberta no Visual Studio com um nome de caminho conhecido.</span><span class="sxs-lookup"><span data-stu-id="97502-118">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="97502-119">Se você tiver uma solução não salva ou nenhuma solução, você pode ver o erro, "solução não é aberta ou não salvas.</span><span class="sxs-lookup"><span data-stu-id="97502-119">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="97502-120">Verifique se que você tiver uma solução aberta e salva."</span><span class="sxs-lookup"><span data-stu-id="97502-120">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="97502-121">Isso indica que o console não é possível determinar a pasta da solução.</span><span class="sxs-lookup"><span data-stu-id="97502-121">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="97502-122">Salvando uma solução não salva, ou criando e salvando uma solução se você não tiver uma aberta, deverá corrigir o erro.</span><span class="sxs-lookup"><span data-stu-id="97502-122">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="97502-123">Abrindo o console e os controles de console</span><span class="sxs-lookup"><span data-stu-id="97502-123">Opening the console and console controls</span></span>

1. <span data-ttu-id="97502-124">Abra o console no Visual Studio usando o **Ferramentas > Gerenciador de pacotes NuGet > Console do Gerenciador de pacotes** comando.</span><span class="sxs-lookup"><span data-stu-id="97502-124">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="97502-125">O console é uma janela do Visual Studio que pode ser organizada e posicionada no entanto, como (consulte [Personalizar layouts de janela no Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="97502-125">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="97502-126">Por padrão, os comandos do console operam em relação a uma origem de pacote específico e um projeto conforme definido no controle na parte superior da janela:</span><span class="sxs-lookup"><span data-stu-id="97502-126">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Controles do Package Manager Console para a origem do pacote e projeto](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="97502-128">A seleção de uma origem de pacote diferente e/ou projeto altera esses padrões para comandos subsequentes.</span><span class="sxs-lookup"><span data-stu-id="97502-128">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="97502-129">Para ignorar essas configurações sem alterar os padrões, a maioria dos comandos de suporte `-Source` e `-ProjectName` opções.</span><span class="sxs-lookup"><span data-stu-id="97502-129">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="97502-130">Para gerenciar fontes de pacote, selecione o ícone de engrenagem.</span><span class="sxs-lookup"><span data-stu-id="97502-130">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="97502-131">Esse é um atalho para o **Ferramentas > Opções > Gerenciador de pacotes NuGet > origens de pacote** caixa de diálogo, conforme descrito no [Gerenciador de pacotes UI](package-manager-ui.md#package-sources) página.</span><span class="sxs-lookup"><span data-stu-id="97502-131">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="97502-132">Além disso, o controle à direita do seletor de projeto limpa o conteúdo do console:</span><span class="sxs-lookup"><span data-stu-id="97502-132">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![As configurações do Console do Gerenciador de pacotes e limpar controles](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="97502-134">O botão mais à direita interrupções de um comando de execução longa.</span><span class="sxs-lookup"><span data-stu-id="97502-134">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="97502-135">Por exemplo, executando `Get-Package -ListAvailable -PageSize 500` lista os pacotes superior a 500 na fonte de padrão (como nuget.org), que pode levar vários minutos para ser executado.</span><span class="sxs-lookup"><span data-stu-id="97502-135">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Controle de parada do Package Manager Console](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="97502-137">Instalação de um pacote</span><span class="sxs-lookup"><span data-stu-id="97502-137">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="97502-138">Ver [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="97502-138">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="97502-139">Instalação de um pacote no console executa as mesmas etapas conforme descrito em [o que acontece quando um pacote é instalado](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), com as seguintes adições:</span><span class="sxs-lookup"><span data-stu-id="97502-139">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), with the following additions:</span></span>

- <span data-ttu-id="97502-140">O Console exibe os termos de licença aplicáveis em sua janela com o contrato implícito.</span><span class="sxs-lookup"><span data-stu-id="97502-140">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="97502-141">Se você não concordar com os termos, você deve desinstalar o pacote imediatamente.</span><span class="sxs-lookup"><span data-stu-id="97502-141">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="97502-142">Também uma referência para o pacote é adicionada ao arquivo de projeto e aparece na **Gerenciador de soluções** sob o **referências** nó, você precisa salvar o projeto para ver as alterações no arquivo de projeto diretamente.</span><span class="sxs-lookup"><span data-stu-id="97502-142">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="97502-143">Desinstalar um pacote</span><span class="sxs-lookup"><span data-stu-id="97502-143">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="97502-144">Ver [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="97502-144">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="97502-145">Use [Get-Package](../tools/ps-ref-get-package.md) para ver todos os pacotes instalados no momento no projeto padrão, se você precisar localizar um identificador.</span><span class="sxs-lookup"><span data-stu-id="97502-145">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="97502-146">Desinstalar um pacote executa as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="97502-146">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="97502-147">Remove as referências ao pacote do projeto (e qualquer formato de gerenciamento está em uso).</span><span class="sxs-lookup"><span data-stu-id="97502-147">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="97502-148">Referências não aparecem mais na **Gerenciador de soluções**.</span><span class="sxs-lookup"><span data-stu-id="97502-148">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="97502-149">(Talvez seja necessário recompilar o projeto para vê-lo removido do **Bin** pasta.)</span><span class="sxs-lookup"><span data-stu-id="97502-149">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="97502-150">Reverte todas as alterações feitas `app.config` ou `web.config` quando o pacote foi instalado.</span><span class="sxs-lookup"><span data-stu-id="97502-150">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="97502-151">Remove instalado anteriormente dependências se não há pacotes restantes usam essas dependências.</span><span class="sxs-lookup"><span data-stu-id="97502-151">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="97502-152">Atualizar um pacote</span><span class="sxs-lookup"><span data-stu-id="97502-152">Updating a package</span></span>

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

<span data-ttu-id="97502-153">Ver [Get-Package](../tools/ps-ref-get-package.md) e [Update-Package](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="97502-153">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="97502-154">Localizar um pacote</span><span class="sxs-lookup"><span data-stu-id="97502-154">Finding a package</span></span>

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

<span data-ttu-id="97502-155">Ver [Find-Package](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="97502-155">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="97502-156">No Visual Studio 2013 e anteriores, use [Get-Package](../tools/ps-ref-get-package.md) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="97502-156">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="97502-157">Disponibilidade do console</span><span class="sxs-lookup"><span data-stu-id="97502-157">Availability of the console</span></span>

<span data-ttu-id="97502-158">No Visual Studio 2017, NuGet e o Gerenciador de pacotes do NuGet são instalados automaticamente quando você seleciona qualquer um. Cargas de trabalho relacionados à rede; Você também pode instalar individualmente, marcando a **componentes individuais > Ferramentas de código > Gerenciador de pacotes NuGet** opção no instalador do Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="97502-158">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="97502-159">Além disso, se estiver faltando o Gerenciador de pacotes do NuGet no Visual Studio 2015 e anteriores, verifique **Ferramentas > extensões e atualizações...**  e pesquise a extensão do Gerenciador de pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="97502-159">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="97502-160">Se você não puder usar o instalador de extensões no Visual Studio, você pode baixar a extensão diretamente [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="97502-160">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="97502-161">O Console do Gerenciador de pacote não está disponível atualmente com o Visual Studio para Mac.</span><span class="sxs-lookup"><span data-stu-id="97502-161">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="97502-162">No entanto, os comandos equivalentes, estão disponíveis por meio de [CLI do NuGet](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="97502-162">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="97502-163">O Visual Studio para Mac tem uma interface do usuário para o gerenciamento de pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="97502-163">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="97502-164">Ver [incluindo um pacote do NuGet em seu projeto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="97502-164">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="97502-165">O Console do Gerenciador de pacote não está incluído com o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="97502-165">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="97502-166">Estendendo o Package Manager Console</span><span class="sxs-lookup"><span data-stu-id="97502-166">Extending the Package Manager Console</span></span>

<span data-ttu-id="97502-167">Alguns pacotes instalados novos comandos para o console.</span><span class="sxs-lookup"><span data-stu-id="97502-167">Some packages install new commands for the console.</span></span> <span data-ttu-id="97502-168">Por exemplo, `MvcScaffolding` cria comandos como `Scaffold` mostrado abaixo, que gera a controladores e exibições MVC do ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="97502-168">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Instalar e usar MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="97502-170">Como configurar um perfil do NuGet PowerShell</span><span class="sxs-lookup"><span data-stu-id="97502-170">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="97502-171">Um perfil do PowerShell permite disponibilizar comandos usados sempre que você usar o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97502-171">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="97502-172">O NuGet dá suporte a um perfil específico do NuGet normalmente encontrado no seguinte local:</span><span class="sxs-lookup"><span data-stu-id="97502-172">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="97502-173">Para localizar o perfil, digite `$profile` no console:</span><span class="sxs-lookup"><span data-stu-id="97502-173">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="97502-174">Para obter mais detalhes, consulte [perfis do Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="97502-174">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="97502-175">Usando a CLI nuget.exe no console do</span><span class="sxs-lookup"><span data-stu-id="97502-175">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="97502-176">Para tornar o [ `nuget.exe` CLI](nuget-exe-cli-reference.md) disponível no Console do Gerenciador de pacotes, instalar o [CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) pacote no console:</span><span class="sxs-lookup"><span data-stu-id="97502-176">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
