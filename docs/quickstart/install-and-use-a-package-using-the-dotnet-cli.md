---
title: Instalar e usar um pacote do NuGet usando a CLI dotnet
description: Um tutorial passo a passo sobre o processo de instalação e uso de um pacote NuGet em um projeto .NET Core.
author: JonDouglas
ms.author: jodou
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: dbe1d3ee8e50a90803140bc2c5cb5821b485a2fd
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859428"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="0e330-103">Início Rápido: Instalar e usar um pacote usando a CLI do dotnet</span><span class="sxs-lookup"><span data-stu-id="0e330-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="0e330-104">Os pacotes NuGet contém código reutilizável que outros desenvolvedores disponibilizam para uso em seus projetos.</span><span class="sxs-lookup"><span data-stu-id="0e330-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="0e330-105">Consulte [O que há de novo no NuGet](../What-is-NuGet.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="0e330-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="0e330-106">Os pacotes são instalados em um projeto do .NET Core usando o comando `dotnet add package`, conforme descrito neste artigo para a popular pacote [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).</span><span class="sxs-lookup"><span data-stu-id="0e330-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="0e330-107">Uma vez instalado, consulte o pacote em código com `using <namespace>` onde \<namespace\> é específico para o pacote que você está usando.</span><span class="sxs-lookup"><span data-stu-id="0e330-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="0e330-108">Em seguida, você pode usar o API do pacote.</span><span class="sxs-lookup"><span data-stu-id="0e330-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="0e330-109">**Começar com nuget.org**: normalmente, os desenvolvedores em .NET encontram os componentes que podem reutilizar em seus próprios aplicativos procurando no nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0e330-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="0e330-110">Você pode pesquisar no nuget.org diretamente ou localizar e instalar pacotes de dentro do Visual Studio, conforme mostrado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="0e330-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e330-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0e330-111">Prerequisites</span></span>

- <span data-ttu-id="0e330-112">O [SDK do .NET Core](https://www.microsoft.com/net/download/), que fornece a ferramenta de linha de comando `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="0e330-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="0e330-113">No Visual Studio 2017 em diante, a CLI do dotnet é instalada automaticamente com qualquer carga de trabalho relacionada ao .NET Core.</span><span class="sxs-lookup"><span data-stu-id="0e330-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="0e330-114">Criar um projeto</span><span class="sxs-lookup"><span data-stu-id="0e330-114">Create a project</span></span>

<span data-ttu-id="0e330-115">Os pacotes NuGet podem ser instalados em algum tipo de projeto do .NET.</span><span class="sxs-lookup"><span data-stu-id="0e330-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="0e330-116">Para este passo a passo, crie um projeto de console do .NET Core simples da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0e330-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="0e330-117">Crie uma pasta para o projeto.</span><span class="sxs-lookup"><span data-stu-id="0e330-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="0e330-118">Abra um prompt de comando e alterne para a nova pasta.</span><span class="sxs-lookup"><span data-stu-id="0e330-118">Open a command prompt and switch to the new folder.</span></span>

1. <span data-ttu-id="0e330-119">Crie o projeto usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="0e330-119">Create the project using the following command:</span></span>

    ```dotnetcli
    dotnet new console
    ```

1. <span data-ttu-id="0e330-120">Use `dotnet run` para testar se o aplicativo foi criado corretamente.</span><span class="sxs-lookup"><span data-stu-id="0e330-120">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="0e330-121">Adicionar o pacote do NuGet Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="0e330-121">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="0e330-122">Use o seguinte comando para instalar o pacote `Newtonsoft.json`:</span><span class="sxs-lookup"><span data-stu-id="0e330-122">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="0e330-123">Após a conclusão do comando, abra o arquivo `.csproj` para ver a referência adicionada:</span><span class="sxs-lookup"><span data-stu-id="0e330-123">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
    <ItemGroup>
      <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
    </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="0e330-124">Use a API Newtonsoft.Json no aplicativo</span><span class="sxs-lookup"><span data-stu-id="0e330-124">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="0e330-125">Abra o arquivo `Program.cs` e adicione a seguinte linha no topo do arquivo:</span><span class="sxs-lookup"><span data-stu-id="0e330-125">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="0e330-126">Adicione o código a seguir antes da linha `class Program`:</span><span class="sxs-lookup"><span data-stu-id="0e330-126">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="0e330-127">Substitua a função `Main` pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="0e330-127">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="0e330-128">Compile e execute o aplicativo usando o comando `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="0e330-128">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="0e330-129">A saída deve ser a representação JSON do objeto `Account` no código:</span><span class="sxs-lookup"><span data-stu-id="0e330-129">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a><span data-ttu-id="0e330-130">Vídeo relacionado</span><span class="sxs-lookup"><span data-stu-id="0e330-130">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

<span data-ttu-id="0e330-131">Encontre mais vídeos sobre o NuGet no [Channel 9](https://channel9.msdn.com/Series/NuGet-101) e no [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="0e330-131">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e330-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0e330-132">Next steps</span></span>

<span data-ttu-id="0e330-133">Parabéns por instalar e usar seu primeiro pacote do NuGet!</span><span class="sxs-lookup"><span data-stu-id="0e330-133">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0e330-134">Instalar e usar pacotes usando a CLI do dotnet</span><span class="sxs-lookup"><span data-stu-id="0e330-134">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)

<span data-ttu-id="0e330-135">Para ver o que mais o NuGet tem a oferecer, selecione os links abaixo.</span><span class="sxs-lookup"><span data-stu-id="0e330-135">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="0e330-136">Visão geral e fluxo de trabalho do consumo de pacote</span><span class="sxs-lookup"><span data-stu-id="0e330-136">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="0e330-137">Localizando e escolhendo pacotes</span><span class="sxs-lookup"><span data-stu-id="0e330-137">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="0e330-138">Referências de pacotes em arquivos de projeto</span><span class="sxs-lookup"><span data-stu-id="0e330-138">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
