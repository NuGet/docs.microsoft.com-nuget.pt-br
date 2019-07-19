---
title: Comando NuGet CLI Pack
description: Referência para o comando do pacote NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e12944bdd5d43b8b9e84908be480a5249dd924f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327653"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="50f4b-103">Commando pack (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="50f4b-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="50f4b-104">**Aplica-se a:** &bullet; **versões com suporte** para criação de pacote: 2.7+</span><span class="sxs-lookup"><span data-stu-id="50f4b-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="50f4b-105">Cria um pacote NuGet com base no arquivo `.nuspec` de projeto ou especificado.</span><span class="sxs-lookup"><span data-stu-id="50f4b-105">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="50f4b-106">O `dotnet pack` comando (consulte os [comandos dotnet](../dotnet-Commands.md)) `msbuild -t:pack` e (consulte [destinos do MSBuild](../msbuild-targets.md)) pode ser usado como alternativas.</span><span class="sxs-lookup"><span data-stu-id="50f4b-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="50f4b-107">Em mono, não há suporte para a criação de um pacote a partir de um arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="50f4b-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="50f4b-108">Você também precisa ajustar caminhos não locais no `.nuspec` arquivo para caminhos em estilo UNIX, pois o NuGet. exe não converte os próprios caminhos do Windows.</span><span class="sxs-lookup"><span data-stu-id="50f4b-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="50f4b-109">Uso</span><span class="sxs-lookup"><span data-stu-id="50f4b-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="50f4b-110">onde `<nuspecPath>` `.nuspec` e `<projectPath>` especifique o arquivo de projeto ou, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="50f4b-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="50f4b-111">Opções</span><span class="sxs-lookup"><span data-stu-id="50f4b-111">Options</span></span>

