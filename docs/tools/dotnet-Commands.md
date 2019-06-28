---
title: comandos de CLI NuGet dotnet
description: Uma referência curta para comandos relacionados ao NuGet usando a interface de linha de comando dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: cc99b327c0edb4aeb573dfa8c2f9b9dba7b8cc38
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426013"
---
# <a name="dotnet-cli-commands"></a><span data-ttu-id="753bf-103">comandos CLI do dotnet</span><span class="sxs-lookup"><span data-stu-id="753bf-103">dotnet CLI commands</span></span>

<span data-ttu-id="753bf-104">O `dotnet` interface de linha de comando (CLI), que é executado no Windows, Mac OS X e Linux, fornece uma série de comandos essenciais, como instalação, restauração e publicação de pacotes.</span><span class="sxs-lookup"><span data-stu-id="753bf-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="753bf-105">Se dotnet satisfizer suas necessidades, não é necessário usar `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="753bf-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="753bf-106">Para obter exemplos de como usar esses comandos para consumir pacotes, consulte [instalar e gerenciar pacotes usando a CLI do dotnet](../consume-packages/install-use-packages-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="753bf-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="753bf-107">Para obter exemplos de como usar esses comandos para criar pacotes, consulte [criar e publicar um pacote usando a CLI do dotnet]... / quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="753bf-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI]../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="753bf-108">Para a referência de comando completo no `dotnet` CLI, consulte [ferramentas de interface de linha de comando (CLI) do .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="753bf-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="753bf-109">Consumo de pacote</span><span class="sxs-lookup"><span data-stu-id="753bf-109">Package consumption</span></span>

- <span data-ttu-id="753bf-110">[**dotnet Adicionar pacote**](/dotnet/core/tools/dotnet-add-package): Adiciona uma referência de pacote para o arquivo de projeto, em seguida, executa `dotnet restore` para instalar o pacote.</span><span class="sxs-lookup"><span data-stu-id="753bf-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="753bf-111">[**remover o pacote dotnet**](/dotnet/core/tools/dotnet-remove-package): Remove uma referência de pacote do arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="753bf-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="753bf-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restaura as dependências e as ferramentas de um projeto.</span><span class="sxs-lookup"><span data-stu-id="753bf-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="753bf-113">A partir do NuGet 4.0, ele é executado o mesmo código que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="753bf-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="753bf-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lista os locais do *global-packages*, *http-cache*, e *temp* limpa o conteúdo dessas pastas e pastas.</span><span class="sxs-lookup"><span data-stu-id="753bf-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="753bf-115">Criação de pacote</span><span class="sxs-lookup"><span data-stu-id="753bf-115">Package creation</span></span>

- <span data-ttu-id="753bf-116">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Empacota o código em um pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="753bf-116">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="753bf-117">A partir do NuGet 4.0, ele é executado o mesmo código que `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="753bf-117">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="753bf-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Envia um pacote a um servidor e os publica, aplicável para nuget.org, o Visual Studio Team Services e servidores NuGet de terceiros.</span><span class="sxs-lookup"><span data-stu-id="753bf-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="753bf-119">[**Excluir nuget dotnet**](/dotnet/core/tools/dotnet-nuget-delete): Exclui ou retira da lista um pacote de um host aplicável para nuget.org, o Visual Studio Team Services e servidores NuGet de terceiros.</span><span class="sxs-lookup"><span data-stu-id="753bf-119">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
