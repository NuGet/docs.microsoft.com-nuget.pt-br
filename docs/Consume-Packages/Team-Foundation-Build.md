---
title: "Explicação passo a passo da restauração de pacotes do NuGet com o Team Foundation Build | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3113cccd-35f7-4980-8a6e-fc06556b5064
description: Um passo a passo de como restaurar pacotes do NuGet com o Team Foundation Build (no TFS e no Visual Studio Team Services).
keywords: "Restauração do pacote do NuGet, NuGet e TFS, NuGet e VSTS, sistemas de build do NuGet, build do team foundation, projetos do MSBuild personalizados, build na nuvem, integração contínua"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82decfa1a39cb99c405840a8f13b0bc993111c09
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="e65c3-104">Configurando a restauração de pacote com o Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="e65c3-104">Setting up package restore with Team Foundation Build</span></span>

> <span data-ttu-id="e65c3-105">Aplica-se a:</span><span class="sxs-lookup"><span data-stu-id="e65c3-105">Applies To:</span></span>
>  - <span data-ttu-id="e65c3-106">Projetos do MSBuild personalizados executados em qualquer versão do TFS</span><span class="sxs-lookup"><span data-stu-id="e65c3-106">Custom MSBuild projects running on any version of TFS</span></span>
>  - <span data-ttu-id="e65c3-107">Team Foundation Server 2012 ou superior</span><span class="sxs-lookup"><span data-stu-id="e65c3-107">Team Foundation Server 2012 or earlier</span></span>
>  - <span data-ttu-id="e65c3-108">Modelos do Team Foundation Build Process personalizados migrados para o TFS 2013 ou posterior</span><span class="sxs-lookup"><span data-stu-id="e65c3-108">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
>  - <span data-ttu-id="e65c3-109">Compilar modelos de processo com a funcionalidade de restauração do Nuget removida</span><span class="sxs-lookup"><span data-stu-id="e65c3-109">Build Process Templates With Nuget Restore functionality removed</span></span>
>
> <span data-ttu-id="e65c3-110">Se você estiver usando o Visual Studio Team Services ou o Team Foundation Server 2013 local com seus modelos de processo de build, a Restauração de Pacote Automática ocorrerá como parte do processo de build.</span><span class="sxs-lookup"><span data-stu-id="e65c3-110">If you're using Visual Studio Team Services or on-premises Team Foundation Server 2013 with its build process templates, Automatic Package Restore happens as part of the build process.</span></span>

<span data-ttu-id="e65c3-111">Esta seção fornecerá instruções passo a passo detalhadas sobre como restaurar os pacotes como parte do [Team Services Build](/vsts/build-release/index), tanto para Git como para o Controle de Versão do Team Services.</span><span class="sxs-lookup"><span data-stu-id="e65c3-111">This section will provide a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="e65c3-112">Embora este passo a passo seja específico para o cenário que usa os Visual Studio Team Services, os conceitos também se aplicam a outros controle de versão e sistemas de build.</span><span class="sxs-lookup"><span data-stu-id="e65c3-112">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="e65c3-113">A abordagem geral</span><span class="sxs-lookup"><span data-stu-id="e65c3-113">The general approach</span></span>