| <span data-ttu-id="50f4b-112">Opção</span><span class="sxs-lookup"><span data-stu-id="50f4b-112">Option</span></span> | <span data-ttu-id="50f4b-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="50f4b-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="50f4b-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="50f4b-114">BasePath</span></span> | <span data-ttu-id="50f4b-115">Define o caminho base dos arquivos definidos no `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="50f4b-115">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="50f4b-116">Build</span><span class="sxs-lookup"><span data-stu-id="50f4b-116">Build</span></span> | <span data-ttu-id="50f4b-117">Especifica que o projeto deve ser compilado antes da criação do pacote.</span><span class="sxs-lookup"><span data-stu-id="50f4b-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="50f4b-118">Excluir</span><span class="sxs-lookup"><span data-stu-id="50f4b-118">Exclude</span></span> | <span data-ttu-id="50f4b-119">Especifica um ou mais padrões de curinga a serem excluídos ao criar um pacote.</span><span class="sxs-lookup"><span data-stu-id="50f4b-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="50f4b-120">Para especificar mais de um padrão, repita o sinalizador-Exclude.</span><span class="sxs-lookup"><span data-stu-id="50f4b-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="50f4b-121">Consulte o exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="50f4b-121">See example below.</span></span> |
| <span data-ttu-id="50f4b-122">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="50f4b-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="50f4b-123">Impede a inclusão de diretórios vazios ao compilar o pacote.</span><span class="sxs-lookup"><span data-stu-id="50f4b-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="50f4b-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="50f4b-124">ForceEnglishOutput</span></span> | <span data-ttu-id="50f4b-125">*(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="50f4b-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="50f4b-126">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="50f4b-126">ConfigFile</span></span> | <span data-ttu-id="50f4b-127">Especifique o arquivo de configuração para o comando de pacote.</span><span class="sxs-lookup"><span data-stu-id="50f4b-127">Specify the configuration file for the pack command.</span></span> |
| <span data-ttu-id="50f4b-128">Ajuda</span><span class="sxs-lookup"><span data-stu-id="50f4b-128">Help</span></span> | <span data-ttu-id="50f4b-129">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="50f4b-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="50f4b-130">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="50f4b-130">IncludeReferencedProjects</span></span> | <span data-ttu-id="50f4b-131">Indica que o pacote criado deve incluir projetos referenciados como dependências ou como parte do pacote.</span><span class="sxs-lookup"><span data-stu-id="50f4b-131">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="50f4b-132">Se um projeto referenciado tiver um `.nuspec` arquivo correspondente que tenha o mesmo nome que o projeto, esse projeto referenciado será adicionado como uma dependência.</span><span class="sxs-lookup"><span data-stu-id="50f4b-132">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="50f4b-133">Caso contrário, o projeto referenciado será adicionado como parte do pacote.</span><span class="sxs-lookup"><span data-stu-id="50f4b-133">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="50f4b-134">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="50f4b-134">MinClientVersion</span></span> | <span data-ttu-id="50f4b-135">Defina o atributo *minClientVersion* para o pacote criado.</span><span class="sxs-lookup"><span data-stu-id="50f4b-135">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="50f4b-136">Esse valor substituirá o valor do atributo *minClientVersion* existente (se houver) no `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="50f4b-136">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="50f4b-137">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="50f4b-137">MSBuildPath</span></span> | <span data-ttu-id="50f4b-138">*(4.0 +)* Especifica o caminho do MSBuild a ser usado com o comando, tendo precedência sobre `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="50f4b-138">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="50f4b-139">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="50f4b-139">MSBuildVersion</span></span> | <span data-ttu-id="50f4b-140">*(3,2 +)* Especifica a versão do MSBuild a ser usada com este comando.</span><span class="sxs-lookup"><span data-stu-id="50f4b-140">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="50f4b-141">Os valores com suporte são 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="50f4b-141">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="50f4b-142">Por padrão, o MSBuild em seu caminho é escolhido; caso contrário, ele usa a versão mais recente instalada do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="50f4b-142">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="50f4b-143">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="50f4b-143">NoDefaultExcludes</span></span> | <span data-ttu-id="50f4b-144">Impede a exclusão padrão de arquivos de pacote do NuGet e arquivos e pastas que começam com um `.svn` ponto `.gitignore`, como e.</span><span class="sxs-lookup"><span data-stu-id="50f4b-144">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="50f4b-145">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="50f4b-145">NoPackageAnalysis</span></span> | <span data-ttu-id="50f4b-146">Especifica que o pacote não deve executar a análise de pacote após a compilação do pacote.</span><span class="sxs-lookup"><span data-stu-id="50f4b-146">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="50f4b-147">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="50f4b-147">OutputDirectory</span></span> | <span data-ttu-id="50f4b-148">Especifica a pasta na qual o pacote criado é armazenado.</span><span class="sxs-lookup"><span data-stu-id="50f4b-148">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="50f4b-149">Se nenhuma pasta for especificada, a pasta atual será usada.</span><span class="sxs-lookup"><span data-stu-id="50f4b-149">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="50f4b-150">Propriedades</span><span class="sxs-lookup"><span data-stu-id="50f4b-150">Properties</span></span> | <span data-ttu-id="50f4b-151">Deve aparecer por último na linha de comando após outras opções.</span><span class="sxs-lookup"><span data-stu-id="50f4b-151">Should appear last on the command line after other options.</span></span> <span data-ttu-id="50f4b-152">Especifica uma lista de propriedades que substituem valores no arquivo de projeto; consulte [Propriedades comuns do projeto MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) para nomes de propriedade.</span><span class="sxs-lookup"><span data-stu-id="50f4b-152">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="50f4b-153">O argumento properties aqui é uma lista de pares token = valor, separados por ponto e vírgula, em que cada `$token$` ocorrência de `.nuspec` no arquivo será substituída pelo valor especificado.</span><span class="sxs-lookup"><span data-stu-id="50f4b-153">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="50f4b-154">Os valores podem ser cadeias de caracteres entre aspas.</span><span class="sxs-lookup"><span data-stu-id="50f4b-154">Values can be strings in quotation marks.</span></span> <span data-ttu-id="50f4b-155">Observe que, para a propriedade "Configuration", o padrão é "debug".</span><span class="sxs-lookup"><span data-stu-id="50f4b-155">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="50f4b-156">Para alterar para uma configuração de versão, `-Properties Configuration=Release`use.</span><span class="sxs-lookup"><span data-stu-id="50f4b-156">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="50f4b-157">Sufixo</span><span class="sxs-lookup"><span data-stu-id="50f4b-157">Suffix</span></span> | <span data-ttu-id="50f4b-158">*(3.4.4 +)* Acrescenta um sufixo ao número de versão gerado internamente, normalmente usado para anexar Build ou outros identificadores de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="50f4b-158">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="50f4b-159">Por exemplo, usar `-suffix nightly` criará um pacote com um número de versão `1.2.3-nightly`como.</span><span class="sxs-lookup"><span data-stu-id="50f4b-159">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="50f4b-160">Os sufixos devem começar com uma letra para evitar avisos, erros e possíveis incompatibilidades com versões diferentes do NuGet e do Gerenciador de pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="50f4b-160">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="50f4b-161">Símbolos</span><span class="sxs-lookup"><span data-stu-id="50f4b-161">Symbols</span></span> | <span data-ttu-id="50f4b-162">Especifica que o pacote contém fontes e símbolos.</span><span class="sxs-lookup"><span data-stu-id="50f4b-162">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="50f4b-163">Quando usado com um `.nuspec` arquivo, isso cria um arquivo de pacote NuGet regular e o pacote de símbolos correspondente.</span><span class="sxs-lookup"><span data-stu-id="50f4b-163">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="50f4b-164">Por padrão, ele cria um [pacote de símbolos herdado](../../create-packages/Symbol-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="50f4b-164">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="50f4b-165">O novo formato recomendado para pacotes de símbolos é .snupkg.</span><span class="sxs-lookup"><span data-stu-id="50f4b-165">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="50f4b-166">Veja [Criando pacotes de símbolos (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="50f4b-166">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span> |
| <span data-ttu-id="50f4b-167">Ferramenta</span><span class="sxs-lookup"><span data-stu-id="50f4b-167">Tool</span></span> | <span data-ttu-id="50f4b-168">Especifica que os arquivos de saída do projeto devem ser colocados na `tool` pasta.</span><span class="sxs-lookup"><span data-stu-id="50f4b-168">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="50f4b-169">Verbosity</span><span class="sxs-lookup"><span data-stu-id="50f4b-169">Verbosity</span></span> | <span data-ttu-id="50f4b-170">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="50f4b-170">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="50f4b-171">Versão</span><span class="sxs-lookup"><span data-stu-id="50f4b-171">Version</span></span> | <span data-ttu-id="50f4b-172">Substitui o número de versão do `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="50f4b-172">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="50f4b-173">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="50f4b-173">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="50f4b-174">Excluindo dependências de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="50f4b-174">Excluding development dependencies</span></span>

<span data-ttu-id="50f4b-175">Alguns pacotes NuGet são úteis como dependências de desenvolvimento, que ajudam você a criar sua própria biblioteca, mas não são necessariamente necessárias como dependências de pacote reais.</span><span class="sxs-lookup"><span data-stu-id="50f4b-175">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="50f4b-176">O `pack` comando irá ignorar `package` entradas no `packages.config` que têm o `developmentDependency` atributo definido como `true`.</span><span class="sxs-lookup"><span data-stu-id="50f4b-176">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="50f4b-177">Essas entradas não serão incluídas como dependências no pacote criado.</span><span class="sxs-lookup"><span data-stu-id="50f4b-177">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="50f4b-178">Por exemplo, considere o seguinte `packages.config` arquivo no projeto de origem:</span><span class="sxs-lookup"><span data-stu-id="50f4b-178">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="50f4b-179">Para este projeto, o pacote criado pelo `nuget pack` terá uma dependência de `jQuery` e `microsoft-web-helpers` , mas não `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="50f4b-179">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="50f4b-180">Exemplos</span><span class="sxs-lookup"><span data-stu-id="50f4b-180">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
