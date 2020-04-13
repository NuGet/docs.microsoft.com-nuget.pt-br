---
title: Gerenciar pacotes NuGet usando a CLI do nuget.exe
description: Instruções sobre como usar a CLI do nuget.exe para trabalhar com pacotes NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428684"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>Gerenciar pacotes usando a CLI do nuget.exe

A ferramenta CLI permite que você atualize e restaure pacotes NuGet com facilidade em projetos e soluções. Essa ferramenta fornece todas as funcionalidades do NuGet no Windows e também fornece a maioria dos recursos no Mac e no Linux durante a execução no Mono.

A CLI `nuget.exe` destina-se a seu projeto .NET Framework e a projetos no estilo não SDK (por exemplo, um projeto de estilo não SDK direcionado a bibliotecas .NET Standard). Caso esteja usando um projeto no estilo não SDK que foi migrado para `PackageReference`, use a CLI `dotnet`. A CLI `nuget.exe` exige um arquivo [packages.config](../reference/packages-config.md) para referências de pacote.

> [!NOTE]
> Na maioria dos cenários, recomendamos [migrar os projetos no estilo não SDK](../consume-packages/migrate-packages-config-to-package-reference.md) que usam `packages.config` para PackageReference, assim é possível usar a CLI `dotnet` ao invés da CLI `nuget.exe`. Atualmente, a migração não está disponível para projetos C++ e ASP.NET.

Este artigo mostra o uso básico de alguns dos comandos mais comuns da CLI `nuget.exe`. Para a maioria desses comandos, a ferramenta CLI procura um arquivo de projeto no diretório atual, a menos que um arquivo de projeto seja especificado no comando. Para obter uma lista completa de comandos e os argumentos que podem ser usados, confira [Referência da CLI do nuget.exe](../reference/nuget-exe-cli-reference.md).

## <a name="prerequisites"></a>Pré-requisitos

- Instale a CLI do `nuget.exe` baixando-a de [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), salvando o arquivo `.exe` em uma pasta adequada e adicionando pasta a variável de ambiente PATH.

## <a name="install-a-package"></a>Instalar um pacote

O comando [install](../reference/cli-reference/cli-ref-install.md) baixa e instala um pacote em um projeto, usando como padrão a pasta atual, com as origens do pacote especificadas. Instale novos pacotes na pasta *packages* no diretório raiz do projeto.

> [!IMPORTANT]
> O `install`comando não modifica um arquivo de projeto nem *packages.config*; dessa forma, ele é semelhante a `restore`, pois apenas adiciona pacotes ao disco, mas não altera as dependências de um projeto. Para adicionar uma dependência, adicione um pacote por meio da interface do usuário do Gerenciador de Pacotes ou do Console no Visual Studio ou modifique *packages.config* e, em seguida, execute `install` ou `restore`.

1. Abra uma linha de comando e alterne para o diretório que contém o arquivo de projeto.

2. Use o comando a seguir para instalar um pacote NuGet na pasta *packages*.

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    Para instalar o pacote `Newtonsoft.json` na pasta *packages*, use o seguinte comando:

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

Como alternativa, você pode usar o comando a seguir para instalar um pacote NuGet usando um arquivo `packages.config` existente na pasta *packages*. Isso não adiciona o pacote às dependências do projeto, mas o instala localmente.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>Instalar uma versão específica de um pacote

Se a versão não for especificada quando você usar o comando [install](../reference/cli-reference/cli-ref-install.md), o NuGet instalará a última versão do pacote. Instale também uma versão específica de um pacote NuGet:

```cli
nuget install <packageID | configFilePath> -Version <version>
```

Por exemplo, para adicionar a versão 12.0.1 do pacote `Newtonsoft.json`, use este comando:

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

Para obter mais informações sobre as limitações e o comportamento de `install`, confira [Instalar um pacote](#install-a-package).

## <a name="remove-a-package"></a>Remover um pacote

Para excluir um ou mais pacotes, exclua os pacotes que deseja remover da pasta *packages*.

Caso deseje reinstalar pacotes, use o comando `restore` ou `install`.

## <a name="list-packages"></a>Listar pacotes

Você pode exibir uma lista de pacotes de determinada fonte usando o comando [list](../reference/cli-reference/cli-ref-list.md). Use a opção `-Source` para restringir a pesquisa.

```cli
nuget list -Source <source>
```

Por exemplo, liste os pacotes da pasta *packages*.

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

Se você usar um termo de pesquisa, a pesquisa incluirá os nomes dos pacotes, as marcas e as descrições dos pacotes.

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>Atualizar um pacote individual

O NuGet instala a última versão do pacote quando você usa o comando `install`, a menos que você especifique a versão do pacote.

## <a name="update-all-packages"></a>Atualizar todos os pacotes

Use o comando [update](../reference/cli-reference/cli-ref-update.md) para atualizar todos os pacotes. Atualiza todos os pacotes de um projeto (usando `packages.config`) para as últimas versões disponíveis. É recomendável executar `restore` antes de executar `update`.

```cli
nuget update
```

## <a name="restore-packages"></a>Restaurar pacotes

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a>Obter a versão da CLI

Use este comando:

```cli
nuget help
```

A primeira linha na saída da ajuda mostra a versão. Para evitar a rolagem para cima, use `nuget help | more`.