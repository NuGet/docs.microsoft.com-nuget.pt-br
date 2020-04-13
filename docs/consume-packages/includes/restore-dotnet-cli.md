---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825155"
---
Use o comando [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), que restaura os pacotes listados no arquivo de projeto (confira [PackageReference](../../consume-packages/package-references-in-project-files.md)). Com o .NET Core 2.0 e posterior, a restauração é feita automaticamente com `dotnet build` e `dotnet run`. No NuGet 4.0 em diante, isso executa o mesmo código que `nuget restore`.

Assim como ocorre com outros comandos CLI do `dotnet`, primeiro abra uma linha de comando e alterne para o diretório que contém o arquivo de projeto.

Para restaurar um pacote usando `dotnet restore`:

```dotnetcli
dotnet restore 
```