---
title: "Comando de instalação do NuGet CLI | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência para o comando de instalação de nuget.exe"
keywords: "NuGet instalar referência, o comando do pacote de instalação"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9e824b08486704371eebefb964f86315d82fc222
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2018
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="e5728-104">instalar o comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e5728-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="e5728-105">**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="e5728-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="e5728-106">Baixa e instala um pacote em um projeto, o padrão para a pasta atual, usando fontes de pacote especificado.</span><span class="sxs-lookup"><span data-stu-id="e5728-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="e5728-107">Para baixar um pacote diretamente fora do contexto de um projeto, visite a página do pacote no [nuget.org](https://www.nuget.org) e selecione o **baixar** link.</span><span class="sxs-lookup"><span data-stu-id="e5728-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="e5728-108">Se nenhuma fonte for especificada, aqueles listados no arquivo de configuração global, `%APPDATA%\NuGet\NuGet.Config`, são usados.</span><span class="sxs-lookup"><span data-stu-id="e5728-108">If no sources are specified, those listed in the global configuration file, `%APPDATA%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="e5728-109">Consulte [NuGet Configurando comportamento](../consume-packages/configuring-nuget-behavior.md) para obter detalhes adicionais.</span><span class="sxs-lookup"><span data-stu-id="e5728-109">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="e5728-110">Se nenhum pacote específico é especificada, `install` instala todos os pacotes listados no projeto de `packages.config` arquivo, tornando-o como [ `restore` ](cli-ref-restore.md).</span><span class="sxs-lookup"><span data-stu-id="e5728-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="e5728-111">O `install` comando não modifica um arquivo de projeto ou `packages.config`; desse modo é semelhante a `restore` em que ele apenas adiciona os pacotes para o disco, mas não altera as dependências do projeto.</span><span class="sxs-lookup"><span data-stu-id="e5728-111">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="e5728-112">Para adicionar uma dependência, adicionar um projeto por meio do Gerenciador de pacote da interface do usuário ou o Console no Visual Studio ou modificar `packages.config` e, em seguida, execute um `install` ou `restore`.</span><span class="sxs-lookup"><span data-stu-id="e5728-112">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="e5728-113">Uso</span><span class="sxs-lookup"><span data-stu-id="e5728-113">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="e5728-114">onde `<packageID>` nomeia o pacote de instalação (usando a versão mais recente), ou `<configFilePath>` identifica o `packages.config` arquivo que lista os pacotes para instalar.</span><span class="sxs-lookup"><span data-stu-id="e5728-114">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="e5728-115">Você pode indicar uma versão específica com o `-Version` opção.</span><span class="sxs-lookup"><span data-stu-id="e5728-115">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="e5728-116">Opções</span><span class="sxs-lookup"><span data-stu-id="e5728-116">Options</span></span>

| <span data-ttu-id="e5728-117">Opção</span><span class="sxs-lookup"><span data-stu-id="e5728-117">Option</span></span> | <span data-ttu-id="e5728-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="e5728-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e5728-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e5728-119">ConfigFile</span></span> | <span data-ttu-id="e5728-120">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="e5728-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e5728-121">Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado.</span><span class="sxs-lookup"><span data-stu-id="e5728-121">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="e5728-122">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="e5728-122">DependencyVersion</span></span> | <span data-ttu-id="e5728-123">*(4.4 +)*  Especifica uma versão específica, substituindo o comportamento de resolução de dependência padrão.</span><span class="sxs-lookup"><span data-stu-id="e5728-123">*(4.4+)* Specifies a specific version, overriding the default dependency resolution behavior.</span></span> |
| <span data-ttu-id="e5728-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="e5728-124">DisableParallelProcessing</span></span> | <span data-ttu-id="e5728-125">Desativa a instalação de vários pacotes em paralelo.</span><span class="sxs-lookup"><span data-stu-id="e5728-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="e5728-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="e5728-126">ExcludeVersion</span></span> | <span data-ttu-id="e5728-127">Instala o pacote para uma pasta chamada com apenas o nome do pacote e não o número de versão.</span><span class="sxs-lookup"><span data-stu-id="e5728-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="e5728-128">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="e5728-128">FallbackSource</span></span> | <span data-ttu-id="e5728-129">*(3.2 +)*  Uma lista de fontes de pacote para usar como fallbacks caso o pacote não foi encontrado no primário ou a fonte padrão.</span><span class="sxs-lookup"><span data-stu-id="e5728-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="e5728-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e5728-130">ForceEnglishOutput</span></span> | <span data-ttu-id="e5728-131">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="e5728-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e5728-132">Framework</span><span class="sxs-lookup"><span data-stu-id="e5728-132">Framework</span></span> | <span data-ttu-id="e5728-133">*(4.4 +)*  Usada para selecionar as dependências de estrutura de destino.</span><span class="sxs-lookup"><span data-stu-id="e5728-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="e5728-134">O padrão é 'Any' se não for especificado.</span><span class="sxs-lookup"><span data-stu-id="e5728-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="e5728-135">Ajuda</span><span class="sxs-lookup"><span data-stu-id="e5728-135">Help</span></span> | <span data-ttu-id="e5728-136">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="e5728-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="e5728-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="e5728-137">NoCache</span></span> | <span data-ttu-id="e5728-138">Impede que o NuGet usando pacotes de caches de computador local.</span><span class="sxs-lookup"><span data-stu-id="e5728-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="e5728-139">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="e5728-139">NonInteractive</span></span> | <span data-ttu-id="e5728-140">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="e5728-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e5728-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="e5728-141">OutputDirectory</span></span> | <span data-ttu-id="e5728-142">Especifica a pasta na qual os pacotes são instalados.</span><span class="sxs-lookup"><span data-stu-id="e5728-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="e5728-143">Se nenhuma pasta for especificada, a pasta atual será usada.</span><span class="sxs-lookup"><span data-stu-id="e5728-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="e5728-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="e5728-144">PackageSaveMode</span></span> | <span data-ttu-id="e5728-145">Especifica os tipos de arquivos para salvar após a instalação do pacote: um dos `nuspec`, `nupkg`, ou `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="e5728-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="e5728-146">Versão de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="e5728-146">PreRelease</span></span> | <span data-ttu-id="e5728-147">Permite que os pacotes de pré-lançamento ser instalado.</span><span class="sxs-lookup"><span data-stu-id="e5728-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="e5728-148">Esse sinalizador não é necessário ao restaurar pacotes com `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="e5728-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="e5728-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="e5728-149">RequireConsent</span></span> | <span data-ttu-id="e5728-150">Verifica se a restauração de pacotes é habilitado antes de baixar e instalar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="e5728-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="e5728-151">Para obter detalhes, consulte [restauração do pacote](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="e5728-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="e5728-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="e5728-152">SolutionDirectory</span></span> | <span data-ttu-id="e5728-153">Especifica a pasta raiz da solução para a qual restaurar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="e5728-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="e5728-154">Origem</span><span class="sxs-lookup"><span data-stu-id="e5728-154">Source</span></span> | <span data-ttu-id="e5728-155">Especifica a lista de fontes de pacote (como URLs) para usar.</span><span class="sxs-lookup"><span data-stu-id="e5728-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="e5728-156">Se omitido, o comando usa as fontes fornecidas nos arquivos de configuração, consulte [NuGet Configurando comportamento](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="e5728-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="e5728-157">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="e5728-157">Verbosity</span></span> | <span data-ttu-id="e5728-158">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="e5728-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="e5728-159">Versão</span><span class="sxs-lookup"><span data-stu-id="e5728-159">Version</span></span> | <span data-ttu-id="e5728-160">Especifica a versão do pacote para instalar.</span><span class="sxs-lookup"><span data-stu-id="e5728-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="e5728-161">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e5728-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e5728-162">Exemplos</span><span class="sxs-lookup"><span data-stu-id="e5728-162">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
