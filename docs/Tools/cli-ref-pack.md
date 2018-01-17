---
title: Comando de pacote do NuGet CLI | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 55e9e4d2-8039-4e9b-bdd9-c8b3eb0e894b
description: "Referência para o comando de pacote nuget.exe"
keywords: "referência de pacote do NuGet, o comando de pacote"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0dbecb8f01acf781ab8d2e77e8df7fa405f74cf1
ms.sourcegitcommit: d576d84fb4b6a178eb2ac11f55deb08ac771ba1c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2018
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="84767-104">comando de pacote NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="84767-104">pack command (NuGet CLI)</span></span>

<span data-ttu-id="84767-105">**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="84767-105">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="84767-106">Cria um pacote do NuGet com base em especificado `.nuspec` ou arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="84767-106">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="84767-107">O `dotnet pack` comando (consulte [comandos dotnet](dotnet-Commands.md)) e `msbuild /t:pack` (consulte [destinos do MSBuild](../schema/msbuild-targets.md)) podem ser usadas como alternativas.</span><span class="sxs-lookup"><span data-stu-id="84767-107">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../schema/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="84767-108">Em Mono, criando um pacote de um arquivo de projeto não é suportado.</span><span class="sxs-lookup"><span data-stu-id="84767-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="84767-109">Você também precisa ajustar caminhos de local não o `.nuspec` de arquivos para caminhos no estilo Unix, como nuget.exe não converte nomes de caminho do Windows em si.</span><span class="sxs-lookup"><span data-stu-id="84767-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="84767-110">Uso</span><span class="sxs-lookup"><span data-stu-id="84767-110">Usage</span></span>

```
nuget pack <nuspecPath | projectPath> [options]
```

<span data-ttu-id="84767-111">onde `<nuspecPath>` e `<projectPath>` especificar o `.nuspec` ou projeto de arquivo, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="84767-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="84767-112">Opções</span><span class="sxs-lookup"><span data-stu-id="84767-112">Options</span></span>

