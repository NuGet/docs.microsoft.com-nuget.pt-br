---
title: Comando de atualização da CLI do NuGet
description: Referência para o comando nuget.exe Update
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323642"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="3b7db-103">comando Update (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3b7db-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="3b7db-104">**Aplica-se a:** &bullet; **versões com suporte** do consumo do pacote: todas</span><span class="sxs-lookup"><span data-stu-id="3b7db-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="3b7db-105">Atualiza todos os pacotes de um projeto (usando `packages.config`) para as últimas versões disponíveis.</span><span class="sxs-lookup"><span data-stu-id="3b7db-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="3b7db-106">É recomendável executar [' Restore '](cli-ref-restore.md) antes de executar o `update` .</span><span class="sxs-lookup"><span data-stu-id="3b7db-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="3b7db-107">(Para atualizar um pacote individual, use [`nuget install`](cli-ref-install.md) sem especificar um número de versão, caso em que o NuGet instala a versão mais recente.)</span><span class="sxs-lookup"><span data-stu-id="3b7db-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="3b7db-108">Observação: `update` o não funciona com a CLI em execução em mono (Mac OSX ou Linux) ou ao usar o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3b7db-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="3b7db-109">O `update` comando também atualiza referências de assembly no arquivo de projeto, desde que essas referências já existam.</span><span class="sxs-lookup"><span data-stu-id="3b7db-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="3b7db-110">Se um pacote atualizado tiver um assembly adicionado, uma nova referência *não* será adicionada.</span><span class="sxs-lookup"><span data-stu-id="3b7db-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="3b7db-111">Novas dependências de pacote também não têm suas referências de assembly adicionadas.</span><span class="sxs-lookup"><span data-stu-id="3b7db-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="3b7db-112">Para incluir essas operações como parte de uma atualização, atualize o pacote no Visual Studio usando a interface do usuário do Gerenciador de pacotes ou o console do Gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="3b7db-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="3b7db-113">Esse comando também pode ser usado para atualizar nuget.exe si mesmo usando o sinalizador *-Self* .</span><span class="sxs-lookup"><span data-stu-id="3b7db-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="3b7db-114">Uso</span><span class="sxs-lookup"><span data-stu-id="3b7db-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="3b7db-115">onde `<configPath>` o identifica um `packages.config` arquivo de solução ou que lista as dependências do projeto.</span><span class="sxs-lookup"><span data-stu-id="3b7db-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="3b7db-116">Opções</span><span class="sxs-lookup"><span data-stu-id="3b7db-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="3b7db-117">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="3b7db-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3b7db-118">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="3b7db-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  <span data-ttu-id="3b7db-119">Especifica a versão dos pacotes de dependência a serem usados, que pode ser um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="3b7db-119">Specifies the version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="3b7db-120">*Mais baixo* (padrão): a versão mais baixa</span><span class="sxs-lookup"><span data-stu-id="3b7db-120">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="3b7db-121">*HighestPatch*: a versão com o menor principal, menor o mais baixo, patch mais alto</span><span class="sxs-lookup"><span data-stu-id="3b7db-121">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="3b7db-122">*HighestMinor*: a versão com o menor principal, o mais baixo, o patch mais alto</span><span class="sxs-lookup"><span data-stu-id="3b7db-122">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="3b7db-123">*Mais alto*: a versão mais recente</span><span class="sxs-lookup"><span data-stu-id="3b7db-123">*Highest*: the highest version</span></span></li><li><span data-ttu-id="3b7db-124">*Ignorar*: nenhum pacote de dependência será usado</span><span class="sxs-lookup"><span data-stu-id="3b7db-124">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="3b7db-125">Especifica a ação padrão quando um arquivo de um pacote já existe no projeto de destino.</span><span class="sxs-lookup"><span data-stu-id="3b7db-125">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="3b7db-126">Defina como `Overwrite` para sempre substituir arquivos.</span><span class="sxs-lookup"><span data-stu-id="3b7db-126">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="3b7db-127">Defina como `Ignore` para ignorar arquivos.</span><span class="sxs-lookup"><span data-stu-id="3b7db-127">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="3b7db-128">A `PromptUser` ação, o padrão, solicitará cada arquivo conflitante, a menos que `OverwriteAll` ou `IgnoreAll` seja fornecido, que será aplicado a todos os arquivos restantes.</span><span class="sxs-lookup"><span data-stu-id="3b7db-128">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="3b7db-129">*(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="3b7db-129">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="3b7db-130">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="3b7db-130">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="3b7db-131">Especifica uma lista de IDs de pacote a serem atualizadas.</span><span class="sxs-lookup"><span data-stu-id="3b7db-131">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="3b7db-132">*(4.0 +)* Especifica o caminho do MSBuild a ser usado com o comando, tendo precedência sobre `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="3b7db-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="3b7db-133">*(3,2 +)* Especifica a versão do MSBuild a ser usada com este comando.</span><span class="sxs-lookup"><span data-stu-id="3b7db-133">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="3b7db-134">Os valores com suporte são 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="3b7db-134">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="3b7db-135">Por padrão, o MSBuild em seu caminho é escolhido; caso contrário, ele usa a versão mais recente instalada do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3b7db-135">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="3b7db-136">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="3b7db-136">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="3b7db-137">Permite atualizar para versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="3b7db-137">Allows updating to prerelease versions.</span></span> <span data-ttu-id="3b7db-138">Esse sinalizador não é necessário ao atualizar pacotes de pré-lançamento que já estão instalados.</span><span class="sxs-lookup"><span data-stu-id="3b7db-138">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="3b7db-139">Especifica a pasta local onde os pacotes são instalados.</span><span class="sxs-lookup"><span data-stu-id="3b7db-139">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="3b7db-140">Especifica que somente as atualizações com a versão mais recente disponível na mesma versão principal e secundária do pacote instalado serão instaladas.</span><span class="sxs-lookup"><span data-stu-id="3b7db-140">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="3b7db-141">Atualizações `nuget.exe` para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="3b7db-141">Updates `nuget.exe` to the latest version.</span></span> <span data-ttu-id="3b7db-142">`-Source` pode ser usado no entanto, todos os outros argumentos são ignorados.</span><span class="sxs-lookup"><span data-stu-id="3b7db-142">`-Source` can be used however all other arguments are ignored.</span></span> <span data-ttu-id="3b7db-143">Se nenhuma fonte for fornecida, o verificará se há `nuget.org` atualizações, independentemente das `NuGet.Config` configurações.</span><span class="sxs-lookup"><span data-stu-id="3b7db-143">If no source is provided, checks `nuget.org` for updates regardless of `NuGet.Config` settings.</span></span>

- **`-Source`**

  <span data-ttu-id="3b7db-144">Especifica a lista de origens do pacote (como URLs) a serem usadas para as atualizações.</span><span class="sxs-lookup"><span data-stu-id="3b7db-144">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="3b7db-145">Se omitido, o comando usará as fontes fornecidas em arquivos de configuração, consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="3b7db-145">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="3b7db-146">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="3b7db-146">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="3b7db-147">Quando usado com uma ID de pacote, especifica a versão do pacote a ser atualizada.</span><span class="sxs-lookup"><span data-stu-id="3b7db-147">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="3b7db-148">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3b7db-148">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3b7db-149">Exemplos</span><span class="sxs-lookup"><span data-stu-id="3b7db-149">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
