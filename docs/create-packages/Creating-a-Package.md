---
title: Criar um pacote do NuGet usando a CLI nuget.exe
description: Um guia detalhado sobre como projetar e criar um pacote NuGet, incluindo arquivos e controle de versão.
author: karann-msft
ms.author: feaguila
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: ec06a8f721b7b67ddc5d72323305b9b22f292de6
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699798"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a><span data-ttu-id="704e1-103">Criar um pacote usando a CLI nuget.exe</span><span class="sxs-lookup"><span data-stu-id="704e1-103">Create a package using the nuget.exe CLI</span></span>

<span data-ttu-id="704e1-104">Independentemente do pacote ou do código que ele contém, use uma das ferramentas de CLI, seja `nuget.exe` ou `dotnet.exe`, para empacotar essa funcionalidade em um componente que possa ser compartilhado e usado por diversos desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="704e1-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="704e1-105">Para instalar as ferramentas de CLI do NuGet, confira [Instalar ferramentas de cliente do NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="704e1-105">To install NuGet CLI tools, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="704e1-106">Observe que o Visual Studio não inclui automaticamente uma ferramenta de CLI.</span><span class="sxs-lookup"><span data-stu-id="704e1-106">Note that Visual Studio does not automatically include a CLI tool.</span></span>

- <span data-ttu-id="704e1-107">Para projetos no estilo não SDK, normalmente projetos do .NET Framework, siga as etapas descritas neste artigo para criar um pacote.</span><span class="sxs-lookup"><span data-stu-id="704e1-107">For non-SDK-style projects, typically .NET Framework projects, follow the steps described in this article to create a package.</span></span> <span data-ttu-id="704e1-108">Para saber mais sobre como usar o Visual Studio e a CLI `nuget.exe`, confira [Criar e publicar um pacote do .NET Framework](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="704e1-108">For step-by-step instructions using Visual Studio and the `nuget.exe` CLI, see [Create and publish a .NET Framework package](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).</span></span>

- <span data-ttu-id="704e1-109">Para projetos .NET Core e .NET Standard que usam o [formato de estilo SDK](../resources/check-project-format.md) e quaisquer outros projetos de estilo SDK, confira [Criar um pacote do NuGet usando a CLI dotnet](creating-a-package-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="704e1-109">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, see [Create a NuGet package using the dotnet CLI](creating-a-package-dotnet-cli.md).</span></span>

- <span data-ttu-id="704e1-110">Para projetos migrados de `packages.config` para [PackageReference](../consume-packages/package-references-in-project-files.md), use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="704e1-110">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

<span data-ttu-id="704e1-111">Tecnicamente, um pacote do NuGet é apenas um arquivo ZIP que foi renomeado com a extensão `.nupkg` e cujo conteúdo corresponde a certas convenções.</span><span class="sxs-lookup"><span data-stu-id="704e1-111">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="704e1-112">Este tópico descreve o processo detalhado da criação de um pacote que cumpre as convenções.</span><span class="sxs-lookup"><span data-stu-id="704e1-112">This topic describes the detailed process of creating a package that meets those conventions.</span></span>

<span data-ttu-id="704e1-113">O empacotamento começa com o código compilado (assemblies), símbolos e/ou outros arquivos que você deseja entregar como um pacote (consulte [Visão geral e o fluxo de trabalho](overview-and-workflow.md)).</span><span class="sxs-lookup"><span data-stu-id="704e1-113">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="704e1-114">Esse processo é independente da compilação ou de qualquer outra forma de geração dos arquivos que entram no pacote, embora seja possível extrair informações em um arquivo de projeto para manter os assemblies e pacotes compilados em sincronização.</span><span class="sxs-lookup"><span data-stu-id="704e1-114">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Important]
> <span data-ttu-id="704e1-115">Este tópico se aplica a projetos no estilo não SDK, normalmente projetos que não sejam .NET Core e .NET Standard e que usam o Visual Studio 2017 e versões superiores e o NuGet 4.0 e posterior.</span><span class="sxs-lookup"><span data-stu-id="704e1-115">This topic applies to non-SDK-style projects, typically projects other than .NET Core and .NET Standard projects using Visual Studio 2017 and higher versions and NuGet 4.0+.</span></span>

## <a name="decide-which-assemblies-to-package"></a><span data-ttu-id="704e1-116">Decida quais assemblies são empacotados</span><span class="sxs-lookup"><span data-stu-id="704e1-116">Decide which assemblies to package</span></span>

<span data-ttu-id="704e1-117">Mais pacotes para fins gerais contêm um ou mais assemblies que outros desenvolvedores podem usar em seus próprios projetos.</span><span class="sxs-lookup"><span data-stu-id="704e1-117">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="704e1-118">Em geral, é recomendável ter um assembly por pacote do NuGet, desde que cada assembly seja útil independentemente.</span><span class="sxs-lookup"><span data-stu-id="704e1-118">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="704e1-119">Por exemplo, se você tiver um `Utilities.dll` que depende de `Parser.dll` e `Parser.dll` é útil por conta própria, crie um pacote para cada um.</span><span class="sxs-lookup"><span data-stu-id="704e1-119">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="704e1-120">Isso permite aos desenvolvedores usar `Parser.dll` independentemente de `Utilities.dll`.</span><span class="sxs-lookup"><span data-stu-id="704e1-120">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="704e1-121">Se sua biblioteca é composta por vários assemblies que não são úteis independentemente, não há problema em combiná-los em um pacote.</span><span class="sxs-lookup"><span data-stu-id="704e1-121">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="704e1-122">Usando o exemplo anterior, se `Parser.dll` contém código que é usado apenas por `Utilities.dll`, não há problema em manter `Parser.dll` no mesmo pacote.</span><span class="sxs-lookup"><span data-stu-id="704e1-122">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="704e1-123">Da mesma forma, se `Utilities.dll` depende de `Utilities.resources.dll`, em que novamente o último não é útil por conta própria, coloque ambos no mesmo pacote.</span><span class="sxs-lookup"><span data-stu-id="704e1-123">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="704e1-124">Os recursos são, na verdade, um caso especial.</span><span class="sxs-lookup"><span data-stu-id="704e1-124">Resources are, in fact, a special case.</span></span> <span data-ttu-id="704e1-125">Quando um pacote é instalado em um projeto, o NuGet adiciona automaticamente as referências de assembly às DLLs do pacote, *excluindo* aquelas que são nomeados `.resources.dll` porque são considerados assemblies satélites (consulte [Criando pacotes localizados](creating-localized-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="704e1-125">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="704e1-126">Por esse motivo, evite usar `.resources.dll` para arquivos que contêm código de pacote essencial.</span><span class="sxs-lookup"><span data-stu-id="704e1-126">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="704e1-127">Se sua biblioteca contém assemblies de interoperabilidade COM, siga as diretrizes adicionais em [Criar pacotes com assemblies de interoperabilidade COM](author-packages-with-com-interop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="704e1-127">If your library contains COM interop assemblies, follow additional the guidelines in [Create packages with COM interop assemblies](author-packages-with-com-interop-assemblies.md).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="704e1-128">A função e a estrutura do arquivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="704e1-128">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="704e1-129">Depois que você sabe quais arquivos deseja empacotar, a próxima etapa é criar um manifesto de pacote em um arquivo XML `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="704e1-129">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="704e1-130">O manifesto:</span><span class="sxs-lookup"><span data-stu-id="704e1-130">The manifest:</span></span>

1. <span data-ttu-id="704e1-131">Descreve o conteúdo do pacote e é incluído nele.</span><span class="sxs-lookup"><span data-stu-id="704e1-131">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="704e1-132">Controla a criação do pacote e instrui o NuGet sobre como instalá-lo em um projeto.</span><span class="sxs-lookup"><span data-stu-id="704e1-132">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="704e1-133">Por exemplo, o manifesto identifica outras dependências de pacote, de modo que o NuGet também pode instalar essas dependências quando o pacote principal é instalado.</span><span class="sxs-lookup"><span data-stu-id="704e1-133">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="704e1-134">Contém propriedades obrigatórias e opcionais, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="704e1-134">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="704e1-135">Para obter detalhes exatos, incluindo outras propriedades não mencionadas aqui, consulte a [Referência de .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="704e1-135">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="704e1-136">Propriedades necessárias:</span><span class="sxs-lookup"><span data-stu-id="704e1-136">Required properties:</span></span>

- <span data-ttu-id="704e1-137">O identificador de pacotes, que deve ser exclusivo entre a galeria que hospeda o pacote.</span><span class="sxs-lookup"><span data-stu-id="704e1-137">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="704e1-138">Um número de versão específico na forma *Principal.Secundário.Patch[-Suffix]* em que *-Suffix* identifica [versões de pré-lançamento](prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="704e1-138">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="704e1-139">O título do pacote como ele deve aparecer no host (como nuget.org)</span><span class="sxs-lookup"><span data-stu-id="704e1-139">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="704e1-140">Informações de autor e proprietário.</span><span class="sxs-lookup"><span data-stu-id="704e1-140">Author and owner information.</span></span>
- <span data-ttu-id="704e1-141">Uma descrição longa do pacote.</span><span class="sxs-lookup"><span data-stu-id="704e1-141">A long description of the package.</span></span>

<span data-ttu-id="704e1-142">Propriedades opcionais comuns:</span><span class="sxs-lookup"><span data-stu-id="704e1-142">Common optional properties:</span></span>

- <span data-ttu-id="704e1-143">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="704e1-143">Release notes</span></span>
- <span data-ttu-id="704e1-144">Informações de direitos autorais</span><span class="sxs-lookup"><span data-stu-id="704e1-144">Copyright information</span></span>
- <span data-ttu-id="704e1-145">Uma breve descrição para a [Interface do usuário do Gerenciador de Pacotes no Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="704e1-145">A short description for the [Package Manager UI in Visual Studio](../consume-packages/install-use-packages-visual-studio.md)</span></span>
- <span data-ttu-id="704e1-146">Uma identificação de localidade</span><span class="sxs-lookup"><span data-stu-id="704e1-146">A locale ID</span></span>
- <span data-ttu-id="704e1-147">URL de Projeto</span><span class="sxs-lookup"><span data-stu-id="704e1-147">Project URL</span></span>
- <span data-ttu-id="704e1-148">Licença como uma expressão ou um arquivo ( `licenseUrl` é preterido, use o [ `license` elemento de metadados nuspec](../reference/nuspec.md#license) em vez disso)</span><span class="sxs-lookup"><span data-stu-id="704e1-148">License as an expression or file (`licenseUrl` is deprecated, use [`license` nuspec metadata element](../reference/nuspec.md#license) instead)</span></span>
- <span data-ttu-id="704e1-149">Um arquivo de ícone ( `iconUrl` é preterido, use o [ `icon` elemento de metadados nuspec](../reference/nuspec.md#icon) )</span><span class="sxs-lookup"><span data-stu-id="704e1-149">An icon file (`iconUrl` is deprecated use [`icon` nuspec metadata element](../reference/nuspec.md#icon) instead)</span></span>
- <span data-ttu-id="704e1-150">Listas de dependências e referências</span><span class="sxs-lookup"><span data-stu-id="704e1-150">Lists of dependencies and references</span></span>
- <span data-ttu-id="704e1-151">Marcas que auxiliam em pesquisas de galeria</span><span class="sxs-lookup"><span data-stu-id="704e1-151">Tags that assist in gallery searches</span></span>

<span data-ttu-id="704e1-152">A seguir está um arquivo `.nuspec` típico (mas fictício), com os comentários que descrevem as propriedades:</span><span class="sxs-lookup"><span data-stu-id="704e1-152">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- Package version number that is used when resolving dependencies -->
        <version>1.8.3</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

        <!-- Icon is used in Visual Studio's package manager UI -->
        <icon>icon.png</icon>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
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
        <file src="icon.png" target="" />
    </files>
</package>
```

<span data-ttu-id="704e1-153">Para obter detalhes sobre como declarar dependências e especificar números de versão, consulte [packages.config](../reference/packages-config.md) e [Controle de versão do pacote](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="704e1-153">For details on declaring dependencies and specifying version numbers, see [packages.config](../reference/packages-config.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="704e1-154">Também é possível extrair ativos das dependências diretamente no pacote usando o os atributos `include` e `exclude` no elemento `dependency`.</span><span class="sxs-lookup"><span data-stu-id="704e1-154">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="704e1-155">Consulte [Referência de .nuspec – Dependências](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="704e1-155">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="704e1-156">Como o manifesto está incluído no pacote criado com base nele, encontre vários exemplos adicionais examinando os pacotes existentes.</span><span class="sxs-lookup"><span data-stu-id="704e1-156">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="704e1-157">Uma boa fonte é a pasta *global-packages* em seu computador, cuja localização é retornada pelo comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="704e1-157">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="704e1-158">Acesse qualquer pasta *package\version*, copie o arquivo `.nupkg` para um arquivo `.zip` e depois abra esse arquivo `.zip` e examine o `.nuspec` dentro dele.</span><span class="sxs-lookup"><span data-stu-id="704e1-158">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="704e1-159">Ao criar um `.nuspec` de um projeto do Visual Studio, o manifesto contém tokens que são substituídos com informações do projeto quando o pacote é compilado.</span><span class="sxs-lookup"><span data-stu-id="704e1-159">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="704e1-160">Consulte [Criando o .nuspec de um projeto do Visual Studio](#from-a-visual-studio-project).</span><span class="sxs-lookup"><span data-stu-id="704e1-160">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="create-the-nuspec-file"></a><span data-ttu-id="704e1-161">Criar o arquivo .nuspec</span><span class="sxs-lookup"><span data-stu-id="704e1-161">Create the .nuspec file</span></span>

<span data-ttu-id="704e1-162">Criar um manifesto completo normalmente começa com um arquivo `.nuspec` básico gerado usando um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="704e1-162">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="704e1-163">Um diretório de trabalho baseado em convenção</span><span class="sxs-lookup"><span data-stu-id="704e1-163">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="704e1-164">Uma DLL de assembly</span><span class="sxs-lookup"><span data-stu-id="704e1-164">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="704e1-165">Um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="704e1-165">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="704e1-166">Novo arquivo com valores padrão</span><span class="sxs-lookup"><span data-stu-id="704e1-166">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="704e1-167">Em seguida, edite o arquivo manualmente para que ele descreva o conteúdo exato que você deseja no pacote final.</span><span class="sxs-lookup"><span data-stu-id="704e1-167">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="704e1-168">Arquivos `.nuspec` gerados contêm espaços reservados que precisam ser modificados antes de criar o pacote com o comando `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="704e1-168">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="704e1-169">Esse comando falhará se o `.nuspec` contiver algum espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="704e1-169">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="704e1-170">De um diretório de trabalho baseado em convenção</span><span class="sxs-lookup"><span data-stu-id="704e1-170">From a convention-based working directory</span></span>

<span data-ttu-id="704e1-171">Como um pacote do NuGet é apenas um arquivo ZIP que foi renomeado com a extensão `.nupkg`, geralmente é mais fácil criar a estrutura de pastas que você deseja no sistema de arquivos local para depois criar o arquivo `.nuspec` diretamente dessa estrutura.</span><span class="sxs-lookup"><span data-stu-id="704e1-171">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="704e1-172">O comando `nuget pack` adicionará automaticamente todos os arquivos nessa estrutura de pastas (excluindo as pastas que começam com `.`, permitindo que você mantenha arquivos particulares na mesma estrutura).</span><span class="sxs-lookup"><span data-stu-id="704e1-172">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="704e1-173">A vantagem dessa abordagem é que você não precisa especificar no manifesto quais arquivos você deseja incluir no pacote (conforme explicado mais adiante neste tópico).</span><span class="sxs-lookup"><span data-stu-id="704e1-173">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="704e1-174">Basta fazer com que o processo de build produza a estrutura de pasta exata que vai para o pacote e incluir facilmente outros arquivos que não podem fazer parte de um projeto, caso contrário:</span><span class="sxs-lookup"><span data-stu-id="704e1-174">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="704e1-175">O conteúdo e o código-fonte que devem ser inseridos no projeto de destino.</span><span class="sxs-lookup"><span data-stu-id="704e1-175">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="704e1-176">Scripts do PowerShell</span><span class="sxs-lookup"><span data-stu-id="704e1-176">PowerShell scripts</span></span>
- <span data-ttu-id="704e1-177">Transformações em configuração existentes e arquivos de código-fonte em um projeto.</span><span class="sxs-lookup"><span data-stu-id="704e1-177">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="704e1-178">As convenções de pasta são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="704e1-178">The folder conventions are as follows:</span></span>

| <span data-ttu-id="704e1-179">Pasta</span><span class="sxs-lookup"><span data-stu-id="704e1-179">Folder</span></span> | <span data-ttu-id="704e1-180">Descrição</span><span class="sxs-lookup"><span data-stu-id="704e1-180">Description</span></span> | <span data-ttu-id="704e1-181">Ação após a instalação do pacote</span><span class="sxs-lookup"><span data-stu-id="704e1-181">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="704e1-182">(raiz)</span><span class="sxs-lookup"><span data-stu-id="704e1-182">(root)</span></span> | <span data-ttu-id="704e1-183">Local para leiame.txt</span><span class="sxs-lookup"><span data-stu-id="704e1-183">Location for readme.txt</span></span> | <span data-ttu-id="704e1-184">O Visual Studio exibe um arquivo Leiame.txt na raiz do pacote quando este é instalado.</span><span class="sxs-lookup"><span data-stu-id="704e1-184">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="704e1-185">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="704e1-185">lib/{tfm}</span></span> | <span data-ttu-id="704e1-186">Arquivos de assembly (`.dll`), documentação (`.xml`) e símbolo (`.pdb`) para TFM (Moniker de Estrutura de Destino)</span><span class="sxs-lookup"><span data-stu-id="704e1-186">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="704e1-187">Os assemblies são adicionados como referências para a compilação e o runtime também; `.xml` e `.pdb` são copiados para as pastas do projeto.</span><span class="sxs-lookup"><span data-stu-id="704e1-187">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="704e1-188">Consulte [Suporte a várias estruturas de destino](supporting-multiple-target-frameworks.md) para ver a criação de subpastas específicas de destino da estrutura.</span><span class="sxs-lookup"><span data-stu-id="704e1-188">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="704e1-189">ref/{tfm}</span><span class="sxs-lookup"><span data-stu-id="704e1-189">ref/{tfm}</span></span> | <span data-ttu-id="704e1-190">Arquivos de assembly (`.dll`) e símbolo (`.pdb`) para TFM (Moniker de Estrutura de Destino)</span><span class="sxs-lookup"><span data-stu-id="704e1-190">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="704e1-191">Assemblies são adicionados como referências apenas para o tempo de compilação, portanto, nada será copiado para a pasta lixeira do projeto.</span><span class="sxs-lookup"><span data-stu-id="704e1-191">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="704e1-192">runtimes</span><span class="sxs-lookup"><span data-stu-id="704e1-192">runtimes</span></span> | <span data-ttu-id="704e1-193">Arquivos de assembly específico de arquitetura (`.dll`), símbolo (`.pdb`) e recurso nativo (`.pri`)</span><span class="sxs-lookup"><span data-stu-id="704e1-193">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="704e1-194">Assemblies são adicionados como referências apenas para o runtime. Outros arquivos são copiados para as pastas do projeto.</span><span class="sxs-lookup"><span data-stu-id="704e1-194">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="704e1-195">Deve sempre haver um assembly específico (TFM) `AnyCPU` correspondente na pasta `/ref/{tfm}` para oferecer o assembly de tempo de compilação correspondente.</span><span class="sxs-lookup"><span data-stu-id="704e1-195">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="704e1-196">Consulte [Suporte a várias estruturas de destino](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="704e1-196">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="704e1-197">conteúdo</span><span class="sxs-lookup"><span data-stu-id="704e1-197">content</span></span> | <span data-ttu-id="704e1-198">Arquivos arbitrários</span><span class="sxs-lookup"><span data-stu-id="704e1-198">Arbitrary files</span></span> | <span data-ttu-id="704e1-199">O conteúdo é copiado para a raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="704e1-199">Contents are copied to the project root.</span></span> <span data-ttu-id="704e1-200">Pense na pasta **content** como a raiz do aplicativo de destino que, enfim, consome o pacote.</span><span class="sxs-lookup"><span data-stu-id="704e1-200">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="704e1-201">Para fazer o pacote adicionar uma imagem à pasta */imagens* do aplicativo, coloque-o na pasta *content/images* do pacote.</span><span class="sxs-lookup"><span data-stu-id="704e1-201">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="704e1-202">compilar</span><span class="sxs-lookup"><span data-stu-id="704e1-202">build</span></span> | <span data-ttu-id="704e1-203">Arquivos `.targets` e `.props` do MSBuild *(3.x+)*</span><span class="sxs-lookup"><span data-stu-id="704e1-203">*(3.x+)* MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="704e1-204">Inserido automaticamente no projeto.</span><span class="sxs-lookup"><span data-stu-id="704e1-204">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="704e1-205">buildMultiTargeting</span><span class="sxs-lookup"><span data-stu-id="704e1-205">buildMultiTargeting</span></span> | <span data-ttu-id="704e1-206">Arquivos `.targets` e `.props` do MSBuild *(4.0+)* para direcionamento entre estruturas</span><span class="sxs-lookup"><span data-stu-id="704e1-206">*(4.0+)* MSBuild `.targets` and `.props` files for cross-framework targeting</span></span> | <span data-ttu-id="704e1-207">Inserido automaticamente no projeto.</span><span class="sxs-lookup"><span data-stu-id="704e1-207">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="704e1-208">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="704e1-208">buildTransitive</span></span> | <span data-ttu-id="704e1-209">Arquivos `.targets` e `.props` do MSBuild *(5.0+)* que fluem para qualquer projeto de consumo.</span><span class="sxs-lookup"><span data-stu-id="704e1-209">*(5.0+)* MSBuild `.targets` and `.props` files that flow transitively to any consuming project.</span></span> <span data-ttu-id="704e1-210">Confira a página de [recursos](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior).</span><span class="sxs-lookup"><span data-stu-id="704e1-210">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> | <span data-ttu-id="704e1-211">Inserido automaticamente no projeto.</span><span class="sxs-lookup"><span data-stu-id="704e1-211">Automatically inserted into the project.</span></span> |
| <span data-ttu-id="704e1-212">tools</span><span class="sxs-lookup"><span data-stu-id="704e1-212">tools</span></span> | <span data-ttu-id="704e1-213">Scripts e programas do Powershell acessíveis do Console do Gerenciador de Pacotes</span><span class="sxs-lookup"><span data-stu-id="704e1-213">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="704e1-214">A pasta `tools` é adicionada à variável de ambiente `PATH` somente para o Console do Gerenciador de Pacotes (especificamente, *não* para o `PATH` conforme definido para MSBuild ao criar o projeto).</span><span class="sxs-lookup"><span data-stu-id="704e1-214">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="704e1-215">Como a estrutura de pastas pode conter qualquer número de assemblies para uma infinidade de estruturas de destino, esse método é necessário ao criar pacotes compatíveis com várias estruturas.</span><span class="sxs-lookup"><span data-stu-id="704e1-215">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="704e1-216">Em qualquer caso, uma vez que a estrutura de pastas esteja em vigor, execute o seguinte comando nessa pasta para criar o arquivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="704e1-216">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="704e1-217">Novamente, o `.nuspec` gerado não contém nenhuma referência explícita a arquivos na estrutura de pasta.</span><span class="sxs-lookup"><span data-stu-id="704e1-217">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="704e1-218">O NuGet inclui automaticamente todos os arquivos quando o pacote é criado.</span><span class="sxs-lookup"><span data-stu-id="704e1-218">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="704e1-219">No entanto, você ainda precisa editar os valores de espaço reservado em outras partes do manifesto.</span><span class="sxs-lookup"><span data-stu-id="704e1-219">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="704e1-220">De uma DLL de assembly</span><span class="sxs-lookup"><span data-stu-id="704e1-220">From an assembly DLL</span></span>

<span data-ttu-id="704e1-221">No caso mais simples de criar um pacote de um assembly, você pode gerar um arquivo `.nuspec` dos metadados no assembly usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="704e1-221">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="704e1-222">Usar este formulário substitui alguns espaços reservados no manifesto por valores específicos do assembly.</span><span class="sxs-lookup"><span data-stu-id="704e1-222">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="704e1-223">Por exemplo, a propriedade `<id>` é definida como o nome do assembly e `<version>` é definido como a versão do assembly.</span><span class="sxs-lookup"><span data-stu-id="704e1-223">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="704e1-224">Outras propriedades no manifesto, no entanto, não têm valores correspondentes no assembly e, portanto, ainda contêm espaços reservados.</span><span class="sxs-lookup"><span data-stu-id="704e1-224">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="704e1-225">De um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="704e1-225">From a Visual Studio project</span></span>

<span data-ttu-id="704e1-226">É muito conveniente criar um `.nuspec` de um arquivo `.csproj` ou `.vbproj`, pois outros pacotes que foram instalados nesses projetos são referenciados automaticamente como dependências.</span><span class="sxs-lookup"><span data-stu-id="704e1-226">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="704e1-227">Simplesmente use o comando a seguir na mesma pasta que o arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="704e1-227">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="704e1-228">O arquivo `<project-name>.nuspec` resultante contém *tokens* que são substituídos no tempo de empacotamento pelos valores do projeto, incluindo referências aos outros pacotes que já foram instalados.</span><span class="sxs-lookup"><span data-stu-id="704e1-228">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="704e1-229">Se você tiver dependências de pacote para incluir no *.nuspec*, use `nuget pack` e obtenha o arquivo *.nuspec* do arquivo *.nupkg* gerado.</span><span class="sxs-lookup"><span data-stu-id="704e1-229">If you have package dependencies to include in the *.nuspec*, instead use `nuget pack`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="704e1-230">Por exemplo, use o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="704e1-230">For example, use the following command.</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

<span data-ttu-id="704e1-231">Um token é delimitado por símbolos `$` em ambos os lados da propriedade de projeto.</span><span class="sxs-lookup"><span data-stu-id="704e1-231">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="704e1-232">Por exemplo, o valor `<id>` em um manifesto gerado dessa forma normalmente aparece da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="704e1-232">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="704e1-233">Esse token é substituído pelo valor `AssemblyName` do arquivo de projeto no tempo de empacotamento.</span><span class="sxs-lookup"><span data-stu-id="704e1-233">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="704e1-234">Para ver o mapeamento exato de valores de projeto para tokens `.nuspec`, consulte a [Referência de tokens de substituição](../reference/nuspec.md#replacement-tokens).</span><span class="sxs-lookup"><span data-stu-id="704e1-234">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="704e1-235">Tokens eliminam a necessidade de atualizar valores cruciais como o número de versão do `.nuspec` ao atualizar o projeto.</span><span class="sxs-lookup"><span data-stu-id="704e1-235">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="704e1-236">(Você sempre pode substituir os tokens por valores literais, se desejado.)</span><span class="sxs-lookup"><span data-stu-id="704e1-236">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="704e1-237">Observe que há várias opções de empacotamento adicional disponíveis ao trabalhar em um projeto do Visual Studio, conforme descrito em [Executando o pacote do nuget para gerar o arquivo .nupkg](#run-nuget-pack-to-generate-the-nupkg-file) posteriormente.</span><span class="sxs-lookup"><span data-stu-id="704e1-237">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#run-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="704e1-238">Pacotes de nível de solução</span><span class="sxs-lookup"><span data-stu-id="704e1-238">Solution-level packages</span></span>

<span data-ttu-id="704e1-239">*Somente NuGet 2. x. Não disponível no NuGet 3.0 +.*</span><span class="sxs-lookup"><span data-stu-id="704e1-239">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="704e1-240">O NuGet 2.x é compatível com a noção de um pacote de nível de solução que instala ferramentas ou comandos adicionais para o Console do Gerenciador de Pacotes (o conteúdo da pasta `tools`), mas não adiciona referências, conteúdo ou personalizações de build aos projetos na solução.</span><span class="sxs-lookup"><span data-stu-id="704e1-240">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="704e1-241">Esses pacotes não contém arquivos em suas pastas `lib`, `content` ou `build` diretas e nenhuma de suas dependências têm arquivos em suas respectivas pastas `lib`, `content` ou `build`.</span><span class="sxs-lookup"><span data-stu-id="704e1-241">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="704e1-242">O NuGet rastreia os pacotes instalados no nível da solução em um arquivo `packages.config` na pasta `.nuget`, em vez do arquivo `packages.config` do projeto.</span><span class="sxs-lookup"><span data-stu-id="704e1-242">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="704e1-243">Novo arquivo com valores padrão</span><span class="sxs-lookup"><span data-stu-id="704e1-243">New file with default values</span></span>

<span data-ttu-id="704e1-244">O comando a seguir cria um manifesto padrão com espaços reservados, que garante que você inicie com a estrutura de arquivos apropriada:</span><span class="sxs-lookup"><span data-stu-id="704e1-244">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="704e1-245">Se você omitir \<package-name\> , o arquivo resultante será `Package.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="704e1-245">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="704e1-246">Se você fornecer um nome como `Contoso.Utility.UsefulStuff`, o arquivo será `Contoso.Utility.UsefulStuff.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="704e1-246">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="704e1-247">O `.nuspec` resultante contém espaços reservados para valores como o `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="704e1-247">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="704e1-248">Edite o arquivo antes de usá-lo para criar o arquivo `.nupkg` final.</span><span class="sxs-lookup"><span data-stu-id="704e1-248">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="704e1-249">Escolha um identificador de pacote exclusivo e definindo o número de versão</span><span class="sxs-lookup"><span data-stu-id="704e1-249">Choose a unique package identifier and setting the version number</span></span>

<span data-ttu-id="704e1-250">O identificador de pacote (elemento `<id>`) e o número de versão (elemento `<version>`) são os dois valores mais importantes no manifesto, pois eles identificam exclusivamente o código exato que está contido no pacote.</span><span class="sxs-lookup"><span data-stu-id="704e1-250">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="704e1-251">**Práticas recomendadas para o identificador de pacote:**</span><span class="sxs-lookup"><span data-stu-id="704e1-251">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="704e1-252">**Exclusividade**: o identificador deve ser exclusivo no nuget.org ou na galeria que hospeda o pacote.</span><span class="sxs-lookup"><span data-stu-id="704e1-252">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="704e1-253">Antes de decidir sobre um identificador, pesquise a galeria aplicável para verificar se o nome já está em uso.</span><span class="sxs-lookup"><span data-stu-id="704e1-253">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="704e1-254">Para evitar conflitos, um bom padrão é usar o nome da sua empresa como a primeira parte do identificador, como `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="704e1-254">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="704e1-255">**Nomes semelhantes a namespace**: siga um padrão semelhante aos namespaces no .NET, usando a notação de ponto em vez de hifens.</span><span class="sxs-lookup"><span data-stu-id="704e1-255">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="704e1-256">Por exemplo, use `Contoso.Utility.UsefulStuff` em vez de `Contoso-Utility-UsefulStuff` ou `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="704e1-256">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="704e1-257">Também é útil para os consumidores quando o identificador de pacote corresponde os namespaces usados no código.</span><span class="sxs-lookup"><span data-stu-id="704e1-257">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="704e1-258">**Pacotes de exemplo**: se você gerar um pacote de código de exemplo que demonstra como usar outro pacote, anexe `.Sample` como um sufixo ao identificador, como em `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="704e1-258">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="704e1-259">(O pacote de exemplo, obviamente, teria uma dependência do outro pacote.) Ao criar um pacote de exemplo, use o método de diretório de trabalho baseado em Convenção descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="704e1-259">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="704e1-260">Na pasta `content`, organize o código de exemplo em uma pasta chamada `\Samples\<identifier>` como no `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="704e1-260">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="704e1-261">**Práticas recomendadas para a versão de pacote:**</span><span class="sxs-lookup"><span data-stu-id="704e1-261">**Best practices for the package version:**</span></span>

- <span data-ttu-id="704e1-262">Em geral, defina a versão do pacote para corresponder à biblioteca, embora isso não seja estritamente necessário.</span><span class="sxs-lookup"><span data-stu-id="704e1-262">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="704e1-263">Isso é muito simples quando você limita um pacote a um único assembly, conforme descrito anteriormente em [Decidir quais assemblies serão empacotados](#decide-which-assemblies-to-package).</span><span class="sxs-lookup"><span data-stu-id="704e1-263">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#decide-which-assemblies-to-package).</span></span> <span data-ttu-id="704e1-264">Em geral, lembre-se que o NuGet em si lida com versões do pacote ao resolver as dependências, não versões de assembly.</span><span class="sxs-lookup"><span data-stu-id="704e1-264">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="704e1-265">Ao usar um esquema de versão não padrão, considere as regras de controle de versão do NuGet, conforme explicado em [Controle de versão do pacote](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="704e1-265">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../concepts/package-versioning.md).</span></span>

> <span data-ttu-id="704e1-266">A seguinte série de breves postagens no blog também é útil para entender o controle de versão:</span><span class="sxs-lookup"><span data-stu-id="704e1-266">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="704e1-267">Parte 1: assumindo o DLL Hell</span><span class="sxs-lookup"><span data-stu-id="704e1-267">Part 1: Taking on DLL Hell</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="704e1-268">Parte 2: o algoritmo principal</span><span class="sxs-lookup"><span data-stu-id="704e1-268">Part 2: The core algorithm</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="704e1-269">Parte 3: unificação por meio de redirecionamentos de associação</span><span class="sxs-lookup"><span data-stu-id="704e1-269">Part 3: Unification via Binding Redirects</span></span>](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a><span data-ttu-id="704e1-270">Adicione um Leiame e outros arquivos</span><span class="sxs-lookup"><span data-stu-id="704e1-270">Add a readme and other files</span></span>

<span data-ttu-id="704e1-271">Para especificar diretamente os arquivos a serem incluídos no pacote, use o nó `<files>` no arquivo `.nuspec`, que *segue* a marca `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="704e1-271">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
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
> <span data-ttu-id="704e1-272">Ao usar a abordagem de diretório de trabalho baseado em convenção, você pode colocar o Leiame.txt na raiz do pacote e outros conteúdos na pasta `content`.</span><span class="sxs-lookup"><span data-stu-id="704e1-272">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="704e1-273">Nenhum elemento `<file>` é necessário no manifesto.</span><span class="sxs-lookup"><span data-stu-id="704e1-273">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="704e1-274">Quando você inclui um arquivo chamado `readme.txt` na raiz do pacote, o Visual Studio exibe o conteúdo do arquivo como texto sem formatação imediatamente depois de instalar o pacote diretamente.</span><span class="sxs-lookup"><span data-stu-id="704e1-274">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="704e1-275">(Arquivos Leiame não são exibidos para pacotes instalados como dependências).</span><span class="sxs-lookup"><span data-stu-id="704e1-275">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="704e1-276">Por exemplo, mostramos aqui como o arquivo Leiame para o pacote HtmlAgilityPack é exibido:</span><span class="sxs-lookup"><span data-stu-id="704e1-276">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![A exibição de um arquivo Leiame para um pacote do NuGet na instalação](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="704e1-278">Se você incluir um nó `<files>` vazio no arquivo `.nuspec`, o NuGet não incluirá nenhum outro conteúdo no pacote que não seja o que está na pasta `lib`.</span><span class="sxs-lookup"><span data-stu-id="704e1-278">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="include-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="704e1-279">Incluir objetivos e destinos de MSBuild em um pacote</span><span class="sxs-lookup"><span data-stu-id="704e1-279">Include MSBuild props and targets in a package</span></span>

<span data-ttu-id="704e1-280">Em alguns casos, convém adicionar destinos ou propriedades de build personalizados a projetos que consomem o pacote, como a execução de uma ferramenta personalizada ou um processo durante o build.</span><span class="sxs-lookup"><span data-stu-id="704e1-280">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="704e1-281">Faça isso colocando arquivos no formato `<package_id>.targets` ou `<package_id>.props` (como `Contoso.Utility.UsefulStuff.targets`) dentro da pasta `\build` do projeto.</span><span class="sxs-lookup"><span data-stu-id="704e1-281">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="704e1-282">Arquivos na pasta `\build` raiz são considerados adequados para todas as estruturas de destino.</span><span class="sxs-lookup"><span data-stu-id="704e1-282">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="704e1-283">Para fornecer arquivos específicos de estrutura, primeiro coloque-os em subpastas apropriadas, como os seguintes:</span><span class="sxs-lookup"><span data-stu-id="704e1-283">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

```
    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
```

<span data-ttu-id="704e1-284">Em seguida, no arquivo `.nuspec`, faça referência a esses arquivos no nó `<files>`:</span><span class="sxs-lookup"><span data-stu-id="704e1-284">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

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

<span data-ttu-id="704e1-285">Incluindo os arquivos de propriedades e de destinos do MSBuild em um pacote [introduzidos com o NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), portanto é recomendado adicionar o atributo `minClientVersion="2.5"` ao elemento `metadata` para indicar a versão mínima necessária do cliente NuGet para consumir o pacote.</span><span class="sxs-lookup"><span data-stu-id="704e1-285">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="704e1-286">Quando o NuGet instala um pacote com arquivos `\build`, ele adiciona elementos `<Import>` do MSBuild ao arquivo de projeto que aponta para os arquivos `.targets` e `.props`.</span><span class="sxs-lookup"><span data-stu-id="704e1-286">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="704e1-287">( `.props` é adicionado na parte superior do arquivo de projeto; `.targets` é adicionado na parte inferior.) Um elemento diferente do MSBuild condicional `<Import>` é adicionado para cada estrutura de destino.</span><span class="sxs-lookup"><span data-stu-id="704e1-287">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="704e1-288">É possível colocar os arquivos `.props` e `.targets` do MSBuild na pasta `\buildMultiTargeting` para direcionamento entre estruturas.</span><span class="sxs-lookup"><span data-stu-id="704e1-288">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildMultiTargeting` folder.</span></span> <span data-ttu-id="704e1-289">Durante a instalação do pacote, o NuGet adiciona elementos `<Import>` correspondentes ao arquivo de projeto contanto que a estrutura de destino não esteja definida (a propriedade `$(TargetFramework)` do MSBuild deve estar vazia).</span><span class="sxs-lookup"><span data-stu-id="704e1-289">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="704e1-290">Com o NuGet 3.x, os destinos não são adicionados ao projeto, mas são disponibilizados por meio de `{projectName}.nuget.g.targets` e `{projectName}.nuget.g.props`.</span><span class="sxs-lookup"><span data-stu-id="704e1-290">With NuGet 3.x, targets are not added to the project but are instead made available through `{projectName}.nuget.g.targets` and `{projectName}.nuget.g.props`.</span></span>

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="704e1-291">Execute o nuget pack para gerar o arquivo .nupkg</span><span class="sxs-lookup"><span data-stu-id="704e1-291">Run nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="704e1-292">Ao usar um assembly ou o diretório de trabalho baseado em convenção, crie um pacote executando `nuget pack` com seu arquivo `.nuspec`, substituindo `<project-name>` pelo nome do seu arquivo específico:</span><span class="sxs-lookup"><span data-stu-id="704e1-292">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="704e1-293">Ao usar um projeto do Visual Studio, execute `nuget pack` com o arquivo de projeto, que carrega automaticamente o arquivo `.nuspec` do projeto e substitui todos os tokens dentro dele usando valores no arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="704e1-293">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="704e1-294">É necessário usar o arquivo de projeto diretamente para a substituição do token porque o projeto é a origem dos valores de token.</span><span class="sxs-lookup"><span data-stu-id="704e1-294">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="704e1-295">A substituição do token não ocorre se você usar `nuget pack` com um arquivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="704e1-295">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="704e1-296">Em todos os casos, o `nuget pack` exclui pastas que começam com um ponto, como `.git` ou `.hg`.</span><span class="sxs-lookup"><span data-stu-id="704e1-296">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="704e1-297">O NuGet indica se há erros no arquivo `.nuspec` que precisam de correção, como se esquecer de alterar os valores de espaço reservado no manifesto.</span><span class="sxs-lookup"><span data-stu-id="704e1-297">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="704e1-298">Depois que o `nuget pack` for bem-sucedido, você tem um arquivo `.nupkg` que pode ser publicado para uma galeria adequada conforme descrito em [Publicar um pacote](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="704e1-298">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="704e1-299">Uma maneira útil de examinar um pacote após a criação é abri-lo na ferramenta [Explorador de Pacotes](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer).</span><span class="sxs-lookup"><span data-stu-id="704e1-299">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="704e1-300">Isso fornece uma exibição gráfica do conteúdo do pacote e seu manifesto.</span><span class="sxs-lookup"><span data-stu-id="704e1-300">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="704e1-301">Você também pode renomear o arquivo `.nupkg` resultante para um arquivo `.zip` e explorar seu conteúdo diretamente.</span><span class="sxs-lookup"><span data-stu-id="704e1-301">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="704e1-302">Opções adicionais</span><span class="sxs-lookup"><span data-stu-id="704e1-302">Additional options</span></span>

<span data-ttu-id="704e1-303">Você pode usar várias opções de linha de comando com `nuget pack` para excluir arquivos, substituir o número de versão no manifesto e alterar a pasta de saída, entre outros recursos.</span><span class="sxs-lookup"><span data-stu-id="704e1-303">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="704e1-304">Para ver uma lista completa, consulte a [referência de comandos do pacote](../reference/cli-reference/cli-ref-pack.md).</span><span class="sxs-lookup"><span data-stu-id="704e1-304">For a complete list, refer to the [pack command reference](../reference/cli-reference/cli-ref-pack.md).</span></span>

<span data-ttu-id="704e1-305">As opções a seguir são algumas das escolhas comuns nos projetos do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="704e1-305">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="704e1-306">**Projetos referenciados**: se o projeto faz referência a outros projetos, você pode adicionar os projetos referenciados como parte do pacote ou como dependências, usando a opção `-IncludeReferencedProjects`:</span><span class="sxs-lookup"><span data-stu-id="704e1-306">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="704e1-307">Esse processo de inclusão é recursivo, portanto, se `MyProject.csproj` faz referência a projetos B e C e os projetos fazem referência a D, E e F, os arquivos de B, C, D, E e F estarão incluídos no pacote.</span><span class="sxs-lookup"><span data-stu-id="704e1-307">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="704e1-308">Se um projeto referenciado inclui um arquivo `.nuspec` próprio, o NuGet adiciona esse projeto referenciado como uma dependência em vez disso.</span><span class="sxs-lookup"><span data-stu-id="704e1-308">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="704e1-309">Esse projeto precisa ser empacotado e publicado separadamente.</span><span class="sxs-lookup"><span data-stu-id="704e1-309">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="704e1-310">**Configuração de build**: por padrão, o NuGet usa a configuração de build padrão definida no arquivo de projeto, normalmente *Depurar*.</span><span class="sxs-lookup"><span data-stu-id="704e1-310">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="704e1-311">Para empacotar arquivos de uma configuração de build diferente, como *Versão*, use a opção `-properties` com a configuração:</span><span class="sxs-lookup"><span data-stu-id="704e1-311">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="704e1-312">**Símbolos**: para incluir os símbolos que permitem que os consumidores executem o código do seu pacote em etapas no depurador, use a opção `-Symbols`:</span><span class="sxs-lookup"><span data-stu-id="704e1-312">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a><span data-ttu-id="704e1-313">Instalação do pacote de teste</span><span class="sxs-lookup"><span data-stu-id="704e1-313">Test package installation</span></span>

<span data-ttu-id="704e1-314">Antes de publicar um pacote, geralmente é recomendável testar o processo de instalação de um pacote em um projeto.</span><span class="sxs-lookup"><span data-stu-id="704e1-314">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="704e1-315">Os testes garantem que os arquivos todos terminem em seus lugares corretos no projeto.</span><span class="sxs-lookup"><span data-stu-id="704e1-315">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="704e1-316">Você pode testar instalações manualmente no Visual Studio ou na linha de comando usando as [etapas de instalação do pacote](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package) normais.</span><span class="sxs-lookup"><span data-stu-id="704e1-316">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

<span data-ttu-id="704e1-317">Para testes automatizados, o processo básico é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="704e1-317">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="704e1-318">Copie o arquivo `.nupkg` para uma pasta local.</span><span class="sxs-lookup"><span data-stu-id="704e1-318">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="704e1-319">Adicione a pasta às origens de pacote usando o comando `nuget sources add -name <name> -source <path>` (consulte [origens do nuget](../reference/cli-reference/cli-ref-sources.md)).</span><span class="sxs-lookup"><span data-stu-id="704e1-319">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../reference/cli-reference/cli-ref-sources.md)).</span></span> <span data-ttu-id="704e1-320">Observe que é preciso apenas configurar essa origem local uma vez em qualquer computador.</span><span class="sxs-lookup"><span data-stu-id="704e1-320">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="704e1-321">Instale o pacote da origem usando `nuget install <packageID> -source <name>` em que `<name>` corresponde ao nome de sua origem conforme fornecido para `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="704e1-321">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="704e1-322">Especificar a origem garante que o pacote seja instalado somente dela.</span><span class="sxs-lookup"><span data-stu-id="704e1-322">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="704e1-323">Examine seu sistema de arquivos para verificar se os arquivos estão instalados corretamente.</span><span class="sxs-lookup"><span data-stu-id="704e1-323">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="704e1-324">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="704e1-324">Next Steps</span></span>

<span data-ttu-id="704e1-325">Depois de criar um pacote, que é um arquivo `.nupkg`, você pode publicá-lo na galeria de sua escolha conforme descrito em [Publicar um pacote](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="704e1-325">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="704e1-326">Você também poderá estender os recursos do seu pacote ou dar suporte a outros cenários conforme descrito nos tópicos a seguir:</span><span class="sxs-lookup"><span data-stu-id="704e1-326">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="704e1-327">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="704e1-327">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="704e1-328">Suporte a várias estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="704e1-328">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="704e1-329">Transformações dos arquivos de configuração e de origem</span><span class="sxs-lookup"><span data-stu-id="704e1-329">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="704e1-330">Localização</span><span class="sxs-lookup"><span data-stu-id="704e1-330">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="704e1-331">Versões de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="704e1-331">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="704e1-332">Definir tipo de pacote</span><span class="sxs-lookup"><span data-stu-id="704e1-332">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="704e1-333">Criar pacotes com assemblies de interoperabilidade COM</span><span class="sxs-lookup"><span data-stu-id="704e1-333">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="704e1-334">Por fim, há tipos de pacote adicionais a serem considerados:</span><span class="sxs-lookup"><span data-stu-id="704e1-334">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="704e1-335">Pacotes nativos</span><span class="sxs-lookup"><span data-stu-id="704e1-335">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="704e1-336">Pacotes de símbolo</span><span class="sxs-lookup"><span data-stu-id="704e1-336">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
