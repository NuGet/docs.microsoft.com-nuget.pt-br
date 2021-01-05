---
title: comandos do NuGet da CLI dotnet
description: Uma referência curta para comandos relacionados ao NuGet usando a interface de linha de comando dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 87cb3c8153931a0917338de9f7001406b5e12dfc
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699820"
---
# <a name="dotnet-cli-commands"></a>Comandos da CLI do dotnet

A `dotnet` CLI (interface de linha de comando), que é executada no Windows, Mac os X e Linux, fornece vários comandos essenciais, como instalação, restauração e publicação de pacotes. Se dotnet atender às suas necessidades, não será necessário usar `nuget.exe` .

Para obter exemplos de como usar esses comandos para consumir pacotes, consulte [instalar e gerenciar pacotes usando a CLI do dotnet](../consume-packages/install-use-packages-dotnet-cli.md). Para obter exemplos de como usar esses comandos para criar pacotes, consulte [criar e publicar um pacote usando a CLI dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Para obter a referência de comando completa na `dotnet` CLI, consulte [ferramentas de interface de linha de comando (CLI) do .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Consumo de pacote

- [**dotnet adicionar pacote**](/dotnet/core/tools/dotnet-add-package): adiciona uma referência de pacote ao arquivo de projeto e, em seguida, é executado `dotnet restore` para instalar o pacote.
- [**dotnet remover pacote**](/dotnet/core/tools/dotnet-remove-package): Remove uma referência de pacote do arquivo de projeto.
- [**dotnet Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaura as dependências e as ferramentas de um projeto. No NuGet 4.0 em diante, isso executa o mesmo código que `nuget restore`.
- [**dotnet NuGet locais**](/dotnet/core/tools/dotnet-nuget-locals): lista os locais das pastas *global-Packages*, *http-cache* e *Temp* e limpa o conteúdo dessas pastas.
- [**dotnet New nugetconfig**](/dotnet/core/tools/dotnet-new): cria um [`nuget.config`](../reference/nuget-config-file.md) arquivo para configurar o comportamento do NuGet.

## <a name="package-creation"></a>Criação de pacote

- [**dotnet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): compacta o código em um pacote NuGet.
- [**Push NuGet do dotnet**](/dotnet/core/tools/dotnet-nuget-push): publica um pacote em um servidor NuGet. Aplicável a [servidores nuget](../hosting-packages/overview.md)nuget.org, Azure Artifacts e de terceiros.
- [**dotnet NuGet Delete**](/dotnet/core/tools/dotnet-nuget-delete): exclui ou deslista um pacote de um servidor NuGet. Aplicável a [servidores nuget](../hosting-packages/overview.md)nuget.org, Azure Artifacts e de terceiros.
- [**verificar NuGet do dotnet**](/dotnet/core/tools/dotnet-nuget-verify): verifica um pacote NuGet assinado.
