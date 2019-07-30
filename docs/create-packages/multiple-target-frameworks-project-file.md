---
title: Multiplataformas para pacotes do NuGet em seu arquivo de projeto
description: Descrição dos diversos métodos para várias versões do .NET Framework de dentro de um único pacote do NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 1ff02871872cee9e8cbf8c7d7c74d804f7dc5b99
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68346111"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a>Suporte a várias versões de .NET Framework em seu arquivo de projeto

Ao criar um projeto pela primeira vez, recomendamos criar uma biblioteca de classes .NET Standard, pois ela fornece compatibilidade com uma grande variedade de projetos de consumo. Ao usar o .NET Standard, é possível adicionar [suporte de plataforma cruzada](/dotnet/standard/library-guidance/cross-platform-targeting) a uma biblioteca .NET por padrão. No entanto, em alguns cenários, talvez seja necessário incluir um código direcionado a uma estrutura específica. Este artigo mostra como fazer isso para projetos de [estilo SDK](../resources/check-project-format.md).

Para projetos de estilo SDK, é possível configurar o suporte para várias estruturas de destinos ([TFM](/dotnet/standard/frameworks)) no arquivo de projeto e, em seguida, usar `dotnet pack` ou `msbuild /t:pack` para criar o pacote.

> [!NOTE]
> A CLI nuget.exe não é compatível com o empacotamento de projetos em estilo SDK, portanto é preciso usar `dotnet pack` ou `msbuild /t:pack`. É recomendável [incluir todas as propriedades](../reference/msbuild-targets.md#pack-target) que geralmente estão no arquivo `.nuspec` no arquivo de projeto. Para oferecer suporte a várias versões do .NET Framework em um projeto de estilo não SDK, confira [Suporte a várias versões do .NET Framework](supporting-multiple-target-frameworks.md).

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a>Criar um projeto compatível com várias versões de .NET Framework

1. Crie uma nova biblioteca de classes .NET Standard no Visual Studio ou use `dotnet new classlib`.

   Recomendamos criar uma biblioteca de classes .NET Standard para obter a melhor compatibilidade.

2. Edite o arquivo *.csproj* para ser compatível com as estruturas de destino.

   Por exemplo, altere `<TargetFramework>netstandard2.0</TargetFramework>` para `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`.

   Certifique-se de alterar o elemento XML de singular para plural (adicione o plural às marcas de abrir e fechar).

3. Se você tem qualquer código que funciona apenas em um TFM, use `#if NET45` ou `#if NETSTANDARD20` para separar o código dependente do TFM. Para saber mais, confira [Como usar Multiplataformas](/dotnet/core/tutorials/libraries#how-to-multitarget). Por exemplo, use o seguinte código:

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

4. Adicione qualquer metadado do NuGet desejado a *.csproj* como propriedades do MSBuild.

   Para obter a lista de metadados de pacote disponíveis e os nomes de propriedade do MSBuild, confira o [pacote de destino](../reference/msbuild-targets.md#pack-target). Confira também [Controlar ativos de dependência](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

   Se quiser separar as propriedades relacionadas à compilação dos metadados do NuGet, use um `PropertyGroup` diferente ou coloque as propriedades do NuGet em outro arquivo e use a diretiva `Import` do MSBuild para incluí-lo. `Directory.Build.Props` e `Directory.Build.Targets` também têm suporte a partir do MSBuild 15.0.

5. Agora, use `dotnet pack` e os *.nupkg* resultantes como destino do .NET Standard 2.0 e do .NET Framework 4.5.

Este é o arquivo *.csproj* que é gerado usando as etapas anteriores e o SDK do .NET Core 2.2.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a>Consulte também

[Como especificar as estruturas de destino](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
[Direcionamento para plataforma cruzada](/dotnet/standard/library-guidance/cross-platform-targeting)
