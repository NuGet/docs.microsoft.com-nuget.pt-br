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
# <a name="dotnet-commands"></a><span data-ttu-id="101d2-104">comandos dotNet</span><span class="sxs-lookup"><span data-stu-id="101d2-104">dotNet commands</span></span>

<span data-ttu-id="101d2-105">A interface de linha de comando DotNet, que é executado no Windows, Mac OS X e Linux, fornece um número de comandos de nuget.exe essenciais, como listado abaixo.</span><span class="sxs-lookup"><span data-stu-id="101d2-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="101d2-106">Onde dotnet fornece os comandos desejados, não é necessário fazer o download de nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="101d2-106">Where dotnet provides the desired commands, it is not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="101d2-107">[**pacote de dotnet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): pacotes de código para NETCore SDK projetos em um pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="101d2-107">[**dotnet pack**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs code for NETCore SDK projects into a NuGet package.</span></span> <span data-ttu-id="101d2-108">Todos os outros tipos de projeto devem usar[`nuget pack`](cli-ref-pack.md)</span><span class="sxs-lookup"><span data-stu-id="101d2-108">All other project types should use [`nuget pack`](cli-ref-pack.md)</span></span>
- <span data-ttu-id="101d2-109">[**restauração dotnet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaura as dependências e as ferramentas de um projeto.</span><span class="sxs-lookup"><span data-stu-id="101d2-109">[**dotnet restore**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="101d2-110">A partir do NuGet 4.0, isso executará o mesmo código que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="101d2-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="101d2-111">[**locais do nuget dotnet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): limpa ou lista os recursos locais do NuGet como http-solicitação de cache, cache temporário ou pasta pacotes global de todo o computador.</span><span class="sxs-lookup"><span data-stu-id="101d2-111">[**dotnet nuget locals**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="101d2-112">[**dotnet nuget push**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): envia um pacote para um servidor e o publica, aplicável nuget.org, Visual Studio Team Services ou todos os servidores NuGet de terceiros.</span><span class="sxs-lookup"><span data-stu-id="101d2-112">[**dotnet nuget push**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="101d2-113">[**Excluir dotnet nuget**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): exclui ou unlists um pacote de um servidor, aplicável nuget.org, Visual Studio Team Services ou todos os servidores NuGet de terceiros.</span><span class="sxs-lookup"><span data-stu-id="101d2-113">[**dotnet nuget delete**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
