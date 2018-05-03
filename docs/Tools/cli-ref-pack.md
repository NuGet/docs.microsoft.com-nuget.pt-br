---
title: Comando de pacote do NuGet CLI
description: Referência para o comando de pacote nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a2468b099a822e69298ea78c80cfd1d5d5c09938
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="45879-103">comando de pacote NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="45879-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="45879-104">**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="45879-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="45879-105">Cria um pacote do NuGet com base em especificado `.nuspec` ou arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="45879-105">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="45879-106">O `dotnet pack` comando (consulte [comandos dotnet](dotnet-Commands.md)) e `msbuild /t:pack` (consulte [destinos do MSBuild](../reference/msbuild-targets.md)) podem ser usadas como alternativas.</span><span class="sxs-lookup"><span data-stu-id="45879-106">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="45879-107">Em Mono, criando um pacote de um arquivo de projeto não é suportado.</span><span class="sxs-lookup"><span data-stu-id="45879-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="45879-108">Você também precisa ajustar caminhos de local não o `.nuspec` de arquivos para caminhos no estilo Unix, como nuget.exe não converte nomes de caminho do Windows em si.</span><span class="sxs-lookup"><span data-stu-id="45879-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="45879-109">Uso</span><span class="sxs-lookup"><span data-stu-id="45879-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="45879-110">onde `<nuspecPath>` e `<projectPath>` especificar o `.nuspec` ou projeto de arquivo, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="45879-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="45879-111">Opções</span><span class="sxs-lookup"><span data-stu-id="45879-111">Options</span></span>

