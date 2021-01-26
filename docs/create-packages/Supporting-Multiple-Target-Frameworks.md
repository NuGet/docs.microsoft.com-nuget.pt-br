---
title: Multiplataforma para pacotes do NuGet
description: Descrição dos diversos métodos para várias versões do .NET Framework de dentro de um único pacote do NuGet.
author: JonDouglas
ms.author: jodou
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: e919b11670589900d9e588db33fd68b8df592ac2
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774556"
---
# <a name="support-multiple-net-versions"></a><span data-ttu-id="e992f-103">Suporte a várias versões do .NET</span><span class="sxs-lookup"><span data-stu-id="e992f-103">Support multiple .NET versions</span></span>

<span data-ttu-id="e992f-104">Muitas bibliotecas se destinam a uma versão específica do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="e992f-104">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="e992f-105">Por exemplo, você pode ter uma versão da biblioteca específica para a UWP e outra versão para aproveitar os recursos no .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="e992f-105">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span> <span data-ttu-id="e992f-106">Para acomodar isso, o NuGet é compatível com a colocação de várias versões da mesma biblioteca em um único pacote.</span><span class="sxs-lookup"><span data-stu-id="e992f-106">To accommodate this, NuGet supports putting multiple versions of the same library in a single package.</span></span>

<span data-ttu-id="e992f-107">Este artigo descreve o layout de um pacote NuGet, independentemente de como o pacote ou os assemblies são compilados (ou seja, o layout é o mesmo se você estiver usando vários arquivos *. csproj* de estilo não SDK e um arquivo *. nuspec* personalizado, ou um único SDK multiplataforma-Style *. csproj*).</span><span class="sxs-lookup"><span data-stu-id="e992f-107">This article describes the layout of a NuGet package, regardless of how the package or assemblies are built (that is, the layout is the same whether using multiple non-SDK-style *.csproj* files and a custom *.nuspec* file, or a single multi-targeted SDK-style *.csproj*).</span></span> <span data-ttu-id="e992f-108">Para um projeto no estilo SDK, os [destinos do pacote](../reference/msbuild-targets.md) do NuGet reconhecem como o pacote deve ser definido e automatiza a colocação dos assemblies nas pastas corretas da biblioteca e a criação de grupos de dependências para cada estrutura de destino (TFM).</span><span class="sxs-lookup"><span data-stu-id="e992f-108">For an SDK-style project, NuGet [pack targets](../reference/msbuild-targets.md) knows how the package must be layed out and automates putting the assemblies in the correct lib folders and creating dependency groups for each target framework (TFM).</span></span> <span data-ttu-id="e992f-109">Para saber mais, confira [Suporte a várias versões de .NET Framework em seu arquivo de projeto](multiple-target-frameworks-project-file.md).</span><span class="sxs-lookup"><span data-stu-id="e992f-109">For detailed instructions, see [Support multiple .NET Framework versions in your project file](multiple-target-frameworks-project-file.md).</span></span>

