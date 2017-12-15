---
title: "Comando de restauração do NuGet CLI | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee41020-e548-4e61-b8cd-c82b77ac6af7
description: "Referência do comando de restauração de nuget.exe"
keywords: "NuGet restaure referência, restaure o comando de pacotes"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b435a3c2ffe08e3c2f8fc6a4dacb06cf674e4fb9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="ccdbd-104">comando de restauração (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ccdbd-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="ccdbd-105">**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="ccdbd-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="ccdbd-106">NuGet 2.7 +: Baixa e instala todos os pacotes ausentes no `packages` pasta.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-106">NuGet 2.7+: Downloads and installs any packages missing from the `packages` folder.</span></span>

<span data-ttu-id="ccdbd-107">NuGet 3.3 + com projetos usando o `project.json`: gera um `project.lock.json` arquivo e um `<project>.nuget.props` de arquivo, se necessário.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-107">NuGet 3.3+ with projects using `project.json`: Generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="ccdbd-108">(Os dois arquivos podem ser omitidos do controle de origem).</span><span class="sxs-lookup"><span data-stu-id="ccdbd-108">(Both files can be omitted from source control.)</span></span>

<span data-ttu-id="ccdbd-109">NuGet 4.0 e posteriores com o projeto no qual pacote de referências são incluídas no arquivo de projeto diretamente: gera um `<project>.nuget.props` de arquivos, se necessário, o `obj` pasta.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-109">NuGet 4.0+ with project in which package references are included in the project file directly: Generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="ccdbd-110">(O arquivo pode ser omitido do controle de origem).</span><span class="sxs-lookup"><span data-stu-id="ccdbd-110">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="ccdbd-111">Mac OSX e Linux com a CLI em Mono, restaurando os pacotes não há suporte para o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-111">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with the PackageReference format.</span></span>

## <a name="usage"></a><span data-ttu-id="ccdbd-112">Uso</span><span class="sxs-lookup"><span data-stu-id="ccdbd-112">Usage</span></span>

```
nuget restore <projectPath> [options]
```

<span data-ttu-id="ccdbd-113">onde `<projectPath>` Especifica o local de uma solução, uma `packages.config` arquivo, ou um `project.json` arquivo.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-113">where `<projectPath>` specifies the location of a solution, a `packages.config` file, or a `project.json` file.</span></span> <span data-ttu-id="ccdbd-114">Consulte [comentários](#remarks) abaixo para obter detalhes de comportamentos.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-114">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="ccdbd-115">Opções</span><span class="sxs-lookup"><span data-stu-id="ccdbd-115">Options</span></span>

| <span data-ttu-id="ccdbd-116">Opção</span><span class="sxs-lookup"><span data-stu-id="ccdbd-116">Option</span></span> | <span data-ttu-id="ccdbd-117">Descrição</span><span class="sxs-lookup"><span data-stu-id="ccdbd-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ccdbd-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ccdbd-118">ConfigFile</span></span> | <span data-ttu-id="ccdbd-119">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ccdbd-120">Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="ccdbd-121">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="ccdbd-121">DirectDownload</span></span> | <span data-ttu-id="ccdbd-122">*(4.0 +)*  Baixa pacotes diretamente sem populá caches com binários ou metadados.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-122">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="ccdbd-123">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="ccdbd-123">DisableParallelProcessing</span></span> | <span data-ttu-id="ccdbd-124">Desabilita a restauração de vários pacotes em paralelo.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-124">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="ccdbd-125">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="ccdbd-125">FallbackSource</span></span> | <span data-ttu-id="ccdbd-126">*(3.2 +)*  Uma lista de fontes de pacote para usar como fallbacks caso o pacote não foi encontrado no primário ou a fonte padrão.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-126">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="ccdbd-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ccdbd-127">ForceEnglishOutput</span></span> | <span data-ttu-id="ccdbd-128">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ccdbd-129">Ajuda</span><span class="sxs-lookup"><span data-stu-id="ccdbd-129">Help</span></span> | <span data-ttu-id="ccdbd-130">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="ccdbd-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="ccdbd-131">MSBuildPath</span></span> | <span data-ttu-id="ccdbd-132">*(4.0 +)*  Especifica o caminho do MSBuild para usar com o comando tendo precedência sobre `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="ccdbd-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="ccdbd-133">MSBuildVersion</span></span> | <span data-ttu-id="ccdbd-134">*(3.2 +)*  Especifica a versão do MSBuild a ser usado com este comando.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="ccdbd-135">Valores com suporte são 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-135">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="ccdbd-136">Por padrão que o MSBuild em seu caminho é separado, caso contrário, o padrão é a versão mais recente instalada do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="ccdbd-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="ccdbd-137">NoCache</span></span> | <span data-ttu-id="ccdbd-138">Impede que o NuGet usando pacotes de caches de computador local.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="ccdbd-139">Não interativo</span><span class="sxs-lookup"><span data-stu-id="ccdbd-139">NonInteractive</span></span> | <span data-ttu-id="ccdbd-140">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ccdbd-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="ccdbd-141">OutputDirectory</span></span> | <span data-ttu-id="ccdbd-142">Especifica a pasta na qual os pacotes são instalados.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="ccdbd-143">Se nenhuma pasta for especificada, a pasta atual será usada.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="ccdbd-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="ccdbd-144">PackageSaveMode</span></span> | <span data-ttu-id="ccdbd-145">Especifica os tipos de arquivos para salvar após a instalação do pacote: um dos `nuspec`, `nupkg`, ou `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="ccdbd-146">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="ccdbd-146">PackagesDirectory</span></span> | <span data-ttu-id="ccdbd-147">Mesmo que `OutputDirectory`.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-147">Same as `OutputDirectory`.</span></span> |
| <span data-ttu-id="ccdbd-148">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="ccdbd-148">Project2ProjectTimeOut</span></span> | <span data-ttu-id="ccdbd-149">Tempo limite em segundos para resolver referências de projeto ao projeto.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-149">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="ccdbd-150">Recursiva</span><span class="sxs-lookup"><span data-stu-id="ccdbd-150">Recursive</span></span> | <span data-ttu-id="ccdbd-151">*(4.0 +)*  Restaura todos os projetos de referências para os projetos UWP e .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-151">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="ccdbd-152">Não se aplicam a projetos usando `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-152">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="ccdbd-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="ccdbd-153">RequireConsent</span></span> | <span data-ttu-id="ccdbd-154">Verifica se a restauração de pacotes é habilitado antes de baixar e instalar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="ccdbd-155">Para obter detalhes, consulte [restauração do pacote](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="ccdbd-155">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="ccdbd-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="ccdbd-156">SolutionDirectory</span></span> | <span data-ttu-id="ccdbd-157">Especifica a pasta de solução.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-157">Specifies the solution folder.</span></span> <span data-ttu-id="ccdbd-158">Não é válido ao restaurar pacotes para uma solução.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-158">Not valid when restoring packages for a solution.</span></span> |
| <span data-ttu-id="ccdbd-159">Origem</span><span class="sxs-lookup"><span data-stu-id="ccdbd-159">Source</span></span> | <span data-ttu-id="ccdbd-160">Especifica a lista de fontes de pacote (como URLs) para usar para a restauração.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-160">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="ccdbd-161">Se omitido, o comando usa as fontes fornecidas nos arquivos de configuração, consulte [NuGet Configurando comportamento](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ccdbd-161">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="ccdbd-162">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="ccdbd-162">Verbosity</span></span> |<span data-ttu-id="ccdbd-163">> especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-163">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="ccdbd-164">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ccdbd-164">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="ccdbd-165">Comentários</span><span class="sxs-lookup"><span data-stu-id="ccdbd-165">Remarks</span></span>

<span data-ttu-id="ccdbd-166">O comando restore executa as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ccdbd-166">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="ccdbd-167">Determine o modo de operação do comando restore.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-167">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="ccdbd-168">tipo de arquivo projectPath</span><span class="sxs-lookup"><span data-stu-id="ccdbd-168">projectPath file type</span></span> | <span data-ttu-id="ccdbd-169">Comportamento</span><span class="sxs-lookup"><span data-stu-id="ccdbd-169">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="ccdbd-170">Solução (pasta)</span><span class="sxs-lookup"><span data-stu-id="ccdbd-170">Solution (folder)</span></span> | <span data-ttu-id="ccdbd-171">NuGet procura um `.sln` de arquivo e usa esse encontrado; caso contrário, retorna um erro.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-171">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="ccdbd-172">`(SolutionDir)\.nuget`é usado como a pasta inicial.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-172">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="ccdbd-173">`.sln`arquivo</span><span class="sxs-lookup"><span data-stu-id="ccdbd-173">`.sln` file</span></span> | <span data-ttu-id="ccdbd-174">Restaurar os pacotes identificados pela solução; gera um erro se `-SolutionDirectory` é usado.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-174">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="ccdbd-175">`$(SolutionDir)\.nuget`é usado como a pasta inicial.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-175">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="ccdbd-176">`packages.config`, `project.json`, ou arquivo de projeto</span><span class="sxs-lookup"><span data-stu-id="ccdbd-176">`packages.config`, `project.json`, or project file</span></span> | <span data-ttu-id="ccdbd-177">Restaure os pacotes listados no arquivo, resolvendo e instalando dependências.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-177">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="ccdbd-178">Outro tipo de arquivo</span><span class="sxs-lookup"><span data-stu-id="ccdbd-178">Other file type</span></span> | <span data-ttu-id="ccdbd-179">Arquivo é considerado um `.sln` arquivo acima; se não for uma solução, o NuGet fornece um erro.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-179">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="ccdbd-180">(projectPath não especificado)</span><span class="sxs-lookup"><span data-stu-id="ccdbd-180">(projectPath not specified)</span></span> | <span data-ttu-id="ccdbd-181">-NuGet procura por arquivos de solução na pasta atual.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-181">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="ccdbd-182">Se for encontrado um único arquivo, que é usado para restaurar os pacotes; Se várias soluções forem encontradas, o NuGet apresentará um erro.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-182">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="ccdbd-183">-Se não houver nenhum arquivo de solução, o NuGet procura um `packages.config` ou `project.json` e a usa para restaurar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-183">- If there are no solution files, NuGet looks for a `packages.config` or `project.json` and uses that to restore packages.</span></span>
    |<span data-ttu-id="ccdbd-184">-Se nenhum arquivo de solução, `packages.config`, ou `project.json` for encontrado, o NuGet apresentará um erro.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-184">- If no solution file, `packages.config`, or `project.json` is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="ccdbd-185">Determine a pasta de pacotes usando a seguinte ordem de prioridade (NuGet apresentará um erro se nenhuma dessas pastas são encontradas):</span><span class="sxs-lookup"><span data-stu-id="ccdbd-185">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="ccdbd-186">O `%userprofile%\.nuget\packages` valor em `project.json`.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-186">The `%userprofile%\.nuget\packages` value in `project.json`.</span></span>
    - <span data-ttu-id="ccdbd-187">A pasta especificada com `-PackagesDirectory`.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-187">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="ccdbd-188">O `repositoryPath` vale em`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="ccdbd-188">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="ccdbd-189">A pasta especificada com`-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="ccdbd-189">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="ccdbd-190">Ao restaurar pacotes para uma solução, o NuGet faz o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ccdbd-190">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="ccdbd-191">Carrega o arquivo de solução.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-191">Loads the solution file.</span></span>
    - <span data-ttu-id="ccdbd-192">Restaura os pacotes de nível de solução listados na `$(SolutionDir)\.nuget\packages.config` para o `packages` pasta.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-192">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="ccdbd-193">Restaurar os pacotes listados na `$(ProjectDir)\packages.config` para o `packages` pasta.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-193">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="ccdbd-194">Para cada pacote especificado, restaurar o pacote em paralelo, a menos que `-DisableParallelProcessing` for especificado.</span><span class="sxs-lookup"><span data-stu-id="ccdbd-194">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="ccdbd-195">Exemplos</span><span class="sxs-lookup"><span data-stu-id="ccdbd-195">Examples</span></span>

```
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
