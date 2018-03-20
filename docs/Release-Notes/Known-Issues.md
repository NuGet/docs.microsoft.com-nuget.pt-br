---
title: Problemas conhecidos do NuGet | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Problemas conhecidos com o NuGet, incluindo autenticação, instalação de pacote e ferramentas."
keywords: Problemas conhecidos do NuGet, problemas do NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ac00e3f11c54290a31319e7f2946fd965a0a9288
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2018
---
# <a name="known-issues-with-nuget"></a>Problemas conhecidos com o NuGet

Esses são os problemas comuns conhecidos do NuGet relatados com mais frequência. Se você estiver tendo problemas para instalar o NuGet ou gerenciar pacotes, veja esses problemas conhecidos e suas soluções.

> [!Note]
> A partir do NuGet 4.0, problemas conhecidos fazem parte das respectivas notas de versão.

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>Problemas de autenticação com feeds do NuGet no VSTS com nuget.exe v3.4.3

**Problema:**

Quando usamos o comando a seguir para armazenar as credenciais, podemos acabar duplicando a criptografia do Token de Acesso Pessoal.

$PAT = "Seu token de acesso pessoal" $Feed = "Sua url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT

**Solução alternativa:**

Armazenar senhas em texto não criptografado usando a opção [-StorePasswordInClearText](../tools/cli-ref-sources.md).

## <a name="error-installing-packages-with-nuget-34-341"></a>Erro ao instalar pacotes com o NuGet 3.4, 3.4.1

**Problema:**

No NuGet 3.4 e 3.4.1, ao usar o suplemento do NuGet, nenhuma origem é relatada como disponível e você não consegue adicionar novas origens na janela de configuração. O resultado é semelhante à imagem abaixo:

![Configuração do NuGet sem origens](./media/knownIssue-34-NoSources.PNG)

