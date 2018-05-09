---
title: Instalar as ferramentas de cliente do NuGet
description: Diretrizes sobre como instalar as ferramentas de cliente, o dotnet e a CLI (interface de linha de comando) do nuget e o Gerenciador de Pacotes para o Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 04/09/2018
ms.topic: quickstart
ms.openlocfilehash: 6681c910768bc705f5e09340e04e4d368fde5efe
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2018
---
# <a name="installing-nuget-client-tools"></a>Instalar as ferramentas de cliente do NuGet

> **Deseja instalar um pacote? Confira [Formas de instalar pacotes NuGet](consume-packages/ways-to-install-a-package.md).**

Para trabalhar com o NuGet, como um consumidor ou criador de pacotes, você pode usar [ferramentas de CLI (interface de linha de comando)](#cli-tools), bem como os [recursos do NuGet no Visual Studio](#visual-studio). Este artigo descreve brevemente os recursos das várias ferramentas, como instalá-las e uma comparação da [disponibilidade de recursos](#feature-availability). Para começar a usar o NuGet para consumir pacotes, confira [Instalar e usar um pacote (CLI do .NET)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) e [Instalar e usar um pacote (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). Para começar a criar pacotes do NuGet, confira [Criar e publicar um pacote do NET Standard (CLI do dotnet)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) e [Criar e publicar um pacote do NET Standard (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md).

| Ferramenta&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Descrição | Download&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Incluído com o SDK do .NET Core e fornece os principais recursos do NuGet em todas as plataformas. | [SDK do .NET Core](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Fornece todos os recursos do NuGet no Windows e a maioria dos recursos no Mac e Linux quando executado em Mono. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | No Windows, fornece funcionalidades do NuGet por meio da interface do usuário do Gerenciador de Pacotes e do Console do Gerenciador de Pacotes, incluídos com as cargas de trabalho relacionadas ao .NET. No Mac, oferece alguns recursos por meio da interface do usuário. No Visual Studio Code, recursos do NuGet são fornecidos por meio de extensões. | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

A [CLI do MSBuild](reference/msbuild-targets.md) também fornece a capacidade de restaurar e criar pacotes, que é útil principalmente em servidores de compilação. O MSBuild não é uma ferramenta para fins gerais para trabalhar com o NuGet.

## <a name="cli-tools"></a>Ferramentas da CLI

As duas ferramentas da CLI do NuGet são `dotnet.exe` e `nuget.exe`. Confira [disponibilidade de recursos](#feature-availability) para obter uma comparação.

### <a name="dotnetexe-cli"></a>CLI do dotnet.exe

A CLI do .NET Core 2.0, `dotnet.exe`, funciona em todas as plataformas (Windows, Mac e Linux) e fornece os principais recursos do NuGet, como instalação, restauração e publicação de pacotes. `dotnet` fornece integração direta com os arquivos de projeto do .NET Core (como `.csproj`), o que é útil na maioria dos cenários. `dotnet` também é compilado diretamente para cada plataforma, e não exige a instalação do Mono.

Instalação:

- Em computadores de desenvolvedor, instale o [SDK do .NET Core](https://aka.ms/dotnetcoregs).
- Para servidores de compilação, siga as instruções em [Usar o SDK do .NET Core e ferramentas na Integração contínua](/dotnet/core/tools/using-ci-with-cli).

Para saber mais, confira [Ferramentas da interface de linha de comando do .NET Core](/dotnet/core/tools/index?tabs=netcore2x#tabpanel_fXL5YCOYDa_netcore2x).

### <a name="nugetexe-cli"></a>CLI do nuget.exe

A CLI do NuGet, `nuget.exe`, é o utilitário de linha de comando do Windows que fornece todos os recursos do NuGet; ele também pode ser executado no Mac OSX e Linux usando [Mono](http://www.mono-project.com/docs/getting-started/install/) com algumas limitações. Ao contrário de `dotnet`, a CLI do `nuget.exe` não afeta os arquivos de projeto e não atualiza `packages.config` durante a instalação de pacotes.

Instalação:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Use `nuget update -self` no Windows para atualizar o nuget.exe existente para a versão mais recente.

> [!Note]
> A CLI do NuGet mais recente recomendada está sempre disponível em `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`. Para fins de compatibilidade com sistemas mais antigos de integração contínua, uma URL anterior, `https://nuget.org/nuget.exe`, atualmente fornece a [ferramenta da CLI 2.8.6 preterida](https://github.com/NuGet/NuGetGallery/issues/5381).

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code: os recursos do NuGet estão disponíveis por meio de extensões do marketplace, ou use as ferramentas de CLI `dotnet.exe` ou `nuget.exe`.

- Visual Studio para Mac: os recursos NuGet são incorporados diretamente. Consulte [Incluindo um pacote do NuGet no seu projeto](/visualstudio/mac/nuget-walkthrough) para ver uma explicação passo a passo. Para outros recursos, use as ferramentas da CLI `dotnet.exe` ou `nuget.exe`.

- Visual Studio no Windows: o **Gerenciador de Pacotes NuGet** está incluído com o Visual Studio 2012 e posterior. O Gerenciador de Pacotes fornece a [IU do Gerenciador de Pacotes](tools/package-manager-ui.md) e o [Console do Gerenciador de Pacote](tools/package-manager-console.md), por meio dos quais você pode executar a maioria das operações do NuGet.
  - O instalador do Visual Studio 2017 inclui o Gerenciador de Pacotes do NuGet com qualquer carga de trabalho que utiliza o .NET. Para instalar separadamente ou para verificar se o Gerenciador de Pacotes está instalado, execute o instalador do Visual Studio 2017 e marque a opção em **Componentes individuais > Ferramentas de código > Gerenciador de pacotes do NuGet**.
  - A IU e o Console do Gerenciador de Pacotes são exclusivos para o Visual Studio no Windows. Eles não estão disponíveis no Visual Studio para Mac no momento.
  - O Visual Studio não inclui automaticamente a CLI do `nuget.exe`, que deve ser instalada separadamente, conforme descrito anteriormente.
  - Os comandos do Console do Gerenciador de Pacotes funcionam apenas dentro do Visual Studio no Windows e não em outros ambientes de PowerShell.
  - Para o Visual Studio 2010 e versões anteriores, instale a extensão "Gerenciador de Pacotes NuGet para Visual Studio".
  - As extensões do NuGet para Visual Studio 2013 e 2015 também podem ser baixadas de [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).
  - Se você quiser visualizar futuros recursos do NuGet, instale o [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), que funciona lado a lado com as versões estáveis do Visual Studio. Para relatar problemas ou compartilhar ideias para versões prévias, abra um problema no [repositório GitHub do NuGet](https://github.com/Nuget/Home/issues).

## <a name="feature-availability"></a>Disponibilidade de recursos

| Recurso | CLI do dotnet | CLI do nuget (Windows) | CLI do nuget (Mono) | Visual Studio (Windows) | Visual Studio para Mac |
| --- | --- | --- | --- | --- | --- |
| Pesquisar pacotes |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Instalar/desinstalar pacotes | &#10004;(1) | &#10004;(2) | &#10004; | &#10004; | &#10004; |
| Atualizar pacotes | &#10004; | &#10004; | | &#10004; | &#10004; |
| Restaurar pacotes | &#10004; | &#10004; | &#10004;(3) | &#10004; | &#10004; |
| Gerenciar feeds de pacote (origens) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Gerenciar pacotes em um feed | &#10004;(1) | &#10004; | &#10004; | | |
| Definir chaves de API para feeds | | &#10004; | &#10004; | | |
| Criar pacotes (4) | &#10004; | &#10004; | &#10004;(5) | &#10004; | |
| Publicar pacotes | &#10004;(1) | &#10004; | &#10004; | &#10004; |  |
| Replicar pacotes |  | &#10004; | &#10004; | | |
| Gerenciar *global-package* e pastas de cache | &#10004; | &#10004; | &#10004; | | |
| Gerenciar a configuração do NuGet | | &#10004; | &#10004; | | |

(1) Pacotes em nuget.org apenas

(2) Não afeta os arquivos de projeto, em vez disso use `dotnet.exe`.

(3) Funciona somente com o arquivo `packages.config` e não com os arquivos de solução (`.sln`).

(4) Vários recursos avançados de pacote são disponibilizados por meio da CLI apenas quando não são representados nas ferramentas de interface do usuário do Visual Studio.

(5) Funciona com arquivos `.nuspec`, mas não com arquivos de projeto.

### <a name="related-topics"></a>Tópicos relacionados

- [Comandos dotnet](tools/dotnet-commands.md)
- [Referência da CLI do NuGet](tools/nuget-exe-cli-reference.md)
- [Referência da interface do usuário do Gerenciador de Pacotes](tools/package-manager-ui.md)
- [Referência do Console do Gerenciador de Pacotes](tools/package-manager-console.md)
- [Referência do PowerShell do Console do Gerenciador de Pacotes](tools/powershell-reference.md)
- [Criando um pacote](create-packages/creating-a-package.md)
- [Publicando um pacote](create-packages/publish-a-package.md)

Os desenvolvedores que trabalham no Windows também podem explorar o [Explorador de Pacotes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), uma ferramenta autônoma e de software livre para explorar, criar e editar visualmente os pacotes NuGet. Por exemplo, é muito útil fazer alterações experimentais em uma estrutura de pacote sem recompilar o pacote.
