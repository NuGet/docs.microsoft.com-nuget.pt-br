---
title: Empacotamento e restauração do NuGet como destinos do MSBuild
description: O pack e restore do NuGet podem funcionar diretamente como destinos do MSBuild com o NuGet 4.0 e superior.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 8403ae38b5d2e907c6f06b162a18cdcd5425565b
ms.sourcegitcommit: 5aa49478dc466c67db5c3edda7c6ce8dcd8ae033
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68817526"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="3b00e-103">Empacotamento e restauração do NuGet como destinos do MSBuild</span><span class="sxs-lookup"><span data-stu-id="3b00e-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="3b00e-104">*NuGet 4.0 ou superior*</span><span class="sxs-lookup"><span data-stu-id="3b00e-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="3b00e-105">Com o formato [PackageReference](../consume-packages/package-references-in-project-files.md) , o NuGet 4.0 + pode armazenar todos os metadados do manifesto diretamente dentro de um arquivo de projeto `.nuspec` em vez de usar um arquivo separado.</span><span class="sxs-lookup"><span data-stu-id="3b00e-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="3b00e-106">Com o MSBuild 15.1 ou superior, o NuGet também é um cidadão de primeira classe do MSBuild com os destinos `pack` e `restore`, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="3b00e-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="3b00e-107">Esses destinos permitem que você trabalhe com o NuGet como faria com qualquer outra tarefa ou destino do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3b00e-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="3b00e-108">Para obter instruções sobre como criar um pacote NuGet usando o MSBuild, consulte [criar um pacote NuGet usando o MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="3b00e-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="3b00e-109">(Para NuGet 3.x e anteriores, use os comandos [pack](../reference/cli-reference/cli-ref-pack.md) e [restore](../reference/cli-reference/cli-ref-restore.md) na CLI do NuGet.)</span><span class="sxs-lookup"><span data-stu-id="3b00e-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="3b00e-110">Ordem de build de destino</span><span class="sxs-lookup"><span data-stu-id="3b00e-110">Target build order</span></span>

<span data-ttu-id="3b00e-111">Como `pack` e `restore` são os destinos do MSBuild, você pode acessá-los para melhorar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3b00e-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="3b00e-112">Por exemplo, digamos que você deseja copiar o pacote para um compartilhamento de rede após empacotá-lo.</span><span class="sxs-lookup"><span data-stu-id="3b00e-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="3b00e-113">Você pode fazer isso adicionando o seguinte ao seu arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="3b00e-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="3b00e-114">Da mesma forma, você pode gravar uma tarefa do MSBuild, escrever seu próprio destino e consumir propriedades do NuGet na tarefa de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3b00e-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="3b00e-115">pack target</span><span class="sxs-lookup"><span data-stu-id="3b00e-115">pack target</span></span>

