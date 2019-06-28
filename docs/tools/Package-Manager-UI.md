---
title: Instalar e gerenciar pacotes NuGet no Visual Studio
description: Instruções sobre como usar a UI do Gerenciador de pacotes NuGet no Visual Studio para trabalhar com pacotes do NuGet.
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 97e5de3f07199cd3c6a645749c8f2f1603ca630e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426244"
---
# <a name="install-and-manage-packages-in-visual-studio"></a><span data-ttu-id="2107e-103">Instalar e gerenciar pacotes no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2107e-103">Install and manage packages in Visual Studio</span></span>

<span data-ttu-id="2107e-104">UI do Gerenciador de pacotes NuGet no Visual Studio no Windows permite que você instalar, desinstalar e atualizar pacotes do NuGet em projetos e soluções com facilidade.</span><span class="sxs-lookup"><span data-stu-id="2107e-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="2107e-105">Para obter a experiência no Visual Studio para Mac, consulte [incluindo um pacote do NuGet em seu projeto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="2107e-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="2107e-106">A UI do Gerenciador de pacotes não está incluída no Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2107e-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="2107e-107">Verifique se você está ignorando o Gerenciador de pacotes do NuGet no Visual Studio 2015, **Ferramentas > extensões e atualizações...**  e procure o *NuGet Package Manager* extensão.</span><span class="sxs-lookup"><span data-stu-id="2107e-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="2107e-108">Se você não puder usar o instalador de extensões no Visual Studio, baixe a extensão diretamente [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="2107e-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="2107e-109">A partir do Visual Studio 2017, NuGet e o Gerenciador de pacotes do NuGet são instalados automaticamente com qualquer um. Cargas de trabalho relacionados à rede.</span><span class="sxs-lookup"><span data-stu-id="2107e-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="2107e-110">Instalá-lo individualmente selecionando o **componentes individuais > Ferramentas de código > Gerenciador de pacotes NuGet** opção no instalador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2107e-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="2107e-111">Localizando e instalando um pacote</span><span class="sxs-lookup"><span data-stu-id="2107e-111">Finding and installing a package</span></span>

1. <span data-ttu-id="2107e-112">No **Gerenciador de soluções**, clique com botão direito seja **referências** ou um projeto e selecione **gerenciar pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="2107e-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Gerenciar a opção de menu de pacotes do NuGet](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="2107e-114">O **navegue** guia exibe os pacotes por popularidade da fonte selecionada no momento (consulte [origens de pacotes](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="2107e-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="2107e-115">Pesquisar um pacote específico usando a caixa de pesquisa no canto superior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="2107e-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="2107e-116">Selecione um pacote na lista para exibir suas informações, que também permite que o **instalar** botão juntamente com uma lista suspensa de seleção de versão.</span><span class="sxs-lookup"><span data-stu-id="2107e-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Gerenciar guia Procurar de caixa de diálogo de pacotes do NuGet](media/Search.png)

1. <span data-ttu-id="2107e-118">Selecione a versão desejada na lista suspensa e selecione **instalar**.</span><span class="sxs-lookup"><span data-stu-id="2107e-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="2107e-119">Visual Studio instala o pacote e suas dependências no projeto.</span><span class="sxs-lookup"><span data-stu-id="2107e-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="2107e-120">Você pode ser solicitado a aceitar os termos de licença.</span><span class="sxs-lookup"><span data-stu-id="2107e-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="2107e-121">Quando a instalação for concluída, os pacotes adicionados aparecem na **instalado** guia. Pacotes também são listados na **referências** nó do Gerenciador de soluções, indicando que você possa consultá-los no projeto com `using` instruções.</span><span class="sxs-lookup"><span data-stu-id="2107e-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Referências no Gerenciador de soluções](media/References.png)

> [!Tip]
> <span data-ttu-id="2107e-123">Para incluir versões de pré-lançamento na pesquisa e fazer versões de pré-lançamento disponível na versão de lista suspensa, selecione o **incluir pré-lançamento** opção.</span><span class="sxs-lookup"><span data-stu-id="2107e-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="2107e-124">Desinstalar um pacote</span><span class="sxs-lookup"><span data-stu-id="2107e-124">Uninstalling a package</span></span>

