---
title: Criar um pacote NuGet usando MSBuild
description: Um guia detalhado para o processo de design e criação de um pacote do NuGet, incluindo os principais pontos de decisão como arquivos e controle de versão.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9512899a4086d17d2584f16833aba33efb321eae
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380699"
---
# <a name="create-a-nuget-package-using-msbuild"></a>Criar um pacote NuGet usando MSBuild

Ao criar um pacote NuGet de seu criar, você empacota essa funcionalidade em um componente que pode ser compartilhado e usado por uma infinidade de outros desenvolvedores. Este artigo descreve como criar um pacote usando MSBuild. O MSBuild vem pré-instalado com todas as cargas de trabalho do Visual Studio que contêm o NuGet. Além disso, você também pode usar o MSBuild por meio da CLI do dotnet com [dotnet msbuild](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild)

Para projetos .NET Core e .NET Standard que usam projetos no [formato de estilo SDK](../resources/check-project-format.md) e quaisquer outros estilos SDK, o NuGet usa as informações do arquivo de projeto diretamente para criar um pacote.  Para projetos que não são de estilo SDK e que usam `<PackageReference>`, o NuGet também usa o arquivo de projeto para criar um pacote.

Projetos de estilo SDK têm a funcionalidade de empacotamento disponível por padrão. Para projetos de PackageReference que não são de estilo SDK, você precisa adicionar o pacote NuGet.Build.Tasks.Pack às dependências do projeto. Para obter informações detalhadas sobre os destinos de empacotamento do MSBuild, confira [Empacotamento e restauração do NuGet como destinos do MSBuild](../reference/msbuild-targets.md).

O comando que cria um pacote, `msbuild -t:pack`, é a funcionalidade equivalente a `dotnet pack`.

> [!IMPORTANT]
> Este tópico se aplica a projetos com [estilo SDK](../resources/check-project-format.md), normalmente projetos do .NET Core e do .NET Standard, e a projetos que não são de estilo SDK que usam PackageReference.

## <a name="set-properties"></a>Definir propriedades

As propriedades a seguir são necessárias para criar um pacote.

- `PackageId`, o identificador de pacotes, que deve ser exclusivo na galeria que hospeda o pacote. Se não for especificado, o valor padrão será `AssemblyName`.
- `Version`, um número de versão específico na forma *Principal.Secundário.Patch[-Sufixo]* em que *-Sufixo* identifica as [versões de pré-lançamento](prerelease-packages.md). Se esse campo não for especificado, o valor padrão será 1.0.0.
- O título do pacote como ele deve aparecer no host (como nuget.org)
- `Authors`, informações de autor e proprietário. Se não for especificado, o valor padrão será `AssemblyName`.
- `Company`, o nome da empresa. Se não for especificado, o valor padrão será `AssemblyName`.

No Visual Studio, é possível definir esses valores nas propriedades do projeto (clique com o botão direito do mouse no projeto no Gerenciador de Soluções, escolha **Propriedades** e selecione a guia **Pacote**). Você também pode definir essas propriedades diretamente nos arquivos do projeto ( *.csproj*).

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Dê ao pacote um identificador exclusivo em nuget.org ou qualquer origem de pacote que estiver usando.

O exemplo a seguir mostra um arquivo de projeto simples e completo com essas propriedades incluídas.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

