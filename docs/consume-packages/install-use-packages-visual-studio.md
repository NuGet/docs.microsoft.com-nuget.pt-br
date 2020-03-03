---
title: Instalar e gerenciar pacotes do NuGet no Visual Studio
description: Instruções para usar a interface do usuário do Gerenciador de Pacotes do NuGet no Visual Studio para trabalhar com pacotes do NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 3adceac8c725d9ea1610aea090753c9c1d8bc818
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231001"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a><span data-ttu-id="7d9d6-103">Instalar e gerenciar pacotes no Visual Studio usando o Gerenciador de Pacotes do NuGet</span><span class="sxs-lookup"><span data-stu-id="7d9d6-103">Install and manage packages in Visual Studio using the NuGet Package Manager</span></span>

<span data-ttu-id="7d9d6-104">A interface do usuário do Gerenciador de Pacotes do NuGet no Visual Studio no Windows possibilita instalar, desinstalar e atualizar pacotes do NuGet com facilidade em projetos e soluções.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="7d9d6-105">Para obter a experiência no Visual Studio para Mac, confira [Incluir um pacote do NuGet em seu projeto](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span><span class="sxs-lookup"><span data-stu-id="7d9d6-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span></span> <span data-ttu-id="7d9d6-106">A interface do usuário do Gerenciador de Pacotes não está incluída no Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="7d9d6-107">Se você não tem o Gerenciador de Pacotes do NuGet no Visual Studio 2015, marque **Ferramentas > Extensões e Atualizações...** e pesquise pela extensão *Gerenciador de Pacotes do NuGet*.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="7d9d6-108">Se não é possível usar o instalador de extensões no Visual Studio, baixe a extensão diretamente de [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="7d9d6-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="7d9d6-109">A partir do Visual Studio 2017, o NuGet e o Gerenciador de Pacotes do NuGet são instalados automaticamente com qualquer carga de trabalho relacionada ao .NET.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="7d9d6-110">Para instalá-los individualmente, selecione a opção **Componentes individuais > Ferramentas de código > Gerenciador de Pacotes do NuGet** no instalador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="7d9d6-111">Encontrar e instalar um pacote</span><span class="sxs-lookup"><span data-stu-id="7d9d6-111">Find and install a package</span></span>

1. <span data-ttu-id="7d9d6-112">No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Referências** ou em um projeto e selecione **Gerenciar Pacotes do NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Opção de menu Gerenciar Pacotes do NuGet](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="7d9d6-114">A guia **Procurar** exibe pacotes por popularidade a partir da origem selecionada no momento (confira [origens de pacotes](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="7d9d6-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="7d9d6-115">Procure um pacote específico usando a caixa de pesquisa no canto superior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="7d9d6-116">Selecione um pacote na lista para exibir as informações sobre ele, o que também habilita o botão **Instalar** com uma lista suspensa de seleção de versão.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Guia Procurar da caixa de diálogo Gerenciar Pacotes do NuGet](media/Search.png)

1. <span data-ttu-id="7d9d6-118">Selecione a versão desejada na lista suspensa e selecione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="7d9d6-119">O Visual Studio instala o pacote e suas dependências no projeto.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="7d9d6-120">Você pode ser solicitado a aceitar os termos de licença.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="7d9d6-121">Quando a instalação for concluída, os pacotes adicionados aparecerão na guia **instalado** . os pacotes também são listados no nó **referências** de Gerenciador de soluções, indicando que você pode consultá-los no projeto com instruções `using`.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Referências no Gerenciador de Soluções](media/References.png)

> [!Tip]
> <span data-ttu-id="7d9d6-123">Para incluir versões de pré-lançamento na pesquisa e disponibilizar essas versões na lista suspensa de versões, selecione a opção **Incluir pré-lançamento**.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

> [!Note]
> <span data-ttu-id="7d9d6-124">O NuGet tem dois formatos nos quais um projeto pode usar pacotes: [`PackageReference`](package-references-in-project-files.md) e [`packages.config`](../reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="7d9d6-124">NuGet has two formats in which a project may use packages: [`PackageReference`](package-references-in-project-files.md) and [`packages.config`](../reference/packages-config.md).</span></span> <span data-ttu-id="7d9d6-125">[O padrão pode ser definido na janela Opções do Visual Studio](Package-Restore.md#choose-default-package-management-format).</span><span class="sxs-lookup"><span data-stu-id="7d9d6-125">[The default can be set in Visual Studio's options window](Package-Restore.md#choose-default-package-management-format).</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="7d9d6-126">Desinstalar um pacote</span><span class="sxs-lookup"><span data-stu-id="7d9d6-126">Uninstall a package</span></span>

1. <span data-ttu-id="7d9d6-127">No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Referências** ou no projeto desejado e selecione **Gerenciar Pacotes do NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-127">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="7d9d6-128">Selecione a guia **Instalado**.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-128">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="7d9d6-129">Selecione o pacote a desinstalar (usando a pesquisa para filtrar a lista, se necessário) e selecione **Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-129">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Desinstalar um pacote](media/UninstallPackage.png)

1. <span data-ttu-id="7d9d6-131">Os controles **Incluir pré-lançamento** e **Origem do pacote** não têm efeito ao desinstalar pacotes.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-131">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="7d9d6-132">Atualizar um pacote</span><span class="sxs-lookup"><span data-stu-id="7d9d6-132">Update a package</span></span>

1. <span data-ttu-id="7d9d6-133">Em **Gerenciador de soluções**, clique com o botão direito do mouse em **referências** ou projeto desejado e selecione **gerenciar pacotes NuGet...**. (Em projetos de site, clique com o botão direito do mouse na pasta **bin** .)</span><span class="sxs-lookup"><span data-stu-id="7d9d6-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="7d9d6-134">Selecione a guia **Atualizações** para ver os pacotes que têm atualizações disponíveis das origens de pacotes selecionadas.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-134">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="7d9d6-135">Selecione **Incluir pré-lançamento** para incorporar pacotes de pré-lançamento à lista de atualizações.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-135">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="7d9d6-136">Selecione o pacote a atualizar, escolha a versão desejada na lista suspensa à direita e selecione **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-136">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Atualizar um pacote](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="7d9d6-138">Em alguns pacotes, o botão **Atualizar** fica desabilitado e uma mensagem é exibida informando que é "Referenciado implicitamente por um SDK" (ou "Autorreferenciado").</span><span class="sxs-lookup"><span data-stu-id="7d9d6-138">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="7d9d6-139">Essa mensagem indica que o pacote faz parte de uma estrutura ou SDK mais amplo e não deve ser atualizado de forma independente.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-139">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="7d9d6-140">(Esses pacotes são marcados internamente com `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Por exemplo, `Microsoft.NETCore.App` faz parte do SDK do .NET Core, e a versão do pacote não é igual à versão da estrutura de tempo de execução usada pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-140">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="7d9d6-141">É preciso [atualizar a instalação do .NET Core](https://aka.ms/dotnet-download) para obter novas versões do ASP.NET Core e do runtime do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-141">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="7d9d6-142">[Confira este documento para saber mais sobre o controle de versão e os metapacotes do .NET Core](/dotnet/core/packages).</span><span class="sxs-lookup"><span data-stu-id="7d9d6-142">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="7d9d6-143">Isso se aplica aos seguintes pacotes usados com frequência:</span><span class="sxs-lookup"><span data-stu-id="7d9d6-143">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="7d9d6-144">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="7d9d6-144">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="7d9d6-145">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="7d9d6-145">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="7d9d6-146">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="7d9d6-146">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="7d9d6-147">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="7d9d6-147">NETStandard.Library</span></span>

    ![Exemplo de pacote marcado como Referenciado implicitamente ou Autorreferenciado](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="7d9d6-149">Para atualizar vários pacotes para suas versões mais recentes, selecione-os na lista e selecione o botão **Atualizar** acima da lista.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-149">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="7d9d6-150">Você também pode atualizar um pacote individual na guia **instalado** . Nesse caso, os detalhes do pacote incluem um seletor de versão (sujeito à opção de **pré-lançamento de inclusão** ) e um botão de **atualização** .</span><span class="sxs-lookup"><span data-stu-id="7d9d6-150">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="manage-packages-for-the-solution"></a><span data-ttu-id="7d9d6-151">Gerenciar pacotes para a solução</span><span class="sxs-lookup"><span data-stu-id="7d9d6-151">Manage packages for the solution</span></span>

<span data-ttu-id="7d9d6-152">O gerenciamento de pacotes para uma solução é um meio conveniente de trabalhar com vários projetos ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-152">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="7d9d6-153">Selecione o comando no menu **Ferramentas > Gerenciador de Pacotes do NuGet > Gerenciar Pacotes do NuGet para Solução...** ou clique com o botão direito do mouse na solução e selecione **Gerenciar Pacotes do NuGet...**:</span><span class="sxs-lookup"><span data-stu-id="7d9d6-153">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Gerenciar Pacotes do NuGet para a solução](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="7d9d6-155">Ao gerenciar pacotes para a solução, a interface do usuário possibilita selecionar os projetos afetados pelas operações:</span><span class="sxs-lookup"><span data-stu-id="7d9d6-155">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Seletor de projeto ao gerenciar pacotes para a solução](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="7d9d6-157">Guia Consolidar</span><span class="sxs-lookup"><span data-stu-id="7d9d6-157">Consolidate tab</span></span>

<span data-ttu-id="7d9d6-158">Os desenvolvedores costumam considerar uma prática inadequada usar versões diferentes do mesmo pacote do NuGet em diferentes projetos na mesma solução.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-158">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="7d9d6-159">Ao optar por gerenciar pacotes para uma solução, a interface do usuário do Gerenciador de Pacotes fornece uma guia **Consolidar**, em que é possível ver facilmente onde os pacotes com números de versão distintos são usados por diferentes projetos na solução:</span><span class="sxs-lookup"><span data-stu-id="7d9d6-159">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Guia Consolidar da interface do usuário do Gerenciador de Pacotes](media/ConsolidateTab.png)

<span data-ttu-id="7d9d6-161">Neste exemplo, o projeto ClassLibrary1 está usando EntityFramework 6.2.0, enquanto o ConsoleApp1 está usando EntityFramework 6.1.0.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-161">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="7d9d6-162">Para consolidar as versões de pacote, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7d9d6-162">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="7d9d6-163">Selecione os projetos a atualizar na lista de projetos.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-163">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="7d9d6-164">Selecione a versão a usar em todos esses projetos no controle **Versão**, como o EntityFramework 6.2.0.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-164">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="7d9d6-165">Selecione o botão **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-165">Select the **Install** button.</span></span>

<span data-ttu-id="7d9d6-166">O Gerenciador de Pacotes instala a versão de pacote selecionada em todos os projetos selecionados e, após isso, o pacote não aparece mais na guia **Consolidar**.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-166">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="7d9d6-167">Origens de pacotes</span><span class="sxs-lookup"><span data-stu-id="7d9d6-167">Package sources</span></span>

<span data-ttu-id="7d9d6-168">Para alterar a origem da qual o Visual Studio obtém pacotes, selecione uma no seletor de origem:</span><span class="sxs-lookup"><span data-stu-id="7d9d6-168">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Seletor de origem de pacotes na interface do usuário do Gerenciador de Pacotes](media/PackageSourceDropDown.png)

<span data-ttu-id="7d9d6-170">Para gerenciar origens de pacotes:</span><span class="sxs-lookup"><span data-stu-id="7d9d6-170">To manage package sources:</span></span>

1. <span data-ttu-id="7d9d6-171">Selecione o ícone **Configurações** na interface do usuário do Gerenciador de Pacotes descrita abaixo ou use o comando **Ferramentas> Opções** e role até **Gerenciador de Pacotes do NuGet**:</span><span class="sxs-lookup"><span data-stu-id="7d9d6-171">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Ícone de configurações da interface do usuário do Gerenciador de Pacotes](media/PackageSourceSettings.png)

1. <span data-ttu-id="7d9d6-173">Selecione o nó **Origens do Pacote**:</span><span class="sxs-lookup"><span data-stu-id="7d9d6-173">Select the **Package Sources** node:</span></span>

    ![Opções de Origens do Pacote](media/options.png)

1. <span data-ttu-id="7d9d6-175">Para adicionar uma origem, selecione **+**, edite o nome, insira a URL ou o caminho no controle **Origem** e selecione **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-175">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="7d9d6-176">A origem agora aparece na lista suspensa do seletor.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-176">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="7d9d6-177">Para alterar uma origem de pacotes, selecione-a, faça as edições nas caixas **Nome** e **Origem** e selecione **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-177">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="7d9d6-178">Para desabilitar uma origem de pacotes, desmarque a caixa à esquerda do nome na lista.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-178">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="7d9d6-179">Para remover uma origem de pacotes, selecione-a e, em seguida, selecione o botão **X**.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-179">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="7d9d6-180">O uso dos botões de seta para cima e para baixo não altera a ordem de prioridade das origens de pacotes.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-180">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="7d9d6-181">O Visual Studio ignora a ordem das origens de pacotes, usando o pacote de qualquer origem que responder às solicitações primeiro.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-181">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="7d9d6-182">Para saber mais, confira [Restauração de pacote](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="7d9d6-182">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="7d9d6-183">Caso uma origem de pacotes reapareça depois de ser excluída, pode ser listada em arquivos `NuGet.Config` no nível do computador ou do usuário.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-183">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="7d9d6-184">Confira [Configurações comuns do NuGet](../consume-packages/configuring-nuget-behavior.md) para conhecer o local desses arquivos, depois remova a origem editando os arquivos manualmente ou usando o [comando nuget sources](../reference/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="7d9d6-184">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../reference/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="7d9d6-185">Controle de opções do Gerenciador de Pacotes</span><span class="sxs-lookup"><span data-stu-id="7d9d6-185">Package manager Options control</span></span>

<span data-ttu-id="7d9d6-186">Ao selecionar um pacote, a interface do usuário do Gerenciador de Pacotes exibe um controle **Opções** pequeno e expansível abaixo do seletor de versão (mostrado aqui recolhido e expandido).</span><span class="sxs-lookup"><span data-stu-id="7d9d6-186">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="7d9d6-187">Em alguns tipos de projeto, apenas a opção **Mostrar janela de visualização** é fornecida.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-187">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Opções do Gerenciador de Pacotes](media/PackageManagerUIOptions.png)

<span data-ttu-id="7d9d6-189">As seções a seguir explicam essas opções.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-189">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="7d9d6-190">Mostrar janela de visualização</span><span class="sxs-lookup"><span data-stu-id="7d9d6-190">Show preview window</span></span>

<span data-ttu-id="7d9d6-191">Quando selecionada, uma janela modal exibe as dependências de um pacote escolhido antes da instalação do pacote:</span><span class="sxs-lookup"><span data-stu-id="7d9d6-191">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Exemplo da caixa de diálogo Visualizar](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="7d9d6-193">Opções de instalação e atualização</span><span class="sxs-lookup"><span data-stu-id="7d9d6-193">Install and Update Options</span></span>

<span data-ttu-id="7d9d6-194">Não disponíveis para todos os tipos de projeto.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-194">(Not available for all project types.)</span></span>

<span data-ttu-id="7d9d6-195">**Comportamento da dependência** define como o NuGet decide quais versões de pacotes dependentes serão instaladas:</span><span class="sxs-lookup"><span data-stu-id="7d9d6-195">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="7d9d6-196">*Ignorar Dependências* ignora a instalação de dependências, o que normalmente interrompe a instalação do pacote.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-196">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="7d9d6-197">*Mais Baixa* [Padrão] instala a dependência com o número de versão mínimo que atende aos requisitos do pacote principal escolhido.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-197">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="7d9d6-198">*Patch Mais Alto* instala a versão com os mesmos números de versão principal e secundária, mas com o número de patch mais alto.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-198">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="7d9d6-199">Por exemplo, se a versão 1.2.2 for especificada, a versão mais alta que começa com 1.2 será instalada</span><span class="sxs-lookup"><span data-stu-id="7d9d6-199">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="7d9d6-200">*Secundário Mais Alto* instala a versão com o mesmo número de versão principal, mas com o número secundário e o número de patch mais altos.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-200">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="7d9d6-201">Se a versão 1.2.2 for especificada, a versão mais alta que começa com 1 será instalada</span><span class="sxs-lookup"><span data-stu-id="7d9d6-201">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="7d9d6-202">*Mais Alta* instala a versão mais alta disponível do pacote.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-202">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="7d9d6-203">**Ação de conflito de arquivo** especifica como o NuGet deve lidar com pacotes que já existem no projeto ou no computador local:</span><span class="sxs-lookup"><span data-stu-id="7d9d6-203">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="7d9d6-204">*Avisar* instrui o NuGet a perguntar se os pacotes existentes serão mantidos ou substituídos.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-204">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="7d9d6-205">*Ignorar tudo* instrui o NuGet a ignorar a substituição de pacotes existentes.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-205">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="7d9d6-206">*Substituir Tudo* instrui o NuGet a substituir pacotes existentes.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-206">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="7d9d6-207">Opções de desinstalação</span><span class="sxs-lookup"><span data-stu-id="7d9d6-207">Uninstall Options</span></span>

<span data-ttu-id="7d9d6-208">Não disponíveis para todos os tipos de projeto.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-208">(Not available for all project types.)</span></span>

<span data-ttu-id="7d9d6-209">**Remover dependências**: quando selecionada, remove todos os pacotes dependentes caso não estejam referenciados em outro lugar no projeto.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-209">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="7d9d6-210">**Forçar desinstalação, mesmo se houver dependências**: quando selecionada, desinstala um pacote mesmo se ele ainda está sendo referenciado no projeto.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-210">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="7d9d6-211">Normalmente, isso é usado em combinação com **Remover dependências** para remover um pacote e quaisquer dependências que ele instalou.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-211">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="7d9d6-212">No entanto, o uso dessa opção pode causar referências inválidas no projeto.</span><span class="sxs-lookup"><span data-stu-id="7d9d6-212">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="7d9d6-213">Nesses casos, talvez seja necessário [reinstalar os outros pacotes](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="7d9d6-213">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
