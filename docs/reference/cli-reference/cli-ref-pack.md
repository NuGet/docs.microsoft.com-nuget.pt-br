---
title: Comando NuGet CLI Pack
description: Referência para o comando do pacote de nuget.exe
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e2906d53119cb8c922df7d177cd686836ac50a5a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780042"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="948a1-103">comando Pack (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="948a1-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="948a1-104">**Aplica-se a:** &bullet; **versões com suporte** para criação de pacote: 2.7 +</span><span class="sxs-lookup"><span data-stu-id="948a1-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="948a1-105">Cria um pacote NuGet com base no arquivo [. nuspec](../nuspec.md) ou projeto especificado.</span><span class="sxs-lookup"><span data-stu-id="948a1-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="948a1-106">O `dotnet pack` comando (consulte os [comandos dotnet](../dotnet-Commands.md)) e `msbuild -t:pack` (consulte [destinos do MSBuild](../msbuild-targets.md)) pode ser usado como alternativas.</span><span class="sxs-lookup"><span data-stu-id="948a1-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="948a1-107">Use o [`dotnet pack`](../dotnet-Commands.md) ou [`msbuild -t:pack`](../msbuild-targets.md) para projetos baseados em [PackageReference](../../consume-packages/package-references-in-project-files.md) .</span><span class="sxs-lookup"><span data-stu-id="948a1-107">Use [`dotnet pack`](../dotnet-Commands.md) or [`msbuild -t:pack`](../msbuild-targets.md) for [PackageReference](../../consume-packages/package-references-in-project-files.md) based projects.</span></span>
> <span data-ttu-id="948a1-108">Em mono, não há suporte para a criação de um pacote a partir de um arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="948a1-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="948a1-109">Você também precisa ajustar caminhos não locais no `.nuspec` arquivo para caminhos em estilo UNIX, pois nuget.exe não converte os próprios caminhos do Windows.</span><span class="sxs-lookup"><span data-stu-id="948a1-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="948a1-110">Uso</span><span class="sxs-lookup"><span data-stu-id="948a1-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="948a1-111">onde `<nuspecPath>` e `<projectPath>` especifique o `.nuspec` arquivo de projeto ou, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="948a1-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="948a1-112">Opções</span><span class="sxs-lookup"><span data-stu-id="948a1-112">Options</span></span>
- **`-BasePath`**

   <span data-ttu-id="948a1-113">Define o caminho base dos arquivos definidos no arquivo [. nuspec](../nuspec.md) .</span><span class="sxs-lookup"><span data-stu-id="948a1-113">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span>

