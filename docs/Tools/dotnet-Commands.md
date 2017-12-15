---
title: comandos do NuGet dotNet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0c81dbc4-2c14-4ec8-b87a-b802a899c3ea
description: "Uma referência curta para comandos relacionados NuGet usando a interface de linha de comando dotnet."
keywords: "comandos do NuGet dotnet, pacote dotnet, restauração dotnet, dotnet nuget locais, dotnet nuget push, dotnet nuget delete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ff4779f46db102f1384650d82118b34fedd4413
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="dotnet-commands"></a>comandos dotNet

A interface de linha de comando DotNet, que é executado no Windows, Mac OS X e Linux, fornece um número de comandos de nuget.exe essenciais, como listado abaixo. Onde dotnet fornece os comandos desejados, não é necessário fazer o download de nuget.exe.

- [**pacote de dotnet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): pacotes de código para NETCore SDK projetos em um pacote do NuGet. Todos os outros tipos de projeto devem usar[`nuget pack`](cli-ref-pack.md)
- [**restauração dotnet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaura as dependências e as ferramentas de um projeto. A partir do NuGet 4.0, isso executará o mesmo código que `nuget restore`.
- [**locais do nuget dotnet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): limpa ou lista os recursos locais do NuGet como http-solicitação de cache, cache temporário ou pasta pacotes global de todo o computador.
- [**dotnet nuget push**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): envia um pacote para um servidor e o publica, aplicável nuget.org, Visual Studio Team Services ou todos os servidores NuGet de terceiros.
- [**Excluir dotnet nuget**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): exclui ou unlists um pacote de um servidor, aplicável nuget.org, Visual Studio Team Services ou todos os servidores NuGet de terceiros.
