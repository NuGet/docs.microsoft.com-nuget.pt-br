---
title: Comando de pacote da CLI do NuGet
description: Referência do comando de pacote nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b5bd8bd30ad134f36433b8e4721ce131425a1483
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453358"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="a8f04-103">Commando pack (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a8f04-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="a8f04-104">**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** 2.7 ou superior</span><span class="sxs-lookup"><span data-stu-id="a8f04-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="a8f04-105">Cria um pacote do NuGet com base em especificado `.nuspec` ou arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="a8f04-105">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="a8f04-106">O `dotnet pack` comando (consulte [comandos dotnet](dotnet-Commands.md)) e `msbuild -t:pack` (consulte [destinos do MSBuild](../reference/msbuild-targets.md)) pode ser usado como alternativas.</span><span class="sxs-lookup"><span data-stu-id="a8f04-106">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="a8f04-107">Em Mono, criando um pacote em um arquivo de projeto não é suportado.</span><span class="sxs-lookup"><span data-stu-id="a8f04-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="a8f04-108">Você também precisará ajustar os caminhos de local não no `.nuspec` de arquivo para caminhos no estilo Unix, como nuget.exe não converte nomes de caminhos do Windows em si.</span><span class="sxs-lookup"><span data-stu-id="a8f04-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="a8f04-109">Uso</span><span class="sxs-lookup"><span data-stu-id="a8f04-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="a8f04-110">em que `<nuspecPath>` e `<projectPath>` especifique o `.nuspec` ou projeto de arquivo, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="a8f04-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="a8f04-111">Opções</span><span class="sxs-lookup"><span data-stu-id="a8f04-111">Options</span></span>

