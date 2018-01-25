---
title: comandos do NuGet dotNet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Uma referência curta para comandos relacionados NuGet usando a interface de linha de comando dotnet."
keywords: "comandos do NuGet dotnet, pacote dotnet, restauração dotnet, dotnet nuget locais, dotnet nuget push, dotnet nuget delete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d06e4590ab87b68e7846a13b2eba0f59eb9529d6
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="8ca0d-104">comandos dotNet</span><span class="sxs-lookup"><span data-stu-id="8ca0d-104">dotNet commands</span></span>

<span data-ttu-id="8ca0d-105">A interface de linha de comando DotNet, que é executado no Windows, Mac OS X e Linux, fornece um número de comandos de nuget.exe essenciais, como listado abaixo.</span><span class="sxs-lookup"><span data-stu-id="8ca0d-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="8ca0d-106">Onde dotnet fornece os comandos desejados, não é necessário fazer o download de nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="8ca0d-106">Where dotnet provides the desired commands, it's not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="8ca0d-107">[**pacote de dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): pacotes de código em um pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="8ca0d-107">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="8ca0d-108">A partir do NuGet 4.0, isso executará o mesmo código que `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="8ca0d-108">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="8ca0d-109">[**restauração dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaura as dependências e as ferramentas de um projeto.</span><span class="sxs-lookup"><span data-stu-id="8ca0d-109">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="8ca0d-110">A partir do NuGet 4.0, isso executará o mesmo código que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="8ca0d-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="8ca0d-111">[**locais do nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): limpa ou lista os recursos locais do NuGet como http-solicitação de cache, cache temporário ou pasta pacotes global de todo o computador.</span><span class="sxs-lookup"><span data-stu-id="8ca0d-111">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="8ca0d-112">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): envia um pacote para um servidor e o publica, aplicável nuget.org, Visual Studio Team Services ou todos os servidores NuGet de terceiros.</span><span class="sxs-lookup"><span data-stu-id="8ca0d-112">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="8ca0d-113">[**Excluir dotnet nuget**](/dotnet/core/tools/dotnet-nuget-delete): exclui ou unlists um pacote de um servidor, aplicável nuget.org, Visual Studio Team Services ou todos os servidores NuGet de terceiros.</span><span class="sxs-lookup"><span data-stu-id="8ca0d-113">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
