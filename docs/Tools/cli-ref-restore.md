---
title: "Comando de restauração do NuGet CLI | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência do comando de restauração de nuget.exe"
keywords: "NuGet restaure referência, restaure o comando de pacotes"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 93d7b6967d9297ee822df1583351385210775173
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="04f54-104">comando de restauração (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="04f54-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="04f54-105">**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="04f54-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="04f54-106">Baixa e instala todos os pacotes ausentes no `packages` pasta.</span><span class="sxs-lookup"><span data-stu-id="04f54-106">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="04f54-107">Quando usado com o NuGet 4.0 + e o formato PackageReference, gera um `<project>.nuget.props` de arquivos, se necessário, o `obj` pasta.</span><span class="sxs-lookup"><span data-stu-id="04f54-107">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="04f54-108">(O arquivo pode ser omitido do controle de origem).</span><span class="sxs-lookup"><span data-stu-id="04f54-108">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="04f54-109">No Mac OSX e Linux com a CLI em Mono, restaurando os pacotes não tem suporte com PackageReference.</span><span class="sxs-lookup"><span data-stu-id="04f54-109">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="04f54-110">Uso</span><span class="sxs-lookup"><span data-stu-id="04f54-110">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="04f54-111">onde `<projectPath>` Especifica o local de uma solução ou um `packages.config` arquivo.</span><span class="sxs-lookup"><span data-stu-id="04f54-111">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="04f54-112">Consulte [comentários](#remarks) abaixo para obter detalhes de comportamentos.</span><span class="sxs-lookup"><span data-stu-id="04f54-112">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="04f54-113">Opções</span><span class="sxs-lookup"><span data-stu-id="04f54-113">Options</span></span>

| <span data-ttu-id="04f54-114">Opção</span><span class="sxs-lookup"><span data-stu-id="04f54-114">Option</span></span> | <span data-ttu-id="04f54-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="04f54-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="04f54-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="04f54-116">ConfigFile</span></span> | <span data-ttu-id="04f54-117">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="04f54-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="04f54-118">Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado.</span><span class="sxs-lookup"><span data-stu-id="04f54-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="04f54-119">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="04f54-119">DirectDownload</span></span> | <span data-ttu-id="04f54-120">*(4.0 +)*  Baixa pacotes diretamente sem populá caches com binários ou metadados.</span><span class="sxs-lookup"><span data-stu-id="04f54-120">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="04f54-121">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="04f54-121">DisableParallelProcessing</span></span> | <span data-ttu-id="04f54-122">Desabilita a restauração de vários pacotes em paralelo.</span><span class="sxs-lookup"><span data-stu-id="04f54-122">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="04f54-123">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="04f54-123">FallbackSource</span></span> | <span data-ttu-id="04f54-124">*(3.2 +)*  Uma lista de fontes de pacote para usar como fallbacks caso o pacote não foi encontrado no primário ou a fonte padrão.</span><span class="sxs-lookup"><span data-stu-id="04f54-124">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="04f54-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="04f54-125">ForceEnglishOutput</span></span> | <span data-ttu-id="04f54-126">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="04f54-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="04f54-127">Ajuda</span><span class="sxs-lookup"><span data-stu-id="04f54-127">Help</span></span> | <span data-ttu-id="04f54-128">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="04f54-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="04f54-129">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="04f54-129">MSBuildPath</span></span> | <span data-ttu-id="04f54-130">*(4.0 +)*  Especifica o caminho do MSBuild para usar com o comando tendo precedência sobre `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="04f54-130">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="04f54-131">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="04f54-131">MSBuildVersion</span></span> | <span data-ttu-id="04f54-132">*(3.2 +)*  Especifica a versão do MSBuild a ser usado com este comando.</span><span class="sxs-lookup"><span data-stu-id="04f54-132">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="04f54-133">Valores com suporte são 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="04f54-133">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="04f54-134">Por padrão que o MSBuild em seu caminho é separado, caso contrário, o padrão é a versão mais recente instalada do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="04f54-134">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="04f54-135">NoCache</span><span class="sxs-lookup"><span data-stu-id="04f54-135">NoCache</span></span> | <span data-ttu-id="04f54-136">Impede que o NuGet usando pacotes de caches de computador local.</span><span class="sxs-lookup"><span data-stu-id="04f54-136">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="04f54-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="04f54-137">NonInteractive</span></span> | <span data-ttu-id="04f54-138">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="04f54-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="04f54-139">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="04f54-139">OutputDirectory</span></span> | <span data-ttu-id="04f54-140">Especifica a pasta na qual os pacotes são instalados.</span><span class="sxs-lookup"><span data-stu-id="04f54-140">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="04f54-141">Se nenhuma pasta for especificada, a pasta atual será usada.</span><span class="sxs-lookup"><span data-stu-id="04f54-141">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="04f54-142">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="04f54-142">PackageSaveMode</span></span> | <span data-ttu-id="04f54-143">Especifica os tipos de arquivos para salvar após a instalação do pacote: um dos `nuspec`, `nupkg`, ou `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="04f54-143">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="04f54-144">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="04f54-144">PackagesDirectory</span></span> | <span data-ttu-id="04f54-145">Mesmo que `OutputDirectory`.</span><span class="sxs-lookup"><span data-stu-id="04f54-145">Same as `OutputDirectory`.</span></span> |
| <span data-ttu-id="04f54-146">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="04f54-146">Project2ProjectTimeOut</span></span> | <span data-ttu-id="04f54-147">Tempo limite em segundos para resolver referências de projeto ao projeto.</span><span class="sxs-lookup"><span data-stu-id="04f54-147">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="04f54-148">Recursiva</span><span class="sxs-lookup"><span data-stu-id="04f54-148">Recursive</span></span> | <span data-ttu-id="04f54-149">*(4.0 +)*  Restaura todos os projetos de referências para os projetos UWP e .NET Core.</span><span class="sxs-lookup"><span data-stu-id="04f54-149">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="04f54-150">Não se aplicam a projetos usando `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="04f54-150">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="04f54-151">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="04f54-151">RequireConsent</span></span> | <span data-ttu-id="04f54-152">Verifica se a restauração de pacotes é habilitado antes de baixar e instalar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="04f54-152">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="04f54-153">Para obter detalhes, consulte [restauração do pacote](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="04f54-153">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="04f54-154">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="04f54-154">SolutionDirectory</span></span> | <span data-ttu-id="04f54-155">Especifica a pasta de solução.</span><span class="sxs-lookup"><span data-stu-id="04f54-155">Specifies the solution folder.</span></span> <span data-ttu-id="04f54-156">Não é válido ao restaurar pacotes para uma solução.</span><span class="sxs-lookup"><span data-stu-id="04f54-156">Not valid when restoring packages for a solution.</span></span> |
| <span data-ttu-id="04f54-157">Origem</span><span class="sxs-lookup"><span data-stu-id="04f54-157">Source</span></span> | <span data-ttu-id="04f54-158">Especifica a lista de fontes de pacote (como URLs) para usar para a restauração.</span><span class="sxs-lookup"><span data-stu-id="04f54-158">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="04f54-159">Se omitido, o comando usa as fontes fornecidas nos arquivos de configuração, consulte [NuGet Configurando comportamento](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="04f54-159">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="04f54-160">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="04f54-160">Verbosity</span></span> |<span data-ttu-id="04f54-161">> especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="04f54-161">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="04f54-162">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="04f54-162">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="04f54-163">Comentários</span><span class="sxs-lookup"><span data-stu-id="04f54-163">Remarks</span></span>

<span data-ttu-id="04f54-164">O comando restore executa as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="04f54-164">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="04f54-165">Determine o modo de operação do comando restore.</span><span class="sxs-lookup"><span data-stu-id="04f54-165">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="04f54-166">tipo de arquivo projectPath</span><span class="sxs-lookup"><span data-stu-id="04f54-166">projectPath file type</span></span> | <span data-ttu-id="04f54-167">Comportamento</span><span class="sxs-lookup"><span data-stu-id="04f54-167">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="04f54-168">Solução (pasta)</span><span class="sxs-lookup"><span data-stu-id="04f54-168">Solution (folder)</span></span> | <span data-ttu-id="04f54-169">NuGet procura um `.sln` de arquivo e usa esse encontrado; caso contrário, retorna um erro.</span><span class="sxs-lookup"><span data-stu-id="04f54-169">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="04f54-170">`(SolutionDir)\.nuget`é usado como a pasta inicial.</span><span class="sxs-lookup"><span data-stu-id="04f54-170">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="04f54-171">`.sln`arquivo</span><span class="sxs-lookup"><span data-stu-id="04f54-171">`.sln` file</span></span> | <span data-ttu-id="04f54-172">Restaurar os pacotes identificados pela solução; gera um erro se `-SolutionDirectory` é usado.</span><span class="sxs-lookup"><span data-stu-id="04f54-172">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="04f54-173">`$(SolutionDir)\.nuget`é usado como a pasta inicial.</span><span class="sxs-lookup"><span data-stu-id="04f54-173">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="04f54-174">`packages.config`ou o arquivo de projeto</span><span class="sxs-lookup"><span data-stu-id="04f54-174">`packages.config` or project file</span></span> | <span data-ttu-id="04f54-175">Restaure os pacotes listados no arquivo, resolvendo e instalando dependências.</span><span class="sxs-lookup"><span data-stu-id="04f54-175">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="04f54-176">Outro tipo de arquivo</span><span class="sxs-lookup"><span data-stu-id="04f54-176">Other file type</span></span> | <span data-ttu-id="04f54-177">Arquivo é considerado um `.sln` arquivo acima; se não for uma solução, o NuGet fornece um erro.</span><span class="sxs-lookup"><span data-stu-id="04f54-177">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="04f54-178">(projectPath não especificado)</span><span class="sxs-lookup"><span data-stu-id="04f54-178">(projectPath not specified)</span></span> | <span data-ttu-id="04f54-179">-NuGet procura por arquivos de solução na pasta atual.</span><span class="sxs-lookup"><span data-stu-id="04f54-179">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="04f54-180">Se for encontrado um único arquivo, que é usado para restaurar os pacotes; Se várias soluções forem encontradas, o NuGet apresentará um erro.</span><span class="sxs-lookup"><span data-stu-id="04f54-180">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="04f54-181">-Se não houver nenhum arquivo de solução, o NuGet procura um `packages.config` e a usa para restaurar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="04f54-181">- If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span>
    |<span data-ttu-id="04f54-182">-Se não houver solução ou `packages.config` arquivo for encontrado, o NuGet apresentará um erro.</span><span class="sxs-lookup"><span data-stu-id="04f54-182">- If no solution or `packages.config` file is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="04f54-183">Determine a pasta de pacotes usando a seguinte ordem de prioridade (NuGet apresentará um erro se nenhuma dessas pastas são encontradas):</span><span class="sxs-lookup"><span data-stu-id="04f54-183">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="04f54-184">A pasta especificada com `-PackagesDirectory`.</span><span class="sxs-lookup"><span data-stu-id="04f54-184">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="04f54-185">O `repositoryPath` vale em`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="04f54-185">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="04f54-186">A pasta especificada com`-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="04f54-186">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="04f54-187">Ao restaurar pacotes para uma solução, o NuGet faz o seguinte:</span><span class="sxs-lookup"><span data-stu-id="04f54-187">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="04f54-188">Carrega o arquivo de solução.</span><span class="sxs-lookup"><span data-stu-id="04f54-188">Loads the solution file.</span></span>
    - <span data-ttu-id="04f54-189">Restaura os pacotes de nível de solução listados na `$(SolutionDir)\.nuget\packages.config` para o `packages` pasta.</span><span class="sxs-lookup"><span data-stu-id="04f54-189">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="04f54-190">Restaurar os pacotes listados na `$(ProjectDir)\packages.config` para o `packages` pasta.</span><span class="sxs-lookup"><span data-stu-id="04f54-190">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="04f54-191">Para cada pacote especificado, restaurar o pacote em paralelo, a menos que `-DisableParallelProcessing` for especificado.</span><span class="sxs-lookup"><span data-stu-id="04f54-191">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="04f54-192">Exemplos</span><span class="sxs-lookup"><span data-stu-id="04f54-192">Examples</span></span>

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
