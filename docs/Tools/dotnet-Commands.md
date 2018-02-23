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
# <a name="dotnet-commands"></a><span data-ttu-id="2178f-104">comandos dotNet</span><span class="sxs-lookup"><span data-stu-id="2178f-104">dotNet commands</span></span>

<span data-ttu-id="2178f-105">O `dotnet` interface de linha de comando, que é executado no Windows, Mac OS X e Linux, fornece um número de comandos nuget.exe essenciais, como listado abaixo.</span><span class="sxs-lookup"><span data-stu-id="2178f-105">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="2178f-106">Se dotnet satisfizer suas necessidades, não é necessário usar `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="2178f-106">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="2178f-107">Para obter informações completas sobre `dotnet`, consulte [ferramentas de interface de linha de comando (CLI) do .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="2178f-107">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="2178f-108">Consumo de pacote</span><span class="sxs-lookup"><span data-stu-id="2178f-108">Package consumption</span></span>

- <span data-ttu-id="2178f-109">[**dotnet Adicionar pacote**](/dotnet/core/tools/dotnet-add-package): adiciona uma referência de pacote para o arquivo de projeto e, em seguida, executa `dotnet restore` para instalar o pacote.</span><span class="sxs-lookup"><span data-stu-id="2178f-109">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="2178f-110">[**dotnet remover pacote**](/dotnet/core/tools/dotnet-remove-package): remove uma referência de pacote do arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="2178f-110">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="2178f-111">[**restauração dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaura as dependências e as ferramentas de um projeto.</span><span class="sxs-lookup"><span data-stu-id="2178f-111">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="2178f-112">A partir do NuGet 4.0, isso executará o mesmo código que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="2178f-112">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="2178f-113">[**locais do nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): limpa ou lista os recursos locais do NuGet como o cache de solicitação de http, o cache temporário e a pasta pacotes global de todo o computador.</span><span class="sxs-lookup"><span data-stu-id="2178f-113">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as the http-request cache, the temporary cache, and the machine-wide global packages folder.</span></span>

## <a name="package-creation"></a><span data-ttu-id="2178f-114">Criação de pacote</span><span class="sxs-lookup"><span data-stu-id="2178f-114">Package creation</span></span>

- <span data-ttu-id="2178f-115">[**pacote de dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): pacotes de código em um pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="2178f-115">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="2178f-116">A partir do NuGet 4.0, isso executará o mesmo código que `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="2178f-116">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="2178f-117">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): envia um pacote para um servidor e o publica, aplicáveis a nuget.org, Visual Studio Team Services e servidores de NuGet de terceiros.</span><span class="sxs-lookup"><span data-stu-id="2178f-117">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="2178f-118">[**Excluir dotnet nuget**](/dotnet/core/tools/dotnet-nuget-delete): exclui ou unlists um pacote de um host aplicável nuget.org, Visual Studio Team Services e servidores de NuGet de terceiros.</span><span class="sxs-lookup"><span data-stu-id="2178f-118">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
