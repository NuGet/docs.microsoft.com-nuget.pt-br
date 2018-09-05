---
title: comandos do NuGet dotnet
description: Uma referência curta para comandos relacionados ao NuGet usando a interface de linha de comando dotnet.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: 88e058be674ecddc500665bfa3517f19acde0cd7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546310"
---
# <a name="dotnet-commands"></a>Comandos dotnet

O `dotnet` interface de linha de comando, que é executado no Windows, Mac OS X e Linux, fornece um número de comandos nuget.exe essenciais, como listado abaixo. Se dotnet satisfizer suas necessidades, não é necessário usar `nuget.exe`.

Para obter informações completas sobre `dotnet`, consulte [ferramentas de interface de linha de comando (CLI) do .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Consumo de pacote

- [**dotnet Adicionar pacote**](/dotnet/core/tools/dotnet-add-package): adiciona uma referência de pacote para o arquivo de projeto, em seguida, executa `dotnet restore` para instalar o pacote.
- [**remover o pacote dotnet**](/dotnet/core/tools/dotnet-remove-package): remove uma referência de pacote do arquivo de projeto.
- [**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaura as dependências e as ferramentas de um projeto. A partir do NuGet 4.0, ele é executado o mesmo código que `nuget restore`.
- [**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): lista os locais das *global-packages*, *http-cache*, e *temp* pastas e limpa o conteúdo de Essas pastas.

## <a name="package-creation"></a>Criação de pacote

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): empacota o código em um pacote do NuGet. A partir do NuGet 4.0, ele é executado o mesmo código que `nuget pack`.
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): envia um pacote a um servidor e os publica, aplicável para nuget.org, o Visual Studio Team Services e servidores NuGet de terceiros.
- [**Excluir nuget dotnet**](/dotnet/core/tools/dotnet-nuget-delete): exclui ou retira da lista um pacote de um host aplicável para nuget.org, o Visual Studio Team Services e servidores NuGet de terceiros.
