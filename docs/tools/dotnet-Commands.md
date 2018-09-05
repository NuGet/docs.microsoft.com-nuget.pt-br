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
# <a name="dotnet-commands"></a><span data-ttu-id="3e805-103">Comandos dotnet</span><span class="sxs-lookup"><span data-stu-id="3e805-103">dotnet commands</span></span>

<span data-ttu-id="3e805-104">O `dotnet` interface de linha de comando, que é executado no Windows, Mac OS X e Linux, fornece um número de comandos nuget.exe essenciais, como listado abaixo.</span><span class="sxs-lookup"><span data-stu-id="3e805-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="3e805-105">Se dotnet satisfizer suas necessidades, não é necessário usar `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="3e805-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="3e805-106">Para obter informações completas sobre `dotnet`, consulte [ferramentas de interface de linha de comando (CLI) do .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="3e805-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="3e805-107">Consumo de pacote</span><span class="sxs-lookup"><span data-stu-id="3e805-107">Package consumption</span></span>

- <span data-ttu-id="3e805-108">[**dotnet Adicionar pacote**](/dotnet/core/tools/dotnet-add-package): adiciona uma referência de pacote para o arquivo de projeto, em seguida, executa `dotnet restore` para instalar o pacote.</span><span class="sxs-lookup"><span data-stu-id="3e805-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="3e805-109">[**remover o pacote dotnet**](/dotnet/core/tools/dotnet-remove-package): remove uma referência de pacote do arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="3e805-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="3e805-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): restaura as dependências e as ferramentas de um projeto.</span><span class="sxs-lookup"><span data-stu-id="3e805-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="3e805-111">A partir do NuGet 4.0, ele é executado o mesmo código que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="3e805-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="3e805-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): lista os locais das *global-packages*, *http-cache*, e *temp* pastas e limpa o conteúdo de Essas pastas.</span><span class="sxs-lookup"><span data-stu-id="3e805-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="3e805-113">Criação de pacote</span><span class="sxs-lookup"><span data-stu-id="3e805-113">Package creation</span></span>

- <span data-ttu-id="3e805-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): empacota o código em um pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="3e805-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="3e805-115">A partir do NuGet 4.0, ele é executado o mesmo código que `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="3e805-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="3e805-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): envia um pacote a um servidor e os publica, aplicável para nuget.org, o Visual Studio Team Services e servidores NuGet de terceiros.</span><span class="sxs-lookup"><span data-stu-id="3e805-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="3e805-117">[**Excluir nuget dotnet**](/dotnet/core/tools/dotnet-nuget-delete): exclui ou retira da lista um pacote de um host aplicável para nuget.org, o Visual Studio Team Services e servidores NuGet de terceiros.</span><span class="sxs-lookup"><span data-stu-id="3e805-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
