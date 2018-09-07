---
title: Passo a passo da restauração do pacote do NuGet com o Team Foundation Build
description: Um passo a passo de como restaurar pacotes do NuGet com o Team Foundation Build (no TFS e no Visual Studio Team Services).
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0e69491525fce03e504d9d455bee2718510c83c2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549879"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Configurando a restauração de pacote com o Team Foundation Build

Este artigo fornece instruções passo a passo detalhadas sobre como restaurar os pacotes como parte do [Team Services Build](/vsts/build-release/index), tanto para Git como para o Controle de Versão do Team Services.

Embora este passo a passo seja específico para o cenário que usa os Visual Studio Team Services, os conceitos também se aplicam a outros controle de versão e sistemas de build.

Aplica-se a:

- Projetos do MSBuild personalizados executados em qualquer versão do TFS
- Team Foundation Server 2012 ou superior
- Modelos do Team Foundation Build Process personalizados migrados para o TFS 2013 ou posterior
- Compilar modelos de processo com a funcionalidade de restauração do Nuget removida

Se você estiver usando o Visual Studio Team Services ou o Team Foundation Server 2013 com seus modelos de processo de compilação, a Restauração de Pacote Automática ocorrerá como parte do processo de compilação.

## <a name="the-general-approach"></a>A abordagem geral

Uma vantagem de usar o NuGet é que você pode usá-lo para evitar fazer check in de binários para seu sistema de controle de versão.

