---
title: Comando de atualização da CLI do NuGet
description: Referência para o comando de atualização NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327503"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="a0926-103">Commando update (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a0926-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="a0926-104">**Aplica-se a:** &bullet; **versões com suporte** do consumo do pacote: todas</span><span class="sxs-lookup"><span data-stu-id="a0926-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a0926-105">Atualiza todos os pacotes de um projeto (usando `packages.config`) para as últimas versões disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a0926-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="a0926-106">É recomendável executar [' Restore '](cli-ref-restore.md) antes de executar `update`o.</span><span class="sxs-lookup"><span data-stu-id="a0926-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="a0926-107">(Para atualizar um pacote individual, use [`nuget install`](cli-ref-install.md) sem especificar um número de versão, caso em que o NuGet instala a versão mais recente.)</span><span class="sxs-lookup"><span data-stu-id="a0926-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="a0926-108">Observação: `update` o não funciona com a CLI em execução em mono (Mac OSX ou Linux) ou ao usar o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="a0926-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="a0926-109">O `update` comando também atualiza referências de assembly no arquivo de projeto, desde que essas referências já existam.</span><span class="sxs-lookup"><span data-stu-id="a0926-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="a0926-110">Se um pacote atualizado tiver um assembly adicionado, uma nova referência *não* será adicionada.</span><span class="sxs-lookup"><span data-stu-id="a0926-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="a0926-111">Novas dependências de pacote também não têm suas referências de assembly adicionadas.</span><span class="sxs-lookup"><span data-stu-id="a0926-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="a0926-112">Para incluir essas operações como parte de uma atualização, atualize o pacote no Visual Studio usando a interface do usuário do Gerenciador de pacotes ou o console do Gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="a0926-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="a0926-113">Esse comando também pode ser usado para atualizar o NuGet. exe usando o sinalizador *-Self* .</span><span class="sxs-lookup"><span data-stu-id="a0926-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="a0926-114">Uso</span><span class="sxs-lookup"><span data-stu-id="a0926-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="a0926-115">onde `<configPath>` o identifica um `packages.config` arquivo de solução ou que lista as dependências do projeto.</span><span class="sxs-lookup"><span data-stu-id="a0926-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="a0926-116">Opções</span><span class="sxs-lookup"><span data-stu-id="a0926-116">Options</span></span>

| <span data-ttu-id="a0926-117">Opção</span><span class="sxs-lookup"><span data-stu-id="a0926-117">Option</span></span> | <span data-ttu-id="a0926-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="a0926-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a0926-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a0926-119">ConfigFile</span></span> | <span data-ttu-id="a0926-120">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="a0926-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a0926-121">Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="a0926-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a0926-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="a0926-122">FileConflictAction</span></span> | <span data-ttu-id="a0926-123">Especifica a ação a ser tomada quando solicitado a substituir ou ignorar os arquivos existentes referenciados pelo projeto.</span><span class="sxs-lookup"><span data-stu-id="a0926-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="a0926-124">Os valores são *substituir, ignorar, nenhum*.</span><span class="sxs-lookup"><span data-stu-id="a0926-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="a0926-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a0926-125">ForceEnglishOutput</span></span> | <span data-ttu-id="a0926-126">*(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="a0926-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a0926-127">Help</span><span class="sxs-lookup"><span data-stu-id="a0926-127">Help</span></span> | <span data-ttu-id="a0926-128">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="a0926-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="a0926-129">Id</span><span class="sxs-lookup"><span data-stu-id="a0926-129">Id</span></span> | <span data-ttu-id="a0926-130">Especifica uma lista de IDs de pacote a serem atualizadas.</span><span class="sxs-lookup"><span data-stu-id="a0926-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="a0926-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="a0926-131">MSBuildPath</span></span> | <span data-ttu-id="a0926-132">*(4.0 +)* Especifica o caminho do MSBuild a ser usado com o comando, tendo precedência sobre `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="a0926-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="a0926-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="a0926-133">MSBuildVersion</span></span> | <span data-ttu-id="a0926-134">*(3,2 +)* Especifica a versão do MSBuild a ser usada com este comando.</span><span class="sxs-lookup"><span data-stu-id="a0926-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="a0926-135">Os valores com suporte são 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="a0926-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="a0926-136">Por padrão, o MSBuild em seu caminho é escolhido; caso contrário, ele usa a versão mais recente instalada do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="a0926-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="a0926-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a0926-137">NonInteractive</span></span> | <span data-ttu-id="a0926-138">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="a0926-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a0926-139">Pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="a0926-139">PreRelease</span></span> | <span data-ttu-id="a0926-140">Permite atualizar para versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="a0926-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="a0926-141">Esse sinalizador não é necessário ao atualizar pacotes de pré-lançamento que já estão instalados.</span><span class="sxs-lookup"><span data-stu-id="a0926-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="a0926-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="a0926-142">RepositoryPath</span></span> | <span data-ttu-id="a0926-143">Especifica a pasta local onde os pacotes são instalados.</span><span class="sxs-lookup"><span data-stu-id="a0926-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="a0926-144">Removidos</span><span class="sxs-lookup"><span data-stu-id="a0926-144">Safe</span></span> | <span data-ttu-id="a0926-145">Especifica que somente as atualizações com a versão mais recente disponível na mesma versão principal e secundária do pacote instalado serão instaladas.</span><span class="sxs-lookup"><span data-stu-id="a0926-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="a0926-146">Auto-restauração</span><span class="sxs-lookup"><span data-stu-id="a0926-146">Self</span></span> | <span data-ttu-id="a0926-147">Atualiza o NuGet. exe para a versão mais recente; todos os outros argumentos são ignorados.</span><span class="sxs-lookup"><span data-stu-id="a0926-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="a0926-148">Origem</span><span class="sxs-lookup"><span data-stu-id="a0926-148">Source</span></span> | <span data-ttu-id="a0926-149">Especifica a lista de origens do pacote (como URLs) a serem usadas para as atualizações.</span><span class="sxs-lookup"><span data-stu-id="a0926-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="a0926-150">Se omitido, o comando usará as fontes fornecidas em arquivos de configuração, consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="a0926-150">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="a0926-151">Verbosity</span><span class="sxs-lookup"><span data-stu-id="a0926-151">Verbosity</span></span> | <span data-ttu-id="a0926-152">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="a0926-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="a0926-153">Versão</span><span class="sxs-lookup"><span data-stu-id="a0926-153">Version</span></span> | <span data-ttu-id="a0926-154">Quando usado com uma ID de pacote, especifica a versão do pacote a ser atualizada.</span><span class="sxs-lookup"><span data-stu-id="a0926-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="a0926-155">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a0926-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a0926-156">Exemplos</span><span class="sxs-lookup"><span data-stu-id="a0926-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
