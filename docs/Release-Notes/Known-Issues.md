---
title: Problemas conhecidos do NuGet | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 42e7a619-1c69-454b-8243-16e2f9f950d0
description: "Problemas conhecidos com o NuGet, incluindo autenticação, instalação de pacote e ferramentas."
keywords: Problemas conhecidos do NuGet, problemas do NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ce145212da3830216e123f39257a6707712f88c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="known-issues-with-nuget"></a><span data-ttu-id="24fb5-104">Problemas conhecidos com o NuGet</span><span class="sxs-lookup"><span data-stu-id="24fb5-104">Known Issues with NuGet</span></span>

<span data-ttu-id="24fb5-105">Esses são os problemas comuns conhecidos do NuGet relatados com mais frequência.</span><span class="sxs-lookup"><span data-stu-id="24fb5-105">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="24fb5-106">Se você estiver tendo problemas para instalar o NuGet ou gerenciar pacotes, veja esses problemas conhecidos e suas soluções.</span><span class="sxs-lookup"><span data-stu-id="24fb5-106">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="24fb5-107">A partir do NuGet 4.0, problemas conhecidos fazem parte das respectivas notas de versão.</span><span class="sxs-lookup"><span data-stu-id="24fb5-107">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="24fb5-108">Problemas de autenticação com feeds do NuGet no VSTS com nuget.exe v3.4.3</span><span class="sxs-lookup"><span data-stu-id="24fb5-108">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="24fb5-109">**Problema:**</span><span class="sxs-lookup"><span data-stu-id="24fb5-109">**Problem:**</span></span>

<span data-ttu-id="24fb5-110">Quando usamos o comando a seguir para armazenar as credenciais, podemos acabar duplicando a criptografia do Token de Acesso Pessoal.</span><span class="sxs-lookup"><span data-stu-id="24fb5-110">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="24fb5-111">$PAT = "Seu token de acesso pessoal" $Feed = "Sua url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span><span class="sxs-lookup"><span data-stu-id="24fb5-111">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="24fb5-112">**Solução alternativa:**</span><span class="sxs-lookup"><span data-stu-id="24fb5-112">**Workaround:**</span></span>

