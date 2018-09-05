---
title: Notas de versão 1.4 do NuGet
description: Notas de versão do NuGet 1.4, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f4d712f83ea108a82a1bc4910c2a721a8c24d51
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550625"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="53969-103">Notas de versão 1.4 do NuGet</span><span class="sxs-lookup"><span data-stu-id="53969-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="53969-104">[Notas de versão do NuGet 1.3](../release-notes/nuget-1.3.md) | [notas de versão do NuGet 1.5](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="53969-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="53969-105">O NuGet 1.4 foi lançado em 17 de junho de 2011.</span><span class="sxs-lookup"><span data-stu-id="53969-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="53969-106">Recursos</span><span class="sxs-lookup"><span data-stu-id="53969-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="53969-107">Aprimoramentos do pacote de atualização</span><span class="sxs-lookup"><span data-stu-id="53969-107">Update-Package improvements</span></span>
<span data-ttu-id="53969-108">O NuGet 1.4 apresenta muitos aprimoramentos ao comando Update-Package, tornando mais fácil de manter os pacotes na mesma versão de vários projetos em uma solução.</span><span class="sxs-lookup"><span data-stu-id="53969-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="53969-109">Por exemplo, ao atualizar um pacote para a versão mais recente, é muito comum que deseja que todos os projetos com que o pacote instalado para ser atualizado para o mesmo verision.</span><span class="sxs-lookup"><span data-stu-id="53969-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="53969-110">O `Update-Package` comando agora torna mais fácil:</span><span class="sxs-lookup"><span data-stu-id="53969-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="53969-111">Atualizar todos os pacotes em um único projeto</span><span class="sxs-lookup"><span data-stu-id="53969-111">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="53969-112">Atualizar um pacote em todos os projetos</span><span class="sxs-lookup"><span data-stu-id="53969-112">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="53969-113">Atualizar todos os pacotes em todos os projetos</span><span class="sxs-lookup"><span data-stu-id="53969-113">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="53969-114">Executar uma atualização "segura" de todos os pacotes</span><span class="sxs-lookup"><span data-stu-id="53969-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="53969-115">O `-Safe` sinalizador restringe atualizações para versões somente com o mesmo componente de versão principal e secundária.</span><span class="sxs-lookup"><span data-stu-id="53969-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="53969-116">Por exemplo, se versão 1.0.0 de um pacote é instalado, e as versões 1.0.1, 1.0.2 e 1.1 estiverem disponíveis no feed, o `-Safe` sinalizador atualiza o pacote à 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="53969-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="53969-117">Atualizar sem a `-Safe` sinalizador seria atualize o pacote para a versão mais recente, 1.1.</span><span class="sxs-lookup"><span data-stu-id="53969-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="53969-118">Gerenciamento de pacotes no nível da solução</span><span class="sxs-lookup"><span data-stu-id="53969-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="53969-119">Antes do NuGet 1.4, era complicado usando a caixa de diálogo instalar um pacote em vários projetos.</span><span class="sxs-lookup"><span data-stu-id="53969-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="53969-120">Ele necessário iniciar a caixa de diálogo, uma vez por projeto.</span><span class="sxs-lookup"><span data-stu-id="53969-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="53969-121">O NuGet 1.4 adiciona suporte para instalar/desinstalar/atualização de pacotes em vários projetos ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="53969-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="53969-122">Basta iniciar o clique direito a solução e selecionando o **gerenciar pacotes NuGet** opção de menu.</span><span class="sxs-lookup"><span data-stu-id="53969-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Caixa de diálogo de nível Manage NuGet Packages de solução](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="53969-124">Observe que, na barra de título da caixa de diálogo, o nome da solução é exibido, não o nome de um projeto.</span><span class="sxs-lookup"><span data-stu-id="53969-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="53969-125">Operações de pacote agora fornecem uma lista de caixas de seleção com a lista de projetos, a que a operação deve ser aplicada.</span><span class="sxs-lookup"><span data-stu-id="53969-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Gerenciar a seleção de projeto de pacotes do NuGet](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="53969-127">Para obter mais detalhes, consulte o tópico sobre [pacotes de gerenciamento para a solução](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="53969-127">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="53969-128">Restringindo é atualizado para versões de permissão</span><span class="sxs-lookup"><span data-stu-id="53969-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="53969-129">Por padrão, ao executar o `Update-Package` comando em um pacote (ou atualizando o pacote usando a caixa de diálogo), ele será atualizado para a versão mais recente no feed.</span><span class="sxs-lookup"><span data-stu-id="53969-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="53969-130">Com o novo suporte para todos os pacotes de atualização, pode haver casos em que você deseja bloquear a um intervalo de versão específica de um pacote.</span><span class="sxs-lookup"><span data-stu-id="53969-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="53969-131">Por exemplo, você pode saber com antecedência que seu aplicativo só funcionará com a versão 2. \* de um pacote, mas não 3.0 e superior.</span><span class="sxs-lookup"><span data-stu-id="53969-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="53969-132">Para evitar que acidentalmente a atualização do pacote para 3, o NuGet 1.4 adiciona suporte para restringir o intervalo de versões de pacotes podem ser atualizados para editando manualmente o `packages.config` do arquivo usando o novo `allowedVersions` atributo.</span><span class="sxs-lookup"><span data-stu-id="53969-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="53969-133">Por exemplo, o exemplo a seguir mostra como bloquear o `SomePackage` pacote da versão 2.0-3.0 (exclusivo) de intervalo.</span><span class="sxs-lookup"><span data-stu-id="53969-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="53969-134">O `allowedVersions` atributo aceita valores usando o [formato de intervalo de versão](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="53969-134">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="53969-135">Observe que no 1.4, bloqueio de um pacote para um intervalo de versão específico deve ser editado manualmente.</span><span class="sxs-lookup"><span data-stu-id="53969-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="53969-136">No NuGet 1.5 estamos planejando adicionar suporte para o posicionamento desse intervalo por meio de `Install-Package` comando.</span><span class="sxs-lookup"><span data-stu-id="53969-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="53969-137">Visualizador de pacote</span><span class="sxs-lookup"><span data-stu-id="53969-137">Package Visualizer</span></span>
<span data-ttu-id="53969-138">O novo Visualizador de pacote, iniciado por meio de **ferramentas** -> **Library Package Manager** -> **pacote visualizador** opção de menu permite que você visualize facilmente a todos os projetos e suas dependências de pacote em uma solução.</span><span class="sxs-lookup"><span data-stu-id="53969-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="53969-139">_**Observação importante:** esse recurso se beneficia do suporte DGML no Visual Studio. Criar a visualização só tem suporte no Visual Studio Ultimate. Exibir um diagrama DGML só tem suporte no Visual Studio Premium ou superior._</span><span class="sxs-lookup"><span data-stu-id="53969-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Visualizador de pacote](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="53969-141">Verificação de atualização automática para a caixa de diálogo do NuGet</span><span class="sxs-lookup"><span data-stu-id="53969-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="53969-142">Algumas versões do NuGet introduzem novos recursos expressados por meio de `.nuspec` arquivo que não são compreendidas por versões mais antigas da caixa de diálogo do NuGet.</span><span class="sxs-lookup"><span data-stu-id="53969-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="53969-143">Um exemplo é a introdução em NuGet 1.4 para [especificando os assemblies do framework](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="53969-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="53969-144">Por isso, é importante usar a versão mais recente do NuGet para garantir que você pode usar pacotes aproveitando os recursos mais recentes.</span><span class="sxs-lookup"><span data-stu-id="53969-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="53969-145">Para fazer atualizações para o NuGet mais visível, a caixa de diálogo do NuGet contém a lógica para realçar quando uma versão mais recente está disponível.</span><span class="sxs-lookup"><span data-stu-id="53969-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="53969-146">_**Observação**: A verificação é feita apenas se o **Online** guia foi selecionada na sessão atual._</span><span class="sxs-lookup"><span data-stu-id="53969-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Gerenciar a caixa de diálogo de pacotes do NuGet com a nova versão disponível](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="53969-148">Para desativar a verificação automática de atualizações, vá para a caixa de diálogo de configurações do NuGet e desmarque a opção **verifique automaticamente atualizações**.</span><span class="sxs-lookup"><span data-stu-id="53969-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![Configurações do NuGet](./media/nuget-settings.png)

<span data-ttu-id="53969-150">Esse recurso, na verdade, foi adicionado na versão 1.3 do NuGet, mas não será visível, é claro que, até que uma atualização para 1.3, como o NuGet 1.4, foi disponibilizado.</span><span class="sxs-lookup"><span data-stu-id="53969-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="53969-151">Aprimoramentos do diálogo do Gerenciador de pacotes</span><span class="sxs-lookup"><span data-stu-id="53969-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="53969-152">**Nomes de menu aprimorado**: opções de Menu para iniciar a caixa de diálogo foram renomeadas para maior clareza.</span><span class="sxs-lookup"><span data-stu-id="53969-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="53969-153">A opção de menu é agora **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="53969-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="53969-154">**Painel de detalhes mostra a data de atualização mais recente**: caixa de diálogo o NuGet exibe a data da atualização mais recente no painel de detalhes para um pacote quando o **Online** ou **atualiza** guia é selecionada.</span><span class="sxs-lookup"><span data-stu-id="53969-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="53969-155">**Lista de marcas exibido**: caixa de diálogo o Nuget exibe marcas.</span><span class="sxs-lookup"><span data-stu-id="53969-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="53969-156">Melhorias do PowerShell</span><span class="sxs-lookup"><span data-stu-id="53969-156">Powershell Improvements</span></span>
* <span data-ttu-id="53969-157">**Scripts do PowerShell assinados**: NuGet inclui scripts assinados do Powershell, permitindo o uso em ambientes mais restritivas.</span><span class="sxs-lookup"><span data-stu-id="53969-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="53969-158">**Solicitar suporte**: O Package Manager Console agora dá suporte a solicitar por meio de `$host.ui.Prompt` e `$host.ui.PromptForChoice` comandos.</span><span class="sxs-lookup"><span data-stu-id="53969-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="53969-159">**Nomes de origem do pacote**: o nome de uma origem de pacote é suportado ao especificar uma origem de pacote usando o `-Source` sinalizador.</span><span class="sxs-lookup"><span data-stu-id="53969-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="53969-160">aprimoramentos de linha de comando NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="53969-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="53969-161">**Comandos do NuGet personalizado**: nuget.exe é extensível por meio de comandos personalizados usando o MEF.</span><span class="sxs-lookup"><span data-stu-id="53969-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="53969-162">**Mais simples do fluxo de trabalho para a criação de pacotes de símbolos**: O `-Symbols` sinalizador pode ser aplicado a uma estrutura de pastas de convenção normal com base em criação de um pacote de símbolos, incluindo apenas o código-fonte e `.pdb` arquivos dentro da pasta.</span><span class="sxs-lookup"><span data-stu-id="53969-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="53969-163">**Especificar várias fontes**: O `NuGet install` comando dá suporte à especificação de várias fontes usando ponto e vírgula como delimitador ou especificando `-Source` várias vezes.</span><span class="sxs-lookup"><span data-stu-id="53969-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="53969-164">**Suporte de autenticação de proxy**: NuGet 1.4 adiciona suporte para solicitar as credenciais do usuário ao usar o NuGet atrás de um proxy que exija autenticação.</span><span class="sxs-lookup"><span data-stu-id="53969-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="53969-165">**NuGet.exe atualizar alteração significativa**: O `-Self` sinalizador agora é necessário para nuget.exe atualize a mesmo.</span><span class="sxs-lookup"><span data-stu-id="53969-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="53969-166">`nuget.exe Update` agora entra em um caminho para o `packages.config` de arquivo e tentará atualizar pacotes.</span><span class="sxs-lookup"><span data-stu-id="53969-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="53969-167">Observe que essa atualização é limitada em que ele não será: * * atualizar, adicionar, remover o conteúdo no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="53969-167">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="53969-168">* * Executar scripts do Powershell dentro do pacote.</span><span class="sxs-lookup"><span data-stu-id="53969-168">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="53969-169">Suporte de servidor do NuGet para enviar por push pacotes usando nuget.exe</span><span class="sxs-lookup"><span data-stu-id="53969-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="53969-170">NuGet inclui uma maneira simples de host uma [web leve com base em repositório NuGet](../hosting-packages/nuget-server.md) por meio de `NuGet.Server` pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="53969-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="53969-171">Com o NuGet 1.4, o servidor leve dá suporte a envio por push e excluir pacotes usando nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="53969-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="53969-172">A versão mais recente do `NuGet.Server` adiciona um novo `appSetting`, denominado `apiKey`.</span><span class="sxs-lookup"><span data-stu-id="53969-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="53969-173">Quando a chave for omitida ou deixada em branco, o push de pacotes para o feed está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="53969-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="53969-174">Configurar o apiKey para um valor (o ideal é que uma senha forte) permite enviar por push pacotes usando nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="53969-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="53969-175">Suporte para Windows Phone ferramentas Mango Edition</span><span class="sxs-lookup"><span data-stu-id="53969-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="53969-176">A versão release candidate das ferramentas do Windows Phone para Mango agora tem suporte ao NuGet.</span><span class="sxs-lookup"><span data-stu-id="53969-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="53969-177">Atualmente, as ferramentas do Windows Phone não tem suporte para o Gerenciador de extensão do Visual Studio, então instalar o NuGet para ferramentas do Windows Phone, talvez você precise baixar e executar o VSIX manualmente.</span><span class="sxs-lookup"><span data-stu-id="53969-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="53969-178">Para desinstalar o NuGet para ferramentas do Windows Phone, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="53969-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="53969-179">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="53969-179">Bug Fixes</span></span>
<span data-ttu-id="53969-180">O NuGet 1.4 tinha um total de 88 fixos de itens de trabalho.</span><span class="sxs-lookup"><span data-stu-id="53969-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="53969-181">71 deles foram marcados como bugs.</span><span class="sxs-lookup"><span data-stu-id="53969-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="53969-182">Para obter uma lista completa de trabalho itens corrigidos no NuGet 1.4, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="53969-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="53969-183">Correções de bug, vale a pena observar:</span><span class="sxs-lookup"><span data-stu-id="53969-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="53969-184">[Problema 603](http://nuget.codeplex.com/workitem/603): dependências de pacotes em diferentes repositórios resolve corretamente ao especificar uma origem de pacote específico.</span><span class="sxs-lookup"><span data-stu-id="53969-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="53969-185">[Problema 1036](http://nuget.codeplex.com/workitem/1036): adicionando `NuGet Pack SomeProject.csproj` como evento pós-compilação não faz com que um loop infinito.</span><span class="sxs-lookup"><span data-stu-id="53969-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="53969-186">[Problema 961](http://nuget.codeplex.com/workitem/961): `-Source` sinalizador dá suporte a caminhos relativos.</span><span class="sxs-lookup"><span data-stu-id="53969-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="53969-187">Atualização do NuGet 1.4</span><span class="sxs-lookup"><span data-stu-id="53969-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="53969-188">Logo após o lançamento do NuGet 1.4, descobrimos alguns problemas que foram importantes para corrigir.</span><span class="sxs-lookup"><span data-stu-id="53969-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="53969-189">O número de versão específico dessa atualização para 1.4 é 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="53969-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="53969-190">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="53969-190">Bug Fixes</span></span>
* <span data-ttu-id="53969-191">[Problema 1220](http://nuget.codeplex.com/workitem/1220): não executa o pacote de atualização `install.ps1` / `uninstall.ps1` em todos os projetos quando há mais de um projeto</span><span class="sxs-lookup"><span data-stu-id="53969-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="53969-192">[Problema 1156](http://nuget.codeplex.com/workitem/1156): console do Gerenciador de pacotes preso no W2K3/XP (quando 2 do Powershell não está instalado)</span><span class="sxs-lookup"><span data-stu-id="53969-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