| <span data-ttu-id="a8f04-112">Opção</span><span class="sxs-lookup"><span data-stu-id="a8f04-112">Option</span></span> | <span data-ttu-id="a8f04-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="a8f04-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a8f04-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="a8f04-114">BasePath</span></span> | <span data-ttu-id="a8f04-115">Define o caminho base dos arquivos definidos no `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="a8f04-115">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="a8f04-116">Build</span><span class="sxs-lookup"><span data-stu-id="a8f04-116">Build</span></span> | <span data-ttu-id="a8f04-117">Especifica que o projeto deve ser compilado antes de compilar o pacote.</span><span class="sxs-lookup"><span data-stu-id="a8f04-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="a8f04-118">Excluir</span><span class="sxs-lookup"><span data-stu-id="a8f04-118">Exclude</span></span> | <span data-ttu-id="a8f04-119">Especifica um ou mais padrões de curinga a ser excluído durante a criação de um pacote.</span><span class="sxs-lookup"><span data-stu-id="a8f04-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="a8f04-120">Para especificar mais de um padrão, repita-sinalizador de exclusão.</span><span class="sxs-lookup"><span data-stu-id="a8f04-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="a8f04-121">Consulte o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="a8f04-121">See example below.</span></span> |
| <span data-ttu-id="a8f04-122">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="a8f04-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="a8f04-123">Impede a inclusão de diretórios vazios ao criar o pacote.</span><span class="sxs-lookup"><span data-stu-id="a8f04-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="a8f04-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a8f04-124">ForceEnglishOutput</span></span> | <span data-ttu-id="a8f04-125">*(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="a8f04-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a8f04-126">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a8f04-126">ConfigFile</span></span> | <span data-ttu-id="a8f04-127">Especifique o arquivo de configuração para o comando pack.</span><span class="sxs-lookup"><span data-stu-id="a8f04-127">Specify the configuration file for the pack command.</span></span> |
| <span data-ttu-id="a8f04-128">Ajuda</span><span class="sxs-lookup"><span data-stu-id="a8f04-128">Help</span></span> | <span data-ttu-id="a8f04-129">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="a8f04-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="a8f04-130">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="a8f04-130">IncludeReferencedProjects</span></span> | <span data-ttu-id="a8f04-131">Indica que o pacote criado deve incluir nos projetos referenciados como dependências ou como parte do pacote.</span><span class="sxs-lookup"><span data-stu-id="a8f04-131">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="a8f04-132">Se um projeto referenciado tem um correspondente `.nuspec` arquivo que tem o mesmo nome que o projeto, em seguida, esse projeto referenciado é adicionado como uma dependência.</span><span class="sxs-lookup"><span data-stu-id="a8f04-132">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="a8f04-133">Caso contrário, o projeto referenciado é adicionado como parte do pacote.</span><span class="sxs-lookup"><span data-stu-id="a8f04-133">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="a8f04-134">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="a8f04-134">MinClientVersion</span></span> | <span data-ttu-id="a8f04-135">Defina as *minClientVersion* atributo para o pacote criado.</span><span class="sxs-lookup"><span data-stu-id="a8f04-135">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="a8f04-136">Esse valor substituirá o valor existente *minClientVersion* atributo (se houver) no `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="a8f04-136">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="a8f04-137">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="a8f04-137">MSBuildPath</span></span> | <span data-ttu-id="a8f04-138">*(4.0 e posteriores)*  Especifica o caminho do MSBuild a usar com o comando, tendo precedência sobre `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="a8f04-138">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="a8f04-139">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="a8f04-139">MSBuildVersion</span></span> | <span data-ttu-id="a8f04-140">*(3.2 e superior)*  Especifica a versão do MSBuild a ser usado com este comando.</span><span class="sxs-lookup"><span data-stu-id="a8f04-140">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="a8f04-141">Valores com suporte são 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="a8f04-141">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="a8f04-142">Por padrão que o MSBuild em seu caminho é escolhido, caso contrário, o padrão é a versão mais recente instalada do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="a8f04-142">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="a8f04-143">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="a8f04-143">NoDefaultExcludes</span></span> | <span data-ttu-id="a8f04-144">Impede a exclusão de padrão do NuGet empacotar arquivos e arquivos e pastas que iniciam com um ponto, como `.svn` e `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="a8f04-144">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="a8f04-145">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="a8f04-145">NoPackageAnalysis</span></span> | <span data-ttu-id="a8f04-146">Especifica que o pacote não deve executar a análise de pacote após a compilação do pacote.</span><span class="sxs-lookup"><span data-stu-id="a8f04-146">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="a8f04-147">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="a8f04-147">OutputDirectory</span></span> | <span data-ttu-id="a8f04-148">Especifica a pasta na qual o pacote criado é armazenado.</span><span class="sxs-lookup"><span data-stu-id="a8f04-148">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="a8f04-149">Se nenhuma pasta for especificada, a pasta atual será usada.</span><span class="sxs-lookup"><span data-stu-id="a8f04-149">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="a8f04-150">Propriedades</span><span class="sxs-lookup"><span data-stu-id="a8f04-150">Properties</span></span> | <span data-ttu-id="a8f04-151">Deve aparecer por último na linha de comando após outras opções.</span><span class="sxs-lookup"><span data-stu-id="a8f04-151">Should appear last on the command line after other options.</span></span> <span data-ttu-id="a8f04-152">Especifica uma lista de propriedades que substituem os valores no arquivo de projeto; ver [propriedades de projeto comuns do MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) para nomes de propriedade.</span><span class="sxs-lookup"><span data-stu-id="a8f04-152">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="a8f04-153">O argumento de propriedades aqui está uma lista de token = pares de valor, separados por ponto e vírgula, onde cada ocorrência de `$token$` no `.nuspec` arquivo será substituído com o valor fornecido.</span><span class="sxs-lookup"><span data-stu-id="a8f04-153">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="a8f04-154">Valores podem ser cadeias de caracteres entre aspas.</span><span class="sxs-lookup"><span data-stu-id="a8f04-154">Values can be strings in quotation marks.</span></span> <span data-ttu-id="a8f04-155">Observe que para a propriedade de "Configuração", o padrão é "Debug".</span><span class="sxs-lookup"><span data-stu-id="a8f04-155">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="a8f04-156">Para alterar para uma configuração de versão, use `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="a8f04-156">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="a8f04-157">Sufixo</span><span class="sxs-lookup"><span data-stu-id="a8f04-157">Suffix</span></span> | <span data-ttu-id="a8f04-158">*(3.4.4+)*  Anexa um sufixo para o número de versão gerado internamente, normalmente usado para acrescentar o build ou outros identificadores de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="a8f04-158">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="a8f04-159">Por exemplo, usando `-suffix nightly` criará um pacote com um tipo de número de versão `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="a8f04-159">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="a8f04-160">Sufixos devem começar com uma letra para evitar possíveis incompatibilidades com diferentes versões do NuGet e o Gerenciador de pacotes do NuGet, erros e avisos.</span><span class="sxs-lookup"><span data-stu-id="a8f04-160">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="a8f04-161">Símbolos</span><span class="sxs-lookup"><span data-stu-id="a8f04-161">Symbols</span></span> | <span data-ttu-id="a8f04-162">Especifica que o pacote contém fontes e símbolos.</span><span class="sxs-lookup"><span data-stu-id="a8f04-162">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="a8f04-163">Quando usado com um `.nuspec` arquivo, isso cria um arquivo de pacote do NuGet regular e correspondente símbolos de pacote.</span><span class="sxs-lookup"><span data-stu-id="a8f04-163">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="a8f04-164">Por padrão, ele cria um [pacote de símbolos herdados](../create-packages/Symbol-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="a8f04-164">By default it creates a [legacy symbol package](../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="a8f04-165">O novo formato recomendado para pacotes de símbolos é .snupkg.</span><span class="sxs-lookup"><span data-stu-id="a8f04-165">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="a8f04-166">Veja [Criando pacotes de símbolos (.snupkg)](../create-packages/Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="a8f04-166">See [Creating symbol packages (.snupkg)](../create-packages/Symbol-Packages-snupkg.md).</span></span> |
| <span data-ttu-id="a8f04-167">Ferramenta</span><span class="sxs-lookup"><span data-stu-id="a8f04-167">Tool</span></span> | <span data-ttu-id="a8f04-168">Especifica que os arquivos de saída do projeto devem ser colocados no `tool` pasta.</span><span class="sxs-lookup"><span data-stu-id="a8f04-168">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="a8f04-169">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="a8f04-169">Verbosity</span></span> | <span data-ttu-id="a8f04-170">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="a8f04-170">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="a8f04-171">Versão</span><span class="sxs-lookup"><span data-stu-id="a8f04-171">Version</span></span> | <span data-ttu-id="a8f04-172">Substitui o número de versão dos `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="a8f04-172">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="a8f04-173">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a8f04-173">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="a8f04-174">Excluindo as dependências de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="a8f04-174">Excluding development dependencies</span></span>

<span data-ttu-id="a8f04-175">Alguns pacotes do NuGet são úteis como dependências de desenvolvimento, que ajudam a criar sua própria biblioteca, mas não são necessariamente necessários como dependências do pacote real.</span><span class="sxs-lookup"><span data-stu-id="a8f04-175">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="a8f04-176">O `pack` comando ignorará `package` entradas na `packages.config` que têm o `developmentDependency` atributo definido como `true`.</span><span class="sxs-lookup"><span data-stu-id="a8f04-176">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="a8f04-177">Essas entradas não incluirá como um dependências no pacote criado.</span><span class="sxs-lookup"><span data-stu-id="a8f04-177">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="a8f04-178">Por exemplo, considere o seguinte `packages.config` arquivo no projeto de origem:</span><span class="sxs-lookup"><span data-stu-id="a8f04-178">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="a8f04-179">Para este projeto, o pacote criado pelo `nuget pack` terá uma dependência no `jQuery` e `microsoft-web-helpers` mas não `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="a8f04-179">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="a8f04-180">Exemplos</span><span class="sxs-lookup"><span data-stu-id="a8f04-180">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
