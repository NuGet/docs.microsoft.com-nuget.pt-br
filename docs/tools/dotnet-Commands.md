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
# <a name="dotnet-commands"></a><span data-ttu-id="ff519-103">Comandos dotnet</span><span class="sxs-lookup"><span data-stu-id="ff519-103">dotnet commands</span></span>

<span data-ttu-id="ff519-104">O `dotnet` interface de linha de comando, que é executado no Windows, Mac OS X e Linux, fornece um número de comandos nuget.exe essenciais, como listado abaixo.</span><span class="sxs-lookup"><span data-stu-id="ff519-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="ff519-105">Se dotnet satisfizer suas necessidades, não é necessário usar `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="ff519-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="ff519-106">Para obter informações completas sobre `dotnet`, consulte [ferramentas de interface de linha de comando (CLI) do .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="ff519-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="ff519-107">Consumo de pacote</span><span class="sxs-lookup"><span data-stu-id="ff519-107">Package consumption</span></span>

- <span data-ttu-id="ff519-108">[**dotnet Adicionar pacote**](/dotnet/core/tools/dotnet-add-package): adiciona uma referência de pacote para o arquivo de projeto e, em seguida, executa `dotnet restore` para instalar o pacote.</span><span class="sxs-lookup"><span data-stu-id="ff519-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="ff519-109">[**dotnet remover pacote**](/dotnet/core/tools/dotnet-remove-package): remove uma referência de pacote do arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="ff519-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="ff519-110">[**restauração dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaura as dependências e as ferramentas de um projeto.</span><span class="sxs-lookup"><span data-stu-id="ff519-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="ff519-111">A partir do NuGet 4.0, isso executará o mesmo código que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="ff519-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="ff519-112">[**dotnet nuget locais**](/dotnet/core/tools/dotnet-nuget-locals): lista de locais do *pacotes global*, *cache http*, e *temp* pastas e limpa o conteúdo de Essas pastas.</span><span class="sxs-lookup"><span data-stu-id="ff519-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="ff519-113">Criação de pacote</span><span class="sxs-lookup"><span data-stu-id="ff519-113">Package creation</span></span>

- <span data-ttu-id="ff519-114">[**pacote de dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): pacotes de código em um pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="ff519-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="ff519-115">A partir do NuGet 4.0, isso executará o mesmo código que `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="ff519-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="ff519-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): envia um pacote para um servidor e o publica, aplicáveis a nuget.org, Visual Studio Team Services e servidores de NuGet de terceiros.</span><span class="sxs-lookup"><span data-stu-id="ff519-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="ff519-117">[**Excluir dotnet nuget**](/dotnet/core/tools/dotnet-nuget-delete): exclui ou unlists um pacote de um host aplicável nuget.org, Visual Studio Team Services e servidores de NuGet de terceiros.</span><span class="sxs-lookup"><span data-stu-id="ff519-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
