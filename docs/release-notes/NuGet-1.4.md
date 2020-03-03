---
title: Notas de versão do NuGet 1,4
description: Notas de versão do NuGet 1,4 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b31c02b9251d6d45d952fdf8b111493495d57ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230701"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="f3cc5-103">Notas de versão do NuGet 1,4</span><span class="sxs-lookup"><span data-stu-id="f3cc5-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="f3cc5-104">[Notas de versão do nuget 1,3](../release-notes/nuget-1.3.md) | [notas de versão do NuGet 1,5](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="f3cc5-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="f3cc5-105">O NuGet 1,4 foi lançado em 17 de junho de 2011.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="f3cc5-106">Recursos</span><span class="sxs-lookup"><span data-stu-id="f3cc5-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="f3cc5-107">Aprimoramentos do pacote de atualização</span><span class="sxs-lookup"><span data-stu-id="f3cc5-107">Update-Package improvements</span></span>
<span data-ttu-id="f3cc5-108">O NuGet 1,4 apresenta muitos aprimoramentos no comando Update-Package, facilitando a manutenção de pacotes na mesma versão em vários projetos em uma solução.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="f3cc5-109">Por exemplo, ao atualizar um pacote para a versão mais recente, é muito comum que você queira que todos os projetos com o pacote instalado sejam atualizados para o mesmo verision.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="f3cc5-110">O comando `Update-Package` agora torna mais fácil:</span><span class="sxs-lookup"><span data-stu-id="f3cc5-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="f3cc5-111">Atualizar todos os pacotes em um único projeto</span><span class="sxs-lookup"><span data-stu-id="f3cc5-111">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="f3cc5-112">Atualizar um pacote em todos os projetos</span><span class="sxs-lookup"><span data-stu-id="f3cc5-112">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="f3cc5-113">Atualizar todos os pacotes em todos os projetos</span><span class="sxs-lookup"><span data-stu-id="f3cc5-113">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="f3cc5-114">Executar uma atualização "segura" em todos os pacotes</span><span class="sxs-lookup"><span data-stu-id="f3cc5-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="f3cc5-115">O sinalizador de `-Safe` restringe atualizações para apenas versões com o mesmo componente de versão principal e secundária.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="f3cc5-116">Por exemplo, se a versão 1.0.0 de um pacote estiver instalada e as versões 1.0.1, 1.0.2 e 1,1 estiverem disponíveis no feed, o sinalizador de `-Safe` atualizará o pacote para 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="f3cc5-117">Atualizar sem o sinalizador de `-Safe` atualizaria o pacote para a versão mais recente, 1,1.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="f3cc5-118">Gerenciando pacotes no nível da solução</span><span class="sxs-lookup"><span data-stu-id="f3cc5-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="f3cc5-119">Antes do NuGet 1,4, a instalação de um pacote em vários projetos era complicada usando a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="f3cc5-120">Ele exigiu a inicialização da caixa de diálogo uma vez por projeto.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="f3cc5-121">O NuGet 1,4 adiciona suporte para instalação/desinstalação/atualização de pacotes em vários projetos ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="f3cc5-122">Basta iniciar o clicando com o botão direito do mouse na solução e selecionando a opção de menu **gerenciar pacotes NuGet** .</span><span class="sxs-lookup"><span data-stu-id="f3cc5-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Caixa de diálogo gerenciar pacotes NuGet no nível da solução](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="f3cc5-124">Observe que na barra de título da caixa de diálogo, o nome da solução é exibido, não o nome de um projeto.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="f3cc5-125">As operações de pacote agora fornecem uma lista de caixas de seleção com a lista de projetos aos quais a operação deve ser aplicada.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Gerenciar a seleção de projeto de pacotes NuGet](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="f3cc5-127">Para obter mais detalhes, consulte o tópico sobre como [gerenciar pacotes para a solução](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="f3cc5-127">For more details, see the topic on [Managing Packages for the Solution](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="f3cc5-128">Restringindo atualizações para versões permitidas</span><span class="sxs-lookup"><span data-stu-id="f3cc5-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="f3cc5-129">Por padrão, ao executar o comando `Update-Package` em um pacote (ou atualizar o pacote usando a caixa de diálogo), ele será atualizado para a versão mais recente no feed.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="f3cc5-130">Com o novo suporte para atualizar todos os pacotes, pode haver casos em que você deseja bloquear um pacote para um intervalo de versão específico.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="f3cc5-131">Por exemplo, você pode saber com antecedência que seu aplicativo só funcionará com a versão 2. \* de um pacote, mas não 3,0 e acima.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="f3cc5-132">Para evitar a atualização acidental do pacote para 3, o NuGet 1,4 adiciona suporte para restringir o intervalo de versões para as quais os pacotes podem ser atualizados manualmente editando o arquivo de `packages.config` usando o novo atributo `allowedVersions`.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="f3cc5-133">Por exemplo, o exemplo a seguir mostra como bloquear o pacote de `SomePackage` o intervalo de versão 2,0-3,0 (exclusivo).</span><span class="sxs-lookup"><span data-stu-id="f3cc5-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="f3cc5-134">O atributo `allowedVersions` aceita valores usando o [formato de intervalo de versão](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="f3cc5-134">The `allowedVersions` attribute accepts values using the [version range format](../concepts/package-versioning.md#version-ranges).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="f3cc5-135">Observe que, em 1,4, o bloqueio de um pacote para um intervalo de versão específico deve ser editado manualmente.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="f3cc5-136">No NuGet 1,5, planejamos adicionar suporte para colocar esse intervalo por meio do comando `Install-Package`.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="f3cc5-137">Visualizador de pacote</span><span class="sxs-lookup"><span data-stu-id="f3cc5-137">Package Visualizer</span></span>
<span data-ttu-id="f3cc5-138">O novo Visualizador de pacote, iniciado por meio da opção de menu **ferramentas** -> **Gerenciador de pacotes de biblioteca** -> Visualizador de **pacotes** , permite que você visualize facilmente todos os projetos e suas dependências de pacote dentro de uma solução.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="f3cc5-139">_**Observação importante:** Esse recurso aproveita o suporte do DGML no Visual Studio. Só há suporte para a criação da visualização no Visual Studio Ultimate. Só há suporte para a exibição de um diagrama DGML no Visual Studio Premium ou superior._</span><span class="sxs-lookup"><span data-stu-id="f3cc5-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Visualizador de pacote](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="f3cc5-141">Verificação de atualização automática para a caixa de diálogo do NuGet</span><span class="sxs-lookup"><span data-stu-id="f3cc5-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="f3cc5-142">Algumas versões do NuGet introduzem novos recursos expressos por meio do arquivo de `.nuspec` que não são compreendidos por versões mais antigas da caixa de diálogo do NuGet.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="f3cc5-143">Um exemplo é a introdução no NuGet 1,4 para [especificar assemblies de estrutura](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="f3cc5-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="f3cc5-144">Por isso, é importante usar a versão mais recente do NuGet para garantir que você possa usar pacotes que aproveitam os recursos mais recentes.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="f3cc5-145">Para tornar as atualizações do NuGet mais visíveis, a caixa de diálogo NuGet contém a lógica para realçar quando uma versão mais recente está disponível.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="f3cc5-146">_**Observação**: a verificação só será feita se a guia **online** tiver sido selecionada na sessão atual._</span><span class="sxs-lookup"><span data-stu-id="f3cc5-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Caixa de diálogo gerenciar pacotes NuGet com a nova versão disponível](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="f3cc5-148">Para desativar a verificação automática de atualizações, vá para a caixa de diálogo Configurações do NuGet e desmarque **verificar automaticamente se há atualizações**.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![Configurações do NuGet](./media/nuget-settings.png)

<span data-ttu-id="f3cc5-150">Esse recurso foi realmente adicionado no NuGet 1,3, mas não estaria visível, é claro, até que uma atualização para 1,3, como o NuGet 1,4, fosse disponibilizada.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="f3cc5-151">Melhorias da caixa de diálogo do Gerenciador de pacotes</span><span class="sxs-lookup"><span data-stu-id="f3cc5-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="f3cc5-152">**Nomes de menu aprimorados**: as opções de menu para iniciar a caixa de diálogo foram renomeadas para fins de clareza.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="f3cc5-153">A opção de menu agora é **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="f3cc5-154">O **painel de detalhes mostra a data de atualização mais recente**: a caixa de diálogo NuGet exibe a data da última atualização no painel de detalhes de um pacote quando a guia **online** ou **atualizações** está selecionada.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="f3cc5-155">**Lista de marcas exibidas**: a caixa de diálogo NuGet exibe marcas.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="f3cc5-156">Aprimoramentos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3cc5-156">Powershell Improvements</span></span>
* <span data-ttu-id="f3cc5-157">**Scripts do PowerShell assinados**: o NuGet inclui scripts do PowerShell assinados que habilitam o uso em ambientes mais restritivos.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="f3cc5-158">**Solicitando suporte**: o console do Gerenciador de pacotes agora dá suporte à solicitação por meio dos comandos `$host.ui.Prompt` e `$host.ui.PromptForChoice`.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="f3cc5-159">**Nomes de origem de pacote**: o fornecimento do nome de uma origem de pacote tem suporte ao especificar uma origem de pacote usando o sinalizador `-Source`.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="f3cc5-160">aprimoramentos na linha de comando do NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="f3cc5-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="f3cc5-161">**Comandos personalizados do NuGet**: o NuGet. exe é extensível por meio de comandos personalizados usando o MEF.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="f3cc5-162">**Mais simples o fluxo de trabalho para a criação de pacotes de símbolo**: o sinalizador `-Symbols` pode ser aplicado a uma estrutura de pastas baseada em Convenção normal criando um pacote de símbolos, incluindo apenas os arquivos de origem e de `.pdb` dentro da pasta.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="f3cc5-163">**Especificando várias fontes**: o comando `NuGet install` dá suporte à especificação de várias fontes usando ponto e vírgula como um delimitador ou especificando `-Source` várias vezes.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="f3cc5-164">**Suporte à autenticação de proxy**: o NuGet 1,4 adiciona suporte para solicitar credenciais de usuário ao usar o NuGet por trás de um proxy que requer autenticação.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="f3cc5-165">**alteração significativa na atualização do NuGet. exe**: o sinalizador `-Self` agora é necessário para que o NuGet. exe se atualize.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="f3cc5-166">`nuget.exe Update` agora usa um caminho para o arquivo de `packages.config` e tentará atualizar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="f3cc5-167">Observe que essa atualização é limitada, pois não irá: \* \* atualizar, adicionar, remover conteúdo no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-167">Note that this update is limited in that it will not: \*\* Update, add, remove content in the project file.</span></span>
<span data-ttu-id="f3cc5-168">\* \* Executar scripts do PowerShell dentro do pacote.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-168">\*\* Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="f3cc5-169">Suporte do servidor NuGet para enviar pacotes por push usando NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="f3cc5-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="f3cc5-170">O NuGet inclui uma maneira simples de hospedar um [repositório NuGet baseado na Web leve](../hosting-packages/nuget-server.md) por meio do pacote NuGet `NuGet.Server`.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="f3cc5-171">Com o NuGet 1,4, o servidor leve dá suporte ao envio e exclusão de pacotes usando NuGet. exe.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="f3cc5-172">A versão mais recente do `NuGet.Server` adiciona um novo `appSetting`, chamado `apiKey`.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="f3cc5-173">Quando a chave é omitida ou deixada em branco, o envio de pacotes para o feed é desabilitado.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="f3cc5-174">Definir o apiKey como um valor (idealmente uma senha forte) permite enviar pacotes por push usando NuGet. exe.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="f3cc5-175">Suporte para ferramentas do Windows Phone Mango Edition</span><span class="sxs-lookup"><span data-stu-id="f3cc5-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="f3cc5-176">Agora, o NuGet tem suporte na versão Release Candidate do Windows Phone Tools para Mango.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="f3cc5-177">Atualmente, as ferramentas de Windows Phone não têm suporte para o Gerenciador de extensões do Visual Studio, portanto, para instalar o NuGet para ferramentas de Windows Phone, talvez seja necessário baixar e executar o VSIX manualmente.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="f3cc5-178">Para desinstalar o NuGet para ferramentas de Windows Phone, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="f3cc5-179">Correções de bugs</span><span class="sxs-lookup"><span data-stu-id="f3cc5-179">Bug Fixes</span></span>
<span data-ttu-id="f3cc5-180">O NuGet 1,4 tinha um total de 88 itens de trabalho corrigidos.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="f3cc5-181">71 deles foram marcados como bugs.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="f3cc5-182">Para obter uma lista completa de itens de trabalho corrigidos no NuGet 1,4, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="f3cc5-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="f3cc5-183">Correções de bugs vale a pena observar:</span><span class="sxs-lookup"><span data-stu-id="f3cc5-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="f3cc5-184">[Problema 603](http://nuget.codeplex.com/workitem/603): as dependências de pacote em diferentes repositórios são resolvidas corretamente ao especificar uma origem de pacote específica.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="f3cc5-185">[Problema 1036](http://nuget.codeplex.com/workitem/1036): a adição de `NuGet Pack SomeProject.csproj` ao evento de pós-compilação não causa mais um loop infinito.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="f3cc5-186">[Problema 961](http://nuget.codeplex.com/workitem/961): `-Source` sinalizador dá suporte a caminhos relativos.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="f3cc5-187">Atualização do NuGet 1,4</span><span class="sxs-lookup"><span data-stu-id="f3cc5-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="f3cc5-188">Logo após o lançamento do NuGet 1,4, encontramos alguns problemas que eram importantes para corrigir.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="f3cc5-189">O número de versão específico desta atualização para 1,4 é 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="f3cc5-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="f3cc5-190">Correções de bugs</span><span class="sxs-lookup"><span data-stu-id="f3cc5-190">Bug Fixes</span></span>
* <span data-ttu-id="f3cc5-191">[Problema 1220](http://nuget.codeplex.com/workitem/1220): Update-Package não executa `install.ps1`/`uninstall.ps1` em todos os projetos quando há mais de um projeto</span><span class="sxs-lookup"><span data-stu-id="f3cc5-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="f3cc5-192">[Problema 1156](http://nuget.codeplex.com/workitem/1156): o Gerenciador de pacotes console paralisado no W2K3/XP (quando o PowerShell 2 não está instalado)</span><span class="sxs-lookup"><span data-stu-id="f3cc5-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
