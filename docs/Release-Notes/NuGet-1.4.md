---
title: Notas de versão do NuGet 1.4 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Notas de versão do NuGet 1.4 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs.
keywords: Notas de versão 1.4 do NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 1229cd7fddb826902478b69cfdbc16a8ed192b64
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="09f87-104">Notas de versão 1.4 do NuGet</span><span class="sxs-lookup"><span data-stu-id="09f87-104">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="09f87-105">[Notas de versão do NuGet 1.3](../release-notes/nuget-1.3.md) | [notas de versão do NuGet 1.5](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="09f87-105">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="09f87-106">NuGet 1.4 foi lançado em 17 de junho de 2011.</span><span class="sxs-lookup"><span data-stu-id="09f87-106">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="09f87-107">Recursos</span><span class="sxs-lookup"><span data-stu-id="09f87-107">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="09f87-108">Aprimoramentos do pacote de atualização</span><span class="sxs-lookup"><span data-stu-id="09f87-108">Update-Package improvements</span></span>
<span data-ttu-id="09f87-109">NuGet 1.4 apresenta muitos aprimoramentos para o comando de pacote de atualização, tornando mais fácil de manter os pacotes a mesma versão de vários projetos em uma solução.</span><span class="sxs-lookup"><span data-stu-id="09f87-109">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="09f87-110">Por exemplo, ao atualizar um pacote para a versão mais recente, é muito comum que deseja que todos os projetos com esse pacote instalado para ser atualizado para o mesmo verision.</span><span class="sxs-lookup"><span data-stu-id="09f87-110">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="09f87-111">O `Update-Package` comando agora torna mais fácil:</span><span class="sxs-lookup"><span data-stu-id="09f87-111">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="09f87-112">Atualizar todos os pacotes em um único projeto</span><span class="sxs-lookup"><span data-stu-id="09f87-112">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="09f87-113">Atualizar um pacote em todos os projetos</span><span class="sxs-lookup"><span data-stu-id="09f87-113">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="09f87-114">Atualizar todos os pacotes em todos os projetos</span><span class="sxs-lookup"><span data-stu-id="09f87-114">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="09f87-115">Executar uma atualização "segura" de todos os pacotes</span><span class="sxs-lookup"><span data-stu-id="09f87-115">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="09f87-116">O `-Safe` sinalizador restringe as atualizações para versões somente com o mesmo componente de versão principal e secundária.</span><span class="sxs-lookup"><span data-stu-id="09f87-116">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="09f87-117">Por exemplo, se a versão 1.0.0 de um pacote estiver instalada e as versões 1.0.1, 1.0.2 e 1.1 estão disponíveis no feed, o `-Safe` sinalizador atualiza o pacote para 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="09f87-117">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="09f87-118">Atualizar sem a `-Safe` sinalizador deve atualizar o pacote para a versão mais recente, 1.1.</span><span class="sxs-lookup"><span data-stu-id="09f87-118">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="09f87-119">Gerenciando pacotes no nível da solução</span><span class="sxs-lookup"><span data-stu-id="09f87-119">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="09f87-120">Antes do NuGet 1.4, instalar um pacote em vários projetos era difícil de usar a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="09f87-120">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="09f87-121">Ele necessário iniciar a caixa de diálogo, uma vez por projeto.</span><span class="sxs-lookup"><span data-stu-id="09f87-121">It required launching the dialog once per project.</span></span>

<span data-ttu-id="09f87-122">1.4 NuGet adiciona suporte para instalar/desinstalar/atualizar pacotes em vários projetos ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="09f87-122">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="09f87-123">Basta iniciar o clique direito a solução e selecionando o **gerenciar pacotes NuGet** opção de menu.</span><span class="sxs-lookup"><span data-stu-id="09f87-123">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Caixa de diálogo solução nível gerenciar pacotes do NuGet](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="09f87-125">Observe que, na barra de título da caixa de diálogo, o nome da solução é exibido, não o nome de um projeto.</span><span class="sxs-lookup"><span data-stu-id="09f87-125">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="09f87-126">Operações de pacote agora fornecem uma lista de caixas de seleção com a lista de projetos, a que a operação deve aplicar.</span><span class="sxs-lookup"><span data-stu-id="09f87-126">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Gerenciar a seleção de projeto de pacotes do NuGet](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="09f87-128">Para obter mais detalhes, consulte o tópico sobre [pacotes de gerenciamento para a solução](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="09f87-128">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="09f87-129">Restringir atualiza permitido versões</span><span class="sxs-lookup"><span data-stu-id="09f87-129">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="09f87-130">Por padrão, ao executar o `Update-Package` comando em um pacote (ou a atualização do pacote usando a caixa de diálogo), ele será atualizado para a versão mais recente no feed.</span><span class="sxs-lookup"><span data-stu-id="09f87-130">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="09f87-131">Com o novo suporte para todos os pacotes de atualização, pode haver casos em que você deseja bloquear a um intervalo de versão específica de um pacote.</span><span class="sxs-lookup"><span data-stu-id="09f87-131">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="09f87-132">Por exemplo, você pode saber com antecedência que seu aplicativo funcionará apenas com 2.\* de versão de um pacote, mas não 3.0 e posterior.</span><span class="sxs-lookup"><span data-stu-id="09f87-132">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="09f87-133">Para evitar acidentalmente a atualização do pacote como 3, o NuGet 1.4 adiciona suporte para restringir o intervalo de versões pacotes podem ser atualizados para editando manualmente a `packages.config` arquivo usando o novo `allowedVersions` atributo.</span><span class="sxs-lookup"><span data-stu-id="09f87-133">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="09f87-134">Por exemplo, o exemplo a seguir mostra como bloquear o `SomePackage` pacote da versão 2.0-3.0 (exclusivo) de intervalo.</span><span class="sxs-lookup"><span data-stu-id="09f87-134">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="09f87-135">O `allowedVersions` atributo aceita valores usando o [formato de versão do intervalo](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="09f87-135">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="09f87-136">Observe que na 1.4, um pacote a um intervalo de versão específica de bloqueio deve ser editados manualmente.</span><span class="sxs-lookup"><span data-stu-id="09f87-136">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="09f87-137">1.5 NuGet estamos planejando adicionar suporte para colocar esse intervalo por meio de `Install-Package` comando.</span><span class="sxs-lookup"><span data-stu-id="09f87-137">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="09f87-138">Visualizador de pacote</span><span class="sxs-lookup"><span data-stu-id="09f87-138">Package Visualizer</span></span>
<span data-ttu-id="09f87-139">O novo Visualizador de pacote, iniciado por meio de **ferramentas** -> **Gerenciador de biblioteca de pacote** -> **pacote visualizador** opção de menu, permite que você visualize facilmente todos os projetos e suas dependências do pacote dentro de uma solução.</span><span class="sxs-lookup"><span data-stu-id="09f87-139">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="09f87-140">_**Observação importante:** esse recurso aproveita o suporte DGML no Visual Studio. Criando a visualização só tem suporte no Visual Studio Ultimate. Exibir um diagrama DGML só tem suporte no Visual Studio Premium ou superior._</span><span class="sxs-lookup"><span data-stu-id="09f87-140">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Visualizador de pacote](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="09f87-142">Verificação de atualização automática para a caixa de diálogo do NuGet</span><span class="sxs-lookup"><span data-stu-id="09f87-142">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="09f87-143">Algumas versões do NuGet introduzem novos recursos expressados por meio de `.nuspec` arquivo que não são compreendidos por versões mais antigas da caixa de diálogo do NuGet.</span><span class="sxs-lookup"><span data-stu-id="09f87-143">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="09f87-144">Um exemplo é o lançamento em NuGet 1.4 para [especificando assemblies do framework](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="09f87-144">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="09f87-145">Por isso, é importante usar a versão mais recente do NuGet para garantir que você pode usar pacotes que aproveitam os recursos mais recentes.</span><span class="sxs-lookup"><span data-stu-id="09f87-145">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="09f87-146">Para fazer atualizações NuGet mais visível, a caixa de diálogo do NuGet contém a lógica para realçar quando uma versão mais recente está disponível.</span><span class="sxs-lookup"><span data-stu-id="09f87-146">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="09f87-147">_**Observação**: A verificação é feita apenas se o **Online** guia foi selecionada na sessão atual._</span><span class="sxs-lookup"><span data-stu-id="09f87-147">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Gerenciar pacotes NuGet a caixa de diálogo com a nova versão disponível](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="09f87-149">Para desativar a verificação automática de atualizações, vá para a caixa de diálogo de configurações do NuGet e desmarque **verificar automaticamente se há atualizações**.</span><span class="sxs-lookup"><span data-stu-id="09f87-149">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![Configurações do NuGet](./media/nuget-settings.png)

<span data-ttu-id="09f87-151">Esse recurso, na verdade, foi adicionado no NuGet 1.3, mas não será visível, é claro que, até que uma atualização 1.3, como NuGet 1.4, foi disponibilizado.</span><span class="sxs-lookup"><span data-stu-id="09f87-151">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="09f87-152">Aprimoramentos do diálogo de Gerenciador de pacotes</span><span class="sxs-lookup"><span data-stu-id="09f87-152">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="09f87-153">**Nomes de menu aprimorado**: opções de Menu para iniciar a caixa de diálogo foram renomeado para maior clareza.</span><span class="sxs-lookup"><span data-stu-id="09f87-153">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="09f87-154">A opção de menu é agora **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="09f87-154">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="09f87-155">**Painel de detalhes mostra a data de atualização mais recente**: caixa de diálogo o NuGet exibe a data da última atualização no painel de detalhes de um pacote quando o **Online** ou **atualiza** guia é selecionada.</span><span class="sxs-lookup"><span data-stu-id="09f87-155">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="09f87-156">**Lista de marcas exibidas**: caixa de diálogo o Nuget exibe marcas.</span><span class="sxs-lookup"><span data-stu-id="09f87-156">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="09f87-157">Melhorias do PowerShell</span><span class="sxs-lookup"><span data-stu-id="09f87-157">Powershell Improvements</span></span>
* <span data-ttu-id="09f87-158">**Scripts do PowerShell assinados**: NuGet inclui scripts assinados do Powershell habilitando o uso em ambientes mais restritivos.</span><span class="sxs-lookup"><span data-stu-id="09f87-158">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="09f87-159">**Solicitando suporte**: O Package Manager Console agora dá suporte ao solicitar por meio de `$host.ui.Prompt` e `$host.ui.PromptForChoice` comandos.</span><span class="sxs-lookup"><span data-stu-id="09f87-159">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="09f87-160">**Nomes de origem do pacote**: o nome de uma origem do pacote é suportado ao especificar uma origem de pacote usando o `-Source` sinalizador.</span><span class="sxs-lookup"><span data-stu-id="09f87-160">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="09f87-161">aprimoramentos de linha de comando NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="09f87-161">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="09f87-162">**Comandos personalizados NuGet**: nuget.exe é extensível via comandos personalizados usando MEF.</span><span class="sxs-lookup"><span data-stu-id="09f87-162">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="09f87-163">**Mais simples de fluxo de trabalho para a criação de pacotes de símbolos**: O `-Symbols` sinalizador pode ser aplicado a uma estrutura de pastas de convenção normal com base em criar um pacote de símbolos, incluindo apenas o código-fonte e `.pdb` arquivos dentro da pasta.</span><span class="sxs-lookup"><span data-stu-id="09f87-163">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="09f87-164">**Especificar várias fontes**: O `NuGet install` comando oferece suporte à especificação de várias fontes com ponto e vírgula como delimitador ou especificando `-Source` várias vezes.</span><span class="sxs-lookup"><span data-stu-id="09f87-164">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="09f87-165">**Suporte de autenticação de proxy**: NuGet 1.4 adiciona suporte para solicitar as credenciais do usuário ao usar o NuGet atrás de um proxy que requer autenticação.</span><span class="sxs-lookup"><span data-stu-id="09f87-165">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="09f87-166">**NuGet.exe atualizar alterações recentes**: O `-Self` sinalizador agora é necessário para nuget.exe atualize a mesmo.</span><span class="sxs-lookup"><span data-stu-id="09f87-166">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="09f87-167">`nuget.exe Update` agora entra em um caminho para o `packages.config` de arquivo e tentará atualizar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="09f87-167">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="09f87-168">Observe que essa atualização é limitada em que ele não será: * * atualizar, adicionar, remover o conteúdo no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="09f87-168">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="09f87-169">* * Execute scripts do Powershell dentro do pacote.</span><span class="sxs-lookup"><span data-stu-id="09f87-169">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="09f87-170">Suporte do servidor do NuGet para enviar pacotes usando nuget.exe</span><span class="sxs-lookup"><span data-stu-id="09f87-170">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="09f87-171">NuGet inclui uma maneira simples de host um [da web com base em repositório do NuGet](../hosting-packages/nuget-server.md) por meio de `NuGet.Server` pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="09f87-171">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="09f87-172">Com o NuGet 1.4, com suporte no servidor leve Push e excluir pacotes usando nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="09f87-172">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="09f87-173">A versão mais recente do `NuGet.Server` adiciona um novo `appSetting`, denominado `apiKey`.</span><span class="sxs-lookup"><span data-stu-id="09f87-173">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="09f87-174">Quando a chave for omitida ou deixada em branco, o envio de pacotes para o feed está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="09f87-174">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="09f87-175">Definir o apiKey para um valor (o ideal é uma senha forte) permite que o envio de pacotes usando nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="09f87-175">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="09f87-176">Suporte para edição de manga de ferramentas do Windows Phone</span><span class="sxs-lookup"><span data-stu-id="09f87-176">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="09f87-177">NuGet agora há suporte para a versão release candidate das ferramentas do Windows Phone para Mango.</span><span class="sxs-lookup"><span data-stu-id="09f87-177">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="09f87-178">Atualmente, ferramentas do Windows Phone não tem suporte para o Gerenciador de extensão do Visual Studio, portanto instalar o NuGet para ferramentas do Windows Phone, você precisará baixar e executar o VSIX manualmente.</span><span class="sxs-lookup"><span data-stu-id="09f87-178">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="09f87-179">Para desinstalar o NuGet para ferramentas do Windows Phone, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="09f87-179">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="09f87-180">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="09f87-180">Bug Fixes</span></span>
<span data-ttu-id="09f87-181">NuGet 1.4 tinha um total de 88 fixos de itens de trabalho.</span><span class="sxs-lookup"><span data-stu-id="09f87-181">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="09f87-182">71 deles foram marcadas como bugs.</span><span class="sxs-lookup"><span data-stu-id="09f87-182">71 of those were marked as bugs.</span></span>

<span data-ttu-id="09f87-183">Para obter uma lista completa de trabalho itens corrigidos no NuGet 1.4, por favor, exibição de [NuGet Issue Tracker para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="09f87-183">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="09f87-184">Correções de bug, vale a pena observar:</span><span class="sxs-lookup"><span data-stu-id="09f87-184">Bug fixes worth noting:</span></span>

* <span data-ttu-id="09f87-185">[Problema 603](http://nuget.codeplex.com/workitem/603): dependências de pacote em repositórios diferentes resolve corretamente ao especificar uma origem de pacote específico.</span><span class="sxs-lookup"><span data-stu-id="09f87-185">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="09f87-186">[Problema 1036](http://nuget.codeplex.com/workitem/1036): adicionando `NuGet Pack SomeProject.csproj` como evento pós-compilação não faz com que um loop infinito.</span><span class="sxs-lookup"><span data-stu-id="09f87-186">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="09f87-187">[Problema 961](http://nuget.codeplex.com/workitem/961): `-Source` sinalizador dá suporte a caminhos relativos.</span><span class="sxs-lookup"><span data-stu-id="09f87-187">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="09f87-188">Atualização do NuGet 1.4</span><span class="sxs-lookup"><span data-stu-id="09f87-188">NuGet 1.4 Update</span></span>
<span data-ttu-id="09f87-189">Logo após o lançamento do NuGet 1.4, descobrimos que alguns dos problemas que foram importante para corrigir.</span><span class="sxs-lookup"><span data-stu-id="09f87-189">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="09f87-190">O número de versão específico dessa atualização para 1.4 é 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="09f87-190">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="09f87-191">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="09f87-191">Bug Fixes</span></span>
* <span data-ttu-id="09f87-192">[Problema 1220](http://nuget.codeplex.com/workitem/1220): pacote de atualização não executa `install.ps1` / `uninstall.ps1` em todos os projetos quando há mais de um projeto</span><span class="sxs-lookup"><span data-stu-id="09f87-192">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="09f87-193">[Problema 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Console presa no W2K3/XP (quando 2 do Powershell não está instalado)</span><span class="sxs-lookup"><span data-stu-id="09f87-193">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
