---
title: Instalar as ferramentas de cliente do NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: Diretrizes sobre como instalar as ferramentas de cliente, a CLI (interface de linha de comando) e o Gerenciador de Pacotes para o Visual Studio.
keywords: CLI do nuget.exe, ferramentas de cliente do NuGet, gerenciador de pacotes do NuGet, console do gerenciador de pacotes do NuGet, NuGet para Visual Studio, canal beta do NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1abb30458c9ebfb0ffb28be254efd9709a9627f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="installing-nuget-client-tools"></a>Instalar as ferramentas de cliente do NuGet

> [!Tip]
> **Deseja instalar um pacote? Consulte [Guia de início rápido – Usar um pacote](../Quickstart/Use-a-Package.md).**

Há duas ferramentas primárias disponíveis para ajudar você a compilar, publicar e consumir pacotes do NuGet:

1. A [**CLI do NuGet**](#nuget-cli) é o utilitário de linha de comando do Windows que fornece todos os recursos do NuGet; ele também pode ser executado no Mac OSX e Linux usando Mono ou por meio da CLI do .NET Core (`dotnet`).
1. O [**Gerenciador de Pacotes do NuGet no Visual Studio**](#nuget-package-manager-in-visual-studio) (somente Windows) é uma ferramenta de GUI para gerenciar pacotes e inclui um console do PowerShell por meio do qual você pode usar alguns comandos do NuGet diretamente no Visual Studio. A Interface do usuário e o Console do Gerenciador de Pacotes são incluídos no Visual Studio (no Windows) 2012 e posterior e podem ser instalados manualmente para versões anteriores.

    Com o Visual Studio para Mac, os recursos NuGet são incorporados diretamente. Consulte [Incluindo um pacote do NuGet no seu projeto](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough) para ver uma explicação passo a passo.

    No momento, o Visual Studio Code não tem suporte interno para o NuGet. Usar a CLI do NuGet ou a [CLI do dotnet](../Tools/dotnet-Commands.md).

A CLI do NuGet e o Gerenciador de Pacotes são compatíveis com as seguintes operações:

- Pesquisar pacotes
- Instalar pacotes
- Atualizar pacotes
- Desinstalar pacotes
- Restaurar os pacotes (interface do usuário somente no Gerenciador de Pacotes)
- Gerenciar as origens do NuGet

Os seguintes recursos são compatíveis somente com a CLI do NuGet:

- Gerenciar pacotes (nuget.org ou feed privado)
- Criar pacotes 
- Publicar pacotes
- Gerenciar o Nuget.Config
- Gerenciar o cache do NuGet
- Replicando um pacote

> [!Note]
> Outra boa ferramenta é o [Explorador de Pacotes do NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), uma ferramenta autônoma e de software livre para explorar, criar e editar visualmente os pacotes do NuGet. Por exemplo, é muito útil fazer alterações experimentais em uma estrutura de pacote sem a necessidade de recompilar o pacote a cada vez.
> A cadeia de ferramentas da [CLI do .NET Core](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) de multiplataforma, usada para desenvolver aplicativos do .NET Core, compatível com vários comandos do NuGet, como delete, locals, push, pack e restore. 

## <a name="nuget-cli"></a>CLI do NuGet

A interface de linha de comando do NuGet fornece acesso a todos os recursos do NuGet e pode ser executada no Windows, Mac OSX e Linux, conforme descrito nas seções a seguir.

### <a name="windows"></a>Windows

**Download direto:**

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> Com o NuGet 1.4 ou superior, você pode usar `nuget update -self` para atualizar seu nuget.exe existente para a versão mais recente.

**Outros métodos:**

- **Chocolatey**: instale o pacote [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) do Chocolatey usando o cliente do [Chocolatey](http://chocolatey.org). 

    ```ps
    choco install nuget.commandline
    ```

- **Visual Studio**: instale o pacote [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) do Console do Gerenciador de Pacotes no Visual Studio.

    > [!Note]
    > **Para usuários do NuGet 2.x**: devido a alterações significativas introduzidas no NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) aponta para a versão NuGet 2.x estável mais recente, a fim de impedir que os sistemas de integração contínua sejam potencialmente interrompidos.

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a>Mac OSX e Linux

No Mac OSX e Linux, há duas maneiras de executar a CLI do NuGet:

- Instale o [SDK do .NET Core](https://www.microsoft.com/net/download/core), que inclui os principais recursos do NuGet. Downloads também são listados em [github.com/dotnet/cli](https://github.com/dotnet/cli). Se você precisar de recursos mais completos, use a segunda opção abaixo para usar `nuget.exe` com o Mono.

- Instale [Mono](http://www.mono-project.com/docs/getting-started/install/) e, em seguida, use o executável `nuget.exe` de linha de comando do Windows (versão 3.2 e posterior) de [nuget.org/downloads](https://nuget.org/downloads). Executar o NuGet em Mono está sujeito às seguintes limitações:

    - Comandos testados que funcionam:
        - config
        - excluir
        - help
        - install
        - lista
        - push
        - setApiKey
        - origens
        - spec

    - Comandos que funcionam parcialmente:
        - pack: funciona com arquivos `.nuspec`, mas não com arquivos de projeto.
        - restore: funciona com arquivos `packages.config` e `project.json`, mas não com arquivos (`.sln`) da solução.

    - Comandos que não funcionam:
        - atualizar

### <a name="related-topics"></a>Tópicos relacionados

- [Referência da CLI do NuGet](../tools/nuget-exe-cli-reference.md)
- [Criando um pacote](../create-packages/creating-a-package.md)
- [Publicando um pacote](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a>Gerenciador de Pacotes do NuGet no Visual Studio

O Gerenciador de Pacotes do NuGet está incluído em todas as edições do Visual Studio no Windows 2012 e posterior. Ele inclui a interface do usuário do Gerenciador de Pacotes ([referência](../tools/package-manager-ui.md)) e o Console do Gerenciador de Pacotes por meio do qual você pode acessar as ferramentas que vêm com determinados pacotes ([referência](../tools/package-manager-console.md)).

O instalador do Visual Studio 2017 inclui o Gerenciador de Pacotes do NuGet com qualquer carga de trabalho que utiliza o .NET. Para instalar separadamente ou para verificar se o Gerenciador de Pacotes está instalado, execute o instalador do Visual Studio 2017 e marque a opção em **Componentes individuais > Ferramentas de código > Gerenciador de pacotes do NuGet**.

> [!Note]
> O console requer o [PowerShell 2.0](http://support.microsoft.com/kb/968929), que já estará instalado no Windows 7 ou superior e Windows Server 2008 R2 ou superior.
>
> Comandos do Console do Gerenciador de Pacotes também funcionam apenas dentro do Visual Studio no Windows. Use a CLI do NuGet fora do ambiente, incluindo com o Visual Studio para Mac e o Visual Studio Code.

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a>Instalação do Gerenciador de Pacotes para Visual Studio 2010 e anterior

*Essas etapas não são necessárias para o Visual Studio 2012 e versões posteriores, que já incluem o Gerenciador de Pacotes.*

1. No Visual Studio 2010 e versões anteriores, clique em **Ferramentas > Extensão e atualizações**.
1. Navegue até **Online**, pesquise “Gerenciador de Pacotes do NuGet para Visual Studio” e clique em **Baixar**.
1. Na caixa de diálogo Instalador, clique em **Instalar**.
1. Quando a instalação for concluída, reinicie o Visual Studio.

> [!Tip]
> Se você não conseguir usar a caixa de diálogo **Extensões e atualizações** no Visual Studio (por exemplo, se estiver bloqueado por um proxy), poderá baixar as extensões para o Visual Studio 2013 e 2015 diretamente no [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

### <a name="updating-the-package-manager"></a>Atualizando o Gerenciador de Pacotes

Para o Visual Studio 2015 Atualização 2 e posterior, o Gerenciador de Pacotes é atualizado automaticamente para a versão estável mais recente.

Para o Visual Studio 2015 Atualização 1 e anterior, selecione o comando **Ferramentas > Extensões e Atualizações** e clique na guia **Atualizações** para ver se uma nova versão do Gerenciador de Pacotes está disponível.  

### <a name="nuget-previews"></a>Visualizações do NuGet

Se você quiser visualizar futuros recursos do NuGet, instale o [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), que funciona lado a lado com as versões estáveis do Visual Studio.

Observe que o Canal Beta do NuGet anterior (`https://dotnet.myget.org/F/nuget-beta/vsix/`) para Visual Studio 2015 não é mais usado.

Para relatar problemas com qualquer versão do NuGet ou compartilhar ideias, abra um problema no [repositório GitHub do NuGet](https://github.com/Nuget/Home).

### <a name="related-topics"></a>Tópicos relacionados

- [Referência da interface do usuário do Gerenciador de Pacotes](../tools/package-manager-ui.md)
- [Referência do Console do Gerenciador de Pacotes](../tools/package-manager-console.md)
- [Referência do PowerShell do Console do Gerenciador de Pacotes](../tools/powershell-reference.md)