| <span data-ttu-id="84767-113">Opção</span><span class="sxs-lookup"><span data-stu-id="84767-113">Option</span></span> | <span data-ttu-id="84767-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="84767-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="84767-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="84767-115">BasePath</span></span> | <span data-ttu-id="84767-116">Define o caminho base dos arquivos definidos no `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="84767-116">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="84767-117">Build</span><span class="sxs-lookup"><span data-stu-id="84767-117">Build</span></span> | <span data-ttu-id="84767-118">Especifica que o projeto deve ser criado antes de criar o pacote.</span><span class="sxs-lookup"><span data-stu-id="84767-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="84767-119">Excluir</span><span class="sxs-lookup"><span data-stu-id="84767-119">Exclude</span></span> | <span data-ttu-id="84767-120">Especifica um ou mais padrões de curinga para excluir ao criar um pacote.</span><span class="sxs-lookup"><span data-stu-id="84767-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="84767-121">Para especificar mais de um padrão, repita-sinalizador de exclusão.</span><span class="sxs-lookup"><span data-stu-id="84767-121">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="84767-122">Consulte o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="84767-122">See example below.</span></span> |
| <span data-ttu-id="84767-123">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="84767-123">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="84767-124">Impede a inclusão de diretórios vazios ao criar o pacote.</span><span class="sxs-lookup"><span data-stu-id="84767-124">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="84767-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="84767-125">ForceEnglishOutput</span></span> | <span data-ttu-id="84767-126">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="84767-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="84767-127">Ajuda</span><span class="sxs-lookup"><span data-stu-id="84767-127">Help</span></span> | <span data-ttu-id="84767-128">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="84767-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="84767-129">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="84767-129">IncludeReferencedProjects</span></span> | <span data-ttu-id="84767-130">Indica que o pacote criado deve incluir projetos referenciados como dependências ou como parte do pacote.</span><span class="sxs-lookup"><span data-stu-id="84767-130">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="84767-131">Se um projeto referenciado tem um correspondente `.nuspec` arquivo que tem o mesmo nome do projeto, em seguida, o projeto referenciado será adicionado como uma dependência.</span><span class="sxs-lookup"><span data-stu-id="84767-131">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="84767-132">Caso contrário, o projeto referenciado é adicionado como parte do pacote.</span><span class="sxs-lookup"><span data-stu-id="84767-132">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="84767-133">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="84767-133">MinClientVersion</span></span> | <span data-ttu-id="84767-134">Definir o *minClientVersion* atributo para o pacote criado.</span><span class="sxs-lookup"><span data-stu-id="84767-134">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="84767-135">Esse valor substituirá o valor existente *minClientVersion* atributo (se houver) no `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="84767-135">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="84767-136">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="84767-136">MSBuildPath</span></span> | <span data-ttu-id="84767-137">*(4.0 +)*  Especifica o caminho do MSBuild para usar com o comando tendo precedência sobre `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="84767-137">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="84767-138">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="84767-138">MSBuildVersion</span></span> | <span data-ttu-id="84767-139">*(3.2 +)*  Especifica a versão do MSBuild a ser usado com este comando.</span><span class="sxs-lookup"><span data-stu-id="84767-139">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="84767-140">Valores com suporte são 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="84767-140">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="84767-141">Por padrão que o MSBuild em seu caminho é separado, caso contrário, o padrão é a versão mais recente instalada do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="84767-141">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="84767-142">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="84767-142">NoDefaultExcludes</span></span> | <span data-ttu-id="84767-143">Impede a exclusão padrão do NuGet compactar arquivos e arquivos e pastas que iniciam com um ponto, como `.svn` e `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="84767-143">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="84767-144">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="84767-144">NoPackageAnalysis</span></span> | <span data-ttu-id="84767-145">Especifica que o pacote não deve executar a análise de pacote após a compilação do pacote.</span><span class="sxs-lookup"><span data-stu-id="84767-145">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="84767-146">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="84767-146">OutputDirectory</span></span> | <span data-ttu-id="84767-147">Especifica a pasta na qual o pacote criado é armazenado.</span><span class="sxs-lookup"><span data-stu-id="84767-147">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="84767-148">Se nenhuma pasta for especificada, a pasta atual será usada.</span><span class="sxs-lookup"><span data-stu-id="84767-148">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="84767-149">Propriedades</span><span class="sxs-lookup"><span data-stu-id="84767-149">Properties</span></span> | <span data-ttu-id="84767-150">Especifica uma lista de propriedades que substituem os valores no arquivo de projeto; consulte [propriedades comuns de projeto MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) para nomes de propriedade.</span><span class="sxs-lookup"><span data-stu-id="84767-150">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="84767-151">O argumento de propriedades aqui está uma lista de token = pares de valor, separados por ponto e vírgula, onde cada ocorrência de `$token$` no `.nuspec` arquivo será substituído pelo valor especificado.</span><span class="sxs-lookup"><span data-stu-id="84767-151">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="84767-152">Valores podem ser cadeias de caracteres entre aspas.</span><span class="sxs-lookup"><span data-stu-id="84767-152">Values can be strings in quotation marks.</span></span> <span data-ttu-id="84767-153">Observe que para a propriedade "Configuração", o padrão é "Debug".</span><span class="sxs-lookup"><span data-stu-id="84767-153">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="84767-154">Para alterar para uma configuração de versão, use `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="84767-154">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="84767-155">Sufixo</span><span class="sxs-lookup"><span data-stu-id="84767-155">Suffix</span></span> | <span data-ttu-id="84767-156">*(3.4.4+)*  Anexa um sufixo para o número de versão gerados internamente, normalmente usado para anexar construção ou outros identificadores de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="84767-156">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="84767-157">Por exemplo, usando `-suffix nightly` criará um pacote com um tipo de número de versão `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="84767-157">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="84767-158">Sufixos devem começar com uma letra para evitar avisos, erros e incompatibilidades com versões diferentes do NuGet e o NuGet Package Manager.</span><span class="sxs-lookup"><span data-stu-id="84767-158">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="84767-159">Símbolos</span><span class="sxs-lookup"><span data-stu-id="84767-159">Symbols</span></span> | <span data-ttu-id="84767-160">Especifica que o pacote contém fontes e símbolos.</span><span class="sxs-lookup"><span data-stu-id="84767-160">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="84767-161">Quando usado com um `.nuspec` arquivo, isso cria um arquivo de pacote do NuGet regular e pacote de símbolos correspondentes.</span><span class="sxs-lookup"><span data-stu-id="84767-161">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="84767-162">Ferramenta</span><span class="sxs-lookup"><span data-stu-id="84767-162">Tool</span></span> | <span data-ttu-id="84767-163">Especifica que os arquivos de saída do projeto devem ser colocados no `tool` pasta.</span><span class="sxs-lookup"><span data-stu-id="84767-163">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="84767-164">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="84767-164">Verbosity</span></span> | <span data-ttu-id="84767-165">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="84767-165">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="84767-166">Versão</span><span class="sxs-lookup"><span data-stu-id="84767-166">Version</span></span> | <span data-ttu-id="84767-167">Substitui o número da versão de `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="84767-167">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="84767-168">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="84767-168">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="84767-169">Excluindo dependências de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="84767-169">Excluding development dependencies</span></span>

<span data-ttu-id="84767-170">Alguns pacotes NuGet são úteis como dependências de desenvolvimento, o que ajuda a criar sua própria biblioteca, mas não são necessariamente necessários como dependências do pacote real.</span><span class="sxs-lookup"><span data-stu-id="84767-170">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="84767-171">O `pack` comando irá ignorar `package` entradas em `packages.config` que têm o `developmentDependency` atributo definido como `true`.</span><span class="sxs-lookup"><span data-stu-id="84767-171">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="84767-172">Essas entradas não incluirá como um dependências do pacote criado.</span><span class="sxs-lookup"><span data-stu-id="84767-172">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="84767-173">Por exemplo, considere o seguinte `packages.config` arquivo no projeto de origem:</span><span class="sxs-lookup"><span data-stu-id="84767-173">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="84767-174">Para este projeto, o pacote criado pelo `nuget pack` terá uma dependência no `jQuery` e `microsoft-web-helpers` mas não `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="84767-174">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="84767-175">Exemplos</span><span class="sxs-lookup"><span data-stu-id="84767-175">Examples</span></span>

```
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
