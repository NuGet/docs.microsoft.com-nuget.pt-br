---
title: "Referência de interface do usuário do Gerenciador de pacotes do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 62f6962b-7b84-4452-ae0d-a9e1ef1fc6f0
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
description: "Instruções para usar o NuGet Package Manager UI no Visual Studio para trabalhar com pacotes do NuGet."
keywords: "NuGet UI, Gerenciador de pacotes do NuGet da interface do usuário, o NuGet no Visual Studio, gerenciamento de pacotes do NuGet, interface de usuário do NuGet, o Gerenciador de pacotes no Visual Studio"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88e987054f3c59a327f71b15330a99eb350449e5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-package-manager-ui"></a><span data-ttu-id="2bec4-104">Interface do usuário de Gerenciador de pacotes do NuGet</span><span class="sxs-lookup"><span data-stu-id="2bec4-104">NuGet Package Manager UI</span></span>

<span data-ttu-id="2bec4-105">O NuGet Package Manager UI no Visual Studio no Windows permite que você facilmente instalar, desinstalar e atualizar pacotes do NuGet em projetos e soluções.</span><span class="sxs-lookup"><span data-stu-id="2bec4-105">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="2bec4-106">Para obter a experiência no Visual Studio para Mac, consulte [incluindo NuGet um pacote em seu projeto](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="2bec4-106">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="2bec4-107">A UI do Gerenciador de pacote não está incluída com o código do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2bec4-107">The Package Manager UI is not included with Visual Studio Code.</span></span>

<span data-ttu-id="2bec4-108">Neste tópico:</span><span class="sxs-lookup"><span data-stu-id="2bec4-108">In this topic:</span></span>

- [<span data-ttu-id="2bec4-109">Localizar e instalar um pacote (guia de navegação)</span><span class="sxs-lookup"><span data-stu-id="2bec4-109">Finding and installing a package (Browse tab)</span></span>](#finding-and-installing-a-package)
- [<span data-ttu-id="2bec4-110">Desinstalar um pacote (guia instalado)</span><span class="sxs-lookup"><span data-stu-id="2bec4-110">Uninstalling a package (Installed tab)</span></span>](#uninstalling-a-package)
- <span data-ttu-id="2bec4-111">[Atualizando um pacote (guias instalado e atualizações)](#updating-a-package) (inclui o ["Mencionada implicitamente por um SDK" ou "AutoReferenced" mensagem](#implicit_reference))</span><span class="sxs-lookup"><span data-stu-id="2bec4-111">[Updating a package (Installed and Updates tabs)](#updating-a-package) (includes the ["Implicitly referenced by an SDK" or "AutoReferenced" message](#implicit_reference))</span></span>
- <span data-ttu-id="2bec4-112">[Gerenciando pacotes para a solução](#managing-packages-for-the-solution) (trabalhando com vários projetos ao mesmo tempo).</span><span class="sxs-lookup"><span data-stu-id="2bec4-112">[Managing packages for the solution](#managing-packages-for-the-solution) (working with multiple projects at the same time).</span></span>
- [<span data-ttu-id="2bec4-113">Fontes de pacote</span><span class="sxs-lookup"><span data-stu-id="2bec4-113">Package sources</span></span>](#package-sources)
- [<span data-ttu-id="2bec4-114">Controle de opções do Gerenciador de pacote</span><span class="sxs-lookup"><span data-stu-id="2bec4-114">Package manager Options control</span></span>](#package-manager-options-control)

> [!Note]
> <span data-ttu-id="2bec4-115">Verifique se está faltando o NuGet Package Manager no Visual Studio 2015, **Ferramentas > extensões e atualizações...**  e procure o *NuGet Package Manager* extensão.</span><span class="sxs-lookup"><span data-stu-id="2bec4-115">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="2bec4-116">Se não for possível usar o instalador de extensões do Visual Studio, baixe a extensão diretamente do [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="2bec4-116">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="2bec4-117">No Visual Studio de 2017, o NuGet e o NuGet Package Manager são instalados automaticamente com qualquer. Cargas de trabalho relacionados à rede.</span><span class="sxs-lookup"><span data-stu-id="2bec4-117">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="2bec4-118">Instalá-lo individuall selecionando o **componentes individuais > código Ferramentas > Gerenciador de pacotes do NuGet** opção no instalador do Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="2bec4-118">Install it individuall by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="2bec4-119">Localizar e instalar um pacote</span><span class="sxs-lookup"><span data-stu-id="2bec4-119">Finding and installing a package</span></span>

1. <span data-ttu-id="2bec4-120">Em **Solution Explorer**, clique **referências** ou um projeto e selecione **gerenciar pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="2bec4-120">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Gerenciar a opção de menu de pacotes do NuGet](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="2bec4-122">O **procurar** guia exibe pacotes por popularidade da origem selecionada atualmente (consulte [pacote fontes](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="2bec4-122">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="2bec4-123">Procurar por um pacote específico usando a caixa de pesquisa no canto superior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="2bec4-123">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="2bec4-124">Selecione um pacote na lista para exibir suas informações, que também permite que o **instalar** botão juntamente com um menu suspenso de seleção de versão.</span><span class="sxs-lookup"><span data-stu-id="2bec4-124">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Gerenciar guia Procurar de caixa de diálogo de pacotes do NuGet](media/Search.png)

1. <span data-ttu-id="2bec4-126">Selecione a versão desejada na lista suspensa e selecione **instalar**.</span><span class="sxs-lookup"><span data-stu-id="2bec4-126">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="2bec4-127">O Visual Studio instala o pacote e suas dependências no projeto.</span><span class="sxs-lookup"><span data-stu-id="2bec4-127">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="2bec4-128">Você poderá ser solicitado a aceitar os termos de licença.</span><span class="sxs-lookup"><span data-stu-id="2bec4-128">You may be asked to accept license terms.</span></span> <span data-ttu-id="2bec4-129">Quando a instalação for concluída, os pacotes adicionados são exibidos no **instalado** guia. Os pacotes também são listados no **referências** nó do Gerenciador de soluções, indicando que você possa consultá-los no projeto com `using` instruções.</span><span class="sxs-lookup"><span data-stu-id="2bec4-129">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Referências no Gerenciador de soluções](media/References.png)

> [!Tip]
    > <span data-ttu-id="2bec4-131">Para incluir as versões de pré-lançamento na pesquisa e para disponibilizar as versões de pré-lançamento na versão de lista suspensa, selecione o **incluir pré-lançamento** opção.</span><span class="sxs-lookup"><span data-stu-id="2bec4-131">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="2bec4-132">Desinstalar um pacote</span><span class="sxs-lookup"><span data-stu-id="2bec4-132">Uninstalling a package</span></span>

1. <span data-ttu-id="2bec4-133">Em **Solution Explorer**, clique **referências** ou o projeto desejado e selecione **gerenciar pacotes NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="2bec4-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="2bec4-134">Selecione o **instalado** guia.</span><span class="sxs-lookup"><span data-stu-id="2bec4-134">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="2bec4-135">Selecione o pacote para desinstalar (usando a pesquisa para filtrar a lista, se necessário) e selecione **desinstalação**.</span><span class="sxs-lookup"><span data-stu-id="2bec4-135">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Desinstalar um pacote](media/UninstallPackage.png)

1. <span data-ttu-id="2bec4-137">Observe que o **incluem preprelease** e **origem do pacote** controles não têm nenhum efeito durante a desinstalação de pacotes.</span><span class="sxs-lookup"><span data-stu-id="2bec4-137">Note that the **Include preprelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="2bec4-138">Um pacote de atualização</span><span class="sxs-lookup"><span data-stu-id="2bec4-138">Updating a package</span></span>

1. <span data-ttu-id="2bec4-139">Em **Solution Explorer**, clique **referências** ou o projeto desejado e selecione **gerenciar pacotes NuGet...** . (Em projetos de site da web, clique com botão direito do **Bin** pasta.)</span><span class="sxs-lookup"><span data-stu-id="2bec4-139">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="2bec4-140">Selecione o **atualizações** guia para ver os pacotes que têm atualizações disponíveis de origens do pacote selecionado.</span><span class="sxs-lookup"><span data-stu-id="2bec4-140">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="2bec4-141">Selecione **incluir pré-lançamento** inclui pacotes pré-lançados na lista de atualização.</span><span class="sxs-lookup"><span data-stu-id="2bec4-141">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="2bec4-142">Selecione o pacote para atualizar, selecione a versão desejada na lista suspensa à direita e selecione **atualizar**.</span><span class="sxs-lookup"><span data-stu-id="2bec4-142">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Um pacote de atualização](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="2bec4-144">Para alguns pacotes, o **atualização** botão será desabilitado e será exibida uma mensagem dizendo que é "implicitamente referenciado por um SDK" (ou "AutoReferenced").</span><span class="sxs-lookup"><span data-stu-id="2bec4-144">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="2bec4-145">A mensagem indica que o pacote, como Microsoft.NETCore.App ou Microsoft.NETStandard.Library, faz parte de uma estrutura ou o SDK maior e não deve ser atualizado independentemente.</span><span class="sxs-lookup"><span data-stu-id="2bec4-145">The message indicates that the package, such as Microsoft.NETCore.App or Microsoft.NETStandard.Library, is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="2bec4-146">(Esse packagee internamente são marcados com `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Para atualizar o pacote, atualize o SDK ao qual ele pertence.</span><span class="sxs-lookup"><span data-stu-id="2bec4-146">(Such packagee are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) To update the package, update the SDK to which it belongs.</span></span>

    ![Pacote de exemplo são marcados como implicitamente referências ou AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="2bec4-148">Para atualizar vários pacotes para as versões mais recentes, selecione na lista e selecione o **atualizar** botão acima da lista.</span><span class="sxs-lookup"><span data-stu-id="2bec4-148">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="2bec4-149">Você também pode atualizar um pacote individual do **instalado** guia. Nesse caso, os detalhes do pacote incluem um seletor de versão (sujeito a **incluir pré-lançamento** opção) e um **atualização** botão.</span><span class="sxs-lookup"><span data-stu-id="2bec4-149">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="2bec4-150">Gerenciando pacotes para a solução</span><span class="sxs-lookup"><span data-stu-id="2bec4-150">Managing packages for the solution</span></span>

<span data-ttu-id="2bec4-151">Gerenciando pacotes para uma solução é uma maneira conveniente para trabalhar com vários projetos simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="2bec4-151">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="2bec4-152">Selecione o **Ferramentas > Gerenciador de pacotes do NuGet > Gerenciar pacotes NuGet para solução...**  menu de comando, ou a solução e selecione **gerenciar pacotes NuGet...** :</span><span class="sxs-lookup"><span data-stu-id="2bec4-152">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Gerenciar pacotes NuGet para a solução](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="2bec4-154">Ao gerenciar pacotes da solução, a interface do usuário permite que você selecione os projetos que são afetados pelas operações:</span><span class="sxs-lookup"><span data-stu-id="2bec4-154">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Seletor de projeto ao gerenciar pacotes da solução](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="2bec4-156">Consolidar guia</span><span class="sxs-lookup"><span data-stu-id="2bec4-156">Consolidate tab</span></span>

<span data-ttu-id="2bec4-157">Os desenvolvedores geralmente ele considerar prática inadequada para usar versões diferentes do mesmo pacote do NuGet em diferentes projetos na mesma solução.</span><span class="sxs-lookup"><span data-stu-id="2bec4-157">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="2bec4-158">Quando você optar por gerenciar os pacotes para uma solução, a UI Package Manager fornece um **consolidar** guia na qual você pode ver facilmente onde os pacotes com números de versão diferentes são usados por diferentes projetos na solução:</span><span class="sxs-lookup"><span data-stu-id="2bec4-158">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Guia de consolidar de interface do usuário do Gerenciador de pacotes](media/ConsolidateTab.png)

<span data-ttu-id="2bec4-160">Neste exemplo, o projeto ClassLibrary1 está usando EntityFramework 6.2.0, enquanto ConsoleApp1 é usando o EntityFramework 6.2.0.</span><span class="sxs-lookup"><span data-stu-id="2bec4-160">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.2.0.</span></span> <span data-ttu-id="2bec4-161">Para consolidar as versões do pacote, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2bec4-161">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="2bec4-162">Selecione os projetos para atualizar a lista de projeto.</span><span class="sxs-lookup"><span data-stu-id="2bec4-162">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="2bec4-163">Selecione a versão a ser usado em todos os projetos no **versão** controle, como EntityFramework 6.2.0.</span><span class="sxs-lookup"><span data-stu-id="2bec4-163">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="2bec4-164">Selecione o **instalar** botão.</span><span class="sxs-lookup"><span data-stu-id="2bec4-164">Select the **Install** button.</span></span>

<span data-ttu-id="2bec4-165">O Gerenciador de pacote instala a versão do pacote selecionado em todos os projetos selecionados, após o qual o pacote não aparecerá mais no **consolidar** guia.</span><span class="sxs-lookup"><span data-stu-id="2bec4-165">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="2bec4-166">Fontes de pacote</span><span class="sxs-lookup"><span data-stu-id="2bec4-166">Package sources</span></span>

<span data-ttu-id="2bec4-167">Para alterar a origem do qual o Visual Studio obtém pacotes, selecione um do seletor de origem:</span><span class="sxs-lookup"><span data-stu-id="2bec4-167">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Seletor de origem do pacote no Gerenciador de pacote da interface do usuário](media/PackageSourceDropDown.png)

<span data-ttu-id="2bec4-169">Para gerenciar fontes de pacote:</span><span class="sxs-lookup"><span data-stu-id="2bec4-169">To manage package sources:</span></span>

1. <span data-ttu-id="2bec4-170">Selecione o **configurações** ícone na UI do Gerenciador de pacotes descritas a seguir ou use o **Ferramentas > Opções** de comando e role até **NuGet Package Manager**:</span><span class="sxs-lookup"><span data-stu-id="2bec4-170">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Ícone de configurações de interface do usuário do pacote manager](media/PackageSourceSettings.png)

1. <span data-ttu-id="2bec4-172">Selecione o **origens do pacote** nó:</span><span class="sxs-lookup"><span data-stu-id="2bec4-172">Select the **Package Sources** node:</span></span>

    ![Opções de fontes de pacote](media/options.png)

1. <span data-ttu-id="2bec4-174">Para adicionar uma fonte, selecione  **+** , edite o nome, digite a URL ou caminho de **fonte** controle e selecione **atualização**.</span><span class="sxs-lookup"><span data-stu-id="2bec4-174">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="2bec4-175">A fonte agora aparece no seletor de lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="2bec4-175">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="2bec4-176">Para alterar uma origem do pacote, selecioná-lo, faça edições no **nome** e **fonte** caixas e selecione **atualização**.</span><span class="sxs-lookup"><span data-stu-id="2bec4-176">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="2bec4-177">Para desabilitar uma origem do pacote, desmarque a caixa à esquerda do nome na lista.</span><span class="sxs-lookup"><span data-stu-id="2bec4-177">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="2bec4-178">Para remover uma origem do pacote, selecione-o e, em seguida, selecione o **X** botão.</span><span class="sxs-lookup"><span data-stu-id="2bec4-178">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="2bec4-179">Use a cima e para os botões de seta para alterar a ordem de prioridade das origens do pacote.</span><span class="sxs-lookup"><span data-stu-id="2bec4-179">Use the up and down arrow buttons to change the priority order of the package sources.</span></span> <span data-ttu-id="2bec4-180">O Visual Studio procura essas fontes na ordem de prioridade ao restaurar pacotes para um projeto.</span><span class="sxs-lookup"><span data-stu-id="2bec4-180">Visual Studio searches these sources in the priority order when restoring packages for a project.</span></span> <span data-ttu-id="2bec4-181">Para obter mais informações, consulte [restauração do pacote](../Consume-Packages/Package-Restore.md).</span><span class="sxs-lookup"><span data-stu-id="2bec4-181">For more information, see [Package restore](../Consume-Packages/Package-Restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="2bec4-182">Se uma origem de pacote reaparecer após a exclusão, podem ser listado em um nível de computador ou usuário `NuGet.Config` arquivos.</span><span class="sxs-lookup"><span data-stu-id="2bec4-182">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="2bec4-183">Consulte [NuGet Configurando comportamento](../Consume-Packages/Configuring-NuGet-Behavior.md) para o local desses arquivos, em seguida, remover a fonte editando os arquivos manualmente ou usando o [nuget fontes comando](../tools/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="2bec4-183">See [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="2bec4-184">Controle de opções do Gerenciador de pacote</span><span class="sxs-lookup"><span data-stu-id="2bec4-184">Package manager Options control</span></span>

<span data-ttu-id="2bec4-185">Quando um pacote é selecionado, a UI Package Manager exibe um pequeno expansível **opções** controle abaixo do seletor de versão (mostrado aqui ambos recolhidos e expandidos).</span><span class="sxs-lookup"><span data-stu-id="2bec4-185">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="2bec4-186">Observe que, para alguns tipos, como .NET Core e empresas de projeto a `project.json` formato de referência, somente o **Mostrar janela de visualização** opção é fornecida.</span><span class="sxs-lookup"><span data-stu-id="2bec4-186">Note that for some project types, such as .NET Core and those using the `project.json` reference format, only the **Show preview window** option is provided.</span></span>

![Opções do Gerenciador de pacote](media/PackageManagerUIOptions.png)

<span data-ttu-id="2bec4-188">As seções a seguir explicam essas opções.</span><span class="sxs-lookup"><span data-stu-id="2bec4-188">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="2bec4-189">Mostrar janela de visualização</span><span class="sxs-lookup"><span data-stu-id="2bec4-189">Show preview window</span></span>

<span data-ttu-id="2bec4-190">Quando selecionada, uma janela modal exibe quais as dependências de um pacote escolhido antes de instalar o pacote:</span><span class="sxs-lookup"><span data-stu-id="2bec4-190">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Caixa de diálogo de visualização de exemplo](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="2bec4-192">Opções de atualização e instalação</span><span class="sxs-lookup"><span data-stu-id="2bec4-192">Install and Update Options</span></span>

<span data-ttu-id="2bec4-193">(Não disponível para todos os tipos de projeto.)</span><span class="sxs-lookup"><span data-stu-id="2bec4-193">(Not available for all project types.)</span></span>

<span data-ttu-id="2bec4-194">**Comportamento da dependência** configura como o NuGet decide quais versões dos pacotes dependentes para instalar:</span><span class="sxs-lookup"><span data-stu-id="2bec4-194">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="2bec4-195">*Ignorar dependências* ignora a instalação de todas as dependências, que normalmente interrompe o pacote que está sendo instalado.</span><span class="sxs-lookup"><span data-stu-id="2bec4-195">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="2bec4-196">*Menor* [padrão] instala a dependência com o número de versão mínima que atenda aos requisitos do pacote principal escolhido.</span><span class="sxs-lookup"><span data-stu-id="2bec4-196">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="2bec4-197">*Patch do mais alto* instala a versão com os mesmos números de versão primária e secundária, mas o número mais alto de patch.</span><span class="sxs-lookup"><span data-stu-id="2bec4-197">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="2bec4-198">Por exemplo, se a versão 1.2.2 for especificada, em seguida, a versão mais recente que começa com 1.2 será instalada</span><span class="sxs-lookup"><span data-stu-id="2bec4-198">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="2bec4-199">*Mais alta secundária* instala a versão com o mesmo número de versão principal, mas o número mais alto de pequena e o número de patch.</span><span class="sxs-lookup"><span data-stu-id="2bec4-199">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="2bec4-200">Se a versão 1.2.2 for especificada, a versão mais recente que começa com 1 será instalada</span><span class="sxs-lookup"><span data-stu-id="2bec4-200">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="2bec4-201">*Mais alto* instala a versão mais recente disponível do pacote.</span><span class="sxs-lookup"><span data-stu-id="2bec4-201">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="2bec4-202">**Ação de conflitos de arquivo** Especifica como o NuGet deve manipular pacotes que já existem no projeto ou no computador local:</span><span class="sxs-lookup"><span data-stu-id="2bec4-202">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="2bec4-203">*Prompt* instrui o NuGet para perguntar se deseja manter ou substituir os pacotes existentes.</span><span class="sxs-lookup"><span data-stu-id="2bec4-203">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="2bec4-204">*Ignorar tudo* instrui o NuGet para ignorar a substituição de todos os pacotes existentes.</span><span class="sxs-lookup"><span data-stu-id="2bec4-204">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="2bec4-205">*Substituir todos os* instrui o NuGet para substituir todos os pacotes existentes.</span><span class="sxs-lookup"><span data-stu-id="2bec4-205">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="2bec4-206">As opções de desinstalação</span><span class="sxs-lookup"><span data-stu-id="2bec4-206">Uninstall Options</span></span>

<span data-ttu-id="2bec4-207">(Não disponível para todos os tipos de projeto.)</span><span class="sxs-lookup"><span data-stu-id="2bec4-207">(Not available for all project types.)</span></span>

<span data-ttu-id="2bec4-208">**Remover dependências**: quando selecionada, remove todos os pacotes dependentes que elas não são referenciadas em outro lugar no projeto.</span><span class="sxs-lookup"><span data-stu-id="2bec4-208">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="2bec4-209">**Forçar desinstalação mesmo se houver dependências nele**: quando selecionado, desinstala um pacote mesmo se ele ainda está sendo referenciado no projeto.</span><span class="sxs-lookup"><span data-stu-id="2bec4-209">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="2bec4-210">Isso geralmente é usado em combinação com **remover dependências** para remover um pacote e tudo o que ele instalado de dependências.</span><span class="sxs-lookup"><span data-stu-id="2bec4-210">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="2bec4-211">O uso dessa opção pode, no entanto, levar a um referências quebradas no projeto.</span><span class="sxs-lookup"><span data-stu-id="2bec4-211">Using this option may, however, lead to a broken references in the project.</span></span> <span data-ttu-id="2bec4-212">Nesses casos você talvez seja necessário [reinstalar esses outros pacotes](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="2bec4-212">In such cases you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>