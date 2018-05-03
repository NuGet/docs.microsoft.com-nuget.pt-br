---
title: Guia do NuGet Package Manager Console
description: Instruções para usar o NuGet Package Manager Console no Visual Studio para trabalhar com pacotes.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 64912f0dc32a492d9c23a02f45b4303c69faf340
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="package-manager-console"></a>Console do Gerenciador de Pacotes

O NuGet Package Manager Console é incorporado ao Visual Studio na versão 2012 e versões posterior do Windows. (Não é incluído no Visual Studio para Mac ou o código do Visual Studio.)

O console permite que você use [comandos do PowerShell do NuGet](../tools/powershell-reference.md) para localizar, instalar, desinstalar e atualizar pacotes do NuGet. É necessário em casos onde o UI Package Manager não oferece uma maneira de executar uma operação usando o console. Para usar `nuget.exe` comandos no console do, consulte [usando a CLI nuget.exe no console do](#using-the-nugetexe-cli-in-the-console).

Por exemplo, localizar e instalar um pacote é feito com três etapas simples:

1. Abra o projeto/solução no Visual Studio e abra o console usando o **Ferramentas > Gerenciador de pacotes do NuGet > Package Manager Console** comando.

1. Encontre o pacote que você deseja instalar. Se você já sabe que isso, vá para a etapa 3.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Execute o comando de instalação:

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> Todas as operações que estão disponíveis no console do também podem ser feitas com o [NuGet CLI](../tools/nuget-exe-cli-reference.md). No entanto, comandos do console operam dentro do contexto do Visual Studio e uma projeto/solução salva e geralmente realizar mais de seus comandos CLI equivalentes. Por exemplo, instalando um pacote por meio do console adiciona uma referência ao projeto enquanto o comando CLI não. Por esse motivo, os desenvolvedores trabalhando no Visual Studio normalmente preferem usando o console de CLI.

> [!Tip]
> Muitas operações de console dependem da existência de uma solução aberta no Visual Studio com um nome de caminho conhecido. Se você tiver uma solução não salva ou nenhuma solução, você pode ver o erro, "solução não está aberta ou não foi salvo. Verifique se que você tiver uma solução aberta e salva." Isso indica que o console não é possível determinar a pasta de solução. Salvando uma solução não salva, ou criar e salvar uma solução se você não tiver um abrir, deve corrigir o erro.

## <a name="opening-the-console-and-console-controls"></a>Abrir o console e os controles do console

1. Abra o console no Visual Studio usando o **Ferramentas > Gerenciador de pacotes do NuGet > Package Manager Console** comando. O console é uma janela do Visual Studio que pode ser organizada e posicionada você quiser (consulte [Personalizar layouts de janela no Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Por padrão, comandos do console de operam em relação a uma origem de pacote específico e o projeto como definido no controle na parte superior da janela:

    ![Controles de Console do Gerenciador de pacotes de origem do pacote e projeto](media/PackageManagerConsoleControls1.png)

1. Selecionar uma origem de pacote diferente e/ou projeto altera esses padrões para comandos subsequentes. Ignorar essas configurações sem alterar os padrões, a maioria dos comandos suporte `-Source` e `-ProjectName` opções.

1. Para gerenciar fontes de pacote, selecione o ícone de engrenagem. Este é um atalho para o **Ferramentas > Opções > NuGet Package Manager > fontes de pacote** caixa de diálogo, conforme descrito no [Package Manager UI](package-manager-ui.md#package-sources) página. Além disso, o controle à direita do seletor de projeto limpa o conteúdo do console:

    ![As configurações do Console do Gerenciador de pacotes e desmarque os controles](media/PackageManagerConsoleControls2.png)

1. O botão mais à direita interrupções de um comando de execução longa. Por exemplo, executando `Get-Package -ListAvailable -PageSize 500` lista os pacotes superior 500 na origem padrão (como nuget.org), que pode levar vários minutos para ser executado.

    ![Controle de parada do Console do Gerenciador de pacotes](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>Instalação de um pacote

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Consulte [Install-Package](../tools/ps-ref-install-package.md).

Instalação de um pacote no console executa as mesmas etapas, conforme descrito em [o que acontece quando um pacote é instalado](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), com as seguintes adições:

- O Console exibe os termos de licença aplicáveis em sua janela com contrato implícito. Se você não concorda com os termos, você deve desinstalar o pacote imediatamente.
- Também uma referência para o pacote é adicionada ao arquivo de projeto e aparece no **Solution Explorer** sob o **referências** nó, você precisa salvar o projeto para ver as alterações no arquivo de projeto diretamente.

## <a name="uninstalling-a-package"></a>Desinstalar um pacote

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Consulte [Uninstall-Package](../tools/ps-ref-uninstall-package.md). Use [Get-Package](../tools/ps-ref-get-package.md) para ver todos os pacotes instalados no projeto padrão se você precisar localizar um identificador.

Desinstalar um pacote executa as seguintes ações:

- Remove as referências ao pacote do projeto (e qualquer formato de gerenciamento está em uso). As referências não aparecem mais na **Gerenciador de soluções**. (Talvez seja necessário recompilar o projeto para vê-lo removido o **Bin** pasta.)
- Reverte as alterações feitas `app.config` ou `web.config` quando o pacote foi instalado.
- Dependências de remove anteriormente instalado se não há pacotes restantes usam essas dependências.

## <a name="updating-a-package"></a>Um pacote de atualização

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

Consulte [Get-Package](../tools/ps-ref-get-package.md) e [pacote de atualização](../tools/ps-ref-update-package.md)

## <a name="finding-a-package"></a>Localizar um pacote

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

Consulte [Find-Package](../tools/ps-ref-find-package.md). No Visual Studio 2013 e anteriores, use [Get-Package](../tools/ps-ref-get-package.md) em vez disso.

## <a name="availability-of-the-console"></a>Disponibilidade do console

No Visual Studio de 2017, o NuGet e o NuGet Package Manager são instalados automaticamente quando você seleciona qualquer. Cargas de trabalho relacionados à rede; Você também pode instalar individualmente, verificando o **componentes individuais > código Ferramentas > Gerenciador de pacotes do NuGet** opção no instalador do Visual Studio de 2017.

Além disso, se estiver faltando o Gerenciador de pacotes do NuGet no Visual Studio 2015 e versões anteriores, verifique **Ferramentas > extensões e atualizações...**  e procure a extensão do Gerenciador de pacotes do NuGet. Se não for possível usar o instalador de extensões do Visual Studio, você pode baixar a extensão diretamente do [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).

O Console do Gerenciador de pacote não está atualmente disponível com o Visual Studio para Mac. No entanto, os comandos equivalentes, estão disponíveis por meio de [NuGet CLI](nuget-exe-CLI-reference.md). Visual Studio para Mac tem uma interface de usuário para gerenciar pacotes NuGet. Consulte [incluindo NuGet um pacote em seu projeto](/visualstudio/mac/nuget-walkthrough).

O Console do Gerenciador de pacote não está incluído no código do Visual Studio.

## <a name="extending-the-package-manager-console"></a>Estendendo o Package Manager Console

Alguns pacotes instalam novos comandos do console. Por exemplo, `MvcScaffolding` cria os comandos `Scaffold` mostrado abaixo, que gera os controladores do ASP.NET MVC e modos de exibição:

![Instalar e usar MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Configurando um perfil do NuGet PowerShell

Um perfil do PowerShell permite disponibilizar comandos usados com frequência, sempre que você usar o PowerShell. O NuGet dá suporte a um perfil específico do NuGet normalmente encontrado no seguinte local:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Para localizar o perfil, digite `$profile` no console:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Para obter mais detalhes, consulte [perfis do Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="using-the-nugetexe-cli-in-the-console"></a>Usando a CLI nuget.exe no console do

Para fazer o [ `nuget.exe` CLI](nuget-exe-cli-reference.md) disponíveis no Console do Gerenciador de pacotes, instale o [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) pacote no console do:

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
