---
title: Guia do NuGet Package Manager Console | Microsoft Docs
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2b92b119-6861-406c-82af-9d739af230e4
description: "Instruções para usar o NuGet Package Manager Console no Visual Studio para trabalhar com pacotes."
keywords: Console de Gerenciador de pacote do NuGet, powershell do NuGet, gerenciar os pacotes NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d9df514c6f92a3ea0841503d86c44271e70f95f2
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="package-manager-console"></a>Console do Gerenciador de pacotes

O NuGet Package Manager Console é incorporado ao Visual Studio na versão 2012 e versões posterior do Windows. (Não é incluído no Visual Studio para Mac ou o código do Visual Studio.)

O console permite que você use [comandos do PowerShell do NuGet](../tools/powershell-reference.md) para localizar, instalar, desinstalar e atualizar pacotes do NuGet. É necessário em casos onde o UI Package Manager não oferece uma maneira de executar uma operação usando o console.

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

Neste tópico:

- [Abrindo o console](#opening-the-console-and-console-controls)
- [Instalação de um pacote](#installing-a-package)
- [Desinstalar um pacote](#uninstalling-a-package)
- [Localizar um pacote](#finding-a-package)
- [Um pacote de atualização](#updating-a-package)
- [Disponibilidade do console](#availability-of-the-console)
- [Estendendo o Package Manager Console](#extending-the-package-manager-console)
- [Configurando um perfil do NuGet PowerShell](#setting-up-a-nuget-powershell-profile)

> [!Important]
> Todas as operações que estão disponíveis no console do também podem ser feitas com o [NuGet CLI](../tools/nuget-exe-cli-reference.md). No entanto, comandos do console operam dentro do contexto do Visual Studio e uma projeto/solução salva e geralmente realizar mais de seus comandos CLI equivalentes. Por exemplo, instalando um pacote por meio do console adiciona uma referência ao projeto enquanto o comando CLI não. Por esse motivo, os desenvolvedores trabalhando no Visual Studio normalmente preferem usando o console de CLI.

> [!Tip]
> Muitas operações de console dependem da existência de uma solução aberta no Visual Studio com um nome de caminho conhecido. Se você tiver uma solução não salva ou nenhuma solução, você pode ver o erro, "solução não está aberta ou não foi salvo. Verifique se que você tiver uma solução aberta e salva." Isso indica que o console não é possível determinar a pasta de solução. Salvando uma solução não salva, ou criar e salvar uma solução se você não tiver um abrir, deve corrigir o erro.

## <a name="opening-the-console-and-console-controls"></a>Abrir o console e os controles do console

1. Abra o console no Visual Studio usando o **Ferramentas > Gerenciador de pacotes do NuGet > Package Manager Console** comando. O console é uma janela do Visual Studio que pode ser organizada e posicionada você quiser (consulte [Personalizar layouts de janela no Visual Studio](https://docs.microsoft.com/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Por padrão, comandos do console de operam em relação a uma origem de pacote específico e o projeto como definido no controle na parte superior da janela:

    ![Controles de Console do Gerenciador de pacotes de origem do pacote e projeto](media/PackageManagerConsoleControls1.png)

1. Selecionar uma origem de pacote diferente e/ou projeto altera esses padrões para comandos subsequentes. Ignorar essas configurações sem alterar os padrões, a maioria dos comandos suporte `-Source` e `-ProjectName` opções.

1. Para gerenciar fontes de pacote, selecione o ícone de engrenagem. Este é um atalho para o **Ferramentas > Opções > NuGet Package Manager > fontes de pacote** caixa de diálogo, conforme descrito no [Package Manager UI](Package-Manager-UI.md#package-sources) página. Além disso, o controle à direita do seletor de projeto limpa o conteúdo do console:

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

Instalação de um pacote executa as seguintes ações:

- Exibe os termos de licença aplicáveis na janela do console com um contrato implícito. Se você não concorda com os termos, você deve desinstalar o pacote imediatamente.
- Adiciona uma referência ao projeto em qualquer formato de referência está em uso. Referências subsequentemente aparecem no Gerenciador de soluções e o arquivo de formato de referência aplicáveis. No entanto, observe que, com PackageReference, você precisa salvar o projeto para ver as alterações no arquivo de projeto diretamente.
- Armazena em cache o pacote:
    - PackageReference: pacote é armazenado em cache `%USERPROFILE%\.nuget\packages` e o bloqueio de arquivos ou seja, `project.assets.json` é atualizada.
    - `packages.config`: cria um `packages` pasta na raiz da solução e cópias o pacote de arquivos em uma subpasta dentro dele. O `package.config` arquivo está atualizado.
- Atualizações `app.config` e/ou `web.config` se o pacote usa [transformações de arquivos de origem e configuração](../create-packages/source-and-config-file-transformations.md).
- Instala todas as dependências, se ainda não estiverem presentes no projeto. Isso pode atualizar versões de pacote no processo, conforme descrito em [resolução de dependência](../consume-packages/dependency-resolution.md).
- Exibe o arquivo do pacote Leiame, se disponível, em uma janela do Visual Studio.

> [!Tip]
> Uma das principais vantagens de instalação de pacotes com o `Install-Package` comando no console do é o que adiciona uma referência ao projeto, como se você usou o Gerenciador de pacotes UI. Em contraste, o `nuget install` comando CLI apenas baixa o pacote e não adiciona automaticamente uma referência.

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

- Remove as referências ao pacote do projeto (e qualquer formato de referência está em uso). As referências não aparecem mais no Gerenciador de soluções. (Talvez seja necessário recompilar o projeto para vê-lo removido o **Bin** pasta.)
- Reverte as alterações feitas `app.config` ou `web.config` quando o pacote foi instalado.
- Dependências de remove anteriormente instalado se não há pacotes restantes usam essas dependências.

> [!Tip]
> Como `Install-Package`, o `Uninstall-Package` comando tem o benefício de referências do projeto, ao contrário de `nuget uninstall` comando CLI.

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

Além disso, se estiver faltando o Gerenciador de pacotes do NuGet no Visual Studio 2015 e versões anteriores, verifique **Ferramentas > extensões e atualizações...**  e procure a extensão do Gerenciador de pacotes do NuGet. Se não for possível usar o instalador de extensões do Visual Studio, você pode baixar a extensão diretamente do [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

O Console do Gerenciador de pacote não está atualmente disponível com o Visual Studio para Mac. No entanto, os comandos equivalentes, estão disponíveis por meio de [NuGet CLI](nuget-exe-CLI-reference.md). Visual Studio para Mac tem uma interface de usuário para gerenciar pacotes NuGet. Consulte [incluindo NuGet um pacote em seu projeto](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).

O Console do Gerenciador de pacote não está incluído no código do Visual Studio.

## <a name="extending-the-package-manager-console"></a>Estendendo o Package Manager Console

Alguns pacotes instalam novos comandos do console. Por exemplo, `MvcScaffolding` cria os comandos `Scaffold` mostrado abaixo, que gera os controladores do ASP.NET MVC e modos de exibição:

![Instalar e usar MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Configurando um perfil de PowerShell do NuGet

Um perfil do PowerShell permite disponibilizar comandos usados com frequência, sempre que você usar o PowerShell. O NuGet dá suporte a um perfil específico do NuGet normalmente encontrado no seguinte local:

```
%UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Para localizar o perfil, digite `$profile` no console:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Para obter mais detalhes, consulte [perfis do Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).
