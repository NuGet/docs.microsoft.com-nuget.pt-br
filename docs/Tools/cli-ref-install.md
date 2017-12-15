---
title: "Comando de instalação do NuGet CLI | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 59ac622f-837c-4545-bc93-a56330e02d71
description: "Referência para o comando de instalação de nuget.exe"
keywords: "NuGet instalar referência, o comando do pacote de instalação"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88c123a7f2a3d628713cefcc4b110fb0205093b4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="24c09-104">instalar o comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="24c09-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="24c09-105">**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="24c09-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="24c09-106">Baixa e instala um pacote em um projeto, o padrão para a pasta atual, usando fontes de pacote especificado.</span><span class="sxs-lookup"><span data-stu-id="24c09-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="24c09-107">Para baixar um pacote diretamente fora do contexto de um projeto, visite a página do pacote no [nuget.org](https://www.nuget.org) e selecione o **baixar** link.</span><span class="sxs-lookup"><span data-stu-id="24c09-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span> 

<span data-ttu-id="24c09-108">Se nenhuma fonte for especificada, aqueles listados no arquivo de configuração global, `%APPDATA%\NuGet\NuGet.Config`, são usados.</span><span class="sxs-lookup"><span data-stu-id="24c09-108">If no sources are specified, those listed in the global configuration file, `%APPDATA%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="24c09-109">Consulte [Configurando NuGet comportamento](../consume-packages/configuring-nuget-behavior.md) para obter detalhes adicionais.</span><span class="sxs-lookup"><span data-stu-id="24c09-109">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="24c09-110">Se nenhum pacote específico é especificada, `install` instala todos os pacotes listados no projeto de `packages.config` arquivo, tornando-o como [ `restore` ](#restore).</span><span class="sxs-lookup"><span data-stu-id="24c09-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](#restore).</span></span> <span data-ttu-id="24c09-111">(O `install` comando não funciona com `project.json`.)</span><span class="sxs-lookup"><span data-stu-id="24c09-111">(The `install` command does not work with `project.json`.)</span></span>

<span data-ttu-id="24c09-112">O `install` comando não modifica um arquivo de projeto ou `packages.config`; desse modo é semelhante a `restore` em que ele apenas adiciona os pacotes para o disco, mas não altera as dependências do projeto.</span><span class="sxs-lookup"><span data-stu-id="24c09-112">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="24c09-113">Para adicionar uma dependência, adicionar um projeto por meio do Gerenciador de pacote da interface do usuário ou o Console no Visual Studio ou modificar `packages.config` e, em seguida, execute um `install` ou `restore`.</span><span class="sxs-lookup"><span data-stu-id="24c09-113">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span> <span data-ttu-id="24c09-114">Para projetos que usam `project.json`, você pode modificar esse arquivo e, em seguida, executar `restore`.</span><span class="sxs-lookup"><span data-stu-id="24c09-114">For projects using `project.json`, you can modify that file and then run `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="24c09-115">Uso</span><span class="sxs-lookup"><span data-stu-id="24c09-115">Usage</span></span>

