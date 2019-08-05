---
title: Multiplataformas para pacotes do NuGet em seu arquivo de projeto
description: Descrição dos diversos métodos para várias versões do .NET Framework de dentro de um único pacote do NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: b7870bb6aac39f0865d88efc8c16751fdbecc3a8
ms.sourcegitcommit: cae759ad8518c049575a30ad3bf04fe5d06244fb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2019
ms.locfileid: "68616783"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a><span data-ttu-id="322a3-103">Suporte a várias versões de .NET Framework em seu arquivo de projeto</span><span class="sxs-lookup"><span data-stu-id="322a3-103">Support multiple .NET Framework versions in your project file</span></span>

<span data-ttu-id="322a3-104">Ao criar um projeto pela primeira vez, recomendamos criar uma biblioteca de classes .NET Standard, pois ela fornece compatibilidade com uma grande variedade de projetos de consumo.</span><span class="sxs-lookup"><span data-stu-id="322a3-104">When you first create a project, we recommend you create a .NET Standard class library, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="322a3-105">Ao usar o .NET Standard, é possível adicionar [suporte de plataforma cruzada](/dotnet/standard/library-guidance/cross-platform-targeting) a uma biblioteca .NET por padrão.</span><span class="sxs-lookup"><span data-stu-id="322a3-105">By using .NET Standard, you add [cross-platform support](/dotnet/standard/library-guidance/cross-platform-targeting) to a .NET library by default.</span></span> <span data-ttu-id="322a3-106">No entanto, em alguns cenários, talvez seja necessário incluir um código direcionado a uma estrutura específica.</span><span class="sxs-lookup"><span data-stu-id="322a3-106">However, in some scenarios, you may also need to include code that targets a particular framework.</span></span> <span data-ttu-id="322a3-107">Este artigo mostra como fazer isso para projetos de [estilo SDK](../resources/check-project-format.md).</span><span class="sxs-lookup"><span data-stu-id="322a3-107">This article shows you how to do that for [SDK-style](../resources/check-project-format.md) projects.</span></span>

<span data-ttu-id="322a3-108">Para projetos de estilo SDK, é possível configurar o suporte para várias estruturas de destinos ([TFM](/dotnet/standard/frameworks)) no arquivo de projeto e, em seguida, usar `dotnet pack` ou `msbuild /t:pack` para criar o pacote.</span><span class="sxs-lookup"><span data-stu-id="322a3-108">For SDK-style projects, you can configure support for multiple targets frameworks ([TFM](/dotnet/standard/frameworks)) in your project file, then use `dotnet pack` or `msbuild /t:pack` to create the package.</span></span>

