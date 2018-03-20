---
title: Como criar um pacote do NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 456797cb-e3e4-4b88-9b01-8b5153cee802
description: "Um guia detalhado para o processo de design e criação de um pacote do NuGet, incluindo os principais pontos de decisão como arquivos e controle de versão."
keywords: "Criação de pacotes do NuGet, criando um pacote, manifesto de nuspec, convenções de pacote do NuGet, versão do pacote do NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 613e3eb9d08a0da96340f32b13c486508fa32439
ms.sourcegitcommit: df21fe770900644d476d51622a999597a6f20ef8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/12/2018
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="f22e4-104">Criando pacotes do NuGet</span><span class="sxs-lookup"><span data-stu-id="f22e4-104">Creating NuGet packages</span></span>

<span data-ttu-id="f22e4-105">Independentemente do que o pacote ou o código que ele contém fazem, use `nuget.exe` para empacotar essa funcionalidade em um componente que pode ser compartilhado e usado por uma infinidade de outros desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="f22e4-105">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="f22e4-106">Para instalar o `nuget.exe`, consulte [Instalar a CLI do NuGet](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="f22e4-106">To install `nuget.exe`, see [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span> <span data-ttu-id="f22e4-107">Observe que o Visual Studio não inclui automaticamente `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-107">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="f22e4-108">Tecnicamente, um pacote do NuGet é apenas um arquivo ZIP que foi renomeado com a extensão `.nupkg` e cujo conteúdo corresponde a certas convenções.</span><span class="sxs-lookup"><span data-stu-id="f22e4-108">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="f22e4-109">Este tópico descreve o processo detalhado da criação de um pacote que cumpre as convenções.</span><span class="sxs-lookup"><span data-stu-id="f22e4-109">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="f22e4-110">Para ver uma explicação passo a passo concentrada, veja [Início rápido: criar e publicar um pacote](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="f22e4-110">For a focused walkthrough, refer to [Quickstart: create and publish a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="f22e4-111">O empacotamento começa com o código compilado (assemblies), símbolos e/ou outros arquivos que você deseja entregar como um pacote (consulte [Visão geral e o fluxo de trabalho](overview-and-workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="f22e4-111">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="f22e4-112">Esse processo é independente da compilação ou da geração dos arquivos que entram no pacote, embora você possa obter informações em um arquivo de projeto para manter os assemblies e pacotes compilados em sincronia.</span><span class="sxs-lookup"><span data-stu-id="f22e4-112">This process is independent from compiling or otherwise generating the files that go into the package, although you can use draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Note]
> <span data-ttu-id="f22e4-113">Este tópico se aplica aos tipos de projeto diferente de projetos .NET Core usando o Visual Studio 2017 e o NuGet 4.0.</span><span class="sxs-lookup"><span data-stu-id="f22e4-113">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="f22e4-114">Nesses projetos .NET Core, o NuGet usa as informações do arquivo do projeto diretamente.</span><span class="sxs-lookup"><span data-stu-id="f22e4-114">In those .NET Core projects, NuGet uses information in the project file directly.</span></span> <span data-ttu-id="f22e4-115">Para obter detalhes, consulte [Criar pacotes do .NET Standard com o Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) e [Empacotamento e restauração do NuGet como destinos do MSBuild](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="f22e4-115">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="f22e4-116">Decidir quais assemblies são empacotados</span><span class="sxs-lookup"><span data-stu-id="f22e4-116">Deciding which assemblies to package</span></span>

<span data-ttu-id="f22e4-117">Mais pacotes para fins gerais contêm um ou mais assemblies que outros desenvolvedores podem usar em seus próprios projetos.</span><span class="sxs-lookup"><span data-stu-id="f22e4-117">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="f22e4-118">Em geral, é recomendável ter um assembly por pacote do NuGet, desde que cada assembly seja útil independentemente.</span><span class="sxs-lookup"><span data-stu-id="f22e4-118">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="f22e4-119">Por exemplo, se você tiver um `Utilities.dll` que depende de `Parser.dll` e `Parser.dll` é útil por conta própria, crie um pacote para cada um.</span><span class="sxs-lookup"><span data-stu-id="f22e4-119">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="f22e4-120">Isso permite aos desenvolvedores usar `Parser.dll` independentemente de `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-120">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="f22e4-121">Se sua biblioteca é composta por vários assemblies que não são úteis independentemente, não há problema em combiná-los em um pacote.</span><span class="sxs-lookup"><span data-stu-id="f22e4-121">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="f22e4-122">Usando o exemplo anterior, se `Parser.dll` contém código que é usado apenas por `Utilities.dll`, não há problema em manter `Parser.dll` no mesmo pacote.</span><span class="sxs-lookup"><span data-stu-id="f22e4-122">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="f22e4-123">Da mesma forma, se `Utilities.dll` depende de `Utilities.resources.dll`, em que novamente o último não é útil por conta própria, coloque ambos no mesmo pacote.</span><span class="sxs-lookup"><span data-stu-id="f22e4-123">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="f22e4-124">Os recursos são, na verdade, um caso especial.</span><span class="sxs-lookup"><span data-stu-id="f22e4-124">Resources are, in fact, a special case.</span></span> <span data-ttu-id="f22e4-125">Quando um pacote é instalado em um projeto, o NuGet adiciona automaticamente as referências de assembly às DLLs do pacote, *excluindo* aquelas que são nomeados `.resources.dll` porque são considerados assemblies satélites (consulte [Criando pacotes localizados](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="f22e4-125">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="f22e4-126">Por esse motivo, evite usar `.resources.dll` para arquivos que contêm código de pacote essencial.</span><span class="sxs-lookup"><span data-stu-id="f22e4-126">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="f22e4-127">Se sua biblioteca contém assemblies de interoperabilidade COM, siga as diretrizes adicionais em [Criar pacotes com assemblies de interoperabilidade COM](#authoring-packages-with-com-interop-assemblies).</span><span class="sxs-lookup"><span data-stu-id="f22e4-127">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="f22e4-128">A função e a estrutura do arquivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="f22e4-128">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="f22e4-129">Depois que você sabe quais arquivos deseja empacotar, a próxima etapa é criar um manifesto de pacote em um arquivo XML `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-129">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="f22e4-130">O manifesto:</span><span class="sxs-lookup"><span data-stu-id="f22e4-130">The manifest:</span></span>

1. <span data-ttu-id="f22e4-131">Descreve o conteúdo do pacote e é incluído nele.</span><span class="sxs-lookup"><span data-stu-id="f22e4-131">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="f22e4-132">Controla a criação do pacote e instrui o NuGet sobre como instalá-lo em um projeto.</span><span class="sxs-lookup"><span data-stu-id="f22e4-132">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="f22e4-133">Por exemplo, o manifesto identifica outras dependências de pacote, de modo que o NuGet também pode instalar essas dependências quando o pacote principal é instalado.</span><span class="sxs-lookup"><span data-stu-id="f22e4-133">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="f22e4-134">Contém propriedades obrigatórias e opcionais, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="f22e4-134">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="f22e4-135">Para obter detalhes exatos, incluindo outras propriedades não mencionadas aqui, consulte a [Referência de .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="f22e4-135">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="f22e4-136">Propriedades necessárias:</span><span class="sxs-lookup"><span data-stu-id="f22e4-136">Required properties:</span></span>

- <span data-ttu-id="f22e4-137">O identificador de pacotes, que deve ser exclusivo entre a galeria que hospeda o pacote.</span><span class="sxs-lookup"><span data-stu-id="f22e4-137">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="f22e4-138">Um número de versão específico na forma *Principal.Secundário.Patch[-Suffix]* em que *-Suffix* identifica [versões de pré-lançamento](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="f22e4-138">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="f22e4-139">O título do pacote como ele deve aparecer no host (como nuget.org)</span><span class="sxs-lookup"><span data-stu-id="f22e4-139">The package title as it should appears on the host (like nuget.org)</span></span>
- <span data-ttu-id="f22e4-140">Informações de autor e proprietário.</span><span class="sxs-lookup"><span data-stu-id="f22e4-140">Author and owner information.</span></span>
- <span data-ttu-id="f22e4-141">Uma descrição longa do pacote.</span><span class="sxs-lookup"><span data-stu-id="f22e4-141">A long description of the package.</span></span>

<span data-ttu-id="f22e4-142">Propriedades opcionais comuns:</span><span class="sxs-lookup"><span data-stu-id="f22e4-142">Common optional properties:</span></span>

- <span data-ttu-id="f22e4-143">Notas de Versão</span><span class="sxs-lookup"><span data-stu-id="f22e4-143">Release notes</span></span>
- <span data-ttu-id="f22e4-144">Informações de direitos autorais</span><span class="sxs-lookup"><span data-stu-id="f22e4-144">Copyright information</span></span>
- <span data-ttu-id="f22e4-145">Uma breve descrição para a [Interface do usuário do Gerenciador de Pacotes no Visual Studio](../tools/package-manager-ui.md)</span><span class="sxs-lookup"><span data-stu-id="f22e4-145">A short description for the [Package Manager UI in Visual Studio](../tools/package-manager-ui.md)</span></span>
- <span data-ttu-id="f22e4-146">Uma identificação de localidade</span><span class="sxs-lookup"><span data-stu-id="f22e4-146">A locale ID</span></span>
- <span data-ttu-id="f22e4-147">Página inicial e URLs de licença</span><span class="sxs-lookup"><span data-stu-id="f22e4-147">Home page and license URLs</span></span>
- <span data-ttu-id="f22e4-148">Uma URL de ícone</span><span class="sxs-lookup"><span data-stu-id="f22e4-148">An icon URL</span></span>
- <span data-ttu-id="f22e4-149">Listas de dependências e referências</span><span class="sxs-lookup"><span data-stu-id="f22e4-149">Lists of dependencies and references</span></span>
- <span data-ttu-id="f22e4-150">Marcas que auxiliam em pesquisas de galeria</span><span class="sxs-lookup"><span data-stu-id="f22e4-150">Tags that assist in gallery searches</span></span>

<span data-ttu-id="f22e4-151">A seguir está um arquivo `.nuspec` típico (mas fictício), com os comentários que descrevem as propriedades:</span><span class="sxs-lookup"><span data-stu-id="f22e4-151">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- The identifier that must be unique within the hosting gallery -->
    <id>Contoso.Utility.UsefulStuff</id>

    <!-- The package version number that is used when resolving dependencies -->
    <version>1.8.3-beta</version>

    <!-- Authors contain text that appears directly on the gallery -->
    <authors>Dejana Tesic, Rajeev Dey</authors>

    <!-- Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  -->
    <owners>dejanatc, rjdey</owners>

    <!-- License and project URLs provide links for the gallery -->
    <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
    <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

    <!-- The icon is used in Visual Studio's package manager UI -->
    <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

    <!-- If true, this value prompts the user to accept the license when
            installing the package. -->
    <requireLicenseAcceptance>false</requireLicenseAcceptance>

    <!-- Any details about this particular release -->
    <releaseNotes>Bug fixes and performance improvements</releaseNotes>

    <!-- The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. -->
    <description>Core utility functions for web applications</description>

    <!-- Copyright information -->
    <copyright>Copyright ©2016 Contoso Corporation</copyright>

    <!-- Tags appear in the gallery and can be used for tag searches -->
    <tags>web utility http json url parsing</tags>

    <!-- Dependencies are automatically installed when the package is installed -->
    <dependencies>
        <dependency id="Newtonsoft.Json" version="9.0" />
    </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

<span data-ttu-id="f22e4-152">Para obter detalhes sobre como declarar dependências e especificar os números de versão, consulte [Controle de versão do pacote](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="f22e4-152">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="f22e4-153">Também é possível extrair ativos das dependências diretamente no pacote usando o os atributos `include` e `exclude` no elemento `dependency`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-153">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="f22e4-154">Consulte [Referência de .nuspec – Dependências](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="f22e4-154">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="f22e4-155">Como o manifesto está incluído no pacote criado com base nele, encontre vários exemplos adicionais examinando os pacotes existentes.</span><span class="sxs-lookup"><span data-stu-id="f22e4-155">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="f22e4-156">Uma boa fonte é o cache do pacotes global em seu computador, o local do qual será retornado pelo comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f22e4-156">A good source is the global package cache on your machine, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="f22e4-157">Acesse qualquer pasta *package\version*, copie o arquivo `.nupkg` para um arquivo `.zip` e depois abra esse arquivo `.zip` e examine o `.nuspec` dentro dele.</span><span class="sxs-lookup"><span data-stu-id="f22e4-157">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="f22e4-158">Ao criar um `.nuspec` de um projeto do Visual Studio, o manifesto contém tokens que são substituídos com informações do projeto quando o pacote é compilado.</span><span class="sxs-lookup"><span data-stu-id="f22e4-158">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="f22e4-159">Consulte [Criando o .nuspec de um projeto do Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="f22e4-159">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="f22e4-160">Criando o arquivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="f22e4-160">Creating the .nuspec file</span></span>

<span data-ttu-id="f22e4-161">Criar um manifesto completo normalmente começa com um arquivo `.nuspec` básico gerado usando um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="f22e4-161">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="f22e4-162">Um diretório de trabalho baseado em convenção</span><span class="sxs-lookup"><span data-stu-id="f22e4-162">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="f22e4-163">Uma DLL de assembly</span><span class="sxs-lookup"><span data-stu-id="f22e4-163">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="f22e4-164">Um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f22e4-164">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="f22e4-165">Novo arquivo com valores padrão</span><span class="sxs-lookup"><span data-stu-id="f22e4-165">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="f22e4-166">Em seguida, edite o arquivo manualmente para que ele descreva o conteúdo exato que você deseja no pacote final.</span><span class="sxs-lookup"><span data-stu-id="f22e4-166">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="f22e4-167">Arquivos `.nuspec` gerados contêm espaços reservados que precisam ser modificados antes de criar o pacote com o comando `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-167">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="f22e4-168">Esse comando falhará se o `.nuspec` contiver algum espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="f22e4-168">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="f22e4-169">De um diretório de trabalho baseado em convenção</span><span class="sxs-lookup"><span data-stu-id="f22e4-169">From a convention-based working directory</span></span>

<span data-ttu-id="f22e4-170">Como um pacote do NuGet é apenas um arquivo ZIP que foi renomeado com a extensão `.nupkg`, geralmente é mais fácil criar a estrutura de pastas que você deseja no sistema de arquivos para depois criar o arquivo `.nuspec` diretamente dessa estrutura.</span><span class="sxs-lookup"><span data-stu-id="f22e4-170">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, its often easiest to create the folder structure you want on the file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="f22e4-171">O comando `nuget pack` adicionará automaticamente todos os arquivos nessa estrutura de pastas (excluindo as pastas que começam com `.`, permitindo que você mantenha arquivos particulares na mesma estrutura).</span><span class="sxs-lookup"><span data-stu-id="f22e4-171">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you keep private files in the same structure).</span></span>

<span data-ttu-id="f22e4-172">A vantagem dessa abordagem é que você não precisa especificar no manifesto quais arquivos você deseja incluir no pacote (conforme explicado mais adiante neste tópico).</span><span class="sxs-lookup"><span data-stu-id="f22e4-172">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="f22e4-173">Basta fazer com que o processo de build produza a estrutura de pasta exata que vai para o pacote e incluir facilmente outros arquivos que não podem fazer parte de um projeto, caso contrário:</span><span class="sxs-lookup"><span data-stu-id="f22e4-173">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="f22e4-174">O conteúdo e o código-fonte que devem ser inseridos no projeto de destino.</span><span class="sxs-lookup"><span data-stu-id="f22e4-174">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="f22e4-175">Scripts do PowerShell (pacotes usados no NuGet 2.x podem incluir scripts de instalação, o que não é compatível com o NuGet 3.x e posterior).</span><span class="sxs-lookup"><span data-stu-id="f22e4-175">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="f22e4-176">Transformações em configuração existentes e arquivos de código-fonte em um projeto.</span><span class="sxs-lookup"><span data-stu-id="f22e4-176">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="f22e4-177">As convenções de pasta são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="f22e4-177">The folder conventions are as follows:</span></span>

| <span data-ttu-id="f22e4-178">Pasta</span><span class="sxs-lookup"><span data-stu-id="f22e4-178">Folder</span></span> | <span data-ttu-id="f22e4-179">Descrição</span><span class="sxs-lookup"><span data-stu-id="f22e4-179">Description</span></span> | <span data-ttu-id="f22e4-180">Ação após a instalação do pacote</span><span class="sxs-lookup"><span data-stu-id="f22e4-180">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f22e4-181">(raiz)</span><span class="sxs-lookup"><span data-stu-id="f22e4-181">(root)</span></span> | <span data-ttu-id="f22e4-182">Local para leiame.txt</span><span class="sxs-lookup"><span data-stu-id="f22e4-182">Location for readme.txt</span></span> | <span data-ttu-id="f22e4-183">O Visual Studio exibe um arquivo Leiame.txt na raiz do pacote quando este é instalado.</span><span class="sxs-lookup"><span data-stu-id="f22e4-183">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="f22e4-184">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="f22e4-184">lib/{tfm}</span></span> | <span data-ttu-id="f22e4-185">Arquivos de assembly (`.dll`), documentação (`.xml`) e símbolo (`.pdb`) para TFM (Moniker de Estrutura de Destino)</span><span class="sxs-lookup"><span data-stu-id="f22e4-185">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="f22e4-186">Assemblies são adicionados como referências; `.xml` e `.pdb` são copiados para as pastas do projeto.</span><span class="sxs-lookup"><span data-stu-id="f22e4-186">Assemblies are added as references; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="f22e4-187">Consulte [Suporte a várias estruturas de destino](supporting-multiple-target-frameworks.md) para ver a criação de subpastas específicas de destino da estrutura.</span><span class="sxs-lookup"><span data-stu-id="f22e4-187">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="f22e4-188">runtimes</span><span class="sxs-lookup"><span data-stu-id="f22e4-188">runtimes</span></span> | <span data-ttu-id="f22e4-189">Arquivos de assembly específico de arquitetura (`.dll`), símbolo (`.pdb`) e recurso nativo (`.pri`)</span><span class="sxs-lookup"><span data-stu-id="f22e4-189">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="f22e4-190">Assemblies são adicionados como referências; outros arquivos são copiados para as pastas do projeto.</span><span class="sxs-lookup"><span data-stu-id="f22e4-190">Assemblies are added as references; other files are copied into project folders.</span></span> <span data-ttu-id="f22e4-191">Consulte [Suporte a várias estruturas de destino](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="f22e4-191">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="f22e4-192">conteúdo</span><span class="sxs-lookup"><span data-stu-id="f22e4-192">content</span></span> | <span data-ttu-id="f22e4-193">Arquivos arbitrários</span><span class="sxs-lookup"><span data-stu-id="f22e4-193">Arbitrary files</span></span> | <span data-ttu-id="f22e4-194">O conteúdo é copiado para a raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="f22e4-194">Contents are copied to the project root.</span></span> <span data-ttu-id="f22e4-195">Pense na pasta **content** como a raiz do aplicativo de destino que, enfim, consome o pacote.</span><span class="sxs-lookup"><span data-stu-id="f22e4-195">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="f22e4-196">Para fazer o pacote adicionar uma imagem à pasta */imagens* do aplicativo, coloque-o na pasta *content/images* do pacote.</span><span class="sxs-lookup"><span data-stu-id="f22e4-196">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="f22e4-197">build</span><span class="sxs-lookup"><span data-stu-id="f22e4-197">build</span></span> | <span data-ttu-id="f22e4-198">Arquivos `.targets` e `.props` do MSBuild</span><span class="sxs-lookup"><span data-stu-id="f22e4-198">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="f22e4-199">Inserido automaticamente no arquivo de projeto ou em `project.lock.json` (NuGet 3.x+).</span><span class="sxs-lookup"><span data-stu-id="f22e4-199">Automatically inserted into the project file or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="f22e4-200">ferramentas</span><span class="sxs-lookup"><span data-stu-id="f22e4-200">tools</span></span> | <span data-ttu-id="f22e4-201">Scripts e programas do Powershell acessíveis do Console do Gerenciador de Pacotes</span><span class="sxs-lookup"><span data-stu-id="f22e4-201">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="f22e4-202">A pasta `tools` é adicionada à variável de ambiente `PATH` somente para o Console do Gerenciador de Pacotes (especificamente, *não* para o `PATH` conforme definido para MSBuild ao criar o projeto).</span><span class="sxs-lookup"><span data-stu-id="f22e4-202">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="f22e4-203">Como a estrutura de pastas pode conter qualquer número de assemblies para uma infinidade de estruturas de destino, esse método é necessário ao criar pacotes compatíveis com várias estruturas</span><span class="sxs-lookup"><span data-stu-id="f22e4-203">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks</span></span> 

<span data-ttu-id="f22e4-204">Em qualquer caso, uma vez que a estrutura de pastas esteja em vigor, execute o seguinte comando nessa pasta para criar o arquivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="f22e4-204">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="f22e4-205">Novamente, o `.nuspec` gerado não contém nenhuma referência explícita a arquivos na estrutura de pasta.</span><span class="sxs-lookup"><span data-stu-id="f22e4-205">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="f22e4-206">O NuGet inclui automaticamente todos os arquivos quando o pacote é criado.</span><span class="sxs-lookup"><span data-stu-id="f22e4-206">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="f22e4-207">No entanto, você ainda precisa editar os valores de espaço reservado em outras partes do manifesto.</span><span class="sxs-lookup"><span data-stu-id="f22e4-207">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="f22e4-208">De uma DLL de assembly</span><span class="sxs-lookup"><span data-stu-id="f22e4-208">From an assembly DLL</span></span>

<span data-ttu-id="f22e4-209">No caso mais simples de criar um pacote de um assembly, você pode gerar um arquivo `.nuspec` dos metadados no assembly usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="f22e4-209">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="f22e4-210">Usar este formulário substitui alguns espaços reservados no manifesto por valores específicos do assembly.</span><span class="sxs-lookup"><span data-stu-id="f22e4-210">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="f22e4-211">Por exemplo, a propriedade `<id>` é definida como o nome do assembly e `<version>` é definido como a versão do assembly.</span><span class="sxs-lookup"><span data-stu-id="f22e4-211">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="f22e4-212">Outras propriedades no manifesto, no entanto, não têm valores correspondentes no assembly e, portanto, ainda contêm espaços reservados.</span><span class="sxs-lookup"><span data-stu-id="f22e4-212">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="f22e4-213">De um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f22e4-213">From a Visual Studio project</span></span>

<span data-ttu-id="f22e4-214">É muito conveniente criar um `.nuspec` de um arquivo `.csproj` ou `.vbproj`, pois outros pacotes que foram instalados nesses projetos são referenciados automaticamente como dependências.</span><span class="sxs-lookup"><span data-stu-id="f22e4-214">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="f22e4-215">Simplesmente use o comando a seguir na mesma pasta que o arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="f22e4-215">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="f22e4-216">O arquivo `<project-name>.nuspec` resultante contém *tokens* que são substituídos no tempo de empacotamento pelos valores do projeto, incluindo referências aos outros pacotes que já foram instalados.</span><span class="sxs-lookup"><span data-stu-id="f22e4-216">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="f22e4-217">Um token é delimitado por símbolos `$` em ambos os lados da propriedade de projeto.</span><span class="sxs-lookup"><span data-stu-id="f22e4-217">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="f22e4-218">Por exemplo, o valor `<id>` em um manifesto gerado dessa forma normalmente aparece da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f22e4-218">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="f22e4-219">Esse token é substituído pelo valor `AssemblyName` do arquivo de projeto no tempo de empacotamento.</span><span class="sxs-lookup"><span data-stu-id="f22e4-219">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="f22e4-220">Para ver o mapeamento exato de valores de projeto para tokens `.nuspec`, consulte a [Referência de tokens de substituição](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="f22e4-220">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="f22e4-221">Tokens eliminam a necessidade de atualizar valores cruciais como o número de versão do `.nuspec` ao atualizar o projeto.</span><span class="sxs-lookup"><span data-stu-id="f22e4-221">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="f22e4-222">(Você sempre pode substituir os tokens por valores literais, se desejado.)</span><span class="sxs-lookup"><span data-stu-id="f22e4-222">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="f22e4-223">Observe que há várias opções de empacotamento adicional disponíveis ao trabalhar em um projeto do Visual Studio, conforme descrito em [Executando o pacote do nuget para gerar o arquivo .nupkg](#running-nuget-pack-to-generate-the-nupkg-file) posteriormente.</span><span class="sxs-lookup"><span data-stu-id="f22e4-223">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="f22e4-224">Pacotes de nível de solução</span><span class="sxs-lookup"><span data-stu-id="f22e4-224">Solution-level packages</span></span>

<span data-ttu-id="f22e4-225">*Somente NuGet 2.x. Não disponível no NuGet 3.0 ou superior.*</span><span class="sxs-lookup"><span data-stu-id="f22e4-225">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="f22e4-226">O NuGet 2.x é compatível com a noção de um pacote de nível de solução que instala ferramentas ou comandos adicionais para o Console do Gerenciador de Pacotes (o conteúdo da pasta `tools`), mas não adiciona referências, conteúdo ou personalizações de build aos projetos na solução.</span><span class="sxs-lookup"><span data-stu-id="f22e4-226">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="f22e4-227">Esses pacotes não contém arquivos em suas pastas `lib`, `content` ou `build` diretas e nenhuma de suas dependências têm arquivos em suas respectivas pastas `lib`, `content` ou `build`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-227">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="f22e4-228">O NuGet rastreia os pacotes instalados no nível da solução em um arquivo `packages.config` na pasta `.nuget`, em vez do arquivo `packages.config` do projeto.</span><span class="sxs-lookup"><span data-stu-id="f22e4-228">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="f22e4-229">Novo arquivo com valores padrão</span><span class="sxs-lookup"><span data-stu-id="f22e4-229">New file with default values</span></span>

<span data-ttu-id="f22e4-230">O comando a seguir cria um manifesto padrão com espaços reservados, que garante que você inicie com a estrutura de arquivos apropriada:</span><span class="sxs-lookup"><span data-stu-id="f22e4-230">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="f22e4-231">Se você omitir \<package-name\>, o arquivo resultante será `Package.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-231">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="f22e4-232">Se você fornecer um nome como `Contoso.Utility.UsefulStuff`, o arquivo será `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-232">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="f22e4-233">O `.nuspec` resultante contém espaços reservados para valores como o `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-233">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="f22e4-234">Edite o arquivo antes de usá-lo para criar o arquivo `.nupkg` final.</span><span class="sxs-lookup"><span data-stu-id="f22e4-234">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="f22e4-235">Escolhendo um identificador de pacote exclusivo e definindo o número de versão</span><span class="sxs-lookup"><span data-stu-id="f22e4-235">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="f22e4-236">O identificador de pacote (elemento `<id>`) e o número de versão (elemento `<version>`) são os dois valores mais importantes no manifesto, pois eles identificam exclusivamente o código exato que está contido no pacote.</span><span class="sxs-lookup"><span data-stu-id="f22e4-236">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="f22e4-237">**Práticas recomendadas para o identificador de pacote:**</span><span class="sxs-lookup"><span data-stu-id="f22e4-237">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="f22e4-238">**Exclusividade**: o identificador deve ser exclusivo no nuget.org ou na galeria que hospeda o pacote.</span><span class="sxs-lookup"><span data-stu-id="f22e4-238">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="f22e4-239">Antes de decidir sobre um identificador, pesquise a galeria aplicável para verificar se o nome já está em uso.</span><span class="sxs-lookup"><span data-stu-id="f22e4-239">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="f22e4-240">Para evitar conflitos, um bom padrão é usar o nome da sua empresa como a primeira parte do identificador, como `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-240">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="f22e4-241">**Nomes semelhantes a namespace**: siga um padrão semelhante aos namespaces no .NET, usando a notação de ponto em vez de hifens.</span><span class="sxs-lookup"><span data-stu-id="f22e4-241">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="f22e4-242">Por exemplo, use `Contoso.Utility.UsefulStuff` em vez de `Contoso-Utility-UsefulStuff` ou `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-242">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="f22e4-243">Também é útil para os consumidores quando o identificador de pacote corresponde os namespaces usados no código.</span><span class="sxs-lookup"><span data-stu-id="f22e4-243">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="f22e4-244">**Pacotes de exemplo**: se você gerar um pacote de código de exemplo que demonstra como usar outro pacote, anexe `.Sample` como um sufixo ao identificador, como em `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-244">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="f22e4-245">(O pacote de exemplo logicamente teria uma dependência do outro pacote.) Ao criar um pacote de exemplo, use o método de diretório de trabalho baseado em convenção descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f22e4-245">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="f22e4-246">Na pasta `content`, organize o código de exemplo em uma pasta chamada `\Samples\<identifier>` como no `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-246">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="f22e4-247">**Práticas recomendadas para a versão de pacote:**</span><span class="sxs-lookup"><span data-stu-id="f22e4-247">**Best practices for the package version:**</span></span>

- <span data-ttu-id="f22e4-248">Em geral, defina a versão do pacote para corresponder à biblioteca, embora isso não seja estritamente necessário.</span><span class="sxs-lookup"><span data-stu-id="f22e4-248">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="f22e4-249">Isso é muito simples quando você limita um pacote a um único assembly, conforme descrito anteriormente em [Decidir quais assemblies serão empacotados](#deciding-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="f22e4-249">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="f22e4-250">Em geral, lembre-se que o NuGet em si lida com versões do pacote ao resolver as dependências, não versões de assembly.</span><span class="sxs-lookup"><span data-stu-id="f22e4-250">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="f22e4-251">Ao usar um esquema de versão não padrão, considere as regras de controle de versão do NuGet, conforme explicado em [Controle de versão do pacote](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="f22e4-251">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="f22e4-252">A seguinte série de breves postagens no blog também é útil para entender o controle de versão:</span><span class="sxs-lookup"><span data-stu-id="f22e4-252">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="f22e4-253">Parte 1: assumindo o DLL Hell</span><span class="sxs-lookup"><span data-stu-id="f22e4-253">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="f22e4-254">Parte 2: o algoritmo principal</span><span class="sxs-lookup"><span data-stu-id="f22e4-254">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="f22e4-255">Parte 3: unificação por meio de redirecionamentos de associação</span><span class="sxs-lookup"><span data-stu-id="f22e4-255">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a><span data-ttu-id="f22e4-256">Definindo um tipo de pacote</span><span class="sxs-lookup"><span data-stu-id="f22e4-256">Setting a package type</span></span>

<span data-ttu-id="f22e4-257">Com o NuGet 3.5 ou superior, os pacotes podem ser marcados com um *tipo de pacote* específico para indicar o uso pretendido.</span><span class="sxs-lookup"><span data-stu-id="f22e4-257">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="f22e4-258">Pacotes não marcados com um tipo, incluindo todos os pacotes criados com versões anteriores do NuGet, usam o tipo `Dependency` como padrão.</span><span class="sxs-lookup"><span data-stu-id="f22e4-258">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="f22e4-259">Pacotes do tipo `Dependency` adicionam ativos de tempo de build ou de execução a bibliotecas e aplicativos e podem ser instalados em qualquer tipo de projeto (supondo que eles sejam compatíveis).</span><span class="sxs-lookup"><span data-stu-id="f22e4-259">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="f22e4-260">Pacotes do tipo `DotnetCliTool` são extensões para a [CLI do .NET](/dotnet/articles/core/tools/index) e são invocados na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="f22e4-260">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="f22e4-261">Esses pacotes podem ser instalados somente em projetos do .NET Core e não têm nenhum efeito sobre operações de restauração.</span><span class="sxs-lookup"><span data-stu-id="f22e4-261">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="f22e4-262">Mais detalhes sobre essas extensões por projeto estão disponíveis na documentação da [extensibilidade do .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).</span><span class="sxs-lookup"><span data-stu-id="f22e4-262">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="f22e4-263">Pacotes de tipo personalizado usam um identificador de tipo arbitrário que está em conformidade com as mesmas regras de formato que as IDs de pacote.</span><span class="sxs-lookup"><span data-stu-id="f22e4-263">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="f22e4-264">Qualquer tipo diferente de `Dependency` e `DotnetCliTool`, no entanto, não é reconhecido pelo Gerenciador de Pacotes do NuGet no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f22e4-264">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="f22e4-265">Os tipos de pacote são definidos no arquivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-265">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="f22e4-266">É melhor para compatibilidade com versões anteriores *não* definir explicitamente o tipo `Dependency` e, em vez disso, contar com o NuGet, supondo este tipo quando nenhum tipo é especificado.</span><span class="sxs-lookup"><span data-stu-id="f22e4-266">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="f22e4-267">`.nuspec`: indica o tipo de pacote em um nó `packageTypes\packageType` sob o elemento `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="f22e4-267">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="f22e4-268">Adicionar um Leiame e outros arquivos</span><span class="sxs-lookup"><span data-stu-id="f22e4-268">Adding a readme and other files</span></span>

<span data-ttu-id="f22e4-269">Para especificar diretamente os arquivos a serem incluídos no pacote, use o nó `<files>` no arquivo `.nuspec`, que *segue* a marca `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="f22e4-269">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
    <!-- Add a readme -->
    <file src="readme.txt" target="" />

    <!-- Add files from an arbitrary folder that's not necessarily in the project -->
    <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> <span data-ttu-id="f22e4-270">Ao usar a abordagem de diretório de trabalho baseado em convenção, você pode colocar o Leiame.txt na raiz do pacote e outros conteúdos na pasta `content`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-270">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="f22e4-271">Nenhum elemento `<file>` é necessário no manifesto.</span><span class="sxs-lookup"><span data-stu-id="f22e4-271">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="f22e4-272">Quando você inclui um arquivo chamado `readme.txt` na raiz do pacote, o Visual Studio exibe o conteúdo do arquivo como texto sem formatação imediatamente depois de instalar o pacote diretamente.</span><span class="sxs-lookup"><span data-stu-id="f22e4-272">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="f22e4-273">(Arquivos Leiame não são exibidos para pacotes instalados como dependências).</span><span class="sxs-lookup"><span data-stu-id="f22e4-273">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="f22e4-274">Por exemplo, mostramos aqui como o arquivo Leiame para o pacote HtmlAgilityPack é exibido:</span><span class="sxs-lookup"><span data-stu-id="f22e4-274">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![A exibição de um arquivo Leiame para um pacote do NuGet na instalação](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="f22e4-276">Se você incluir um nó `<files>` vazio no arquivo `.nuspec`, o NuGet não incluirá nenhum outro conteúdo no pacote que não seja o que está na pasta `lib`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-276">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="f22e4-277">Incluir objetos e destinos de MSBuild em um pacote</span><span class="sxs-lookup"><span data-stu-id="f22e4-277">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="f22e4-278">Em alguns casos, convém adicionar destinos ou propriedades de build personalizados a projetos que consomem o pacote, como a execução de uma ferramenta personalizada ou um processo durante o build.</span><span class="sxs-lookup"><span data-stu-id="f22e4-278">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="f22e4-279">Faça isso colocando arquivos no formato `<package_id>.targets` ou `<package_id>.props` (como `Contoso.Utility.UsefulStuff.targets`) dentro da pasta `\build` do projeto.</span><span class="sxs-lookup"><span data-stu-id="f22e4-279">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="f22e4-280">Arquivos na pasta `\build` raiz são considerados adequados para todas as estruturas de destino.</span><span class="sxs-lookup"><span data-stu-id="f22e4-280">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="f22e4-281">Para fornecer arquivos específicos de estrutura, primeiro coloque-os em subpastas apropriadas, como os seguintes:</span><span class="sxs-lookup"><span data-stu-id="f22e4-281">To provide framework-specific files, first place those within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="f22e4-282">Em seguida, no arquivo `.nuspec`, faça referência a esses arquivos no nó `<files>`:</span><span class="sxs-lookup"><span data-stu-id="f22e4-282">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
    <!-- Include everything in \build -->
    <file src="build\**" target="build" />

    <!-- Other files -->
    <!-- ... -->
    </files>
</package>
```

<span data-ttu-id="f22e4-283">Incluindo os arquivos de propriedades e de destinos do MSBuild em um pacote [introduzidos com o NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), portanto é recomendado adicionar o atributo `minClientVersion="2.5"` ao elemento `metadata` para indicar a versão mínima necessária do cliente NuGet para consumir o pacote.</span><span class="sxs-lookup"><span data-stu-id="f22e4-283">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="f22e4-284">Quando o NuGet instala um pacote com arquivos `\build`, ele adiciona elementos `<Import>` do MSBuild ao arquivo de projeto que aponta para os arquivos `.targets` e `.props`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-284">When NuGet installs a package with `\build` files, it adds an MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="f22e4-285">(`.props` é adicionado à parte superior do arquivo de projeto; `.targets` é adicionado à parte inferior.)</span><span class="sxs-lookup"><span data-stu-id="f22e4-285">(`.props` is added at the top of the project file; `.targets` is added at the bottom.)</span></span>

<span data-ttu-id="f22e4-286">Com o NuGet 3.x, os destinos não são adicionados ao projeto, mas são disponibilizados por meio do `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-286">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="f22e4-287">Criação de pacotes com assemblies de interoperabilidade COM</span><span class="sxs-lookup"><span data-stu-id="f22e4-287">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="f22e4-288">Pacotes que contêm assemblies de interoperabilidade COM devem incluir um [arquivo de destino](#including-msbuild-props-and-targets-in-a-package) apropriado para que os metadados `EmbedInteropTypes` corretos são adicionados a projetos usando o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="f22e4-288">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="f22e4-289">Por padrão, os metadados `EmbedInteropTypes` são sempre falsos para todos os assemblies quando PackageReference é usado, por isso o arquivo de destino adiciona tais metadados explicitamente.</span><span class="sxs-lookup"><span data-stu-id="f22e4-289">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="f22e4-290">Para evitar conflitos, o nome de destino deve ser exclusivo; o ideal é usar uma combinação de nome do pacote e o assembly que está sendo inserido, substituindo o `{InteropAssemblyName}` no exemplo a seguir por esse valor.</span><span class="sxs-lookup"><span data-stu-id="f22e4-290">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="f22e4-291">(Consulte também [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) para ver um exemplo.)</span><span class="sxs-lookup"><span data-stu-id="f22e4-291">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="EmbeddingAssemblyNameFromPackageId" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <PropertyGroup>
    <_InteropAssemblyFileName>{InteropAssemblyName}</_InteropAssemblyFileName>
  </PropertyGroup>
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '$(_InteropAssemblyFileName)' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="f22e4-292">Observe que ao usar o formato de referência `packages.config`, adicionar referências aos assemblies dos pacotes faz com que o NuGet e o Visual Studio verifiquem os assemblies de interoperabilidade COM e defina o `EmbedInteropTypes` como true no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="f22e4-292">Note that when using the `packages.config` reference format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="f22e4-293">Nesse caso, os destinos são substituídos.</span><span class="sxs-lookup"><span data-stu-id="f22e4-293">In this case the targets are overriden.</span></span>

<span data-ttu-id="f22e4-294">Além disso, por padrão, os [ativos de build não fluem transitivamente](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="f22e4-294">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="f22e4-295">Pacotes criados conforme descrito aqui funcionam de forma diferente quando passam por pull como uma dependência transitiva de uma referência de projeto a projeto.</span><span class="sxs-lookup"><span data-stu-id="f22e4-295">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="f22e4-296">O consumidor de pacotes pode permitir que eles fluam modificando o valor padrão de PrivateAssets para não incluir o build.</span><span class="sxs-lookup"><span data-stu-id="f22e4-296">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="f22e4-297">Executando o nuget pack para gerar o arquivo .nupkg</span><span class="sxs-lookup"><span data-stu-id="f22e4-297">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="f22e4-298">Ao usar um assembly ou o diretório de trabalho baseado em convenção, crie um pacote executando `nuget pack` com seu arquivo `.nuspec`, substituindo `<manifest-name>` pelo nome do seu arquivo específico:</span><span class="sxs-lookup"><span data-stu-id="f22e4-298">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<manifest-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="f22e4-299">Ao usar um projeto do Visual Studio, execute `nuget pack` com o arquivo de projeto, que carrega automaticamente o arquivo `.nuspec` do projeto e substitui todos os tokens dentro dele usando valores no arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="f22e4-299">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="f22e4-300">É necessário usar o arquivo de projeto diretamente para a substituição do token porque o projeto é a origem dos valores de token.</span><span class="sxs-lookup"><span data-stu-id="f22e4-300">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="f22e4-301">A substituição do token não ocorre se você usar `nuget pack` com um arquivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-301">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="f22e4-302">Em todos os casos, o `nuget pack` exclui pastas que começam com um ponto, como `.git` ou `.hg`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-302">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="f22e4-303">O NuGet indica se há erros no arquivo `.nuspec` que precisam de correção, como se esquecer de alterar os valores de espaço reservado no manifesto.</span><span class="sxs-lookup"><span data-stu-id="f22e4-303">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="f22e4-304">Depois que o `nuget pack` for bem-sucedido, você tem um arquivo `.nupkg` que pode ser publicado para uma galeria adequada conforme descrito em [Publicar um pacote](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="f22e4-304">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="f22e4-305">Uma maneira útil de examinar um pacote após a criação é abri-lo na ferramenta [Explorador de Pacotes](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer).</span><span class="sxs-lookup"><span data-stu-id="f22e4-305">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="f22e4-306">Isso fornece uma exibição gráfica do conteúdo do pacote e seu manifesto.</span><span class="sxs-lookup"><span data-stu-id="f22e4-306">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="f22e4-307">Você também pode renomear o arquivo `.nupkg` resultante para um arquivo `.zip` e explorar seu conteúdo diretamente.</span><span class="sxs-lookup"><span data-stu-id="f22e4-307">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="f22e4-308">Opções adicionais</span><span class="sxs-lookup"><span data-stu-id="f22e4-308">Additional options</span></span>

<span data-ttu-id="f22e4-309">Você pode usar várias opções de linha de comando com `nuget pack` para excluir arquivos, substituir o número de versão no manifesto e alterar a pasta de saída, entre outros recursos.</span><span class="sxs-lookup"><span data-stu-id="f22e4-309">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="f22e4-310">Para ver uma lista completa, consulte a [referência de comandos do pacote](../tools/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="f22e4-310">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="f22e4-311">As opções a seguir são algumas das escolhas comuns nos projetos do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="f22e4-311">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="f22e4-312">**Projetos referenciados**: se o projeto faz referência a outros projetos, você pode adicionar os projetos referenciados como parte do pacote ou como dependências, usando a opção `-IncludeReferencedProjects`:</span><span class="sxs-lookup"><span data-stu-id="f22e4-312">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="f22e4-313">Esse processo de inclusão é recursivo, portanto, se `MyProject.csproj` faz referência a projetos B e C e os projetos fazem referência a D, E e F, os arquivos de B, C, D, E e F estarão incluídos no pacote.</span><span class="sxs-lookup"><span data-stu-id="f22e4-313">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="f22e4-314">Se um projeto referenciado inclui um arquivo `.nuspec` próprio, o NuGet adiciona esse projeto referenciado como uma dependência em vez disso.</span><span class="sxs-lookup"><span data-stu-id="f22e4-314">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="f22e4-315">Esse projeto precisa ser empacotado e publicado separadamente.</span><span class="sxs-lookup"><span data-stu-id="f22e4-315">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="f22e4-316">**Configuração de build**: por padrão, o NuGet usa a configuração de build padrão definida no arquivo de projeto, normalmente *Depurar*.</span><span class="sxs-lookup"><span data-stu-id="f22e4-316">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="f22e4-317">Para empacotar arquivos de uma configuração de build diferente, como *Versão*, use a opção `-properties` com a configuração:</span><span class="sxs-lookup"><span data-stu-id="f22e4-317">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="f22e4-318">**Símbolos**: para incluir os símbolos que permitem que os consumidores executem o código do seu pacote em etapas no depurador, use a opção `-Symbols`:</span><span class="sxs-lookup"><span data-stu-id="f22e4-318">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="f22e4-319">Testando a instalação do pacote</span><span class="sxs-lookup"><span data-stu-id="f22e4-319">Testing package installation</span></span>

<span data-ttu-id="f22e4-320">Antes de publicar um pacote, geralmente é recomendável testar o processo de instalação de um pacote em um projeto.</span><span class="sxs-lookup"><span data-stu-id="f22e4-320">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="f22e4-321">Os testes garantem que os arquivos todos terminem em seus lugares corretos no projeto.</span><span class="sxs-lookup"><span data-stu-id="f22e4-321">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="f22e4-322">Você pode testar instalações manualmente no Visual Studio ou na linha de comando usando as [etapas de instalação do pacote](../consume-packages/ways-to-install-a-package.md) normais.</span><span class="sxs-lookup"><span data-stu-id="f22e4-322">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/ways-to-install-a-package.md).</span></span>

<span data-ttu-id="f22e4-323">Para testes automatizados, o processo básico é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f22e4-323">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="f22e4-324">Copie o arquivo `.nupkg` para uma pasta local.</span><span class="sxs-lookup"><span data-stu-id="f22e4-324">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="f22e4-325">Adicione a pasta às origens de pacote usando o comando `nuget sources add -name <name> -source <path>` (consulte [origens do nuget](../tools/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="f22e4-325">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="f22e4-326">Observe que é preciso apenas configurar essa origem local uma vez em qualquer computador.</span><span class="sxs-lookup"><span data-stu-id="f22e4-326">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="f22e4-327">Instale o pacote da origem usando `nuget install <packageID> -source <name>` em que `<name>` corresponde ao nome de sua origem conforme fornecido para `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="f22e4-327">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="f22e4-328">Especificar a origem garante que o pacote seja instalado somente dela.</span><span class="sxs-lookup"><span data-stu-id="f22e4-328">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="f22e4-329">Examine o sistema de arquivos para verificar se os arquivos estão instalados corretamente.</span><span class="sxs-lookup"><span data-stu-id="f22e4-329">Examine the file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f22e4-330">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f22e4-330">Next Steps</span></span>

<span data-ttu-id="f22e4-331">Depois de criar um pacote, que é um arquivo `.nupkg`, você pode publicá-lo na galeria de sua escolha conforme descrito em [Publicar um pacote](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="f22e4-331">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="f22e4-332">Você também poderá estender os recursos do seu pacote ou dar suporte a outros cenários conforme descrito nos tópicos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f22e4-332">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="f22e4-333">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="f22e4-333">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="f22e4-334">Suporte a várias estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="f22e4-334">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="f22e4-335">Transformações dos arquivos de configuração e de origem</span><span class="sxs-lookup"><span data-stu-id="f22e4-335">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="f22e4-336">Localização</span><span class="sxs-lookup"><span data-stu-id="f22e4-336">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="f22e4-337">Versões de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="f22e4-337">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="f22e4-338">Por fim, há tipos de pacote adicionais a serem considerados:</span><span class="sxs-lookup"><span data-stu-id="f22e4-338">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="f22e4-339">Pacotes nativos</span><span class="sxs-lookup"><span data-stu-id="f22e4-339">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="f22e4-340">Pacotes de Símbolo</span><span class="sxs-lookup"><span data-stu-id="f22e4-340">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
