---
title: Instalar e gerenciar pacotes do NuGet usando o console no Visual Studio
description: Instruções para usar o Console do Gerenciador de pacotes do NuGet no Visual Studio para trabalhar com pacotes.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 42031f7b5fe4d3c1b4dbe5e1bfbf9197014e0e88
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428950"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a>Instalar e gerenciar pacotes com o Console do Gerenciador de Pacotes no Visual Studio (PowerShell)

O Console do Gerenciador de pacotes do NuGet possibilita usar os [comandos do PowerShell para NuGet](../reference/powershell-reference.md) para localizar, instalar, desinstalar e atualizar os pacotes do NuGet. O uso do console é necessário nos casos em que a interface do usuário do Gerenciador de Pacotes não fornece uma maneira de executar uma operação. Para usar os comandos da CLI `nuget.exe` no console, confira [Usar a CLI nuget.exe no console](#use-the-nugetexe-cli-in-the-console).

O console é integrado ao Visual Studio no Windows. Ele não está incluído no Visual Studio para Mac ou no Visual Studio Code.

## <a name="find-and-install-a-package"></a>Encontrar e instalar um pacote

Por exemplo, encontrar e instalar um pacote é feito com três etapas fáceis:

1. Abra o projeto/solução no Visual Studio e abra o console usando o comando **Ferramentas > Gerenciador de pacotes do NuGet > Console do Gerenciador de Pacotes**.

1. Localize o pacote que você deseja instalar. Se já sabe qual é, pule para a etapa 3.

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
> Todas as operações que estão disponíveis no console também podem ser feitas com a [CLI NuGet](../reference/nuget-exe-cli-reference.md). No entanto, os comandos do console operam dentro do contexto do Visual Studio e de um projeto/solução salvo e, muitas vezes, executam mais do que seus comandos equivalentes de CLI. Por exemplo, a instalação de um pacote por meio do console adiciona uma referência ao projeto, enquanto o comando da CLI, não. Por esse motivo, os desenvolvedores que trabalham no Visual Studio normalmente preferem usar o console ao invés da CLI.

> [!Tip]
> Muitas operações de console dependem de ter uma solução aberta no Visual Studio com um nome de caminho conhecido. Se uma solução não está salva, ou se não há uma solução, ocorrerá o erro "A solução não está aberta ou não foi salva. Verifique se tem uma solução aberta e salva". Isso indica que o console não pode determinar a pasta da solução. Salvar uma solução que não foi salva, ou criar e salvar uma solução se uma não estiver aberta, deve corrigir o erro.

## <a name="opening-the-console-and-console-controls"></a>Abrir o console e os controles do console

1. Abra o console no Visual Studio usando o comando **Ferramentas > Gerenciador de pacotes do NuGet > Console do Gerenciador de Pacotes**. O console é uma janela do Visual Studio que pode ser organizada e posicionada como você desejar (confira [Personalizar layouts de janela no Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Por padrão, os comandos do console operam em relação a um projeto e origem de pacote específicos, como definido no controle na parte superior da janela:

    ![Controles do Console do Gerenciador de Pacotes para o projeto e a origem do pacote](media/PackageManagerConsoleControls1.png)

1. A seleção de um projeto e/ou origem de pacote diferente altera esses padrões para os comandos subsequentes. Para substituir essas configurações sem alterar os padrões, a maioria dos comandos é compatível com as opções `-Source` e `-ProjectName`.

1. Para gerenciar as origens dos pacote, selecione o ícone de engrenagem. Este é um atalho para a caixa de diálogo **Ferramentas > Opções > Gerenciador de pacotes do NuGet > Origens do Pacote**, como descrito na página [Interface do usuário do Gerenciador de Pacotes](install-use-packages-visual-studio.md#package-sources). Além disso, o controle à direita do seletor de projeto limpa o conteúdo do console:

    ![Configurações do Console do Gerenciador de pacotes e controles desmarcados](media/PackageManagerConsoleControls2.png)

1. O botão mais à direita interrompe um comando de execução longa. Por exemplo, a execução de `Get-Package -ListAvailable -PageSize 500` lista os primeiros 500 pacotes na origem padrão (como nuget.org), o que pode demorar vários minutos para executar.

    ![Controle de interrupção do Console do Gerenciador de Pacotes](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a>Instalar um pacote

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Confira [Install-Package](../reference/ps-reference/ps-ref-install-package.md).

A instalação de um pacote no console executa as mesmas etapas, como descrito em [O que acontece quando um pacote é instalado](../concepts/package-installation-process.md), com as seguintes adições:

- O console exibe os termos de licenças aplicáveis em sua janela com o contrato implícito. Se você não concordar com os termos, deverá desinstalar o pacote imediatamente.
- Além disso, uma referência ao pacote é adicionada ao arquivo de projeto e aparece no **Gerenciador de Soluções** sob o nó **Referências**; é preciso salvar o projeto para ver as alterações diretamente no arquivo de projeto.

## <a name="uninstall-a-package"></a>Desinstalar um pacote

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Confira [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md). Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) para ver todos os pacotes atualmente instalados no projeto padrão, caso precise encontrar um identificador.

A desinstalação de um pacote executa as seguintes ações:

- Remove as referências ao pacote do projeto (e qualquer formato de gerenciamento em uso). As referências não aparecem mais no **Gerenciador de Soluções**. (Talvez seja necessário recompilar o projeto para vê-lo removido da pasta **Bin**.)
- Reverte todas as alterações feitas em `app.config` ou `web.config` quando o pacote foi instalado.
- Remove as dependências instaladas anteriormente se nenhum pacote restante usa essas dependências.

## <a name="update-a-package"></a>Atualizar um pacote

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

Confira [Get-Package](../reference/ps-reference/ps-ref-get-package.md) e [Update-Package](../reference/ps-reference/ps-ref-update-package.md)

## <a name="find-a-package"></a>Localizar um pacote

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

Confira [Find-Package](../reference/ps-reference/ps-ref-find-package.md). No Visual Studio 2013 e anteriores, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md).

## <a name="availability-of-the-console"></a>Disponibilidade do console

A partir do Visual Studio 2017, o NuGet e o Gerenciador de pacotes do NuGet são instalados automaticamente ao seleciona qualquer carga de trabalho relacionada a .NET. Também é possível instalá-los individualmente marcando a opção **Componentes individuais > Ferramentas de código > Gerenciador de pacotes do NuGet** no instalador do Visual Studio.

Além disso, se você não tem o Gerenciador de pacotes do NuGet no Visual Studio 2015 e anteriores, marque **Ferramentas > Extensões e Atualizações...** e pesquise pela extensão Gerenciador de pacotes do NuGet. Se não é possível usar o instalador de extensões no Visual Studio, baixe a extensão diretamente de [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

O Console do Gerenciador de Pacotes não está disponível atualmente no Visual Studio para Mac. No entanto, os comandos equivalentes estão disponíveis por meio da [CLI NuGet](../reference/nuget-exe-CLI-reference.md). O Visual Studio para Mac tem uma interface do usuário para gerenciar pacotes do NuGet. Confira [Incluindo um pacote do NuGet no projeto](/visualstudio/mac/nuget-walkthrough).

O Console do Gerenciador de Pacotes não está incluso no Visual Studio Code.

## <a name="extend-the-package-manager-console"></a>Estender o Console do Gerenciador de Pacotes

Alguns pacotes instalam novos comandos no console. Por exemplo, `MvcScaffolding` cria comandos como `Scaffold`, como mostrado abaixo, que gera os controladores e exibições do ASP.NET MVC:

![Instalar e usar MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a>Configurar um perfil do PowerShell do NuGet

Um perfil do PowerShell possibilita disponibilizar os comandos usados com frequência sempre que usar o PowerShell. O NuGet é compatível com um perfil específico do NuGet, normalmente encontrado no seguinte local:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Para localizar o perfil, digite `$profile` no console:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Para saber mais, confira [Perfis do Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="use-the-nugetexe-cli-in-the-console"></a>Usar a CLI nuget.exe no console

Para disponibilizar a [CLI `nuget.exe`](../reference/nuget-exe-cli-reference.md) no Console do Gerenciador de Pacotes, instale o pacote [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) pelo console:

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