| <span data-ttu-id="45879-112">Opção</span><span class="sxs-lookup"><span data-stu-id="45879-112">Option</span></span> | <span data-ttu-id="45879-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="45879-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="45879-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="45879-114">BasePath</span></span> | <span data-ttu-id="45879-115">Define o caminho base dos arquivos definidos no `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="45879-115">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="45879-116">Build</span><span class="sxs-lookup"><span data-stu-id="45879-116">Build</span></span> | <span data-ttu-id="45879-117">Especifica que o projeto deve ser criado antes de criar o pacote.</span><span class="sxs-lookup"><span data-stu-id="45879-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="45879-118">Excluir</span><span class="sxs-lookup"><span data-stu-id="45879-118">Exclude</span></span> | <span data-ttu-id="45879-119">Especifica um ou mais padrões de curinga para excluir ao criar um pacote.</span><span class="sxs-lookup"><span data-stu-id="45879-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="45879-120">Para especificar mais de um padrão, repita-sinalizador de exclusão.</span><span class="sxs-lookup"><span data-stu-id="45879-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="45879-121">Consulte o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="45879-121">See example below.</span></span> |
| <span data-ttu-id="45879-122">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="45879-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="45879-123">Impede a inclusão de diretórios vazios ao criar o pacote.</span><span class="sxs-lookup"><span data-stu-id="45879-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="45879-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="45879-124">ForceEnglishOutput</span></span> | <span data-ttu-id="45879-125">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="45879-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="45879-126">Ajuda</span><span class="sxs-lookup"><span data-stu-id="45879-126">Help</span></span> | <span data-ttu-id="45879-127">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="45879-127">Displays help information for the command.</span></span> |
| <span data-ttu-id="45879-128">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="45879-128">IncludeReferencedProjects</span></span> | <span data-ttu-id="45879-129">Indica que o pacote criado deve incluir projetos referenciados como dependências ou como parte do pacote.</span><span class="sxs-lookup"><span data-stu-id="45879-129">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="45879-130">Se um projeto referenciado tem um correspondente `.nuspec` arquivo que tem o mesmo nome do projeto, em seguida, o projeto referenciado será adicionado como uma dependência.</span><span class="sxs-lookup"><span data-stu-id="45879-130">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="45879-131">Caso contrário, o projeto referenciado é adicionado como parte do pacote.</span><span class="sxs-lookup"><span data-stu-id="45879-131">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="45879-132">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="45879-132">MinClientVersion</span></span> | <span data-ttu-id="45879-133">Definir o *minClientVersion* atributo para o pacote criado.</span><span class="sxs-lookup"><span data-stu-id="45879-133">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="45879-134">Esse valor substituirá o valor existente *minClientVersion* atributo (se houver) no `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="45879-134">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="45879-135">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="45879-135">MSBuildPath</span></span> | <span data-ttu-id="45879-136">*(4.0 +)*  Especifica o caminho do MSBuild para usar com o comando tendo precedência sobre `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="45879-136">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="45879-137">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="45879-137">MSBuildVersion</span></span> | <span data-ttu-id="45879-138">*(3.2 +)*  Especifica a versão do MSBuild a ser usado com este comando.</span><span class="sxs-lookup"><span data-stu-id="45879-138">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="45879-139">Valores com suporte são 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="45879-139">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="45879-140">Por padrão que o MSBuild em seu caminho é separado, caso contrário, o padrão é a versão mais recente instalada do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="45879-140">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="45879-141">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="45879-141">NoDefaultExcludes</span></span> | <span data-ttu-id="45879-142">Impede a exclusão padrão do NuGet compactar arquivos e arquivos e pastas que iniciam com um ponto, como `.svn` e `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="45879-142">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="45879-143">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="45879-143">NoPackageAnalysis</span></span> | <span data-ttu-id="45879-144">Especifica que o pacote não deve executar a análise de pacote após a compilação do pacote.</span><span class="sxs-lookup"><span data-stu-id="45879-144">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="45879-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="45879-145">OutputDirectory</span></span> | <span data-ttu-id="45879-146">Especifica a pasta na qual o pacote criado é armazenado.</span><span class="sxs-lookup"><span data-stu-id="45879-146">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="45879-147">Se nenhuma pasta for especificada, a pasta atual será usada.</span><span class="sxs-lookup"><span data-stu-id="45879-147">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="45879-148">Propriedades</span><span class="sxs-lookup"><span data-stu-id="45879-148">Properties</span></span> | <span data-ttu-id="45879-149">Deve aparecer por último na linha de comando após outras opções.</span><span class="sxs-lookup"><span data-stu-id="45879-149">Should appear last on the command line after other options.</span></span> <span data-ttu-id="45879-150">Especifica uma lista de propriedades que substituem os valores no arquivo de projeto; consulte [propriedades comuns de projeto MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) para nomes de propriedade.</span><span class="sxs-lookup"><span data-stu-id="45879-150">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="45879-151">O argumento de propriedades aqui está uma lista de token = pares de valor, separados por ponto e vírgula, onde cada ocorrência de `$token$` no `.nuspec` arquivo será substituído pelo valor especificado.</span><span class="sxs-lookup"><span data-stu-id="45879-151">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="45879-152">Valores podem ser cadeias de caracteres entre aspas.</span><span class="sxs-lookup"><span data-stu-id="45879-152">Values can be strings in quotation marks.</span></span> <span data-ttu-id="45879-153">Observe que para a propriedade "Configuração", o padrão é "Debug".</span><span class="sxs-lookup"><span data-stu-id="45879-153">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="45879-154">Para alterar para uma configuração de versão, use `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="45879-154">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="45879-155">Sufixo</span><span class="sxs-lookup"><span data-stu-id="45879-155">Suffix</span></span> | <span data-ttu-id="45879-156">*(3.4.4+)*  Anexa um sufixo para o número de versão gerados internamente, normalmente usado para anexar construção ou outros identificadores de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="45879-156">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="45879-157">Por exemplo, usando `-suffix nightly` criará um pacote com um tipo de número de versão `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="45879-157">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="45879-158">Sufixos devem começar com uma letra para evitar avisos, erros e incompatibilidades com versões diferentes do NuGet e o NuGet Package Manager.</span><span class="sxs-lookup"><span data-stu-id="45879-158">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="45879-159">Símbolos</span><span class="sxs-lookup"><span data-stu-id="45879-159">Symbols</span></span> | <span data-ttu-id="45879-160">Especifica que o pacote contém fontes e símbolos.</span><span class="sxs-lookup"><span data-stu-id="45879-160">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="45879-161">Quando usado com um `.nuspec` arquivo, isso cria um arquivo de pacote do NuGet regular e pacote de símbolos correspondentes.</span><span class="sxs-lookup"><span data-stu-id="45879-161">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="45879-162">Ferramenta</span><span class="sxs-lookup"><span data-stu-id="45879-162">Tool</span></span> | <span data-ttu-id="45879-163">Especifica que os arquivos de saída do projeto devem ser colocados no `tool` pasta.</span><span class="sxs-lookup"><span data-stu-id="45879-163">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="45879-164">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="45879-164">Verbosity</span></span> | <span data-ttu-id="45879-165">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="45879-165">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="45879-166">Versão</span><span class="sxs-lookup"><span data-stu-id="45879-166">Version</span></span> | <span data-ttu-id="45879-167">Substitui o número da versão de `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="45879-167">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="45879-168">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="45879-168">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="45879-169">Excluindo dependências de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="45879-169">Excluding development dependencies</span></span>

<span data-ttu-id="45879-170">Alguns pacotes NuGet são úteis como dependências de desenvolvimento, o que ajuda a criar sua própria biblioteca, mas não são necessariamente necessários como dependências do pacote real.</span><span class="sxs-lookup"><span data-stu-id="45879-170">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="45879-171">O `pack` comando irá ignorar `package` entradas em `packages.config` que têm o `developmentDependency` atributo definido como `true`.</span><span class="sxs-lookup"><span data-stu-id="45879-171">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="45879-172">Essas entradas não incluirá como um dependências do pacote criado.</span><span class="sxs-lookup"><span data-stu-id="45879-172">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="45879-173">Por exemplo, considere o seguinte `packages.config` arquivo no projeto de origem:</span><span class="sxs-lookup"><span data-stu-id="45879-173">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="45879-174">Para este projeto, o pacote criado pelo `nuget pack` terá uma dependência no `jQuery` e `microsoft-web-helpers` mas não `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="45879-174">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="45879-175">Exemplos</span><span class="sxs-lookup"><span data-stu-id="45879-175">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