```
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="24c09-116">onde `<packageID>` nomeia o pacote de instalação (usando a versão mais recente), ou `<configFilePath>` identifica o `packages.config` arquivo que lista os pacotes para instalar.</span><span class="sxs-lookup"><span data-stu-id="24c09-116">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="24c09-117">Você pode indicar uma versão específica com o `-Version` opção.</span><span class="sxs-lookup"><span data-stu-id="24c09-117">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="24c09-118">Opções</span><span class="sxs-lookup"><span data-stu-id="24c09-118">Options</span></span>

| <span data-ttu-id="24c09-119">Opção</span><span class="sxs-lookup"><span data-stu-id="24c09-119">Option</span></span> | <span data-ttu-id="24c09-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="24c09-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="24c09-121">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="24c09-121">ConfigFile</span></span> | <span data-ttu-id="24c09-122">*(2.5 +)*  NuGet o arquivo de configuração para aplicar.</span><span class="sxs-lookup"><span data-stu-id="24c09-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="24c09-123">Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado.</span><span class="sxs-lookup"><span data-stu-id="24c09-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="24c09-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="24c09-124">DisableParallelProcessing</span></span> | <span data-ttu-id="24c09-125">Desativa a instalação de vários pacotes em paralelo.</span><span class="sxs-lookup"><span data-stu-id="24c09-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="24c09-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="24c09-126">ExcludeVersion</span></span> | <span data-ttu-id="24c09-127">Instala o pacote para uma pasta chamada com apenas o nome do pacote e não o número de versão.</span><span class="sxs-lookup"><span data-stu-id="24c09-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="24c09-128">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="24c09-128">FallbackSource</span></span> | <span data-ttu-id="24c09-129">*(3.2 +)*  Uma lista de fontes de pacote para usar como fallbacks caso o pacote não foi encontrado no primário ou a fonte padrão.</span><span class="sxs-lookup"><span data-stu-id="24c09-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="24c09-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="24c09-130">ForceEnglishOutput</span></span> | <span data-ttu-id="24c09-131">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="24c09-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="24c09-132">Framework</span><span class="sxs-lookup"><span data-stu-id="24c09-132">Framework</span></span> | <span data-ttu-id="24c09-133">*(4.4 +)*  Usada para selecionar as dependências de estrutura de destino.</span><span class="sxs-lookup"><span data-stu-id="24c09-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="24c09-134">O padrão é 'Any' se não for especificado.</span><span class="sxs-lookup"><span data-stu-id="24c09-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="24c09-135">Ajuda</span><span class="sxs-lookup"><span data-stu-id="24c09-135">Help</span></span> | <span data-ttu-id="24c09-136">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="24c09-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="24c09-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="24c09-137">NoCache</span></span> | <span data-ttu-id="24c09-138">Impede que o NuGet usando pacotes de caches de computador local.</span><span class="sxs-lookup"><span data-stu-id="24c09-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="24c09-139">Não interativo</span><span class="sxs-lookup"><span data-stu-id="24c09-139">NonInteractive</span></span> | <span data-ttu-id="24c09-140">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="24c09-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="24c09-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="24c09-141">OutputDirectory</span></span> | <span data-ttu-id="24c09-142">Especifica a pasta na qual os pacotes são instalados.</span><span class="sxs-lookup"><span data-stu-id="24c09-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="24c09-143">Se nenhuma pasta for especificada, a pasta atual será usada.</span><span class="sxs-lookup"><span data-stu-id="24c09-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="24c09-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="24c09-144">PackageSaveMode</span></span> | <span data-ttu-id="24c09-145">Especifica os tipos de arquivos para salvar após a instalação do pacote: um dos `nuspec`, `nupkg`, ou `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="24c09-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="24c09-146">Versão de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="24c09-146">PreRelease</span></span> | <span data-ttu-id="24c09-147">Permite que os pacotes de pré-lançamento ser instalado.</span><span class="sxs-lookup"><span data-stu-id="24c09-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="24c09-148">Esse sinalizador não é necessário ao restaurar pacotes com `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="24c09-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="24c09-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="24c09-149">RequireConsent</span></span> | <span data-ttu-id="24c09-150">Verifica se a restauração de pacotes é habilitado antes de baixar e instalar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="24c09-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="24c09-151">Para obter detalhes, consulte [restauração do pacote](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="24c09-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="24c09-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="24c09-152">SolutionDirectory</span></span> | <span data-ttu-id="24c09-153">Especifica a pasta raiz da solução para a qual restaurar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="24c09-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="24c09-154">Origem</span><span class="sxs-lookup"><span data-stu-id="24c09-154">Source</span></span> | <span data-ttu-id="24c09-155">Especifica a lista de fontes de pacote (como URLs) para usar.</span><span class="sxs-lookup"><span data-stu-id="24c09-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="24c09-156">Se omitido, o comando usa as fontes fornecidas nos arquivos de configuração, consulte [NuGet Configurando comportamento](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="24c09-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="24c09-157">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="24c09-157">Verbosity</span></span> | <span data-ttu-id="24c09-158">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="24c09-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="24c09-159">Versão</span><span class="sxs-lookup"><span data-stu-id="24c09-159">Version</span></span> | <span data-ttu-id="24c09-160">Especifica a versão do pacote para instalar.</span><span class="sxs-lookup"><span data-stu-id="24c09-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="24c09-161">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="24c09-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="24c09-162">Exemplos</span><span class="sxs-lookup"><span data-stu-id="24c09-162">Examples</span></span>

```
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
