---
title: Migrando do package.config para formatos de PackageReference | Microsoft Docs
author: karann-msft
ms.author: karann
manager: unniravindranathan
ms.date: 03/27/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Obter detalhes sobre como migrar um projeto do formato de gerenciamento package.config para PackageReference com suporte pelo NuGet 4.0 + e VS2017 e .NET Core 2.0
keywords: NuGet migrator, migrar, referências de pacote, projeto Packages de arquivos, PackageReference, VS2017, 2017 do Visual Studio, o NuGet 4, .NET Core 2.0
ms.reviewer:
- karann
- unnir
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 10bd2fe95a6af11806a7edd7a43eaa497486fd80
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/03/2018
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="768dc-104">Migrar de Packages. config para PackageReference</span><span class="sxs-lookup"><span data-stu-id="768dc-104">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="768dc-105">Visual Studio 2017 versão 15,7 Preview 3 e posterior oferece suporte a migração de um projeto a partir de [Packages](./packages-config.md) formato de gerenciamento para o [PackageReference](../consume-packages/Package-References-in-Project-Files.md) formato.</span><span class="sxs-lookup"><span data-stu-id="768dc-105">Visual Studio 2017 Version 15.7 Preview 3 and later supports migrating a project from the [packages.config](./packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="768dc-106">Benefícios do uso de PackageReference</span><span class="sxs-lookup"><span data-stu-id="768dc-106">Benefits of using PackageReference</span></span>

* <span data-ttu-id="768dc-107">**Gerenciar todas as dependências de projeto em um só lugar**: assim como referências de projeto ao projeto e referências de assembly, o pacote NuGet faz referência (usando o `PackageReference` nó) são gerenciados diretamente nos arquivos de projeto em vez de usar um separado arquivo Packages. config.</span><span class="sxs-lookup"><span data-stu-id="768dc-107">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="768dc-108">**Uma exibição organizada de dependências de nível superior**: diferentemente Packages, PackageReference lista somente os pacotes do NuGet instalados diretamente no projeto.</span><span class="sxs-lookup"><span data-stu-id="768dc-108">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="768dc-109">Como resultado, o NuGet Package Manager UI e o arquivo de projeto não são organizadas com dependências de nível inferior.</span><span class="sxs-lookup"><span data-stu-id="768dc-109">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="768dc-110">**Melhorias de desempenho**: ao usar PackageReference, os pacotes são mantidos no *pacotes global* pasta (conforme descrito em [Gerenciando os pacotes globais e as pastas do cache](../consume-packages/managing-the-global-packages-and-cache-folders.md) em vez de em um `packages` pasta dentro da solução.</span><span class="sxs-lookup"><span data-stu-id="768dc-110">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="768dc-111">Como resultado, PackageReference desempenho mais rápido e consome menos espaço em disco.</span><span class="sxs-lookup"><span data-stu-id="768dc-111">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="768dc-112">**Problema controle sobre as dependências e fluxo de conteúdo**: usando os recursos existentes do MSBuild permite que você [condicionalmente fazem referência a um pacote do NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) e escolha as referências de pacote por estrutura de destino, configuração, plataforma ou outros pontos.</span><span class="sxs-lookup"><span data-stu-id="768dc-112">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="768dc-113">**PackageReference está em desenvolvimento ativo**: consulte [PackageReference problemas no GitHub](https://aka.ms/nuget-pr-improvements).</span><span class="sxs-lookup"><span data-stu-id="768dc-113">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="768dc-114">Packages. config não está mais em desenvolvimento ativo.</span><span class="sxs-lookup"><span data-stu-id="768dc-114">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="768dc-115">Limitações</span><span class="sxs-lookup"><span data-stu-id="768dc-115">Limitations</span></span>

* <span data-ttu-id="768dc-116">NuGet PackageReference não está disponível no Visual Studio 2015 e anteriores.</span><span class="sxs-lookup"><span data-stu-id="768dc-116">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="768dc-117">Migrado de projetos pode ser aberto apenas no Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="768dc-117">Migrated projects can be opened only in Visual Studio 2017.</span></span>
* <span data-ttu-id="768dc-118">Migração não está disponível atualmente para o projeto C++ e ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="768dc-118">Migration is not currently available for C++ and ASP.NET project.</span></span>
* <span data-ttu-id="768dc-119">Alguns pacotes podem não ser totalmente compatíveis com PackageReference.</span><span class="sxs-lookup"><span data-stu-id="768dc-119">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="768dc-120">Para obter mais informações, consulte [problemas de compatibilidade do pacote](#package-compatibility-issues).</span><span class="sxs-lookup"><span data-stu-id="768dc-120">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

## <a name="migration-steps"></a><span data-ttu-id="768dc-121">Etapas de migração</span><span class="sxs-lookup"><span data-stu-id="768dc-121">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="768dc-122">Antes de inicia a migração, o Visual Studio cria um backup do projeto para permitir que você [reverta a Packages](#how-to-roll-back-to-packagesconfig) se necessário.</span><span class="sxs-lookup"><span data-stu-id="768dc-122">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="768dc-123">Abrir uma solução que contém o projeto usando `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="768dc-123">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="768dc-124">Em **Solution Explorer**, com o botão direito no **referências** nó ou o `packages.config` de arquivo e selecione **migrar Packages para PackageReference...** .</span><span class="sxs-lookup"><span data-stu-id="768dc-124">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="768dc-125">O migrator analisa as referências do pacote NuGet do projeto e tenta categorizá-los em **dependências de nível superior** (diretório você instalou pacotes do NuGet) e **dependências transitivas**(pacotes que foram instalados como dependências dos pacotes de nível superior).</span><span class="sxs-lookup"><span data-stu-id="768dc-125">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directory) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="768dc-126">PackageReference dá suporte à restauração do pacote transitiva e resolve dependências dinamicamente, que significa que as dependências transitivas não precisam ser instaladas explicitamente.</span><span class="sxs-lookup"><span data-stu-id="768dc-126">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="768dc-127">(Opcional) Você pode optar por tratar de um pacote do NuGet classificado como uma dependência transitiva como uma dependência de nível superior, selecionando o **nível superior** opção para o pacote.</span><span class="sxs-lookup"><span data-stu-id="768dc-127">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="768dc-128">Essa opção é automaticamente definida para pacotes que contêm ativos que não fluem transitivamente (aqueles no `build`, `buildCrossTargeting`, `contentFiles`, ou `analyzers` pastas) e aqueles marcado como uma dependência de desenvolvimento (`developmentDependency = "true"`).</span><span class="sxs-lookup"><span data-stu-id="768dc-128">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="768dc-129">Analise qualquer [problemas de compatibilidade do pacote](#package-compatibility-issues).</span><span class="sxs-lookup"><span data-stu-id="768dc-129">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="768dc-130">Selecione **Okey** para iniciar a migração.</span><span class="sxs-lookup"><span data-stu-id="768dc-130">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="768dc-131">No final da migração, o Visual Studio fornece um relatório com um caminho para o backup, a lista de pacotes instalados (dependências de nível superior), uma lista de pacotes referenciados como dependências transitivas e uma lista de problemas de compatibilidade identificado no início de migração.</span><span class="sxs-lookup"><span data-stu-id="768dc-131">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="768dc-132">O relatório é salvo na pasta de backup.</span><span class="sxs-lookup"><span data-stu-id="768dc-132">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="768dc-133">Valide que a solução é compilado e executado.</span><span class="sxs-lookup"><span data-stu-id="768dc-133">Validate that the solution builds and runs.</span></span> <span data-ttu-id="768dc-134">Se você encontrar problemas, [um problema de arquivo no GitHub](https://github.com/NuGet/Home/issues/).</span><span class="sxs-lookup"><span data-stu-id="768dc-134">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="768dc-135">Como reverter para Packages. config</span><span class="sxs-lookup"><span data-stu-id="768dc-135">How to roll back to packages.config</span></span>

1. <span data-ttu-id="768dc-136">Feche o projeto migrado.</span><span class="sxs-lookup"><span data-stu-id="768dc-136">Close the migrated project.</span></span>

1. <span data-ttu-id="768dc-137">Copie o arquivo de projeto e `packages.config` do backup (geralmente `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) para a pasta do projeto.</span><span class="sxs-lookup"><span data-stu-id="768dc-137">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span>

1. <span data-ttu-id="768dc-138">Abra o projeto.</span><span class="sxs-lookup"><span data-stu-id="768dc-138">Open the project.</span></span>

1. <span data-ttu-id="768dc-139">Abra o Console do Gerenciador de pacote usando o **Ferramentas > Gerenciador de pacotes do NuGet > Package Manager Console** comando de menu.</span><span class="sxs-lookup"><span data-stu-id="768dc-139">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="768dc-140">Execute o seguinte comando no Console:</span><span class="sxs-lookup"><span data-stu-id="768dc-140">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a><span data-ttu-id="768dc-141">Problemas de compatibilidade de pacote</span><span class="sxs-lookup"><span data-stu-id="768dc-141">Package compatibility issues</span></span>

<span data-ttu-id="768dc-142">Não há suporte para alguns aspectos que tinham suporte em Packages. config em PackageReference.</span><span class="sxs-lookup"><span data-stu-id="768dc-142">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="768dc-143">O migrator analisa e detecta esses problemas.</span><span class="sxs-lookup"><span data-stu-id="768dc-143">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="768dc-144">Qualquer pacote que tem um ou mais dos seguintes problemas pode não se comportar conforme o esperado após a migração.</span><span class="sxs-lookup"><span data-stu-id="768dc-144">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="768dc-145">scripts "install.ps1" são ignorados quando o pacote for instalado depois da migração</span><span class="sxs-lookup"><span data-stu-id="768dc-145">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="768dc-146">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="768dc-146">**Description**</span></span> | <span data-ttu-id="768dc-147">Com PackageReference, install.ps1 e uninstall.ps1 scripts do PowerShell não são executadas durante a instalação ou desinstalação de um pacote.</span><span class="sxs-lookup"><span data-stu-id="768dc-147">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="768dc-148">**Impacto potencial**</span><span class="sxs-lookup"><span data-stu-id="768dc-148">**Potential impact**</span></span> | <span data-ttu-id="768dc-149">Pacotes que dependem desses scripts para configurar o comportamento de alguns no projeto de destino podem não funcionar conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="768dc-149">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="768dc-150">ativos de "conteúdo" não estão disponíveis quando o pacote for instalado depois da migração</span><span class="sxs-lookup"><span data-stu-id="768dc-150">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="768dc-151">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="768dc-151">**Description**</span></span> | <span data-ttu-id="768dc-152">Ativos em um pacote `content` pasta não são compatíveis com PackageReference e são ignorados.</span><span class="sxs-lookup"><span data-stu-id="768dc-152">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="768dc-153">PackageReference adiciona suporte para `contentFiles` ter um suporte melhor transitivo e conteúdo compartilhado.</span><span class="sxs-lookup"><span data-stu-id="768dc-153">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="768dc-154">**Impacto potencial**</span><span class="sxs-lookup"><span data-stu-id="768dc-154">**Potential impact**</span></span> | <span data-ttu-id="768dc-155">Ativos em `content` não são copiados para o projeto e o projeto de código que depende da presença desses ativos requer a refatoração.</span><span class="sxs-lookup"><span data-stu-id="768dc-155">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="768dc-156">Transformações XDT não são aplicadas quando o pacote for instalado depois da atualização</span><span class="sxs-lookup"><span data-stu-id="768dc-156">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="768dc-157">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="768dc-157">**Description**</span></span> | <span data-ttu-id="768dc-158">Não há suporte para transformações XDT com PackageReference e `.xdt` arquivos são ignorados ao instalar ou desinstalar um pacote.</span><span class="sxs-lookup"><span data-stu-id="768dc-158">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="768dc-159">**Impacto potencial**</span><span class="sxs-lookup"><span data-stu-id="768dc-159">**Potential impact**</span></span> | <span data-ttu-id="768dc-160">Transformações XDT não são aplicadas para os arquivos XML de projeto, geralmente, `web.config.install.xdt` e `web.config.uninstall.xdt`, que significa que o projeto` web.config` arquivo não é atualizado quando o pacote for instalado ou desinstalado.</span><span class="sxs-lookup"><span data-stu-id="768dc-160">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="768dc-161">Assemblies na raiz da biblioteca são ignorados quando o pacote for instalado depois da migração</span><span class="sxs-lookup"><span data-stu-id="768dc-161">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="768dc-162">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="768dc-162">**Description**</span></span> | <span data-ttu-id="768dc-163">Com PackageReference, assemblies presentes na raiz da `lib` pasta sem uma destino do framework subpasta específica são ignorados.</span><span class="sxs-lookup"><span data-stu-id="768dc-163">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="768dc-164">NuGet procura uma subpasta, o moniker da estrutura de destino (TFM) correspondente para o framework de destino do projeto de correspondência e instala os assemblies de correspondência no projeto.</span><span class="sxs-lookup"><span data-stu-id="768dc-164">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="768dc-165">**Impacto potencial**</span><span class="sxs-lookup"><span data-stu-id="768dc-165">**Potential impact**</span></span> | <span data-ttu-id="768dc-166">Pacotes que não têm uma subpasta correspondente o moniker da estrutura de destino (TFM) correspondente para o framework de destino do projeto não podem se comportar conforme o esperado após a transição ou falha de instalação durante a migração</span><span class="sxs-lookup"><span data-stu-id="768dc-166">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="768dc-167">Encontrado um problema?</span><span class="sxs-lookup"><span data-stu-id="768dc-167">Found an issue?</span></span> <span data-ttu-id="768dc-168">Relatá-lo!</span><span class="sxs-lookup"><span data-stu-id="768dc-168">Report it!</span></span>

<span data-ttu-id="768dc-169">Se você tiver um problema com a experiência de migração, [um problema de arquivo no repositório do NuGet GitHub](https://github.com/NuGet/Home/issues/).</span><span class="sxs-lookup"><span data-stu-id="768dc-169">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