Isso é especialmente interessante se você estiver usando um sistema de [controle de versão distribuída](http://en.wikipedia.org/wiki/Distributed_revision_control) como git porque os desenvolvedores precisam clonar o repositório inteiro, incluindo o histórico completo, para começar a trabalhar localmente. Fazer check-in de binários pode causar sobrecarga significativa no repositório, visto que arquivos binários normalmente são armazenados sem compactação delta.

O NuGet tem sido compatível com a [restauração de pacotes](../consume-packages/package-restore.md) como parte do build há bastante tempo. A implementação anterior tinha um problema de ovo e a galinha para os pacotes que desejam estender o processo de build porque os pacotes restaurados do NuGet durante a compilação do projeto. No entanto, o MSBuild não permite estender o build durante o build; poderíamos argumentar que isso é um problema no MSBuild, mas eu diria que se trata de um problema inerente. Dependendo de qual aspecto você precisa estender, pode ser muito tarde registrar no momento em que o pacote é restaurado.

A solução para esse problema é verificar se os pacotes foram restaurados como a primeira etapa no processo de build:

```cli
nuget restore path\to\solution.sln
```

Quando o processo de build restaura os pacotes antes de compilar o código, você não precisa fazer check-in de arquivos `.targets`

> [!Note]
> Os pacotes devem ser criados para permitir o carregamento no Visual Studio. Caso contrário, ainda pode ser recomendável fazer check-in em arquivos `.targets` para que outros desenvolvedores possam simplesmente abrir a solução sem a necessidade de restaurar os pacotes.

O seguinte projeto de demonstração mostra como configurar o build de forma que as pastas `packages` os arquivos `.targets` não precisam passar por check-in. Ele também mostra como configurar um build automatizado no Team Foundation Service para este projeto de exemplo.

## <a name="repository-structure"></a>Estrutura do repositório

Nosso projeto de demonstração é uma ferramenta de linha de comando simples que usa o argumento de linha de comando para consultar o Bing. Ele se destina ao .NET Framework 4 e usa muitos dos [pacotes BCL](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async) e [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).

A estrutura do repositório será semelhante ao seguinte:

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

Você pode ver que não fizemos check-in na pasta `packages` nem qualquer arquivo `.targets`.

No entanto, fizemos check-in no `nuget.exe`, pois ele é necessário durante o build. Seguindo as convenções mais usadas, nós o colocamos em uma pasta `tools` compartilhada.

O código-fonte está na pasta `src`. Embora a nossa demonstração use apenas uma única solução, é possível imaginar facilmente que essa pasta contém mais de uma solução.

### <a name="ignore-files"></a>Ignorar arquivos

> [!Note]
> Atualmente, há um [bug conhecido no cliente do NuGet](https://nuget.codeplex.com/workitem/4072) que faz com que o cliente ainda adicione a pasta `packages` ao controle de versão. Uma solução alternativa é desabilitar a integração de controle do código-fonte. Para fazer isso, você precisa de um arquivo `Nuget.Config ` na pasta `.nuget` paralela à sua solução. Se essa pasta ainda não existir, você precisará criá-la. No [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), adicione o conteúdo a seguir:

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

Para se comunicar com o controle de versão que nós não temos intenção de fazer check-in nas pastas dos **pacotes**, também adicionamos ignorar arquivos ao git (`.gitignore`) e ao controle de versão do TF (`.tfignore`). Esses arquivos descrevem padrões dos arquivos para os quais você não deseja fazer check-in.

O arquivo `.gitignore` se parece com o seguinte:

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

O arquivo `.gitignore` é [muito poderoso](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html). Por exemplo, se você geralmente não quiser fazer check-in do conteúdo da pasta `packages`, mas deseja prosseguir com a orientação anterior de fazer check-in nos arquivos `.targets`, você poderia ter a seguinte regra em vez disso:

    packages
    !packages/**/*.targets

Isso excluirá todas as pastas `packages`, mas incluirá novamente todos os arquivos `.targets` contidos. Aliás, você pode encontrar um modelo para arquivos `.gitignore` especificamente projetado para as necessidades de desenvolvedores do Visual Studio [aqui](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).

O controle de versão do TF dá suporte a um mecanismo muito semelhante por meio do arquivo [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control). A sintaxe é praticamente a mesma:

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a>build.proj

Para nossa demonstração, manteremos o processo de build bastante simples. Vamos criar um projeto do MSBuild que cria todas as soluções enquanto verifica se os pacotes são restaurados antes de compilar as soluções.

Este projeto terá os três destinos convencionais `Clean`, `Build` e `Rebuild`, bem como um novo destino `RestorePackages`.

- Os destinos de `Build` e `Rebuild` dependem do `RestorePackages`. Isso garante que você pode tanto executar `Build` e `Rebuild` quanto contar com os pacotes que estão sendo restaurados.
- `Clean`, `Build` e `Rebuild` invocam o destino do MSBuild correspondente em todos os arquivos de solução.
- O destino `RestorePackages` invoca `nuget.exe` para cada arquivo de solução. Isso é feito usando a [funcionalidade de envio em lotes do MSBuild](/visualstudio/msbuild/msbuild-batching).

O resultado se parece com o seguinte:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a>Configurar o Team Build

O Team Build oferece vários modelos de processo. Para esta demonstração, estamos usando o Team Foundation Service. Contudo, instalações locais do TFS serão muito semelhantes.

O Git e o Controle de Versão do TF têm diferentes modelos de Team Build, por isso as etapas a seguir variarão dependendo de qual sistema de controle de versão você está usando. Em ambos os casos, tudo o que você precisa é selecionar o build.proj como o projeto que você deseja compilar.

Primeiro, vamos analisar o modelo de processo para o git. No modelo baseado em git, o build é selecionado por meio da propriedade `Solution to build`:

![Processo de build para git](media/PackageRestoreTeamBuildGit.png)

Observe que essa propriedade é um local em seu repositório. Como nosso `build.proj` está na raiz, simplesmente usamos `build.proj`. Se você colocar o arquivo de build em uma pasta chamada `tools`, o valor será `tools\build.proj`.

No modelo de controle de versão do TF, o projeto é selecionado por meio da propriedade `Projects`:

![Processo de build para TFVC](media/PackageRestoreTeamBuildTFVC.png)

Em contraste com modelo baseado em git, o controle de versão do TF é compatível com seletores (o botão do lado direito com três pontos). Para evitar erros de digitação, sugerimos usá-los para selecionar o projeto.
