---
title: Formatos de analisador de plataforma de compilador de .NET para NuGet
description: Convenções de analisadores do .NET que são empacotados e distribuídos com pacotes do NuGet que implementam uma API ou biblioteca.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0a8db9f6c55b7e79f9b338119e0b3ac6cb7a1e35
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324793"
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="fe364-103">Formatos de NuGet do Analisador</span><span class="sxs-lookup"><span data-stu-id="fe364-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="fe364-104">O .NET Compiler Platform (também conhecido como "Roslyn") permite que os desenvolvedores criem [analisadores](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) que examinam a árvore de sintaxe e semântica de código porque ele está sendo gravado.</span><span class="sxs-lookup"><span data-stu-id="fe364-104">The .NET Compiler Platform (also known as "Roslyn") allows developers to create [analyzers](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="fe364-105">Isso fornece aos desenvolvedores uma maneira de criar ferramentas de análise específica de domínio, como aquelas que ajudam a orientar o uso de uma determinada API ou biblioteca.</span><span class="sxs-lookup"><span data-stu-id="fe364-105">This provides developers with a way to create domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="fe364-106">Você pode encontrar mais informações no wiki do GitHub do [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki).</span><span class="sxs-lookup"><span data-stu-id="fe364-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="fe364-107">Consulte também o artigo [Use o Roslyn para escrever um analisador de código dinâmico para sua API](https://msdn.microsoft.com/magazine/dn879356.aspx) na MSDN Magazine.</span><span class="sxs-lookup"><span data-stu-id="fe364-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span></span>

<span data-ttu-id="fe364-108">Os próprios analisadores normalmente são empacotados e distribuídos como parte dos pacotes do NuGet que implementam a API ou a biblioteca em questão.</span><span class="sxs-lookup"><span data-stu-id="fe364-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="fe364-109">Para ver um bom exemplo, consulte o pacote [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers), que tem o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="fe364-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="fe364-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="fe364-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="fe364-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="fe364-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="fe364-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="fe364-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="fe364-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="fe364-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="fe364-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="fe364-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="fe364-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="fe364-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="fe364-116">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="fe364-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="fe364-117">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="fe364-117">tools\install.ps1</span></span>
- <span data-ttu-id="fe364-118">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="fe364-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="fe364-119">Como podemos ver, as DLLs do analisador são colocadas em uma pasta `analyzers` no pacote.</span><span class="sxs-lookup"><span data-stu-id="fe364-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="fe364-120">Arquivos de objetos, que são incluídos para desabilitar as regras FxCop herdadas em prol da implementação do analisador, são colocados na pasta `build`.</span><span class="sxs-lookup"><span data-stu-id="fe364-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="fe364-121">Instalar e desinstalar os scripts compatíveis com projetos que usam `packages.config` são colocados em `tools`.</span><span class="sxs-lookup"><span data-stu-id="fe364-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="fe364-122">Observe também que, como este pacote não tem nenhum requisito específico de plataforma, a pasta `platform` foi omitida.</span><span class="sxs-lookup"><span data-stu-id="fe364-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="fe364-123">Formato do caminho de analisadores</span><span class="sxs-lookup"><span data-stu-id="fe364-123">Analyzers path format</span></span>

<span data-ttu-id="fe364-124">O uso da pasta `analyzers` é semelhante àquela usada para [estruturas de destino](../create-packages/supporting-multiple-target-frameworks.md), exceto os especificadores no caminho descrevem as dependências do host de desenvolvimento em vez do tempo de build.</span><span class="sxs-lookup"><span data-stu-id="fe364-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="fe364-125">O formato geral é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fe364-125">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- <span data-ttu-id="fe364-126">**framework_name**: a área de superfície da API *opcional* do .NET Framework que as DLLs independentes precisam executar.</span><span class="sxs-lookup"><span data-stu-id="fe364-126">**framework_name**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="fe364-127">`dotnet` é atualmente o único valor válido porque Roslyn é o único host que pode executar analisadores.</span><span class="sxs-lookup"><span data-stu-id="fe364-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="fe364-128">Se nenhum destino for especificado, é considerado que as DLLs se aplicam a *todos* os destinos.</span><span class="sxs-lookup"><span data-stu-id="fe364-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="fe364-129">**supported_language**: o idioma ao qual a DLL se aplica, um dos `cs` (C#), `vb` (Visual Basic) e `fs` (F#).</span><span class="sxs-lookup"><span data-stu-id="fe364-129">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="fe364-130">O idioma indica que o analisador deve ser carregado apenas para um projeto usando o idioma.</span><span class="sxs-lookup"><span data-stu-id="fe364-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="fe364-131">Se nenhum idioma for especificado, a DLL será considerado como para aplicar a *todos os* linguagens que dão suporte a analisadores.</span><span class="sxs-lookup"><span data-stu-id="fe364-131">If no language is specified then the DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="fe364-132">**analyzer_name**: especifica as DLLs do analisador.</span><span class="sxs-lookup"><span data-stu-id="fe364-132">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="fe364-133">Se você precisar de arquivos adicionais além de DLLs, eles deverão ser incluídos por meio de arquivos de destinos ou de propriedades.</span><span class="sxs-lookup"><span data-stu-id="fe364-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="fe364-134">Scripts de instalação e desinstalação</span><span class="sxs-lookup"><span data-stu-id="fe364-134">Install and uninstall scripts</span></span>

<span data-ttu-id="fe364-135">Se estiver usando o projeto do usuário `packages.config`, o script MSBuild que seleciona o analisador não entra em ação, portanto, você deve colocar `install.ps1` e `uninstall.ps1` no `tools` pasta com o conteúdo que são descritos abaixo.</span><span class="sxs-lookup"><span data-stu-id="fe364-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should place `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="fe364-136">**Conteúdo do arquivo Install.ps1**</span><span class="sxs-lookup"><span data-stu-id="fe364-136">**install.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Install the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Install language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}
```


<span data-ttu-id="fe364-137">**Conteúdo do arquivo uninstall.ps1**</span><span class="sxs-lookup"><span data-stu-id="fe364-137">**uninstall.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                try
                {
                    $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
                }
                catch
                {

                }
            }
        }
    }
}
```