O arquivo `NuGet.Config` na pasta `%AppData%\NuGet\` (Windows) ou `~/.nuget/` (Mac/Linux) foi esvaziado acidentalmente. Para corrigir isso: feche o Visual Studio (no Windows se aplicável), exclua o arquivo `NuGet.Config` e tente realizar a operação novamente. O NuGet gerará um novo `NuGet.Config` e você poderá continuar.

## <a name="error-installing-packages-with-nuget-27"></a>Erro ao instalar pacotes com o NuGet 2.7

**Problema:**

No NuGet 2.7 ou superior, quando você tenta instalar qualquer pacote que contém as referências de assembly, receberá a mensagem de erro **“A cadeia de caracteres de entrada não estava no formato correto.”**, como mostrado abaixo:

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

Isso é causado pela biblioteca de tipos para o componente COM de `VSLangProj.dll` cujo registro está sendo cancelado no sistema. Isso pode acontecer, por exemplo, quando você tem duas versões do Visual Studio instaladas lado a lado e desinstala a versão mais antiga. Isso pode inadvertidamente cancelar o registro das biblioteca COM acima.

**Solução:**:

Execute este comando de um **prompt com privilégios elevados** para registrar novamente a biblioteca de tipos para `VSLangProj.dll`

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

Se o comando falhar, verifique se o arquivo existe no local.

Para obter mais informações sobre esse erro, consulte [item de trabalho](https://nuget.codeplex.com/workitem/3609 "Item de trabalho 3609").

## <a name="build-failure-after-package-update-in-vs-2012"></a>Falha de build após a atualização de pacote no VS 2012

O problema: você está usando o VS 2012 RTM. Ao atualizar pacotes do NuGet, você receberá esta mensagem: “não foi possível concluir a desinstalação de um ou mais pacotes”. e é solicitado que você reinicie o Visual Studio. Após a reinicialização do VS, você receberá erros de build estranhos.

A causa é que certos arquivos dos pacotes antigo estão bloqueados por um processo do MSBuild em segundo plano. Mesmo depois de reiniciar o VS, o processo de MSBuild em segundo plano ainda usa os arquivos nos pacotes antigos, causando falhas de build.

A correção é instalar a Atualização do VS 2012, por exemplo, VS 2012 Atualização 2.

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>Fazendo upgrade para o NuGet mais recente de uma versão mais antiga causa um erro de verificação de assinatura

Se você estiver executando o VS 2010 SP1, poderá encontrar a seguinte mensagem de erro ao tentar fazer upgrade no NuGet se tiver uma versão mais antiga instalada.

![Instalador de Extensões do Visual Studio](./media/Visual-Studio-Extension-Installer.png)

Ao exibir os logs, você poderá ver uma menção de um `SignatureMismatchException`.

Para evitar que isso ocorra, há um [hotfix do Visual Studio 2010 SP1](http://bit.ly/vsixcertfix) que você pode instalar.
Outra opção é usar a solução alternativa de simplesmente desinstalar o NuGet (enquanto o Visual Studio é executado como Administrador) e, em seguida, instalá-lo da Galeria de Extensões do VS.  Veja [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) para obter mais informações.

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>O Console do Gerenciador de Pacotes gera uma exceção quando o suplemento do Reflector Visual Studio também é instalado.

Ao executar o console do Gerenciador de Pacotes, você pode encontrar a seguinte mensagem de exceção se você tiver o suplemento do Reflector VS instalado.

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

ou

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

Entramos em contato com o autor do suplemento em busca de negociarmos uma resolução.

<p class="info">Atualização: verificamos que a versão mais recente do Reflector, 6.5, não causa mais essa exceção no console.</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>Falha ao abrir o Console do Gerenciador de Pacotes com a exceção ObjectSecurity

Você pode encontrar esses erros ao tentar abrir o Console do Gerenciador de Pacotes:

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

Nesse caso, siga a solução [discutida em StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) para corrigi-los.

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>A caixa de diálogo Adicionar referência da biblioteca de pacote gerará uma exceção se a solução contiver um projeto do InstallShield Limited Edition

Nós identificamos que, se sua solução contiver um ou mais projetos do InstallShield Limited Edition, a caixa de diálogo **Adicionar referência de biblioteca de pacote** gerará uma exceção ao ser aberto. Atualmente, ainda não há nenhuma solução alternativa, exceto remover os projetos do InstallShield ou descarregá-los.

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>O botão Desinstalar está esmaecido? O NuGet exige privilégios de administrador para instalar/desinstalar

Se você tentar desinstalar o NuGet por meio do Gerenciador de Extensões do Visual Studio, poderá perceber que o botão Desinstalar está desabilitado. O NuGet exige privilégios de administrador para ser instalado e desinstalado. Reinicie o Visual Studio como administrador para desinstalar a extensão. O NuGet não requer acesso de administrador para usá-lo.

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>O Console do Gerenciador de Pacotes falha quando eu o abro no Windows XP. Qual é o problema?

O NuGet requer o tempo de execução do Powershell 2.0. O Windows XP, por padrão, não têm o Powershell 2.0. Você pode baixar o tempo de execução do PowerShell 2.0 em [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929). Após a instalação, reinicie o Visual Studio e será possível abrir o Console do Gerenciador de Pacotes.

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>O Visual Studio 2010 SP1 Beta falha na saída se o Console de Gerenciador de Pacote estiver aberto.

Se você tiver instalado o Visual Studio 2010 SP1 Beta, poderá perceber que, se você deixar o Console do Gerenciador de Pacotes abertos e fechar o Visual Studio, ele falhará. Este é um problema conhecido do Visual Studio e será corrigido na versão SP1 RTM. Por enquanto, basta ignorar a falha ou desinstalar o SP1 Beta, se possível.

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>O elemento 'metadata' ... tem um elemento filho inválido, por isso uma exceção ocorre

Se você instalou pacotes compilados com uma versão de pré-lançamento do NuGet, poderá encontrar uma mensagem de erro dizendo “o elemento 'metadata' no namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' tem um elemento filho inválido” ao executar a versão RTM do NuGet com esse projeto. Você precisa desinstalar e reinstalar cada pacote usando a versão RTM do NuGet.

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>Tentativa de instalar ou desinstalar resultou no erro "Não é possível criar um arquivo quando ele já existe."

Por algum motivo, as extensões do Visual Studio podem demonstrar certa estranheza se você tiver desinstalado a extensão do VSIX, mas alguns arquivos restaram. Para solucionar esse problema:

1. Sair do Visual Studio
1. Abra a pasta a seguir (ela pode estar em uma unidade diferente no seu computador)

    C:\Arquivos de Programas (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<versão>\

1. Exclua todos os arquivos com a extensão *.deleteme*.
1. Abra novamente o Visual Studio

Depois de seguir essas etapas, você deverá ser capaz de continuar.

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>Em casos raros, a compilação com Análise de Código ativada causa o erro.

Você pode obter o seguinte erro se instalar FluentNHibernate com o console do Gerenciador de Pacotes e, em seguida, compile seu projeto com “Análise de código” ativado.

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

Por padrão, FluentNHibernate requer NHibernate 3.0.0.2001. No entanto, por padrão, o NuGet instalará o NHibernate 3.0.0.4000 em seu projeto e adicionará os redirecionamentos de associação apropriados para que ele funcione. Seu projeto será compilado corretamente a análise de código não estiver ativada. Em contraste com o compilador, a ferramenta de análise de código não segue corretamente os redirecionamentos de associação para usar 3.0.0.4000 em vez de 3.0.0.2001. Você pode contornar o problema instalando o NHibernate 3.0.0.2001 ou dizer à ferramenta de análise de código para se comportar do mesmo modo que o compilador fazendo o seguinte:

1. Acesse *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*
1. Abra o FxCopCmd.exe.config e altere `AssemblyReferenceResolveMode` de `StrongName` para `StrongNameIgnoringVersion`.
1. Salve a alteração e recompile o projeto.

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>O comando Write-Error não funciona em install.ps1/uninstall.ps1/init.ps1

Este é um problema conhecido. Em vez de chamar Write-Error, tente chamar throw.

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>Instalar o NuGet com acesso restrito no Windows 2003 pode causar falhas no Visual Studio

Ao tentar instalar o NuGet usando o Gerenciador de Extensões do Visual Studio sem estar em execução como administrador, a caixa de diálogo &#8220;Executar como&#8221;. é exibida com a caixa de seleção rotulada &#8220;Executar este programa com acesso restrito&#8221;. selecionada por padrão.

![Caixa de diálogo restrita Executar como](./media/RunAsRestricted.png)

Clicar em OK com isso marcado causa uma falha no Visual Studio. Lembre-se de desmarcar essa opção antes de instalar o NuGet.

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>Não é possível desinstalar o NuGet para Ferramentas do Windows Phone

Ferramentas do Windows Phone não são compatíveis com o Gerenciador de Extensões do Visual Studio. Para desinstalar o NuGet, execute o seguinte comando.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>Alterar a diferenciação entre maiúsculas e minúsculas de IDs do pacote do NuGet interrompe a restauração do pacote

Conforme discutido em detalhes em [neste problema do GitHub](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), é possível alterar a diferenciação entre minúsculas e maiúsculas de pacotes do NuGet por meio do suporte ao NuGet, porém isso causa complicações durante a restauração de pacote para usuários que têm pacotes existentes com um padrão diferente de maiúsculas e minúsculas no cache local. É recomendável solicitar uma alteração de caso somente quando você tem uma maneira de se comunicar com os usuários existentes do seu pacote sobre a interrupção que pode ocorrer na restauração do pacote de tempo de build.

## <a name="reporting-issues"></a>Relatando problemas

Para relatar problemas do NuGet, visite [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).
