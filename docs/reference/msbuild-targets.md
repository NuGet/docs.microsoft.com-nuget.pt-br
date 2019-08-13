---
title: Empacotamento e restauração do NuGet como destinos do MSBuild
description: O pack e restore do NuGet podem funcionar diretamente como destinos do MSBuild com o NuGet 4.0 e superior.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: d8d1b2ef0185381d16c1bb73035588fe90bcfd14
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959688"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="79782-103">Empacotamento e restauração do NuGet como destinos do MSBuild</span><span class="sxs-lookup"><span data-stu-id="79782-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="79782-104">*NuGet 4.0 ou superior*</span><span class="sxs-lookup"><span data-stu-id="79782-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="79782-105">Com o formato [PackageReference](../consume-packages/package-references-in-project-files.md) , o NuGet 4.0 + pode armazenar todos os metadados do manifesto diretamente dentro de um arquivo de projeto `.nuspec` em vez de usar um arquivo separado.</span><span class="sxs-lookup"><span data-stu-id="79782-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="79782-106">Com o MSBuild 15.1 ou superior, o NuGet também é um cidadão de primeira classe do MSBuild com os destinos `pack` e `restore`, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="79782-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="79782-107">Esses destinos permitem que você trabalhe com o NuGet como faria com qualquer outra tarefa ou destino do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="79782-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="79782-108">Para obter instruções sobre como criar um pacote NuGet usando o MSBuild, consulte [criar um pacote NuGet usando o MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="79782-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="79782-109">(Para NuGet 3.x e anteriores, use os comandos [pack](../reference/cli-reference/cli-ref-pack.md) e [restore](../reference/cli-reference/cli-ref-restore.md) na CLI do NuGet.)</span><span class="sxs-lookup"><span data-stu-id="79782-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="79782-110">Ordem de build de destino</span><span class="sxs-lookup"><span data-stu-id="79782-110">Target build order</span></span>

<span data-ttu-id="79782-111">Como `pack` e `restore` são os destinos do MSBuild, você pode acessá-los para melhorar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="79782-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="79782-112">Por exemplo, digamos que você deseja copiar o pacote para um compartilhamento de rede após empacotá-lo.</span><span class="sxs-lookup"><span data-stu-id="79782-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="79782-113">Você pode fazer isso adicionando o seguinte ao seu arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="79782-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="79782-114">Da mesma forma, você pode gravar uma tarefa do MSBuild, escrever seu próprio destino e consumir propriedades do NuGet na tarefa de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="79782-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="79782-115">`$(OutputPath)`é relativo e espera que você esteja executando o comando da raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="79782-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="79782-116">pack target</span><span class="sxs-lookup"><span data-stu-id="79782-116">pack target</span></span>

<span data-ttu-id="79782-117">Para projetos de .net Standard usando o formato PackageReference, `msbuild -t:pack` o uso de desenha entradas do arquivo de projeto para usar na criação de um pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="79782-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="79782-118">A tabela abaixo descreve as propriedades do MSBuild que podem ser adicionadas a um arquivo do projeto dentro do primeiro nó `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="79782-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="79782-119">Você pode fazer essas edições facilmente no Visual Studio 2017 e posterior clicando com o botão direito do mouse no projeto e selecionando **Editar {project_name}** no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="79782-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="79782-120">Para sua conveniência, a tabela é organizada pela propriedade equivalente em um arquivo [`.nuspec` ](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="79782-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="79782-121">Observe que as propriedades `Owners` e `Summary` de `.nuspec` não são compatíveis com o MSBuild.</span><span class="sxs-lookup"><span data-stu-id="79782-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="79782-122">Valor de atributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="79782-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="79782-123">Propriedade do MSBuild</span><span class="sxs-lookup"><span data-stu-id="79782-123">MSBuild Property</span></span> | <span data-ttu-id="79782-124">Padrão</span><span class="sxs-lookup"><span data-stu-id="79782-124">Default</span></span> | <span data-ttu-id="79782-125">Observações</span><span class="sxs-lookup"><span data-stu-id="79782-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="79782-126">Id</span><span class="sxs-lookup"><span data-stu-id="79782-126">Id</span></span> | <span data-ttu-id="79782-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="79782-127">PackageId</span></span> | <span data-ttu-id="79782-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="79782-128">AssemblyName</span></span> | <span data-ttu-id="79782-129">$(AssemblyName) do MSBuild</span><span class="sxs-lookup"><span data-stu-id="79782-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="79782-130">Versão</span><span class="sxs-lookup"><span data-stu-id="79782-130">Version</span></span> | <span data-ttu-id="79782-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="79782-131">PackageVersion</span></span> | <span data-ttu-id="79782-132">Versão</span><span class="sxs-lookup"><span data-stu-id="79782-132">Version</span></span> | <span data-ttu-id="79782-133">Isso é compatível com semver, por exemplo “1.0.0”, “1.0.0-beta” ou “1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="79782-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="79782-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="79782-134">VersionPrefix</span></span> | <span data-ttu-id="79782-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="79782-135">PackageVersionPrefix</span></span> | <span data-ttu-id="79782-136">empty</span><span class="sxs-lookup"><span data-stu-id="79782-136">empty</span></span> | <span data-ttu-id="79782-137">A configuração PackageVersion substitui PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="79782-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="79782-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="79782-138">VersionSuffix</span></span> | <span data-ttu-id="79782-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="79782-139">PackageVersionSuffix</span></span> | <span data-ttu-id="79782-140">empty</span><span class="sxs-lookup"><span data-stu-id="79782-140">empty</span></span> | <span data-ttu-id="79782-141">$(VersionSuffix) do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="79782-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="79782-142">A configuração PackageVersion substitui PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="79782-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="79782-143">Autores</span><span class="sxs-lookup"><span data-stu-id="79782-143">Authors</span></span> | <span data-ttu-id="79782-144">Autores</span><span class="sxs-lookup"><span data-stu-id="79782-144">Authors</span></span> | <span data-ttu-id="79782-145">Nome do usuário atual</span><span class="sxs-lookup"><span data-stu-id="79782-145">Username of the current user</span></span> | |
| <span data-ttu-id="79782-146">Proprietários</span><span class="sxs-lookup"><span data-stu-id="79782-146">Owners</span></span> | <span data-ttu-id="79782-147">N/D</span><span class="sxs-lookup"><span data-stu-id="79782-147">N/A</span></span> | <span data-ttu-id="79782-148">Não está presente no NuSpec</span><span class="sxs-lookup"><span data-stu-id="79782-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="79782-149">Título</span><span class="sxs-lookup"><span data-stu-id="79782-149">Title</span></span> | <span data-ttu-id="79782-150">Título</span><span class="sxs-lookup"><span data-stu-id="79782-150">Title</span></span> | <span data-ttu-id="79782-151">O PackageId</span><span class="sxs-lookup"><span data-stu-id="79782-151">The PackageId</span></span>| |
| <span data-ttu-id="79782-152">Descrição</span><span class="sxs-lookup"><span data-stu-id="79782-152">Description</span></span> | <span data-ttu-id="79782-153">Descrição</span><span class="sxs-lookup"><span data-stu-id="79782-153">Description</span></span> | <span data-ttu-id="79782-154">“Package Description”</span><span class="sxs-lookup"><span data-stu-id="79782-154">"Package Description"</span></span> | |
| <span data-ttu-id="79782-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="79782-155">Copyright</span></span> | <span data-ttu-id="79782-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="79782-156">Copyright</span></span> | <span data-ttu-id="79782-157">empty</span><span class="sxs-lookup"><span data-stu-id="79782-157">empty</span></span> | |
| <span data-ttu-id="79782-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="79782-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="79782-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="79782-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="79782-160">false</span><span class="sxs-lookup"><span data-stu-id="79782-160">false</span></span> | |
| <span data-ttu-id="79782-161">carteira</span><span class="sxs-lookup"><span data-stu-id="79782-161">license</span></span> | <span data-ttu-id="79782-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="79782-162">PackageLicenseExpression</span></span> | <span data-ttu-id="79782-163">empty</span><span class="sxs-lookup"><span data-stu-id="79782-163">empty</span></span> | <span data-ttu-id="79782-164">Corresponde a`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="79782-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="79782-165">carteira</span><span class="sxs-lookup"><span data-stu-id="79782-165">license</span></span> | <span data-ttu-id="79782-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="79782-166">PackageLicenseFile</span></span> | <span data-ttu-id="79782-167">empty</span><span class="sxs-lookup"><span data-stu-id="79782-167">empty</span></span> | <span data-ttu-id="79782-168">Corresponde ao `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="79782-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="79782-169">Talvez seja necessário empacotar explicitamente o arquivo de licença referenciado.</span><span class="sxs-lookup"><span data-stu-id="79782-169">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="79782-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="79782-170">LicenseUrl</span></span> | <span data-ttu-id="79782-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="79782-171">PackageLicenseUrl</span></span> | <span data-ttu-id="79782-172">empty</span><span class="sxs-lookup"><span data-stu-id="79782-172">empty</span></span> | <span data-ttu-id="79782-173">`licenseUrl`está sendo preterido, use a propriedade PackageLicenseExpression ou PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="79782-173">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="79782-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="79782-174">ProjectUrl</span></span> | <span data-ttu-id="79782-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="79782-175">PackageProjectUrl</span></span> | <span data-ttu-id="79782-176">empty</span><span class="sxs-lookup"><span data-stu-id="79782-176">empty</span></span> | |
| <span data-ttu-id="79782-177">IconUrl</span><span class="sxs-lookup"><span data-stu-id="79782-177">IconUrl</span></span> | <span data-ttu-id="79782-178">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="79782-178">PackageIconUrl</span></span> | <span data-ttu-id="79782-179">empty</span><span class="sxs-lookup"><span data-stu-id="79782-179">empty</span></span> | |
| <span data-ttu-id="79782-180">Marcas</span><span class="sxs-lookup"><span data-stu-id="79782-180">Tags</span></span> | <span data-ttu-id="79782-181">PackageTags</span><span class="sxs-lookup"><span data-stu-id="79782-181">PackageTags</span></span> | <span data-ttu-id="79782-182">empty</span><span class="sxs-lookup"><span data-stu-id="79782-182">empty</span></span> | <span data-ttu-id="79782-183">Marcas são delimitadas por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="79782-183">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="79782-184">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="79782-184">ReleaseNotes</span></span> | <span data-ttu-id="79782-185">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="79782-185">PackageReleaseNotes</span></span> | <span data-ttu-id="79782-186">empty</span><span class="sxs-lookup"><span data-stu-id="79782-186">empty</span></span> | |
| <span data-ttu-id="79782-187">Repositório/URL</span><span class="sxs-lookup"><span data-stu-id="79782-187">Repository/Url</span></span> | <span data-ttu-id="79782-188">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="79782-188">RepositoryUrl</span></span> | <span data-ttu-id="79782-189">empty</span><span class="sxs-lookup"><span data-stu-id="79782-189">empty</span></span> | <span data-ttu-id="79782-190">URL do repositório usada para clonar ou recuperar o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="79782-190">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="79782-191">Exemplo *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="79782-191">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="79782-192">Repositório/tipo</span><span class="sxs-lookup"><span data-stu-id="79782-192">Repository/Type</span></span> | <span data-ttu-id="79782-193">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="79782-193">RepositoryType</span></span> | <span data-ttu-id="79782-194">empty</span><span class="sxs-lookup"><span data-stu-id="79782-194">empty</span></span> | <span data-ttu-id="79782-195">Tipo de repositório.</span><span class="sxs-lookup"><span data-stu-id="79782-195">Repository type.</span></span> <span data-ttu-id="79782-196">Exemplos: *git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="79782-196">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="79782-197">Repositório/Branch</span><span class="sxs-lookup"><span data-stu-id="79782-197">Repository/Branch</span></span> | <span data-ttu-id="79782-198">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="79782-198">RepositoryBranch</span></span> | <span data-ttu-id="79782-199">empty</span><span class="sxs-lookup"><span data-stu-id="79782-199">empty</span></span> | <span data-ttu-id="79782-200">Informações opcionais da ramificação do repositório.</span><span class="sxs-lookup"><span data-stu-id="79782-200">Optional repository branch information.</span></span> <span data-ttu-id="79782-201">*RepositoryUrl* também deve ser especificado para que essa propriedade seja incluída.</span><span class="sxs-lookup"><span data-stu-id="79782-201">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="79782-202">Exemplo: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="79782-202">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="79782-203">Repositório/confirmação</span><span class="sxs-lookup"><span data-stu-id="79782-203">Repository/Commit</span></span> | <span data-ttu-id="79782-204">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="79782-204">RepositoryCommit</span></span> | <span data-ttu-id="79782-205">empty</span><span class="sxs-lookup"><span data-stu-id="79782-205">empty</span></span> | <span data-ttu-id="79782-206">Confirmação opcional do repositório ou conjunto de alterações para indicar de qual fonte o pacote foi criado.</span><span class="sxs-lookup"><span data-stu-id="79782-206">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="79782-207">*RepositoryUrl* também deve ser especificado para que essa propriedade seja incluída.</span><span class="sxs-lookup"><span data-stu-id="79782-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="79782-208">Exemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="79782-208">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="79782-209">PackageType</span><span class="sxs-lookup"><span data-stu-id="79782-209">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="79782-210">Resumo</span><span class="sxs-lookup"><span data-stu-id="79782-210">Summary</span></span> | <span data-ttu-id="79782-211">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="79782-211">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="79782-212">pack target inputs</span><span class="sxs-lookup"><span data-stu-id="79782-212">pack target inputs</span></span>

- <span data-ttu-id="79782-213">IsPackable</span><span class="sxs-lookup"><span data-stu-id="79782-213">IsPackable</span></span>
- <span data-ttu-id="79782-214">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="79782-214">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="79782-215">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="79782-215">PackageVersion</span></span>
- <span data-ttu-id="79782-216">PackageId</span><span class="sxs-lookup"><span data-stu-id="79782-216">PackageId</span></span>
- <span data-ttu-id="79782-217">Autores</span><span class="sxs-lookup"><span data-stu-id="79782-217">Authors</span></span>
- <span data-ttu-id="79782-218">Descrição</span><span class="sxs-lookup"><span data-stu-id="79782-218">Description</span></span>
- <span data-ttu-id="79782-219">Copyright</span><span class="sxs-lookup"><span data-stu-id="79782-219">Copyright</span></span>
- <span data-ttu-id="79782-220">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="79782-220">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="79782-221">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="79782-221">DevelopmentDependency</span></span>
- <span data-ttu-id="79782-222">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="79782-222">PackageLicenseExpression</span></span>
- <span data-ttu-id="79782-223">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="79782-223">PackageLicenseFile</span></span>
- <span data-ttu-id="79782-224">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="79782-224">PackageLicenseUrl</span></span>
- <span data-ttu-id="79782-225">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="79782-225">PackageProjectUrl</span></span>
- <span data-ttu-id="79782-226">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="79782-226">PackageIconUrl</span></span>
- <span data-ttu-id="79782-227">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="79782-227">PackageReleaseNotes</span></span>
- <span data-ttu-id="79782-228">PackageTags</span><span class="sxs-lookup"><span data-stu-id="79782-228">PackageTags</span></span>
- <span data-ttu-id="79782-229">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="79782-229">PackageOutputPath</span></span>
- <span data-ttu-id="79782-230">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="79782-230">IncludeSymbols</span></span>
- <span data-ttu-id="79782-231">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="79782-231">IncludeSource</span></span>
- <span data-ttu-id="79782-232">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="79782-232">PackageTypes</span></span>
- <span data-ttu-id="79782-233">IsTool</span><span class="sxs-lookup"><span data-stu-id="79782-233">IsTool</span></span>
- <span data-ttu-id="79782-234">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="79782-234">RepositoryUrl</span></span>
- <span data-ttu-id="79782-235">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="79782-235">RepositoryType</span></span>
- <span data-ttu-id="79782-236">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="79782-236">RepositoryBranch</span></span>
- <span data-ttu-id="79782-237">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="79782-237">RepositoryCommit</span></span>
- <span data-ttu-id="79782-238">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="79782-238">NoPackageAnalysis</span></span>
- <span data-ttu-id="79782-239">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="79782-239">MinClientVersion</span></span>
- <span data-ttu-id="79782-240">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="79782-240">IncludeBuildOutput</span></span>
- <span data-ttu-id="79782-241">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="79782-241">IncludeContentInPack</span></span>
- <span data-ttu-id="79782-242">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="79782-242">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="79782-243">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="79782-243">ContentTargetFolders</span></span>
- <span data-ttu-id="79782-244">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="79782-244">NuspecFile</span></span>
- <span data-ttu-id="79782-245">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="79782-245">NuspecBasePath</span></span>
- <span data-ttu-id="79782-246">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="79782-246">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="79782-247">pack scenarios</span><span class="sxs-lookup"><span data-stu-id="79782-247">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="79782-248">Suprimir dependências</span><span class="sxs-lookup"><span data-stu-id="79782-248">Suppress dependencies</span></span>

<span data-ttu-id="79782-249">Para suprimir dependências de pacote do pacote NuGet `SuppressDependenciesWhenPacking` gerado `true` , defina como que permitirá ignorar todas as dependências do arquivo nupkg gerado.</span><span class="sxs-lookup"><span data-stu-id="79782-249">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="79782-250">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="79782-250">PackageIconUrl</span></span>

<span data-ttu-id="79782-251">Como parte da alteração do [problema do NuGet 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` eventualmente será alterado para `PackageIconUri` e pode ser um caminho relativo para um arquivo de ícone que será incluído na raiz do pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="79782-251">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="79782-252">Assemblies de saída</span><span class="sxs-lookup"><span data-stu-id="79782-252">Output assemblies</span></span>

<span data-ttu-id="79782-253">O `nuget pack` copia arquivos de saída com extensões `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="79782-253">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="79782-254">Os arquivos de saída que são copiados dependem do que o MSBuild fornece do destino `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="79782-254">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="79782-255">Há duas propriedades de MSBuild que você pode usar em seu arquivo de projeto ou a linha de comando para controlar onde ficam os assemblies de saída:</span><span class="sxs-lookup"><span data-stu-id="79782-255">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="79782-256">`IncludeBuildOutput`: Um booliano que determina se os assemblies de saída de compilação devem ser incluídos no pacote.</span><span class="sxs-lookup"><span data-stu-id="79782-256">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="79782-257">`BuildOutputTargetFolder`: Especifica a pasta na qual os assemblies de saída devem ser colocados.</span><span class="sxs-lookup"><span data-stu-id="79782-257">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="79782-258">Os assemblies de saída (e outros arquivos de saída) são copiados para suas respectivas pastas de estrutura.</span><span class="sxs-lookup"><span data-stu-id="79782-258">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="79782-259">Referências de pacote</span><span class="sxs-lookup"><span data-stu-id="79782-259">Package references</span></span>

<span data-ttu-id="79782-260">Consulte [Referências de pacote em arquivos de projeto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="79782-260">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="79782-261">Referências de projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="79782-261">Project to project references</span></span>

<span data-ttu-id="79782-262">As referências projeto a projeto são consideradas como referências de pacote do nuget por padrão, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="79782-262">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="79782-263">Você também pode adicionar os seguintes metadados à referência de projeto:</span><span class="sxs-lookup"><span data-stu-id="79782-263">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="79782-264">Incluindo o conteúdo em um pacote</span><span class="sxs-lookup"><span data-stu-id="79782-264">Including content in a package</span></span>

<span data-ttu-id="79782-265">Para incluir o conteúdo, adicione metadados extras ao item `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="79782-265">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="79782-266">Por padrão, tudo que pertencer ao tipo “Conteúdo” é incluído no pacote, a menos que seja substituído por entradas como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="79782-266">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="79782-267">Por padrão, tudo é adicionado à raiz da pasta `content` e `contentFiles\any\<target_framework>` dentro de um pacote e preserva a estrutura e pasta relativa, a menos que você especifique um caminho de pacote:</span><span class="sxs-lookup"><span data-stu-id="79782-267">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="79782-268">Se você quiser copiar todo o conteúdo somente para determinadas pastas raiz (em vez de para `content` e `contentFiles`), será possível usar a propriedade `ContentTargetFolders` do MSBuild, que assume como padrão "content;contentFiles", mas pode ser definida como qualquer outro nome de pasta.</span><span class="sxs-lookup"><span data-stu-id="79782-268">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="79782-269">Observe que só especificar “contentFiles” em `ContentTargetFolders` coloca os arquivos em `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` com base em `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="79782-269">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="79782-270">`PackagePath` pode ser um conjunto de caminhos de destino separados por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="79782-270">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="79782-271">Especificar um caminho de pacote vazio adicionaria o arquivo à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="79782-271">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="79782-272">Por exemplo, o seguinte adiciona `libuv.txt` a `content\myfiles`, `content\samples` e a raiz do pacote:</span><span class="sxs-lookup"><span data-stu-id="79782-272">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="79782-273">Há também uma propriedade de MSBuild `$(IncludeContentInPack)`, que assume o padrão `true`.</span><span class="sxs-lookup"><span data-stu-id="79782-273">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="79782-274">Se isso for definido como `false` em qualquer projeto, o conteúdo desse projeto não está incluso no pacote do nuget.</span><span class="sxs-lookup"><span data-stu-id="79782-274">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="79782-275">Outros metadados específicos do pacote que pode ser definido em qualquer um dos itens acima ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, que define os valores ```CopyToOutput``` e ```Flatten``` na entrada ```contentFiles``` no nuspec de saída.</span><span class="sxs-lookup"><span data-stu-id="79782-275">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="79782-276">Além de itens de Conteúdo, os metadados `<Pack>` e `<PackagePath>` também podem ser definidos em arquivos com uma ação de Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.</span><span class="sxs-lookup"><span data-stu-id="79782-276">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="79782-277">Para o pacote acrescentar o nome de arquivo ao caminho do pacote ao usar padrões glob, seu caminho de pacote deve terminar com o caractere separador de pasta, caso contrário, o caminho do pacote será tratado como o caminho completo, incluindo o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="79782-277">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="79782-278">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="79782-278">IncludeSymbols</span></span>

<span data-ttu-id="79782-279">Ao usar o `MSBuild -t:pack -p:IncludeSymbols=true`, os arquivos `.pdb` correspondentes são copiados junto com outros arquivos de saída (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="79782-279">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="79782-280">Observe que a configuração `IncludeSymbols=true` cria um pacote regular *e* um pacote de símbolos.</span><span class="sxs-lookup"><span data-stu-id="79782-280">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="79782-281">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="79782-281">IncludeSource</span></span>

<span data-ttu-id="79782-282">Isso é o mesmo que `IncludeSymbols`, exceto que também copia os arquivos de origem com arquivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="79782-282">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="79782-283">Todos os arquivos do tipo `Compile` são copiadas para `src\<ProjectName>\`, preservando a estrutura de pastas do caminho relativo no pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="79782-283">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="79782-284">O mesmo também ocorre para arquivos de origem de qualquer `ProjectReference` que tem `TreatAsPackageReference` definido como `false`.</span><span class="sxs-lookup"><span data-stu-id="79782-284">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="79782-285">Se um arquivo do tipo Compilação estiver fora da pasta de projeto, ele será adicionado apenas a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="79782-285">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="79782-286">Empacotando uma expressão de licença ou um arquivo de licença</span><span class="sxs-lookup"><span data-stu-id="79782-286">Packing a license expression or a license file</span></span>

<span data-ttu-id="79782-287">Ao usar uma expressão de licença, a propriedade PackageLicenseExpression deve ser usada.</span><span class="sxs-lookup"><span data-stu-id="79782-287">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="79782-288">[Exemplo de expressão de licença](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="79782-288">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="79782-289">[Saiba mais sobre as expressões de licença e as licenças que são aceitas pelo NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="79782-289">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="79782-290">Ao empacotar um arquivo de licença, você precisa usar a propriedade PackageLicenseFile para especificar o caminho do pacote, em relação à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="79782-290">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="79782-291">Além disso, você precisa certificar-se de que o arquivo está incluído no pacote.</span><span class="sxs-lookup"><span data-stu-id="79782-291">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="79782-292">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="79782-292">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="79782-293">[Exemplo de arquivo de licença](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="79782-293">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="79782-294">IsTool</span><span class="sxs-lookup"><span data-stu-id="79782-294">IsTool</span></span>

<span data-ttu-id="79782-295">Ao usar `MSBuild -t:pack -p:IsTool=true`, todos os arquivos de saída, conforme especificado no cenário [Assemblies de saída](#output-assemblies), são copiados para a pasta `tools` em vez da pasta `lib`.</span><span class="sxs-lookup"><span data-stu-id="79782-295">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="79782-296">Observe que isso é diferente de um `DotNetCliTool` que é especificado pela configuração do `PackageType` no arquivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="79782-296">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="79782-297">Empacotamento usando um .nuspec</span><span class="sxs-lookup"><span data-stu-id="79782-297">Packing using a .nuspec</span></span>

<span data-ttu-id="79782-298">Embora seja recomendável [incluir todas as propriedades](../reference/msbuild-targets.md#pack-target) que normalmente estão no `.nuspec` arquivo no arquivo de projeto, você pode optar por usar um `.nuspec` arquivo para empacotar seu projeto.</span><span class="sxs-lookup"><span data-stu-id="79782-298">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="79782-299">Para um projeto de estilo não-SDK que usa `PackageReference`o, você deve `NuGet.Build.Tasks.Pack.targets` importar para que a tarefa de pacote possa ser executada.</span><span class="sxs-lookup"><span data-stu-id="79782-299">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="79782-300">Você ainda precisa restaurar o projeto antes de poder empacotar um arquivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="79782-300">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="79782-301">(Um projeto no estilo SDK inclui os destinos do pacote por padrão.)</span><span class="sxs-lookup"><span data-stu-id="79782-301">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="79782-302">A estrutura de destino do arquivo de projeto é irrelevante e não é usada ao empacotar um nuspec.</span><span class="sxs-lookup"><span data-stu-id="79782-302">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="79782-303">As três propriedades MSBuild a seguir são relevantes para empacotamento usando um `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="79782-303">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="79782-304">`NuspecFile`: caminho relativo ou absoluto para o arquivo `.nuspec` que está sendo usado para o empacotamento.</span><span class="sxs-lookup"><span data-stu-id="79782-304">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="79782-305">`NuspecProperties`: uma lista separada por ponto e vírgula de pares chave/valor.</span><span class="sxs-lookup"><span data-stu-id="79782-305">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="79782-306">Devido à maneira como a análise de linha de comando do MSBuild funciona, várias propriedades precisam ser especificadas da seguinte maneira: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="79782-306">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="79782-307">`NuspecBasePath`: Caminho base do `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="79782-307">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="79782-308">Se estiver usando `dotnet.exe` para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="79782-308">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="79782-309">Se estiver usando o MSBuild para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="79782-309">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="79782-310">Observe que empacotar um nuspec usando dotNet. exe ou MSBuild também leva a criar o projeto por padrão.</span><span class="sxs-lookup"><span data-stu-id="79782-310">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="79782-311">Isso pode ser evitado passando ```--no-build``` a propriedade para dotnet. exe, que é o equivalente à ```<NoBuild>true</NoBuild> ``` configuração em seu arquivo de projeto, juntamente ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` com a configuração no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="79782-311">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="79782-312">Um exemplo de um arquivo *. csproj* para empacotar um arquivo nuspec é:</span><span class="sxs-lookup"><span data-stu-id="79782-312">An example of a *.csproj* file to pack a nuspec file is:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="79782-313">Pontos de extensão avançados para criar pacote personalizado</span><span class="sxs-lookup"><span data-stu-id="79782-313">Advanced extension points to create customized package</span></span>

<span data-ttu-id="79782-314">O `pack` destino fornece dois pontos de extensão que são executados na compilação interna, específica da estrutura de destino.</span><span class="sxs-lookup"><span data-stu-id="79782-314">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="79782-315">Os pontos de extensão dão suporte à inclusão de conteúdo específico da estrutura de destino e assemblies em um pacote:</span><span class="sxs-lookup"><span data-stu-id="79782-315">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="79782-316">`TargetsForTfmSpecificBuildOutput`alvo Use para arquivos dentro da `lib` pasta ou de uma pasta especificada `BuildOutputTargetFolder`usando.</span><span class="sxs-lookup"><span data-stu-id="79782-316">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="79782-317">`TargetsForTfmSpecificContentInPackage`alvo Use para arquivos fora do `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="79782-317">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="79782-318">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="79782-318">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="79782-319">Escreva um destino personalizado e especifique-o como o valor da `$(TargetsForTfmSpecificBuildOutput)` propriedade.</span><span class="sxs-lookup"><span data-stu-id="79782-319">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="79782-320">Para todos os arquivos que precisam entrar em `BuildOutputTargetFolder` (lib por padrão), o destino deve gravar esses arquivos no grupo `BuildOutputInPackage` de itens e definir os dois valores de metadados a seguir:</span><span class="sxs-lookup"><span data-stu-id="79782-320">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="79782-321">`FinalOutputPath`: O caminho absoluto do arquivo; Se não for fornecido, a identidade será usada para avaliar o caminho de origem.</span><span class="sxs-lookup"><span data-stu-id="79782-321">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="79782-322">`TargetPath`:  Adicional Defina quando o arquivo precisa entrar em uma subpasta no `lib\<TargetFramework>` , como assemblies satélite que estão sob suas respectivas pastas de cultura.</span><span class="sxs-lookup"><span data-stu-id="79782-322">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="79782-323">O padrão é o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="79782-323">Defaults to the name of the file.</span></span>

<span data-ttu-id="79782-324">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="79782-324">Example:</span></span>

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="79782-325">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="79782-325">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="79782-326">Escreva um destino personalizado e especifique-o como o valor da `$(TargetsForTfmSpecificContentInPackage)` propriedade.</span><span class="sxs-lookup"><span data-stu-id="79782-326">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="79782-327">Para todos os arquivos a serem incluídos no pacote, o destino deve gravar esses arquivos no grupo `TfmSpecificPackageFile` de itens e definir os seguintes metadados opcionais:</span><span class="sxs-lookup"><span data-stu-id="79782-327">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="79782-328">`PackagePath`: Caminho em que o arquivo deve ser apresentado no pacote.</span><span class="sxs-lookup"><span data-stu-id="79782-328">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="79782-329">O NuGet emitirá um aviso se mais de um arquivo for adicionado ao mesmo caminho de pacote.</span><span class="sxs-lookup"><span data-stu-id="79782-329">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="79782-330">`BuildAction`: A ação de compilação a ser atribuída ao arquivo, necessária somente se o caminho do pacote estiver `contentFiles` na pasta.</span><span class="sxs-lookup"><span data-stu-id="79782-330">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="79782-331">O padrão é "None".</span><span class="sxs-lookup"><span data-stu-id="79782-331">Defaults to "None".</span></span>

<span data-ttu-id="79782-332">Um exemplo:</span><span class="sxs-lookup"><span data-stu-id="79782-332">An example:</span></span>
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a><span data-ttu-id="79782-333">restore target</span><span class="sxs-lookup"><span data-stu-id="79782-333">restore target</span></span>

<span data-ttu-id="79782-334">`MSBuild -t:restore` (que `nuget restore` e `dotnet restore` usam com projetos do .NET Core), restaura pacotes referenciados no arquivo de projeto da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="79782-334">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="79782-335">Ler todas as referências projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="79782-335">Read all project to project references</span></span>
1. <span data-ttu-id="79782-336">Ler as propriedades do projeto para localizar a pasta intermediária e as estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="79782-336">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="79782-337">Transmitir dados do MSBuild para NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="79782-337">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="79782-338">Executar restauração</span><span class="sxs-lookup"><span data-stu-id="79782-338">Run restore</span></span>
1. <span data-ttu-id="79782-339">Baixar os pacotes</span><span class="sxs-lookup"><span data-stu-id="79782-339">Download packages</span></span>
1. <span data-ttu-id="79782-340">Gravar arquivo de ativos, destinos e objetos</span><span class="sxs-lookup"><span data-stu-id="79782-340">Write assets file, targets, and props</span></span>

<span data-ttu-id="79782-341">O `restore` destino funciona **apenas** para projetos que usam o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="79782-341">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="79782-342">Ele não funciona para projetos que usam o `packages.config` formato; em vez disso, use a [restauração do NuGet](../reference/cli-reference/cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="79782-342">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="79782-343">Restaurar propriedades</span><span class="sxs-lookup"><span data-stu-id="79782-343">Restore properties</span></span>

<span data-ttu-id="79782-344">Configurações de restauração adicionais podem vir de propriedades MSBuild no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="79782-344">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="79782-345">Os valores também podem ser definidos na linha de comando usando a opção `-p:` (consulte os Exemplos abaixo).</span><span class="sxs-lookup"><span data-stu-id="79782-345">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="79782-346">Propriedade</span><span class="sxs-lookup"><span data-stu-id="79782-346">Property</span></span> | <span data-ttu-id="79782-347">Descrição</span><span class="sxs-lookup"><span data-stu-id="79782-347">Description</span></span> |
|--------|--------|
| <span data-ttu-id="79782-348">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="79782-348">RestoreSources</span></span> | <span data-ttu-id="79782-349">Uma lista delimitada por ponto e vírgula de origens de pacote.</span><span class="sxs-lookup"><span data-stu-id="79782-349">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="79782-350">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="79782-350">RestorePackagesPath</span></span> | <span data-ttu-id="79782-351">Caminho da pasta dos pacotes do usuário.</span><span class="sxs-lookup"><span data-stu-id="79782-351">User packages folder path.</span></span> |
| <span data-ttu-id="79782-352">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="79782-352">RestoreDisableParallel</span></span> | <span data-ttu-id="79782-353">Limite os downloads para um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="79782-353">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="79782-354">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="79782-354">RestoreConfigFile</span></span> | <span data-ttu-id="79782-355">Caminho para um arquivo `Nuget.Config` a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="79782-355">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="79782-356">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="79782-356">RestoreNoCache</span></span> | <span data-ttu-id="79782-357">Se for true, evita o uso de pacotes armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="79782-357">If true, avoids using cached packages.</span></span> <span data-ttu-id="79782-358">Consulte [Gerenciando os pacotes globais e as pastas de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="79782-358">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="79782-359">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="79782-359">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="79782-360">Se verdadeiro, ignora origens de pacote com falha ou ausentes.</span><span class="sxs-lookup"><span data-stu-id="79782-360">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="79782-361">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="79782-361">RestoreFallbackFolders</span></span> | <span data-ttu-id="79782-362">Pastas de fallback, usadas da mesma maneira que a pasta pacotes de usuário é usada.</span><span class="sxs-lookup"><span data-stu-id="79782-362">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="79782-363">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="79782-363">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="79782-364">Fontes adicionais a serem usadas durante a restauração.</span><span class="sxs-lookup"><span data-stu-id="79782-364">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="79782-365">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="79782-365">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="79782-366">Pastas de fallback adicionais a serem usadas durante a restauração.</span><span class="sxs-lookup"><span data-stu-id="79782-366">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="79782-367">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="79782-367">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="79782-368">Exclui as pastas de fallback especificadas em`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="79782-368">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="79782-369">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="79782-369">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="79782-370">Caminho para `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="79782-370">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="79782-371">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="79782-371">RestoreGraphProjectInput</span></span> | <span data-ttu-id="79782-372">Lista separada por ponto e vírgula de projetos a serem restaurados, que devem conter caminhos absolutos.</span><span class="sxs-lookup"><span data-stu-id="79782-372">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="79782-373">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="79782-373">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="79782-374">Quando os projetos são coletados via MSBuild, ele determina se eles são coletados usando a `SkipNonexistentTargets` otimização.</span><span class="sxs-lookup"><span data-stu-id="79782-374">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="79782-375">Quando não definido, o padrão é `true`.</span><span class="sxs-lookup"><span data-stu-id="79782-375">When not set, defaults to `true`.</span></span> <span data-ttu-id="79782-376">A conseqüência é um comportamento com falha rápida quando os destinos de um projeto não podem ser importados.</span><span class="sxs-lookup"><span data-stu-id="79782-376">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="79782-377">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="79782-377">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="79782-378">Pasta de saída, padronizando `BaseIntermediateOutputPath` para e `obj` a pasta.</span><span class="sxs-lookup"><span data-stu-id="79782-378">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="79782-379">Exemplos</span><span class="sxs-lookup"><span data-stu-id="79782-379">Examples</span></span>

<span data-ttu-id="79782-380">Linha de comando:</span><span class="sxs-lookup"><span data-stu-id="79782-380">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="79782-381">Arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="79782-381">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="79782-382">Restaurar saídas</span><span class="sxs-lookup"><span data-stu-id="79782-382">Restore outputs</span></span>

<span data-ttu-id="79782-383">A restauração cria os seguintes arquivos na pasta `obj` de build:</span><span class="sxs-lookup"><span data-stu-id="79782-383">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="79782-384">Arquivo</span><span class="sxs-lookup"><span data-stu-id="79782-384">File</span></span> | <span data-ttu-id="79782-385">Descrição</span><span class="sxs-lookup"><span data-stu-id="79782-385">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="79782-386">Contém o grafo de dependência de todas as referências de pacote.</span><span class="sxs-lookup"><span data-stu-id="79782-386">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="79782-387">Referências a objetos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="79782-387">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="79782-388">Referências a destinos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="79782-388">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="79782-389">Restaurando e compilando com um comando do MSBuild</span><span class="sxs-lookup"><span data-stu-id="79782-389">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="79782-390">Devido ao fato de que o NuGet pode restaurar pacotes que desativam destinos e props do MSBuild, as avaliações de restauração e compilação são executadas com propriedades globais diferentes.</span><span class="sxs-lookup"><span data-stu-id="79782-390">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="79782-391">Isso significa que o seguinte terá um comportamento imprevisível e geralmente incorreto.</span><span class="sxs-lookup"><span data-stu-id="79782-391">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="79782-392">Em vez disso, a abordagem recomendada é:</span><span class="sxs-lookup"><span data-stu-id="79782-392">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="79782-393">A mesma lógica se aplica a outros destinos semelhantes `build`a.</span><span class="sxs-lookup"><span data-stu-id="79782-393">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="79782-394">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="79782-394">PackageTargetFallback</span></span>

<span data-ttu-id="79782-395">O elemento `PackageTargetFallback` permite especificar um conjunto de destinos compatíveis a serem usados ao restaurar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="79782-395">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="79782-396">Ele foi desenvolvido para permitir que os pacotes que usam o dotnet [TxM](../reference/target-frameworks.md) funcionem com pacotes compatíveis que não declaram um dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="79782-396">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="79782-397">Ou seja, se o projeto usar o dotnet TxM, todos os pacotes dos quais ele depende também deverão ter um dotnet TxM, a menos que você adicione o `<PackageTargetFallback>` ao projeto para permitir que plataformas não dotnet sejam compatíveis com o dotnet.</span><span class="sxs-lookup"><span data-stu-id="79782-397">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="79782-398">Por exemplo, se o projeto está usando o `netstandard1.6` TxM e um pacote dependente contém apenas `lib/net45/a.dll` e `lib/portable-net45+win81/a.dll`, o projeto não será compilado.</span><span class="sxs-lookup"><span data-stu-id="79782-398">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="79782-399">Se a DLL que você deseja colocar é esta última, é possível adicionar um `PackageTargetFallback` como mostrado a seguir para dizer que a DLL `portable-net45+win81` é compatível:</span><span class="sxs-lookup"><span data-stu-id="79782-399">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="79782-400">Para declarar um fallback para todos os destinos em seu projeto, deixe o atributo `Condition` de fora.</span><span class="sxs-lookup"><span data-stu-id="79782-400">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="79782-401">Você também pode estender qualquer `PackageTargetFallback` existente incluindo `$(PackageTargetFallback)` conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="79782-401">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="79782-402">Substituindo uma biblioteca de um grafo de restauração</span><span class="sxs-lookup"><span data-stu-id="79782-402">Replacing one library from a restore graph</span></span>

<span data-ttu-id="79782-403">Se uma restauração está trazendo o assembly errado, é possível excluir a escolha padrão do pacote e substituí-lo por outro de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="79782-403">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="79782-404">Primeiro com um `PackageReference` de nível superior, exclua todos os ativos:</span><span class="sxs-lookup"><span data-stu-id="79782-404">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="79782-405">Em seguida, adicione sua própria referência à cópia local apropriada da DLL:</span><span class="sxs-lookup"><span data-stu-id="79782-405">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
