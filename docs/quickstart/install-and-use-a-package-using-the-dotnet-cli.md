---
title: Guia de introdução ao uso de pacotes do NuGet por meio da CLI do dotnet
description: Um tutorial passo a passo sobre o processo de instalação e uso de um pacote NuGet em um projeto .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: bb24ccbfdd4a6a94cf7116f16b0862871e176e50
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549270"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Início Rápido: Instalar e usar um pacote usando a CLI do dotnet

Os pacotes NuGet contém código reutilizável que outros desenvolvedores disponibilizam para uso em seus projetos. Consulte [O que há de novo no NuGet](../What-is-NuGet.md) para obter mais informações. Os pacotes são instalados em um projeto do .NET Core usando o comando `dotnet add package`, conforme descrito neste artigo para a popular pacote [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).

Depois de instalado, consulte o pacote no código com `using <namespace>` em que \<namespace\> é específico para o pacote que você está usando. Em seguida, você pode usar o API do pacote.

> [!Tip]
> **Começar com nuget.org**: normalmente, os desenvolvedores em .NET encontram os componentes que podem reutilizar em seus próprios aplicativos procurando no nuget.org. Você pode pesquisar no nuget.org diretamente ou localizar e instalar pacotes de dentro do Visual Studio, conforme mostrado neste artigo.

## <a name="prerequisites"></a>Pré-requisitos

- O [SDK do .NET Core](https://www.microsoft.com/net/download/), que fornece a ferramenta de linha de comando `dotnet`.

## <a name="create-a-project"></a>Criar um projeto

Os pacotes NuGet podem ser instalados em algum tipo de projeto do .NET. Para este passo a passo, crie um projeto de console do .NET Core simples da seguinte maneira:

1. Crie uma pasta para o projeto.

1. Crie o projeto usando o seguinte comando:

    ```cli
    dotnet new console
    ```

1. Use `dotnet run` para testar se o aplicativo foi criado corretamente.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Adicionar o pacote do NuGet Newtonsoft.Json

1. Use o seguinte comando para instalar o pacote `Newtonsoft.json`:

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. Após a conclusão do comando, abra o arquivo `.csproj` para ver a referência adicionada:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Use a API Newtonsoft.Json no aplicativo

1. Abra o arquivo `Program.cs` e adicione a seguinte linha no topo do arquivo:

    ```cs
    using Newtonsoft.Json;
    ```

1. Adicione o código a seguir antes da linha `class Program`:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. Substitua a função `Main` pelo seguinte:

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. Compile e execute o aplicativo usando o comando `dotnet run`. A saída deve ser a representação JSON do objeto `Account` no código:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a>Artigos relacionados

- [Visão geral e fluxo de trabalho do consumo de pacote](../consume-packages/overview-and-workflow.md)
- [Localizando e escolhendo pacotes](../consume-packages/finding-and-choosing-packages.md)
- [Maneiras de instalar um pacote](../consume-packages/ways-to-install-a-package.md)
- [Configurando o Comportamento de NuGet](../consume-packages/configuring-nuget-behavior.md)