Defina também as propriedades opcionais, como `Title`, `PackageDescription` e `PackageTags`, conforme descrito em [Destinos do pacote MSBuild](../reference/msbuild-targets.md#pack-target), [Controlar ativos de dependência](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) e [Propriedades de metadados do NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

> [!NOTE]
> Para pacotes compilados para consumo público, preste atenção especial à propriedade **PackageTags**, à medida que as marcas ajudam outras pessoas a localizar o pacote e entender o que ele faz.

Para obter detalhes sobre como declarar dependências e especificar números de versão, consulte [Referências de pacote em arquivos de projeto](../consume-packages/package-references-in-project-files.md) e [Controle de versão do pacote](../concepts/package-versioning.md). Também é possível extrair ativos de dependências diretamente no pacote usando os atributos `<IncludeAssets>` e `<ExcludeAssets>`. Para saber mais, confira [Controlar ativos de dependência](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Escolher um identificador de pacote exclusivo e definir o número de versão

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a>Adicionar o pacote NuGet.Build.Tasks.Pack

Se você estiver usando o MSBuild com um projeto que não é de estilo SDK e com PackageReference, adicione o pacote NuGet.Build.Tasks.Pack ao projeto.

1. Abra o arquivo de projeto e adicione o seguinte após o elemento `<PropertyGroup>`:

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. Abra um prompt de comando do Desenvolvedor (na caixa **Pesquisar**, digite **Prompt de Comando do Desenvolvedor**).

   Você normalmente deseja iniciar o Prompt de Comando do Desenvolvedor para Visual Studio usando o menu **Iniciar**, pois ele estará configurado com todos os caminhos necessários para o MSBuild.

3. Alterne para a pasta que contém o arquivo de projeto e digite o seguinte comando para instalar o pacote NuGet.Build.Tasks.Pack.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   Verifique se a saída de MSBuild indica que a compilação foi concluída com êxito.

## <a name="run-the-msbuild--tpack-command"></a>Execute o comando msbuild -t:pack

Para compilar um pacote do NuGet (um arquivo `.nupkg`) do projeto, execute o comando `msbuild -t:pack`, que também compila o projeto automaticamente:

No prompt de comando do Desenvolvedor para Visual Studio, digite o seguinte comando:

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

A saída mostra o caminho até o arquivo `.nupkg`.

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a>Gerar pacote automaticamente no build

Para executar `msbuild -t:pack` automaticamente ao compilar ou restaurar o projeto, adicione a seguinte linha ao arquivo de projeto em `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Ao executar `msbuild -t:pack` em uma solução, isso empacota todos os projetos na solução que são empacotáveis (a propriedade [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) é definida como `true`).

> [!NOTE]
> Ao gerar automaticamente o pacote, o tempo de empacotamento aumenta o tempo de compilação do seu projeto.

### <a name="test-package-installation"></a>Instalação do pacote de teste

Antes de publicar um pacote, geralmente é recomendável testar o processo de instalação de um pacote em um projeto. Os testes garantem que os arquivos todos terminem em seus lugares corretos no projeto.

Você pode testar instalações manualmente no Visual Studio ou na linha de comando usando as [etapas de instalação do pacote](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package) normais.

> [!IMPORTANT]
> Os pacotes são imutáveis. Se corrigir um problema, altere o conteúdo do pacote e empacote novamente. Quando você testar novamente, ainda estará usando a versão antiga do pacote até que [limpe sua pasta de pacotes globais](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders). Isso é especialmente relevante ao testar pacotes que não usam um rótulo de pré-lançamento exclusivo em cada compilação.

## <a name="next-steps"></a>Próximas etapas

Depois de criar um pacote, que é um arquivo `.nupkg`, você pode publicá-lo na galeria de sua escolha conforme descrito em [Publicar um pacote](../nuget-org/publish-a-package.md).

Você também poderá estender os recursos do seu pacote ou dar suporte a outros cenários conforme descrito nos tópicos a seguir:

- [Empacotamento e restauração do NuGet como destinos do MSBuild](../reference/msbuild-targets.md)
- [Controle de versão do pacote](../concepts/package-versioning.md)
- [Suporte a várias estruturas de destino](../create-packages/multiple-target-frameworks-project-file.md)
- [Transformações dos arquivos de configuração e de origem](../create-packages/source-and-config-file-transformations.md)
- [Localização](../create-packages/creating-localized-packages.md)
- [Versões de pré-lançamento](../create-packages/prerelease-packages.md)
- [Definir tipo de pacote](../create-packages/set-package-type.md)
- [Criar pacotes com assemblies de interoperabilidade COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Por fim, há tipos de pacote adicionais a serem considerados:

- [Pacotes nativos](../guides/native-packages.md)
- [Pacotes de Símbolo](../create-packages/symbol-packages-snupkg.md)
