---
title: comandos do NuGet dotnet
description: Uma referência curta para comandos relacionados NuGet usando a interface de linha de comando dotnet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: dd30c5d5e29ff7ef7c6622a9b93c32b908198d52
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816990"
---
# <a name="dotnet-commands"></a>Comandos dotnet

O `dotnet` interface de linha de comando, que é executado no Windows, Mac OS X e Linux, fornece um número de comandos nuget.exe essenciais, como listado abaixo. Se dotnet satisfizer suas necessidades, não é necessário usar `nuget.exe`.

Para obter informações completas sobre `dotnet`, consulte [ferramentas de interface de linha de comando (CLI) do .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Consumo de pacote

- [**dotnet Adicionar pacote**](/dotnet/core/tools/dotnet-add-package): adiciona uma referência de pacote para o arquivo de projeto e, em seguida, executa `dotnet restore` para instalar o pacote.
- [**dotnet remover pacote**](/dotnet/core/tools/dotnet-remove-package): remove uma referência de pacote do arquivo de projeto.
- [**restauração dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaura as dependências e as ferramentas de um projeto. A partir do NuGet 4.0, isso executará o mesmo código que `nuget restore`.
- [**dotnet nuget locais**](/dotnet/core/tools/dotnet-nuget-locals): lista de locais do *pacotes global*, *cache http*, e *temp* pastas e limpa o conteúdo de Essas pastas.

## <a name="package-creation"></a>Criação de pacote

- [**pacote de dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): pacotes de código em um pacote do NuGet. A partir do NuGet 4.0, isso executará o mesmo código que `nuget pack`.
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): envia um pacote para um servidor e o publica, aplicáveis a nuget.org, Visual Studio Team Services e servidores de NuGet de terceiros.
- [**Excluir dotnet nuget**](/dotnet/core/tools/dotnet-nuget-delete): exclui ou unlists um pacote de um host aplicável nuget.org, Visual Studio Team Services e servidores de NuGet de terceiros.
