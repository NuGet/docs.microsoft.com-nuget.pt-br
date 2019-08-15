---
ms.openlocfilehash: 9764479d88cc8d87a9f455e64bd46ae8de15055d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860592"
---
Use o comando [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), que restaura os pacotes listados no arquivo de projeto (confira [PackageReference](../../consume-packages/package-references-in-project-files.md)). Com o .NET Core 2.0 e posterior, a restauração é feita automaticamente com `dotnet build` e `dotnet run`. No NuGet 4.0 em diante, isso executa o mesmo código que `nuget restore`.

Assim como ocorre com outros comandos CLI do `dotnet`, primeiro abra uma linha de comando e alterne para o diretório que contém o arquivo de projeto.

Para restaurar um pacote usando `dotnet restore`:

```cli
dotnet restore 
```