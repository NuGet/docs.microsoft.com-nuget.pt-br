---
title: "Conteúdo do arquivo project.json do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/17/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Diversos bits de conteúdo do project.json removidos de outras áreas da documentação do NuGet."
keywords: Arquivo project.json do NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 42a40c6c637839c13effc9e476ac5702a92cfd2a
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2018
---
# <a name="projectjson-archive"></a><span data-ttu-id="142fa-104">Arquivo project.json</span><span class="sxs-lookup"><span data-stu-id="142fa-104">project.json archive</span></span>

<span data-ttu-id="142fa-105">O formato de referência `project.json` foi introduzido com o NuGet 3.x e é usado para determinados tipos de projeto.</span><span class="sxs-lookup"><span data-stu-id="142fa-105">The `project.json` reference format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="142fa-106">Ele foi substituído com a introdução do formato PackageReference, no qual as dependências são listadas diretamente em um arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="142fa-106">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="142fa-107">Consulte também:</span><span class="sxs-lookup"><span data-stu-id="142fa-107">Also see:</span></span>

- [<span data-ttu-id="142fa-108">Esquema do project.json</span><span class="sxs-lookup"><span data-stu-id="142fa-108">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="142fa-109">Impacto do project.json em autores de pacote</span><span class="sxs-lookup"><span data-stu-id="142fa-109">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="142fa-110">project.json e UWP</span><span class="sxs-lookup"><span data-stu-id="142fa-110">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-reference-format"></a><span data-ttu-id="142fa-111">Formato de referência do project.json</span><span class="sxs-lookup"><span data-stu-id="142fa-111">project.json reference format</span></span>

<span data-ttu-id="142fa-112">*Originalmente em [Restauração do pacote](../what-is-nuget.md).*</span><span class="sxs-lookup"><span data-stu-id="142fa-112">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="142fa-113">Na lista de formatos de referência:</span><span class="sxs-lookup"><span data-stu-id="142fa-113">In the list of reference formats:</span></span>

- <span data-ttu-id="142fa-114">[`project.json`](project-json.md): *(preterido)* Um arquivo JSON que mantém uma lista de dependências do projeto com um grafo geral do pacote em um arquivo associado, `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="142fa-114">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="142fa-115">Esse formato foi preterido em favor de PackageReference.</span><span class="sxs-lookup"><span data-stu-id="142fa-115">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="142fa-116">Restauração do nuget no Mono</span><span class="sxs-lookup"><span data-stu-id="142fa-116">nuget restore on Mono</span></span>

<span data-ttu-id="142fa-117">*Originalmente em [Instalar as ferramentas de cliente do NuGet](../install-nuget-client-tools.md).*</span><span class="sxs-lookup"><span data-stu-id="142fa-117">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="142fa-118">Ferramenta com `project.json`.</span><span class="sxs-lookup"><span data-stu-id="142fa-118">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="142fa-119">Restrições de versões de pacote com restauração</span><span class="sxs-lookup"><span data-stu-id="142fa-119">Constraining package versions with restore</span></span>

<span data-ttu-id="142fa-120">*Originalmente em [Restauração do pacote](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span><span class="sxs-lookup"><span data-stu-id="142fa-120">*Originally in [Package restore](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*</span></span>

- <span data-ttu-id="142fa-121">`project.json`: especifique um intervalo de versão diretamente com o número de versão da dependência.</span><span class="sxs-lookup"><span data-stu-id="142fa-121">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="142fa-122">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="142fa-122">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="142fa-123">Comandos da CLI do NuGet</span><span class="sxs-lookup"><span data-stu-id="142fa-123">NuGet CLI commands</span></span>

- <span data-ttu-id="142fa-124">`nuget install` não funciona com `project.json`.</span><span class="sxs-lookup"><span data-stu-id="142fa-124">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="142fa-125">`nuget restore`: com projetos usando o `project.json`, gera um arquivo `project.lock.json` e um arquivo `<project>.nuget.props`, se for necessário.</span><span class="sxs-lookup"><span data-stu-id="142fa-125">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="142fa-126">(Os dois arquivos podem ser omitidos do controle do código-fonte.) O argumento `<projectPath>` pode apontar um arquivo `project.json` e tem o mesmo comportamento que apontar para um `packages.config` ou arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="142fa-126">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="142fa-127">Na ordem de prioridade das pastas de pacote, `%userprofile%\.nuget\packages` é pesquisado pela primeira vez ao usar `project.json`.</span><span class="sxs-lookup"><span data-stu-id="142fa-127">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="142fa-128">`nuget update`: Em Mono, esse comando não funciona com projetos que usam `project.json`.</span><span class="sxs-lookup"><span data-stu-id="142fa-128">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="142fa-129">Resolução de dependência com PackageReference</span><span class="sxs-lookup"><span data-stu-id="142fa-129">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="142fa-130">*Originalmente em [Resolução de dependência](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span><span class="sxs-lookup"><span data-stu-id="142fa-130">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="142fa-131">O comportamento de PackageReference se aplica também a `project.json`.</span><span class="sxs-lookup"><span data-stu-id="142fa-131">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="142fa-132">A restauração do NuGet grava o grafo de dependência em um arquivo denominado `project.lock.json` juntamente com `project.json`.</span><span class="sxs-lookup"><span data-stu-id="142fa-132">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="142fa-133">Gerenciamento de ativos de dependência</span><span class="sxs-lookup"><span data-stu-id="142fa-133">Managing dependency assets</span></span>

<span data-ttu-id="142fa-134">*Originalmente em [Resolução de dependência](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span><span class="sxs-lookup"><span data-stu-id="142fa-134">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="142fa-135">Ao usar o formato `project.json`, é possível controlar de quais ativos as dependências fluem no projeto de nível superior.</span><span class="sxs-lookup"><span data-stu-id="142fa-135">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="142fa-136">Para obter detalhes, veja [project.json](project-json.md).</span><span class="sxs-lookup"><span data-stu-id="142fa-136">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="142fa-137">Excluindo referências</span><span class="sxs-lookup"><span data-stu-id="142fa-137">Excluding references</span></span>

<span data-ttu-id="142fa-138">*Originalmente em [Resolução de dependência](../consume-packages/dependency-resolution.md#excluding-references).*</span><span class="sxs-lookup"><span data-stu-id="142fa-138">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="142fa-139">`project.json`: adicionar `"exclude" : "all"` à dependência para PackageC:</span><span class="sxs-lookup"><span data-stu-id="142fa-139">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="142fa-140">Resolvendo erros de pacote incompatível</span><span class="sxs-lookup"><span data-stu-id="142fa-140">Resolving incompatible package errors</span></span>

<span data-ttu-id="142fa-141">*Originalmente em [Resolução de dependência](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span><span class="sxs-lookup"><span data-stu-id="142fa-141">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="142fa-142">Um outro jeito de resolver erros:</span><span class="sxs-lookup"><span data-stu-id="142fa-142">An added means of resolving errors:</span></span>

- <span data-ttu-id="142fa-143">**Não recomendável**: como uma solução temporária enquanto você trabalha junto com o autor do pacote, projetos voltados para `netcore`, `netstandard` e `netcoreapp` pode indicar outras estruturas como compatíveis, permitindo assim que os pacotes sejam direcionados para essas outras estruturas a serem usadas.</span><span class="sxs-lookup"><span data-stu-id="142fa-143">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="142fa-144">Consulte [Importações do project.json](project-json.md#imports) e [PackageTargetFallback do restore target do MSBuild](../reference/msbuild-targets.md#packagetargetfallback).</span><span class="sxs-lookup"><span data-stu-id="142fa-144">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="142fa-145">Isso pode causar comportamentos inesperados, por isso, novamente, é melhor resolver as incompatibilidades de pacote trabalhando com o autor do pacote em uma atualização.</span><span class="sxs-lookup"><span data-stu-id="142fa-145">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="142fa-146">Frameworks de destino</span><span class="sxs-lookup"><span data-stu-id="142fa-146">Target frameworks</span></span>

<span data-ttu-id="142fa-147">*Originalmente em [Estruturas de destino](../reference/target-frameworks.md).*</span><span class="sxs-lookup"><span data-stu-id="142fa-147">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="142fa-148">[project.json](project-json.md): o nó `frameworks` especifica as versões da estrutura com as quais o projeto pode ser compilado.</span><span class="sxs-lookup"><span data-stu-id="142fa-148">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="142fa-149">Criar um pacote</span><span class="sxs-lookup"><span data-stu-id="142fa-149">Creating a package</span></span>

<span data-ttu-id="142fa-150">*Originalmente em [Criar um pacote](../create-packages/creating-a-package.md)*</span><span class="sxs-lookup"><span data-stu-id="142fa-150">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="142fa-151">Definindo um tipo de pacote</span><span class="sxs-lookup"><span data-stu-id="142fa-151">Setting a package type</span></span>

<span data-ttu-id="142fa-152">Com o .NET Core 1.x, quando um pacote DotnetCliTool é instalado, o Visual Studio coloca o pacote no nó `project.json` `tools` em vez do nó `dependencies`.</span><span class="sxs-lookup"><span data-stu-id="142fa-152">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="142fa-153">Os tipos de pacote são definidos em `project.json`.</span><span class="sxs-lookup"><span data-stu-id="142fa-153">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="142fa-154">`project.json`: indica o tipo de pacote em um propriedade json `packOptions.packageType`:</span><span class="sxs-lookup"><span data-stu-id="142fa-154">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="142fa-155">Adicionar destinos e objetos ao MSBuild</span><span class="sxs-lookup"><span data-stu-id="142fa-155">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="142fa-156">*Originalmente em [Criar pacotes NuGet do .NET Standard com o Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span><span class="sxs-lookup"><span data-stu-id="142fa-156">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="142fa-157">Ao usar `project.json`, os destinos não são adicionados ao projeto, mas são disponibilizados por meio do `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="142fa-157">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="142fa-158">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="142fa-158">Package versioning</span></span>

<span data-ttu-id="142fa-159">*Originalmente em [Restauração do pacote](../reference/package-versioning.md).*</span><span class="sxs-lookup"><span data-stu-id="142fa-159">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="142fa-160">Ao usar o formato `project.json`, o NuGet também dá suporte ao uso de uma notação de curinga, \*, para as partes principal, secundária, patch e de sufixo de pré-lançamento do número.</span><span class="sxs-lookup"><span data-stu-id="142fa-160">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="142fa-161">Referência do NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="142fa-161">NuGet.Config reference</span></span>

<span data-ttu-id="142fa-162">*Original na [Referência do NuGet.Config](../reference/nuget-config-file.md).*</span><span class="sxs-lookup"><span data-stu-id="142fa-162">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="142fa-163">`globalPackagesFolder` aplica-se somente a `project.json`.</span><span class="sxs-lookup"><span data-stu-id="142fa-163">`globalPackagesFolder` applies only to `project.json`.</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="142fa-164">Referência ao arquivo nuspec</span><span class="sxs-lookup"><span data-stu-id="142fa-164">nuspec file reference</span></span>

<span data-ttu-id="142fa-165">*Originalmente em [Referência a nuspec](../reference/nuspec.md).*</span><span class="sxs-lookup"><span data-stu-id="142fa-165">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="142fa-166">O elemento `<contentFiles>` é usado em vez de `<files>` com `project.json`.</span><span class="sxs-lookup"><span data-stu-id="142fa-166">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="142fa-167">Controle de opções do Gerenciador de Pacotes</span><span class="sxs-lookup"><span data-stu-id="142fa-167">Package manager options control</span></span>

<span data-ttu-id="142fa-168">*Originalmente em [Referência da interface do usuário do Gerenciador de Pacotes](../tools/package-manager-ui.md).*</span><span class="sxs-lookup"><span data-stu-id="142fa-168">*Originally in [Package Manager UI reference](../tools/package-manager-ui.md).*</span></span>

<span data-ttu-id="142fa-169">Os projetos que usam o formato de referência `project.json` mostram apenas a opção **Mostrar janela de visualização**.</span><span class="sxs-lookup"><span data-stu-id="142fa-169">Projects using `project.json` reference format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="142fa-170">Modelos do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="142fa-170">Visual Studio Templates</span></span>

<span data-ttu-id="142fa-171">*Originalmente em [Pacotes NuGet em modelos do Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*</span><span class="sxs-lookup"><span data-stu-id="142fa-171">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="142fa-172">Práticas recomendadas: os modelos não incluem um arquivo `project.json`, nem incluem referências ou conteúdo que seria adicionado quando os pacotes NuGet são instalados.</span><span class="sxs-lookup"><span data-stu-id="142fa-172">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>