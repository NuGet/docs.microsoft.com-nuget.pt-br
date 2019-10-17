---
title: Empacotamento e restauração do NuGet como destinos do MSBuild
description: O pack e restore do NuGet podem funcionar diretamente como destinos do MSBuild com o NuGet 4.0 e superior.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 6a49e410617c14e22f0d4a67d8bfe280f64f5505
ms.sourcegitcommit: 8a424829b1f70cf7590e95db61997af6ae2d7a41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72510799"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="d372b-103">Empacotamento e restauração do NuGet como destinos do MSBuild</span><span class="sxs-lookup"><span data-stu-id="d372b-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="d372b-104">*NuGet 4.0 ou superior*</span><span class="sxs-lookup"><span data-stu-id="d372b-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="d372b-105">Com o formato [PackageReference](../consume-packages/package-references-in-project-files.md) , o NuGet 4.0 + pode armazenar todos os metadados do manifesto diretamente dentro de um arquivo de projeto em vez de usar um arquivo `.nuspec` separado.</span><span class="sxs-lookup"><span data-stu-id="d372b-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="d372b-106">Com o MSBuild 15.1 ou superior, o NuGet também é um cidadão de primeira classe do MSBuild com os destinos `pack` e `restore`, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="d372b-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="d372b-107">Esses destinos permitem que você trabalhe com o NuGet como faria com qualquer outra tarefa ou destino do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="d372b-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="d372b-108">Para obter instruções sobre como criar um pacote NuGet usando o MSBuild, consulte [criar um pacote NuGet usando o MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="d372b-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="d372b-109">(Para NuGet 3.x e anteriores, use os comandos [pack](../reference/cli-reference/cli-ref-pack.md) e [restore](../reference/cli-reference/cli-ref-restore.md) na CLI do NuGet.)</span><span class="sxs-lookup"><span data-stu-id="d372b-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="d372b-110">Ordem de build de destino</span><span class="sxs-lookup"><span data-stu-id="d372b-110">Target build order</span></span>

<span data-ttu-id="d372b-111">Como `pack` e `restore` são os destinos do MSBuild, você pode acessá-los para melhorar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d372b-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="d372b-112">Por exemplo, digamos que você deseja copiar o pacote para um compartilhamento de rede após empacotá-lo.</span><span class="sxs-lookup"><span data-stu-id="d372b-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="d372b-113">Você pode fazer isso adicionando o seguinte ao seu arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="d372b-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="d372b-114">Da mesma forma, você pode gravar uma tarefa do MSBuild, escrever seu próprio destino e consumir propriedades do NuGet na tarefa de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="d372b-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="d372b-115">`$(OutputPath)` é relativo e espera que você esteja executando o comando da raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="d372b-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="d372b-116">pack target</span><span class="sxs-lookup"><span data-stu-id="d372b-116">pack target</span></span>

<span data-ttu-id="d372b-117">Para projetos de .NET Standard usando o formato PackageReference, usar `msbuild -t:pack` desenha entradas do arquivo de projeto para usar na criação de um pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="d372b-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="d372b-118">A tabela abaixo descreve as propriedades do MSBuild que podem ser adicionadas a um arquivo do projeto dentro do primeiro nó `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="d372b-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="d372b-119">Você pode fazer essas edições facilmente no Visual Studio 2017 e posterior clicando com o botão direito do mouse no projeto e selecionando **Editar {project_name}** no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="d372b-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="d372b-120">Para sua conveniência, a tabela é organizada pela propriedade equivalente em um arquivo [`.nuspec` ](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="d372b-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="d372b-121">Observe que as propriedades `Owners` e `Summary` de `.nuspec` não são compatíveis com o MSBuild.</span><span class="sxs-lookup"><span data-stu-id="d372b-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="d372b-122">Valor de atributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="d372b-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="d372b-123">Propriedade do MSBuild</span><span class="sxs-lookup"><span data-stu-id="d372b-123">MSBuild Property</span></span> | <span data-ttu-id="d372b-124">Padrão</span><span class="sxs-lookup"><span data-stu-id="d372b-124">Default</span></span> | <span data-ttu-id="d372b-125">Anotações</span><span class="sxs-lookup"><span data-stu-id="d372b-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="d372b-126">Id</span><span class="sxs-lookup"><span data-stu-id="d372b-126">Id</span></span> | <span data-ttu-id="d372b-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="d372b-127">PackageId</span></span> | <span data-ttu-id="d372b-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="d372b-128">AssemblyName</span></span> | <span data-ttu-id="d372b-129">$(AssemblyName) do MSBuild</span><span class="sxs-lookup"><span data-stu-id="d372b-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="d372b-130">Version</span><span class="sxs-lookup"><span data-stu-id="d372b-130">Version</span></span> | <span data-ttu-id="d372b-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="d372b-131">PackageVersion</span></span> | <span data-ttu-id="d372b-132">Version</span><span class="sxs-lookup"><span data-stu-id="d372b-132">Version</span></span> | <span data-ttu-id="d372b-133">Isso é compatível com semver, por exemplo “1.0.0”, “1.0.0-beta” ou “1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="d372b-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="d372b-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="d372b-134">VersionPrefix</span></span> | <span data-ttu-id="d372b-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="d372b-135">PackageVersionPrefix</span></span> | <span data-ttu-id="d372b-136">empty</span><span class="sxs-lookup"><span data-stu-id="d372b-136">empty</span></span> | <span data-ttu-id="d372b-137">A configuração PackageVersion substitui PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="d372b-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="d372b-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="d372b-138">VersionSuffix</span></span> | <span data-ttu-id="d372b-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="d372b-139">PackageVersionSuffix</span></span> | <span data-ttu-id="d372b-140">empty</span><span class="sxs-lookup"><span data-stu-id="d372b-140">empty</span></span> | <span data-ttu-id="d372b-141">$(VersionSuffix) do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="d372b-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="d372b-142">A configuração PackageVersion substitui PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="d372b-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="d372b-143">Autores</span><span class="sxs-lookup"><span data-stu-id="d372b-143">Authors</span></span> | <span data-ttu-id="d372b-144">Autores</span><span class="sxs-lookup"><span data-stu-id="d372b-144">Authors</span></span> | <span data-ttu-id="d372b-145">Nome do usuário atual</span><span class="sxs-lookup"><span data-stu-id="d372b-145">Username of the current user</span></span> | |
| <span data-ttu-id="d372b-146">Proprietários</span><span class="sxs-lookup"><span data-stu-id="d372b-146">Owners</span></span> | <span data-ttu-id="d372b-147">N/A</span><span class="sxs-lookup"><span data-stu-id="d372b-147">N/A</span></span> | <span data-ttu-id="d372b-148">Não está presente no NuSpec</span><span class="sxs-lookup"><span data-stu-id="d372b-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="d372b-149">Título</span><span class="sxs-lookup"><span data-stu-id="d372b-149">Title</span></span> | <span data-ttu-id="d372b-150">Título</span><span class="sxs-lookup"><span data-stu-id="d372b-150">Title</span></span> | <span data-ttu-id="d372b-151">O PackageId</span><span class="sxs-lookup"><span data-stu-id="d372b-151">The PackageId</span></span>| |
| <span data-ttu-id="d372b-152">Descrição</span><span class="sxs-lookup"><span data-stu-id="d372b-152">Description</span></span> | <span data-ttu-id="d372b-153">Descrição</span><span class="sxs-lookup"><span data-stu-id="d372b-153">Description</span></span> | <span data-ttu-id="d372b-154">“Package Description”</span><span class="sxs-lookup"><span data-stu-id="d372b-154">"Package Description"</span></span> | |
| <span data-ttu-id="d372b-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="d372b-155">Copyright</span></span> | <span data-ttu-id="d372b-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="d372b-156">Copyright</span></span> | <span data-ttu-id="d372b-157">empty</span><span class="sxs-lookup"><span data-stu-id="d372b-157">empty</span></span> | |
| <span data-ttu-id="d372b-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="d372b-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="d372b-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="d372b-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="d372b-160">false</span><span class="sxs-lookup"><span data-stu-id="d372b-160">false</span></span> | |
| <span data-ttu-id="d372b-161">carteira</span><span class="sxs-lookup"><span data-stu-id="d372b-161">license</span></span> | <span data-ttu-id="d372b-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="d372b-162">PackageLicenseExpression</span></span> | <span data-ttu-id="d372b-163">empty</span><span class="sxs-lookup"><span data-stu-id="d372b-163">empty</span></span> | <span data-ttu-id="d372b-164">Corresponde a `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="d372b-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="d372b-165">carteira</span><span class="sxs-lookup"><span data-stu-id="d372b-165">license</span></span> | <span data-ttu-id="d372b-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="d372b-166">PackageLicenseFile</span></span> | <span data-ttu-id="d372b-167">empty</span><span class="sxs-lookup"><span data-stu-id="d372b-167">empty</span></span> | <span data-ttu-id="d372b-168">Corresponde ao `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="d372b-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="d372b-169">Talvez seja necessário empacotar explicitamente o arquivo de licença referenciado.</span><span class="sxs-lookup"><span data-stu-id="d372b-169">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="d372b-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="d372b-170">LicenseUrl</span></span> | <span data-ttu-id="d372b-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="d372b-171">PackageLicenseUrl</span></span> | <span data-ttu-id="d372b-172">empty</span><span class="sxs-lookup"><span data-stu-id="d372b-172">empty</span></span> | <span data-ttu-id="d372b-173">`PackageLicenseUrl` for preterido, use a propriedade PackageLicenseExpression ou PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="d372b-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="d372b-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="d372b-174">ProjectUrl</span></span> | <span data-ttu-id="d372b-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="d372b-175">PackageProjectUrl</span></span> | <span data-ttu-id="d372b-176">empty</span><span class="sxs-lookup"><span data-stu-id="d372b-176">empty</span></span> | |
| <span data-ttu-id="d372b-177">Ícone</span><span class="sxs-lookup"><span data-stu-id="d372b-177">Icon</span></span> | <span data-ttu-id="d372b-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="d372b-178">PackageIcon</span></span> | <span data-ttu-id="d372b-179">empty</span><span class="sxs-lookup"><span data-stu-id="d372b-179">empty</span></span> | <span data-ttu-id="d372b-180">Talvez seja necessário empacotar explicitamente o arquivo de imagem do ícone referenciado.</span><span class="sxs-lookup"><span data-stu-id="d372b-180">You may need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="d372b-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="d372b-181">IconUrl</span></span> | <span data-ttu-id="d372b-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="d372b-182">PackageIconUrl</span></span> | <span data-ttu-id="d372b-183">empty</span><span class="sxs-lookup"><span data-stu-id="d372b-183">empty</span></span> | <span data-ttu-id="d372b-184">`PackageIconUrl` for preterido, use a propriedade PackageIcon</span><span class="sxs-lookup"><span data-stu-id="d372b-184">`PackageIconUrl` is deprecated, use the PackageIcon property</span></span> |
| <span data-ttu-id="d372b-185">Marcas</span><span class="sxs-lookup"><span data-stu-id="d372b-185">Tags</span></span> | <span data-ttu-id="d372b-186">PackageTags</span><span class="sxs-lookup"><span data-stu-id="d372b-186">PackageTags</span></span> | <span data-ttu-id="d372b-187">empty</span><span class="sxs-lookup"><span data-stu-id="d372b-187">empty</span></span> | <span data-ttu-id="d372b-188">Marcas são delimitadas por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="d372b-188">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="d372b-189">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="d372b-189">ReleaseNotes</span></span> | <span data-ttu-id="d372b-190">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="d372b-190">PackageReleaseNotes</span></span> | <span data-ttu-id="d372b-191">empty</span><span class="sxs-lookup"><span data-stu-id="d372b-191">empty</span></span> | |
| <span data-ttu-id="d372b-192">Repositório/URL</span><span class="sxs-lookup"><span data-stu-id="d372b-192">Repository/Url</span></span> | <span data-ttu-id="d372b-193">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="d372b-193">RepositoryUrl</span></span> | <span data-ttu-id="d372b-194">empty</span><span class="sxs-lookup"><span data-stu-id="d372b-194">empty</span></span> | <span data-ttu-id="d372b-195">URL do repositório usada para clonar ou recuperar o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="d372b-195">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="d372b-196">Exemplo: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="d372b-196">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="d372b-197">Repositório/tipo</span><span class="sxs-lookup"><span data-stu-id="d372b-197">Repository/Type</span></span> | <span data-ttu-id="d372b-198">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="d372b-198">RepositoryType</span></span> | <span data-ttu-id="d372b-199">empty</span><span class="sxs-lookup"><span data-stu-id="d372b-199">empty</span></span> | <span data-ttu-id="d372b-200">Tipo de repositório.</span><span class="sxs-lookup"><span data-stu-id="d372b-200">Repository type.</span></span> <span data-ttu-id="d372b-201">Exemplos: *git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="d372b-201">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="d372b-202">Repositório/Branch</span><span class="sxs-lookup"><span data-stu-id="d372b-202">Repository/Branch</span></span> | <span data-ttu-id="d372b-203">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="d372b-203">RepositoryBranch</span></span> | <span data-ttu-id="d372b-204">empty</span><span class="sxs-lookup"><span data-stu-id="d372b-204">empty</span></span> | <span data-ttu-id="d372b-205">Informações opcionais da ramificação do repositório.</span><span class="sxs-lookup"><span data-stu-id="d372b-205">Optional repository branch information.</span></span> <span data-ttu-id="d372b-206">*RepositoryUrl* também deve ser especificado para que essa propriedade seja incluída.</span><span class="sxs-lookup"><span data-stu-id="d372b-206">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="d372b-207">Exemplo: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="d372b-207">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="d372b-208">Repositório/confirmação</span><span class="sxs-lookup"><span data-stu-id="d372b-208">Repository/Commit</span></span> | <span data-ttu-id="d372b-209">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="d372b-209">RepositoryCommit</span></span> | <span data-ttu-id="d372b-210">empty</span><span class="sxs-lookup"><span data-stu-id="d372b-210">empty</span></span> | <span data-ttu-id="d372b-211">Confirmação opcional do repositório ou conjunto de alterações para indicar de qual fonte o pacote foi criado.</span><span class="sxs-lookup"><span data-stu-id="d372b-211">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="d372b-212">*RepositoryUrl* também deve ser especificado para que essa propriedade seja incluída.</span><span class="sxs-lookup"><span data-stu-id="d372b-212">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="d372b-213">Exemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="d372b-213">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="d372b-214">PackageType</span><span class="sxs-lookup"><span data-stu-id="d372b-214">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="d372b-215">Resumo</span><span class="sxs-lookup"><span data-stu-id="d372b-215">Summary</span></span> | <span data-ttu-id="d372b-216">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="d372b-216">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="d372b-217">pack target inputs</span><span class="sxs-lookup"><span data-stu-id="d372b-217">pack target inputs</span></span>

- <span data-ttu-id="d372b-218">IsPackable</span><span class="sxs-lookup"><span data-stu-id="d372b-218">IsPackable</span></span>
- <span data-ttu-id="d372b-219">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="d372b-219">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="d372b-220">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="d372b-220">PackageVersion</span></span>
- <span data-ttu-id="d372b-221">PackageId</span><span class="sxs-lookup"><span data-stu-id="d372b-221">PackageId</span></span>
- <span data-ttu-id="d372b-222">Autores</span><span class="sxs-lookup"><span data-stu-id="d372b-222">Authors</span></span>
- <span data-ttu-id="d372b-223">Descrição</span><span class="sxs-lookup"><span data-stu-id="d372b-223">Description</span></span>
- <span data-ttu-id="d372b-224">Copyright</span><span class="sxs-lookup"><span data-stu-id="d372b-224">Copyright</span></span>
- <span data-ttu-id="d372b-225">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="d372b-225">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="d372b-226">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="d372b-226">DevelopmentDependency</span></span>
- <span data-ttu-id="d372b-227">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="d372b-227">PackageLicenseExpression</span></span>
- <span data-ttu-id="d372b-228">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="d372b-228">PackageLicenseFile</span></span>
- <span data-ttu-id="d372b-229">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="d372b-229">PackageLicenseUrl</span></span>
- <span data-ttu-id="d372b-230">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="d372b-230">PackageProjectUrl</span></span>
- <span data-ttu-id="d372b-231">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="d372b-231">PackageIconUrl</span></span>
- <span data-ttu-id="d372b-232">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="d372b-232">PackageReleaseNotes</span></span>
- <span data-ttu-id="d372b-233">PackageTags</span><span class="sxs-lookup"><span data-stu-id="d372b-233">PackageTags</span></span>
- <span data-ttu-id="d372b-234">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="d372b-234">PackageOutputPath</span></span>
- <span data-ttu-id="d372b-235">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="d372b-235">IncludeSymbols</span></span>
- <span data-ttu-id="d372b-236">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="d372b-236">IncludeSource</span></span>
- <span data-ttu-id="d372b-237">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="d372b-237">PackageTypes</span></span>
- <span data-ttu-id="d372b-238">IsTool</span><span class="sxs-lookup"><span data-stu-id="d372b-238">IsTool</span></span>
- <span data-ttu-id="d372b-239">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="d372b-239">RepositoryUrl</span></span>
- <span data-ttu-id="d372b-240">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="d372b-240">RepositoryType</span></span>
- <span data-ttu-id="d372b-241">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="d372b-241">RepositoryBranch</span></span>
- <span data-ttu-id="d372b-242">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="d372b-242">RepositoryCommit</span></span>
- <span data-ttu-id="d372b-243">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="d372b-243">NoPackageAnalysis</span></span>
- <span data-ttu-id="d372b-244">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="d372b-244">MinClientVersion</span></span>
- <span data-ttu-id="d372b-245">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="d372b-245">IncludeBuildOutput</span></span>
- <span data-ttu-id="d372b-246">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="d372b-246">IncludeContentInPack</span></span>
- <span data-ttu-id="d372b-247">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="d372b-247">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="d372b-248">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="d372b-248">ContentTargetFolders</span></span>
- <span data-ttu-id="d372b-249">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="d372b-249">NuspecFile</span></span>
- <span data-ttu-id="d372b-250">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="d372b-250">NuspecBasePath</span></span>
- <span data-ttu-id="d372b-251">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="d372b-251">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="d372b-252">pack scenarios</span><span class="sxs-lookup"><span data-stu-id="d372b-252">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="d372b-253">Suprimir dependências</span><span class="sxs-lookup"><span data-stu-id="d372b-253">Suppress dependencies</span></span>

<span data-ttu-id="d372b-254">Para suprimir as dependências de pacote do pacote NuGet gerado, defina `SuppressDependenciesWhenPacking` como `true`, o que permitirá ignorar todas as dependências do arquivo nupkg gerado.</span><span class="sxs-lookup"><span data-stu-id="d372b-254">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="d372b-255">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="d372b-255">PackageIconUrl</span></span>

> [!Important]
> <span data-ttu-id="d372b-256">O PackageIconUrl foi preterido com o NuGet 5.3 + & Visual Studio 2019 versão 16.3 +.</span><span class="sxs-lookup"><span data-stu-id="d372b-256">PackageIconUrl is deprecated with NuGet 5.3+ & Visual Studio 2019 version 16.3+.</span></span> <span data-ttu-id="d372b-257">Use [PackageIcon](#packing-an-icon-image-file) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="d372b-257">Use [PackageIcon](#packing-an-icon-image-file) instead.</span></span>

### <a name="packing-an-icon-image-file"></a><span data-ttu-id="d372b-258">Empacotando um arquivo de imagem de ícone</span><span class="sxs-lookup"><span data-stu-id="d372b-258">Packing an icon image file</span></span>

<span data-ttu-id="d372b-259">Ao empacotar um arquivo de imagem de ícone, você precisa usar a propriedade PackageIcon para especificar o caminho do pacote, em relação à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="d372b-259">When packing an icon image file, you need to use PackageIcon property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="d372b-260">Além disso, você precisa certificar-se de que o arquivo está incluído no pacote.</span><span class="sxs-lookup"><span data-stu-id="d372b-260">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="d372b-261">O tamanho do arquivo de imagem é limitado a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="d372b-261">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="d372b-262">Os formatos de arquivo com suporte incluem JPEG e PNG.</span><span class="sxs-lookup"><span data-stu-id="d372b-262">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="d372b-263">Recomendamos uma resolução de imagem de 64 x 64.</span><span class="sxs-lookup"><span data-stu-id="d372b-263">We recommend an image resolution of 64x64.</span></span>

<span data-ttu-id="d372b-264">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d372b-264">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="d372b-265">[Exemplo de ícone de pacote](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="d372b-265">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="d372b-266">Para obter o equivalente do nuspec, dê uma olhada na [referência do nuspec para o ícone](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="d372b-266">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="d372b-267">Assemblies de saída</span><span class="sxs-lookup"><span data-stu-id="d372b-267">Output assemblies</span></span>

<span data-ttu-id="d372b-268">O `nuget pack` copia arquivos de saída com extensões `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="d372b-268">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="d372b-269">Os arquivos de saída que são copiados dependem do que o MSBuild fornece do destino `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="d372b-269">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="d372b-270">Há duas propriedades de MSBuild que você pode usar em seu arquivo de projeto ou a linha de comando para controlar onde ficam os assemblies de saída:</span><span class="sxs-lookup"><span data-stu-id="d372b-270">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="d372b-271">`IncludeBuildOutput`: um valor booliano que determina se os assemblies de saída de build devem ser incluídos no pacote.</span><span class="sxs-lookup"><span data-stu-id="d372b-271">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="d372b-272">`BuildOutputTargetFolder`: especifica a pasta na qual os assemblies de saída devem ser colocados.</span><span class="sxs-lookup"><span data-stu-id="d372b-272">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="d372b-273">Os assemblies de saída (e outros arquivos de saída) são copiados para suas respectivas pastas de estrutura.</span><span class="sxs-lookup"><span data-stu-id="d372b-273">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="d372b-274">Referências de pacote</span><span class="sxs-lookup"><span data-stu-id="d372b-274">Package references</span></span>

<span data-ttu-id="d372b-275">Consulte [Referências de pacote em arquivos de projeto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="d372b-275">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="d372b-276">Referências de projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="d372b-276">Project to project references</span></span>

<span data-ttu-id="d372b-277">As referências projeto a projeto são consideradas como referências de pacote do nuget por padrão, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d372b-277">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="d372b-278">Você também pode adicionar os seguintes metadados à referência de projeto:</span><span class="sxs-lookup"><span data-stu-id="d372b-278">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="d372b-279">Incluindo o conteúdo em um pacote</span><span class="sxs-lookup"><span data-stu-id="d372b-279">Including content in a package</span></span>

<span data-ttu-id="d372b-280">Para incluir o conteúdo, adicione metadados extras ao item `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="d372b-280">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="d372b-281">Por padrão, tudo que pertencer ao tipo “Conteúdo” é incluído no pacote, a menos que seja substituído por entradas como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="d372b-281">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="d372b-282">Por padrão, tudo é adicionado à raiz da pasta `content` e `contentFiles\any\<target_framework>` dentro de um pacote e preserva a estrutura e pasta relativa, a menos que você especifique um caminho de pacote:</span><span class="sxs-lookup"><span data-stu-id="d372b-282">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="d372b-283">Se você quiser copiar todo o conteúdo somente para determinadas pastas raiz (em vez de para `content` e `contentFiles`), será possível usar a propriedade `ContentTargetFolders` do MSBuild, que assume como padrão "content;contentFiles", mas pode ser definida como qualquer outro nome de pasta.</span><span class="sxs-lookup"><span data-stu-id="d372b-283">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="d372b-284">Observe que só especificar “contentFiles” em `ContentTargetFolders` coloca os arquivos em `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` com base em `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="d372b-284">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="d372b-285">`PackagePath` pode ser um conjunto de caminhos de destino separados por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="d372b-285">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="d372b-286">Especificar um caminho de pacote vazio adicionaria o arquivo à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="d372b-286">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="d372b-287">Por exemplo, o seguinte adiciona `libuv.txt` a `content\myfiles`, `content\samples` e a raiz do pacote:</span><span class="sxs-lookup"><span data-stu-id="d372b-287">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="d372b-288">Há também uma propriedade de MSBuild `$(IncludeContentInPack)`, que assume o padrão `true`.</span><span class="sxs-lookup"><span data-stu-id="d372b-288">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="d372b-289">Se isso for definido como `false` em qualquer projeto, o conteúdo desse projeto não está incluso no pacote do nuget.</span><span class="sxs-lookup"><span data-stu-id="d372b-289">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="d372b-290">Outros metadados específicos do pacote que pode ser definido em qualquer um dos itens acima ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, que define os valores ```CopyToOutput``` e ```Flatten``` na entrada ```contentFiles``` no nuspec de saída.</span><span class="sxs-lookup"><span data-stu-id="d372b-290">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="d372b-291">Além de itens de Conteúdo, os metadados `<Pack>` e `<PackagePath>` também podem ser definidos em arquivos com uma ação de Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.</span><span class="sxs-lookup"><span data-stu-id="d372b-291">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="d372b-292">Para o pacote acrescentar o nome de arquivo ao caminho do pacote ao usar padrões glob, seu caminho de pacote deve terminar com o caractere separador de pasta, caso contrário, o caminho do pacote será tratado como o caminho completo, incluindo o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="d372b-292">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="d372b-293">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="d372b-293">IncludeSymbols</span></span>

<span data-ttu-id="d372b-294">Ao usar o `MSBuild -t:pack -p:IncludeSymbols=true`, os arquivos `.pdb` correspondentes são copiados junto com outros arquivos de saída (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="d372b-294">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="d372b-295">Observe que a configuração `IncludeSymbols=true` cria um pacote regular *e* um pacote de símbolos.</span><span class="sxs-lookup"><span data-stu-id="d372b-295">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="d372b-296">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="d372b-296">IncludeSource</span></span>

<span data-ttu-id="d372b-297">Isso é o mesmo que `IncludeSymbols`, exceto que também copia os arquivos de origem com arquivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="d372b-297">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="d372b-298">Todos os arquivos do tipo `Compile` são copiadas para `src\<ProjectName>\`, preservando a estrutura de pastas do caminho relativo no pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="d372b-298">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="d372b-299">O mesmo também ocorre para arquivos de origem de qualquer `ProjectReference` que tem `TreatAsPackageReference` definido como `false`.</span><span class="sxs-lookup"><span data-stu-id="d372b-299">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="d372b-300">Se um arquivo do tipo Compilação estiver fora da pasta de projeto, ele será adicionado apenas a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="d372b-300">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="d372b-301">Empacotando uma expressão de licença ou um arquivo de licença</span><span class="sxs-lookup"><span data-stu-id="d372b-301">Packing a license expression or a license file</span></span>

<span data-ttu-id="d372b-302">Ao usar uma expressão de licença, a propriedade PackageLicenseExpression deve ser usada.</span><span class="sxs-lookup"><span data-stu-id="d372b-302">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="d372b-303">[Exemplo de expressão de licença](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="d372b-303">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="d372b-304">[Saiba mais sobre as expressões de licença e as licenças que são aceitas pelo NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="d372b-304">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="d372b-305">Ao empacotar um arquivo de licença, você precisa usar a propriedade PackageLicenseFile para especificar o caminho do pacote, em relação à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="d372b-305">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="d372b-306">Além disso, você precisa certificar-se de que o arquivo está incluído no pacote.</span><span class="sxs-lookup"><span data-stu-id="d372b-306">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="d372b-307">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d372b-307">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="d372b-308">[Exemplo de arquivo de licença](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="d372b-308">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="d372b-309">IsTool</span><span class="sxs-lookup"><span data-stu-id="d372b-309">IsTool</span></span>

<span data-ttu-id="d372b-310">Ao usar `MSBuild -t:pack -p:IsTool=true`, todos os arquivos de saída, conforme especificado no cenário [Assemblies de saída](#output-assemblies), são copiados para a pasta `tools` em vez da pasta `lib`.</span><span class="sxs-lookup"><span data-stu-id="d372b-310">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="d372b-311">Observe que isso é diferente de um `DotNetCliTool` que é especificado pela configuração do `PackageType` no arquivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="d372b-311">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="d372b-312">Empacotamento usando um .nuspec</span><span class="sxs-lookup"><span data-stu-id="d372b-312">Packing using a .nuspec</span></span>

<span data-ttu-id="d372b-313">Embora seja recomendável [incluir todas as propriedades](../reference/msbuild-targets.md#pack-target) que geralmente estão no arquivo `.nuspec` no arquivo de projeto, você pode optar por usar um arquivo `.nuspec` para empacotar o projeto.</span><span class="sxs-lookup"><span data-stu-id="d372b-313">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="d372b-314">Para um projeto de estilo não-SDK que usa `PackageReference`, você deve importar `NuGet.Build.Tasks.Pack.targets` para que a tarefa de pacote possa ser executada.</span><span class="sxs-lookup"><span data-stu-id="d372b-314">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="d372b-315">Você ainda precisa restaurar o projeto antes de poder empacotar um arquivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="d372b-315">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="d372b-316">(Um projeto no estilo SDK inclui os destinos do pacote por padrão.)</span><span class="sxs-lookup"><span data-stu-id="d372b-316">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="d372b-317">A estrutura de destino do arquivo de projeto é irrelevante e não é usada ao empacotar um nuspec.</span><span class="sxs-lookup"><span data-stu-id="d372b-317">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="d372b-318">As três propriedades MSBuild a seguir são relevantes para empacotamento usando um `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="d372b-318">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="d372b-319">`NuspecFile`: caminho relativo ou absoluto para o arquivo `.nuspec` que está sendo usado para o empacotamento.</span><span class="sxs-lookup"><span data-stu-id="d372b-319">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="d372b-320">`NuspecProperties`: uma lista separada por ponto e vírgula de pares chave/valor.</span><span class="sxs-lookup"><span data-stu-id="d372b-320">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="d372b-321">Devido à maneira como a análise de linha de comando do MSBuild funciona, várias propriedades precisam ser especificadas da seguinte maneira: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="d372b-321">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="d372b-322">`NuspecBasePath`: o caminho base para o arquivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="d372b-322">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="d372b-323">Se estiver usando `dotnet.exe` para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d372b-323">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="d372b-324">Se estiver usando o MSBuild para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d372b-324">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="d372b-325">Observe que empacotar um nuspec usando dotNet. exe ou MSBuild também leva a criar o projeto por padrão.</span><span class="sxs-lookup"><span data-stu-id="d372b-325">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="d372b-326">Isso pode ser evitado passando a propriedade ```--no-build``` para dotnet. exe, que é o equivalente à configuração ```<NoBuild>true</NoBuild> ``` no arquivo de projeto, juntamente com a configuração ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="d372b-326">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="d372b-327">Um exemplo de um arquivo *. csproj* para empacotar um arquivo nuspec é:</span><span class="sxs-lookup"><span data-stu-id="d372b-327">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="d372b-328">Pontos de extensão avançados para criar pacote personalizado</span><span class="sxs-lookup"><span data-stu-id="d372b-328">Advanced extension points to create customized package</span></span>

<span data-ttu-id="d372b-329">O destino `pack` fornece dois pontos de extensão que são executados na compilação interna, específica da estrutura de destino.</span><span class="sxs-lookup"><span data-stu-id="d372b-329">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="d372b-330">Os pontos de extensão dão suporte à inclusão de conteúdo específico da estrutura de destino e assemblies em um pacote:</span><span class="sxs-lookup"><span data-stu-id="d372b-330">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="d372b-331">destino `TargetsForTfmSpecificBuildOutput`: Use para arquivos dentro da pasta `lib` ou de uma pasta especificada usando `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="d372b-331">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="d372b-332">destino `TargetsForTfmSpecificContentInPackage`: Use para arquivos fora do `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="d372b-332">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="d372b-333">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="d372b-333">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="d372b-334">Escreva um destino personalizado e especifique-o como o valor da propriedade `$(TargetsForTfmSpecificBuildOutput)`.</span><span class="sxs-lookup"><span data-stu-id="d372b-334">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="d372b-335">Para todos os arquivos que precisam entrar no `BuildOutputTargetFolder` (lib por padrão), o destino deve gravar esses arquivos no rowgroup `BuildOutputInPackage` e definir os dois valores de metadados a seguir:</span><span class="sxs-lookup"><span data-stu-id="d372b-335">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="d372b-336">`FinalOutputPath`: o caminho absoluto do arquivo; Se não for fornecido, a identidade será usada para avaliar o caminho de origem.</span><span class="sxs-lookup"><span data-stu-id="d372b-336">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="d372b-337">`TargetPath`: (opcional) definido quando o arquivo precisa entrar em uma subpasta dentro de `lib\<TargetFramework>`, como assemblies satélite que estão em suas respectivas pastas de cultura.</span><span class="sxs-lookup"><span data-stu-id="d372b-337">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="d372b-338">O padrão é o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="d372b-338">Defaults to the name of the file.</span></span>

<span data-ttu-id="d372b-339">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="d372b-339">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="d372b-340">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="d372b-340">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="d372b-341">Escreva um destino personalizado e especifique-o como o valor da propriedade `$(TargetsForTfmSpecificContentInPackage)`.</span><span class="sxs-lookup"><span data-stu-id="d372b-341">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="d372b-342">Para todos os arquivos a serem incluídos no pacote, o destino deve gravar esses arquivos no grupo de itens `TfmSpecificPackageFile` e definir os seguintes metadados opcionais:</span><span class="sxs-lookup"><span data-stu-id="d372b-342">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="d372b-343">`PackagePath`: caminho onde o arquivo deve ser apresentado no pacote.</span><span class="sxs-lookup"><span data-stu-id="d372b-343">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="d372b-344">O NuGet emitirá um aviso se mais de um arquivo for adicionado ao mesmo caminho de pacote.</span><span class="sxs-lookup"><span data-stu-id="d372b-344">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="d372b-345">`BuildAction`: a ação de compilação a ser atribuída ao arquivo, necessária somente se o caminho do pacote estiver na pasta `contentFiles`.</span><span class="sxs-lookup"><span data-stu-id="d372b-345">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="d372b-346">O padrão é "None".</span><span class="sxs-lookup"><span data-stu-id="d372b-346">Defaults to "None".</span></span>

<span data-ttu-id="d372b-347">Um exemplo:</span><span class="sxs-lookup"><span data-stu-id="d372b-347">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="d372b-348">restore target</span><span class="sxs-lookup"><span data-stu-id="d372b-348">restore target</span></span>

<span data-ttu-id="d372b-349">`MSBuild -t:restore` (que `nuget restore` e `dotnet restore` usam com projetos do .NET Core), restaura pacotes referenciados no arquivo de projeto da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d372b-349">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="d372b-350">Ler todas as referências projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="d372b-350">Read all project to project references</span></span>
1. <span data-ttu-id="d372b-351">Ler as propriedades do projeto para localizar a pasta intermediária e as estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="d372b-351">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="d372b-352">Transmitir dados do MSBuild para NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="d372b-352">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="d372b-353">Executar restauração</span><span class="sxs-lookup"><span data-stu-id="d372b-353">Run restore</span></span>
1. <span data-ttu-id="d372b-354">Baixar os pacotes</span><span class="sxs-lookup"><span data-stu-id="d372b-354">Download packages</span></span>
1. <span data-ttu-id="d372b-355">Gravar arquivo de ativos, destinos e objetos</span><span class="sxs-lookup"><span data-stu-id="d372b-355">Write assets file, targets, and props</span></span>

<span data-ttu-id="d372b-356">O destino `restore` funciona **apenas** para projetos que usam o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="d372b-356">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="d372b-357">Ele não **funciona para** projetos que usam o formato `packages.config`; em vez disso, use a [restauração do NuGet](../reference/cli-reference/cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="d372b-357">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="d372b-358">Restaurar propriedades</span><span class="sxs-lookup"><span data-stu-id="d372b-358">Restore properties</span></span>

<span data-ttu-id="d372b-359">Configurações de restauração adicionais podem vir de propriedades MSBuild no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="d372b-359">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="d372b-360">Os valores também podem ser definidos na linha de comando usando a opção `-p:` (consulte os Exemplos abaixo).</span><span class="sxs-lookup"><span data-stu-id="d372b-360">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="d372b-361">propriedade</span><span class="sxs-lookup"><span data-stu-id="d372b-361">Property</span></span> | <span data-ttu-id="d372b-362">Descrição</span><span class="sxs-lookup"><span data-stu-id="d372b-362">Description</span></span> |
|--------|--------|
| <span data-ttu-id="d372b-363">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="d372b-363">RestoreSources</span></span> | <span data-ttu-id="d372b-364">Uma lista delimitada por ponto e vírgula de origens de pacote.</span><span class="sxs-lookup"><span data-stu-id="d372b-364">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="d372b-365">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="d372b-365">RestorePackagesPath</span></span> | <span data-ttu-id="d372b-366">Caminho da pasta dos pacotes do usuário.</span><span class="sxs-lookup"><span data-stu-id="d372b-366">User packages folder path.</span></span> |
| <span data-ttu-id="d372b-367">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="d372b-367">RestoreDisableParallel</span></span> | <span data-ttu-id="d372b-368">Limite os downloads para um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="d372b-368">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="d372b-369">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="d372b-369">RestoreConfigFile</span></span> | <span data-ttu-id="d372b-370">Caminho para um arquivo `Nuget.Config` a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="d372b-370">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="d372b-371">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="d372b-371">RestoreNoCache</span></span> | <span data-ttu-id="d372b-372">Se for true, evita o uso de pacotes armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="d372b-372">If true, avoids using cached packages.</span></span> <span data-ttu-id="d372b-373">Consulte [Gerenciando os pacotes globais e as pastas de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="d372b-373">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="d372b-374">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="d372b-374">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="d372b-375">Se verdadeiro, ignora origens de pacote com falha ou ausentes.</span><span class="sxs-lookup"><span data-stu-id="d372b-375">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="d372b-376">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="d372b-376">RestoreFallbackFolders</span></span> | <span data-ttu-id="d372b-377">Pastas de fallback, usadas da mesma maneira que a pasta pacotes de usuário é usada.</span><span class="sxs-lookup"><span data-stu-id="d372b-377">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="d372b-378">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="d372b-378">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="d372b-379">Fontes adicionais a serem usadas durante a restauração.</span><span class="sxs-lookup"><span data-stu-id="d372b-379">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="d372b-380">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="d372b-380">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="d372b-381">Pastas de fallback adicionais a serem usadas durante a restauração.</span><span class="sxs-lookup"><span data-stu-id="d372b-381">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="d372b-382">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="d372b-382">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="d372b-383">Exclui as pastas de fallback especificadas no `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="d372b-383">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="d372b-384">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="d372b-384">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="d372b-385">Caminho para `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="d372b-385">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="d372b-386">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="d372b-386">RestoreGraphProjectInput</span></span> | <span data-ttu-id="d372b-387">Lista separada por ponto e vírgula de projetos a serem restaurados, que devem conter caminhos absolutos.</span><span class="sxs-lookup"><span data-stu-id="d372b-387">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="d372b-388">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="d372b-388">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="d372b-389">Quando os projetos são coletados via MSBuild, ele determina se eles são coletados usando a otimização `SkipNonexistentTargets`.</span><span class="sxs-lookup"><span data-stu-id="d372b-389">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="d372b-390">Quando não definido, o padrão é `true`.</span><span class="sxs-lookup"><span data-stu-id="d372b-390">When not set, defaults to `true`.</span></span> <span data-ttu-id="d372b-391">A conseqüência é um comportamento com falha rápida quando os destinos de um projeto não podem ser importados.</span><span class="sxs-lookup"><span data-stu-id="d372b-391">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="d372b-392">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="d372b-392">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="d372b-393">Pasta de saída, padronizando para `BaseIntermediateOutputPath` e a pasta `obj`.</span><span class="sxs-lookup"><span data-stu-id="d372b-393">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="d372b-394">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="d372b-394">RestoreForce</span></span> | <span data-ttu-id="d372b-395">Em projetos baseados em PackageReference, o forçará a resolução de todas as dependências, mesmo que a última restauração tenha sido bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="d372b-395">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="d372b-396">A especificação desse sinalizador é semelhante à exclusão do arquivo `project.assets.json`.</span><span class="sxs-lookup"><span data-stu-id="d372b-396">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="d372b-397">Isso não ignora o cache http.</span><span class="sxs-lookup"><span data-stu-id="d372b-397">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="d372b-398">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="d372b-398">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="d372b-399">Opta pelo uso de um arquivo de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="d372b-399">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="d372b-400">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="d372b-400">RestoreLockedMode</span></span> | <span data-ttu-id="d372b-401">Execute RESTORE no modo bloqueado.</span><span class="sxs-lookup"><span data-stu-id="d372b-401">Run restore in locked mode.</span></span> <span data-ttu-id="d372b-402">Isso significa que a restauração não reavaliará as dependências.</span><span class="sxs-lookup"><span data-stu-id="d372b-402">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="d372b-403">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="d372b-403">NuGetLockFilePath</span></span> | <span data-ttu-id="d372b-404">Um local personalizado para o arquivo de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="d372b-404">A custom location for the lock file.</span></span> <span data-ttu-id="d372b-405">O local padrão é ao lado do projeto e é denominado `packages.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="d372b-405">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="d372b-406">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="d372b-406">RestoreForceEvaluate</span></span> | <span data-ttu-id="d372b-407">Força a restauração a recalcular as dependências e atualizar o arquivo de bloqueio sem nenhum aviso.</span><span class="sxs-lookup"><span data-stu-id="d372b-407">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> | 

#### <a name="examples"></a><span data-ttu-id="d372b-408">Exemplos</span><span class="sxs-lookup"><span data-stu-id="d372b-408">Examples</span></span>

<span data-ttu-id="d372b-409">Linha de comando:</span><span class="sxs-lookup"><span data-stu-id="d372b-409">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="d372b-410">Arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="d372b-410">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="d372b-411">Restaurar saídas</span><span class="sxs-lookup"><span data-stu-id="d372b-411">Restore outputs</span></span>

<span data-ttu-id="d372b-412">A restauração cria os seguintes arquivos na pasta `obj` de build:</span><span class="sxs-lookup"><span data-stu-id="d372b-412">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="d372b-413">Arquivo</span><span class="sxs-lookup"><span data-stu-id="d372b-413">File</span></span> | <span data-ttu-id="d372b-414">Descrição</span><span class="sxs-lookup"><span data-stu-id="d372b-414">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="d372b-415">Contém o grafo de dependência de todas as referências de pacote.</span><span class="sxs-lookup"><span data-stu-id="d372b-415">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="d372b-416">Referências a objetos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="d372b-416">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="d372b-417">Referências a destinos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="d372b-417">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="d372b-418">Restaurando e compilando com um comando do MSBuild</span><span class="sxs-lookup"><span data-stu-id="d372b-418">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="d372b-419">Devido ao fato de que o NuGet pode restaurar pacotes que desativam destinos e props do MSBuild, as avaliações de restauração e compilação são executadas com propriedades globais diferentes.</span><span class="sxs-lookup"><span data-stu-id="d372b-419">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="d372b-420">Isso significa que o seguinte terá um comportamento imprevisível e geralmente incorreto.</span><span class="sxs-lookup"><span data-stu-id="d372b-420">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="d372b-421">Em vez disso, a abordagem recomendada é:</span><span class="sxs-lookup"><span data-stu-id="d372b-421">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="d372b-422">A mesma lógica se aplica a outros destinos semelhantes a `build`.</span><span class="sxs-lookup"><span data-stu-id="d372b-422">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="d372b-423">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="d372b-423">PackageTargetFallback</span></span>

<span data-ttu-id="d372b-424">O elemento `PackageTargetFallback` permite especificar um conjunto de destinos compatíveis a serem usados ao restaurar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="d372b-424">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="d372b-425">Ele foi desenvolvido para permitir que os pacotes que usam o dotnet [TxM](../reference/target-frameworks.md) funcionem com pacotes compatíveis que não declaram um dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="d372b-425">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="d372b-426">Ou seja, se o projeto usar o dotnet TxM, todos os pacotes dos quais ele depende também deverão ter um dotnet TxM, a menos que você adicione o `<PackageTargetFallback>` ao projeto para permitir que plataformas não dotnet sejam compatíveis com o dotnet.</span><span class="sxs-lookup"><span data-stu-id="d372b-426">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="d372b-427">Por exemplo, se o projeto está usando o `netstandard1.6` TxM e um pacote dependente contém apenas `lib/net45/a.dll` e `lib/portable-net45+win81/a.dll`, o projeto não será compilado.</span><span class="sxs-lookup"><span data-stu-id="d372b-427">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="d372b-428">Se a DLL que você deseja colocar é esta última, é possível adicionar um `PackageTargetFallback` como mostrado a seguir para dizer que a DLL `portable-net45+win81` é compatível:</span><span class="sxs-lookup"><span data-stu-id="d372b-428">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="d372b-429">Para declarar um fallback para todos os destinos em seu projeto, deixe o atributo `Condition` de fora.</span><span class="sxs-lookup"><span data-stu-id="d372b-429">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="d372b-430">Você também pode estender qualquer `PackageTargetFallback` existente incluindo `$(PackageTargetFallback)` conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="d372b-430">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="d372b-431">Substituindo uma biblioteca de um grafo de restauração</span><span class="sxs-lookup"><span data-stu-id="d372b-431">Replacing one library from a restore graph</span></span>

<span data-ttu-id="d372b-432">Se uma restauração está trazendo o assembly errado, é possível excluir a escolha padrão do pacote e substituí-lo por outro de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="d372b-432">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="d372b-433">Primeiro com um `PackageReference` de nível superior, exclua todos os ativos:</span><span class="sxs-lookup"><span data-stu-id="d372b-433">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="d372b-434">Em seguida, adicione sua própria referência à cópia local apropriada da DLL:</span><span class="sxs-lookup"><span data-stu-id="d372b-434">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
