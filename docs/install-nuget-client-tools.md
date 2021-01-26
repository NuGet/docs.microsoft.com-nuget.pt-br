---
title: Instalar as ferramentas de cliente do NuGet
description: Diretrizes sobre como instalar as ferramentas de cliente, o dotnet e a CLI (interface de linha de comando) do nuget e o Gerenciador de Pacotes para o Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 06/20/2019
ms.topic: quickstart
ms.openlocfilehash: 0e3938fc1ac748285ba26541a7d4e907c9a64156
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775901"
---
# <a name="install-nuget-client-tools"></a>Instalar ferramentas de cliente do NuGet

> **Procurando instalar um pacote? Veja [maneiras de instalar pacotes NuGet](consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).**

Para trabalhar com o NuGet, como um consumidor ou criador de pacotes, você pode usar ferramentas de CLI (interface de linha de comando), bem como os recursos do NuGet no Visual Studio. Este artigo descreve brevemente os recursos das várias ferramentas, como instalá-las e uma comparação da [disponibilidade de recursos](#feature-availability). Para começar a usar o NuGet para consumir pacotes, confira [Instalar e usar um pacote (CLI dotnet)](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) e [Instalar e usar um pacote (Visual Studio)](quickstart/install-and-use-a-package-in-visual-studio.md). Para começar a criar pacotes do NuGet, confira [Criar e publicar um pacote do NET Standard (CLI do dotnet)](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) e [Criar e publicar um pacote do NET Standard (Visual Studio)](quickstart/create-and-publish-a-package-using-visual-studio.md).

| Ferramenta&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Descrição | Download&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | Ferramenta CLI para bibliotecas .NET Core e .NET Standard e qualquer [projeto no estilo SDK](resources/check-project-format.md), como aquele direcionado ao .NET Framework. Incluído com o SDK do .NET Core e fornece os principais recursos do NuGet em todas as plataformas. No Visual Studio 2017 em diante, a CLI do dotnet é instalada automaticamente com qualquer carga de trabalho relacionada ao .NET Core.| [SDK do .NET Core](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Ferramenta de CLI para bibliotecas .NET Framework e para qualquer [projeto de estilo não SDK](resources/check-project-format.md), como um que tenha como destino bibliotecas .NET Standard. Fornece todos os recursos do NuGet no Windows e a maioria dos recursos no Mac e Linux quando executado em Mono. | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | No Windows, o **Gerenciador de pacotes NuGet** está incluído no Visual Studio 2012 e posterior. O Visual Studio fornece a [interface do usuário do Gerenciador de Pacotes](consume-packages/install-use-packages-visual-studio.md) e o [Console do Gerenciador de Pacotes](consume-packages/install-use-packages-powershell.md), por meio dos quais você pode executar a maioria das operações do NuGet. | [Visual Studio](https://www.visualstudio.com/downloads/) |
| [Visual Studio para Mac](/visualstudio/mac/nuget-walkthrough) | No Mac, determinados recursos do NuGet são internos diretamente. O console do Gerenciador de pacotes não está disponível no momento. Para outros recursos, use as ferramentas da CLI `dotnet.exe` ou `nuget.exe`.  | [Visual Studio para Mac](https://visualstudio.microsoft.com/vs/mac/) |
| [Visual Studio Code](https://code.visualstudio.com/docs) | No Windows, Mac ou Linux, os recursos do NuGet estão disponíveis por meio de extensões do Marketplace ou usam as `dotnet.exe` ferramentas da CLI do ou do `nuget.exe` . | [Visual Studio Code](https://code.visualstudio.com/Download/)|

A [CLI do MSBuild](reference/msbuild-targets.md) também fornece a capacidade de restaurar e criar pacotes, que é útil principalmente em servidores de compilação. O MSBuild não é uma ferramenta para fins gerais para trabalhar com o NuGet.

Os comandos do Console do Gerenciador de Pacotes funcionam apenas dentro do Visual Studio no Windows e não em outros ambientes de PowerShell.

## <a name="visual-studio"></a>Visual Studio
### <a name="install-on-visual-studio-2017-and-newer"></a>Instalar no Visual Studio 2017 e mais recente
No Visual Studio 2017 em diante, o instalador inclui o Gerenciador de Pacotes NuGet com qualquer carga de trabalho que utilize o .NET. Para instalá-lo separadamente ou para verificar se o Gerenciador de Pacotes está instalado, execute o instalador do Visual Studio e marque a opção em **Componentes Individuais > Ferramentas de código > Gerenciador de pacotes NuGet**.

### <a name="install-on-visual-studio-2015-and-older"></a>Instalar no Visual Studio 2015 e mais antigo
As extensões do NuGet para Visual Studio 2013 e 2015 podem ser baixadas de [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) .

Para o Visual Studio 2010 e versões anteriores, instale a extensão "Gerenciador de Pacotes NuGet para Visual Studio". Observe que, se você não conseguir ver a extensão na primeira página dos resultados da pesquisa, tente alterar a lista suspensa classificar por para "maioria dos downloads" ou uma classificação alfabética.

## <a name="cli-tools"></a>Ferramentas da CLI
Você pode usar a `dotnet` CLI ou a `nuget.exe` CLI para dar suporte aos recursos do NUGET no IDE. A CLI `dotnet` é instalada com algumas cargas de trabalho do Visual Studio, como .NET Core. A CLI `nuget.exe` deve ser instalada separadamente, como descrito anteriormente.

As duas ferramentas da CLI do NuGet são `dotnet.exe` e `nuget.exe`. Confira [disponibilidade de recursos](#feature-availability) para obter uma comparação.

* Para direcionar para o .NET Core ou o .NET Standard, use a CLI do dotnet. A CLI `dotnet` é necessária para o formato de projeto no estilo do SDK, que usa o [atributo do SDK](/dotnet/core/tools/csproj#additions).
* Para definir o .NET Framework como destino (somente projeto no estilo não SDK), use a CLI `nuget.exe`. Se o projeto for migrado do `packages.config` para o PackageReference, use a CLI do dotnet.

### <a name="dotnetexe-cli"></a>CLI do dotnet.exe

A CLI do .NET Core 2.0, `dotnet.exe`, funciona em todas as plataformas (Windows, Mac e Linux) e fornece os principais recursos do NuGet, como instalação, restauração e publicação de pacotes. `dotnet` fornece integração direta com os arquivos de projeto do .NET Core (como `.csproj`), o que é útil na maioria dos cenários. `dotnet` também é compilado diretamente para cada plataforma, e não exige a instalação do Mono.

Instalação:

- Em computadores de desenvolvedor, instale o [SDK do .NET Core](https://aka.ms/dotnetcoregs). No Visual Studio 2017 em diante, a CLI do dotnet é instalada automaticamente com qualquer carga de trabalho relacionada ao .NET Core.
- Para servidores de compilação, siga as instruções em [Usar o SDK do .NET Core e ferramentas na Integração contínua](/dotnet/core/tools/using-ci-with-cli).

Para saber como usar comandos básicos com a CLI do dotnet, confira [Instalar e usar pacotes usando a CLI do dotnet](consume-packages/install-use-packages-dotnet-cli.md).

### <a name="nugetexe-cli"></a>CLI do nuget.exe

A CLI do `nuget.exe`, `nuget.exe`, é o utilitário de linha de comando do Windows que fornece todas as funcionalidades do NuGet; ela também pode ser executada no Mac OSX e no Linux usando o [Mono](https://www.mono-project.com/docs/getting-started/install/) com algumas limitações.

Para saber como usar comandos básicos com a CLI do `nuget.exe`, confira [Instalar e usar pacotes usando a CLI do nuget.exe](consume-packages/install-use-packages-nuget-cli.md).

Instalação:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Use `nuget update -self` no Windows para atualizar o nuget.exe existente para a versão mais recente.

> [!Note]
> A CLI do NuGet mais recente recomendada está sempre disponível em `https://dist.nuget.org/win-x86-commandline/latest/nuget.exe`. Para fins de compatibilidade com sistemas mais antigos de integração contínua, uma URL anterior, `https://nuget.org/nuget.exe`, atualmente fornece a [ferramenta da CLI 2.8.6 preterida](https://github.com/NuGet/NuGetGallery/issues/5381).

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

## <a name="upcoming-features"></a>Recursos futuros
Se você quiser visualizar os próximos recursos do NuGet, instale uma [visualização do Visual Studio](https://www.visualstudio.com/vs/preview/), que funciona lado a lado com as versões estáveis do Visual Studio. Para relatar problemas ou compartilhar ideias para versões prévias, abra um problema no [repositório GitHub do NuGet](https://github.com/Nuget/Home/issues).

### <a name="related-topics"></a>Tópicos relacionados

- [Instalar e gerenciar pacotes usando o Visual Studio](consume-packages/install-use-packages-visual-studio.md)
- [Instalar e gerenciar pacotes usando o PowerShell](consume-packages/install-use-packages-powershell.md)
- [Instalar e gerenciar pacotes usando a CLI do dotnet](consume-packages/install-use-packages-dotnet-cli.md)
- [Instalar e gerenciar pacotes usando a CLI do nuget.exe](consume-packages/install-use-packages-nuget-cli.md)
- [Referência do PowerShell do Console do Gerenciador de Pacotes](reference/powershell-reference.md)
- [Criando um pacote](create-packages/creating-a-package.md)
- [Publicando um pacote](nuget-org/publish-a-package.md)

Os desenvolvedores que trabalham no Windows também podem explorar o [Explorador de Pacotes NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), uma ferramenta autônoma e de software livre para explorar, criar e editar visualmente os pacotes NuGet. Por exemplo, é muito útil fazer alterações experimentais em uma estrutura de pacote sem recompilar o pacote.
