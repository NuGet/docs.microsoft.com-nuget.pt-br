---
title: Comando de atualização de CLI do NuGet
description: Referência do comando de atualização nuget.exe
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ded9b571324d810c2f0e1a46ea76375a28940406
ms.sourcegitcommit: d5a35a097e6b461ae791d9f66b3a85d5219d7305
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56145599"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="f22f5-103">Commando update (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f22f5-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="f22f5-104">**Aplica-se a:** consumo do pacote &bullet; **versões com suporte:** todos os</span><span class="sxs-lookup"><span data-stu-id="f22f5-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f22f5-105">Atualiza todos os pacotes em um projeto (usando `packages.config`) para suas versões mais recentes disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f22f5-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="f22f5-106">É recomendável executar ['restore'](cli-ref-restore.md) antes de executar o `update`.</span><span class="sxs-lookup"><span data-stu-id="f22f5-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="f22f5-107">(Para atualizar um pacote individual, use [ `nuget install` ](cli-ref-install.md) sem especificar um número de versão, em que o NuGet caso instala a versão mais recente.)</span><span class="sxs-lookup"><span data-stu-id="f22f5-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="f22f5-108">Observação: `update` não funciona com a CLI executando em Mono (Mac OSX ou Linux) ou ao usar o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="f22f5-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="f22f5-109">O `update` comando também atualiza as referências de assembly no arquivo de projeto, desde aqueles faz referência já existir.</span><span class="sxs-lookup"><span data-stu-id="f22f5-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="f22f5-110">Se um pacote atualizado tiver um assembly adicionado, uma nova referência será *não* adicionado.</span><span class="sxs-lookup"><span data-stu-id="f22f5-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="f22f5-111">Novas dependências do pacote também não têm suas referências de assembly adicionadas.</span><span class="sxs-lookup"><span data-stu-id="f22f5-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="f22f5-112">Para incluir essas operações como parte de uma atualização, atualize o pacote no Visual Studio usando a UI do Gerenciador de pacotes ou o Console do Gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="f22f5-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="f22f5-113">Esse comando também pode ser usado para atualizar nuget.exe em si usando o *-self* sinalizador.</span><span class="sxs-lookup"><span data-stu-id="f22f5-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="f22f5-114">Uso</span><span class="sxs-lookup"><span data-stu-id="f22f5-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="f22f5-115">em que `<configPath>` identifica um uma `packages.config` ou arquivo de solução que lista as dependências do projeto.</span><span class="sxs-lookup"><span data-stu-id="f22f5-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="f22f5-116">Opções</span><span class="sxs-lookup"><span data-stu-id="f22f5-116">Options</span></span>

| <span data-ttu-id="f22f5-117">Opção</span><span class="sxs-lookup"><span data-stu-id="f22f5-117">Option</span></span> | <span data-ttu-id="f22f5-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="f22f5-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f22f5-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f22f5-119">ConfigFile</span></span> | <span data-ttu-id="f22f5-120">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="f22f5-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f22f5-121">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="f22f5-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f22f5-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="f22f5-122">FileConflictAction</span></span> | <span data-ttu-id="f22f5-123">Especifica a ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes, referenciados pelo projeto.</span><span class="sxs-lookup"><span data-stu-id="f22f5-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="f22f5-124">Os valores são *substituir, ignorar, nenhum*.</span><span class="sxs-lookup"><span data-stu-id="f22f5-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="f22f5-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f22f5-125">ForceEnglishOutput</span></span> | <span data-ttu-id="f22f5-126">*(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="f22f5-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f22f5-127">Ajuda</span><span class="sxs-lookup"><span data-stu-id="f22f5-127">Help</span></span> | <span data-ttu-id="f22f5-128">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="f22f5-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="f22f5-129">Id</span><span class="sxs-lookup"><span data-stu-id="f22f5-129">Id</span></span> | <span data-ttu-id="f22f5-130">Especifica uma lista de IDs de atualização de pacote.</span><span class="sxs-lookup"><span data-stu-id="f22f5-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="f22f5-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="f22f5-131">MSBuildPath</span></span> | <span data-ttu-id="f22f5-132">*(4.0 e posteriores)*  Especifica o caminho do MSBuild a usar com o comando, tendo precedência sobre `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="f22f5-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="f22f5-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="f22f5-133">MSBuildVersion</span></span> | <span data-ttu-id="f22f5-134">*(3.2 e superior)*  Especifica a versão do MSBuild a ser usado com este comando.</span><span class="sxs-lookup"><span data-stu-id="f22f5-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="f22f5-135">Valores com suporte são 4, 12, 14, 15.1, 15.3, 15.4, 15,5, 15.6, 15.7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="f22f5-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="f22f5-136">Por padrão que o MSBuild em seu caminho é escolhido, caso contrário, o padrão é a versão mais recente instalada do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="f22f5-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="f22f5-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f22f5-137">NonInteractive</span></span> | <span data-ttu-id="f22f5-138">Suprime a solicitações de entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="f22f5-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f22f5-139">Versão de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="f22f5-139">PreRelease</span></span> | <span data-ttu-id="f22f5-140">Permite a atualização para versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="f22f5-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="f22f5-141">Este sinalizador não é necessário ao atualizar os pacotes de pré-lançamento que já estão instalados.</span><span class="sxs-lookup"><span data-stu-id="f22f5-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="f22f5-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="f22f5-142">RepositoryPath</span></span> | <span data-ttu-id="f22f5-143">Especifica a pasta local onde os pacotes são instalados.</span><span class="sxs-lookup"><span data-stu-id="f22f5-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="f22f5-144">Safe</span><span class="sxs-lookup"><span data-stu-id="f22f5-144">Safe</span></span> | <span data-ttu-id="f22f5-145">Especifica que atualiza apenas com a versão mais recente disponível dentro da mesma versão principal e secundária como o pacote instalado será instalado.</span><span class="sxs-lookup"><span data-stu-id="f22f5-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="f22f5-146">Self</span><span class="sxs-lookup"><span data-stu-id="f22f5-146">Self</span></span> | <span data-ttu-id="f22f5-147">Nuget.exe atualizações para a versão mais recente; todos os outros argumentos são ignorados.</span><span class="sxs-lookup"><span data-stu-id="f22f5-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="f22f5-148">Origem</span><span class="sxs-lookup"><span data-stu-id="f22f5-148">Source</span></span> | <span data-ttu-id="f22f5-149">Especifica a lista de origens de pacote (como URLs) para usar as atualizações.</span><span class="sxs-lookup"><span data-stu-id="f22f5-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="f22f5-150">Se omitido, o comando usa as fontes fornecidas em arquivos de configuração, consulte [o comportamento do NuGet configurando](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="f22f5-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="f22f5-151">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="f22f5-151">Verbosity</span></span> | <span data-ttu-id="f22f5-152">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="f22f5-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="f22f5-153">Versão</span><span class="sxs-lookup"><span data-stu-id="f22f5-153">Version</span></span> | <span data-ttu-id="f22f5-154">Quando usado com uma ID de pacote, especifica a versão do pacote a atualizar.</span><span class="sxs-lookup"><span data-stu-id="f22f5-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="f22f5-155">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f22f5-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f22f5-156">Exemplos</span><span class="sxs-lookup"><span data-stu-id="f22f5-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
