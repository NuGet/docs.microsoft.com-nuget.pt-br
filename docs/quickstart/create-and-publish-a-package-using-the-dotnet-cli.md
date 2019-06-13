---
title: Criando e publicando um pacote do NuGet usando a CLI do dotnet
description: Um tutorial passo a passo sobre como criar e publicar um pacote NuGet usando a CLI do .NET Core, dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 6aa5c7bcb2a46e5f8dcf8f2c04a91eafe9ca03b6
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66813001"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>Início Rápido: Criar e publicar um pacote (CLI do dotnet)

É um processo simples para criar um pacote NuGet de uma Biblioteca de Classes do .NET e publique-o em nuget.org usando a CLI (interface de linha de comando) `dotnet`.

## <a name="prerequisites"></a>Pré-requisitos

1. Instale o [SDK do .NET Core](https://www.microsoft.com/net/download/), que inclui a CLI do `dotnet`.

1. [Registre-se em uma conta gratuita em nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), se ainda não tiver uma. Criar uma nova conta envia um email de confirmação. Você deve confirmar a conta antes de poder carregar um pacote.

## <a name="create-a-class-library-project"></a>Criar um projeto de biblioteca de classes

Você pode usar um projeto existente da Biblioteca de Classes .NET para o código que você deseja empacotar, ou criar um simples da seguinte maneira:

1. Crie uma pasta chamada `AppLogger` e altere para ela.

1. Crie o projeto usando `dotnet new classlib`, que usa o nome da pasta atual para o projeto.

## <a name="add-package-metadata-to-the-project-file"></a>Adicionar metadados de pacote ao arquivo de projeto

Todos os pacotes NuGet precisam de um manifesto que descreve seu conteúdo e suas dependências. Em um pacote final, o manifesto é um arquivo `.nuspec` gerado das propriedades de metadados do NuGet que você inclui no arquivo do projeto.

1. Abra o arquivo de projeto (`.csproj`) e adicione as seguintes propriedades mínimas dentro da marca `<PropertyGroup>` existente, alterando os valores conforme apropriado:

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > Dê ao pacote um identificador exclusivo em nuget.org ou qualquer host que você esteja usando. Para este passo a passo, recomendamos incluir o "Sample" ou "Test" no nome, pois a etapa de publicação posterior torna o pacote publicamente visível (embora seja improvável que alguém possa usá-lo).

1. Adicione propriedades opcionais descritas em [Propriedades de metadados do NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

    > [!Note]
    > Para pacotes compilados para consumo público, preste atenção especial à propriedade **PackageTags**, à medida que as marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.

## <a name="run-the-pack-command"></a>Executar o comando pack

Para compilar um pacote do NuGet (um arquivo `.nupkg`) do projeto, execute o comando `dotnet pack`, que também compila o projeto automaticamente:

```cli
# Uses the project file in the current folder by default
dotnet pack
```

A saída mostra o caminho até o arquivo `.nupkg`:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Gerar pacote automaticamente no build

Para executar `dotnet pack` automaticamente ao executar `dotnet build`, adicione a seguinte linha ao arquivo de projeto em `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>Publicar o pacote

Depois que você tiver um arquivo `.nupkg`, publique-o em nuget.org usando o comando `dotnet nuget push` juntamente com uma chave de API adquirida em nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Adquirir a chave de sua API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>Publicar com dotnet nuget push

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Erros de publicação

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Gerenciar o pacote publicado

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Tópicos relacionados

- [Criar um pacote](../create-packages/creating-a-package.md)
- [Publicar um pacote](../create-packages/publish-a-package.md)
- [Pacotes de pré-lançamento](../create-packages/Prerelease-Packages.md)
- [Suporte a várias estruturas de destino](../create-packages/supporting-multiple-target-frameworks.md)
- [Controle de versão do pacote](../reference/package-versioning.md)
- [Criando pacotes localizados](../create-packages/creating-localized-packages.md)
- [Criando pacotes de símbolos](../create-packages/symbol-packages-snupkg.md)
- [Assinando pacotes](../create-packages/Sign-a-package.md)
