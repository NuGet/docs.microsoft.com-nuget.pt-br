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
# <a name="analyzer-nuget-formats"></a>Formatos de NuGet do Analisador

O .NET Compiler Platform (também conhecido como "Roslyn") permite que os desenvolvedores criem [analisadores](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) que examinam a árvore de sintaxe e semântica de código porque ele está sendo gravado. Isso fornece aos desenvolvedores uma maneira de criar ferramentas de análise específica de domínio, como aquelas que ajudam a orientar o uso de uma determinada API ou biblioteca. Você pode encontrar mais informações no wiki do GitHub do [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki). Consulte também o artigo [Use o Roslyn para escrever um analisador de código dinâmico para sua API](https://msdn.microsoft.com/magazine/dn879356.aspx) na MSDN Magazine.

Os próprios analisadores normalmente são empacotados e distribuídos como parte dos pacotes do NuGet que implementam a API ou a biblioteca em questão.

Para ver um bom exemplo, consulte o pacote [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers), que tem o seguinte conteúdo:

- analyzers\dotnet\System.Runtime.Analyzers.dll
- analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- tools\install.ps1
- tools\uninstall.ps1

Como podemos ver, as DLLs do analisador são colocadas em uma pasta `analyzers` no pacote.

Arquivos de objetos, que são incluídos para desabilitar as regras FxCop herdadas em prol da implementação do analisador, são colocados na pasta `build`.

Instalar e desinstalar os scripts compatíveis com projetos que usam `packages.config` são colocados em `tools`.

Observe também que, como este pacote não tem nenhum requisito específico de plataforma, a pasta `platform` foi omitida.


## <a name="analyzers-path-format"></a>Formato do caminho de analisadores

O uso da pasta `analyzers` é semelhante àquela usada para [estruturas de destino](../create-packages/supporting-multiple-target-frameworks.md), exceto os especificadores no caminho descrevem as dependências do host de desenvolvimento em vez do tempo de build. O formato geral é o seguinte:

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- **framework_name**: a área de superfície da API *opcional* do .NET Framework que as DLLs independentes precisam executar. `dotnet` é atualmente o único valor válido porque Roslyn é o único host que pode executar analisadores. Se nenhum destino for especificado, é considerado que as DLLs se aplicam a *todos* os destinos.
- **supported_language**: o idioma ao qual a DLL se aplica, um dos `cs` (C#), `vb` (Visual Basic) e `fs` (F#). O idioma indica que o analisador deve ser carregado apenas para um projeto usando o idioma. Se nenhum idioma for especificado, a DLL será considerado como para aplicar a *todos os* linguagens que dão suporte a analisadores.
- **analyzer_name**: especifica as DLLs do analisador. Se você precisar de arquivos adicionais além de DLLs, eles deverão ser incluídos por meio de arquivos de destinos ou de propriedades.


## <a name="install-and-uninstall-scripts"></a>Scripts de instalação e desinstalação

Se estiver usando o projeto do usuário `packages.config`, o script MSBuild que seleciona o analisador não entra em ação, portanto, você deve colocar `install.ps1` e `uninstall.ps1` no `tools` pasta com o conteúdo que são descritos abaixo.

**Conteúdo do arquivo Install.ps1**

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


**Conteúdo do arquivo uninstall.ps1**

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
