---
title: Guia de introdução ao uso de pacotes do NuGet por meio da CLI do dotnet
description: Um tutorial passo a passo sobre o processo de instalação e uso de um pacote NuGet em um projeto .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 0d637c441cf9f36e8e3e04e47b524b2defecae52
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67841667"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="12eea-103">Início Rápido: Instalar e usar um pacote usando a CLI do dotnet</span><span class="sxs-lookup"><span data-stu-id="12eea-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="12eea-104">Os pacotes NuGet contém código reutilizável que outros desenvolvedores disponibilizam para uso em seus projetos.</span><span class="sxs-lookup"><span data-stu-id="12eea-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="12eea-105">Consulte [O que há de novo no NuGet](../What-is-NuGet.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="12eea-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="12eea-106">Os pacotes são instalados em um projeto do .NET Core usando o comando `dotnet add package`, conforme descrito neste artigo para a popular pacote [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).</span><span class="sxs-lookup"><span data-stu-id="12eea-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="12eea-107">Depois de instalado, consulte o pacote no código com `using <namespace>` em que \<namespace\> é específico para o pacote que você está usando.</span><span class="sxs-lookup"><span data-stu-id="12eea-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="12eea-108">Em seguida, você pode usar o API do pacote.</span><span class="sxs-lookup"><span data-stu-id="12eea-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="12eea-109">**Começar no nuget.org**: normalmente, os desenvolvedores em .NET encontram componentes que podem reutilizar em seus próprios aplicativos procurando no nuget.org.</span><span class="sxs-lookup"><span data-stu-id="12eea-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="12eea-110">Você pode pesquisar no nuget.org diretamente ou localizar e instalar pacotes de dentro do Visual Studio, conforme mostrado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="12eea-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12eea-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="12eea-111">Prerequisites</span></span>

- <span data-ttu-id="12eea-112">O [SDK do .NET Core](https://www.microsoft.com/net/download/), que fornece a ferramenta de linha de comando `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="12eea-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="12eea-113">No Visual Studio 2017 em diante, a CLI do dotnet é instalada automaticamente com qualquer carga de trabalho relacionada ao .NET Core.</span><span class="sxs-lookup"><span data-stu-id="12eea-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="12eea-114">Criar um projeto</span><span class="sxs-lookup"><span data-stu-id="12eea-114">Create a project</span></span>

<span data-ttu-id="12eea-115">Os pacotes NuGet podem ser instalados em algum tipo de projeto do .NET.</span><span class="sxs-lookup"><span data-stu-id="12eea-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="12eea-116">Para este passo a passo, crie um projeto de console do .NET Core simples da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="12eea-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="12eea-117">Crie uma pasta para o projeto.</span><span class="sxs-lookup"><span data-stu-id="12eea-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="12eea-118">Crie o projeto usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="12eea-118">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="12eea-119">Use `dotnet run` para testar se o aplicativo foi criado corretamente.</span><span class="sxs-lookup"><span data-stu-id="12eea-119">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="12eea-120">Adicionar o pacote do NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="12eea-120">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="12eea-121">Use o seguinte comando para instalar o pacote `Newtonsoft.json`:</span><span class="sxs-lookup"><span data-stu-id="12eea-121">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="12eea-122">Após a conclusão do comando, abra o arquivo `.csproj` para ver a referência adicionada:</span><span class="sxs-lookup"><span data-stu-id="12eea-122">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="12eea-123">Use a API Newtonsoft.Json no aplicativo</span><span class="sxs-lookup"><span data-stu-id="12eea-123">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="12eea-124">Abra o arquivo `Program.cs` e adicione a seguinte linha no topo do arquivo:</span><span class="sxs-lookup"><span data-stu-id="12eea-124">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="12eea-125">Adicione o código a seguir antes da linha `class Program`:</span><span class="sxs-lookup"><span data-stu-id="12eea-125">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="12eea-126">Substitua a função `Main` pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="12eea-126">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="12eea-127">Compile e execute o aplicativo usando o comando `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="12eea-127">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="12eea-128">A saída deve ser a representação JSON do objeto `Account` no código:</span><span class="sxs-lookup"><span data-stu-id="12eea-128">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="12eea-129">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="12eea-129">Related articles</span></span>

- [<span data-ttu-id="12eea-130">Instalar e usar pacotes usando a CLI do dotnet</span><span class="sxs-lookup"><span data-stu-id="12eea-130">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)
- [<span data-ttu-id="12eea-131">Visão geral e fluxo de trabalho do consumo de pacote</span><span class="sxs-lookup"><span data-stu-id="12eea-131">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="12eea-132">Localizando e escolhendo pacotes</span><span class="sxs-lookup"><span data-stu-id="12eea-132">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="12eea-133">Configurações comuns do NuGet</span><span class="sxs-lookup"><span data-stu-id="12eea-133">Common NuGet configurations</span></span>](../consume-packages/configuring-nuget-behavior.md)
