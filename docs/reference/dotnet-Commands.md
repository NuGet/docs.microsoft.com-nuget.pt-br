---
title: comandos do NuGet da CLI dotnet
description: Uma referência curta para comandos relacionados ao NuGet usando a interface de linha de comando dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327483"
---
# <a name="dotnet-cli-commands"></a>comandos da CLI dotnet

A `dotnet` CLI (interface de linha de comando), que é executada no Windows, Mac os X e Linux, fornece vários comandos essenciais, como instalação, restauração e publicação de pacotes. Se dotnet atender às suas necessidades, não será necessário usar `nuget.exe`.

Para obter exemplos de como usar esses comandos para consumir pacotes, consulte [instalar e gerenciar pacotes usando a CLI do dotnet](../consume-packages/install-use-packages-dotnet-cli.md). Para obter exemplos de como usar esses comandos para criar pacotes, consulte [criar e publicar um pacote usando a CLI dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Para obter a referência de comando `dotnet` completa na CLI, consulte [ferramentas de interface de linha de comando (CLI) do .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Consumo de pacote

- [**dotnet adicionar pacote**](/dotnet/core/tools/dotnet-add-package): Adiciona uma referência de pacote ao arquivo de projeto e, `dotnet restore` em seguida, é executado para instalar o pacote.
- [**dotnet remover pacote**](/dotnet/core/tools/dotnet-remove-package): Remove uma referência de pacote do arquivo de projeto.
- [**dotnet Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restaura as dependências e as ferramentas de um projeto. No NuGet 4.0 em diante, isso executa o mesmo código que `nuget restore`.
- [**locais do NuGet do dotnet**](/dotnet/core/tools/dotnet-nuget-locals): Lista os locais das pastas *global-Packages*, *http-cache*e *Temp* e limpa o conteúdo dessas pastas.
- [**dotnet New nugetconfig**](/dotnet/core/tools/dotnet-new): Cria um [`nuget.config`](../reference/nuget-config-file.md) arquivo para configurar o comportamento do NuGet.

## <a name="package-creation"></a>Criação de pacote

- [**pacote dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Empacota o código em um pacote NuGet.
- [**Push NuGet do dotnet**](/dotnet/core/tools/dotnet-nuget-push): Publica um pacote em um servidor NuGet. Aplicável a [servidores nuget](../hosting-packages/overview.md)nuget.org, Azure Artifacts e de terceiros.
- [**exclusão do NuGet do dotnet**](/dotnet/core/tools/dotnet-nuget-delete): Exclui ou deslista um pacote de um servidor NuGet. Aplicável a [servidores nuget](../hosting-packages/overview.md)nuget.org, Azure Artifacts e de terceiros.