1. <span data-ttu-id="2107e-125">No **Gerenciador de soluções**, clique com botão direito seja **referências** ou o projeto desejado e selecione **gerenciar pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="2107e-125">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="2107e-126">Selecione o **instalado** guia.</span><span class="sxs-lookup"><span data-stu-id="2107e-126">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="2107e-127">Selecione o pacote para desinstalar (usando a pesquisa para filtrar a lista se necessário) e selecione **desinstalação**.</span><span class="sxs-lookup"><span data-stu-id="2107e-127">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Desinstalar um pacote](media/UninstallPackage.png)

1. <span data-ttu-id="2107e-129">Observe que o **incluir pré-lançamento** e **origem do pacote** controles não têm nenhum efeito ao desinstalar pacotes.</span><span class="sxs-lookup"><span data-stu-id="2107e-129">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="2107e-130">Atualizar um pacote</span><span class="sxs-lookup"><span data-stu-id="2107e-130">Updating a package</span></span>

1. <span data-ttu-id="2107e-131">No **Gerenciador de soluções**, clique com botão direito seja **referências** ou o projeto desejado e selecione **gerenciar pacotes NuGet...** . (Em projetos de site da web, clique com botão direito do **Bin** pasta.)</span><span class="sxs-lookup"><span data-stu-id="2107e-131">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="2107e-132">Selecione o **atualizações** guia para ver os pacotes com atualizações disponíveis das fontes de pacote selecionado.</span><span class="sxs-lookup"><span data-stu-id="2107e-132">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="2107e-133">Selecione **incluir pré-lançamento** inclui pacotes pré-lançados na lista de atualização.</span><span class="sxs-lookup"><span data-stu-id="2107e-133">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="2107e-134">Selecione o pacote para atualizar, selecione a versão desejada na lista suspensa à direita e selecione **atualizar**.</span><span class="sxs-lookup"><span data-stu-id="2107e-134">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Atualizar um pacote](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="2107e-136">Para alguns pacotes, o **atualização** botão será desabilitado e será exibida uma mensagem dizendo que ele é "implicitamente referenciado por um SDK" (ou "AutoReferenced").</span><span class="sxs-lookup"><span data-stu-id="2107e-136">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="2107e-137">Esta mensagem indica que o pacote faz parte de uma estrutura ou o SDK maior e não deve ser atualizado de forma independente.</span><span class="sxs-lookup"><span data-stu-id="2107e-137">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="2107e-138">(Internamente, esses pacotes são marcados com `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Por exemplo, `Microsoft.NETCore.App` faz parte do SDK do .NET Core e a versão do pacote não é igual à versão do framework de tempo de execução usado pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2107e-138">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="2107e-139">Você precisará [atualizar sua instalação do .NET Core](https://aka.ms/dotnet-download) para obter novas versões do tempo de execução do ASP.NET Core e .NET Core.</span><span class="sxs-lookup"><span data-stu-id="2107e-139">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="2107e-140">[Consulte este documento para obter mais detalhes sobre metapacotes .NET Core e o controle de versão](/dotnet/core/packages).</span><span class="sxs-lookup"><span data-stu-id="2107e-140">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="2107e-141">Isso se aplica aos seguintes pacotes comumente usados:</span><span class="sxs-lookup"><span data-stu-id="2107e-141">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="2107e-142">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="2107e-142">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="2107e-143">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="2107e-143">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="2107e-144">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="2107e-144">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="2107e-145">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="2107e-145">NETStandard.Library</span></span>

    ![Pacote de exemplo são marcados como implicitamente referências ou AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="2107e-147">Para atualizar vários pacotes para suas versões mais recentes, selecione-os na lista e selecione o **atualizar** botão acima da lista.</span><span class="sxs-lookup"><span data-stu-id="2107e-147">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="2107e-148">Você também pode atualizar um pacote individual do **instalado** guia. Nesse caso, os detalhes do pacote incluem um seletor de versão (sujeito a **incluir pré-lançamento** opção) e um **atualização** botão.</span><span class="sxs-lookup"><span data-stu-id="2107e-148">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="2107e-149">Gerenciamento de pacotes para a solução</span><span class="sxs-lookup"><span data-stu-id="2107e-149">Managing packages for the solution</span></span>

<span data-ttu-id="2107e-150">Gerenciamento de pacotes para uma solução é uma maneira conveniente para trabalhar com vários projetos simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="2107e-150">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="2107e-151">Selecione o **Ferramentas > Gerenciador de pacotes NuGet > Gerenciar pacotes NuGet para solução...**  menu de comando, ou a solução com o botão direito e selecione **gerenciar pacotes NuGet...** :</span><span class="sxs-lookup"><span data-stu-id="2107e-151">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Gerenciar pacotes NuGet para a solução](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="2107e-153">Ao gerenciar pacotes para a solução, a interface do usuário permite que você selecione os projetos que são afetados pelas operações:</span><span class="sxs-lookup"><span data-stu-id="2107e-153">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Seletor de projeto durante o gerenciamento de pacotes para a solução](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="2107e-155">Guia de consolidação</span><span class="sxs-lookup"><span data-stu-id="2107e-155">Consolidate tab</span></span>

<span data-ttu-id="2107e-156">Os desenvolvedores normalmente consideram a ele prática inadequada para usar versões diferentes do mesmo pacote do NuGet em projetos diferentes na mesma solução.</span><span class="sxs-lookup"><span data-stu-id="2107e-156">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="2107e-157">Quando você escolhe gerenciar os pacotes para uma solução, a UI do Gerenciador de pacotes fornece um **consolidar** guia na qual você pode ver facilmente onde os pacotes com números de versão diferentes são usados por diferentes projetos na solução:</span><span class="sxs-lookup"><span data-stu-id="2107e-157">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Guia de consolidar de interface do usuário do Gerenciador de pacotes](media/ConsolidateTab.png)

<span data-ttu-id="2107e-159">Neste exemplo, o projeto ClassLibrary1 está usando o EntityFramework 6.2.0, enquanto ConsoleApp1 é usando o EntityFramework 6.1.0.</span><span class="sxs-lookup"><span data-stu-id="2107e-159">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="2107e-160">Para consolidar as versões do pacote, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2107e-160">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="2107e-161">Selecione os projetos para atualizar na lista de projetos.</span><span class="sxs-lookup"><span data-stu-id="2107e-161">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="2107e-162">Selecione a versão a ser usada em todos os projetos na **versão** controle, como o EntityFramework 6.2.0.</span><span class="sxs-lookup"><span data-stu-id="2107e-162">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="2107e-163">Selecione o **instalar** botão.</span><span class="sxs-lookup"><span data-stu-id="2107e-163">Select the **Install** button.</span></span>

<span data-ttu-id="2107e-164">O Gerenciador de pacotes instala a versão do pacote selecionado em todos os projetos selecionados, após o qual o pacote não aparece mais na **consolidar** guia.</span><span class="sxs-lookup"><span data-stu-id="2107e-164">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="2107e-165">Origens de pacote</span><span class="sxs-lookup"><span data-stu-id="2107e-165">Package sources</span></span>

<span data-ttu-id="2107e-166">Para alterar a origem do qual o Visual Studio obtém pacotes, selecione uma opção do seletor de origem:</span><span class="sxs-lookup"><span data-stu-id="2107e-166">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Seletor de origem do pacote no Gerenciador de pacotes da interface do usuário](media/PackageSourceDropDown.png)

<span data-ttu-id="2107e-168">Para gerenciar fontes de pacote:</span><span class="sxs-lookup"><span data-stu-id="2107e-168">To manage package sources:</span></span>

1. <span data-ttu-id="2107e-169">Selecione o **as configurações** ícone da UI do Gerenciador de pacotes descritas abaixo ou usar o **Ferramentas > Opções** de comando e role até **Gerenciador de pacotes NuGet**:</span><span class="sxs-lookup"><span data-stu-id="2107e-169">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Ícone de configurações de interface do usuário de Gerenciador de pacote](media/PackageSourceSettings.png)

1. <span data-ttu-id="2107e-171">Selecione o **origens do pacote** nó:</span><span class="sxs-lookup"><span data-stu-id="2107e-171">Select the **Package Sources** node:</span></span>

    ![Opções de fontes de pacote](media/options.png)

1. <span data-ttu-id="2107e-173">Para adicionar uma fonte, selecione **+** , edite o nome, insira a URL ou caminho na **fonte** controle e selecione **atualização**.</span><span class="sxs-lookup"><span data-stu-id="2107e-173">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="2107e-174">O código-fonte agora aparece no menu suspenso do seletor.</span><span class="sxs-lookup"><span data-stu-id="2107e-174">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="2107e-175">Para alterar uma origem de pacote, selecione-o, fazer edições na **nome** e **fonte** caixas e selecione **atualização**.</span><span class="sxs-lookup"><span data-stu-id="2107e-175">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="2107e-176">Para desabilitar uma origem de pacote, desmarque a caixa à esquerda do nome na lista.</span><span class="sxs-lookup"><span data-stu-id="2107e-176">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="2107e-177">Para remover uma origem de pacote, selecione-o e, em seguida, selecione a **X** botão.</span><span class="sxs-lookup"><span data-stu-id="2107e-177">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="2107e-178">Usando cima e seta para baixo botões não alteram a ordem de prioridade das fontes de pacote.</span><span class="sxs-lookup"><span data-stu-id="2107e-178">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="2107e-179">Visual Studio ignora a ordem das origens de pacotes, usando o pacote de qualquer origem primeiro para responder às solicitações.</span><span class="sxs-lookup"><span data-stu-id="2107e-179">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="2107e-180">Para obter mais informações, consulte [restauração do pacote](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="2107e-180">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="2107e-181">Se uma origem de pacote for exibida novamente após a exclusão, ele pode estar listado em um nível de computador ou usuário `NuGet.Config` arquivos.</span><span class="sxs-lookup"><span data-stu-id="2107e-181">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="2107e-182">Ver [configurações de NuGet comuns](../consume-packages/configuring-nuget-behavior.md) para o local desses arquivos, em seguida, remover a fonte editando os arquivos manualmente ou usando o [nuget fontes de comando](../tools/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="2107e-182">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="2107e-183">Controle de opções do Gerenciador de pacote</span><span class="sxs-lookup"><span data-stu-id="2107e-183">Package manager Options control</span></span>

<span data-ttu-id="2107e-184">Quando um pacote é selecionado, a UI do Gerenciador de pacotes exibe um pequeno expansível **opções** controle abaixo o seletor de versão (mostrado aqui ambos recolhido ou expandido).</span><span class="sxs-lookup"><span data-stu-id="2107e-184">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="2107e-185">Observe que, para alguns projetos, tipos, somente o **Mostrar janela de visualização** opção é fornecida.</span><span class="sxs-lookup"><span data-stu-id="2107e-185">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Opções do Gerenciador de pacote](media/PackageManagerUIOptions.png)

<span data-ttu-id="2107e-187">As seções a seguir explicam essas opções.</span><span class="sxs-lookup"><span data-stu-id="2107e-187">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="2107e-188">Mostrar janela de visualização</span><span class="sxs-lookup"><span data-stu-id="2107e-188">Show preview window</span></span>

<span data-ttu-id="2107e-189">Quando selecionada, uma janela modal exibe quais as dependências de um pacote escolhido antes de instalar o pacote:</span><span class="sxs-lookup"><span data-stu-id="2107e-189">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Caixa de diálogo de visualização de exemplo](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="2107e-191">Opções de atualização e instalação</span><span class="sxs-lookup"><span data-stu-id="2107e-191">Install and Update Options</span></span>

<span data-ttu-id="2107e-192">(Não disponível para todos os tipos de projeto.)</span><span class="sxs-lookup"><span data-stu-id="2107e-192">(Not available for all project types.)</span></span>

<span data-ttu-id="2107e-193">**Comportamento de dependência** configura como o NuGet decide quais versões dos pacotes dependentes para instalar:</span><span class="sxs-lookup"><span data-stu-id="2107e-193">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="2107e-194">*Ignorar dependências* ignora a instalação de todas as dependências, que geralmente interrompe o pacote que está sendo instalado.</span><span class="sxs-lookup"><span data-stu-id="2107e-194">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="2107e-195">*Mais baixo* [padrão] a dependência é instalado com o número de versão mínima que atende aos requisitos do pacote principal escolhido.</span><span class="sxs-lookup"><span data-stu-id="2107e-195">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="2107e-196">*Patch do mais alto* instala a versão com os mesmos números de versão principal e secundária, mas o número mais alto de patch.</span><span class="sxs-lookup"><span data-stu-id="2107e-196">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="2107e-197">Por exemplo, se a versão 1.2.2 for especificada, em seguida, a versão mais recente que começa com 1.2 será instalada</span><span class="sxs-lookup"><span data-stu-id="2107e-197">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="2107e-198">*Mais alto Minor* instala a versão com o mesmo número de versão principal, mas o menor número mais alto e o número de patch.</span><span class="sxs-lookup"><span data-stu-id="2107e-198">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="2107e-199">Se a versão 1.2.2 for especificada, a versão mais recente que começa com 1 será instalada</span><span class="sxs-lookup"><span data-stu-id="2107e-199">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="2107e-200">*Mais alto* instala a versão disponível mais recente do pacote.</span><span class="sxs-lookup"><span data-stu-id="2107e-200">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="2107e-201">**Ação de conflitos de arquivo** Especifica como o NuGet deve manipular pacotes que já existem no projeto ou no computador local:</span><span class="sxs-lookup"><span data-stu-id="2107e-201">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="2107e-202">*Prompt* instrui o NuGet para perguntar se deseja manter ou substituir os pacotes existentes.</span><span class="sxs-lookup"><span data-stu-id="2107e-202">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="2107e-203">*Ignorar tudo* instrui o NuGet ignore a substituição de todos os pacotes existentes.</span><span class="sxs-lookup"><span data-stu-id="2107e-203">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="2107e-204">*Substituir tudo* instrui o NuGet para substituir todos os pacotes existentes.</span><span class="sxs-lookup"><span data-stu-id="2107e-204">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="2107e-205">Opções de desinstalação</span><span class="sxs-lookup"><span data-stu-id="2107e-205">Uninstall Options</span></span>

<span data-ttu-id="2107e-206">(Não disponível para todos os tipos de projeto.)</span><span class="sxs-lookup"><span data-stu-id="2107e-206">(Not available for all project types.)</span></span>

<span data-ttu-id="2107e-207">**Remover dependências**: quando selecionado, remove todos os pacotes dependentes se elas não são referenciadas em outro lugar no projeto.</span><span class="sxs-lookup"><span data-stu-id="2107e-207">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="2107e-208">**Desinstalação forçada, mesmo se não houver dependências nele**: quando selecionado, desinstala um pacote, mesmo se ele ainda está sendo referenciado no projeto.</span><span class="sxs-lookup"><span data-stu-id="2107e-208">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="2107e-209">Isso normalmente é usado em combinação com **remover dependências** para remover um pacote e tudo o que dependências ele instalado.</span><span class="sxs-lookup"><span data-stu-id="2107e-209">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="2107e-210">O uso dessa opção pode, no entanto, levar a referências quebradas no projeto.</span><span class="sxs-lookup"><span data-stu-id="2107e-210">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="2107e-211">Nesses casos, talvez você precise [reinstalar esses outros pacotes](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="2107e-211">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
