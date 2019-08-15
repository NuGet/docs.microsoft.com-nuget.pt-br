---
ms.openlocfilehash: 9764479d88cc8d87a9f455e64bd46ae8de15055d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860592"
---
<span data-ttu-id="9e9f9-101">Use o comando [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), que restaura os pacotes listados no arquivo de projeto (confira [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="9e9f9-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="9e9f9-102">Com o .NET Core 2.0 e posterior, a restauração é feita automaticamente com `dotnet build` e `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="9e9f9-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="9e9f9-103">No NuGet 4.0 em diante, isso executa o mesmo código que `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="9e9f9-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="9e9f9-104">Assim como ocorre com outros comandos CLI do `dotnet`, primeiro abra uma linha de comando e alterne para o diretório que contém o arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="9e9f9-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="9e9f9-105">Para restaurar um pacote usando `dotnet restore`:</span><span class="sxs-lookup"><span data-stu-id="9e9f9-105">To restore a package using `dotnet restore`:</span></span>

```cli
dotnet restore 
```