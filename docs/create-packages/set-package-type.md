---
title: Definir um tipo de pacote NuGet
description: Descreve os tipos de pacotes para indicar o uso pretendido de um pacote.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: fa369e8327330e13f5adda39a75008e42ac99896
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067266"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="6b554-103">Definir um tipo de pacote NuGet</span><span class="sxs-lookup"><span data-stu-id="6b554-103">Set a NuGet package type</span></span>

<span data-ttu-id="6b554-104">Os pacotes podem ser marcados com mais um ou mais *tipos de pacote* para indicar seu uso pretendido.</span><span class="sxs-lookup"><span data-stu-id="6b554-104">Packages can be marked with one more more *package types* to indicate its intended use.</span></span>

## <a name="known-package-types"></a><span data-ttu-id="6b554-105">Tipos de pacote conhecidos</span><span class="sxs-lookup"><span data-stu-id="6b554-105">Known package types</span></span>

- <span data-ttu-id="6b554-106">Pacotes do tipo `Dependency` adicionam ativos de tempo de build ou de execução a bibliotecas e aplicativos e podem ser instalados em qualquer tipo de projeto (supondo que eles sejam compatíveis).</span><span class="sxs-lookup"><span data-stu-id="6b554-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="6b554-107">`DotnetTool` pacotes de tipo são ferramentas .NET que podem ser instaladas pela [CLI do dotnet](/dotnet/articles/core/tools/index).</span><span class="sxs-lookup"><span data-stu-id="6b554-107">`DotnetTool` type packages are .NET tools that can be installed by the [dotnet CLI](/dotnet/articles/core/tools/index).</span></span>

- <span data-ttu-id="6b554-108">`Template` os pacotes de tipo fornecem [modelos personalizados](/dotnet/core/tools/custom-templates) que podem ser usados para criar arquivos ou projetos, como um aplicativo, serviço, ferramenta ou biblioteca de classes.</span><span class="sxs-lookup"><span data-stu-id="6b554-108">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

<span data-ttu-id="6b554-109">Pacotes não marcados com um tipo, incluindo todos os pacotes criados com versões anteriores do NuGet, usam o tipo `Dependency` como padrão.</span><span class="sxs-lookup"><span data-stu-id="6b554-109">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

> [!NOTE]
> <span data-ttu-id="6b554-110">O suporte para tipos de pacote foi adicionado no NuGet 3,5.</span><span class="sxs-lookup"><span data-stu-id="6b554-110">Support for package types was added in NuGet 3.5.</span></span>
> <span data-ttu-id="6b554-111">Se você não precisar de um tipo de pacote personalizado, é melhor *não* definir explicitamente o tipo de pacote.</span><span class="sxs-lookup"><span data-stu-id="6b554-111">If you don't need a custom package type, it's best to *not* explicitly set the package type.</span></span>
> <span data-ttu-id="6b554-112">O NuGet usa como padrão o `Dependency` tipo quando nenhum tipo é especificado.</span><span class="sxs-lookup"><span data-stu-id="6b554-112">NuGet defaults to the `Dependency` type when no type is specified.</span></span>

## <a name="custom-package-types"></a><span data-ttu-id="6b554-113">Tipos de pacote personalizados</span><span class="sxs-lookup"><span data-stu-id="6b554-113">Custom package types</span></span>