<span data-ttu-id="e65c3-114">Uma vantagem de usar o NuGet é que você pode usá-lo para evitar fazer check in de binários para seu sistema de controle de versão.</span><span class="sxs-lookup"><span data-stu-id="e65c3-114">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="e65c3-115">Isso é especialmente interessante se você estiver usando um sistema de [controle de versão distribuída](http://en.wikipedia.org/wiki/Distributed_revision_control) como git porque os desenvolvedores precisam clonar o repositório inteiro, incluindo o histórico completo, para começar a trabalhar localmente.</span><span class="sxs-lookup"><span data-stu-id="e65c3-115">This is especially interesting if you are using a [distributed version control](http://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="e65c3-116">Fazer check-in de binários pode causar sobrecarga significativa no repositório, visto que arquivos binários normalmente são armazenados sem compactação delta.</span><span class="sxs-lookup"><span data-stu-id="e65c3-116">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="e65c3-117">O NuGet tem sido compatível com a [restauração de pacotes](../consume-packages/package-restore.md) como parte do build há bastante tempo.</span><span class="sxs-lookup"><span data-stu-id="e65c3-117">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="e65c3-118">A implementação anterior tinha um problema de ovo e a galinha para os pacotes que desejam estender o processo de build porque os pacotes restaurados do NuGet durante a compilação do projeto.</span><span class="sxs-lookup"><span data-stu-id="e65c3-118">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="e65c3-119">No entanto, o MSBuild não permite estender o build durante o build; poderíamos argumentar que isso é um problema no MSBuild, mas eu diria que se trata de um problema inerente.</span><span class="sxs-lookup"><span data-stu-id="e65c3-119">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="e65c3-120">Dependendo de qual aspecto você precisa estender, pode ser muito tarde registrar no momento em que o pacote é restaurado.</span><span class="sxs-lookup"><span data-stu-id="e65c3-120">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="e65c3-121">A solução para esse problema é verificar se os pacotes foram restaurados como a primeira etapa no processo de build.</span><span class="sxs-lookup"><span data-stu-id="e65c3-121">The cure to this problem is making sure that packages are restored as the first step in the build process.</span></span> <span data-ttu-id="e65c3-122">O NuGet 2.7 ou superior torna isso fácil por meio de uma linha de comando simplificada:</span><span class="sxs-lookup"><span data-stu-id="e65c3-122">NuGet 2.7+ makes this easy via a simplified command line:</span></span>

```
nuget restore path\to\solution.sln
```

<span data-ttu-id="e65c3-123">Quando o processo de build restaura os pacotes antes de compilar o código, você não precisa fazer check-in de arquivos `.targets`</span><span class="sxs-lookup"><span data-stu-id="e65c3-123">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="e65c3-124">Os pacotes devem ser criados para permitir o carregamento no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e65c3-124">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="e65c3-125">Caso contrário, ainda pode ser recomendável fazer check-in em arquivos `.targets` para que outros desenvolvedores possam simplesmente abrir a solução sem a necessidade de restaurar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="e65c3-125">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="e65c3-126">O seguinte projeto de demonstração mostra como configurar o build de forma que as pastas `packages` os arquivos `.targets` não precisam passar por check-in.</span><span class="sxs-lookup"><span data-stu-id="e65c3-126">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="e65c3-127">Ele também mostra como configurar um build automatizado no Team Foundation Service para este projeto de exemplo.</span><span class="sxs-lookup"><span data-stu-id="e65c3-127">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="e65c3-128">Estrutura do repositório</span><span class="sxs-lookup"><span data-stu-id="e65c3-128">Repository structure</span></span>

<span data-ttu-id="e65c3-129">Nosso projeto de demonstração é uma ferramenta de linha de comando simples que usa o argumento de linha de comando para consultar o Bing.</span><span class="sxs-lookup"><span data-stu-id="e65c3-129">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="e65c3-130">Ele se destina ao .NET Framework 4 e usa muitos dos [pacotes BCL](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async) e [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span><span class="sxs-lookup"><span data-stu-id="e65c3-130">It targets the .NET Framework 4 and uses many of the [BCL packages](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="e65c3-131">A estrutura do repositório será semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="e65c3-131">The structure of the repository looks as follows:</span></span>

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

<span data-ttu-id="e65c3-132">Você pode ver que não fizemos check-in na pasta `packages` nem qualquer arquivo `.targets`.</span><span class="sxs-lookup"><span data-stu-id="e65c3-132">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="e65c3-133">No entanto, fizemos check-in no `nuget.exe`, pois ele é necessário durante o build.</span><span class="sxs-lookup"><span data-stu-id="e65c3-133">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="e65c3-134">Seguindo as convenções mais usadas, nós o colocamos em uma pasta `tools` compartilhada.</span><span class="sxs-lookup"><span data-stu-id="e65c3-134">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="e65c3-135">O código-fonte está na pasta `src`.</span><span class="sxs-lookup"><span data-stu-id="e65c3-135">The source code is under the `src` folder.</span></span> <span data-ttu-id="e65c3-136">Embora a nossa demonstração use apenas uma única solução, é possível imaginar facilmente que essa pasta contém mais de uma solução.</span><span class="sxs-lookup"><span data-stu-id="e65c3-136">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="e65c3-137">Ignorar arquivos</span><span class="sxs-lookup"><span data-stu-id="e65c3-137">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="e65c3-138">Atualmente, há um [bug conhecido no cliente do NuGet](https://nuget.codeplex.com/workitem/4072) que faz com que o cliente ainda adicione a pasta `packages` ao controle de versão.</span><span class="sxs-lookup"><span data-stu-id="e65c3-138">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="e65c3-139">Uma solução alternativa é desabilitar a integração de controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="e65c3-139">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="e65c3-140">Para fazer isso, você precisará de um arquivo `Nuget.Config ` na pasta `.nuget` é paralela à sua solução.</span><span class="sxs-lookup"><span data-stu-id="e65c3-140">In order to do that, you'll need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="e65c3-141">Se essa pasta ainda não existir, você precisará criá-la.</span><span class="sxs-lookup"><span data-stu-id="e65c3-141">If this folder doesn't exist yet, you'll need to create it.</span></span> <span data-ttu-id="e65c3-142">No [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), adicione o conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="e65c3-142">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```


<span data-ttu-id="e65c3-143">Para se comunicar com o controle de versão que nós não temos intenção de fazer check-in nas pastas **pacotes**, também adicionamos ignorar arquivos ao git (`.gitignore`) e ao controle de versão do TF (`.tfignore`).</span><span class="sxs-lookup"><span data-stu-id="e65c3-143">In order to communicate to the version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="e65c3-144">Esses arquivos descrevem padrões dos arquivos para os quais você não deseja fazer check-in.</span><span class="sxs-lookup"><span data-stu-id="e65c3-144">These files describes patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="e65c3-145">O arquivo `.gitignore` se parece com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e65c3-145">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages

<span data-ttu-id="e65c3-146">O arquivo `.gitignore` é [muito poderoso](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="e65c3-146">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="e65c3-147">Por exemplo, se você geralmente não quiser fazer check-in do conteúdo da pasta `packages`, mas deseja prosseguir com a orientação anterior de fazer check-in nos arquivos `.targets`, você poderia ter a seguinte regra em vez disso:</span><span class="sxs-lookup"><span data-stu-id="e65c3-147">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="e65c3-148">Isso excluirá todas as pastas `packages`, mas incluirá novamente todos os arquivos `.targets` contidos.</span><span class="sxs-lookup"><span data-stu-id="e65c3-148">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="e65c3-149">Aliás, você pode encontrar um modelo para arquivos `.gitignore` especificamente projetado para as necessidades de desenvolvedores do Visual Studio [aqui](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="e65c3-149">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="e65c3-150">O controle de versão do TF dá suporte a um mecanismo muito semelhante por meio do arquivo [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control).</span><span class="sxs-lookup"><span data-stu-id="e65c3-150">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="e65c3-151">A sintaxe é praticamente a mesma:</span><span class="sxs-lookup"><span data-stu-id="e65c3-151">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages

## <a name="buildproj"></a><span data-ttu-id="e65c3-152">build.proj</span><span class="sxs-lookup"><span data-stu-id="e65c3-152">build.proj</span></span>

<span data-ttu-id="e65c3-153">Para nossa demonstração, manteremos o processo de build bastante simples.</span><span class="sxs-lookup"><span data-stu-id="e65c3-153">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="e65c3-154">Vamos criar um projeto do MSBuild que cria todas as soluções enquanto verifica se os pacotes são restaurados antes de compilar as soluções.</span><span class="sxs-lookup"><span data-stu-id="e65c3-154">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="e65c3-155">Este projeto terá os três destinos convencionais `Clean`, `Build` e `Rebuild`, bem como um novo destino `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="e65c3-155">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="e65c3-156">Os destinos de `Build` e `Rebuild` dependem do `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="e65c3-156">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="e65c3-157">Isso garante que você pode tanto executar `Build` e `Rebuild` quanto contar com os pacotes que estão sendo restaurados.</span><span class="sxs-lookup"><span data-stu-id="e65c3-157">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="e65c3-158">`Clean`, `Build` e `Rebuild` invocam o destino do MSBuild correspondente em todos os arquivos de solução.</span><span class="sxs-lookup"><span data-stu-id="e65c3-158">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="e65c3-159">O destino `RestorePackages` invoca `nuget.exe` para cada arquivo de solução.</span><span class="sxs-lookup"><span data-stu-id="e65c3-159">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="e65c3-160">Isso é feito usando a [funcionalidade de envio em lotes do MSBuild](/visualstudio/msbuild/msbuild-batching).</span><span class="sxs-lookup"><span data-stu-id="e65c3-160">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="e65c3-161">O resultado se parece com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e65c3-161">The result looks as follows:</span></span>

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

## <a name="configuring-team-build"></a><span data-ttu-id="e65c3-162">Configurar o Team Build</span><span class="sxs-lookup"><span data-stu-id="e65c3-162">Configuring Team Build</span></span>

<span data-ttu-id="e65c3-163">O Team Build oferece vários modelos de processo.</span><span class="sxs-lookup"><span data-stu-id="e65c3-163">Team Build offers various process templates.</span></span> <span data-ttu-id="e65c3-164">Para esta demonstração, estamos usando o Team Foundation Service.</span><span class="sxs-lookup"><span data-stu-id="e65c3-164">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="e65c3-165">Contudo, instalações locais do TFS serão muito semelhantes.</span><span class="sxs-lookup"><span data-stu-id="e65c3-165">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="e65c3-166">O Git e o Controle de Versão do TF têm diferentes modelos de Team Build, por isso as etapas a seguir variarão dependendo de qual sistema de controle de versão você está usando.</span><span class="sxs-lookup"><span data-stu-id="e65c3-166">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="e65c3-167">Em ambos os casos, tudo o que você precisa é selecionar o build.proj como o projeto que você deseja compilar.</span><span class="sxs-lookup"><span data-stu-id="e65c3-167">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="e65c3-168">Primeiro, vamos analisar o modelo de processo para o git.</span><span class="sxs-lookup"><span data-stu-id="e65c3-168">First, let's look at the process template for git.</span></span> <span data-ttu-id="e65c3-169">No modelo baseado em git, o build é selecionado por meio da propriedade `Solution to build`:</span><span class="sxs-lookup"><span data-stu-id="e65c3-169">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Processo de build para git](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="e65c3-171">Observe que essa propriedade é um local em seu repositório.</span><span class="sxs-lookup"><span data-stu-id="e65c3-171">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="e65c3-172">Como nosso `build.proj` está na raiz, simplesmente usamos `build.proj`.</span><span class="sxs-lookup"><span data-stu-id="e65c3-172">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="e65c3-173">Se você colocar o arquivo de build em uma pasta chamada `tools`, o valor será `tools\build.proj`.</span><span class="sxs-lookup"><span data-stu-id="e65c3-173">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="e65c3-174">No modelo de controle de versão do TF, o projeto é selecionado por meio da propriedade `Projects`:</span><span class="sxs-lookup"><span data-stu-id="e65c3-174">In the TF version control template the project is selected via the property `Projects`:</span></span>

![Processo de build para TFVC](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="e65c3-176">Em contraste com modelo baseado em git, o controle de versão do TF é compatível com seletores (o botão do lado direito com três pontos).</span><span class="sxs-lookup"><span data-stu-id="e65c3-176">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="e65c3-177">Para evitar erros de digitação, sugerimos usá-los para selecionar o projeto.</span><span class="sxs-lookup"><span data-stu-id="e65c3-177">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>