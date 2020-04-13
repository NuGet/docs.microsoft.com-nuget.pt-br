---
title: Selecionar os assemblies referenciados por projetos
description: Disponibilize um subconjunto de assemblies no pacote para o compilador, enquanto todos os assemblies estão disponíveis em runtime.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b32075c3f2c06c15c07d36602bdabdaee8b9405a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427471"
---
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="12932-103">Selecionar os assemblies referenciados por projetos</span><span class="sxs-lookup"><span data-stu-id="12932-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="12932-104">As referências de assembly explícitas permitem que um subconjunto de assemblies seja usado para o IntelliSense e a compilação, enquanto todos os assemblies estão disponíveis em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="12932-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="12932-105">`PackageReference` e `packages.config` funcionam de maneira diferente e, como resultado, os autores do pacote precisam tomar cuidado para criar o pacote de modo que ele seja compatível com ambos os tipos de projetos.</span><span class="sxs-lookup"><span data-stu-id="12932-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="12932-106">As referências de assembly explícitas estão relacionadas aos assemblies .NET.</span><span class="sxs-lookup"><span data-stu-id="12932-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="12932-107">Não é um método para distribuir assemblies nativos que são invocados por P/Invoke por um assembly gerenciado.</span><span class="sxs-lookup"><span data-stu-id="12932-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="12932-108">Suporte a `PackageReference`</span><span class="sxs-lookup"><span data-stu-id="12932-108">`PackageReference` support</span></span>

<span data-ttu-id="12932-109">Quando um projeto usar um pacote com `PackageReference` e o pacote contiver um diretório `ref\<tfm>\`, o NuGet classificará aqueles assemblies como ativos em tempo de compilação, enquanto os assemblies `lib\<tfm>\` serão classificados como ativos em runtime.</span><span class="sxs-lookup"><span data-stu-id="12932-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="12932-110">Os assemblies em `ref\<tfm>\` não são usados em runtime.</span><span class="sxs-lookup"><span data-stu-id="12932-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="12932-111">Isso significa que é necessário que qualquer assembly em `ref\<tfm>\` tenha um assembly correspondente em `lib\<tfm>\` ou um diretório `runtime\` relevante, caso contrário, poderão ocorrer erros em runtime.</span><span class="sxs-lookup"><span data-stu-id="12932-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="12932-112">Como os assemblies em `ref\<tfm>\` não são usados em runtime, eles podem ser [assemblies somente de metadados](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) para reduzir o tamanho do pacote.</span><span class="sxs-lookup"><span data-stu-id="12932-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="12932-113">Se um pacote contiver o elemento `<references>` nuspec (usado por `packages.config`, confira abaixo) e não contiver assemblies em `ref\<tfm>\`, o NuGet anunciará os assemblies listados no elemento `<references>` nuspec como ativos de tempo de compilação e de execução.</span><span class="sxs-lookup"><span data-stu-id="12932-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="12932-114">Isso significa que haverá exceções de runtime quando os assemblies referenciados precisarem carregar qualquer outro assembly no diretório `lib\<tfm>\`.</span><span class="sxs-lookup"><span data-stu-id="12932-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="12932-115">Se o pacote contiver um diretório `runtime\`, o NuGet não poderá usar os ativos do diretório `lib\`.</span><span class="sxs-lookup"><span data-stu-id="12932-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="12932-116">Suporte a `packages.config`</span><span class="sxs-lookup"><span data-stu-id="12932-116">`packages.config` support</span></span>

<span data-ttu-id="12932-117">Normalmente, os projetos que usam `packages.config` para gerenciar pacotes NuGet adicionam referências a todos os assemblies do diretório `lib\<tfm>\`.</span><span class="sxs-lookup"><span data-stu-id="12932-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="12932-118">O diretório `ref\` foi adicionado para dar suporte a `PackageReference` e, portanto, não é considerado ao usar `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="12932-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="12932-119">Para definir explicitamente quais conjuntos são `packages.config`referenciados para projetos de uso, o pacote deve usar o [ `<references>` elemento no arquivo nuspec](../reference/nuspec.md#explicit-assembly-references).</span><span class="sxs-lookup"><span data-stu-id="12932-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="12932-120">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="12932-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="12932-121">O projeto `packages.config` usa um processo chamado [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) para copiar os assemblies para o diretório de saída `bin\<configuration>\`.</span><span class="sxs-lookup"><span data-stu-id="12932-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="12932-122">O assembly do projeto é copiado e, em seguida, o sistema de build examina o manifesto do assembly em busca de assemblies referenciados. Depois, ele copia esses assemblies e repete o processo recursivamente para todos os assemblies.</span><span class="sxs-lookup"><span data-stu-id="12932-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="12932-123">Isso significa que, se um dos assemblies do diretório `lib\<tfm>\` não estiver listado em nenhum outro manifesto do assembly como uma dependência (se o assembly for carregado em runtime usando `Assembly.Load`, o MEF ou outra estrutura de injeção de dependência), ele poderá não ser copiado para o diretório de saída `bin\<configuration>\` do projeto, apesar de estar em `bin\<tfm>\`.</span><span class="sxs-lookup"><span data-stu-id="12932-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="12932-124">Exemplo</span><span class="sxs-lookup"><span data-stu-id="12932-124">Example</span></span>

<span data-ttu-id="12932-125">Meu pacote conterá três assemblies, `MyLib.dll`, `MyHelpers.dll` e `MyUtilities.dll`, direcionados ao .NET Framework 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="12932-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="12932-126">`MyUtilities.dll` contém classes que se destinam a ser usadas somente pelos outros dois assemblies, portanto, não quero disponibilizar essas classes no IntelliSense ou em tempo de compilação para projetos que usam meu pacote.</span><span class="sxs-lookup"><span data-stu-id="12932-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="12932-127">Meu arquivo `nuspec` precisa conter os seguintes elementos XML:</span><span class="sxs-lookup"><span data-stu-id="12932-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="12932-128">e os arquivos no pacote serão:</span><span class="sxs-lookup"><span data-stu-id="12932-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
