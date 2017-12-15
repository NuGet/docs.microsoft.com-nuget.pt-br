---
title: Comando update do NuGet CLI | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 61fde945-6983-46a5-8636-da0fada4e641
description: "Referência para o comando de atualização de nuget.exe"
keywords: "referência de atualização do NuGet, comando de pacote de atualização"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 654144e93a99a4a4f8d79c0db5660cfb7c6c308e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="44c9d-104">comando de atualização (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="44c9d-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="44c9d-105">**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="44c9d-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="44c9d-106">Atualiza todos os pacotes em um projeto (usando `packages.config`) para suas versões mais recentes disponíveis.</span><span class="sxs-lookup"><span data-stu-id="44c9d-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="44c9d-107">É recomendável executar ['restore'](#restore) antes de executar o `update`.</span><span class="sxs-lookup"><span data-stu-id="44c9d-107">It is recommended to run ['restore'](#restore) before running the `update`.</span></span> <span data-ttu-id="44c9d-108">(Para atualizar um pacote individual, use [ `nuget install` ](cli-ref-install.md) sem especificar um número de versão, em que o NuGet caso instala a versão mais recente.)</span><span class="sxs-lookup"><span data-stu-id="44c9d-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="44c9d-109">Observação: `update` não funciona com a CLI em execução em Mono (Mac OSX ou Linux).</span><span class="sxs-lookup"><span data-stu-id="44c9d-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux).</span></span> <span data-ttu-id="44c9d-110">O comando também funciona com projetos usando `project.json` ou PackageReference formatos de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="44c9d-110">The command also does not work with projects using `project.json` or PackageReference management formats.</span></span>

<span data-ttu-id="44c9d-111">O `update` comando também atualiza as referências de assembly no arquivo de projeto, desde que as referências já existe.</span><span class="sxs-lookup"><span data-stu-id="44c9d-111">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="44c9d-112">Se um pacote atualizado tem um assembly adicionado, uma nova referência é *não* adicionado.</span><span class="sxs-lookup"><span data-stu-id="44c9d-112">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="44c9d-113">Novas dependências do pacote também não têm suas referências de assembly adicionadas.</span><span class="sxs-lookup"><span data-stu-id="44c9d-113">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="44c9d-114">Para incluir essas operações como parte de uma atualização, atualize o pacote no Visual Studio usando a UI Package Manager ou o Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="44c9d-114">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="44c9d-115">Este comando também pode ser usado para atualizar o nuget.exe si mesmo usando o *-self* sinalizador.</span><span class="sxs-lookup"><span data-stu-id="44c9d-115">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="44c9d-116">Uso</span><span class="sxs-lookup"><span data-stu-id="44c9d-116">Usage</span></span>

```
nuget update <configPath> [options]
```

<span data-ttu-id="44c9d-117">onde `<configPath>` identifica em uma `packages.config` ou arquivo de solução que lista as dependências do projeto.</span><span class="sxs-lookup"><span data-stu-id="44c9d-117">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="44c9d-118">Opções</span><span class="sxs-lookup"><span data-stu-id="44c9d-118">Options</span></span>

| <span data-ttu-id="44c9d-119">Opção</span><span class="sxs-lookup"><span data-stu-id="44c9d-119">Option</span></span> | <span data-ttu-id="44c9d-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="44c9d-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44c9d-121">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="44c9d-121">ConfigFile</span></span> | <span data-ttu-id="44c9d-122">*(2.5 +)*  NuGet o arquivo de configuração para aplicar.</span><span class="sxs-lookup"><span data-stu-id="44c9d-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="44c9d-123">Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado.</span><span class="sxs-lookup"><span data-stu-id="44c9d-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="44c9d-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="44c9d-124">FileConflictAction</span></span> | <span data-ttu-id="44c9d-125">*(2.5 +)*  Especifica a ação a ser tomada quando for solicitado a substituir ou ignorar os arquivos existentes, referenciados pelo projeto.</span><span class="sxs-lookup"><span data-stu-id="44c9d-125">*(2.5+)* Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="44c9d-126">Os valores são *substituir, ignorar, nenhum*.</span><span class="sxs-lookup"><span data-stu-id="44c9d-126">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="44c9d-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="44c9d-127">ForceEnglishOutput</span></span> | <span data-ttu-id="44c9d-128">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="44c9d-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="44c9d-129">Ajuda</span><span class="sxs-lookup"><span data-stu-id="44c9d-129">Help</span></span> | <span data-ttu-id="44c9d-130">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="44c9d-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="44c9d-131">Id</span><span class="sxs-lookup"><span data-stu-id="44c9d-131">Id</span></span> | <span data-ttu-id="44c9d-132">Especifica uma lista de IDs para a atualização do pacote.</span><span class="sxs-lookup"><span data-stu-id="44c9d-132">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="44c9d-133">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="44c9d-133">MSBuildPath</span></span> | <span data-ttu-id="44c9d-134">*(4.0 +)*  Especifica o caminho do MSBuild para usar com o comando tendo precedência sobre `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="44c9d-134">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="44c9d-135">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="44c9d-135">MSBuildVersion</span></span> | <span data-ttu-id="44c9d-136">*(3.2 +)*  Especifica a versão do MSBuild a ser usado com este comando.</span><span class="sxs-lookup"><span data-stu-id="44c9d-136">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="44c9d-137">Valores com suporte são 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="44c9d-137">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="44c9d-138">Por padrão que o MSBuild em seu caminho é separado, caso contrário, o padrão é a versão mais recente instalada do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="44c9d-138">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="44c9d-139">Não interativo</span><span class="sxs-lookup"><span data-stu-id="44c9d-139">NonInteractive</span></span> | <span data-ttu-id="44c9d-140">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="44c9d-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="44c9d-141">Versão de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="44c9d-141">PreRelease</span></span> | <span data-ttu-id="44c9d-142">Permite a atualização para as versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="44c9d-142">Allows updating to prerelease versions.</span></span> <span data-ttu-id="44c9d-143">Este sinalizador não é necessário ao atualizar os pacotes de pré-lançamento que já estão instalados.</span><span class="sxs-lookup"><span data-stu-id="44c9d-143">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="44c9d-144">Caminho do repositório</span><span class="sxs-lookup"><span data-stu-id="44c9d-144">RepositoryPath</span></span> | <span data-ttu-id="44c9d-145">Especifica a pasta local onde os pacotes estão instalados.</span><span class="sxs-lookup"><span data-stu-id="44c9d-145">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="44c9d-146">Safe</span><span class="sxs-lookup"><span data-stu-id="44c9d-146">Safe</span></span> | <span data-ttu-id="44c9d-147">Especifica que apenas atualizações com a versão mais recente disponível dentro da mesma versão principal e secundária, o pacote instalado será instalado.</span><span class="sxs-lookup"><span data-stu-id="44c9d-147">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="44c9d-148">Self</span><span class="sxs-lookup"><span data-stu-id="44c9d-148">Self</span></span> | <span data-ttu-id="44c9d-149">*(1.4 +)*  Atualiza nuget.exe para a versão mais recente; todos os outros argumentos são ignorados.</span><span class="sxs-lookup"><span data-stu-id="44c9d-149">*(1.4+)* Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="44c9d-150">Origem</span><span class="sxs-lookup"><span data-stu-id="44c9d-150">Source</span></span> | <span data-ttu-id="44c9d-151">Especifica a lista de fontes de pacote (como URLs) para usar as atualizações.</span><span class="sxs-lookup"><span data-stu-id="44c9d-151">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="44c9d-152">Se omitido, o comando usa as fontes fornecidas nos arquivos de configuração, consulte [NuGet Configurando comportamento](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="44c9d-152">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="44c9d-153">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="44c9d-153">Verbosity</span></span> | <span data-ttu-id="44c9d-154">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="44c9d-154">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="44c9d-155">Versão</span><span class="sxs-lookup"><span data-stu-id="44c9d-155">Version</span></span> | <span data-ttu-id="44c9d-156">Quando usado com uma ID de pacote, especifica a versão do pacote para atualizar.</span><span class="sxs-lookup"><span data-stu-id="44c9d-156">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="44c9d-157">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="44c9d-157">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="44c9d-158">Exemplos</span><span class="sxs-lookup"><span data-stu-id="44c9d-158">Examples</span></span>

```
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