<span data-ttu-id="e992f-110">Você deve definir manualmente o pacote conforme descrito neste artigo ao usar o método de diretório de trabalho baseado em convenções descrito em [Criar um pacote](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="e992f-110">You must manually lay out the package as described in this article when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> <span data-ttu-id="e992f-111">Para um projeto em estilo SDK, é recomendado o método automatizado, mas você também pode optar por definir manualmente o pacote como descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="e992f-111">For an SDK-style project, the automated method is recommended, but you may also choose to manually lay out the package as described in this article.</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="e992f-112">Estrutura da pasta de versão do Framework</span><span class="sxs-lookup"><span data-stu-id="e992f-112">Framework version folder structure</span></span>

<span data-ttu-id="e992f-113">Ao compilar um pacote que contém somente uma versão de uma biblioteca ou destinado a várias estruturas, sempre crie as subpastas em `lib` usando nomes de estrutura que diferenciam maiúsculas de minúsculas com a seguinte convenção:</span><span class="sxs-lookup"><span data-stu-id="e992f-113">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

```
lib\{framework name}[{version}]
```

<span data-ttu-id="e992f-114">Para ver uma lista completa de nomes compatíveis, consulte a [Referência a Estruturas de Destino](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="e992f-114">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="e992f-115">Você nunca deve ter uma versão da biblioteca que não seja específico para uma estrutura e colocada diretamente na pasta `lib` raiz.</span><span class="sxs-lookup"><span data-stu-id="e992f-115">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="e992f-116">(Essa capacidade era compatível somente com `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="e992f-116">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="e992f-117">Isso tornaria a biblioteca compatível com qualquer estrutura de destino e permitiria que ela fosse instalada em qualquer lugar, provavelmente resultando em erros de runtime inesperados.</span><span class="sxs-lookup"><span data-stu-id="e992f-117">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="e992f-118">A adição de assemblies à pasta raiz (como `lib\abc.dll`) ou subpastas (como `lib\abc\abc.dll`) foi preterida e será ignorada ao usar o formato de PackagesReference.</span><span class="sxs-lookup"><span data-stu-id="e992f-118">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="e992f-119">Por exemplo, a seguinte estrutura de pastas a seguir é compatível com quatro versões de um assembly que são específicas da estrutura:</span><span class="sxs-lookup"><span data-stu-id="e992f-119">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

```
\lib
    \net46
        \MyAssembly.dll
    \net461
        \MyAssembly.dll
    \uap
        \MyAssembly.dll
    \netcore
        \MyAssembly.dll
```

<span data-ttu-id="e992f-120">Para incluir facilmente todos esses arquivos ao criar o pacote, use um curinga `**` recursivo na seção `<files>` do seu `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="e992f-120">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="e992f-121">Pastas específicas de arquitetura</span><span class="sxs-lookup"><span data-stu-id="e992f-121">Architecture-specific folders</span></span>

<span data-ttu-id="e992f-122">Se você tiver assemblies específicos de arquitetura, ou seja, assemblies separados destinados ao ARM, x86 e x64, será preciso colocá-los em uma pasta chamada `runtimes` dentro de subpastas denominadas `{platform}-{architecture}\lib\{framework}` ou `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="e992f-122">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="e992f-123">Por exemplo, a seguinte estrutura de pasta acomodaria DLLs nativos e gerenciados direcionados para o Windows 10 e a estrutura `uap10.0`:</span><span class="sxs-lookup"><span data-stu-id="e992f-123">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

```
\runtimes
    \win10-arm
        \native
        \lib\uap10.0
    \win10-x86
        \native
        \lib\uap10.0
    \win10-x64
        \native
        \lib\uap10.0
```

<span data-ttu-id="e992f-124">Esses assemblies só estarão disponíveis no runtime, portanto, se você quiser fornecer o assembly de tempo de compilação correspondente, também terá um assembly `AnyCPU` na pasta `/ref/{tfm}`.</span><span class="sxs-lookup"><span data-stu-id="e992f-124">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref/{tfm}` folder.</span></span> 

<span data-ttu-id="e992f-125">O NuGet sempre escolhe esses recursos de compilação ou de runtime de uma pasta, portanto, se houver alguns ativos compatíveis de `/ref`, `/lib` será ignorado para adicionar conjuntos de tempo de compilação.</span><span class="sxs-lookup"><span data-stu-id="e992f-125">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="e992f-126">Da mesma forma, se houver alguns ativos compatíveis `/runtimes` , também `/lib` serão ignorados para tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="e992f-126">Similarly, if there are some compatible assets from `/runtimes` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="e992f-127">Consulte [Criar pacotes de UWP](../guides/create-uwp-packages.md) para obter um exemplo de referência a esses arquivos no manifesto `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="e992f-127">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="e992f-128">Confira também [Como empacotar um componente de aplicativo da Windows Store com o NuGet](/archive/blogs/mim/packaging-a-windows-store-apps-component-with-nuget-part-2)</span><span class="sxs-lookup"><span data-stu-id="e992f-128">Also, see [Packing a Windows store app component with NuGet](/archive/blogs/mim/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="e992f-129">Correspondendo versões de assembly e a estrutura de destino em um projeto</span><span class="sxs-lookup"><span data-stu-id="e992f-129">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="e992f-130">Quando o NuGet instala um pacote que tem várias versões de assembly, ele tenta corresponder o nome da estrutura do assembly com a estrutura de destino do projeto.</span><span class="sxs-lookup"><span data-stu-id="e992f-130">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="e992f-131">Se nenhuma correspondência for encontrada, o NuGet copia o assembly para a versão mais recente que seja menor ou igual à estrutura de destino do projeto, se disponível.</span><span class="sxs-lookup"><span data-stu-id="e992f-131">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="e992f-132">Se nenhum assembly compatível for localizado, o NuGet retornará uma mensagem de erro apropriado.</span><span class="sxs-lookup"><span data-stu-id="e992f-132">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="e992f-133">Considere, por exemplo, a estrutura de pastas a seguir em um pacote:</span><span class="sxs-lookup"><span data-stu-id="e992f-133">For example, consider the following folder structure in a package:</span></span>

```
\lib
    \net45
        \MyAssembly.dll
    \net461
        \MyAssembly.dll
```

<span data-ttu-id="e992f-134">Ao instalar esse pacote em um projeto voltado para o .NET Framework 4.6, o NuGet instala o assembly na pasta `net45`, pois é a versão mais recente disponível que é menor ou igual a 4.6.</span><span class="sxs-lookup"><span data-stu-id="e992f-134">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="e992f-135">Se o projeto se destina ao .NET Framework 4.6.1, por outro lado, o NuGet instala o assembly na pasta `net461`.</span><span class="sxs-lookup"><span data-stu-id="e992f-135">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="e992f-136">Se o projeto se destina ao .NET framework 4.0 e versões anterior, o NuGet gera uma mensagem de erro apropriada por não encontrar o assembly compatível.</span><span class="sxs-lookup"><span data-stu-id="e992f-136">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="e992f-137">Agrupando assemblies por versão de estrutura</span><span class="sxs-lookup"><span data-stu-id="e992f-137">Grouping assemblies by framework version</span></span>

<span data-ttu-id="e992f-138">O NuGet copia assemblies apenas de uma única pasta de biblioteca no pacote.</span><span class="sxs-lookup"><span data-stu-id="e992f-138">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="e992f-139">Suponha, por exemplo, que um pacote tem a seguinte estrutura de pastas:</span><span class="sxs-lookup"><span data-stu-id="e992f-139">For example, suppose a package has the following folder structure:</span></span>

```
\lib
    \net40
        \MyAssembly.dll (v1.0)
        \MyAssembly.Core.dll (v1.0)
    \net45
        \MyAssembly.dll (v2.0)
```

<span data-ttu-id="e992f-140">Quando o pacote é instalado em um projeto voltado para o .NET Framework 4.5, `MyAssembly.dll` (v2.0) é o único assembly instalado.</span><span class="sxs-lookup"><span data-stu-id="e992f-140">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="e992f-141">`MyAssembly.Core.dll` (v1.0) não está instalado, porque ele não está listado na pasta `net45`.</span><span class="sxs-lookup"><span data-stu-id="e992f-141">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="e992f-142">O NuGet se comporta dessa maneira porque `MyAssembly.Core.dll` pode ter sido mesclado na versão 2.0 do `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="e992f-142">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="e992f-143">Se você quiser que `MyAssembly.Core.dll` seja instalado para o .NET Framework 4.5, coloque uma cópia na pasta `net45`.</span><span class="sxs-lookup"><span data-stu-id="e992f-143">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="e992f-144">Agrupando assemblies por perfil de estrutura</span><span class="sxs-lookup"><span data-stu-id="e992f-144">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="e992f-145">O NuGet também dá suporte ao direcionamento a um perfil de estrutura específico acrescentando um traço e o nome do perfil ao fim da pasta.</span><span class="sxs-lookup"><span data-stu-id="e992f-145">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

<span data-ttu-id="e992f-146">\{nome da estrutura lib}-{perfil}</span><span class="sxs-lookup"><span data-stu-id="e992f-146">lib\{framework name}-{profile}</span></span>

<span data-ttu-id="e992f-147">Os perfis compatíveis são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="e992f-147">The supported profiles are as follows:</span></span>

- <span data-ttu-id="e992f-148">`client`: Perfil do cliente</span><span class="sxs-lookup"><span data-stu-id="e992f-148">`client`: Client Profile</span></span>
- <span data-ttu-id="e992f-149">`full`: Perfil completo</span><span class="sxs-lookup"><span data-stu-id="e992f-149">`full`: Full Profile</span></span>
- <span data-ttu-id="e992f-150">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="e992f-150">`wp`: Windows Phone</span></span>
- <span data-ttu-id="e992f-151">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="e992f-151">`cf`: Compact Framework</span></span>

## <a name="declaring-dependencies-advanced"></a><span data-ttu-id="e992f-152">Declarar dependências (Avançado)</span><span class="sxs-lookup"><span data-stu-id="e992f-152">Declaring dependencies (Advanced)</span></span>

<span data-ttu-id="e992f-153">Ao empacotar um arquivo de projeto, o NuGet tenta gerar automaticamente as dependências do projeto.</span><span class="sxs-lookup"><span data-stu-id="e992f-153">When packing a project file, NuGet tries to automatically generate the dependencies from the project.</span></span> <span data-ttu-id="e992f-154">As informações nesta seção sobre como usar um arquivo *.nuspec* para declarar as dependências normalmente são necessárias apenas em cenários avançados.</span><span class="sxs-lookup"><span data-stu-id="e992f-154">The information in this section about using a *.nuspec* file to declare dependencies is typically necessary for advanced scenarios only.</span></span>

<span data-ttu-id="e992f-155">*(Versão 2.0+)* Você pode declarar as dependências de pacote no *.nuspec* correspondente à estrutura do projeto de destino usando elementos `<group>` no elemento `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="e992f-155">*(Version 2.0+)* You can declare package dependencies in the *.nuspec* corresponding to the target framework of the target project using `<group>` elements within the `<dependencies>` element.</span></span> <span data-ttu-id="e992f-156">Para saber mais, confira [elemento dependencies](../reference/nuspec.md#dependencies-element).</span><span class="sxs-lookup"><span data-stu-id="e992f-156">For more information, see [dependencies element](../reference/nuspec.md#dependencies-element).</span></span>

<span data-ttu-id="e992f-157">Cada grupo tem um atributo chamado `targetFramework` e contém zero ou mais elementos `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="e992f-157">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="e992f-158">Essas referências são instaladas juntas quando a estrutura de destino é compatível com o perfil da estrutura do projeto.</span><span class="sxs-lookup"><span data-stu-id="e992f-158">Those dependencies are installed together when the target framework is compatible with the project's framework profile.</span></span> <span data-ttu-id="e992f-159">Consulte [Estruturas de destino](../reference/target-frameworks.md) para ver os identificadores de estrutura exatos.</span><span class="sxs-lookup"><span data-stu-id="e992f-159">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

<span data-ttu-id="e992f-160">Recomendamos usar um grupo por TFM (Moniker da Estrutura de Destino) para arquivos nas pastas *lib/* e *ref/*.</span><span class="sxs-lookup"><span data-stu-id="e992f-160">We recommend using one group per Target Framework Moniker (TFM) for files in the *lib/* and *ref/* folders.</span></span>

<span data-ttu-id="e992f-161">O exemplo a seguir mostra diferentes variações do elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="e992f-161">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>

    <group targetFramework="net472">
        <dependency id="jQuery" version="1.10.2" />
        <dependency id="WebActivatorEx" version="2.2.0" />
    </group>

    <group targetFramework="net20">
    </group>

</dependencies>
```

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="e992f-162">Determinar qual destino do NuGet deve ser usado</span><span class="sxs-lookup"><span data-stu-id="e992f-162">Determining which NuGet target to use</span></span>

<span data-ttu-id="e992f-163">Quando pacotes de bibliotecas são direcionados à Biblioteca de Classes Portátil, pode ser difícil determinar qual destino NuGet deve ser usado nos nomes de pastas e no arquivo `.nuspec`, especialmente se o direcionamento for apenas de um subconjunto do PCL.</span><span class="sxs-lookup"><span data-stu-id="e992f-163">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="e992f-164">Os seguintes recursos externos ajudarão você com isso:</span><span class="sxs-lookup"><span data-stu-id="e992f-164">The following external resources will help you with this:</span></span>

- <span data-ttu-id="e992f-165">[Perfis de Framework no .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span><span class="sxs-lookup"><span data-stu-id="e992f-165">[Framework profiles in .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span></span>
- <span data-ttu-id="e992f-166">[Perfis de Biblioteca de Classes Portátil](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): tabela que enumera os perfis de PCL e suas metas equivalentes do NuGet</span><span class="sxs-lookup"><span data-stu-id="e992f-166">[Portable Class Library profiles](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="e992f-167">[Ferramenta de perfis da Biblioteca de Classes Portátil](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): ferramenta de linha de comando para determinar perfis de PCL disponíveis no sistema</span><span class="sxs-lookup"><span data-stu-id="e992f-167">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="e992f-168">Arquivos de conteúdo e scripts do PowerShell</span><span class="sxs-lookup"><span data-stu-id="e992f-168">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="e992f-169">Arquivos de conteúdo mutáveis e a execução de script estão disponíveis somente no formato `packages.config`; eles são preteridos com todos os outros formatos e não deve ser usado para nenhum pacote novo.</span><span class="sxs-lookup"><span data-stu-id="e992f-169">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="e992f-170">Com `packages.config`, arquivos de conteúdo e scripts do PowerShell podem ser agrupados pela estrutura de destino usando a mesma convenção de pasta dentro das pastas `content` e `tools`.</span><span class="sxs-lookup"><span data-stu-id="e992f-170">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="e992f-171">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e992f-171">For example:</span></span>

```
\content
    \net46
        \MyContent.txt
    \net461
        \MyContent461.txt
    \uap
        \MyUWPContent.html
    \netcore
\tools
    init.ps1
    \net46
        install.ps1
        uninstall.ps1
    \uap
        install.ps1
        uninstall.ps1
```

<span data-ttu-id="e992f-172">Se uma pasta da estrutura for deixada vazia, o NuGet não adiciona referência de assembly ou arquivos de conteúdo, nem executam os scripts do PowerShell para essa estrutura.</span><span class="sxs-lookup"><span data-stu-id="e992f-172">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="e992f-173">Como `init.ps1` é executado no nível da solução e não depende do projeto, ele precisa ser colocado diretamente na pasta `tools`.</span><span class="sxs-lookup"><span data-stu-id="e992f-173">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="e992f-174">Será ignorado se colocado em uma pasta da estrutura.</span><span class="sxs-lookup"><span data-stu-id="e992f-174">It's ignored if placed under a framework folder.</span></span>