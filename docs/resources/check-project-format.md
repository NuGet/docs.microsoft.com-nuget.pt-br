---
title: Identificar o formato do projeto
description: Descreve como identificar o formato do projeto
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 3d8745ea30115a2d7f3954d171d92b75a434a55b
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843438"
---
# <a name="identify-the-project-format"></a><span data-ttu-id="cf465-103">Identificar o formato do projeto</span><span class="sxs-lookup"><span data-stu-id="cf465-103">Identify the project format</span></span>

<span data-ttu-id="cf465-104">O NuGet funciona com todos os projetos .NET.</span><span class="sxs-lookup"><span data-stu-id="cf465-104">NuGet works with all .NET projects.</span></span> <span data-ttu-id="cf465-105">No entanto, o formato de projeto (estilo SDK ou não) determina algumas das ferramentas e dos métodos que você precisa usar para consumir e criar pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="cf465-105">However, the project format (SDK-style or non-SDK-style) determines some of the tools and methods that you need to use to consume and create NuGet packages.</span></span> <span data-ttu-id="cf465-106">Os projetos de estilo SDK usam o [atributo SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="cf465-106">SDK-style projects use the [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span> <span data-ttu-id="cf465-107">É importante identificar o tipo de projeto porque os métodos e as ferramentas que você usa para consumir e criar pacotes NuGet dependem do formato do projeto.</span><span class="sxs-lookup"><span data-stu-id="cf465-107">It is important to identify your project type because the methods and tools you use to consume and create NuGet packages are dependent on the project format.</span></span> <span data-ttu-id="cf465-108">Para projetos de estilo não SDK, os métodos e as ferramentas também dependem se o projeto foi migrado para o formato `PackageReference` ou não.</span><span class="sxs-lookup"><span data-stu-id="cf465-108">For non-SDK-style projects, the methods and tools are also dependent on whether or not the project has been migrated to `PackageReference` format.</span></span>

<span data-ttu-id="cf465-109">Se o seu projeto é do tipo SDK ou não depende do método usado para criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="cf465-109">Whether your project is SDK-style or not depends on the method used to create the project.</span></span> <span data-ttu-id="cf465-110">A tabela a seguir mostra o formato de projeto padrão e a ferramenta CLI associada para seu projeto ao criá-lo usando o Visual Studio 2017 e versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="cf465-110">The following table shows the default project format and the associated CLI tool for your project when you create it using Visual Studio 2017 and later versions.</span></span>

| <span data-ttu-id="cf465-111">Projeto&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="cf465-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="cf465-112">Formato padrão do projeto</span><span class="sxs-lookup"><span data-stu-id="cf465-112">Default project format</span></span> | <span data-ttu-id="cf465-113">Ferramenta CLI&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="cf465-113">CLI tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="cf465-114">Observações</span><span class="sxs-lookup"><span data-stu-id="cf465-114">Notes</span></span> |
|:------------- |:-------------|:-----|:-----|
| <span data-ttu-id="cf465-115">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="cf465-115">.NET Standard</span></span> | <span data-ttu-id="cf465-116">Estilo SDK</span><span class="sxs-lookup"><span data-stu-id="cf465-116">SDK-style</span></span> | [<span data-ttu-id="cf465-117">CLI do dotnet</span><span class="sxs-lookup"><span data-stu-id="cf465-117">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="cf465-118">Os projetos criados antes do Visual Studio 2017 não são do tipo SDK.</span><span class="sxs-lookup"><span data-stu-id="cf465-118">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="cf465-119">Use a CLI `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="cf465-119">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="cf465-120">.NET Core</span><span class="sxs-lookup"><span data-stu-id="cf465-120">.NET Core</span></span> | <span data-ttu-id="cf465-121">Estilo SDK</span><span class="sxs-lookup"><span data-stu-id="cf465-121">SDK-style</span></span> | [<span data-ttu-id="cf465-122">CLI do dotnet</span><span class="sxs-lookup"><span data-stu-id="cf465-122">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="cf465-123">Os projetos criados antes do Visual Studio 2017 não são do tipo SDK.</span><span class="sxs-lookup"><span data-stu-id="cf465-123">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="cf465-124">Use a CLI `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="cf465-124">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="cf465-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="cf465-125">.NET Framework</span></span> | <span data-ttu-id="cf465-126">Estilo não SDK</span><span class="sxs-lookup"><span data-stu-id="cf465-126">Non-SDK-style</span></span> | [<span data-ttu-id="cf465-127">CLI do nuget.exe</span><span class="sxs-lookup"><span data-stu-id="cf465-127">nuget.exe CLI</span></span>](../install-nuget-client-tools.md#nugetexe-cli) | <span data-ttu-id="cf465-128">Os projetos do .NET Framework criados usando outros métodos podem ser projetos em estilo SDK.</span><span class="sxs-lookup"><span data-stu-id="cf465-128">.NET Framework projects created using other methods may be SDK-style projects.</span></span> <span data-ttu-id="cf465-129">Para isso, use o [CLI do dotnet](../install-nuget-client-tools.md#dotnetexe-cli) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="cf465-129">For these, use [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) instead.</span></span> |
| <span data-ttu-id="cf465-130">Projeto .NET [migrado](../reference/migrate-packages-config-to-package-reference.md)</span><span class="sxs-lookup"><span data-stu-id="cf465-130">[Migrated](../reference/migrate-packages-config-to-package-reference.md) .NET project</span></span> | <span data-ttu-id="cf465-131">Estilo não SDK</span><span class="sxs-lookup"><span data-stu-id="cf465-131">Non-SDK-style</span></span>| <span data-ttu-id="cf465-132">Para criar pacotes, use [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="cf465-132">To create packages, use [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) to create packages.</span></span> | <span data-ttu-id="cf465-133">Para criar pacotes, `msbuild -t:pack` é recomendado.</span><span class="sxs-lookup"><span data-stu-id="cf465-133">To create packages, `msbuild -t:pack` is recommended.</span></span> <span data-ttu-id="cf465-134">Caso contrário, use o [CLI do dotnet](../install-nuget-client-tools.md#dotnetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="cf465-134">Otherwise, use the [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span></span> <span data-ttu-id="cf465-135">Projetos migrados não são projetos no estilo SDK.</span><span class="sxs-lookup"><span data-stu-id="cf465-135">Migrated projects are not SDK-style projects.</span></span> |

## <a name="check-the-project-format"></a><span data-ttu-id="cf465-136">Verificar o formato do projeto</span><span class="sxs-lookup"><span data-stu-id="cf465-136">Check the project format</span></span>

<span data-ttu-id="cf465-137">Se você não tiver certeza se o projeto está no formato de estilo SDK ou não, procure o atributo SDK no elemento `<Project>` no arquivo de projeto (para C#, é o arquivo \*.csproj).</span><span class="sxs-lookup"><span data-stu-id="cf465-137">If you're unsure whether the project is SDK-style format or not, look for the SDK attribute in the `<Project>` element in the project file (For C#, this is the \*.csproj file).</span></span> <span data-ttu-id="cf465-138">Se houver, isso significará que o projeto está no estilo SDK.</span><span class="sxs-lookup"><span data-stu-id="cf465-138">If it is present, the project is an SDK-style project.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a><span data-ttu-id="cf465-139">Verifique o formato do projeto no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cf465-139">Check the project format in Visual Studio</span></span>

<span data-ttu-id="cf465-140">Se você estiver trabalhando no Visual Studio, poderá verificar rapidamente o formato do projeto usando um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="cf465-140">If you are working in Visual Studio, you can quickly check the project format using one of the following methods:</span></span>

- <span data-ttu-id="cf465-141">Clique com o botão direito do mouse no projeto no Gerenciador de Soluções e selecione **Editar myprojectname.csproj**.</span><span class="sxs-lookup"><span data-stu-id="cf465-141">Right-click the project in Solution Explorer and select **Edit myprojectname.csproj**.</span></span>

   <span data-ttu-id="cf465-142">Essa opção só está disponível a partir do Visual Studio 2017 para projetos que usam o atributo de estilo SDK.</span><span class="sxs-lookup"><span data-stu-id="cf465-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="cf465-143">Caso contrário, use o outro método.</span><span class="sxs-lookup"><span data-stu-id="cf465-143">Otherwise, use the other method.</span></span>

   ![Editar o arquivo de projeto](media/edit-project-file.png)

   <span data-ttu-id="cf465-145">Um projeto no estilo SDK mostra o [atributo SDK](/dotnet/core/tools/csproj#additions) no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="cf465-145">An SDK-style project shows the [SDK attribute](/dotnet/core/tools/csproj#additions) in the project file.</span></span>
   
- <span data-ttu-id="cf465-146">No menu **Projeto**, escolha **Descarregar projeto** (ou clique com o botão direito e escolha **Descarregar projeto**).</span><span class="sxs-lookup"><span data-stu-id="cf465-146">From the **Project** menu, choose **Unload Project** (or right-click the project and choose **Unload Project**).</span></span>

   <span data-ttu-id="cf465-147">Este projeto não incluirá o atributo SDK no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="cf465-147">This project will not include the SDK attribute in the project file.</span></span> <span data-ttu-id="cf465-148">Não é um projeto no estilo SDK.</span><span class="sxs-lookup"><span data-stu-id="cf465-148">It is not an SDK-style project.</span></span>

   ![Descarregar o projeto](media/unload-project.png)

   <span data-ttu-id="cf465-150">Em seguida, clique com o botão direito do mouse no projeto descarregado e escolha **Editar myprojectname.csproj**.</span><span class="sxs-lookup"><span data-stu-id="cf465-150">Then, right-click the unloaded project and choose **Edit myprojectname.csproj**.</span></span>

## <a name="see-also"></a><span data-ttu-id="cf465-151">Consulte também</span><span class="sxs-lookup"><span data-stu-id="cf465-151">See also</span></span>

- [<span data-ttu-id="cf465-152">Criar pacotes do .NET Standard com a CLI do dotnet</span><span class="sxs-lookup"><span data-stu-id="cf465-152">Create .NET Standard Packages with dotnet CLI</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="cf465-153">Criar pacotes do .NET Standard com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cf465-153">Create .NET Standard Packages with Visual Studio</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [<span data-ttu-id="cf465-154">Criar e publicar um pacote do .NET Framework (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="cf465-154">Create and publish a .NET Framework package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [<span data-ttu-id="cf465-155">Empacotamento e restauração do NuGet como destinos do MSBuild</span><span class="sxs-lookup"><span data-stu-id="cf465-155">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
