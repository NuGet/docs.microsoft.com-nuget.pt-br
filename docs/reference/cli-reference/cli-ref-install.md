---
title: Comando de instalação da CLI do NuGet
description: Referência para o comando de instalação do nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 23856728d07d07183b5aedcd6218a56a444c410b
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623091"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="ca3f4-103">comando de instalação (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ca3f4-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="ca3f4-104">**Aplica-se a:** &bullet; **versões com suporte** do consumo do pacote: todas</span><span class="sxs-lookup"><span data-stu-id="ca3f4-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ca3f4-105">Baixa e instala um pacote em um projeto, padronizando para a pasta atual, usando as origens do pacote especificado.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="ca3f4-106">Para baixar um pacote diretamente fora do contexto de um projeto, visite a página do pacote em [NuGet.org](https://www.nuget.org) e selecione o link de **Download** .</span><span class="sxs-lookup"><span data-stu-id="ca3f4-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="ca3f4-107">Se nenhuma fonte for especificada, as listadas no arquivo de configuração global, `%appdata%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) serão usadas.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="ca3f4-108">Consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md) para obter detalhes adicionais.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="ca3f4-109">Se nenhum pacote específico for especificado, o `install` instalará todos os pacotes listados no `packages.config` arquivo do projeto, tornando-o semelhante a [`restore`](cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="ca3f4-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="ca3f4-110">O `install` comando não modifica um arquivo de projeto ou `packages.config` ; dessa forma, é semelhante a `restore` ele apenas adiciona pacotes ao disco, mas não altera as dependências de um projeto.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="ca3f4-111">Para adicionar uma dependência, adicione um pacote por meio da interface do usuário ou console do Gerenciador de pacotes no Visual Studio, ou modifique `packages.config` e execute o `install` ou o `restore` .</span><span class="sxs-lookup"><span data-stu-id="ca3f4-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="ca3f4-112">Uso</span><span class="sxs-lookup"><span data-stu-id="ca3f4-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="ca3f4-113">onde `<packageID>` o nomeia o pacote a ser instalado (usando a versão mais recente) ou `<configFilePath>` identifica o `packages.config` arquivo que lista os pacotes a serem instalados.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="ca3f4-114">Você pode indicar uma versão específica com a `-Version` opção.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="ca3f4-115">Opções</span><span class="sxs-lookup"><span data-stu-id="ca3f4-115">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="ca3f4-116">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ca3f4-117">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DependencyVersion`**

  <span data-ttu-id="ca3f4-118">*(4.4 +)* A versão dos pacotes de dependência a serem usados, que pode ser uma das seguintes:</span><span class="sxs-lookup"><span data-stu-id="ca3f4-118">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="ca3f4-119">*Mais baixo* (padrão): a versão mais baixa</span><span class="sxs-lookup"><span data-stu-id="ca3f4-119">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="ca3f4-120">*HighestPatch*: a versão com o menor principal, menor o mais baixo, patch mais alto</span><span class="sxs-lookup"><span data-stu-id="ca3f4-120">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="ca3f4-121">*HighestMinor*: a versão com o menor principal, o mais baixo, o patch mais alto</span><span class="sxs-lookup"><span data-stu-id="ca3f4-121">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="ca3f4-122">*Mais alto*: a versão mais recente</span><span class="sxs-lookup"><span data-stu-id="ca3f4-122">*Highest*: the highest version</span></span></li><li><span data-ttu-id="ca3f4-123">*Ignorar*: nenhum pacote de dependência será usado</span><span class="sxs-lookup"><span data-stu-id="ca3f4-123">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-DirectDownload`**

  <span data-ttu-id="ca3f4-124">Baixe diretamente sem preencher os caches com metadados ou binários.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-124">Download directly without populating any caches with metadata or binaries.</span></span>

- **`-DisableParallelProcessing`**

  <span data-ttu-id="ca3f4-125">Desabilita a instalação de vários pacotes em paralelo.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-125">Disables installing multiple packages in parallel.</span></span>

- **`-x|-ExcludeVersion`**

  <span data-ttu-id="ca3f4-126">Instala o pacote em uma pasta chamada somente com o nome do pacote e não com o número de versão.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-126">Installs the package to a folder named with only the package name and not the version number.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="ca3f4-127">*(3,2 +)* Uma lista de origens do pacote a ser usada como fallbacks caso o pacote não seja encontrado na fonte primária ou padrão.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-127">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="ca3f4-128">*(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Framework`**

  <span data-ttu-id="ca3f4-129">*(4.4 +)* Estrutura de destino usada para selecionar dependências.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-129">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="ca3f4-130">O padrão é ' any ' se não for especificado.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-130">Defaults to 'Any' if not specified.</span></span>

- **`-?|-help`**

  <span data-ttu-id="ca3f4-131">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-131">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="ca3f4-132">Impede que o NuGet use pacotes armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="ca3f4-133">Consulte [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="ca3f4-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="ca3f4-134">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="ca3f4-135">Especifica a pasta na qual os pacotes são instalados.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="ca3f4-136">Se nenhuma pasta for especificada, a pasta atual será usada.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-136">If no folder is specified, the current folder is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="ca3f4-137">Especifica os tipos de arquivos a serem salvos após a instalação do pacote: um dos `nuspec` , `nupkg` ou `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="ca3f4-137">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="ca3f4-138">Permite que pacotes de pré-lançamento sejam instalados.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-138">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="ca3f4-139">Esse sinalizador não é necessário ao restaurar pacotes com o `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="ca3f4-139">This flag is not required when restoring packages with `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="ca3f4-140">Verifica se a restauração de pacotes está habilitada antes de baixar e instalar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-140">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="ca3f4-141">Para obter detalhes, consulte [restauração de pacote](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="ca3f4-141">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="ca3f4-142">Especifica a pasta raiz da solução para a qual os pacotes são restaurados.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-142">Specifies root folder of the solution for which to restore packages.</span></span>

- **`-Source`**

   <span data-ttu-id="ca3f4-143">Especifica a lista de origens do pacote (como URLs) a serem usadas.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-143">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="ca3f4-144">Se omitido, o comando usará as fontes fornecidas em arquivos de configuração, consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ca3f4-144">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="ca3f4-145">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="ca3f4-145">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="ca3f4-146">Especifica a versão do pacote a instalar.</span><span class="sxs-lookup"><span data-stu-id="ca3f4-146">Specifies the version of the package to install.</span></span>

<span data-ttu-id="ca3f4-147">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ca3f4-147">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ca3f4-148">Exemplos</span><span class="sxs-lookup"><span data-stu-id="ca3f4-148">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
