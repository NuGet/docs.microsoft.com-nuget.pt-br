---
title: Selecionar os assemblies referenciados por projetos
description: Disponibilize um subconjunto de assemblies no pacote para o compilador, enquanto todos os assemblies estão disponíveis em runtime.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b2202946d0060e09828250d240f931044d1bf485
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859025"
---
# <a name="select-assemblies-referenced-by-projects"></a>Selecionar os assemblies referenciados por projetos

As referências de assembly explícitas permitem que um subconjunto de assemblies seja usado para o IntelliSense e a compilação, enquanto todos os assemblies estão disponíveis em tempo de execução. `PackageReference` e `packages.config` funcionam de maneira diferente e, como resultado, os autores do pacote precisam tomar cuidado para criar o pacote de modo que ele seja compatível com ambos os tipos de projetos.

> [!Note]
> As referências de assembly explícitas estão relacionadas aos assemblies .NET. Não é um método para distribuir assemblies nativos que são invocados por P/Invoke por um assembly gerenciado.

## <a name="packagereference-support"></a>Suporte a `PackageReference`

Quando um projeto usar um pacote com `PackageReference` e o pacote contiver um diretório `ref\<tfm>\`, o NuGet classificará aqueles assemblies como ativos em tempo de compilação, enquanto os assemblies `lib\<tfm>\` serão classificados como ativos em runtime. Os assemblies em `ref\<tfm>\` não são usados em runtime. Isso significa que é necessário que qualquer assembly em `ref\<tfm>\` tenha um assembly correspondente em `lib\<tfm>\` ou um diretório `runtime\` relevante, caso contrário, poderão ocorrer erros em runtime. Como os assemblies em `ref\<tfm>\` não são usados em runtime, eles podem ser [assemblies somente de metadados](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md) para reduzir o tamanho do pacote.

> [!Important]
> Se um pacote contiver o elemento `<references>` nuspec (usado por `packages.config`, confira abaixo) e não contiver assemblies em `ref\<tfm>\`, o NuGet anunciará os assemblies listados no elemento `<references>` nuspec como ativos de tempo de compilação e de execução. Isso significa que haverá exceções de runtime quando os assemblies referenciados precisarem carregar qualquer outro assembly no diretório `lib\<tfm>\`.

> [!Note]
> Se o pacote contiver um diretório `runtime\`, o NuGet não poderá usar os ativos do diretório `lib\`.

## <a name="packagesconfig-support"></a>Suporte a `packages.config`

Normalmente, os projetos que usam `packages.config` para gerenciar pacotes NuGet adicionam referências a todos os assemblies do diretório `lib\<tfm>\`. O diretório `ref\` foi adicionado para dar suporte a `PackageReference` e, portanto, não é considerado ao usar `packages.config`. Para definir explicitamente quais assemblies são referenciados para projetos usando `packages.config` , o pacote deve usar o [ `<references>` elemento no arquivo nuspec](../reference/nuspec.md#explicit-assembly-references). Por exemplo:

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> O projeto `packages.config` usa um processo chamado [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) para copiar os assemblies para o diretório de saída `bin\<configuration>\`. O assembly do projeto é copiado e, em seguida, o sistema de build examina o manifesto do assembly em busca de assemblies referenciados. Depois, ele copia esses assemblies e repete o processo recursivamente para todos os assemblies. Isso significa que, se um dos assemblies do diretório `lib\<tfm>\` não estiver listado em nenhum outro manifesto do assembly como uma dependência (se o assembly for carregado em runtime usando `Assembly.Load`, o MEF ou outra estrutura de injeção de dependência), ele poderá não ser copiado para o diretório de saída `bin\<configuration>\` do projeto, apesar de estar em `bin\<tfm>\`.

## <a name="example"></a>Exemplo

Meu pacote conterá três assemblies, `MyLib.dll`, `MyHelpers.dll` e `MyUtilities.dll`, direcionados ao .NET Framework 4.7.2. `MyUtilities.dll` contém classes que se destinam a ser usadas somente pelos outros dois assemblies, portanto, não quero disponibilizar essas classes no IntelliSense ou em tempo de compilação para projetos que usam meu pacote. Meu arquivo `nuspec` precisa conter os seguintes elementos XML:

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

e os arquivos no pacote serão:

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
