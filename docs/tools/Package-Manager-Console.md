---
title: Instalar e gerenciar pacotes NuGet no Visual Studio usando o PowerShell
description: Instruções sobre como usar o Console do Gerenciador de pacotes NuGet no Visual Studio para trabalhar com pacotes.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 11ec25598d3110ba84dec5044642e205e13346af
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426213"
---
# <a name="install-and-manage-packages-using-powershell-in-visual-studio"></a>Instalar e gerenciar pacotes no Visual Studio usando o PowerShell

O NuGet Package Manager Console permite que você use [comandos do PowerShell do NuGet](../tools/powershell-reference.md) para localizar, instalar, desinstalar e atualizar pacotes do NuGet. Usando o console é necessário em casos em que o Gerenciador de pacotes UI não fornece uma maneira de executar uma operação. Para usar `nuget.exe` comandos da CLI no console do, consulte [usando a CLI nuget.exe no console do](#using-the-nugetexe-cli-in-the-console).

O console é criado no Visual Studio no Windows. Não é incluído no Visual Studio para Mac ou Visual Studio Code.

## <a name="find-and-install-a-package"></a>Localizar e instalar um pacote

Por exemplo, localizar e instalar um pacote é feito com três etapas fáceis:

1. Abra o projeto/solução no Visual Studio e abra o console usando o **Ferramentas > Gerenciador de pacotes NuGet > Console do Gerenciador de pacotes** comando.

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
> Todas as operações que estão disponíveis no console também podem ser feitas com o [CLI do NuGet](../tools/nuget-exe-cli-reference.md). No entanto, os comandos do console operam dentro do contexto do Visual Studio e uma projeto/solução salva e geralmente realizar mais de seus comandos CLI equivalentes. Por exemplo, instalação de um pacote por meio do console adiciona uma referência ao projeto enquanto o comando da CLI não. Por esse motivo, os desenvolvedores que trabalham no Visual Studio geralmente preferem usando o console da CLI.

> [!Tip]
> Muitas operações de console dependem de você ter uma solução aberta no Visual Studio com um nome de caminho conhecido. Se você tiver uma solução não salva ou nenhuma solução, você pode ver o erro, "solução não é aberta ou não salvas. Verifique se que você tiver uma solução aberta e salva." Isso indica que o console não é possível determinar a pasta da solução. Salvando uma solução não salva, ou criando e salvando uma solução se você não tiver uma aberta, deverá corrigir o erro.

## <a name="opening-the-console-and-console-controls"></a>Abrindo o console e os controles de console

1. Abra o console no Visual Studio usando o **Ferramentas > Gerenciador de pacotes NuGet > Console do Gerenciador de pacotes** comando. O console é uma janela do Visual Studio que pode ser organizada e posicionada no entanto, como (consulte [Personalizar layouts de janela no Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Por padrão, os comandos do console operam em relação a uma origem de pacote específico e um projeto conforme definido no controle na parte superior da janela:

    ![Controles do Package Manager Console para a origem do pacote e projeto](media/PackageManagerConsoleControls1.png)

1. A seleção de uma origem de pacote diferente e/ou projeto altera esses padrões para comandos subsequentes. Para ignorar essas configurações sem alterar os padrões, a maioria dos comandos de suporte `-Source` e `-ProjectName` opções.

1. Para gerenciar fontes de pacote, selecione o ícone de engrenagem. Esse é um atalho para o **Ferramentas > Opções > Gerenciador de pacotes NuGet > origens de pacote** caixa de diálogo, conforme descrito no [Gerenciador de pacotes UI](package-manager-ui.md#package-sources) página. Além disso, o controle à direita do seletor de projeto limpa o conteúdo do console:

    ![As configurações do Console do Gerenciador de pacotes e limpar controles](media/PackageManagerConsoleControls2.png)

1. O botão mais à direita interrupções de um comando de execução longa. Por exemplo, executando `Get-Package -ListAvailable -PageSize 500` lista os pacotes superior a 500 na fonte de padrão (como nuget.org), que pode levar vários minutos para ser executado.

    ![Controle de parada do Package Manager Console](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>Instalação de um pacote

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Ver [Install-Package](../tools/ps-ref-install-package.md).

Instalação de um pacote no console executa as mesmas etapas conforme descrito em [o que acontece quando um pacote é instalado](../concepts/package-installation-process.md), com as seguintes adições:

- O Console exibe os termos de licença aplicáveis em sua janela com o contrato implícito. Se você não concordar com os termos, você deve desinstalar o pacote imediatamente.
- Também uma referência para o pacote é adicionada ao arquivo de projeto e aparece na **Gerenciador de soluções** sob o **referências** nó, você precisa salvar o projeto para ver as alterações no arquivo de projeto diretamente.

## <a name="uninstalling-a-package"></a>Desinstalar um pacote

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Ver [Uninstall-Package](../tools/ps-ref-uninstall-package.md). Use [Get-Package](../tools/ps-ref-get-package.md) para ver todos os pacotes instalados no momento no projeto padrão, se você precisar localizar um identificador.

Desinstalar um pacote executa as seguintes ações:

- Remove as referências ao pacote do projeto (e qualquer formato de gerenciamento está em uso). Referências não aparecem mais na **Gerenciador de soluções**. (Talvez seja necessário recompilar o projeto para vê-lo removido do **Bin** pasta.)
- Reverte todas as alterações feitas `app.config` ou `web.config` quando o pacote foi instalado.
- Remove instalado anteriormente dependências se não há pacotes restantes usam essas dependências.

## <a name="updating-a-package"></a>Atualizar um pacote

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

Ver [Get-Package](../tools/ps-ref-get-package.md) e [Update-Package](../tools/ps-ref-update-package.md)

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

Ver [Find-Package](../tools/ps-ref-find-package.md). No Visual Studio 2013 e anteriores, use [Get-Package](../tools/ps-ref-get-package.md) em vez disso.

## <a name="availability-of-the-console"></a>Disponibilidade do console

A partir do Visual Studio 2017, NuGet e o Gerenciador de pacotes do NuGet são instalados automaticamente quando você seleciona qualquer um. Cargas de trabalho relacionados à rede; Você também pode instalar individualmente, marcando a **componentes individuais > Ferramentas de código > Gerenciador de pacotes NuGet** opção no instalador do Visual Studio.

Além disso, se estiver faltando o Gerenciador de pacotes do NuGet no Visual Studio 2015 e anteriores, verifique **Ferramentas > extensões e atualizações...**  e pesquise a extensão do Gerenciador de pacotes NuGet. Se você não puder usar o instalador de extensões no Visual Studio, você pode baixar a extensão diretamente [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).

O Console do Gerenciador de pacote não está disponível atualmente com o Visual Studio para Mac. No entanto, os comandos equivalentes, estão disponíveis por meio de [CLI do NuGet](nuget-exe-CLI-reference.md). O Visual Studio para Mac tem uma interface do usuário para o gerenciamento de pacotes do NuGet. Ver [incluindo um pacote do NuGet em seu projeto](/visualstudio/mac/nuget-walkthrough).

O Console do Gerenciador de pacote não está incluído com o Visual Studio Code.

## <a name="extending-the-package-manager-console"></a>Estendendo o Package Manager Console

Alguns pacotes instalados novos comandos para o console. Por exemplo, `MvcScaffolding` cria comandos como `Scaffold` mostrado abaixo, que gera a controladores e exibições MVC do ASP.NET:

![Instalar e usar MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Como configurar um perfil do NuGet PowerShell

Um perfil do PowerShell permite disponibilizar comandos usados sempre que você usar o PowerShell. O NuGet dá suporte a um perfil específico do NuGet normalmente encontrado no seguinte local:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Para localizar o perfil, digite `$profile` no console:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Para obter mais detalhes, consulte [perfis do Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="using-the-nugetexe-cli-in-the-console"></a>Usando a CLI nuget.exe no console do

Para tornar o [ `nuget.exe` CLI](nuget-exe-cli-reference.md) disponível no Console do Gerenciador de pacotes, instalar o [CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) pacote no console:

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
