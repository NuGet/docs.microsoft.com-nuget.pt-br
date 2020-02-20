---
title: Criar um pacote do NuGet usando a CLI dotnet
description: Um guia detalhado para o processo de design e criação de um pacote do NuGet, incluindo os principais pontos de decisão como arquivos e controle de versão.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: c198bb73f0e4f5a59826db905eaf4622fe8543bc
ms.sourcegitcommit: 1799d4ac23c8aacee7498fdc72c40dd1646d267b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77476250"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>Criar um pacote do NuGet usando a CLI dotnet

Independentemente do pacote ou do código que ele contém, use uma das ferramentas de CLI, seja `nuget.exe` ou `dotnet.exe`, para empacotar essa funcionalidade em um componente que possa ser compartilhado e usado por diversos desenvolvedores. Este artigo descreve como criar um pacote usando a CLI dotnet. Para instalar a CLI `dotnet`, confira [Instalar as ferramentas de cliente do NuGet](../install-nuget-client-tools.md). A partir do Visual Studio 2017, a CLI dotnet está inclusa nas cargas de trabalho do .NET Core.

Para projetos .NET Core e .NET Standard que usam projetos no [formato de estilo SDK](../resources/check-project-format.md) e quaisquer outros estilos SDK, o NuGet usa as informações do arquivo de projeto diretamente para criar um pacote. Para ver tutoriais passo a passo, confira [Criar pacotes .NET Standard com a CLI dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) e [Criar pacotes .NET Standard com o Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).

`msbuild -t:pack` é uma funcionalidade equivalente a `dotnet pack`. Para compilar com MSBuild, consulte [Criar um pacote NuGet usando MSBuild](creating-a-package-msbuild.md).

> [!IMPORTANT]
> Este tópico aplica-se a projetos no [estilo SDK](../resources/check-project-format.md), normalmente projetos .NET Core e .NET Standard.

## <a name="set-properties"></a>Definir propriedades

As propriedades a seguir são necessárias para criar um pacote.

- `PackageId`, o identificador de pacotes, que deve ser exclusivo na galeria que hospeda o pacote. Se esse campo não for especificado, o valor padrão será `AssemblyName`.
- `Version`, um número de versão específico na forma *Principal.Secundário.Patch[-Sufixo]* em que *-Sufixo* identifica as [versões de pré-lançamento](prerelease-packages.md). Se esse campo não for especificado, o valor padrão será 1.0.0.
- O título do pacote como ele deve aparecer no host (como nuget.org)
- `Authors`, informações de autor e proprietário. Se esse campo não for especificado, o valor padrão será `AssemblyName`.
- `Company`, o nome da empresa. Se esse campo não for especificado, o valor padrão será `AssemblyName`.

No Visual Studio, é possível definir esses valores nas propriedades do projeto (clique com o botão direito do mouse no projeto no Gerenciador de Soluções, escolha **Propriedades** e selecione a guia **Pacote**). Você também pode definir essas propriedades diretamente nos arquivos do projeto (`.csproj`).

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Dê ao pacote um identificador exclusivo em nuget.org ou qualquer origem de pacote que estiver usando.

O exemplo a seguir mostra um arquivo de projeto simples e completo com essas propriedades incluídas. (Você pode criar um novo projeto padrão usando o comando `dotnet new classlib`.)

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
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

## <a name="run-the-pack-command"></a>Executar o comando pack

Para compilar um pacote do NuGet (um arquivo `.nupkg`) do projeto, execute o comando `dotnet pack`, que também compila o projeto automaticamente:

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

A saída mostra o caminho até o arquivo `.nupkg`.

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Gerar pacote automaticamente no build

Para executar `dotnet pack` automaticamente ao executar `dotnet build`, adicione a seguinte linha ao arquivo de projeto em `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Ao executar `dotnet pack` em uma solução, isso empacota todos os projetos na solução que são empacotáveis (a propriedade [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) é definida como `true`).

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

- [Controle de versão do pacote](../concepts/package-versioning.md)
- [Suporte a várias estruturas de destino](../create-packages/multiple-target-frameworks-project-file.md)
- [Ícone Adicionar um pacote](../reference/nuspec.md#icon)
- [Transformações dos arquivos de configuração e de origem](../create-packages/source-and-config-file-transformations.md)
- [Localização](../create-packages/creating-localized-packages.md)
- [Versões de pré-lançamento](../create-packages/prerelease-packages.md)
- [Definir tipo de pacote](../create-packages/set-package-type.md)
- [Criar pacotes com assemblies de interoperabilidade COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Por fim, há tipos de pacote adicionais a serem considerados:

- [Pacotes nativos](../guides/native-packages.md)
- [Pacotes de símbolo](../create-packages/symbol-packages-snupkg.md)
