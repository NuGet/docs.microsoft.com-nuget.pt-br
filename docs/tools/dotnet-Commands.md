---
title: comandos de CLI NuGet dotnet
description: Uma referência curta para comandos relacionados ao NuGet usando a interface de linha de comando dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496475"
---
# <a name="dotnet-cli-commands"></a>comandos CLI do dotnet

O `dotnet` interface de linha de comando (CLI), que é executado no Windows, Mac OS X e Linux, fornece uma série de comandos essenciais, como instalação, restauração e publicação de pacotes. Se dotnet satisfizer suas necessidades, não é necessário usar `nuget.exe`.

Para obter exemplos de como usar esses comandos para consumir pacotes, consulte [instalar e gerenciar pacotes usando a CLI do dotnet](../consume-packages/install-use-packages-dotnet-cli.md). Para obter exemplos de como usar esses comandos para criar pacotes, consulte [criar e publicar um pacote usando a CLI do dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Para a referência de comando completo no `dotnet` CLI, consulte [ferramentas de interface de linha de comando (CLI) do .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Consumo de pacote

- [**dotnet Adicionar pacote**](/dotnet/core/tools/dotnet-add-package): Adiciona uma referência de pacote para o arquivo de projeto, em seguida, executa `dotnet restore` para instalar o pacote.
- [**remover o pacote dotnet**](/dotnet/core/tools/dotnet-remove-package): Remove uma referência de pacote do arquivo de projeto.
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restaura as dependências e as ferramentas de um projeto. A partir do NuGet 4.0, ele é executado o mesmo código que `nuget restore`.
- [**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lista os locais do *global-packages*, *http-cache*, e *temp* limpa o conteúdo dessas pastas e pastas.
- [**nugetconfig de novo dotnet**](/dotnet/core/tools/dotnet-new): Cria uma [ `nuget.config` ](../reference/nuget-config-file.md) arquivo para configurar o comportamento do NuGet.

## <a name="package-creation"></a>Criação de pacote

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Empacota o código em um pacote do NuGet.
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Publica um pacote em um servidor do NuGet. Aplicável para o nuget.org, artefatos do Azure, e [servidores de NuGet de terceiros](../hosting-packages/overview.md).
- [**Excluir nuget dotnet**](/dotnet/core/tools/dotnet-nuget-delete): Exclui ou retira da lista um pacote a partir de um servidor do NuGet. Aplicável para o nuget.org, artefatos do Azure, e [servidores de NuGet de terceiros](../hosting-packages/overview.md).