<span data-ttu-id="3b00e-116">Para projetos de .net Standard usando o formato PackageReference, `msbuild -t:pack` o uso de desenha entradas do arquivo de projeto para usar na criação de um pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="3b00e-116">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="3b00e-117">A tabela abaixo descreve as propriedades do MSBuild que podem ser adicionadas a um arquivo do projeto dentro do primeiro nó `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="3b00e-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="3b00e-118">Você pode fazer essas edições facilmente no Visual Studio 2017 e posterior clicando com o botão direito do mouse no projeto e selecionando **Editar {project_name}** no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="3b00e-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="3b00e-119">Para sua conveniência, a tabela é organizada pela propriedade equivalente em um arquivo [`.nuspec` ](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="3b00e-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="3b00e-120">Observe que as propriedades `Owners` e `Summary` de `.nuspec` não são compatíveis com o MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3b00e-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="3b00e-121">Valor de atributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="3b00e-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="3b00e-122">Propriedade do MSBuild</span><span class="sxs-lookup"><span data-stu-id="3b00e-122">MSBuild Property</span></span> | <span data-ttu-id="3b00e-123">Padrão</span><span class="sxs-lookup"><span data-stu-id="3b00e-123">Default</span></span> | <span data-ttu-id="3b00e-124">Observações</span><span class="sxs-lookup"><span data-stu-id="3b00e-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="3b00e-125">Id</span><span class="sxs-lookup"><span data-stu-id="3b00e-125">Id</span></span> | <span data-ttu-id="3b00e-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="3b00e-126">PackageId</span></span> | <span data-ttu-id="3b00e-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="3b00e-127">AssemblyName</span></span> | <span data-ttu-id="3b00e-128">$(AssemblyName) do MSBuild</span><span class="sxs-lookup"><span data-stu-id="3b00e-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="3b00e-129">Versão</span><span class="sxs-lookup"><span data-stu-id="3b00e-129">Version</span></span> | <span data-ttu-id="3b00e-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="3b00e-130">PackageVersion</span></span> | <span data-ttu-id="3b00e-131">Versão</span><span class="sxs-lookup"><span data-stu-id="3b00e-131">Version</span></span> | <span data-ttu-id="3b00e-132">Isso é compatível com semver, por exemplo “1.0.0”, “1.0.0-beta” ou “1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="3b00e-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="3b00e-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="3b00e-133">VersionPrefix</span></span> | <span data-ttu-id="3b00e-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="3b00e-134">PackageVersionPrefix</span></span> | <span data-ttu-id="3b00e-135">empty</span><span class="sxs-lookup"><span data-stu-id="3b00e-135">empty</span></span> | <span data-ttu-id="3b00e-136">A configuração PackageVersion substitui PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="3b00e-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="3b00e-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="3b00e-137">VersionSuffix</span></span> | <span data-ttu-id="3b00e-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="3b00e-138">PackageVersionSuffix</span></span> | <span data-ttu-id="3b00e-139">empty</span><span class="sxs-lookup"><span data-stu-id="3b00e-139">empty</span></span> | <span data-ttu-id="3b00e-140">$(VersionSuffix) do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3b00e-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="3b00e-141">A configuração PackageVersion substitui PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="3b00e-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="3b00e-142">Autores</span><span class="sxs-lookup"><span data-stu-id="3b00e-142">Authors</span></span> | <span data-ttu-id="3b00e-143">Autores</span><span class="sxs-lookup"><span data-stu-id="3b00e-143">Authors</span></span> | <span data-ttu-id="3b00e-144">Nome do usuário atual</span><span class="sxs-lookup"><span data-stu-id="3b00e-144">Username of the current user</span></span> | |
| <span data-ttu-id="3b00e-145">Proprietários</span><span class="sxs-lookup"><span data-stu-id="3b00e-145">Owners</span></span> | <span data-ttu-id="3b00e-146">N/D</span><span class="sxs-lookup"><span data-stu-id="3b00e-146">N/A</span></span> | <span data-ttu-id="3b00e-147">Não está presente no NuSpec</span><span class="sxs-lookup"><span data-stu-id="3b00e-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="3b00e-148">Título</span><span class="sxs-lookup"><span data-stu-id="3b00e-148">Title</span></span> | <span data-ttu-id="3b00e-149">Título</span><span class="sxs-lookup"><span data-stu-id="3b00e-149">Title</span></span> | <span data-ttu-id="3b00e-150">O PackageId</span><span class="sxs-lookup"><span data-stu-id="3b00e-150">The PackageId</span></span>| |
| <span data-ttu-id="3b00e-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="3b00e-151">Description</span></span> | <span data-ttu-id="3b00e-152">Descrição</span><span class="sxs-lookup"><span data-stu-id="3b00e-152">Description</span></span> | <span data-ttu-id="3b00e-153">“Package Description”</span><span class="sxs-lookup"><span data-stu-id="3b00e-153">"Package Description"</span></span> | |
| <span data-ttu-id="3b00e-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="3b00e-154">Copyright</span></span> | <span data-ttu-id="3b00e-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="3b00e-155">Copyright</span></span> | <span data-ttu-id="3b00e-156">empty</span><span class="sxs-lookup"><span data-stu-id="3b00e-156">empty</span></span> | |
| <span data-ttu-id="3b00e-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3b00e-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="3b00e-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3b00e-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="3b00e-159">false</span><span class="sxs-lookup"><span data-stu-id="3b00e-159">false</span></span> | |
| <span data-ttu-id="3b00e-160">carteira</span><span class="sxs-lookup"><span data-stu-id="3b00e-160">license</span></span> | <span data-ttu-id="3b00e-161">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="3b00e-161">PackageLicenseExpression</span></span> | <span data-ttu-id="3b00e-162">empty</span><span class="sxs-lookup"><span data-stu-id="3b00e-162">empty</span></span> | <span data-ttu-id="3b00e-163">Corresponde a`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="3b00e-163">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="3b00e-164">carteira</span><span class="sxs-lookup"><span data-stu-id="3b00e-164">license</span></span> | <span data-ttu-id="3b00e-165">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="3b00e-165">PackageLicenseFile</span></span> | <span data-ttu-id="3b00e-166">empty</span><span class="sxs-lookup"><span data-stu-id="3b00e-166">empty</span></span> | <span data-ttu-id="3b00e-167">Corresponde ao `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="3b00e-167">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="3b00e-168">Talvez seja necessário empacotar explicitamente o arquivo de licença referenciado.</span><span class="sxs-lookup"><span data-stu-id="3b00e-168">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="3b00e-169">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3b00e-169">LicenseUrl</span></span> | <span data-ttu-id="3b00e-170">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3b00e-170">PackageLicenseUrl</span></span> | <span data-ttu-id="3b00e-171">empty</span><span class="sxs-lookup"><span data-stu-id="3b00e-171">empty</span></span> | <span data-ttu-id="3b00e-172">`licenseUrl`está sendo preterido, use a propriedade PackageLicenseExpression ou PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="3b00e-172">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="3b00e-173">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3b00e-173">ProjectUrl</span></span> | <span data-ttu-id="3b00e-174">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3b00e-174">PackageProjectUrl</span></span> | <span data-ttu-id="3b00e-175">empty</span><span class="sxs-lookup"><span data-stu-id="3b00e-175">empty</span></span> | |
| <span data-ttu-id="3b00e-176">IconUrl</span><span class="sxs-lookup"><span data-stu-id="3b00e-176">IconUrl</span></span> | <span data-ttu-id="3b00e-177">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="3b00e-177">PackageIconUrl</span></span> | <span data-ttu-id="3b00e-178">empty</span><span class="sxs-lookup"><span data-stu-id="3b00e-178">empty</span></span> | |
| <span data-ttu-id="3b00e-179">Marcas</span><span class="sxs-lookup"><span data-stu-id="3b00e-179">Tags</span></span> | <span data-ttu-id="3b00e-180">PackageTags</span><span class="sxs-lookup"><span data-stu-id="3b00e-180">PackageTags</span></span> | <span data-ttu-id="3b00e-181">empty</span><span class="sxs-lookup"><span data-stu-id="3b00e-181">empty</span></span> | <span data-ttu-id="3b00e-182">Marcas são delimitadas por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="3b00e-182">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="3b00e-183">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3b00e-183">ReleaseNotes</span></span> | <span data-ttu-id="3b00e-184">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3b00e-184">PackageReleaseNotes</span></span> | <span data-ttu-id="3b00e-185">empty</span><span class="sxs-lookup"><span data-stu-id="3b00e-185">empty</span></span> | |
| <span data-ttu-id="3b00e-186">Repositório/URL</span><span class="sxs-lookup"><span data-stu-id="3b00e-186">Repository/Url</span></span> | <span data-ttu-id="3b00e-187">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="3b00e-187">RepositoryUrl</span></span> | <span data-ttu-id="3b00e-188">empty</span><span class="sxs-lookup"><span data-stu-id="3b00e-188">empty</span></span> | <span data-ttu-id="3b00e-189">URL do repositório usada para clonar ou recuperar o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="3b00e-189">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="3b00e-190">Exemplo *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="3b00e-190">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="3b00e-191">Repositório/tipo</span><span class="sxs-lookup"><span data-stu-id="3b00e-191">Repository/Type</span></span> | <span data-ttu-id="3b00e-192">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="3b00e-192">RepositoryType</span></span> | <span data-ttu-id="3b00e-193">empty</span><span class="sxs-lookup"><span data-stu-id="3b00e-193">empty</span></span> | <span data-ttu-id="3b00e-194">Tipo de repositório.</span><span class="sxs-lookup"><span data-stu-id="3b00e-194">Repository type.</span></span> <span data-ttu-id="3b00e-195">Exemplos: *git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="3b00e-195">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="3b00e-196">Repositório/Branch</span><span class="sxs-lookup"><span data-stu-id="3b00e-196">Repository/Branch</span></span> | <span data-ttu-id="3b00e-197">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="3b00e-197">RepositoryBranch</span></span> | <span data-ttu-id="3b00e-198">empty</span><span class="sxs-lookup"><span data-stu-id="3b00e-198">empty</span></span> | <span data-ttu-id="3b00e-199">Informações opcionais da ramificação do repositório.</span><span class="sxs-lookup"><span data-stu-id="3b00e-199">Optional repository branch information.</span></span> <span data-ttu-id="3b00e-200">*RepositoryUrl* também deve ser especificado para que essa propriedade seja incluída.</span><span class="sxs-lookup"><span data-stu-id="3b00e-200">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="3b00e-201">Exemplo: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="3b00e-201">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="3b00e-202">Repositório/confirmação</span><span class="sxs-lookup"><span data-stu-id="3b00e-202">Repository/Commit</span></span> | <span data-ttu-id="3b00e-203">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="3b00e-203">RepositoryCommit</span></span> | <span data-ttu-id="3b00e-204">empty</span><span class="sxs-lookup"><span data-stu-id="3b00e-204">empty</span></span> | <span data-ttu-id="3b00e-205">Confirmação opcional do repositório ou conjunto de alterações para indicar de qual fonte o pacote foi criado.</span><span class="sxs-lookup"><span data-stu-id="3b00e-205">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="3b00e-206">*RepositoryUrl* também deve ser especificado para que essa propriedade seja incluída.</span><span class="sxs-lookup"><span data-stu-id="3b00e-206">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="3b00e-207">Exemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="3b00e-207">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="3b00e-208">PackageType</span><span class="sxs-lookup"><span data-stu-id="3b00e-208">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="3b00e-209">Resumo</span><span class="sxs-lookup"><span data-stu-id="3b00e-209">Summary</span></span> | <span data-ttu-id="3b00e-210">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="3b00e-210">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="3b00e-211">pack target inputs</span><span class="sxs-lookup"><span data-stu-id="3b00e-211">pack target inputs</span></span>

- <span data-ttu-id="3b00e-212">IsPackable</span><span class="sxs-lookup"><span data-stu-id="3b00e-212">IsPackable</span></span>
- <span data-ttu-id="3b00e-213">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="3b00e-213">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="3b00e-214">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="3b00e-214">PackageVersion</span></span>
- <span data-ttu-id="3b00e-215">PackageId</span><span class="sxs-lookup"><span data-stu-id="3b00e-215">PackageId</span></span>
- <span data-ttu-id="3b00e-216">Autores</span><span class="sxs-lookup"><span data-stu-id="3b00e-216">Authors</span></span>
- <span data-ttu-id="3b00e-217">Descrição</span><span class="sxs-lookup"><span data-stu-id="3b00e-217">Description</span></span>
- <span data-ttu-id="3b00e-218">Copyright</span><span class="sxs-lookup"><span data-stu-id="3b00e-218">Copyright</span></span>
- <span data-ttu-id="3b00e-219">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3b00e-219">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="3b00e-220">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="3b00e-220">DevelopmentDependency</span></span>
- <span data-ttu-id="3b00e-221">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="3b00e-221">PackageLicenseExpression</span></span>
- <span data-ttu-id="3b00e-222">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="3b00e-222">PackageLicenseFile</span></span>
- <span data-ttu-id="3b00e-223">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="3b00e-223">PackageLicenseUrl</span></span>
- <span data-ttu-id="3b00e-224">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="3b00e-224">PackageProjectUrl</span></span>
- <span data-ttu-id="3b00e-225">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="3b00e-225">PackageIconUrl</span></span>
- <span data-ttu-id="3b00e-226">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="3b00e-226">PackageReleaseNotes</span></span>
- <span data-ttu-id="3b00e-227">PackageTags</span><span class="sxs-lookup"><span data-stu-id="3b00e-227">PackageTags</span></span>
- <span data-ttu-id="3b00e-228">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="3b00e-228">PackageOutputPath</span></span>
- <span data-ttu-id="3b00e-229">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="3b00e-229">IncludeSymbols</span></span>
- <span data-ttu-id="3b00e-230">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="3b00e-230">IncludeSource</span></span>
- <span data-ttu-id="3b00e-231">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="3b00e-231">PackageTypes</span></span>
- <span data-ttu-id="3b00e-232">IsTool</span><span class="sxs-lookup"><span data-stu-id="3b00e-232">IsTool</span></span>
- <span data-ttu-id="3b00e-233">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="3b00e-233">RepositoryUrl</span></span>
- <span data-ttu-id="3b00e-234">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="3b00e-234">RepositoryType</span></span>
- <span data-ttu-id="3b00e-235">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="3b00e-235">RepositoryBranch</span></span>
- <span data-ttu-id="3b00e-236">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="3b00e-236">RepositoryCommit</span></span>
- <span data-ttu-id="3b00e-237">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="3b00e-237">NoPackageAnalysis</span></span>
- <span data-ttu-id="3b00e-238">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="3b00e-238">MinClientVersion</span></span>
- <span data-ttu-id="3b00e-239">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="3b00e-239">IncludeBuildOutput</span></span>
- <span data-ttu-id="3b00e-240">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="3b00e-240">IncludeContentInPack</span></span>
- <span data-ttu-id="3b00e-241">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="3b00e-241">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="3b00e-242">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="3b00e-242">ContentTargetFolders</span></span>
- <span data-ttu-id="3b00e-243">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="3b00e-243">NuspecFile</span></span>
- <span data-ttu-id="3b00e-244">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="3b00e-244">NuspecBasePath</span></span>
- <span data-ttu-id="3b00e-245">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="3b00e-245">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="3b00e-246">pack scenarios</span><span class="sxs-lookup"><span data-stu-id="3b00e-246">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="3b00e-247">Suprimir dependências</span><span class="sxs-lookup"><span data-stu-id="3b00e-247">Suppress dependencies</span></span>

<span data-ttu-id="3b00e-248">Para suprimir dependências de pacote do pacote NuGet `SuppressDependenciesWhenPacking` gerado `true` , defina como que permitirá ignorar todas as dependências do arquivo nupkg gerado.</span><span class="sxs-lookup"><span data-stu-id="3b00e-248">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="3b00e-249">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="3b00e-249">PackageIconUrl</span></span>

<span data-ttu-id="3b00e-250">Como parte da alteração do [problema do NuGet 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` eventualmente será alterado para `PackageIconUri` e pode ser um caminho relativo para um arquivo de ícone que será incluído na raiz do pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="3b00e-250">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="3b00e-251">Assemblies de saída</span><span class="sxs-lookup"><span data-stu-id="3b00e-251">Output assemblies</span></span>