- **`-Build`**

  <span data-ttu-id="948a1-114">Especifica que o projeto deve ser compilado antes da criação do pacote.</span><span class="sxs-lookup"><span data-stu-id="948a1-114">Specifies that the project should be built before building the package.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="948a1-115">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="948a1-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="948a1-116">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="948a1-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Exclude`**

  <span data-ttu-id="948a1-117">Especifica um ou mais padrões de curinga a serem excluídos ao criar um pacote.</span><span class="sxs-lookup"><span data-stu-id="948a1-117">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="948a1-118">Para especificar mais de um padrão, repita o sinalizador-Exclude.</span><span class="sxs-lookup"><span data-stu-id="948a1-118">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="948a1-119">Consulte o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="948a1-119">See example below.</span></span>

- **`-ExcludeEmptyDirectories`**

  <span data-ttu-id="948a1-120">Impede a inclusão de diretórios vazios ao compilar o pacote.</span><span class="sxs-lookup"><span data-stu-id="948a1-120">Prevents inclusion of empty directories when building the package.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="948a1-121">*(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="948a1-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="948a1-122">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="948a1-122">Displays help information for the command.</span></span>

- **`-IncludeReferencedProjects`**

  <span data-ttu-id="948a1-123">Indica que o pacote criado deve incluir projetos referenciados como dependências ou como parte do pacote.</span><span class="sxs-lookup"><span data-stu-id="948a1-123">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="948a1-124">Se um projeto referenciado tiver um `.nuspec` arquivo correspondente que tenha o mesmo nome que o projeto, esse projeto referenciado será adicionado como uma dependência.</span><span class="sxs-lookup"><span data-stu-id="948a1-124">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="948a1-125">Caso contrário, o projeto referenciado será adicionado como parte do pacote.</span><span class="sxs-lookup"><span data-stu-id="948a1-125">Otherwise, the referenced project is added as part of the package.</span></span>

- **`-InstallPackageToOutputPath`**

  <span data-ttu-id="948a1-126">Especifique se o comando deve preparar o diretório de saída do pacote para dar suporte ao compartilhamento como feed.</span><span class="sxs-lookup"><span data-stu-id="948a1-126">Specify if the command should prepare the package output directory to support share as feed.</span></span>

- **`-MinClientVersion`**

  <span data-ttu-id="948a1-127">Defina o atributo *minClientVersion* para o pacote criado.</span><span class="sxs-lookup"><span data-stu-id="948a1-127">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="948a1-128">Esse valor substituirá o valor do atributo *minClientVersion* existente (se houver) no `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="948a1-128">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="948a1-129">*(4.0 +)* Especifica o caminho do MSBuild a ser usado com o comando, tendo precedência sobre `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="948a1-129">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="948a1-130">*(3,2 +)* Especifica a versão do MSBuild a ser usada com este comando.</span><span class="sxs-lookup"><span data-stu-id="948a1-130">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="948a1-131">Os valores com suporte são 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="948a1-131">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="948a1-132">Por padrão, o MSBuild em seu caminho é escolhido; caso contrário, ele usa a versão mais recente instalada do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="948a1-132">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoDefaultExcludes`**

  <span data-ttu-id="948a1-133">Impede a exclusão padrão de arquivos de pacote do NuGet e arquivos e pastas que começam com um ponto, como `.svn` e `.gitignore` .</span><span class="sxs-lookup"><span data-stu-id="948a1-133">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="948a1-134">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="948a1-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoPackageAnalysis`**

  <span data-ttu-id="948a1-135">Especifica que o pacote não deve executar a análise de pacote após a compilação do pacote.</span><span class="sxs-lookup"><span data-stu-id="948a1-135">Specifies that pack should not run package analysis after building the package.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="948a1-136">Especifica a pasta na qual o pacote criado é armazenado.</span><span class="sxs-lookup"><span data-stu-id="948a1-136">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="948a1-137">Se nenhuma pasta for especificada, a pasta atual será usada.</span><span class="sxs-lookup"><span data-stu-id="948a1-137">If no folder is specified, the current folder is used.</span></span>

- **`-OutputFileNamesWithoutVersion`**

  <span data-ttu-id="948a1-138">Especifique se o comando deve preparar o nome de saída do pacote sem a versão.</span><span class="sxs-lookup"><span data-stu-id="948a1-138">Specify if the command should prepare the package output name without the version.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="948a1-139">Especifica a pasta de pacotes.</span><span class="sxs-lookup"><span data-stu-id="948a1-139">Specifies the packages folder.</span></span>

- **`-p|-Properties`**

  <span data-ttu-id="948a1-140">Deve aparecer por último na linha de comando após outras opções.</span><span class="sxs-lookup"><span data-stu-id="948a1-140">Should appear last on the command line after other options.</span></span> <span data-ttu-id="948a1-141">Especifica uma lista de propriedades que substituem valores no arquivo de projeto; consulte [Propriedades comuns do projeto MSBuild](/visualstudio/msbuild/common-msbuild-project-properties) para nomes de propriedade.</span><span class="sxs-lookup"><span data-stu-id="948a1-141">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="948a1-142">O argumento properties aqui é uma lista de pares token = valor, separados por ponto e vírgula, em que cada ocorrência de `$token$` no `.nuspec` arquivo será substituída pelo valor especificado.</span><span class="sxs-lookup"><span data-stu-id="948a1-142">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="948a1-143">Os valores podem ser cadeias de caracteres entre aspas.</span><span class="sxs-lookup"><span data-stu-id="948a1-143">Values can be strings in quotation marks.</span></span> <span data-ttu-id="948a1-144">Observe que, para a propriedade "Configuration", o padrão é "debug".</span><span class="sxs-lookup"><span data-stu-id="948a1-144">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="948a1-145">Para alterar para uma configuração de versão, use `-Properties Configuration=Release` .</span><span class="sxs-lookup"><span data-stu-id="948a1-145">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> <span data-ttu-id="948a1-146">**Em geral**, as propriedades devem ser as mesmas que foram usadas durante a compilação do projeto correspondente, a fim de evitar um comportamento potencialmente estranho.</span><span class="sxs-lookup"><span data-stu-id="948a1-146">**In general**, Properties should be the same that were used during the corresponding project build, in order to avoid potentially strange behavior.</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="948a1-147">Especifica o diretório da solução.</span><span class="sxs-lookup"><span data-stu-id="948a1-147">Specifies the solution directory.</span></span>

