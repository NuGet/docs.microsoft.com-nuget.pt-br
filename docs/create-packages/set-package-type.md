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
# <a name="set-a-nuget-package-type"></a>Definir um tipo de pacote NuGet

Os pacotes podem ser marcados com mais um ou mais *tipos de pacote* para indicar seu uso pretendido.

## <a name="known-package-types"></a>Tipos de pacote conhecidos

- Pacotes do tipo `Dependency` adicionam ativos de tempo de build ou de execução a bibliotecas e aplicativos e podem ser instalados em qualquer tipo de projeto (supondo que eles sejam compatíveis).

- `DotnetTool` pacotes de tipo são ferramentas .NET que podem ser instaladas pela [CLI do dotnet](/dotnet/articles/core/tools/index).

- `Template` os pacotes de tipo fornecem [modelos personalizados](/dotnet/core/tools/custom-templates) que podem ser usados para criar arquivos ou projetos, como um aplicativo, serviço, ferramenta ou biblioteca de classes.

Pacotes não marcados com um tipo, incluindo todos os pacotes criados com versões anteriores do NuGet, usam o tipo `Dependency` como padrão.

> [!NOTE]
> O suporte para tipos de pacote foi adicionado no NuGet 3,5.
> Se você não precisar de um tipo de pacote personalizado, é melhor *não* definir explicitamente o tipo de pacote.
> O NuGet usa como padrão o `Dependency` tipo quando nenhum tipo é especificado.

## <a name="custom-package-types"></a>Tipos de pacote personalizados

Você pode marcar seu pacote com um ou mais tipos de pacote personalizados se seu uso não se adequar aos [tipos de pacote conhecidos](#known-package-types).

Por exemplo, imagine que os clientes do `Contoso` aplicativo possam instalar extensões. O aplicativo pode exigir que os autores de extensão usem o tipo de pacote personalizado `ContosoExtension` para identificar seus pacotes como extensões apropriadas que seguem as convenções necessárias.

> [!WARNING]
> Um pacote com um tipo de pacote personalizado não pode ser instalado pelo Visual Studio ou nuget.exe. Consulte [NuGet/Home # 10468](https://github.com/NuGet/Home/issues/10468) para obter mais informações.

# <a name="using-dotnet-cli"></a>[Usando a CLI dotnet](#tab/dotnet)

Os tipos de pacote podem ser definidos no arquivo de projeto ( `.csproj` ):

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

Pacotes com vários usos pretendidos podem ser marcados com vários tipos de pacote usando o `;` delimitador:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

Os tipos de pacote podem ter controle de versão usando um `,` delimitador entre o tipo de pacote e sua [`Version`](/dotnet/api/system.version) cadeia de caracteres:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[Usando nuget.exe](#tab/nugetexe)

Os tipos de pacote são definidos no `.nuspec` arquivo dentro de um `packageTypes\packageType` nó sob o `<metadata>` elemento:

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

Pacotes com vários usos pretendidos podem ser marcados com vários tipos de pacote:

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

Os tipos de pacote podem ter controle de versão usando uma [`Version`](/dotnet/api/system.version) cadeia de caracteres:

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

O formato de uma cadeia de caracteres de tipo de pacote é exatamente como uma ID de pacote. Ou seja, um tipo de pacote é uma cadeia de caracteres que não diferencia maiúsculas de minúsculas que corresponde à expressão regular `^\w+([_.-]\w+)*$` com pelo menos um caractere e, no máximo, 100 caracteres.

Se fornecido, a versão do tipo de pacote é uma [`Version`](/dotnet/api/system.version) cadeia de caracteres. A versão do tipo de pacote é opcional e o padrão é `0.0` .