<span data-ttu-id="24fb5-113">Armazenar senhas em texto não criptografado usando a opção [-StorePasswordInClearText](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="24fb5-113">Store passwords in clear text using the [-StorePasswordInClearText](../tools/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="24fb5-114">Erro ao instalar pacotes com o NuGet 3.4, 3.4.1</span><span class="sxs-lookup"><span data-stu-id="24fb5-114">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="24fb5-115">**Problema:**</span><span class="sxs-lookup"><span data-stu-id="24fb5-115">**Problem:**</span></span>

<span data-ttu-id="24fb5-116">No NuGet 3.4 e 3.4.1, ao usar o suplemento do NuGet, nenhuma origem é relatada como disponível e você não consegue adicionar novas origens na janela de configuração.</span><span class="sxs-lookup"><span data-stu-id="24fb5-116">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="24fb5-117">O resultado é semelhante à imagem abaixo:</span><span class="sxs-lookup"><span data-stu-id="24fb5-117">The result is similar to the image below:</span></span>

![Configuração do NuGet sem origens](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="24fb5-119">O arquivo `NuGet.Config` na sua pasta `%AppData%\NuGet\` foi acidentalmente esvaziado.</span><span class="sxs-lookup"><span data-stu-id="24fb5-119">The `NuGet.Config` file in your `%AppData%\NuGet\` folder has accidentally been emptied.</span></span> <span data-ttu-id="24fb5-120">Para corrigir isso: feche o Visual Studio 2015, exclua o arquivo `NuGet.Config` na pasta `%AppData%\NuGet\` e reinicie o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24fb5-120">To fix this: Close Visual Studio 2015, delete the `NuGet.Config` file in the `%AppData%\NuGet\` folder and restart Visual Studio.</span></span>  <span data-ttu-id="24fb5-121">Um novo arquivo `NuGet.Config` será gerado e você poderá continuar.</span><span class="sxs-lookup"><span data-stu-id="24fb5-121">A new `NuGet.Config` file will be generated and you will be able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="24fb5-122">Erro ao instalar pacotes com o NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="24fb5-122">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="24fb5-123">**Problema:**</span><span class="sxs-lookup"><span data-stu-id="24fb5-123">**Problem:**</span></span>

<span data-ttu-id="24fb5-124">No NuGet 2.7 ou superior, quando você tenta instalar qualquer pacote que contém as referências de assembly, receberá a mensagem de erro **“A cadeia de caracteres de entrada não estava no formato correto.”**, como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="24fb5-124">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

```ps
install-package log4net
    Installing 'log4net 2.0.0'.
    Successfully installed 'log4net 2.0.0'.
    Adding 'log4net 2.0.0' to Tyson.OperatorUpload.
    Install failed. Rolling back...
    install-package : Input string was not in a correct format.
    At line:1 char:1
        install-package log4net
        ~~~~~~~~~~~~~~~~~~~~~~~
        CategoryInfo : NotSpecified: (:) [Install-Package], FormatException
        FullyQualifiedErrorId : NuGetCmdletUnhandledException,NuGet.PowerShell.Commands.InstallPackageCommand
```


<span data-ttu-id="24fb5-125">Isso é causado pela biblioteca de tipos para o componente COM de `VSLangProj.dll` cujo registro está sendo cancelado no sistema.</span><span class="sxs-lookup"><span data-stu-id="24fb5-125">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="24fb5-126">Isso pode acontecer, por exemplo, quando você tem duas versões do Visual Studio instaladas lado a lado e desinstala a versão mais antiga.</span><span class="sxs-lookup"><span data-stu-id="24fb5-126">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="24fb5-127">Isso pode inadvertidamente cancelar o registro das biblioteca COM acima.</span><span class="sxs-lookup"><span data-stu-id="24fb5-127">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="24fb5-128">**Solução:**:</span><span class="sxs-lookup"><span data-stu-id="24fb5-128">**Solution:**:</span></span>

<span data-ttu-id="24fb5-129">Execute este comando de um **prompt com privilégios elevados** para registrar novamente a biblioteca de tipos para `VSLangProj.dll`</span><span class="sxs-lookup"><span data-stu-id="24fb5-129">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="24fb5-130">Se o comando falhar, verifique se o arquivo existe no local.</span><span class="sxs-lookup"><span data-stu-id="24fb5-130">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="24fb5-131">Para obter mais informações sobre esse erro, consulte [item de trabalho](https://nuget.codeplex.com/workitem/3609 "Item de trabalho 3609").</span><span class="sxs-lookup"><span data-stu-id="24fb5-131">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="24fb5-132">Falha de build após a atualização de pacote no VS 2012</span><span class="sxs-lookup"><span data-stu-id="24fb5-132">Build failure after package update in VS 2012</span></span>
<span data-ttu-id="24fb5-133">O problema: você está usando o VS 2012 RTM.</span><span class="sxs-lookup"><span data-stu-id="24fb5-133">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="24fb5-134">Ao atualizar pacotes do NuGet, você receberá esta mensagem: “não foi possível concluir a desinstalação de um ou mais pacotes”.</span><span class="sxs-lookup"><span data-stu-id="24fb5-134">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="24fb5-135">e é solicitado que você reinicie o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24fb5-135">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="24fb5-136">Após a reinicialização do VS, você receberá erros de build estranhos.</span><span class="sxs-lookup"><span data-stu-id="24fb5-136">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="24fb5-137">A causa é que certos arquivos dos pacotes antigo estão bloqueados por um processo do MSBuild em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="24fb5-137">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span>
<span data-ttu-id="24fb5-138">Mesmo depois de reiniciar o VS, o processo de MSBuild em segundo plano ainda usa os arquivos nos pacotes antigos, causando falhas de build.</span><span class="sxs-lookup"><span data-stu-id="24fb5-138">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="24fb5-139">A correção é instalar a Atualização do VS 2012, por exemplo, [VS 2012 Atualização 2](http://www.microsoft.com/download/details.aspx?id=38188).</span><span class="sxs-lookup"><span data-stu-id="24fb5-139">The fix is to install VS 2012 Update, e.g. [VS 2012 Update 2](http://www.microsoft.com/download/details.aspx?id=38188).</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="24fb5-140">Fazendo upgrade para o NuGet mais recente de uma versão mais antiga causa um erro de verificação de assinatura</span><span class="sxs-lookup"><span data-stu-id="24fb5-140">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="24fb5-141">Se você estiver executando o VS 2010 SP1, poderá encontrar a seguinte mensagem de erro ao tentar fazer upgrade no NuGet se tiver uma versão mais antiga instalada.</span><span class="sxs-lookup"><span data-stu-id="24fb5-141">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Instalador de Extensões do Visual Studio](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="24fb5-143">Ao exibir os logs, você poderá ver uma menção de um `SignatureMismatchException`.</span><span class="sxs-lookup"><span data-stu-id="24fb5-143">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="24fb5-144">Para evitar que isso ocorra, há um [hotfix do Visual Studio 2010 SP1](http://bit.ly/vsixcertfix) que você pode instalar.</span><span class="sxs-lookup"><span data-stu-id="24fb5-144">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="24fb5-145">Outra opção é usar a solução alternativa de simplesmente desinstalar o NuGet (enquanto o Visual Studio é executado como Administrador) e, em seguida, instalá-lo da Galeria de Extensões do VS.</span><span class="sxs-lookup"><span data-stu-id="24fb5-145">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="24fb5-146">Consulte [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="24fb5-146">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="24fb5-147">O Console do Gerenciador de Pacotes gera uma exceção quando o suplemento do Reflector Visual Studio também é instalado.</span><span class="sxs-lookup"><span data-stu-id="24fb5-147">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="24fb5-148">Ao executar o console do Gerenciador de Pacotes, você pode encontrar a seguinte mensagem de exceção se você tiver o suplemento do Reflector VS instalado.</span><span class="sxs-lookup"><span data-stu-id="24fb5-148">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="24fb5-149">ou</span><span class="sxs-lookup"><span data-stu-id="24fb5-149">or</span></span>

    System.Management.Automation.CmdletInvocationException: Could not load file or assembly 'Scripts\nuget.psm1' or one of its dependencies. <br />The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) ---&gt; System.IO.FileLoadException: Could not load file or <br />assembly 'Scripts\nuget.psm1' or one of its dependencies. The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) <br />---&gt; System.ArgumentException: Illegal characters in path.
       at System.IO.Path.CheckInvalidPathChars(String path)
       at System.IO.Path.Combine(String path1, String path2)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.<AssemblyPaths>d__1.MoveNext()
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.InnerResolveHandler(String name)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.ResolveHandler(Object sender, ResolveEventArgs args)
       at System.AppDomain.OnAssemblyResolveEvent(RuntimeAssembly assembly, String assemblyFullName)
       --- End of inner exception stack trace ---
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadBinaryModule(Boolean trySnapInName, String moduleName, String fileName, <br />Assembly assemblyToLoad, String moduleBase, SessionState ss, String prefix, Boolean loadTypes, Boolean loadFormats, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleNamedInManifest(String moduleName, String moduleBase, <br />Boolean searchModulePath, <br />String prefix, SessionState ss, Boolean loadTypesFiles, Boolean loadFormatFiles, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleManifest(ExternalScriptInfo scriptInfo, ManifestProcessingFlags <br />manifestProcessingFlags, Version version)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModule(String fileName, String moduleBase, String prefix, SessionState ss, <br />Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ImportModuleCommand.ProcessRecord()
       at System.Management.Automation.Cmdlet.DoProcessRecord()
       at System.Management.Automation.CommandProcessor.ProcessRecord()
       --- End of inner exception stack trace ---
       at System.Management.Automation.Runspaces.PipelineBase.Invoke(IEnumerable input)
       at System.Management.Automation.Runspaces.Pipeline.Invoke()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Invoke(String command, Object input, Boolean outputResults)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHostExtensions.ImportModule(PowerShellHost host, String modulePath)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.LoadStartupScripts()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Initialize()
       at NuGetConsole.Implementation.Console.ConsoleDispatcher.Start()
       at NuGetConsole.Implementation.PowerConsoleToolWindow.MoveFocus(FrameworkElement consolePane)

<span data-ttu-id="24fb5-150">Entramos em contato com o autor do suplemento em busca de negociarmos uma resolução.</span><span class="sxs-lookup"><span data-stu-id="24fb5-150">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="24fb5-151">Atualização: verificamos que a versão mais recente do Reflector, 6.5, não causa mais essa exceção no console.</span><span class="sxs-lookup"><span data-stu-id="24fb5-151">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="24fb5-152">Falha ao abrir o Console do Gerenciador de Pacotes com a exceção ObjectSecurity</span><span class="sxs-lookup"><span data-stu-id="24fb5-152">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="24fb5-153">Você pode encontrar esses erros ao tentar abrir o Console do Gerenciador de Pacotes:</span><span class="sxs-lookup"><span data-stu-id="24fb5-153">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="24fb5-154">Nesse caso, siga a solução [discutida em StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) para corrigi-los.</span><span class="sxs-lookup"><span data-stu-id="24fb5-154">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="24fb5-155">A caixa de diálogo Adicionar referência da biblioteca de pacote gerará uma exceção se a solução contiver um projeto do InstallShield Limited Edition.</span><span class="sxs-lookup"><span data-stu-id="24fb5-155">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project.</span></span>

<span data-ttu-id="24fb5-156">Nós identificamos que, se sua solução contiver um ou mais projetos do InstallShield Limited Edition, a caixa de diálogo **Adicionar referência de biblioteca de pacote** gerará uma exceção ao ser aberto.</span><span class="sxs-lookup"><span data-stu-id="24fb5-156">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="24fb5-157">Atualmente, ainda não há nenhuma solução alternativa, exceto remover os projetos do InstallShield ou descarregá-los.</span><span class="sxs-lookup"><span data-stu-id="24fb5-157">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="24fb5-158">O botão Desinstalar está esmaecido?</span><span class="sxs-lookup"><span data-stu-id="24fb5-158">Uninstall Button Greyed out?</span></span> <span data-ttu-id="24fb5-159">O NuGet exige privilégios de administrador para instalar/desinstalar</span><span class="sxs-lookup"><span data-stu-id="24fb5-159">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="24fb5-160">Se você tentar desinstalar o NuGet por meio do Gerenciador de Extensões do Visual Studio, poderá perceber que o botão Desinstalar está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="24fb5-160">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span>
<span data-ttu-id="24fb5-161">O NuGet exige privilégios de administrador para ser instalado e desinstalado.</span><span class="sxs-lookup"><span data-stu-id="24fb5-161">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="24fb5-162">Reinicie o Visual Studio como administrador para desinstalar a extensão.</span><span class="sxs-lookup"><span data-stu-id="24fb5-162">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span>
<span data-ttu-id="24fb5-163">O NuGet não requer acesso de administrador para usá-lo.</span><span class="sxs-lookup"><span data-stu-id="24fb5-163">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="24fb5-164">O Console do Gerenciador de Pacotes falha quando eu o abro no Windows XP.</span><span class="sxs-lookup"><span data-stu-id="24fb5-164">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="24fb5-165">Qual é o problema?</span><span class="sxs-lookup"><span data-stu-id="24fb5-165">What's wrong?</span></span>

<span data-ttu-id="24fb5-166">O NuGet requer o tempo de execução do Powershell 2.0.</span><span class="sxs-lookup"><span data-stu-id="24fb5-166">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="24fb5-167">O Windows XP, por padrão, não têm o Powershell 2.0.</span><span class="sxs-lookup"><span data-stu-id="24fb5-167">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="24fb5-168">Você pode baixar o tempo de execução do Powershell 2.0 de [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span><span class="sxs-lookup"><span data-stu-id="24fb5-168">You can download the Powershell 2.0 runtime from [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span></span> <span data-ttu-id="24fb5-169">Após a instalação, reinicie o Visual Studio e será possível abrir o Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="24fb5-169">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="24fb5-170">O Visual Studio 2010 SP1 Beta falha na saída se o Console de Gerenciador de Pacote estiver aberto.</span><span class="sxs-lookup"><span data-stu-id="24fb5-170">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="24fb5-171">Se você tiver instalado o Visual Studio 2010 SP1 Beta, poderá perceber que, se você deixar o Console do Gerenciador de Pacotes abertos e fechar o Visual Studio, ele falhará.</span><span class="sxs-lookup"><span data-stu-id="24fb5-171">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="24fb5-172">Este é um problema conhecido do Visual Studio e será corrigido na versão SP1 RTM.</span><span class="sxs-lookup"><span data-stu-id="24fb5-172">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span>
<span data-ttu-id="24fb5-173">Por enquanto, basta ignorar a falha ou desinstalar o SP1 Beta, se possível.</span><span class="sxs-lookup"><span data-stu-id="24fb5-173">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="24fb5-174">O elemento 'metadata' ... tem um elemento filho inválido, por isso uma exceção ocorre</span><span class="sxs-lookup"><span data-stu-id="24fb5-174">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="24fb5-175">Se você instalou pacotes compilados com uma versão de pré-lançamento do NuGet, poderá encontrar uma mensagem de erro dizendo “o elemento 'metadata' no namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' tem um elemento filho inválido” ao executar a versão RTM do NuGet com esse projeto.</span><span class="sxs-lookup"><span data-stu-id="24fb5-175">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="24fb5-176">Você precisará desinstalar e reinstalar cada pacote usando a versão RTM do NuGet.</span><span class="sxs-lookup"><span data-stu-id="24fb5-176">You'll need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-existsrdquo"></a><span data-ttu-id="24fb5-177">Tentativa de instalar ou desinstalar resultou no erro “Não é possível criar um arquivo quando ele já existe.&rdquo;</span><span class="sxs-lookup"><span data-stu-id="24fb5-177">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists.&rdquo;</span></span>

<span data-ttu-id="24fb5-178">Por algum motivo, as extensões do Visual Studio podem demonstrar certa estranheza se você tiver desinstalado a extensão do VSIX, mas alguns arquivos restaram.</span><span class="sxs-lookup"><span data-stu-id="24fb5-178">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="24fb5-179">Para solucionar esse problema:</span><span class="sxs-lookup"><span data-stu-id="24fb5-179">To work around this issue:</span></span>

1. <span data-ttu-id="24fb5-180">Sair do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="24fb5-180">Exit Visual Studio</span></span>
2. <span data-ttu-id="24fb5-181">Abra a pasta a seguir (ela pode estar em uma unidade diferente no seu computador)</span><span class="sxs-lookup"><span data-stu-id="24fb5-181">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="24fb5-182">C:\Arquivos de Programas (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<versão>\\</span><span class="sxs-lookup"><span data-stu-id="24fb5-182">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span></span>

3. <span data-ttu-id="24fb5-183">Exclua todos os arquivos com a extensão *.deleteme*.</span><span class="sxs-lookup"><span data-stu-id="24fb5-183">Delete all the files with the *.deleteme* extensions.</span></span>
4. <span data-ttu-id="24fb5-184">Abra novamente o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="24fb5-184">Re-open Visual Studio</span></span>

<span data-ttu-id="24fb5-185">Depois de seguir essas etapas, você deverá ser capaz de continuar.</span><span class="sxs-lookup"><span data-stu-id="24fb5-185">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="24fb5-186">Em casos raros, a compilação com Análise de Código ativada causa o erro.</span><span class="sxs-lookup"><span data-stu-id="24fb5-186">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="24fb5-187">Você pode obter o seguinte erro se instalar FluentNHibernate com o console do Gerenciador de Pacotes e, em seguida, compile seu projeto com “Análise de código” ativado.</span><span class="sxs-lookup"><span data-stu-id="24fb5-187">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="24fb5-188">Por padrão, FluentNHibernate requer NHibernate 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="24fb5-188">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="24fb5-189">No entanto, por padrão, o NuGet instalará o NHibernate 3.0.0.4000 em seu projeto e adicionará os redirecionamentos de associação apropriados para que ele funcione.</span><span class="sxs-lookup"><span data-stu-id="24fb5-189">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="24fb5-190">Seu projeto será compilado corretamente a análise de código não estiver ativada.</span><span class="sxs-lookup"><span data-stu-id="24fb5-190">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="24fb5-191">Em contraste com o compilador, a ferramenta de análise de código não segue corretamente os redirecionamentos de associação para usar 3.0.0.4000 em vez de 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="24fb5-191">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="24fb5-192">Você pode contornar o problema instalando o NHibernate 3.0.0.2001 ou dizer à ferramenta de análise de código para se comportar do mesmo modo que o compilador fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="24fb5-192">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="24fb5-193">Acesse *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span><span class="sxs-lookup"><span data-stu-id="24fb5-193">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="24fb5-194">Abra o FxCopCmd.exe.config e altere `AssemblyReferenceResolveMode` de `StrongName` para `StrongNameIgnoringVersion`.</span><span class="sxs-lookup"><span data-stu-id="24fb5-194">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="24fb5-195">Salve a alteração e recompile o projeto.</span><span class="sxs-lookup"><span data-stu-id="24fb5-195">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="24fb5-196">O comando Write-Error não funciona em install.ps1/uninstall.ps1/init.ps1</span><span class="sxs-lookup"><span data-stu-id="24fb5-196">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="24fb5-197">Este é um problema conhecido.</span><span class="sxs-lookup"><span data-stu-id="24fb5-197">This is a known issue.</span></span> <span data-ttu-id="24fb5-198">Em vez de chamar Write-Error, tente chamar throw.</span><span class="sxs-lookup"><span data-stu-id="24fb5-198">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="24fb5-199">Instalar o NuGet com acesso restrito no Windows 2003 pode causar falhas no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="24fb5-199">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>
<span data-ttu-id="24fb5-200">Ao tentar instalar o NuGet usando o Gerenciador de Extensões do Visual Studio sem estar em execução como administrador, a caixa de diálogo &#8220;Executar como&#8221;. é exibida com a caixa de seleção rotulada &#8220;Executar este programa com acesso restrito&#8221;. selecionada por padrão.</span><span class="sxs-lookup"><span data-stu-id="24fb5-200">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![Caixa de diálogo restrita Executar como](./media/RunAsRestricted.png)

<span data-ttu-id="24fb5-202">Clicar em OK com isso marcado causa uma falha no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24fb5-202">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="24fb5-203">Lembre-se de desmarcar essa opção antes de instalar o NuGet.</span><span class="sxs-lookup"><span data-stu-id="24fb5-203">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="24fb5-204">Não é possível desinstalar o NuGet para Ferramentas do Windows Phone</span><span class="sxs-lookup"><span data-stu-id="24fb5-204">Cannot uninstall NuGet for Windows Phone Tools</span></span>
<span data-ttu-id="24fb5-205">Ferramentas do Windows Phone não são compatíveis com o Gerenciador de Extensões do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24fb5-205">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="24fb5-206">Para desinstalar o NuGet, execute o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="24fb5-206">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="24fb5-207">Alterar a diferenciação entre maiúsculas e minúsculas de IDs do pacote do NuGet interrompe a restauração do pacote</span><span class="sxs-lookup"><span data-stu-id="24fb5-207">Changing the capitalization of NuGet package IDs breaks package restore</span></span>
<span data-ttu-id="24fb5-208">Conforme discutido em detalhes em [neste problema do GitHub](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), é possível alterar a diferenciação entre minúsculas e maiúsculas de pacotes do NuGet por meio do suporte ao NuGet, porém isso causa complicações durante a restauração de pacote para usuários que têm pacotes existentes com um padrão diferente de maiúsculas e minúsculas no cache local.</span><span class="sxs-lookup"><span data-stu-id="24fb5-208">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their local package cache.</span></span> <span data-ttu-id="24fb5-209">É recomendável solicitar uma alteração de caso somente quando você tem uma maneira de se comunicar com os usuários existentes do seu pacote sobre a interrupção que pode ocorrer na restauração do pacote de tempo de build.</span><span class="sxs-lookup"><span data-stu-id="24fb5-209">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="24fb5-210">Relatando problemas</span><span class="sxs-lookup"><span data-stu-id="24fb5-210">Reporting Issues</span></span>
<span data-ttu-id="24fb5-211">Para relatar problemas em clientes do NuGet, acesse [aqui](https://nuget.codeplex.com/WorkItem/Create).</span><span class="sxs-lookup"><span data-stu-id="24fb5-211">For reporting issues on NuGet Clients, please go [here](https://nuget.codeplex.com/WorkItem/Create).</span></span>
<span data-ttu-id="24fb5-212">Para relatar problemas na galeria do NuGet, acesse [aqui](https://github.com/nuget/nugetgallery/issues).</span><span class="sxs-lookup"><span data-stu-id="24fb5-212">For reporting issues on NuGet Gallery, please go [here](https://github.com/nuget/nugetgallery/issues).</span></span>