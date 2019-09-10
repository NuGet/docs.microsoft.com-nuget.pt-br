---
title: Empacotamento e restauração do NuGet como destinos do MSBuild
description: O pack e restore do NuGet podem funcionar diretamente como destinos do MSBuild com o NuGet 4.0 e superior.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 16b8ff532b87a3e3f96029e77dd166eb39294c0b
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815349"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="0736b-103">Empacotamento e restauração do NuGet como destinos do MSBuild</span><span class="sxs-lookup"><span data-stu-id="0736b-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="0736b-104">*NuGet 4.0 ou superior*</span><span class="sxs-lookup"><span data-stu-id="0736b-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="0736b-105">Com o formato [PackageReference](../consume-packages/package-references-in-project-files.md) , o NuGet 4.0 + pode armazenar todos os metadados do manifesto diretamente dentro de um arquivo de projeto `.nuspec` em vez de usar um arquivo separado.</span><span class="sxs-lookup"><span data-stu-id="0736b-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="0736b-106">Com o MSBuild 15.1 ou superior, o NuGet também é um cidadão de primeira classe do MSBuild com os destinos `pack` e `restore`, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="0736b-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="0736b-107">Esses destinos permitem que você trabalhe com o NuGet como faria com qualquer outra tarefa ou destino do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="0736b-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="0736b-108">Para obter instruções sobre como criar um pacote NuGet usando o MSBuild, consulte [criar um pacote NuGet usando o MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="0736b-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="0736b-109">(Para NuGet 3.x e anteriores, use os comandos [pack](../reference/cli-reference/cli-ref-pack.md) e [restore](../reference/cli-reference/cli-ref-restore.md) na CLI do NuGet.)</span><span class="sxs-lookup"><span data-stu-id="0736b-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="0736b-110">Ordem de build de destino</span><span class="sxs-lookup"><span data-stu-id="0736b-110">Target build order</span></span>

<span data-ttu-id="0736b-111">Como `pack` e `restore` são os destinos do MSBuild, você pode acessá-los para melhorar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0736b-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="0736b-112">Por exemplo, digamos que você deseja copiar o pacote para um compartilhamento de rede após empacotá-lo.</span><span class="sxs-lookup"><span data-stu-id="0736b-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="0736b-113">Você pode fazer isso adicionando o seguinte ao seu arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="0736b-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="0736b-114">Da mesma forma, você pode gravar uma tarefa do MSBuild, escrever seu próprio destino e consumir propriedades do NuGet na tarefa de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="0736b-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="0736b-115">`$(OutputPath)`é relativo e espera que você esteja executando o comando da raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="0736b-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="0736b-116">pack target</span><span class="sxs-lookup"><span data-stu-id="0736b-116">pack target</span></span>

<span data-ttu-id="0736b-117">Para projetos de .net Standard usando o formato PackageReference, `msbuild -t:pack` o uso de desenha entradas do arquivo de projeto para usar na criação de um pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="0736b-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="0736b-118">A tabela abaixo descreve as propriedades do MSBuild que podem ser adicionadas a um arquivo do projeto dentro do primeiro nó `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="0736b-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="0736b-119">Você pode fazer essas edições facilmente no Visual Studio 2017 e posterior clicando com o botão direito do mouse no projeto e selecionando **Editar {project_name}** no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="0736b-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="0736b-120">Para sua conveniência, a tabela é organizada pela propriedade equivalente em um arquivo [`.nuspec` ](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="0736b-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="0736b-121">Observe que as propriedades `Owners` e `Summary` de `.nuspec` não são compatíveis com o MSBuild.</span><span class="sxs-lookup"><span data-stu-id="0736b-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="0736b-122">Valor de atributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="0736b-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="0736b-123">Propriedade do MSBuild</span><span class="sxs-lookup"><span data-stu-id="0736b-123">MSBuild Property</span></span> | <span data-ttu-id="0736b-124">Padrão</span><span class="sxs-lookup"><span data-stu-id="0736b-124">Default</span></span> | <span data-ttu-id="0736b-125">Observações</span><span class="sxs-lookup"><span data-stu-id="0736b-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="0736b-126">Id</span><span class="sxs-lookup"><span data-stu-id="0736b-126">Id</span></span> | <span data-ttu-id="0736b-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="0736b-127">PackageId</span></span> | <span data-ttu-id="0736b-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="0736b-128">AssemblyName</span></span> | <span data-ttu-id="0736b-129">$(AssemblyName) do MSBuild</span><span class="sxs-lookup"><span data-stu-id="0736b-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="0736b-130">Version</span><span class="sxs-lookup"><span data-stu-id="0736b-130">Version</span></span> | <span data-ttu-id="0736b-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="0736b-131">PackageVersion</span></span> | <span data-ttu-id="0736b-132">Version</span><span class="sxs-lookup"><span data-stu-id="0736b-132">Version</span></span> | <span data-ttu-id="0736b-133">Isso é compatível com semver, por exemplo “1.0.0”, “1.0.0-beta” ou “1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="0736b-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="0736b-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="0736b-134">VersionPrefix</span></span> | <span data-ttu-id="0736b-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="0736b-135">PackageVersionPrefix</span></span> | <span data-ttu-id="0736b-136">empty</span><span class="sxs-lookup"><span data-stu-id="0736b-136">empty</span></span> | <span data-ttu-id="0736b-137">A configuração PackageVersion substitui PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="0736b-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="0736b-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="0736b-138">VersionSuffix</span></span> | <span data-ttu-id="0736b-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="0736b-139">PackageVersionSuffix</span></span> | <span data-ttu-id="0736b-140">empty</span><span class="sxs-lookup"><span data-stu-id="0736b-140">empty</span></span> | <span data-ttu-id="0736b-141">$(VersionSuffix) do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="0736b-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="0736b-142">A configuração PackageVersion substitui PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="0736b-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="0736b-143">Autores</span><span class="sxs-lookup"><span data-stu-id="0736b-143">Authors</span></span> | <span data-ttu-id="0736b-144">Autores</span><span class="sxs-lookup"><span data-stu-id="0736b-144">Authors</span></span> | <span data-ttu-id="0736b-145">Nome do usuário atual</span><span class="sxs-lookup"><span data-stu-id="0736b-145">Username of the current user</span></span> | |
| <span data-ttu-id="0736b-146">Proprietários</span><span class="sxs-lookup"><span data-stu-id="0736b-146">Owners</span></span> | <span data-ttu-id="0736b-147">N/D</span><span class="sxs-lookup"><span data-stu-id="0736b-147">N/A</span></span> | <span data-ttu-id="0736b-148">Não está presente no NuSpec</span><span class="sxs-lookup"><span data-stu-id="0736b-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="0736b-149">Título</span><span class="sxs-lookup"><span data-stu-id="0736b-149">Title</span></span> | <span data-ttu-id="0736b-150">Título</span><span class="sxs-lookup"><span data-stu-id="0736b-150">Title</span></span> | <span data-ttu-id="0736b-151">O PackageId</span><span class="sxs-lookup"><span data-stu-id="0736b-151">The PackageId</span></span>| |
| <span data-ttu-id="0736b-152">Descrição</span><span class="sxs-lookup"><span data-stu-id="0736b-152">Description</span></span> | <span data-ttu-id="0736b-153">Descrição</span><span class="sxs-lookup"><span data-stu-id="0736b-153">Description</span></span> | <span data-ttu-id="0736b-154">“Package Description”</span><span class="sxs-lookup"><span data-stu-id="0736b-154">"Package Description"</span></span> | |
| <span data-ttu-id="0736b-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="0736b-155">Copyright</span></span> | <span data-ttu-id="0736b-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="0736b-156">Copyright</span></span> | <span data-ttu-id="0736b-157">empty</span><span class="sxs-lookup"><span data-stu-id="0736b-157">empty</span></span> | |
| <span data-ttu-id="0736b-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="0736b-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="0736b-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="0736b-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="0736b-160">false</span><span class="sxs-lookup"><span data-stu-id="0736b-160">false</span></span> | |
| <span data-ttu-id="0736b-161">carteira</span><span class="sxs-lookup"><span data-stu-id="0736b-161">license</span></span> | <span data-ttu-id="0736b-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="0736b-162">PackageLicenseExpression</span></span> | <span data-ttu-id="0736b-163">empty</span><span class="sxs-lookup"><span data-stu-id="0736b-163">empty</span></span> | <span data-ttu-id="0736b-164">Corresponde a`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="0736b-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="0736b-165">carteira</span><span class="sxs-lookup"><span data-stu-id="0736b-165">license</span></span> | <span data-ttu-id="0736b-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="0736b-166">PackageLicenseFile</span></span> | <span data-ttu-id="0736b-167">empty</span><span class="sxs-lookup"><span data-stu-id="0736b-167">empty</span></span> | <span data-ttu-id="0736b-168">Corresponde ao `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="0736b-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="0736b-169">Talvez seja necessário empacotar explicitamente o arquivo de licença referenciado.</span><span class="sxs-lookup"><span data-stu-id="0736b-169">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="0736b-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="0736b-170">LicenseUrl</span></span> | <span data-ttu-id="0736b-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="0736b-171">PackageLicenseUrl</span></span> | <span data-ttu-id="0736b-172">empty</span><span class="sxs-lookup"><span data-stu-id="0736b-172">empty</span></span> | <span data-ttu-id="0736b-173">`PackageLicenseUrl`é preterido, use a propriedade PackageLicenseExpression ou PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="0736b-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="0736b-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="0736b-174">ProjectUrl</span></span> | <span data-ttu-id="0736b-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="0736b-175">PackageProjectUrl</span></span> | <span data-ttu-id="0736b-176">empty</span><span class="sxs-lookup"><span data-stu-id="0736b-176">empty</span></span> | |
| <span data-ttu-id="0736b-177">Ícone</span><span class="sxs-lookup"><span data-stu-id="0736b-177">Icon</span></span> | <span data-ttu-id="0736b-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="0736b-178">PackageIcon</span></span> | <span data-ttu-id="0736b-179">empty</span><span class="sxs-lookup"><span data-stu-id="0736b-179">empty</span></span> | <span data-ttu-id="0736b-180">Talvez seja necessário empacotar explicitamente o arquivo de imagem do ícone referenciado.</span><span class="sxs-lookup"><span data-stu-id="0736b-180">You may need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="0736b-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="0736b-181">IconUrl</span></span> | <span data-ttu-id="0736b-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="0736b-182">PackageIconUrl</span></span> | <span data-ttu-id="0736b-183">empty</span><span class="sxs-lookup"><span data-stu-id="0736b-183">empty</span></span> | <span data-ttu-id="0736b-184">`PackageIconUrl`é preterido, use a propriedade PackageIcon</span><span class="sxs-lookup"><span data-stu-id="0736b-184">`PackageIconUrl` is deprecated, use the PackageIcon property</span></span> |
| <span data-ttu-id="0736b-185">Marcas</span><span class="sxs-lookup"><span data-stu-id="0736b-185">Tags</span></span> | <span data-ttu-id="0736b-186">PackageTags</span><span class="sxs-lookup"><span data-stu-id="0736b-186">PackageTags</span></span> | <span data-ttu-id="0736b-187">empty</span><span class="sxs-lookup"><span data-stu-id="0736b-187">empty</span></span> | <span data-ttu-id="0736b-188">Marcas são delimitadas por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="0736b-188">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="0736b-189">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="0736b-189">ReleaseNotes</span></span> | <span data-ttu-id="0736b-190">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="0736b-190">PackageReleaseNotes</span></span> | <span data-ttu-id="0736b-191">empty</span><span class="sxs-lookup"><span data-stu-id="0736b-191">empty</span></span> | |
| <span data-ttu-id="0736b-192">Repositório/URL</span><span class="sxs-lookup"><span data-stu-id="0736b-192">Repository/Url</span></span> | <span data-ttu-id="0736b-193">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="0736b-193">RepositoryUrl</span></span> | <span data-ttu-id="0736b-194">empty</span><span class="sxs-lookup"><span data-stu-id="0736b-194">empty</span></span> | <span data-ttu-id="0736b-195">URL do repositório usada para clonar ou recuperar o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="0736b-195">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="0736b-196">Exemplo *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="0736b-196">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="0736b-197">Repositório/tipo</span><span class="sxs-lookup"><span data-stu-id="0736b-197">Repository/Type</span></span> | <span data-ttu-id="0736b-198">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="0736b-198">RepositoryType</span></span> | <span data-ttu-id="0736b-199">empty</span><span class="sxs-lookup"><span data-stu-id="0736b-199">empty</span></span> | <span data-ttu-id="0736b-200">Tipo de repositório.</span><span class="sxs-lookup"><span data-stu-id="0736b-200">Repository type.</span></span> <span data-ttu-id="0736b-201">Exemplos: *git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="0736b-201">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="0736b-202">Repositório/Branch</span><span class="sxs-lookup"><span data-stu-id="0736b-202">Repository/Branch</span></span> | <span data-ttu-id="0736b-203">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="0736b-203">RepositoryBranch</span></span> | <span data-ttu-id="0736b-204">empty</span><span class="sxs-lookup"><span data-stu-id="0736b-204">empty</span></span> | <span data-ttu-id="0736b-205">Informações opcionais da ramificação do repositório.</span><span class="sxs-lookup"><span data-stu-id="0736b-205">Optional repository branch information.</span></span> <span data-ttu-id="0736b-206">*RepositoryUrl* também deve ser especificado para que essa propriedade seja incluída.</span><span class="sxs-lookup"><span data-stu-id="0736b-206">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="0736b-207">Exemplo: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="0736b-207">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="0736b-208">Repositório/confirmação</span><span class="sxs-lookup"><span data-stu-id="0736b-208">Repository/Commit</span></span> | <span data-ttu-id="0736b-209">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="0736b-209">RepositoryCommit</span></span> | <span data-ttu-id="0736b-210">empty</span><span class="sxs-lookup"><span data-stu-id="0736b-210">empty</span></span> | <span data-ttu-id="0736b-211">Confirmação opcional do repositório ou conjunto de alterações para indicar de qual fonte o pacote foi criado.</span><span class="sxs-lookup"><span data-stu-id="0736b-211">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="0736b-212">*RepositoryUrl* também deve ser especificado para que essa propriedade seja incluída.</span><span class="sxs-lookup"><span data-stu-id="0736b-212">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="0736b-213">Exemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="0736b-213">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="0736b-214">PackageType</span><span class="sxs-lookup"><span data-stu-id="0736b-214">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="0736b-215">Resumo</span><span class="sxs-lookup"><span data-stu-id="0736b-215">Summary</span></span> | <span data-ttu-id="0736b-216">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="0736b-216">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="0736b-217">pack target inputs</span><span class="sxs-lookup"><span data-stu-id="0736b-217">pack target inputs</span></span>

- <span data-ttu-id="0736b-218">IsPackable</span><span class="sxs-lookup"><span data-stu-id="0736b-218">IsPackable</span></span>
- <span data-ttu-id="0736b-219">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="0736b-219">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="0736b-220">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="0736b-220">PackageVersion</span></span>
- <span data-ttu-id="0736b-221">PackageId</span><span class="sxs-lookup"><span data-stu-id="0736b-221">PackageId</span></span>
- <span data-ttu-id="0736b-222">Autores</span><span class="sxs-lookup"><span data-stu-id="0736b-222">Authors</span></span>
- <span data-ttu-id="0736b-223">Descrição</span><span class="sxs-lookup"><span data-stu-id="0736b-223">Description</span></span>
- <span data-ttu-id="0736b-224">Copyright</span><span class="sxs-lookup"><span data-stu-id="0736b-224">Copyright</span></span>
- <span data-ttu-id="0736b-225">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="0736b-225">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="0736b-226">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="0736b-226">DevelopmentDependency</span></span>
- <span data-ttu-id="0736b-227">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="0736b-227">PackageLicenseExpression</span></span>
- <span data-ttu-id="0736b-228">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="0736b-228">PackageLicenseFile</span></span>
- <span data-ttu-id="0736b-229">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="0736b-229">PackageLicenseUrl</span></span>
- <span data-ttu-id="0736b-230">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="0736b-230">PackageProjectUrl</span></span>
- <span data-ttu-id="0736b-231">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="0736b-231">PackageIconUrl</span></span>
- <span data-ttu-id="0736b-232">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="0736b-232">PackageReleaseNotes</span></span>
- <span data-ttu-id="0736b-233">PackageTags</span><span class="sxs-lookup"><span data-stu-id="0736b-233">PackageTags</span></span>
- <span data-ttu-id="0736b-234">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="0736b-234">PackageOutputPath</span></span>
- <span data-ttu-id="0736b-235">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="0736b-235">IncludeSymbols</span></span>
- <span data-ttu-id="0736b-236">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="0736b-236">IncludeSource</span></span>
- <span data-ttu-id="0736b-237">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="0736b-237">PackageTypes</span></span>
- <span data-ttu-id="0736b-238">IsTool</span><span class="sxs-lookup"><span data-stu-id="0736b-238">IsTool</span></span>
- <span data-ttu-id="0736b-239">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="0736b-239">RepositoryUrl</span></span>
- <span data-ttu-id="0736b-240">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="0736b-240">RepositoryType</span></span>
- <span data-ttu-id="0736b-241">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="0736b-241">RepositoryBranch</span></span>
- <span data-ttu-id="0736b-242">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="0736b-242">RepositoryCommit</span></span>
- <span data-ttu-id="0736b-243">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="0736b-243">NoPackageAnalysis</span></span>
- <span data-ttu-id="0736b-244">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="0736b-244">MinClientVersion</span></span>
- <span data-ttu-id="0736b-245">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="0736b-245">IncludeBuildOutput</span></span>
- <span data-ttu-id="0736b-246">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="0736b-246">IncludeContentInPack</span></span>
- <span data-ttu-id="0736b-247">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="0736b-247">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="0736b-248">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="0736b-248">ContentTargetFolders</span></span>
- <span data-ttu-id="0736b-249">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="0736b-249">NuspecFile</span></span>
- <span data-ttu-id="0736b-250">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="0736b-250">NuspecBasePath</span></span>
- <span data-ttu-id="0736b-251">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="0736b-251">NuspecProperties</span></span>
- <span data-ttu-id="0736b-252">Determinista</span><span class="sxs-lookup"><span data-stu-id="0736b-252">Deterministic</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="0736b-253">pack scenarios</span><span class="sxs-lookup"><span data-stu-id="0736b-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="0736b-254">Suprimir dependências</span><span class="sxs-lookup"><span data-stu-id="0736b-254">Suppress dependencies</span></span>

<span data-ttu-id="0736b-255">Para suprimir dependências de pacote do pacote NuGet `SuppressDependenciesWhenPacking` gerado `true` , defina como que permitirá ignorar todas as dependências do arquivo nupkg gerado.</span><span class="sxs-lookup"><span data-stu-id="0736b-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="0736b-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="0736b-256">PackageIconUrl</span></span>

> [!Important]
> <span data-ttu-id="0736b-257">PackageIconUrl foi preterido.</span><span class="sxs-lookup"><span data-stu-id="0736b-257">PackageIconUrl is deprecated.</span></span> <span data-ttu-id="0736b-258">Use [PackageIcon](#packing-an-icon-image-file) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="0736b-258">Use [PackageIcon](#packing-an-icon-image-file) instead.</span></span>

### <a name="packing-an-icon-image-file"></a><span data-ttu-id="0736b-259">Empacotando um arquivo de imagem de ícone</span><span class="sxs-lookup"><span data-stu-id="0736b-259">Packing an icon image file</span></span>

<span data-ttu-id="0736b-260">Ao empacotar um arquivo de imagem de ícone, você precisa usar a propriedade PackageIcon para especificar o caminho do pacote, em relação à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="0736b-260">When packing an icon image file, you need to use PackageIcon property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="0736b-261">Além disso, você precisa certificar-se de que o arquivo está incluído no pacote.</span><span class="sxs-lookup"><span data-stu-id="0736b-261">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="0736b-262">O tamanho do arquivo de imagem é limitado a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="0736b-262">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="0736b-263">Os formatos de arquivo com suporte incluem JPEG e PNG.</span><span class="sxs-lookup"><span data-stu-id="0736b-263">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="0736b-264">Recomendamos uma resolução de imagem de 64 x 64.</span><span class="sxs-lookup"><span data-stu-id="0736b-264">We recommend an image resolution of 64x64.</span></span>

<span data-ttu-id="0736b-265">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0736b-265">For example:</span></span>

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

<span data-ttu-id="0736b-266">[Exemplo de ícone de pacote](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="0736b-266">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="0736b-267">Para obter o equivalente do nuspec, dê uma olhada na [referência do nuspec para o ícone](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="0736b-267">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="0736b-268">Assemblies de saída</span><span class="sxs-lookup"><span data-stu-id="0736b-268">Output assemblies</span></span>

<span data-ttu-id="0736b-269">O `nuget pack` copia arquivos de saída com extensões `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="0736b-269">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="0736b-270">Os arquivos de saída que são copiados dependem do que o MSBuild fornece do destino `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="0736b-270">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="0736b-271">Há duas propriedades de MSBuild que você pode usar em seu arquivo de projeto ou a linha de comando para controlar onde ficam os assemblies de saída:</span><span class="sxs-lookup"><span data-stu-id="0736b-271">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="0736b-272">`IncludeBuildOutput`: Um booliano que determina se os assemblies de saída de compilação devem ser incluídos no pacote.</span><span class="sxs-lookup"><span data-stu-id="0736b-272">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="0736b-273">`BuildOutputTargetFolder`: Especifica a pasta na qual os assemblies de saída devem ser colocados.</span><span class="sxs-lookup"><span data-stu-id="0736b-273">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="0736b-274">Os assemblies de saída (e outros arquivos de saída) são copiados para suas respectivas pastas de estrutura.</span><span class="sxs-lookup"><span data-stu-id="0736b-274">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="0736b-275">Referências de pacote</span><span class="sxs-lookup"><span data-stu-id="0736b-275">Package references</span></span>

<span data-ttu-id="0736b-276">Consulte [Referências de pacote em arquivos de projeto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="0736b-276">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="0736b-277">Referências de projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="0736b-277">Project to project references</span></span>

<span data-ttu-id="0736b-278">As referências projeto a projeto são consideradas como referências de pacote do nuget por padrão, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0736b-278">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="0736b-279">Você também pode adicionar os seguintes metadados à referência de projeto:</span><span class="sxs-lookup"><span data-stu-id="0736b-279">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="deterministic"></a><span data-ttu-id="0736b-280">Determinista</span><span class="sxs-lookup"><span data-stu-id="0736b-280">Deterministic</span></span>

<span data-ttu-id="0736b-281">Ao usar `MSBuild -t:pack -p:Deterministic=true`o, várias invocações do destino do pacote irão gerar exatamente o mesmo pacote.</span><span class="sxs-lookup"><span data-stu-id="0736b-281">When using `MSBuild -t:pack -p:Deterministic=true`, multiple invocations of the the pack target will generate the exact same package.</span></span>
<span data-ttu-id="0736b-282">A saída do comando de pacote não é afetada pelo estado de ambiente da máquina.</span><span class="sxs-lookup"><span data-stu-id="0736b-282">The output of the pack command is not affected by the ambient state of the machine.</span></span> <span data-ttu-id="0736b-283">Especificamente, as entradas zip serão marcadas como 1980-01-01.</span><span class="sxs-lookup"><span data-stu-id="0736b-283">Specifically zip entries will be timestamped as 1980-01-01.</span></span> <span data-ttu-id="0736b-284">Para obter o determinante completo, os assemblies devem ser compilados com a opção de compilador respectiva, [determinística](/dotnet/csharp/language-reference/compiler-options/deterministic-compiler-option).</span><span class="sxs-lookup"><span data-stu-id="0736b-284">To achieve full determinism, the assemblies should be built with the respective compiler option [-deterministic](/dotnet/csharp/language-reference/compiler-options/deterministic-compiler-option).</span></span>
<span data-ttu-id="0736b-285">É recomendável que você especifique a propriedade determinística como a seguir, para que o compilador e o NuGet o respeitarão.</span><span class="sxs-lookup"><span data-stu-id="0736b-285">It is recommended that you specify the deterministic property like following, so both the compiler and NuGet will respect it.</span></span>

```xml
<PropertyGroup>
  <Deterministic>true</Deterministic>
</PropertyGroup>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="0736b-286">Incluindo o conteúdo em um pacote</span><span class="sxs-lookup"><span data-stu-id="0736b-286">Including content in a package</span></span>

<span data-ttu-id="0736b-287">Para incluir o conteúdo, adicione metadados extras ao item `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="0736b-287">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="0736b-288">Por padrão, tudo que pertencer ao tipo “Conteúdo” é incluído no pacote, a menos que seja substituído por entradas como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="0736b-288">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="0736b-289">Por padrão, tudo é adicionado à raiz da pasta `content` e `contentFiles\any\<target_framework>` dentro de um pacote e preserva a estrutura e pasta relativa, a menos que você especifique um caminho de pacote:</span><span class="sxs-lookup"><span data-stu-id="0736b-289">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="0736b-290">Se você quiser copiar todo o conteúdo somente para determinadas pastas raiz (em vez de para `content` e `contentFiles`), será possível usar a propriedade `ContentTargetFolders` do MSBuild, que assume como padrão "content;contentFiles", mas pode ser definida como qualquer outro nome de pasta.</span><span class="sxs-lookup"><span data-stu-id="0736b-290">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="0736b-291">Observe que só especificar “contentFiles” em `ContentTargetFolders` coloca os arquivos em `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` com base em `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="0736b-291">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="0736b-292">`PackagePath` pode ser um conjunto de caminhos de destino separados por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="0736b-292">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="0736b-293">Especificar um caminho de pacote vazio adicionaria o arquivo à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="0736b-293">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="0736b-294">Por exemplo, o seguinte adiciona `libuv.txt` a `content\myfiles`, `content\samples` e a raiz do pacote:</span><span class="sxs-lookup"><span data-stu-id="0736b-294">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="0736b-295">Há também uma propriedade de MSBuild `$(IncludeContentInPack)`, que assume o padrão `true`.</span><span class="sxs-lookup"><span data-stu-id="0736b-295">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="0736b-296">Se isso for definido como `false` em qualquer projeto, o conteúdo desse projeto não está incluso no pacote do nuget.</span><span class="sxs-lookup"><span data-stu-id="0736b-296">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="0736b-297">Outros metadados específicos do pacote que pode ser definido em qualquer um dos itens acima ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, que define os valores ```CopyToOutput``` e ```Flatten``` na entrada ```contentFiles``` no nuspec de saída.</span><span class="sxs-lookup"><span data-stu-id="0736b-297">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="0736b-298">Além de itens de Conteúdo, os metadados `<Pack>` e `<PackagePath>` também podem ser definidos em arquivos com uma ação de Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.</span><span class="sxs-lookup"><span data-stu-id="0736b-298">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="0736b-299">Para o pacote acrescentar o nome de arquivo ao caminho do pacote ao usar padrões glob, seu caminho de pacote deve terminar com o caractere separador de pasta, caso contrário, o caminho do pacote será tratado como o caminho completo, incluindo o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="0736b-299">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="0736b-300">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="0736b-300">IncludeSymbols</span></span>

<span data-ttu-id="0736b-301">Ao usar o `MSBuild -t:pack -p:IncludeSymbols=true`, os arquivos `.pdb` correspondentes são copiados junto com outros arquivos de saída (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="0736b-301">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="0736b-302">Observe que a configuração `IncludeSymbols=true` cria um pacote regular *e* um pacote de símbolos.</span><span class="sxs-lookup"><span data-stu-id="0736b-302">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="0736b-303">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="0736b-303">IncludeSource</span></span>

<span data-ttu-id="0736b-304">Isso é o mesmo que `IncludeSymbols`, exceto que também copia os arquivos de origem com arquivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="0736b-304">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="0736b-305">Todos os arquivos do tipo `Compile` são copiadas para `src\<ProjectName>\`, preservando a estrutura de pastas do caminho relativo no pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="0736b-305">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="0736b-306">O mesmo também ocorre para arquivos de origem de qualquer `ProjectReference` que tem `TreatAsPackageReference` definido como `false`.</span><span class="sxs-lookup"><span data-stu-id="0736b-306">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="0736b-307">Se um arquivo do tipo Compilação estiver fora da pasta de projeto, ele será adicionado apenas a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="0736b-307">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="0736b-308">Empacotando uma expressão de licença ou um arquivo de licença</span><span class="sxs-lookup"><span data-stu-id="0736b-308">Packing a license expression or a license file</span></span>

<span data-ttu-id="0736b-309">Ao usar uma expressão de licença, a propriedade PackageLicenseExpression deve ser usada.</span><span class="sxs-lookup"><span data-stu-id="0736b-309">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="0736b-310">[Exemplo de expressão de licença](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="0736b-310">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="0736b-311">[Saiba mais sobre as expressões de licença e as licenças que são aceitas pelo NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="0736b-311">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="0736b-312">Ao empacotar um arquivo de licença, você precisa usar a propriedade PackageLicenseFile para especificar o caminho do pacote, em relação à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="0736b-312">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="0736b-313">Além disso, você precisa certificar-se de que o arquivo está incluído no pacote.</span><span class="sxs-lookup"><span data-stu-id="0736b-313">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="0736b-314">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0736b-314">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="0736b-315">[Exemplo de arquivo de licença](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="0736b-315">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="0736b-316">IsTool</span><span class="sxs-lookup"><span data-stu-id="0736b-316">IsTool</span></span>

<span data-ttu-id="0736b-317">Ao usar `MSBuild -t:pack -p:IsTool=true`, todos os arquivos de saída, conforme especificado no cenário [Assemblies de saída](#output-assemblies), são copiados para a pasta `tools` em vez da pasta `lib`.</span><span class="sxs-lookup"><span data-stu-id="0736b-317">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="0736b-318">Observe que isso é diferente de um `DotNetCliTool` que é especificado pela configuração do `PackageType` no arquivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="0736b-318">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="0736b-319">Empacotamento usando um .nuspec</span><span class="sxs-lookup"><span data-stu-id="0736b-319">Packing using a .nuspec</span></span>

<span data-ttu-id="0736b-320">Embora seja recomendável [incluir todas as propriedades](../reference/msbuild-targets.md#pack-target) que normalmente estão no `.nuspec` arquivo no arquivo de projeto, você pode optar por usar um `.nuspec` arquivo para empacotar seu projeto.</span><span class="sxs-lookup"><span data-stu-id="0736b-320">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="0736b-321">Para um projeto de estilo não-SDK que usa `PackageReference`o, você deve `NuGet.Build.Tasks.Pack.targets` importar para que a tarefa de pacote possa ser executada.</span><span class="sxs-lookup"><span data-stu-id="0736b-321">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="0736b-322">Você ainda precisa restaurar o projeto antes de poder empacotar um arquivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="0736b-322">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="0736b-323">(Um projeto no estilo SDK inclui os destinos do pacote por padrão.)</span><span class="sxs-lookup"><span data-stu-id="0736b-323">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="0736b-324">A estrutura de destino do arquivo de projeto é irrelevante e não é usada ao empacotar um nuspec.</span><span class="sxs-lookup"><span data-stu-id="0736b-324">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="0736b-325">As três propriedades MSBuild a seguir são relevantes para empacotamento usando um `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="0736b-325">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="0736b-326">`NuspecFile`: caminho relativo ou absoluto para o arquivo `.nuspec` que está sendo usado para o empacotamento.</span><span class="sxs-lookup"><span data-stu-id="0736b-326">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="0736b-327">`NuspecProperties`: uma lista separada por ponto e vírgula de pares chave/valor.</span><span class="sxs-lookup"><span data-stu-id="0736b-327">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="0736b-328">Devido à maneira como a análise de linha de comando do MSBuild funciona, várias propriedades precisam ser especificadas da seguinte maneira: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="0736b-328">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="0736b-329">`NuspecBasePath`: Caminho base do `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="0736b-329">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="0736b-330">Se estiver usando `dotnet.exe` para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0736b-330">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="0736b-331">Se estiver usando o MSBuild para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0736b-331">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="0736b-332">Observe que empacotar um nuspec usando dotNet. exe ou MSBuild também leva a criar o projeto por padrão.</span><span class="sxs-lookup"><span data-stu-id="0736b-332">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="0736b-333">Isso pode ser evitado passando ```--no-build``` a propriedade para dotnet. exe, que é o equivalente à ```<NoBuild>true</NoBuild> ``` configuração em seu arquivo de projeto, juntamente ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` com a configuração no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="0736b-333">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="0736b-334">Um exemplo de um arquivo *. csproj* para empacotar um arquivo nuspec é:</span><span class="sxs-lookup"><span data-stu-id="0736b-334">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="0736b-335">Pontos de extensão avançados para criar pacote personalizado</span><span class="sxs-lookup"><span data-stu-id="0736b-335">Advanced extension points to create customized package</span></span>

<span data-ttu-id="0736b-336">O `pack` destino fornece dois pontos de extensão que são executados na compilação interna, específica da estrutura de destino.</span><span class="sxs-lookup"><span data-stu-id="0736b-336">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="0736b-337">Os pontos de extensão dão suporte à inclusão de conteúdo específico da estrutura de destino e assemblies em um pacote:</span><span class="sxs-lookup"><span data-stu-id="0736b-337">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="0736b-338">`TargetsForTfmSpecificBuildOutput`alvo Use para arquivos dentro da `lib` pasta ou de uma pasta especificada `BuildOutputTargetFolder`usando.</span><span class="sxs-lookup"><span data-stu-id="0736b-338">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="0736b-339">`TargetsForTfmSpecificContentInPackage`alvo Use para arquivos fora do `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="0736b-339">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="0736b-340">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="0736b-340">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="0736b-341">Escreva um destino personalizado e especifique-o como o valor da `$(TargetsForTfmSpecificBuildOutput)` propriedade.</span><span class="sxs-lookup"><span data-stu-id="0736b-341">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="0736b-342">Para todos os arquivos que precisam entrar em `BuildOutputTargetFolder` (lib por padrão), o destino deve gravar esses arquivos no grupo `BuildOutputInPackage` de itens e definir os dois valores de metadados a seguir:</span><span class="sxs-lookup"><span data-stu-id="0736b-342">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="0736b-343">`FinalOutputPath`: O caminho absoluto do arquivo; Se não for fornecido, a identidade será usada para avaliar o caminho de origem.</span><span class="sxs-lookup"><span data-stu-id="0736b-343">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="0736b-344">`TargetPath`:  Adicional Defina quando o arquivo precisa entrar em uma subpasta no `lib\<TargetFramework>` , como assemblies satélite que estão sob suas respectivas pastas de cultura.</span><span class="sxs-lookup"><span data-stu-id="0736b-344">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="0736b-345">O padrão é o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="0736b-345">Defaults to the name of the file.</span></span>

<span data-ttu-id="0736b-346">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="0736b-346">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="0736b-347">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="0736b-347">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="0736b-348">Escreva um destino personalizado e especifique-o como o valor da `$(TargetsForTfmSpecificContentInPackage)` propriedade.</span><span class="sxs-lookup"><span data-stu-id="0736b-348">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="0736b-349">Para todos os arquivos a serem incluídos no pacote, o destino deve gravar esses arquivos no grupo `TfmSpecificPackageFile` de itens e definir os seguintes metadados opcionais:</span><span class="sxs-lookup"><span data-stu-id="0736b-349">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="0736b-350">`PackagePath`: Caminho em que o arquivo deve ser apresentado no pacote.</span><span class="sxs-lookup"><span data-stu-id="0736b-350">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="0736b-351">O NuGet emitirá um aviso se mais de um arquivo for adicionado ao mesmo caminho de pacote.</span><span class="sxs-lookup"><span data-stu-id="0736b-351">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="0736b-352">`BuildAction`: A ação de compilação a ser atribuída ao arquivo, necessária somente se o caminho do pacote estiver `contentFiles` na pasta.</span><span class="sxs-lookup"><span data-stu-id="0736b-352">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="0736b-353">O padrão é "None".</span><span class="sxs-lookup"><span data-stu-id="0736b-353">Defaults to "None".</span></span>

<span data-ttu-id="0736b-354">Um exemplo:</span><span class="sxs-lookup"><span data-stu-id="0736b-354">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="0736b-355">restore target</span><span class="sxs-lookup"><span data-stu-id="0736b-355">restore target</span></span>

<span data-ttu-id="0736b-356">`MSBuild -t:restore` (que `nuget restore` e `dotnet restore` usam com projetos do .NET Core), restaura pacotes referenciados no arquivo de projeto da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0736b-356">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="0736b-357">Ler todas as referências projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="0736b-357">Read all project to project references</span></span>
1. <span data-ttu-id="0736b-358">Ler as propriedades do projeto para localizar a pasta intermediária e as estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="0736b-358">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="0736b-359">Transmitir dados do MSBuild para NuGet. Build. Tasks. dll</span><span class="sxs-lookup"><span data-stu-id="0736b-359">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="0736b-360">Executar restauração</span><span class="sxs-lookup"><span data-stu-id="0736b-360">Run restore</span></span>
1. <span data-ttu-id="0736b-361">Baixar os pacotes</span><span class="sxs-lookup"><span data-stu-id="0736b-361">Download packages</span></span>
1. <span data-ttu-id="0736b-362">Gravar arquivo de ativos, destinos e objetos</span><span class="sxs-lookup"><span data-stu-id="0736b-362">Write assets file, targets, and props</span></span>

<span data-ttu-id="0736b-363">O `restore` destino funciona **apenas** para projetos que usam o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="0736b-363">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="0736b-364">Ele não **funciona para** projetos que usam o `packages.config` formato; em vez disso, use a [restauração do NuGet](../reference/cli-reference/cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="0736b-364">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="0736b-365">Restaurar propriedades</span><span class="sxs-lookup"><span data-stu-id="0736b-365">Restore properties</span></span>

<span data-ttu-id="0736b-366">Configurações de restauração adicionais podem vir de propriedades MSBuild no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="0736b-366">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="0736b-367">Os valores também podem ser definidos na linha de comando usando a opção `-p:` (consulte os Exemplos abaixo).</span><span class="sxs-lookup"><span data-stu-id="0736b-367">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="0736b-368">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0736b-368">Property</span></span> | <span data-ttu-id="0736b-369">Descrição</span><span class="sxs-lookup"><span data-stu-id="0736b-369">Description</span></span> |
|--------|--------|
| <span data-ttu-id="0736b-370">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="0736b-370">RestoreSources</span></span> | <span data-ttu-id="0736b-371">Uma lista delimitada por ponto e vírgula de origens de pacote.</span><span class="sxs-lookup"><span data-stu-id="0736b-371">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="0736b-372">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="0736b-372">RestorePackagesPath</span></span> | <span data-ttu-id="0736b-373">Caminho da pasta dos pacotes do usuário.</span><span class="sxs-lookup"><span data-stu-id="0736b-373">User packages folder path.</span></span> |
| <span data-ttu-id="0736b-374">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="0736b-374">RestoreDisableParallel</span></span> | <span data-ttu-id="0736b-375">Limite os downloads para um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="0736b-375">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="0736b-376">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="0736b-376">RestoreConfigFile</span></span> | <span data-ttu-id="0736b-377">Caminho para um arquivo `Nuget.Config` a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="0736b-377">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="0736b-378">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="0736b-378">RestoreNoCache</span></span> | <span data-ttu-id="0736b-379">Se for true, evita o uso de pacotes armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="0736b-379">If true, avoids using cached packages.</span></span> <span data-ttu-id="0736b-380">Consulte [Gerenciando os pacotes globais e as pastas de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="0736b-380">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="0736b-381">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="0736b-381">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="0736b-382">Se verdadeiro, ignora origens de pacote com falha ou ausentes.</span><span class="sxs-lookup"><span data-stu-id="0736b-382">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="0736b-383">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="0736b-383">RestoreFallbackFolders</span></span> | <span data-ttu-id="0736b-384">Pastas de fallback, usadas da mesma maneira que a pasta pacotes de usuário é usada.</span><span class="sxs-lookup"><span data-stu-id="0736b-384">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="0736b-385">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="0736b-385">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="0736b-386">Fontes adicionais a serem usadas durante a restauração.</span><span class="sxs-lookup"><span data-stu-id="0736b-386">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="0736b-387">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="0736b-387">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="0736b-388">Pastas de fallback adicionais a serem usadas durante a restauração.</span><span class="sxs-lookup"><span data-stu-id="0736b-388">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="0736b-389">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="0736b-389">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="0736b-390">Exclui as pastas de fallback especificadas em`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="0736b-390">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="0736b-391">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="0736b-391">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="0736b-392">Caminho para `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="0736b-392">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="0736b-393">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="0736b-393">RestoreGraphProjectInput</span></span> | <span data-ttu-id="0736b-394">Lista separada por ponto e vírgula de projetos a serem restaurados, que devem conter caminhos absolutos.</span><span class="sxs-lookup"><span data-stu-id="0736b-394">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="0736b-395">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="0736b-395">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="0736b-396">Quando os projetos são coletados via MSBuild, ele determina se eles são coletados usando a `SkipNonexistentTargets` otimização.</span><span class="sxs-lookup"><span data-stu-id="0736b-396">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="0736b-397">Quando não definido, o padrão é `true`.</span><span class="sxs-lookup"><span data-stu-id="0736b-397">When not set, defaults to `true`.</span></span> <span data-ttu-id="0736b-398">A conseqüência é um comportamento com falha rápida quando os destinos de um projeto não podem ser importados.</span><span class="sxs-lookup"><span data-stu-id="0736b-398">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="0736b-399">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="0736b-399">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="0736b-400">Pasta de saída, padronizando `BaseIntermediateOutputPath` para e `obj` a pasta.</span><span class="sxs-lookup"><span data-stu-id="0736b-400">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="0736b-401">Exemplos</span><span class="sxs-lookup"><span data-stu-id="0736b-401">Examples</span></span>

<span data-ttu-id="0736b-402">Linha de comando:</span><span class="sxs-lookup"><span data-stu-id="0736b-402">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="0736b-403">Arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="0736b-403">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="0736b-404">Restaurar saídas</span><span class="sxs-lookup"><span data-stu-id="0736b-404">Restore outputs</span></span>

<span data-ttu-id="0736b-405">A restauração cria os seguintes arquivos na pasta `obj` de build:</span><span class="sxs-lookup"><span data-stu-id="0736b-405">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="0736b-406">Arquivo</span><span class="sxs-lookup"><span data-stu-id="0736b-406">File</span></span> | <span data-ttu-id="0736b-407">Descrição</span><span class="sxs-lookup"><span data-stu-id="0736b-407">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="0736b-408">Contém o grafo de dependência de todas as referências de pacote.</span><span class="sxs-lookup"><span data-stu-id="0736b-408">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="0736b-409">Referências a objetos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="0736b-409">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="0736b-410">Referências a destinos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="0736b-410">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="0736b-411">Restaurando e compilando com um comando do MSBuild</span><span class="sxs-lookup"><span data-stu-id="0736b-411">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="0736b-412">Devido ao fato de que o NuGet pode restaurar pacotes que desativam destinos e props do MSBuild, as avaliações de restauração e compilação são executadas com propriedades globais diferentes.</span><span class="sxs-lookup"><span data-stu-id="0736b-412">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="0736b-413">Isso significa que o seguinte terá um comportamento imprevisível e geralmente incorreto.</span><span class="sxs-lookup"><span data-stu-id="0736b-413">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="0736b-414">Em vez disso, a abordagem recomendada é:</span><span class="sxs-lookup"><span data-stu-id="0736b-414">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="0736b-415">A mesma lógica se aplica a outros destinos semelhantes `build`a.</span><span class="sxs-lookup"><span data-stu-id="0736b-415">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="0736b-416">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="0736b-416">PackageTargetFallback</span></span>

<span data-ttu-id="0736b-417">O elemento `PackageTargetFallback` permite especificar um conjunto de destinos compatíveis a serem usados ao restaurar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="0736b-417">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="0736b-418">Ele foi desenvolvido para permitir que os pacotes que usam o dotnet [TxM](../reference/target-frameworks.md) funcionem com pacotes compatíveis que não declaram um dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="0736b-418">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="0736b-419">Ou seja, se o projeto usar o dotnet TxM, todos os pacotes dos quais ele depende também deverão ter um dotnet TxM, a menos que você adicione o `<PackageTargetFallback>` ao projeto para permitir que plataformas não dotnet sejam compatíveis com o dotnet.</span><span class="sxs-lookup"><span data-stu-id="0736b-419">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="0736b-420">Por exemplo, se o projeto está usando o `netstandard1.6` TxM e um pacote dependente contém apenas `lib/net45/a.dll` e `lib/portable-net45+win81/a.dll`, o projeto não será compilado.</span><span class="sxs-lookup"><span data-stu-id="0736b-420">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="0736b-421">Se a DLL que você deseja colocar é esta última, é possível adicionar um `PackageTargetFallback` como mostrado a seguir para dizer que a DLL `portable-net45+win81` é compatível:</span><span class="sxs-lookup"><span data-stu-id="0736b-421">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="0736b-422">Para declarar um fallback para todos os destinos em seu projeto, deixe o atributo `Condition` de fora.</span><span class="sxs-lookup"><span data-stu-id="0736b-422">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="0736b-423">Você também pode estender qualquer `PackageTargetFallback` existente incluindo `$(PackageTargetFallback)` conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="0736b-423">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="0736b-424">Substituindo uma biblioteca de um grafo de restauração</span><span class="sxs-lookup"><span data-stu-id="0736b-424">Replacing one library from a restore graph</span></span>

<span data-ttu-id="0736b-425">Se uma restauração está trazendo o assembly errado, é possível excluir a escolha padrão do pacote e substituí-lo por outro de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="0736b-425">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="0736b-426">Primeiro com um `PackageReference` de nível superior, exclua todos os ativos:</span><span class="sxs-lookup"><span data-stu-id="0736b-426">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="0736b-427">Em seguida, adicione sua própria referência à cópia local apropriada da DLL:</span><span class="sxs-lookup"><span data-stu-id="0736b-427">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
