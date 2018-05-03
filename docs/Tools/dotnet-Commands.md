---
title: comandos do NuGet dotnet
description: Uma referência curta para comandos relacionados NuGet usando a interface de linha de comando dotnet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: fe49274af339c987d5e090c99edd78f62f59ce47
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="86adb-103">Comandos dotnet</span><span class="sxs-lookup"><span data-stu-id="86adb-103">dotnet commands</span></span>

<span data-ttu-id="86adb-104">O `dotnet` interface de linha de comando, que é executado no Windows, Mac OS X e Linux, fornece um número de comandos nuget.exe essenciais, como listado abaixo.</span><span class="sxs-lookup"><span data-stu-id="86adb-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="86adb-105">Se dotnet satisfizer suas necessidades, não é necessário usar `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="86adb-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="86adb-106">Para obter informações completas sobre `dotnet`, consulte [ferramentas de interface de linha de comando (CLI) do .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="86adb-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="86adb-107">Consumo de pacote</span><span class="sxs-lookup"><span data-stu-id="86adb-107">Package consumption</span></span>

- <span data-ttu-id="86adb-108">[**dotnet Adicionar pacote**](/dotnet/core/tools/dotnet-add-package): adiciona uma referência de pacote para o arquivo de projeto e, em seguida, executa `dotnet restore` para instalar o pacote.</span><span class="sxs-lookup"><span data-stu-id="86adb-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="86adb-109">[**dotnet remover pacote**](/dotnet/core/tools/dotnet-remove-package): remove uma referência de pacote do arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="86adb-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="86adb-110">[**restauração dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaura as dependências e as ferramentas de um projeto.</span><span class="sxs-lookup"><span data-stu-id="86adb-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="86adb-111">A partir do NuGet 4.0, isso executará o mesmo código que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="86adb-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="86adb-112">[**dotnet nuget locais**](/dotnet/core/tools/dotnet-nuget-locals): lista de locais do *pacotes global*, *cache http*, e *temp* pastas e limpa o conteúdo de Essas pastas.</span><span class="sxs-lookup"><span data-stu-id="86adb-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="86adb-113">Criação de pacote</span><span class="sxs-lookup"><span data-stu-id="86adb-113">Package creation</span></span>

- <span data-ttu-id="86adb-114">[**pacote de dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): pacotes de código em um pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="86adb-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="86adb-115">A partir do NuGet 4.0, isso executará o mesmo código que `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="86adb-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="86adb-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): envia um pacote para um servidor e o publica, aplicáveis a nuget.org, Visual Studio Team Services e servidores de NuGet de terceiros.</span><span class="sxs-lookup"><span data-stu-id="86adb-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="86adb-117">[**Excluir dotnet nuget**](/dotnet/core/tools/dotnet-nuget-delete): exclui ou unlists um pacote de um host aplicável nuget.org, Visual Studio Team Services e servidores de NuGet de terceiros.</span><span class="sxs-lookup"><span data-stu-id="86adb-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