- **`-Suffix`**

  <span data-ttu-id="948a1-148">*(3.4.4 +)* Acrescenta um sufixo ao número de versão gerado internamente, normalmente usado para anexar Build ou outros identificadores de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="948a1-148">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="948a1-149">Por exemplo, usar `-suffix nightly` criará um pacote com um número de versão como `1.2.3-nightly` .</span><span class="sxs-lookup"><span data-stu-id="948a1-149">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="948a1-150">Os sufixos devem começar com uma letra para evitar avisos, erros e possíveis incompatibilidades com versões diferentes do NuGet e do Gerenciador de pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="948a1-150">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span>

- **`-SymbolPackageFormat`**

  <span data-ttu-id="948a1-151">Ao criar um pacote de símbolos, permite escolher entre o `snupkg` `symbols.nupkg` formato e.</span><span class="sxs-lookup"><span data-stu-id="948a1-151">When creating a symbols package, allows to choose between the `snupkg` and `symbols.nupkg` format.</span></span>

- **`-Symbols`**

  <span data-ttu-id="948a1-152">Especifica que o pacote contém fontes e símbolos.</span><span class="sxs-lookup"><span data-stu-id="948a1-152">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="948a1-153">Quando usado com um `.nuspec` arquivo, isso cria um arquivo de pacote NuGet regular e o pacote de símbolos correspondente.</span><span class="sxs-lookup"><span data-stu-id="948a1-153">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="948a1-154">Por padrão, ele cria um [pacote de símbolos herdado](../../create-packages/Symbol-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="948a1-154">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="948a1-155">O novo formato recomendado para pacotes de símbolos é .snupkg.</span><span class="sxs-lookup"><span data-stu-id="948a1-155">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="948a1-156">Veja [Criando pacotes de símbolos (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="948a1-156">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span>

- **`-Tool`**

   <span data-ttu-id="948a1-157">Especifica que os arquivos de saída do projeto devem ser colocados na `tool` pasta.</span><span class="sxs-lookup"><span data-stu-id="948a1-157">Specifies that the output files of the project should be placed in the `tool` folder.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="948a1-158">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="948a1-158">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="948a1-159">Substitui o número de versão do `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="948a1-159">Overrides the version number from the `.nuspec` file.</span></span>

<span data-ttu-id="948a1-160">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="948a1-160">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="948a1-161">Excluindo dependências de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="948a1-161">Excluding development dependencies</span></span>

<span data-ttu-id="948a1-162">Alguns pacotes NuGet são úteis como dependências de desenvolvimento, que ajudam você a criar sua própria biblioteca, mas não são necessariamente necessárias como dependências de pacote reais.</span><span class="sxs-lookup"><span data-stu-id="948a1-162">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="948a1-163">O `pack` comando irá ignorar `package` entradas no `packages.config` que têm o `developmentDependency` atributo definido como `true` .</span><span class="sxs-lookup"><span data-stu-id="948a1-163">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="948a1-164">Essas entradas não serão incluídas como dependências no pacote criado.</span><span class="sxs-lookup"><span data-stu-id="948a1-164">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="948a1-165">Por exemplo, considere o seguinte `packages.config` arquivo no projeto de origem:</span><span class="sxs-lookup"><span data-stu-id="948a1-165">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="948a1-166">Para este projeto, o pacote criado pelo `nuget pack` terá uma dependência de `jQuery` e `microsoft-web-helpers` , mas não `netfx-Guard` .</span><span class="sxs-lookup"><span data-stu-id="948a1-166">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="suppressing-pack-warnings"></a><span data-ttu-id="948a1-167">Suprimindo avisos de pacote</span><span class="sxs-lookup"><span data-stu-id="948a1-167">Suppressing pack warnings</span></span>

<span data-ttu-id="948a1-168">Embora seja recomendável que você resolva todos os avisos do NuGet durante suas operações de pacote, em determinadas situações, a supressão deles é garantida.</span><span class="sxs-lookup"><span data-stu-id="948a1-168">While it is recommended that you resolve all NuGet warnings during your pack operations, in certain situations suppressing them is warranted.</span></span>

<span data-ttu-id="948a1-169">Você pode conseguir isso da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="948a1-169">You can achieve that in the following way:</span></span> 

> <span data-ttu-id="948a1-170">Pacote do pacote de nuget.exe. nuspec – Propriedades nowarn = NU5104</span><span class="sxs-lookup"><span data-stu-id="948a1-170">nuget.exe pack package.nuspec -Properties NoWarn=NU5104</span></span>

## <a name="examples"></a><span data-ttu-id="948a1-171">Exemplos</span><span class="sxs-lookup"><span data-stu-id="948a1-171">Examples</span></span>

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
