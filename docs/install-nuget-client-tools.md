---
title: Instalar as ferramentas de cliente do NuGet
description: Diretrizes sobre como instalar as ferramentas de cliente, o dotnet e a CLI (interface de linha de comando) do nuget e o Gerenciador de Pacotes para o Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 6e3011493b7b89bc43cd9a267aea7fd32d668cec
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426564"
---
# <a name="install-nuget-client-tools"></a>Instalar ferramentas de cliente do NuGet

> **Deseja instalar um pacote? Confira [Formas de instalar pacotes NuGet](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).**

Para trabalhar com o NuGet, como um consumidor ou criador de pacotes, você pode usar ferramentas de CLI (interface de linha de comando), bem como os recursos do NuGet no Visual Studio. Este artigo descreve brevemente os recursos das várias ferramentas, como instalá-las e uma comparação da [disponibilidade de recursos](#feature-availability). Para começar a usar o NuGet para consumir pacotes, confira [Instalar e usar um pacote (CLI do .NET)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) e [Instalar e usar um pacote (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). Para começar a criar pacotes do NuGet, confira [Criar e publicar um pacote do NET Standard (CLI do dotnet)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) e [Criar e publicar um pacote do NET Standard (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md).

| Ferramenta&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | DESCRIÇÃO | Download&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Ferramenta CLI para bibliotecas .NET Core e .NET Standard e qualquer projeto no estilo SDK, como aquele direcionado ao .NET Framework (confira [Atributo SDK](/dotnet/core/tools/csproj#additions)). Incluído com o SDK do .NET Core e fornece os principais recursos do NuGet em todas as plataformas. | [SDK do .NET Core](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Ferramenta CLI para bibliotecas .NET Framework e projetos no estilo não SDK direcionados a bibliotecas .NET Standard. Fornece todos os recursos do NuGet no Windows e a maioria dos recursos no Mac e Linux quando executado em Mono. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | No Windows, fornece funcionalidades do NuGet por meio da interface do usuário do Gerenciador de Pacotes e do Console do Gerenciador de Pacotes, incluídos com as cargas de trabalho relacionadas ao .NET. No Mac, oferece alguns recursos por meio da interface do usuário. No Visual Studio Code, recursos do NuGet são fornecidos por meio de extensões. | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

A [CLI do MSBuild](reference/msbuild-targets.md) também fornece a capacidade de restaurar e criar pacotes, que é útil principalmente em servidores de compilação. O MSBuild não é uma ferramenta para fins gerais para trabalhar com o NuGet.

## <a name="cli-tools"></a>Ferramentas da CLI

As duas ferramentas da CLI do NuGet são `dotnet.exe` e `nuget.exe`. Confira [disponibilidade de recursos](#feature-availability) para obter uma comparação.

* Para direcionar para o .NET Core ou o .NET Standard, use a CLI do dotnet. A CLI do dotnet é necessária para o formato de projeto no estilo do SDK, que usa o [atributo do SDK](/dotnet/core/tools/csproj#additions).
* Para definir o .NET Framework como destino (somente projeto no estilo não SDK), use a `nuget.exe CLI`. Se o projeto for migrado para `packages.config`, use a CLI do dotnet.

### <a name="dotnetexe-cli"></a>CLI do dotnet.exe

A CLI do .NET Core 2.0, `dotnet.exe`, funciona em todas as plataformas (Windows, Mac e Linux) e fornece os principais recursos do NuGet, como instalação, restauração e publicação de pacotes. `dotnet` fornece integração direta com os arquivos de projeto do .NET Core (como `.csproj`), o que é útil na maioria dos cenários. `dotnet` também é compilado diretamente para cada plataforma, e não exige a instalação do Mono.

Instalação:

- Em computadores de desenvolvedor, instale o [SDK do .NET Core](https://aka.ms/dotnetcoregs).
- Para servidores de compilação, siga as instruções em [Usar o SDK do .NET Core e ferramentas na Integração contínua](/dotnet/core/tools/using-ci-with-cli).

Para saber como usar comandos básicos com a CLI do dotnet, confira [Instalar e usar pacotes usando a CLI do dotnet](consume-packages/install-use-packages-dotnet-cli.md).

### <a name="nugetexe-cli"></a>CLI do nuget.exe

A CLI do `nuget.exe`, `nuget.exe`, é o utilitário de linha de comando do Windows que fornece todas as funcionalidades do NuGet; ela também pode ser executada no Mac OSX e no Linux usando o [Mono](http://www.mono-project.com/docs/getting-started/install/) com algumas limitações.

Instalação:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Use `nuget update -self` no Windows para atualizar o nuget.exe existente para a versão mais recente.

Para saber como usar comandos básicos com a CLI do `nuget.exe`, confira [Instalar e usar pacotes usando a CLI do nuget.exe](consume-packages/install-use-packages-nuget-cli.md).

> [!Note]
> A CLI do NuGet mais recente recomendada está sempre disponível em `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`. Para fins de compatibilidade com sistemas mais antigos de integração contínua, uma URL anterior, `https://nuget.org/nuget.exe`, atualmente fornece a [ferramenta da CLI 2.8.6 preterida](https://github.com/NuGet/NuGetGallery/issues/5381).

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code: os recursos do NuGet estão disponíveis por meio de extensões do marketplace, ou use as ferramentas de CLI `dotnet.exe` ou `nuget.exe`.

- Visual Studio para Mac: os recursos NuGet são incorporados diretamente. Consulte [Incluindo um pacote do NuGet no seu projeto](/visualstudio/mac/nuget-walkthrough) para ver uma explicação passo a passo. Para outros recursos, use as ferramentas da CLI `dotnet.exe` ou `nuget.exe`.

- Visual Studio no Windows: o **Gerenciador de Pacotes NuGet** é incluído com o Visual Studio 2012 e posteriores. O Visual Studio fornece a [interface do usuário do Gerenciador de Pacotes](tools/package-manager-ui.md) e o [Console do Gerenciador de Pacotes](tools/package-manager-console.md), por meio dos quais você pode executar a maioria das operações do NuGet.
  - No Visual Studio 2017 em diante, o instalador inclui o Gerenciador de Pacotes NuGet com qualquer carga de trabalho que utilize o .NET. Para instalá-lo separadamente ou para verificar se o Gerenciador de Pacotes está instalado, execute o instalador do Visual Studio e marque a opção em **Componentes Individuais > Ferramentas de código > Gerenciador de pacotes NuGet**.
  - A IU e o Console do Gerenciador de Pacotes são exclusivos para o Visual Studio no Windows. Eles não estão disponíveis no Visual Studio para Mac no momento.
  - Uma ferramenta de CLI é necessário para dar suporte a recursos do NuGet no IDE. Você pode usar a CLI `dotnet` ou `nuget.exe`. A CLI `dotnet` é instalada com algumas cargas de trabalho do Visual Studio, como .NET Core. A CLI `nuget.exe` deve ser instalada separadamente, como descrito anteriormente.
  - Os comandos do Console do Gerenciador de Pacotes funcionam apenas dentro do Visual Studio no Windows e não em outros ambientes de PowerShell.
  - Para o Visual Studio 2010 e versões anteriores, instale a extensão "Gerenciador de Pacotes NuGet para Visual Studio".
  - As extensões do NuGet para Visual Studio 2013 e 2015 também podem ser baixadas de [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).
  - Se você quiser visualizar futuros recursos do NuGet, instale o [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), que funciona lado a lado com as versões estáveis do Visual Studio. Para relatar problemas ou compartilhar ideias para versões prévias, abra um problema no [repositório GitHub do NuGet](https://github.com/Nuget/Home/issues).

## <a name="feature-availability"></a>Disponibilidade de recursos

| Recurso | CLI do dotnet | CLI do nuget (Windows) | CLI do nuget (Mono) | Visual Studio (Windows) | Visual Studio para Mac |
| --- | --- | --- | --- | --- | --- |
| Pesquisar pacotes |  | &#10004; | &#10004; | &#10004; | &#10004; |
| Instalar/desinstalar pacotes | &#10004; | &#10004;(1) | &#10004; | &#10004; | &#10004; |
| Atualizar pacotes | &#10004; | &#10004; | | &#10004; | &#10004; |
| Restaurar pacotes | &#10004; | &#10004; | &#10004;(2) | &#10004; | &#10004; |
| Gerenciar feeds de pacote (origens) | | &#10004; | &#10004; | &#10004; | &#10004; |
| Gerenciar pacotes em um feed | &#10004; | &#10004; | &#10004; | | |
| Definir chaves de API para feeds | | &#10004; | &#10004; | | |
| Criar pacotes(3) | &#10004; | &#10004; | &#10004;(4) | &#10004; | |
| Publicar pacotes | &#10004; | &#10004; | &#10004; | &#10004; |  |
| Replicar pacotes |  | &#10004; | &#10004; | | |
| Gerenciar *global-package* e pastas de cache | &#10004; | &#10004; | &#10004; | | |
| Gerenciar a configuração do NuGet | | &#10004; | &#10004; | | |

(1) Não afeta os arquivos de projeto; em vez disso, use `dotnet.exe`.

(2) Funciona somente com o arquivo `packages.config` e não com os arquivos de solução (`.sln`).

(3) Vários recursos avançados de pacote são disponibilizados por meio da CLI apenas quando não são representados nas ferramentas de interface do usuário do Visual Studio.

(4) Funciona com arquivos `.nuspec`, mas não com arquivos de projeto.

### <a name="related-topics"></a>Tópicos relacionados

- [Instalar e gerenciar pacotes usando o Visual Studio](tools/package-manager-ui.md)
- [Instalar e gerenciar pacotes usando o PowerShell](tools/package-manager-console.md)
- [Instalar e gerenciar pacotes usando a CLI do dotnet](consume-packages/install-use-packages-dotnet-cli.md)
- [Instalar e gerenciar pacotes usando a CLI do nuget.exe](consume-packages/install-use-packages-nuget-cli.md)
- [Referência do PowerShell do Console do Gerenciador de Pacotes](tools/powershell-reference.md)
- [Criando um pacote](create-packages/creating-a-package.md)
- [Publicando um pacote](nuget-org/publish-a-package.md)

Os desenvolvedores que trabalham no Windows também podem explorar o [Explorador de Pacotes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), uma ferramenta autônoma e de software livre para explorar, criar e editar visualmente os pacotes NuGet. Por exemplo, é muito útil fazer alterações experimentais em uma estrutura de pacote sem recompilar o pacote.
