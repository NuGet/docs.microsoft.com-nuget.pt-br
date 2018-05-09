---
title: Multiplataforma para pacotes do NuGet
description: Descrição dos diversos métodos para várias versões do .NET Framework de dentro de um único pacote do NuGet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 09/27/2017
ms.topic: conceptual
ms.openlocfilehash: d1a64c61954381b7ab3a7ecc8aa5a812cfa14e8b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="supporting-multiple-net-framework-versions"></a><span data-ttu-id="2fd1d-103">Suporte a várias versões do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="2fd1d-103">Supporting multiple .NET framework versions</span></span>

<span data-ttu-id="2fd1d-104">*Para projetos do .NET Core que usam o NuGet 4.0 ou superior, consulte [Empacotamento e restauração do NuGet como destinos do MSBuild](../reference/msbuild-targets.md) para ver detalhes sobre direcionamento cruzado.*</span><span class="sxs-lookup"><span data-stu-id="2fd1d-104">*For .NET Core projects using NuGet 4.0+, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) for details on cross-targeting.*</span></span>

<span data-ttu-id="2fd1d-105">Muitas bibliotecas se destinam a uma versão específica do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-105">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="2fd1d-106">Por exemplo, você pode ter uma versão da biblioteca específica para a UWP e outra versão para aproveitar os recursos no .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-106">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span>

