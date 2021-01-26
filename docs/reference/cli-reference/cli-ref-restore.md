---
title: Comando de restauração da CLI do NuGet
description: Referência para o comando nuget.exe Restore
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 49fabbd0ef0c1c0c16f13bdf741296575fa72359
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780026"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="fef92-103">comando Restore (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fef92-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="fef92-104">**Aplica-se a:** &bullet; **versões com suporte** de consumo de pacote: 2.7 +</span><span class="sxs-lookup"><span data-stu-id="fef92-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="fef92-105">Baixa e instala todos os pacotes ausentes da `packages` pasta.</span><span class="sxs-lookup"><span data-stu-id="fef92-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="fef92-106">Quando usado com o NuGet 4.0 + e o formato PackageReference, o gera um `<project>.nuget.props` arquivo, se necessário, na `obj` pasta.</span><span class="sxs-lookup"><span data-stu-id="fef92-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="fef92-107">(O arquivo pode ser omitido do controle do código-fonte.)</span><span class="sxs-lookup"><span data-stu-id="fef92-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="fef92-108">No Mac OSX e no Linux com a CLI no mono, não há suporte para a restauração de pacotes com o PackageReference.</span><span class="sxs-lookup"><span data-stu-id="fef92-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="fef92-109">Uso</span><span class="sxs-lookup"><span data-stu-id="fef92-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="fef92-110">em que `<projectPath>` especifica o local de uma solução ou um `packages.config` arquivo.</span><span class="sxs-lookup"><span data-stu-id="fef92-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="fef92-111">Consulte os [comentários](#remarks) abaixo para obter detalhes comportamentais.</span><span class="sxs-lookup"><span data-stu-id="fef92-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="fef92-112">Opções</span><span class="sxs-lookup"><span data-stu-id="fef92-112">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="fef92-113">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="fef92-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fef92-114">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="fef92-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DirectDownload`**

  <span data-ttu-id="fef92-115">*(4.0 +)* Baixa pacotes diretamente sem preencher os caches com binários ou metadados.</span><span class="sxs-lookup"><span data-stu-id="fef92-115">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span>

- **`-DisableParallelProcessing`**

   <span data-ttu-id="fef92-116">Desabilita a restauração de vários pacotes em paralelo.</span><span class="sxs-lookup"><span data-stu-id="fef92-116">Disables restoring multiple packages in parallel.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="fef92-117">*(3,2 +)* Uma lista de origens do pacote a ser usada como fallbacks caso o pacote não seja encontrado na fonte primária ou padrão.</span><span class="sxs-lookup"><span data-stu-id="fef92-117">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> <span data-ttu-id="fef92-118">Use um ponto e vírgula para separar entradas de lista.</span><span class="sxs-lookup"><span data-stu-id="fef92-118">Use a semicolon to separate list entries.</span></span>

- **`-Force`**

  <span data-ttu-id="fef92-119">Em projetos baseados em PackageReference, o forçará a resolução de todas as dependências, mesmo que a última restauração tenha sido bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="fef92-119">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="fef92-120">A especificação desse sinalizador é semelhante à exclusão do `project.assets.json` arquivo.</span><span class="sxs-lookup"><span data-stu-id="fef92-120">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="fef92-121">Isso não ignora o cache http.</span><span class="sxs-lookup"><span data-stu-id="fef92-121">This does not bypass the http-cache.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="fef92-122">*(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="fef92-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-ForceEvaluate`**

  <span data-ttu-id="fef92-123">Força a restauração a reavaliar todas as dependências mesmo se um arquivo de bloqueio já existir.</span><span class="sxs-lookup"><span data-stu-id="fef92-123">Forces restore to reevaluate all dependencies even if a lock file already exists.</span></span>

- **`-?|-help`**

  <span data-ttu-id="fef92-124">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="fef92-124">Displays help information for the command.</span></span>

- **`-LockFilePath`**

  <span data-ttu-id="fef92-125">Local de saída onde o arquivo de bloqueio do projeto é gravado.</span><span class="sxs-lookup"><span data-stu-id="fef92-125">Output location where project lock file is written.</span></span> <span data-ttu-id="fef92-126">Por padrão, é `PROJECT_ROOT\packages.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="fef92-126">By default, this is `PROJECT_ROOT\packages.lock.json`.</span></span>

- **`-LockedMode`**

  <span data-ttu-id="fef92-127">Não permitir atualização do arquivo de bloqueio do projeto.</span><span class="sxs-lookup"><span data-stu-id="fef92-127">Don't allow updating project lock file.</span></span>

- **`-MSBuildPath`**

   <span data-ttu-id="fef92-128">*(4.0 +)* Especifica o caminho do MSBuild a ser usado com o comando, tendo precedência sobre `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="fef92-128">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="fef92-129">*(3,2 +)* Especifica a versão do MSBuild a ser usada com este comando.</span><span class="sxs-lookup"><span data-stu-id="fef92-129">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="fef92-130">Os valores com suporte são 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="fef92-130">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="fef92-131">Por padrão, o MSBuild em seu caminho é escolhido; caso contrário, ele usa a versão mais recente instalada do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="fef92-131">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoCache`**

  <span data-ttu-id="fef92-132">Impede que o NuGet use pacotes armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="fef92-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="fef92-133">Consulte [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="fef92-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="fef92-134">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="fef92-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="fef92-135">Especifica a pasta na qual os pacotes são instalados.</span><span class="sxs-lookup"><span data-stu-id="fef92-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="fef92-136">Se nenhuma pasta for especificada, a pasta atual será usada.</span><span class="sxs-lookup"><span data-stu-id="fef92-136">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="fef92-137">Necessário ao restaurar com um `packages.config` arquivo, a menos que `PackagesDirectory` ou `SolutionDirectory` seja usado.</span><span class="sxs-lookup"><span data-stu-id="fef92-137">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="fef92-138">Especifica os tipos de arquivos a serem salvos após a instalação do pacote: um dos `nuspec` , `nupkg` ou `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="fef92-138">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="fef92-139">Mesmo que `OutputDirectory`.</span><span class="sxs-lookup"><span data-stu-id="fef92-139">Same as `OutputDirectory`.</span></span> <span data-ttu-id="fef92-140">Necessário ao restaurar com um `packages.config` arquivo, a menos que `OutputDirectory` ou `SolutionDirectory` seja usado.</span><span class="sxs-lookup"><span data-stu-id="fef92-140">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span>

- **`-Project2ProjectTimeOut`**

  <span data-ttu-id="fef92-141">Tempo limite em segundos para resolver referências de projeto para projeto.</span><span class="sxs-lookup"><span data-stu-id="fef92-141">Timeout in seconds for resolving project-to-project references.</span></span>

- **`-Recursive`**

  <span data-ttu-id="fef92-142">*(4.0 +)* Restaura todos os projetos de referência para projetos UWP e .NET Core.</span><span class="sxs-lookup"><span data-stu-id="fef92-142">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="fef92-143">Não se aplica a projetos que usam o `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="fef92-143">Does not apply to projects using `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="fef92-144">Verifica se a restauração de pacotes está habilitada antes de baixar e instalar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="fef92-144">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="fef92-145">Para obter detalhes, consulte [restauração de pacote](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="fef92-145">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="fef92-146">Especifica a pasta da solução.</span><span class="sxs-lookup"><span data-stu-id="fef92-146">Specifies the solution folder.</span></span> <span data-ttu-id="fef92-147">Não é válido ao restaurar pacotes para uma solução.</span><span class="sxs-lookup"><span data-stu-id="fef92-147">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="fef92-148">Necessário ao restaurar com um `packages.config` arquivo, a menos que `PackagesDirectory` ou `OutputDirectory` seja usado.</span><span class="sxs-lookup"><span data-stu-id="fef92-148">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span>

- **`-Source`**

  <span data-ttu-id="fef92-149">Especifica a lista de origens do pacote (como URLs) a serem usadas para a restauração.</span><span class="sxs-lookup"><span data-stu-id="fef92-149">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="fef92-150">Se omitido, o comando usará as fontes fornecidas em arquivos de configuração, consulte [Configurando o comportamento do NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="fef92-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="fef92-151">Use um ponto e vírgula para separar entradas de lista.</span><span class="sxs-lookup"><span data-stu-id="fef92-151">Use a semicolon to separate list entries.</span></span>

- **`-UseLockFile`**

  <span data-ttu-id="fef92-152">Habilita o arquivo de bloqueio do projeto a ser gerado e usado com a restauração.</span><span class="sxs-lookup"><span data-stu-id="fef92-152">Enables project lock file to be generated and used with restore.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="fef92-153">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="fef92-153">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="fef92-154">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fef92-154">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="fef92-155">Comentários</span><span class="sxs-lookup"><span data-stu-id="fef92-155">Remarks</span></span>

<span data-ttu-id="fef92-156">O comando Restore executa as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="fef92-156">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="fef92-157">Determine o modo de operação do comando Restore.</span><span class="sxs-lookup"><span data-stu-id="fef92-157">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="fef92-158">tipo de arquivo projectPath</span><span class="sxs-lookup"><span data-stu-id="fef92-158">projectPath file type</span></span> | <span data-ttu-id="fef92-159">Comportamento</span><span class="sxs-lookup"><span data-stu-id="fef92-159">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="fef92-160">Solução (pasta)</span><span class="sxs-lookup"><span data-stu-id="fef92-160">Solution (folder)</span></span> | <span data-ttu-id="fef92-161">O NuGet procura um `.sln` arquivo e usa-o, se for encontrado; caso contrário, retornará um erro.</span><span class="sxs-lookup"><span data-stu-id="fef92-161">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="fef92-162">`(SolutionDir)\.nuget` é usado como a pasta inicial.</span><span class="sxs-lookup"><span data-stu-id="fef92-162">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="fef92-163">Arquivo `.sln`</span><span class="sxs-lookup"><span data-stu-id="fef92-163">`.sln` file</span></span> | <span data-ttu-id="fef92-164">Restaurar os pacotes identificados pela solução; retornará um erro se `-SolutionDirectory` for usado.</span><span class="sxs-lookup"><span data-stu-id="fef92-164">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="fef92-165">`$(SolutionDir)\.nuget` é usado como a pasta inicial.</span><span class="sxs-lookup"><span data-stu-id="fef92-165">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="fef92-166">`packages.config` ou arquivo de projeto</span><span class="sxs-lookup"><span data-stu-id="fef92-166">`packages.config` or project file</span></span> | <span data-ttu-id="fef92-167">Restaure os pacotes listados no arquivo, resolvendo e instalando dependências.</span><span class="sxs-lookup"><span data-stu-id="fef92-167">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="fef92-168">Outro tipo de arquivo</span><span class="sxs-lookup"><span data-stu-id="fef92-168">Other file type</span></span> | <span data-ttu-id="fef92-169">O arquivo deve ser um `.sln` arquivo como acima; se não for uma solução, o NuGet fornecerá um erro.</span><span class="sxs-lookup"><span data-stu-id="fef92-169">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="fef92-170">(projectPath não especificado)</span><span class="sxs-lookup"><span data-stu-id="fef92-170">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="fef92-171">O NuGet procura arquivos de solução na pasta atual.</span><span class="sxs-lookup"><span data-stu-id="fef92-171">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="fef92-172">Se um único arquivo for encontrado, ele será usado para restaurar pacotes; se várias soluções forem encontradas, o NuGet fornecerá um erro.</span><span class="sxs-lookup"><span data-stu-id="fef92-172">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="fef92-173">Se não houver arquivos de solução, o NuGet procurará por um `packages.config` e o usará para restaurar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="fef92-173">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="fef92-174">Se nenhuma solução ou `packages.config` arquivo for encontrado, o NuGet fornecerá um erro.</span><span class="sxs-lookup"><span data-stu-id="fef92-174">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="fef92-175">Determine a pasta pacotes usando a seguinte ordem de prioridade (o NuGet fornecerá um erro se nenhuma dessas pastas for encontrada):</span><span class="sxs-lookup"><span data-stu-id="fef92-175">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="fef92-176">A pasta especificada com `-PackagesDirectory` .</span><span class="sxs-lookup"><span data-stu-id="fef92-176">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="fef92-177">O `repositoryPath` valor em `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="fef92-177">The `repositoryPath` value in `Nuget.Config`</span></span>
    - <span data-ttu-id="fef92-178">A pasta especificada com `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="fef92-178">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="fef92-179">Ao restaurar pacotes para uma solução, o NuGet faz o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fef92-179">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="fef92-180">Carrega o arquivo de solução.</span><span class="sxs-lookup"><span data-stu-id="fef92-180">Loads the solution file.</span></span>
    - <span data-ttu-id="fef92-181">Restaura os pacotes de nível de solução listados na `$(SolutionDir)\.nuget\packages.config` `packages` pasta.</span><span class="sxs-lookup"><span data-stu-id="fef92-181">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="fef92-182">Restaure os pacotes listados na `$(ProjectDir)\packages.config` `packages` pasta.</span><span class="sxs-lookup"><span data-stu-id="fef92-182">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="fef92-183">Para cada pacote especificado, restaure o pacote em paralelo, a menos que `-DisableParallelProcessing` seja especificado.</span><span class="sxs-lookup"><span data-stu-id="fef92-183">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="fef92-184">Exemplos</span><span class="sxs-lookup"><span data-stu-id="fef92-184">Examples</span></span>

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
