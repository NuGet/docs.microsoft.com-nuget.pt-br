---
title: Instalar e gerenciar pacotes NuGet usando a CLI do dotnet
description: Instruções de uso da CLI do dotnet para trabalhar com pacotes NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 67cca81c48970c7f2e2cf0a64ee5ba57704a31e2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825164"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>Instalar e gerenciar pacotes usando a CLI do dotnet

A ferramenta CLI permite que você instale, desinstale e atualize pacotes NuGet com facilidade em projetos e soluções. Ela é executada no Windows, no Mac OS X e no Linux.

A CLI do dotnet destina-se ao uso em seu projeto .NET Core e .NET Standard (tipos de projeto no estilo SDK) e a todos os outros projetos no estilo SDK (por exemplo, um projeto no estilo SDK direcionado ao .NET Framework). Para obter mais informações, confira [Atributo SDK](/dotnet/core/tools/csproj#additions).

Este artigo mostra o uso básico de alguns dos comandos mais comuns da CLI do dotnet. Para a maioria desses comandos, a ferramenta CLI procura um arquivo de projeto no diretório atual, a menos que um arquivo de projeto seja especificado no comando (o arquivo de projeto é uma opção facultativa). Para obter uma lista completa de comandos e os argumentos que podem ser usados, confira [Ferramentas da CLI (interface de linha de comando) do .NET Core](../reference/dotnet-commands.md).

## <a name="prerequisites"></a>Pré-requisitos

- O [SDK do .NET Core](https://www.microsoft.com/net/download/), que fornece a ferramenta de linha de comando `dotnet`. No Visual Studio 2017 em diante, a CLI do dotnet é instalada automaticamente com qualquer carga de trabalho relacionada ao .NET Core.

## <a name="install-a-package"></a>Instalar um pacote

[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adiciona uma referência de pacote ao arquivo de projeto e, em seguida, executa `dotnet restore` para instalar o pacote.

1. Abra uma linha de comando e alterne para o diretório que contém o arquivo de projeto.

2. Use o seguinte comando para instalar um pacote NuGet:

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    Por exemplo, para instalar o pacote `Newtonsoft.Json`, use o comando a seguir

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. Após a conclusão do comando, examine o arquivo de projeto para verificar se o pacote foi instalado.

   Abra o arquivo `.csproj` para ver a referência adicionada:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>Instalar uma versão específica de um pacote

Se a versão não for especificada, o NuGet instalará a última versão do pacote. Use também o comando [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) para instalar uma versão específica de um pacote NuGet:

```dotnetcli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

Por exemplo, para adicionar a versão 12.0.1 do pacote `Newtonsoft.Json`, use este comando:

```dotnetcli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a>Listar as referências de pacote

Liste as referências de pacote para o projeto usando o comando [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x).

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a>Remover um pacote

Use o comando [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) para remover uma referência de pacote do arquivo de projeto.

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

Por exemplo, para remover o pacote `Newtonsoft.Json`, use o comando a seguir

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Atualizar um pacote

O NuGet instala a última versão do pacote quando você usa o comando `dotnet add package`, a menos que você especifique a versão do pacote (opção `-v`).

## <a name="restore-packages"></a>Restaurar pacotes

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