> [!NOTE]
> <span data-ttu-id="322a3-109">A CLI nuget.exe não é compatível com o empacotamento de projetos em estilo SDK, portanto é preciso usar `dotnet pack` ou `msbuild /t:pack`.</span><span class="sxs-lookup"><span data-stu-id="322a3-109">nuget.exe CLI does not support packing SDK-style projects, so you should only use `dotnet pack` or `msbuild /t:pack`.</span></span> <span data-ttu-id="322a3-110">É recomendável [incluir todas as propriedades](../reference/msbuild-targets.md#pack-target) que geralmente estão no arquivo `.nuspec` no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="322a3-110">We recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="322a3-111">Para oferecer suporte a várias versões do .NET Framework em um projeto de estilo não SDK, confira [Suporte a várias versões do .NET Framework](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="322a3-111">To target multiple .NET Framework versions in a non-SDK-style project, see [Supporting multiple .NET Framework versions](supporting-multiple-target-frameworks.md).</span></span>

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a><span data-ttu-id="322a3-112">Criar um projeto compatível com várias versões de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="322a3-112">Create a project that supports multiple .NET Framework versions</span></span>

1. <span data-ttu-id="322a3-113">Crie uma nova biblioteca de classes .NET Standard no Visual Studio ou use `dotnet new classlib`.</span><span class="sxs-lookup"><span data-stu-id="322a3-113">Create a new .NET Standard class library either in Visual Studio or use `dotnet new classlib`.</span></span>

   <span data-ttu-id="322a3-114">Recomendamos criar uma biblioteca de classes .NET Standard para obter a melhor compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="322a3-114">We recommend that you create a .NET Standard class library for best compatibility.</span></span>

2. <span data-ttu-id="322a3-115">Edite o arquivo *.csproj* para ser compatível com as estruturas de destino.</span><span class="sxs-lookup"><span data-stu-id="322a3-115">Edit the *.csproj* file to support the target frameworks.</span></span>

   <span data-ttu-id="322a3-116">Por exemplo, altere `<TargetFramework>netstandard2.0</TargetFramework>` para `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`.</span><span class="sxs-lookup"><span data-stu-id="322a3-116">For example, change `<TargetFramework>netstandard2.0</TargetFramework>` to `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`.</span></span>

   <span data-ttu-id="322a3-117">Certifique-se de alterar o elemento XML de singular para plural (adicione o plural às marcas de abrir e fechar).</span><span class="sxs-lookup"><span data-stu-id="322a3-117">Make sure that you change the XML element changed from singular to plural (add the "s" to both the open and close tags).</span></span>

3. <span data-ttu-id="322a3-118">Se você tem qualquer código que funciona apenas em um TFM, use `#if NET45` ou `#if NETSTANDARD20` para separar o código dependente do TFM.</span><span class="sxs-lookup"><span data-stu-id="322a3-118">If you have any code that only works in one TFM, you can use `#if NET45` or `#if NETSTANDARD20` to separate TFM-dependent code.</span></span> <span data-ttu-id="322a3-119">Para saber mais, confira [Como usar Multiplataformas](/dotnet/core/tutorials/libraries#how-to-multitarget). Por exemplo, use o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="322a3-119">(For more information, see [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) For example, you can use the following code:</span></span>

   ```csharp
   public string Platform {
      get {
   #if NET45
         return ".NET Framework"
   #elif NETSTANDARD2_0
         return ".NET Standard"
   #else
   #error This code block does not match csproj TargetFrameworks list
   #endif
      }
   }
   ```

4. <span data-ttu-id="322a3-120">Adicione qualquer metadado do NuGet desejado a *.csproj* como propriedades do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="322a3-120">Add any NuGet metadata you want to the *.csproj* as MSBuild properties.</span></span>

   <span data-ttu-id="322a3-121">Para obter a lista de metadados de pacote disponíveis e os nomes de propriedade do MSBuild, confira o [pacote de destino](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="322a3-121">For the list of available package metadata and the MSBuild property names, see [pack target](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="322a3-122">Confira também [Controlar ativos de dependência](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="322a3-122">Also see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

   <span data-ttu-id="322a3-123">Se quiser separar as propriedades relacionadas à compilação dos metadados do NuGet, use um `PropertyGroup` diferente ou coloque as propriedades do NuGet em outro arquivo e use a diretiva `Import` do MSBuild para incluí-lo.</span><span class="sxs-lookup"><span data-stu-id="322a3-123">If you want to separate build-related properties from NuGet metadata, you can use a different `PropertyGroup`, or put the NuGet properties in another file and use MSBuild's `Import` directive to include it.</span></span> <span data-ttu-id="322a3-124">`Directory.Build.Props` e `Directory.Build.Targets` também têm suporte a partir do MSBuild 15.0.</span><span class="sxs-lookup"><span data-stu-id="322a3-124">`Directory.Build.Props` and `Directory.Build.Targets` are also supported starting with MSBuild 15.0.</span></span>

5. <span data-ttu-id="322a3-125">Agora, use `dotnet pack` e os *.nupkg* resultantes como destino do .NET Standard 2.0 e do .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="322a3-125">Now, use `dotnet pack` and the resulting *.nupkg* targets both .NET Standard 2.0 and .NET Framework 4.5.</span></span>

<span data-ttu-id="322a3-126">Este é o arquivo *.csproj* que é gerado usando as etapas anteriores e o SDK do .NET Core 2.2.</span><span class="sxs-lookup"><span data-stu-id="322a3-126">Here is the *.csproj* file that is generated using the preceding steps and .NET Core SDK 2.2.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a><span data-ttu-id="322a3-127">Consulte também</span><span class="sxs-lookup"><span data-stu-id="322a3-127">See also</span></span>

* [<span data-ttu-id="322a3-128">Como especificar estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="322a3-128">How to specify target frameworks</span></span>](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [<span data-ttu-id="322a3-129">Direcionamento de plataforma cruzada</span><span class="sxs-lookup"><span data-stu-id="322a3-129">Cross-platform targeting</span></span>](/dotnet/standard/library-guidance/cross-platform-targeting)