<span data-ttu-id="3b00e-252">O `nuget pack` copia arquivos de saída com extensões `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="3b00e-252">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="3b00e-253">Os arquivos de saída que são copiados dependem do que o MSBuild fornece do destino `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="3b00e-253">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="3b00e-254">Há duas propriedades de MSBuild que você pode usar em seu arquivo de projeto ou a linha de comando para controlar onde ficam os assemblies de saída:</span><span class="sxs-lookup"><span data-stu-id="3b00e-254">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="3b00e-255">`IncludeBuildOutput`: Um booliano que determina se os assemblies de saída de compilação devem ser incluídos no pacote.</span><span class="sxs-lookup"><span data-stu-id="3b00e-255">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="3b00e-256">`BuildOutputTargetFolder`: Especifica a pasta na qual os assemblies de saída devem ser colocados.</span><span class="sxs-lookup"><span data-stu-id="3b00e-256">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="3b00e-257">Os assemblies de saída (e outros arquivos de saída) são copiados para suas respectivas pastas de estrutura.</span><span class="sxs-lookup"><span data-stu-id="3b00e-257">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="3b00e-258">Referências de pacote</span><span class="sxs-lookup"><span data-stu-id="3b00e-258">Package references</span></span>

<span data-ttu-id="3b00e-259">Consulte [Referências de pacote em arquivos de projeto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="3b00e-259">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="3b00e-260">Referências de projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="3b00e-260">Project to project references</span></span>

<span data-ttu-id="3b00e-261">As referências projeto a projeto são consideradas como referências de pacote do nuget por padrão, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b00e-261">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="3b00e-262">Você também pode adicionar os seguintes metadados à referência de projeto:</span><span class="sxs-lookup"><span data-stu-id="3b00e-262">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="3b00e-263">Incluindo o conteúdo em um pacote</span><span class="sxs-lookup"><span data-stu-id="3b00e-263">Including content in a package</span></span>

<span data-ttu-id="3b00e-264">Para incluir o conteúdo, adicione metadados extras ao item `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="3b00e-264">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="3b00e-265">Por padrão, tudo que pertencer ao tipo “Conteúdo” é incluído no pacote, a menos que seja substituído por entradas como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="3b00e-265">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="3b00e-266">Por padrão, tudo é adicionado à raiz da pasta `content` e `contentFiles\any\<target_framework>` dentro de um pacote e preserva a estrutura e pasta relativa, a menos que você especifique um caminho de pacote:</span><span class="sxs-lookup"><span data-stu-id="3b00e-266">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="3b00e-267">Se você quiser copiar todo o conteúdo somente para determinadas pastas raiz (em vez de para `content` e `contentFiles`), será possível usar a propriedade `ContentTargetFolders` do MSBuild, que assume como padrão "content;contentFiles", mas pode ser definida como qualquer outro nome de pasta.</span><span class="sxs-lookup"><span data-stu-id="3b00e-267">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="3b00e-268">Observe que só especificar “contentFiles” em `ContentTargetFolders` coloca os arquivos em `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` com base em `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="3b00e-268">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="3b00e-269">`PackagePath` pode ser um conjunto de caminhos de destino separados por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="3b00e-269">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="3b00e-270">Especificar um caminho de pacote vazio adicionaria o arquivo à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="3b00e-270">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="3b00e-271">Por exemplo, o seguinte adiciona `libuv.txt` a `content\myfiles`, `content\samples` e a raiz do pacote:</span><span class="sxs-lookup"><span data-stu-id="3b00e-271">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="3b00e-272">Há também uma propriedade de MSBuild `$(IncludeContentInPack)`, que assume o padrão `true`.</span><span class="sxs-lookup"><span data-stu-id="3b00e-272">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="3b00e-273">Se isso for definido como `false` em qualquer projeto, o conteúdo desse projeto não está incluso no pacote do nuget.</span><span class="sxs-lookup"><span data-stu-id="3b00e-273">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="3b00e-274">Outros metadados específicos do pacote que pode ser definido em qualquer um dos itens acima ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, que define os valores ```CopyToOutput``` e ```Flatten``` na entrada ```contentFiles``` no nuspec de saída.</span><span class="sxs-lookup"><span data-stu-id="3b00e-274">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="3b00e-275">Além de itens de Conteúdo, os metadados `<Pack>` e `<PackagePath>` também podem ser definidos em arquivos com uma ação de Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.</span><span class="sxs-lookup"><span data-stu-id="3b00e-275">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="3b00e-276">Para o pacote acrescentar o nome de arquivo ao caminho do pacote ao usar padrões glob, seu caminho de pacote deve terminar com o caractere separador de pasta, caso contrário, o caminho do pacote será tratado como o caminho completo, incluindo o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="3b00e-276">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="3b00e-277">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="3b00e-277">IncludeSymbols</span></span>

<span data-ttu-id="3b00e-278">Ao usar o `MSBuild -t:pack -p:IncludeSymbols=true`, os arquivos `.pdb` correspondentes são copiados junto com outros arquivos de saída (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="3b00e-278">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="3b00e-279">Observe que a configuração `IncludeSymbols=true` cria um pacote regular *e* um pacote de símbolos.</span><span class="sxs-lookup"><span data-stu-id="3b00e-279">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="3b00e-280">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="3b00e-280">IncludeSource</span></span>

<span data-ttu-id="3b00e-281">Isso é o mesmo que `IncludeSymbols`, exceto que também copia os arquivos de origem com arquivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="3b00e-281">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="3b00e-282">Todos os arquivos do tipo `Compile` são copiadas para `src\<ProjectName>\`, preservando a estrutura de pastas do caminho relativo no pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="3b00e-282">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="3b00e-283">O mesmo também ocorre para arquivos de origem de qualquer `ProjectReference` que tem `TreatAsPackageReference` definido como `false`.</span><span class="sxs-lookup"><span data-stu-id="3b00e-283">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="3b00e-284">Se um arquivo do tipo Compilação estiver fora da pasta de projeto, ele será adicionado apenas a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="3b00e-284">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="3b00e-285">Empacotando uma expressão de licença ou um arquivo de licença</span><span class="sxs-lookup"><span data-stu-id="3b00e-285">Packing a license expression or a license file</span></span>

<span data-ttu-id="3b00e-286">Ao usar uma expressão de licença, a propriedade PackageLicenseExpression deve ser usada.</span><span class="sxs-lookup"><span data-stu-id="3b00e-286">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="3b00e-287">[Exemplo de expressão de licença](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="3b00e-287">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="3b00e-288">[Saiba mais sobre as expressões de licença e as licenças que são aceitas pelo NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="3b00e-288">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="3b00e-289">Ao empacotar um arquivo de licença, você precisa usar a propriedade PackageLicenseFile para especificar o caminho do pacote, em relação à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="3b00e-289">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="3b00e-290">Além disso, você precisa certificar-se de que o arquivo está incluído no pacote.</span><span class="sxs-lookup"><span data-stu-id="3b00e-290">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="3b00e-291">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b00e-291">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="3b00e-292">[Exemplo de arquivo de licença](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="3b00e-292">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="3b00e-293">IsTool</span><span class="sxs-lookup"><span data-stu-id="3b00e-293">IsTool</span></span>

<span data-ttu-id="3b00e-294">Ao usar `MSBuild -t:pack -p:IsTool=true`, todos os arquivos de saída, conforme especificado no cenário [Assemblies de saída](#output-assemblies), são copiados para a pasta `tools` em vez da pasta `lib`.</span><span class="sxs-lookup"><span data-stu-id="3b00e-294">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="3b00e-295">Observe que isso é diferente de um `DotNetCliTool` que é especificado pela configuração do `PackageType` no arquivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="3b00e-295">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="3b00e-296">Empacotamento usando um .nuspec</span><span class="sxs-lookup"><span data-stu-id="3b00e-296">Packing using a .nuspec</span></span>

<span data-ttu-id="3b00e-297">Embora seja recomendável [incluir todas as propriedades](../reference/msbuild-targets.md#pack-target) que normalmente estão no `.nuspec` arquivo no arquivo de projeto, você pode optar por usar um `.nuspec` arquivo para empacotar seu projeto.</span><span class="sxs-lookup"><span data-stu-id="3b00e-297">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="3b00e-298">Para um projeto de estilo não-SDK que usa `PackageReference`o, você deve `NuGet.Build.Tasks.Pack.targets` importar para que a tarefa de pacote possa ser executada.</span><span class="sxs-lookup"><span data-stu-id="3b00e-298">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="3b00e-299">Você ainda precisa restaurar o projeto antes de poder empacotar um arquivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="3b00e-299">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="3b00e-300">(Um projeto no estilo SDK inclui os destinos do pacote por padrão.)</span><span class="sxs-lookup"><span data-stu-id="3b00e-300">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="3b00e-301">A estrutura de destino do arquivo de projeto é irrelevante e não é usada ao empacotar um nuspec.</span><span class="sxs-lookup"><span data-stu-id="3b00e-301">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="3b00e-302">As três propriedades MSBuild a seguir são relevantes para empacotamento usando um `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="3b00e-302">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="3b00e-303">`NuspecFile`: caminho relativo ou absoluto para o arquivo `.nuspec` que está sendo usado para o empacotamento.</span><span class="sxs-lookup"><span data-stu-id="3b00e-303">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="3b00e-304">`NuspecProperties`: uma lista separada por ponto e vírgula de pares chave/valor.</span><span class="sxs-lookup"><span data-stu-id="3b00e-304">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="3b00e-305">Devido à maneira como a análise de linha de comando do MSBuild funciona, várias propriedades precisam ser especificadas da seguinte maneira: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="3b00e-305">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="3b00e-306">`NuspecBasePath`: Caminho base do `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="3b00e-306">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="3b00e-307">Se estiver usando `dotnet.exe` para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3b00e-307">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="3b00e-308">Se estiver usando o MSBuild para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3b00e-308">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="3b00e-309">Observe que empacotar um nuspec usando dotNet. exe ou MSBuild também leva a criar o projeto por padrão.</span><span class="sxs-lookup"><span data-stu-id="3b00e-309">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="3b00e-310">Isso pode ser evitado passando ```--no-build``` a propriedade para dotnet. exe, que é o equivalente à ```<NoBuild>true</NoBuild> ``` configuração em seu arquivo de projeto, juntamente ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` com a configuração no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="3b00e-310">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="3b00e-311">Um exemplo de um arquivo *. csproj* para empacotar um arquivo nuspec é:</span><span class="sxs-lookup"><span data-stu-id="3b00e-311">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="3b00e-312">Pontos de extensão avançados para criar pacote personalizado</span><span class="sxs-lookup"><span data-stu-id="3b00e-312">Advanced extension points to create customized package</span></span>

<span data-ttu-id="3b00e-313">O `pack` destino fornece dois pontos de extensão que são executados na compilação interna, específica da estrutura de destino.</span><span class="sxs-lookup"><span data-stu-id="3b00e-313">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="3b00e-314">Os pontos de extensão dão suporte à inclusão de conteúdo específico da estrutura de destino e assemblies em um pacote:</span><span class="sxs-lookup"><span data-stu-id="3b00e-314">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="3b00e-315">`TargetsForTfmSpecificBuildOutput`alvo Use para arquivos dentro da `lib` pasta ou de uma pasta especificada `BuildOutputTargetFolder`usando.</span><span class="sxs-lookup"><span data-stu-id="3b00e-315">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="3b00e-316">`TargetsForTfmSpecificContentInPackage`alvo Use para arquivos fora do `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="3b00e-316">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="3b00e-317">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="3b00e-317">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="3b00e-318">Escreva um destino personalizado e especifique-o como o valor da `$(TargetsForTfmSpecificBuildOutput)` propriedade.</span><span class="sxs-lookup"><span data-stu-id="3b00e-318">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="3b00e-319">Para todos os arquivos que precisam entrar em `BuildOutputTargetFolder` (lib por padrão), o destino deve gravar esses arquivos no grupo `BuildOutputInPackage` de itens e definir os dois valores de metadados a seguir:</span><span class="sxs-lookup"><span data-stu-id="3b00e-319">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="3b00e-320">`FinalOutputPath`: O caminho absoluto do arquivo; Se não for fornecido, a identidade será usada para avaliar o caminho de origem.</span><span class="sxs-lookup"><span data-stu-id="3b00e-320">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="3b00e-321">`TargetPath`:  Adicional Defina quando o arquivo precisa entrar em uma subpasta no `lib\<TargetFramework>` , como assemblies satélite que estão sob suas respectivas pastas de cultura.</span><span class="sxs-lookup"><span data-stu-id="3b00e-321">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="3b00e-322">O padrão é o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="3b00e-322">Defaults to the name of the file.</span></span>

<span data-ttu-id="3b00e-323">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b00e-323">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="3b00e-324">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="3b00e-324">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="3b00e-325">Escreva um destino personalizado e especifique-o como o valor da `$(TargetsForTfmSpecificContentInPackage)` propriedade.</span><span class="sxs-lookup"><span data-stu-id="3b00e-325">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="3b00e-326">Para todos os arquivos a serem incluídos no pacote, o destino deve gravar esses arquivos no grupo `TfmSpecificPackageFile` de itens e definir os seguintes metadados opcionais:</span><span class="sxs-lookup"><span data-stu-id="3b00e-326">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="3b00e-327">`PackagePath`: Caminho em que o arquivo deve ser apresentado no pacote.</span><span class="sxs-lookup"><span data-stu-id="3b00e-327">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="3b00e-328">O NuGet emitirá um aviso se mais de um arquivo for adicionado ao mesmo caminho de pacote.</span><span class="sxs-lookup"><span data-stu-id="3b00e-328">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="3b00e-329">`BuildAction`: A ação de compilação a ser atribuída ao arquivo, necessária somente se o caminho do pacote estiver `contentFiles` na pasta.</span><span class="sxs-lookup"><span data-stu-id="3b00e-329">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="3b00e-330">O padrão é "None".</span><span class="sxs-lookup"><span data-stu-id="3b00e-330">Defaults to "None".</span></span>

<span data-ttu-id="3b00e-331">Um exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b00e-331">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="3b00e-332">restore target</span><span class="sxs-lookup"><span data-stu-id="3b00e-332">restore target</span></span>

<span data-ttu-id="3b00e-333">`MSBuild -t:restore` (que `nuget restore` e `dotnet restore` usam com projetos do .NET Core), restaura pacotes referenciados no arquivo de projeto da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3b00e-333">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="3b00e-334">Ler todas as referências projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="3b00e-334">Read all project to project references</span></span>
1. <span data-ttu-id="3b00e-335">Ler as propriedades do projeto para localizar a pasta intermediária e as estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="3b00e-335">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="3b00e-336">Transmitir dados do MSBuild para NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="3b00e-336">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="3b00e-337">Executar restauração</span><span class="sxs-lookup"><span data-stu-id="3b00e-337">Run restore</span></span>
1. <span data-ttu-id="3b00e-338">Baixar os pacotes</span><span class="sxs-lookup"><span data-stu-id="3b00e-338">Download packages</span></span>
1. <span data-ttu-id="3b00e-339">Gravar arquivo de ativos, destinos e objetos</span><span class="sxs-lookup"><span data-stu-id="3b00e-339">Write assets file, targets, and props</span></span>

<span data-ttu-id="3b00e-340">O `restore` destino funciona **apenas** para projetos que usam o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="3b00e-340">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="3b00e-341">Ele não funciona para projetos que usam o `packages.config` formato; em vez disso, use a [restauração do NuGet](../reference/cli-reference/cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="3b00e-341">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="3b00e-342">Restaurar propriedades</span><span class="sxs-lookup"><span data-stu-id="3b00e-342">Restore properties</span></span>

<span data-ttu-id="3b00e-343">Configurações de restauração adicionais podem vir de propriedades MSBuild no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="3b00e-343">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="3b00e-344">Os valores também podem ser definidos na linha de comando usando a opção `-p:` (consulte os Exemplos abaixo).</span><span class="sxs-lookup"><span data-stu-id="3b00e-344">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="3b00e-345">Propriedade</span><span class="sxs-lookup"><span data-stu-id="3b00e-345">Property</span></span> | <span data-ttu-id="3b00e-346">Descrição</span><span class="sxs-lookup"><span data-stu-id="3b00e-346">Description</span></span> |
|--------|--------|
| <span data-ttu-id="3b00e-347">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="3b00e-347">RestoreSources</span></span> | <span data-ttu-id="3b00e-348">Uma lista delimitada por ponto e vírgula de origens de pacote.</span><span class="sxs-lookup"><span data-stu-id="3b00e-348">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="3b00e-349">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="3b00e-349">RestorePackagesPath</span></span> | <span data-ttu-id="3b00e-350">Caminho da pasta dos pacotes do usuário.</span><span class="sxs-lookup"><span data-stu-id="3b00e-350">User packages folder path.</span></span> |
| <span data-ttu-id="3b00e-351">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="3b00e-351">RestoreDisableParallel</span></span> | <span data-ttu-id="3b00e-352">Limite os downloads para um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="3b00e-352">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="3b00e-353">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="3b00e-353">RestoreConfigFile</span></span> | <span data-ttu-id="3b00e-354">Caminho para um arquivo `Nuget.Config` a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="3b00e-354">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="3b00e-355">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="3b00e-355">RestoreNoCache</span></span> | <span data-ttu-id="3b00e-356">Se for true, evita o uso de pacotes armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="3b00e-356">If true, avoids using cached packages.</span></span> <span data-ttu-id="3b00e-357">Consulte [Gerenciando os pacotes globais e as pastas de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="3b00e-357">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="3b00e-358">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="3b00e-358">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="3b00e-359">Se verdadeiro, ignora origens de pacote com falha ou ausentes.</span><span class="sxs-lookup"><span data-stu-id="3b00e-359">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="3b00e-360">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="3b00e-360">RestoreFallbackFolders</span></span> | <span data-ttu-id="3b00e-361">Pastas de fallback, usadas da mesma maneira que a pasta pacotes de usuário é usada.</span><span class="sxs-lookup"><span data-stu-id="3b00e-361">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="3b00e-362">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="3b00e-362">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="3b00e-363">Fontes adicionais a serem usadas durante a restauração.</span><span class="sxs-lookup"><span data-stu-id="3b00e-363">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="3b00e-364">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="3b00e-364">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="3b00e-365">Pastas de fallback adicionais a serem usadas durante a restauração.</span><span class="sxs-lookup"><span data-stu-id="3b00e-365">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="3b00e-366">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="3b00e-366">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="3b00e-367">Exclui as pastas de fallback especificadas em`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="3b00e-367">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="3b00e-368">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="3b00e-368">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="3b00e-369">Caminho para `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="3b00e-369">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="3b00e-370">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="3b00e-370">RestoreGraphProjectInput</span></span> | <span data-ttu-id="3b00e-371">Lista separada por ponto e vírgula de projetos a serem restaurados, que devem conter caminhos absolutos.</span><span class="sxs-lookup"><span data-stu-id="3b00e-371">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="3b00e-372">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="3b00e-372">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="3b00e-373">Quando os projetos são coletados via MSBuild, ele determina se eles são coletados usando a `SkipNonexistentTargets` otimização.</span><span class="sxs-lookup"><span data-stu-id="3b00e-373">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="3b00e-374">Quando não definido, o padrão é `true`.</span><span class="sxs-lookup"><span data-stu-id="3b00e-374">When not set, defaults to `true`.</span></span> <span data-ttu-id="3b00e-375">A conseqüência é um comportamento com falha rápida quando os destinos de um projeto não podem ser importados.</span><span class="sxs-lookup"><span data-stu-id="3b00e-375">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="3b00e-376">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="3b00e-376">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="3b00e-377">Pasta de saída, padronizando `BaseIntermediateOutputPath` para e `obj` a pasta.</span><span class="sxs-lookup"><span data-stu-id="3b00e-377">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="3b00e-378">Exemplos</span><span class="sxs-lookup"><span data-stu-id="3b00e-378">Examples</span></span>

<span data-ttu-id="3b00e-379">Linha de comando:</span><span class="sxs-lookup"><span data-stu-id="3b00e-379">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="3b00e-380">Arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="3b00e-380">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="3b00e-381">Restaurar saídas</span><span class="sxs-lookup"><span data-stu-id="3b00e-381">Restore outputs</span></span>

<span data-ttu-id="3b00e-382">A restauração cria os seguintes arquivos na pasta `obj` de build:</span><span class="sxs-lookup"><span data-stu-id="3b00e-382">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="3b00e-383">Arquivo</span><span class="sxs-lookup"><span data-stu-id="3b00e-383">File</span></span> | <span data-ttu-id="3b00e-384">Descrição</span><span class="sxs-lookup"><span data-stu-id="3b00e-384">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="3b00e-385">Contém o grafo de dependência de todas as referências de pacote.</span><span class="sxs-lookup"><span data-stu-id="3b00e-385">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="3b00e-386">Referências a objetos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="3b00e-386">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="3b00e-387">Referências a destinos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="3b00e-387">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="3b00e-388">Restaurando e compilando com um comando do MSBuild</span><span class="sxs-lookup"><span data-stu-id="3b00e-388">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="3b00e-389">Devido ao fato de que o NuGet pode restaurar pacotes que desativam destinos e props do MSBuild, as avaliações de restauração e compilação são executadas com propriedades globais diferentes.</span><span class="sxs-lookup"><span data-stu-id="3b00e-389">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="3b00e-390">Isso significa que o seguinte terá um comportamento imprevisível e geralmente incorreto.</span><span class="sxs-lookup"><span data-stu-id="3b00e-390">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="3b00e-391">Em vez disso, a abordagem recomendada é:</span><span class="sxs-lookup"><span data-stu-id="3b00e-391">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="3b00e-392">A mesma lógica se aplica a outros destinos semelhantes `build`a.</span><span class="sxs-lookup"><span data-stu-id="3b00e-392">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="3b00e-393">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="3b00e-393">PackageTargetFallback</span></span>

<span data-ttu-id="3b00e-394">O elemento `PackageTargetFallback` permite especificar um conjunto de destinos compatíveis a serem usados ao restaurar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="3b00e-394">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="3b00e-395">Ele foi desenvolvido para permitir que os pacotes que usam o dotnet [TxM](../reference/target-frameworks.md) funcionem com pacotes compatíveis que não declaram um dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="3b00e-395">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="3b00e-396">Ou seja, se o projeto usar o dotnet TxM, todos os pacotes dos quais ele depende também deverão ter um dotnet TxM, a menos que você adicione o `<PackageTargetFallback>` ao projeto para permitir que plataformas não dotnet sejam compatíveis com o dotnet.</span><span class="sxs-lookup"><span data-stu-id="3b00e-396">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="3b00e-397">Por exemplo, se o projeto está usando o `netstandard1.6` TxM e um pacote dependente contém apenas `lib/net45/a.dll` e `lib/portable-net45+win81/a.dll`, o projeto não será compilado.</span><span class="sxs-lookup"><span data-stu-id="3b00e-397">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="3b00e-398">Se a DLL que você deseja colocar é esta última, é possível adicionar um `PackageTargetFallback` como mostrado a seguir para dizer que a DLL `portable-net45+win81` é compatível:</span><span class="sxs-lookup"><span data-stu-id="3b00e-398">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="3b00e-399">Para declarar um fallback para todos os destinos em seu projeto, deixe o atributo `Condition` de fora.</span><span class="sxs-lookup"><span data-stu-id="3b00e-399">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="3b00e-400">Você também pode estender qualquer `PackageTargetFallback` existente incluindo `$(PackageTargetFallback)` conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="3b00e-400">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="3b00e-401">Substituindo uma biblioteca de um grafo de restauração</span><span class="sxs-lookup"><span data-stu-id="3b00e-401">Replacing one library from a restore graph</span></span>

<span data-ttu-id="3b00e-402">Se uma restauração está trazendo o assembly errado, é possível excluir a escolha padrão do pacote e substituí-lo por outro de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="3b00e-402">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="3b00e-403">Primeiro com um `PackageReference` de nível superior, exclua todos os ativos:</span><span class="sxs-lookup"><span data-stu-id="3b00e-403">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="3b00e-404">Em seguida, adicione sua própria referência à cópia local apropriada da DLL:</span><span class="sxs-lookup"><span data-stu-id="3b00e-404">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