<span data-ttu-id="2fd1d-107">Para acomodar a isso, o NuGet é compatível com a colocação de várias versões na mesma biblioteca em um único pacote ao usar o método de diretório de trabalho baseado em convenção descrito em [Criando um pacote](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="2fd1d-107">To accommodate this, NuGet supports putting multiple versions of the same library in a single package when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="2fd1d-108">Estrutura da pasta de versão do Framework</span><span class="sxs-lookup"><span data-stu-id="2fd1d-108">Framework version folder structure</span></span>

<span data-ttu-id="2fd1d-109">Ao compilar um pacote que contém somente uma versão de uma biblioteca ou destinado a várias estruturas, sempre crie as subpastas em `lib` usando nomes de estrutura que diferenciam maiúsculas de minúsculas com a seguinte convenção:</span><span class="sxs-lookup"><span data-stu-id="2fd1d-109">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="2fd1d-110">Para ver uma lista completa de nomes compatíveis, consulte a [Referência a Estruturas de Destino](../reference/target-frameworks.md#supported-frameworks).</span><span class="sxs-lookup"><span data-stu-id="2fd1d-110">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="2fd1d-111">Você nunca deve ter uma versão da biblioteca que não seja específico para uma estrutura e colocada diretamente na pasta `lib` raiz.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-111">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="2fd1d-112">(Essa capacidade era compatível somente com `packages.config`).</span><span class="sxs-lookup"><span data-stu-id="2fd1d-112">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="2fd1d-113">Isso o tornaria compatível com qualquer estrutura de destino e permitiria que ele seja instalado em qualquer lugar, provavelmente resultando em erros de tempo de execução inesperados.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-113">Doing so would make the compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="2fd1d-114">A adição de assemblies à pasta raiz (como `lib\abc.dll`) ou subpastas (como `lib\abc\abc.dll`) foi preterida e será ignorada ao usar o formato de PackagesReference.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-114">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="2fd1d-115">Por exemplo, a seguinte estrutura de pastas a seguir é compatível com quatro versões de um assembly que são específicas da estrutura:</span><span class="sxs-lookup"><span data-stu-id="2fd1d-115">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="2fd1d-116">Para incluir facilmente todos esses arquivos ao criar o pacote, use um curinga `**` recursivo na seção `<files>` do seu `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="2fd1d-116">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="2fd1d-117">Pastas específicas de arquitetura</span><span class="sxs-lookup"><span data-stu-id="2fd1d-117">Architecture-specific folders</span></span>

<span data-ttu-id="2fd1d-118">Se você tiver assemblies específicos de arquitetura, ou seja, assemblies separados destinados ao ARM, x86 e x64, será preciso colocá-los em uma pasta chamada `runtimes` dentro de subpastas denominadas `{platform}-{architecture}\lib\{framework}` ou `{platform}-{architecture}\native`.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-118">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="2fd1d-119">Por exemplo, a seguinte estrutura de pasta acomodaria DLLs nativos e gerenciados direcionados para o Windows 10 e a estrutura `uap10.0`:</span><span class="sxs-lookup"><span data-stu-id="2fd1d-119">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="2fd1d-120">Consulte [Criar pacotes de UWP](../guides/create-uwp-packages.md) para obter um exemplo de referência a esses arquivos no manifesto `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-120">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="2fd1d-121">Correspondendo versões de assembly e a estrutura de destino em um projeto</span><span class="sxs-lookup"><span data-stu-id="2fd1d-121">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="2fd1d-122">Quando o NuGet instala um pacote que tem várias versões de assembly, ele tenta corresponder o nome da estrutura do assembly com a estrutura de destino do projeto.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-122">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="2fd1d-123">Se nenhuma correspondência for encontrada, o NuGet copia o assembly para a versão mais recente que seja menor ou igual à estrutura de destino do projeto, se disponível.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-123">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="2fd1d-124">Se nenhum assembly compatível for localizado, o NuGet retornará uma mensagem de erro apropriado.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-124">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="2fd1d-125">Considere, por exemplo, a estrutura de pastas a seguir em um pacote:</span><span class="sxs-lookup"><span data-stu-id="2fd1d-125">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="2fd1d-126">Ao instalar esse pacote em um projeto voltado para o .NET Framework 4.6, o NuGet instala o assembly na pasta `net45`, pois é a versão mais recente disponível que é menor ou igual a 4.6.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-126">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="2fd1d-127">Se o projeto se destina ao .NET Framework 4.6.1, por outro lado, o NuGet instala o assembly na pasta `net461`.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-127">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="2fd1d-128">Se o projeto se destina ao .NET framework 4.0 e versões anterior, o NuGet gera uma mensagem de erro apropriada por não encontrar o assembly compatível.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-128">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="2fd1d-129">Agrupando assemblies por versão de estrutura</span><span class="sxs-lookup"><span data-stu-id="2fd1d-129">Grouping assemblies by framework version</span></span>

<span data-ttu-id="2fd1d-130">O NuGet copia assemblies apenas de uma única pasta de biblioteca no pacote.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-130">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="2fd1d-131">Suponha, por exemplo, que um pacote tem a seguinte estrutura de pastas:</span><span class="sxs-lookup"><span data-stu-id="2fd1d-131">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="2fd1d-132">Quando o pacote é instalado em um projeto voltado para o .NET Framework 4.5, `MyAssembly.dll` (v2.0) é o único assembly instalado.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-132">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="2fd1d-133">`MyAssembly.Core.dll` (v1.0) não está instalado, porque ele não está listado na pasta `net45`.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-133">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="2fd1d-134">O NuGet se comporta dessa maneira porque `MyAssembly.Core.dll` pode ter sido mesclado na versão 2.0 do `MyAssembly.dll`.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-134">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="2fd1d-135">Se você quiser que `MyAssembly.Core.dll` seja instalado para o .NET Framework 4.5, coloque uma cópia na pasta `net45`.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-135">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="2fd1d-136">Agrupando assemblies por perfil de estrutura</span><span class="sxs-lookup"><span data-stu-id="2fd1d-136">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="2fd1d-137">O NuGet também dá suporte ao direcionamento a um perfil de estrutura específico acrescentando um traço e o nome do perfil ao fim da pasta.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-137">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="2fd1d-138">Os perfis compatíveis são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="2fd1d-138">The supported profiles are as follows:</span></span>

- <span data-ttu-id="2fd1d-139">`client`: Perfil do cliente</span><span class="sxs-lookup"><span data-stu-id="2fd1d-139">`client`: Client Profile</span></span>
- <span data-ttu-id="2fd1d-140">`full`: Perfil completo</span><span class="sxs-lookup"><span data-stu-id="2fd1d-140">`full`: Full Profile</span></span>
- <span data-ttu-id="2fd1d-141">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="2fd1d-141">`wp`: Windows Phone</span></span>
- <span data-ttu-id="2fd1d-142">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="2fd1d-142">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="2fd1d-143">Determinar qual destino do NuGet deve ser usado</span><span class="sxs-lookup"><span data-stu-id="2fd1d-143">Determining which NuGet target to use</span></span>

<span data-ttu-id="2fd1d-144">Quando pacotes de bibliotecas são direcionados à Biblioteca de Classes Portátil, pode ser difícil determinar qual destino NuGet deve ser usado nos nomes de pastas e no arquivo `.nuspec`, especialmente se o direcionamento for apenas de um subconjunto do PCL.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-144">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="2fd1d-145">Os seguintes recursos externos ajudarão você com isso:</span><span class="sxs-lookup"><span data-stu-id="2fd1d-145">The following external resources will help you with this:</span></span>

- <span data-ttu-id="2fd1d-146">[Perfis do Frameworks no .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="2fd1d-146">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span></span>
- <span data-ttu-id="2fd1d-147">[Perfis de Biblioteca de Classes Portátil](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): tabela que enumera os perfis de PCL e suas metas equivalentes do NuGet</span><span class="sxs-lookup"><span data-stu-id="2fd1d-147">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="2fd1d-148">[Ferramenta de perfis da Biblioteca de Classes Portátil](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): ferramenta de linha de comando para determinar perfis de PCL disponíveis no sistema</span><span class="sxs-lookup"><span data-stu-id="2fd1d-148">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="2fd1d-149">Arquivos de conteúdo e scripts do PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fd1d-149">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="2fd1d-150">Arquivos de conteúdo mutáveis e a execução de script estão disponíveis somente no formato `packages.config`; eles são preteridos com todos os outros formatos e não deve ser usado para nenhum pacote novo.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-150">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="2fd1d-151">Com `packages.config`, arquivos de conteúdo e scripts do PowerShell podem ser agrupados pela estrutura de destino usando a mesma convenção de pasta dentro das pastas `content` e `tools`.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-151">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="2fd1d-152">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2fd1d-152">For example:</span></span>

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

<span data-ttu-id="2fd1d-153">Se uma pasta da estrutura for deixada vazia, o NuGet não adiciona referência de assembly ou arquivos de conteúdo, nem executam os scripts do PowerShell para essa estrutura.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-153">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="2fd1d-154">Como `init.ps1` é executado no nível da solução e não depende do projeto, ele precisa ser colocado diretamente na pasta `tools`.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-154">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="2fd1d-155">Será ignorado se colocado em uma pasta da estrutura.</span><span class="sxs-lookup"><span data-stu-id="2fd1d-155">It's ignored if placed under a framework folder.</span></span>
