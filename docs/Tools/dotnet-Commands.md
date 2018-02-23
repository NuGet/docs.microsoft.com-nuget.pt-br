---
title: comandos do NuGet dotNet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Uma referência curta para comandos relacionados NuGet usando a interface de linha de comando dotnet."
keywords: "comandos do NuGet dotnet, pacote dotnet, restauração dotnet, dotnet nuget locais, dotnet nuget push, dotnet nuget delete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2851938cd43b35454d8e4ad595fbd93229d4dd72
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/20/2018
---
# <a name="dotnet-commands"></a>comandos dotNet

O `dotnet` interface de linha de comando, que é executado no Windows, Mac OS X e Linux, fornece um número de comandos nuget.exe essenciais, como listado abaixo. Se dotnet satisfizer suas necessidades, não é necessário usar `nuget.exe`.

Para obter informações completas sobre `dotnet`, consulte [ferramentas de interface de linha de comando (CLI) do .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Consumo de pacote

- [**dotnet Adicionar pacote**](/dotnet/core/tools/dotnet-add-package): adiciona uma referência de pacote para o arquivo de projeto e, em seguida, executa `dotnet restore` para instalar o pacote.
- [**dotnet remover pacote**](/dotnet/core/tools/dotnet-remove-package): remove uma referência de pacote do arquivo de projeto.
- [**restauração dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaura as dependências e as ferramentas de um projeto. A partir do NuGet 4.0, isso executará o mesmo código que `nuget restore`.
- [**locais do nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): limpa ou lista os recursos locais do NuGet como o cache de solicitação de http, o cache temporário e a pasta pacotes global de todo o computador.

## <a name="package-creation"></a>Criação de pacote

- [**pacote de dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): pacotes de código em um pacote do NuGet. A partir do NuGet 4.0, isso executará o mesmo código que `nuget pack`.
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): envia um pacote para um servidor e o publica, aplicáveis a nuget.org, Visual Studio Team Services e servidores de NuGet de terceiros.
- [**Excluir dotnet nuget**](/dotnet/core/tools/dotnet-nuget-delete): exclui ou unlists um pacote de um host aplicável nuget.org, Visual Studio Team Services e servidores de NuGet de terceiros.