<span data-ttu-id="6b554-114">Você pode marcar seu pacote com um ou mais tipos de pacote personalizados se seu uso não se adequar aos [tipos de pacote conhecidos](#known-package-types).</span><span class="sxs-lookup"><span data-stu-id="6b554-114">You can mark your package with one or more custom package types if its use does not fit the [known package types](#known-package-types).</span></span>

<span data-ttu-id="6b554-115">Por exemplo, imagine que os clientes do `Contoso` aplicativo possam instalar extensões.</span><span class="sxs-lookup"><span data-stu-id="6b554-115">For example, imagine that customers of the `Contoso` app can install extensions.</span></span> <span data-ttu-id="6b554-116">O aplicativo pode exigir que os autores de extensão usem o tipo de pacote personalizado `ContosoExtension` para identificar seus pacotes como extensões apropriadas que seguem as convenções necessárias.</span><span class="sxs-lookup"><span data-stu-id="6b554-116">The app could require extension authors to use the custom package type `ContosoExtension` to identify their packages as proper extensions that follow the required conventions.</span></span>

> [!WARNING]
> <span data-ttu-id="6b554-117">Um pacote com um tipo de pacote personalizado não pode ser instalado pelo Visual Studio ou nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="6b554-117">A package with a custom package type cannot be installed by Visual Studio or nuget.exe.</span></span> <span data-ttu-id="6b554-118">Consulte [NuGet/Home # 10468](https://github.com/NuGet/Home/issues/10468) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="6b554-118">See [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468) for more information.</span></span>

# <a name="using-dotnet-cli"></a>[<span data-ttu-id="6b554-119">Usando a CLI dotnet</span><span class="sxs-lookup"><span data-stu-id="6b554-119">Using dotnet CLI</span></span>](#tab/dotnet)

<span data-ttu-id="6b554-120">Os tipos de pacote podem ser definidos no arquivo de projeto ( `.csproj` ):</span><span class="sxs-lookup"><span data-stu-id="6b554-120">Package types can be set in the project file (`.csproj`):</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="6b554-121">Pacotes com vários usos pretendidos podem ser marcados com vários tipos de pacote usando o `;` delimitador:</span><span class="sxs-lookup"><span data-stu-id="6b554-121">Packages with multiple intended uses can be marked with multiple package types using the `;` delimiter:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="6b554-122">Os tipos de pacote podem ter controle de versão usando um `,` delimitador entre o tipo de pacote e sua [`Version`](/dotnet/api/system.version) cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="6b554-122">Package types can be versioned using a `,` delimiter between the package type and its [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[<span data-ttu-id="6b554-123">Usando nuget.exe</span><span class="sxs-lookup"><span data-stu-id="6b554-123">Using nuget.exe</span></span>](#tab/nugetexe)

<span data-ttu-id="6b554-124">Os tipos de pacote são definidos no `.nuspec` arquivo dentro de um `packageTypes\packageType` nó sob o `<metadata>` elemento:</span><span class="sxs-lookup"><span data-stu-id="6b554-124">Package types are set in the `.nuspec` file within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="ContosoExtension" />
        </packageTypes>
    </metadata>
</package>
```

<span data-ttu-id="6b554-125">Pacotes com vários usos pretendidos podem ser marcados com vários tipos de pacote:</span><span class="sxs-lookup"><span data-stu-id="6b554-125">Packages with multiple intended uses may be marked with multiple package types:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

<span data-ttu-id="6b554-126">Os tipos de pacote podem ter controle de versão usando uma [`Version`](/dotnet/api/system.version) cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="6b554-126">Package types can be versioned using a [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" version="1.0.0.0" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

---

<span data-ttu-id="6b554-127">O formato de uma cadeia de caracteres de tipo de pacote é exatamente como uma ID de pacote.</span><span class="sxs-lookup"><span data-stu-id="6b554-127">The format of a package type string is exactly like a package ID.</span></span> <span data-ttu-id="6b554-128">Ou seja, um tipo de pacote é uma cadeia de caracteres que não diferencia maiúsculas de minúsculas que corresponde à expressão regular `^\w+([_.-]\w+)*$` com pelo menos um caractere e, no máximo, 100 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6b554-128">That is, a package type is a case-insensitive string matching the regular expression `^\w+([_.-]\w+)*$` having at least one character and at most 100 characters.</span></span>

<span data-ttu-id="6b554-129">Se fornecido, a versão do tipo de pacote é uma [`Version`](/dotnet/api/system.version) cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="6b554-129">If provided, the package type version is a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="6b554-130">A versão do tipo de pacote é opcional e o padrão é `0.0` .</span><span class="sxs-lookup"><span data-stu-id="6b554-130">The package type version is optional and defaults to `0.0`.</span></span>
