---
title: Comando de instalação do NuGet CLI | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referência para o comando de instalação de nuget.exe
keywords: NuGet instalar referência, o comando do pacote de instalação
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 121d7b50767f1d466d6d0d8494f324b02d8ff6f1
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="cf262-104">instalar o comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cf262-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="cf262-105">**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="cf262-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="cf262-106">Baixa e instala um pacote em um projeto, o padrão para a pasta atual, usando fontes de pacote especificado.</span><span class="sxs-lookup"><span data-stu-id="cf262-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="cf262-107">Para baixar um pacote diretamente fora do contexto de um projeto, visite a página do pacote no [nuget.org](https://www.nuget.org) e selecione o **baixar** link.</span><span class="sxs-lookup"><span data-stu-id="cf262-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="cf262-108">Se nenhuma fonte for especificada, aqueles listados no arquivo de configuração global, `%appdata%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac Linux), são usados.</span><span class="sxs-lookup"><span data-stu-id="cf262-108">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="cf262-109">Consulte [NuGet Configurando comportamento](../consume-packages/configuring-nuget-behavior.md) para obter detalhes adicionais.</span><span class="sxs-lookup"><span data-stu-id="cf262-109">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="cf262-110">Se nenhum pacote específico é especificada, `install` instala todos os pacotes listados no projeto de `packages.config` arquivo, tornando-o como [ `restore` ](cli-ref-restore.md).</span><span class="sxs-lookup"><span data-stu-id="cf262-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="cf262-111">O `install` comando não modifica um arquivo de projeto ou `packages.config`; desse modo é semelhante a `restore` em que ele apenas adiciona os pacotes para o disco, mas não altera as dependências do projeto.</span><span class="sxs-lookup"><span data-stu-id="cf262-111">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="cf262-112">Para adicionar uma dependência, adicionar um projeto por meio do Gerenciador de pacote da interface do usuário ou o Console no Visual Studio ou modificar `packages.config` e, em seguida, execute um `install` ou `restore`.</span><span class="sxs-lookup"><span data-stu-id="cf262-112">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="cf262-113">Uso</span><span class="sxs-lookup"><span data-stu-id="cf262-113">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="cf262-114">onde `<packageID>` nomeia o pacote de instalação (usando a versão mais recente), ou `<configFilePath>` identifica o `packages.config` arquivo que lista os pacotes para instalar.</span><span class="sxs-lookup"><span data-stu-id="cf262-114">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="cf262-115">Você pode indicar uma versão específica com o `-Version` opção.</span><span class="sxs-lookup"><span data-stu-id="cf262-115">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="cf262-116">Opções</span><span class="sxs-lookup"><span data-stu-id="cf262-116">Options</span></span>

| <span data-ttu-id="cf262-117">Opção</span><span class="sxs-lookup"><span data-stu-id="cf262-117">Option</span></span> | <span data-ttu-id="cf262-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="cf262-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cf262-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="cf262-119">ConfigFile</span></span> | <span data-ttu-id="cf262-120">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="cf262-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cf262-121">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="cf262-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="cf262-122">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="cf262-122">DependencyVersion</span></span> | <span data-ttu-id="cf262-123">*(4.4 +)*  Especifica uma versão específica, substituindo o comportamento de resolução de dependência padrão.</span><span class="sxs-lookup"><span data-stu-id="cf262-123">*(4.4+)* Specifies a specific version, overriding the default dependency resolution behavior.</span></span> |
| <span data-ttu-id="cf262-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="cf262-124">DisableParallelProcessing</span></span> | <span data-ttu-id="cf262-125">Desativa a instalação de vários pacotes em paralelo.</span><span class="sxs-lookup"><span data-stu-id="cf262-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="cf262-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="cf262-126">ExcludeVersion</span></span> | <span data-ttu-id="cf262-127">Instala o pacote para uma pasta chamada com apenas o nome do pacote e não o número de versão.</span><span class="sxs-lookup"><span data-stu-id="cf262-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="cf262-128">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="cf262-128">FallbackSource</span></span> | <span data-ttu-id="cf262-129">*(3.2 +)*  Uma lista de fontes de pacote para usar como fallbacks caso o pacote não foi encontrado no primário ou a fonte padrão.</span><span class="sxs-lookup"><span data-stu-id="cf262-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="cf262-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cf262-130">ForceEnglishOutput</span></span> | <span data-ttu-id="cf262-131">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="cf262-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cf262-132">Framework</span><span class="sxs-lookup"><span data-stu-id="cf262-132">Framework</span></span> | <span data-ttu-id="cf262-133">*(4.4 +)*  Usada para selecionar as dependências de estrutura de destino.</span><span class="sxs-lookup"><span data-stu-id="cf262-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="cf262-134">O padrão é 'Any' se não for especificado.</span><span class="sxs-lookup"><span data-stu-id="cf262-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="cf262-135">Ajuda</span><span class="sxs-lookup"><span data-stu-id="cf262-135">Help</span></span> | <span data-ttu-id="cf262-136">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="cf262-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="cf262-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="cf262-137">NoCache</span></span> | <span data-ttu-id="cf262-138">Impede que o NuGet usando pacotes armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="cf262-138">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="cf262-139">Consulte [Gerenciando os pacotes globais e as pastas do cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="cf262-139">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="cf262-140">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="cf262-140">NonInteractive</span></span> | <span data-ttu-id="cf262-141">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="cf262-141">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="cf262-142">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="cf262-142">OutputDirectory</span></span> | <span data-ttu-id="cf262-143">Especifica a pasta na qual os pacotes são instalados.</span><span class="sxs-lookup"><span data-stu-id="cf262-143">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="cf262-144">Se nenhuma pasta for especificada, a pasta atual será usada.</span><span class="sxs-lookup"><span data-stu-id="cf262-144">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="cf262-145">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="cf262-145">PackageSaveMode</span></span> | <span data-ttu-id="cf262-146">Especifica os tipos de arquivos para salvar após a instalação do pacote: um dos `nuspec`, `nupkg`, ou `nuspec;nupkg`.</span><span class="sxs-lookup"><span data-stu-id="cf262-146">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="cf262-147">Versão de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="cf262-147">PreRelease</span></span> | <span data-ttu-id="cf262-148">Permite que os pacotes de pré-lançamento ser instalado.</span><span class="sxs-lookup"><span data-stu-id="cf262-148">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="cf262-149">Esse sinalizador não é necessário ao restaurar pacotes com `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="cf262-149">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="cf262-150">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="cf262-150">RequireConsent</span></span> | <span data-ttu-id="cf262-151">Verifica se a restauração de pacotes é habilitado antes de baixar e instalar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="cf262-151">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="cf262-152">Para obter detalhes, consulte [restauração do pacote](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="cf262-152">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="cf262-153">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="cf262-153">SolutionDirectory</span></span> | <span data-ttu-id="cf262-154">Especifica a pasta raiz da solução para a qual restaurar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="cf262-154">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="cf262-155">Origem</span><span class="sxs-lookup"><span data-stu-id="cf262-155">Source</span></span> | <span data-ttu-id="cf262-156">Especifica a lista de fontes de pacote (como URLs) para usar.</span><span class="sxs-lookup"><span data-stu-id="cf262-156">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="cf262-157">Se omitido, o comando usa as fontes fornecidas nos arquivos de configuração, consulte [NuGet Configurando comportamento](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="cf262-157">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="cf262-158">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="cf262-158">Verbosity</span></span> | <span data-ttu-id="cf262-159">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="cf262-159">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="cf262-160">Versão</span><span class="sxs-lookup"><span data-stu-id="cf262-160">Version</span></span> | <span data-ttu-id="cf262-161">Especifica a versão do pacote para instalar.</span><span class="sxs-lookup"><span data-stu-id="cf262-161">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="cf262-162">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cf262-162">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cf262-163">Exemplos</span><span class="sxs-lookup"><span data-stu-id="cf262-163">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
