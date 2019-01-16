---
title: Empacotamento e restauração do NuGet como destinos do MSBuild
description: O pack e restore do NuGet podem funcionar diretamente como destinos do MSBuild com o NuGet 4.0 e superior.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 8132595cbfaf553736fbcc81aada283a44d6cdbf
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324845"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="37daf-103">Empacotamento e restauração do NuGet como destinos do MSBuild</span><span class="sxs-lookup"><span data-stu-id="37daf-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="37daf-104">*NuGet 4.0 ou superior*</span><span class="sxs-lookup"><span data-stu-id="37daf-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="37daf-105">Com o formato PackageReference, o NuGet 4.0 e posterior pode armazenar todos os metadados de manifesto diretamente dentro de um arquivo de projeto em vez de usar um arquivo `.nuspec` separado.</span><span class="sxs-lookup"><span data-stu-id="37daf-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="37daf-106">Com o MSBuild 15.1 ou superior, o NuGet também é um cidadão de primeira classe do MSBuild com os destinos `pack` e `restore`, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="37daf-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="37daf-107">Esses destinos permitem que você trabalhe com o NuGet como faria com qualquer outra tarefa ou destino do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="37daf-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="37daf-108">(Para NuGet 3.x e anteriores, use os comandos [pack](../tools/cli-ref-pack.md) e [restore](../tools/cli-ref-restore.md) na CLI do NuGet.)</span><span class="sxs-lookup"><span data-stu-id="37daf-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="37daf-109">Ordem de build de destino</span><span class="sxs-lookup"><span data-stu-id="37daf-109">Target build order</span></span>

<span data-ttu-id="37daf-110">Como `pack` e `restore` são os destinos do MSBuild, você pode acessá-los para melhorar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="37daf-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="37daf-111">Por exemplo, digamos que você deseja copiar o pacote para um compartilhamento de rede após empacotá-lo.</span><span class="sxs-lookup"><span data-stu-id="37daf-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="37daf-112">Você pode fazer isso adicionando o seguinte ao seu arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="37daf-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="37daf-113">Da mesma forma, você pode gravar uma tarefa do MSBuild, escrever seu próprio destino e consumir propriedades do NuGet na tarefa de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="37daf-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="37daf-114">pack target</span><span class="sxs-lookup"><span data-stu-id="37daf-114">pack target</span></span>

<span data-ttu-id="37daf-115">Para projetos do .NET Standard usando o formato PackageReference, `msbuild -t:pack` extrai as entradas do arquivo de projeto para usar na criação de um pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="37daf-115">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="37daf-116">A tabela abaixo descreve as propriedades do MSBuild que podem ser adicionadas a um arquivo do projeto dentro do primeiro nó `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="37daf-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="37daf-117">Você pode fazer essas edições facilmente no Visual Studio 2017 e posterior clicando com o botão direito do mouse no projeto e selecionando **Editar {project_name}** no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="37daf-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="37daf-118">Para sua conveniência, a tabela é organizada pela propriedade equivalente em um arquivo [`.nuspec` ](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="37daf-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="37daf-119">Observe que as propriedades `Owners` e `Summary` de `.nuspec` não são compatíveis com o MSBuild.</span><span class="sxs-lookup"><span data-stu-id="37daf-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="37daf-120">Valor de atributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="37daf-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="37daf-121">Propriedade do MSBuild</span><span class="sxs-lookup"><span data-stu-id="37daf-121">MSBuild Property</span></span> | <span data-ttu-id="37daf-122">Padrão</span><span class="sxs-lookup"><span data-stu-id="37daf-122">Default</span></span> | <span data-ttu-id="37daf-123">Observações</span><span class="sxs-lookup"><span data-stu-id="37daf-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="37daf-124">Id</span><span class="sxs-lookup"><span data-stu-id="37daf-124">Id</span></span> | <span data-ttu-id="37daf-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="37daf-125">PackageId</span></span> | <span data-ttu-id="37daf-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="37daf-126">AssemblyName</span></span> | <span data-ttu-id="37daf-127">$(AssemblyName) do MSBuild</span><span class="sxs-lookup"><span data-stu-id="37daf-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="37daf-128">Versão</span><span class="sxs-lookup"><span data-stu-id="37daf-128">Version</span></span> | <span data-ttu-id="37daf-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="37daf-129">PackageVersion</span></span> | <span data-ttu-id="37daf-130">Versão</span><span class="sxs-lookup"><span data-stu-id="37daf-130">Version</span></span> | <span data-ttu-id="37daf-131">Isso é compatível com semver, por exemplo “1.0.0”, “1.0.0-beta” ou “1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="37daf-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="37daf-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="37daf-132">VersionPrefix</span></span> | <span data-ttu-id="37daf-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="37daf-133">PackageVersionPrefix</span></span> | <span data-ttu-id="37daf-134">empty</span><span class="sxs-lookup"><span data-stu-id="37daf-134">empty</span></span> | <span data-ttu-id="37daf-135">A configuração PackageVersion substitui PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="37daf-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="37daf-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="37daf-136">VersionSuffix</span></span> | <span data-ttu-id="37daf-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="37daf-137">PackageVersionSuffix</span></span> | <span data-ttu-id="37daf-138">empty</span><span class="sxs-lookup"><span data-stu-id="37daf-138">empty</span></span> | <span data-ttu-id="37daf-139">$(VersionSuffix) do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="37daf-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="37daf-140">A configuração PackageVersion substitui PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="37daf-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="37daf-141">Autores</span><span class="sxs-lookup"><span data-stu-id="37daf-141">Authors</span></span> | <span data-ttu-id="37daf-142">Autores</span><span class="sxs-lookup"><span data-stu-id="37daf-142">Authors</span></span> | <span data-ttu-id="37daf-143">Nome do usuário atual</span><span class="sxs-lookup"><span data-stu-id="37daf-143">Username of the current user</span></span> | |
| <span data-ttu-id="37daf-144">Proprietários</span><span class="sxs-lookup"><span data-stu-id="37daf-144">Owners</span></span> | <span data-ttu-id="37daf-145">N/D</span><span class="sxs-lookup"><span data-stu-id="37daf-145">N/A</span></span> | <span data-ttu-id="37daf-146">Não está presente no NuSpec</span><span class="sxs-lookup"><span data-stu-id="37daf-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="37daf-147">Título</span><span class="sxs-lookup"><span data-stu-id="37daf-147">Title</span></span> | <span data-ttu-id="37daf-148">Título</span><span class="sxs-lookup"><span data-stu-id="37daf-148">Title</span></span> | <span data-ttu-id="37daf-149">O PackageId</span><span class="sxs-lookup"><span data-stu-id="37daf-149">The PackageId</span></span>| |
| <span data-ttu-id="37daf-150">Descrição</span><span class="sxs-lookup"><span data-stu-id="37daf-150">Description</span></span> | <span data-ttu-id="37daf-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="37daf-151">Description</span></span> | <span data-ttu-id="37daf-152">“Package Description”</span><span class="sxs-lookup"><span data-stu-id="37daf-152">"Package Description"</span></span> | |
| <span data-ttu-id="37daf-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="37daf-153">Copyright</span></span> | <span data-ttu-id="37daf-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="37daf-154">Copyright</span></span> | <span data-ttu-id="37daf-155">empty</span><span class="sxs-lookup"><span data-stu-id="37daf-155">empty</span></span> | |
| <span data-ttu-id="37daf-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="37daf-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="37daf-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="37daf-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="37daf-158">false</span><span class="sxs-lookup"><span data-stu-id="37daf-158">false</span></span> | |
| <span data-ttu-id="37daf-159">Licença</span><span class="sxs-lookup"><span data-stu-id="37daf-159">license</span></span> | <span data-ttu-id="37daf-160">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="37daf-160">PackageLicenseExpression</span></span> | <span data-ttu-id="37daf-161">empty</span><span class="sxs-lookup"><span data-stu-id="37daf-161">empty</span></span> | <span data-ttu-id="37daf-162">Corresponde a `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="37daf-162">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="37daf-163">Licença</span><span class="sxs-lookup"><span data-stu-id="37daf-163">license</span></span> | <span data-ttu-id="37daf-164">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="37daf-164">PackageLicenseFile</span></span> | <span data-ttu-id="37daf-165">empty</span><span class="sxs-lookup"><span data-stu-id="37daf-165">empty</span></span> | <span data-ttu-id="37daf-166">Corresponde ao `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="37daf-166">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="37daf-167">Talvez você precise explicitamente o arquivo de licença referenciado do pacote.</span><span class="sxs-lookup"><span data-stu-id="37daf-167">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="37daf-168">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="37daf-168">LicenseUrl</span></span> | <span data-ttu-id="37daf-169">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="37daf-169">PackageLicenseUrl</span></span> | <span data-ttu-id="37daf-170">empty</span><span class="sxs-lookup"><span data-stu-id="37daf-170">empty</span></span> | <span data-ttu-id="37daf-171">`licenseUrl` está sendo preterido, use a propriedade PackageLicenseExpression ou PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="37daf-171">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="37daf-172">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="37daf-172">ProjectUrl</span></span> | <span data-ttu-id="37daf-173">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="37daf-173">PackageProjectUrl</span></span> | <span data-ttu-id="37daf-174">empty</span><span class="sxs-lookup"><span data-stu-id="37daf-174">empty</span></span> | |
| <span data-ttu-id="37daf-175">IconUrl</span><span class="sxs-lookup"><span data-stu-id="37daf-175">IconUrl</span></span> | <span data-ttu-id="37daf-176">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="37daf-176">PackageIconUrl</span></span> | <span data-ttu-id="37daf-177">empty</span><span class="sxs-lookup"><span data-stu-id="37daf-177">empty</span></span> | |
| <span data-ttu-id="37daf-178">Marcas</span><span class="sxs-lookup"><span data-stu-id="37daf-178">Tags</span></span> | <span data-ttu-id="37daf-179">PackageTags</span><span class="sxs-lookup"><span data-stu-id="37daf-179">PackageTags</span></span> | <span data-ttu-id="37daf-180">empty</span><span class="sxs-lookup"><span data-stu-id="37daf-180">empty</span></span> | <span data-ttu-id="37daf-181">Marcas são delimitadas por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="37daf-181">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="37daf-182">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="37daf-182">ReleaseNotes</span></span> | <span data-ttu-id="37daf-183">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="37daf-183">PackageReleaseNotes</span></span> | <span data-ttu-id="37daf-184">empty</span><span class="sxs-lookup"><span data-stu-id="37daf-184">empty</span></span> | |
| <span data-ttu-id="37daf-185">Url do repositório</span><span class="sxs-lookup"><span data-stu-id="37daf-185">Repository/Url</span></span> | <span data-ttu-id="37daf-186">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="37daf-186">RepositoryUrl</span></span> | <span data-ttu-id="37daf-187">empty</span><span class="sxs-lookup"><span data-stu-id="37daf-187">empty</span></span> | <span data-ttu-id="37daf-188">URL do repositório usado para clonar ou recuperar o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="37daf-188">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="37daf-189">Exemplo: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="37daf-189">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="37daf-190">Tipo do repositório</span><span class="sxs-lookup"><span data-stu-id="37daf-190">Repository/Type</span></span> | <span data-ttu-id="37daf-191">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="37daf-191">RepositoryType</span></span> | <span data-ttu-id="37daf-192">empty</span><span class="sxs-lookup"><span data-stu-id="37daf-192">empty</span></span> | <span data-ttu-id="37daf-193">Tipo de repositório.</span><span class="sxs-lookup"><span data-stu-id="37daf-193">Repository type.</span></span> <span data-ttu-id="37daf-194">Exemplos: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="37daf-194">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="37daf-195">/ Ramificação do repositório</span><span class="sxs-lookup"><span data-stu-id="37daf-195">Repository/Branch</span></span> | <span data-ttu-id="37daf-196">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="37daf-196">RepositoryBranch</span></span> | <span data-ttu-id="37daf-197">empty</span><span class="sxs-lookup"><span data-stu-id="37daf-197">empty</span></span> | <span data-ttu-id="37daf-198">Informações de branch do repositório opcional.</span><span class="sxs-lookup"><span data-stu-id="37daf-198">Optional repository branch information.</span></span> <span data-ttu-id="37daf-199">*{1&gt;repositoryurl&lt;1* também deve ser especificado para essa propriedade a ser incluído.</span><span class="sxs-lookup"><span data-stu-id="37daf-199">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="37daf-200">Exemplo: *mestre* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="37daf-200">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="37daf-201">Repositório/confirmação</span><span class="sxs-lookup"><span data-stu-id="37daf-201">Repository/Commit</span></span> | <span data-ttu-id="37daf-202">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="37daf-202">RepositoryCommit</span></span> | <span data-ttu-id="37daf-203">empty</span><span class="sxs-lookup"><span data-stu-id="37daf-203">empty</span></span> | <span data-ttu-id="37daf-204">Confirmação do repositório opcional ou conjunto de alterações para indicar que o pacote de código-fonte foi compilado.</span><span class="sxs-lookup"><span data-stu-id="37daf-204">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="37daf-205">*{1&gt;repositoryurl&lt;1* também deve ser especificado para essa propriedade a ser incluído.</span><span class="sxs-lookup"><span data-stu-id="37daf-205">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="37daf-206">Exemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="37daf-206">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="37daf-207">PackageType</span><span class="sxs-lookup"><span data-stu-id="37daf-207">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="37daf-208">Resumo</span><span class="sxs-lookup"><span data-stu-id="37daf-208">Summary</span></span> | <span data-ttu-id="37daf-209">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="37daf-209">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="37daf-210">pack target inputs</span><span class="sxs-lookup"><span data-stu-id="37daf-210">pack target inputs</span></span>

- <span data-ttu-id="37daf-211">IsPackable</span><span class="sxs-lookup"><span data-stu-id="37daf-211">IsPackable</span></span>
- <span data-ttu-id="37daf-212">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="37daf-212">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="37daf-213">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="37daf-213">PackageVersion</span></span>
- <span data-ttu-id="37daf-214">PackageId</span><span class="sxs-lookup"><span data-stu-id="37daf-214">PackageId</span></span>
- <span data-ttu-id="37daf-215">Autores</span><span class="sxs-lookup"><span data-stu-id="37daf-215">Authors</span></span>
- <span data-ttu-id="37daf-216">Descrição</span><span class="sxs-lookup"><span data-stu-id="37daf-216">Description</span></span>
- <span data-ttu-id="37daf-217">Copyright</span><span class="sxs-lookup"><span data-stu-id="37daf-217">Copyright</span></span>
- <span data-ttu-id="37daf-218">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="37daf-218">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="37daf-219">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="37daf-219">DevelopmentDependency</span></span>
- <span data-ttu-id="37daf-220">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="37daf-220">PackageLicenseExpression</span></span>
- <span data-ttu-id="37daf-221">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="37daf-221">PackageLicenseFile</span></span>
- <span data-ttu-id="37daf-222">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="37daf-222">PackageLicenseUrl</span></span>
- <span data-ttu-id="37daf-223">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="37daf-223">PackageProjectUrl</span></span>
- <span data-ttu-id="37daf-224">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="37daf-224">PackageIconUrl</span></span>
- <span data-ttu-id="37daf-225">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="37daf-225">PackageReleaseNotes</span></span>
- <span data-ttu-id="37daf-226">PackageTags</span><span class="sxs-lookup"><span data-stu-id="37daf-226">PackageTags</span></span>
- <span data-ttu-id="37daf-227">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="37daf-227">PackageOutputPath</span></span>
- <span data-ttu-id="37daf-228">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="37daf-228">IncludeSymbols</span></span>
- <span data-ttu-id="37daf-229">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="37daf-229">IncludeSource</span></span>
- <span data-ttu-id="37daf-230">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="37daf-230">PackageTypes</span></span>
- <span data-ttu-id="37daf-231">IsTool</span><span class="sxs-lookup"><span data-stu-id="37daf-231">IsTool</span></span>
- <span data-ttu-id="37daf-232">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="37daf-232">RepositoryUrl</span></span>
- <span data-ttu-id="37daf-233">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="37daf-233">RepositoryType</span></span>
- <span data-ttu-id="37daf-234">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="37daf-234">RepositoryBranch</span></span>
- <span data-ttu-id="37daf-235">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="37daf-235">RepositoryCommit</span></span>
- <span data-ttu-id="37daf-236">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="37daf-236">NoPackageAnalysis</span></span>
- <span data-ttu-id="37daf-237">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="37daf-237">MinClientVersion</span></span>
- <span data-ttu-id="37daf-238">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="37daf-238">IncludeBuildOutput</span></span>
- <span data-ttu-id="37daf-239">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="37daf-239">IncludeContentInPack</span></span>
- <span data-ttu-id="37daf-240">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="37daf-240">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="37daf-241">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="37daf-241">ContentTargetFolders</span></span>
- <span data-ttu-id="37daf-242">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="37daf-242">NuspecFile</span></span>
- <span data-ttu-id="37daf-243">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="37daf-243">NuspecBasePath</span></span>
- <span data-ttu-id="37daf-244">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="37daf-244">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="37daf-245">pack scenarios</span><span class="sxs-lookup"><span data-stu-id="37daf-245">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="37daf-246">Suprimir as dependências</span><span class="sxs-lookup"><span data-stu-id="37daf-246">Suppress dependencies</span></span>

<span data-ttu-id="37daf-247">Para suprimir as dependências do pacote do pacote do NuGet gerado, defina `SuppressDependenciesWhenPacking` para `true` que permitirá ignorando todas as dependências de arquivo nupkg gerado.</span><span class="sxs-lookup"><span data-stu-id="37daf-247">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="37daf-248">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="37daf-248">PackageIconUrl</span></span>

<span data-ttu-id="37daf-249">Como parte da alteração para [NuGet problema 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` eventualmente será alterado para `PackageIconUri` e pode ser um caminho relativo para um arquivo de ícone que será incluído na raiz do pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="37daf-249">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="37daf-250">Assemblies de saída</span><span class="sxs-lookup"><span data-stu-id="37daf-250">Output assemblies</span></span>

<span data-ttu-id="37daf-251">O `nuget pack` copia arquivos de saída com extensões `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="37daf-251">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="37daf-252">Os arquivos de saída que são copiados dependem do que o MSBuild fornece do destino `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="37daf-252">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="37daf-253">Há duas propriedades de MSBuild que você pode usar em seu arquivo de projeto ou a linha de comando para controlar onde ficam os assemblies de saída:</span><span class="sxs-lookup"><span data-stu-id="37daf-253">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="37daf-254">`IncludeBuildOutput`: Um booliano que determina se os assemblies de saída de compilação devem ser incluídos no pacote.</span><span class="sxs-lookup"><span data-stu-id="37daf-254">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="37daf-255">`BuildOutputTargetFolder`: Especifica a pasta na qual os assemblies de saída devem ser colocados.</span><span class="sxs-lookup"><span data-stu-id="37daf-255">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="37daf-256">Os assemblies de saída (e outros arquivos de saída) são copiados para suas respectivas pastas de estrutura.</span><span class="sxs-lookup"><span data-stu-id="37daf-256">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="37daf-257">Referências de pacote</span><span class="sxs-lookup"><span data-stu-id="37daf-257">Package references</span></span>

<span data-ttu-id="37daf-258">Consulte [Referências de pacote em arquivos de projeto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="37daf-258">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="37daf-259">Referências de projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="37daf-259">Project to project references</span></span>

<span data-ttu-id="37daf-260">As referências projeto a projeto são consideradas como referências de pacote do nuget por padrão, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="37daf-260">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="37daf-261">Você também pode adicionar os seguintes metadados à referência de projeto:</span><span class="sxs-lookup"><span data-stu-id="37daf-261">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="37daf-262">Incluindo o conteúdo em um pacote</span><span class="sxs-lookup"><span data-stu-id="37daf-262">Including content in a package</span></span>

<span data-ttu-id="37daf-263">Para incluir o conteúdo, adicione metadados extras ao item `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="37daf-263">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="37daf-264">Por padrão, tudo que pertencer ao tipo “Conteúdo” é incluído no pacote, a menos que seja substituído por entradas como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="37daf-264">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="37daf-265">Por padrão, tudo é adicionado à raiz da pasta `content` e `contentFiles\any\<target_framework>` dentro de um pacote e preserva a estrutura e pasta relativa, a menos que você especifique um caminho de pacote:</span><span class="sxs-lookup"><span data-stu-id="37daf-265">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="37daf-266">Se você quiser copiar todo o conteúdo somente para determinadas pastas raiz (em vez de para `content` e `contentFiles`), será possível usar a propriedade `ContentTargetFolders` do MSBuild, que assume como padrão "content;contentFiles", mas pode ser definida como qualquer outro nome de pasta.</span><span class="sxs-lookup"><span data-stu-id="37daf-266">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="37daf-267">Observe que só especificar “contentFiles” em `ContentTargetFolders` coloca os arquivos em `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` com base em `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="37daf-267">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="37daf-268">`PackagePath` pode ser um conjunto de caminhos de destino separados por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="37daf-268">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="37daf-269">Especificar um caminho de pacote vazio adicionaria o arquivo à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="37daf-269">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="37daf-270">Por exemplo, o seguinte adiciona `libuv.txt` a `content\myfiles`, `content\samples` e a raiz do pacote:</span><span class="sxs-lookup"><span data-stu-id="37daf-270">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="37daf-271">Há também uma propriedade de MSBuild `$(IncludeContentInPack)`, que assume o padrão `true`.</span><span class="sxs-lookup"><span data-stu-id="37daf-271">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="37daf-272">Se isso for definido como `false` em qualquer projeto, o conteúdo desse projeto não está incluso no pacote do nuget.</span><span class="sxs-lookup"><span data-stu-id="37daf-272">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="37daf-273">Outros metadados específicos do pacote que pode ser definido em qualquer um dos itens acima ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, que define os valores ```CopyToOutput``` e ```Flatten``` na entrada ```contentFiles``` no nuspec de saída.</span><span class="sxs-lookup"><span data-stu-id="37daf-273">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="37daf-274">Além de itens de Conteúdo, os metadados `<Pack>` e `<PackagePath>` também podem ser definidos em arquivos com uma ação de Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.</span><span class="sxs-lookup"><span data-stu-id="37daf-274">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="37daf-275">Para o pacote acrescentar o nome de arquivo ao caminho do pacote ao usar padrões glob, seu caminho de pacote deve terminar com o caractere separador de pasta, caso contrário, o caminho do pacote será tratado como o caminho completo, incluindo o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="37daf-275">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="37daf-276">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="37daf-276">IncludeSymbols</span></span>

<span data-ttu-id="37daf-277">Ao usar o `MSBuild -t:pack -p:IncludeSymbols=true`, os arquivos `.pdb` correspondentes são copiados junto com outros arquivos de saída (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="37daf-277">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="37daf-278">Observe que a configuração `IncludeSymbols=true` cria um pacote regular *e* um pacote de símbolos.</span><span class="sxs-lookup"><span data-stu-id="37daf-278">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="37daf-279">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="37daf-279">IncludeSource</span></span>

<span data-ttu-id="37daf-280">Isso é o mesmo que `IncludeSymbols`, exceto que também copia os arquivos de origem com arquivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="37daf-280">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="37daf-281">Todos os arquivos do tipo `Compile` são copiadas para `src\<ProjectName>\`, preservando a estrutura de pastas do caminho relativo no pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="37daf-281">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="37daf-282">O mesmo também ocorre para arquivos de origem de qualquer `ProjectReference` que tem `TreatAsPackageReference` definido como `false`.</span><span class="sxs-lookup"><span data-stu-id="37daf-282">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="37daf-283">Se um arquivo do tipo Compilação estiver fora da pasta de projeto, ele será adicionado apenas a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="37daf-283">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="37daf-284">Uma expressão de licença ou um arquivo de licença de remessa</span><span class="sxs-lookup"><span data-stu-id="37daf-284">Packing a license expression or a license file</span></span>

<span data-ttu-id="37daf-285">Ao usar uma expressão de licença, a propriedade PackageLicenseExpression deve ser usada.</span><span class="sxs-lookup"><span data-stu-id="37daf-285">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="37daf-286">[Exemplo de expressão de licença](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="37daf-286">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="37daf-287">[Saiba mais sobre expressões de licença e licenças que são aceitos pelo NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="37daf-287">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="37daf-288">Ao empacotar um arquivo de licença, você precisa usar a propriedade PackageLicenseFile para especificar o caminho do pacote, relativo à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="37daf-288">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="37daf-289">Além disso, você precisa certificar-se de que o arquivo está incluído no pacote.</span><span class="sxs-lookup"><span data-stu-id="37daf-289">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="37daf-290">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="37daf-290">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="37daf-291">[Exemplo de arquivo de licença](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="37daf-291">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="37daf-292">IsTool</span><span class="sxs-lookup"><span data-stu-id="37daf-292">IsTool</span></span>

<span data-ttu-id="37daf-293">Ao usar `MSBuild -t:pack -p:IsTool=true`, todos os arquivos de saída, conforme especificado no cenário [Assemblies de saída](#output-assemblies), são copiados para a pasta `tools` em vez da pasta `lib`.</span><span class="sxs-lookup"><span data-stu-id="37daf-293">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="37daf-294">Observe que isso é diferente de um `DotNetCliTool` que é especificado pela configuração do `PackageType` no arquivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="37daf-294">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="37daf-295">Empacotamento usando um .nuspec</span><span class="sxs-lookup"><span data-stu-id="37daf-295">Packing using a .nuspec</span></span>

<span data-ttu-id="37daf-296">Você pode usar um `.nuspec` arquivo para empacotar seu projeto desde que você tenha um arquivo de projeto do SDK para importar `NuGet.Build.Tasks.Pack.targets` para que a tarefa de pacote pode ser executada.</span><span class="sxs-lookup"><span data-stu-id="37daf-296">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="37daf-297">Você ainda precisará restaurar o projeto antes que você pode empacotar um arquivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="37daf-297">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="37daf-298">A estrutura de destino do arquivo de projeto é irrelevante e não usados ao empacotar um nuspec.</span><span class="sxs-lookup"><span data-stu-id="37daf-298">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="37daf-299">As três propriedades MSBuild a seguir são relevantes para empacotamento usando um `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="37daf-299">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="37daf-300">`NuspecFile`: caminho relativo ou absoluto para o arquivo `.nuspec` que está sendo usado para o empacotamento.</span><span class="sxs-lookup"><span data-stu-id="37daf-300">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="37daf-301">`NuspecProperties`: uma lista separada por ponto e vírgula de pares chave/valor.</span><span class="sxs-lookup"><span data-stu-id="37daf-301">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="37daf-302">Devido à maneira como a análise de linha de comando do MSBuild funciona, várias propriedades precisam ser especificadas da seguinte maneira: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="37daf-302">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="37daf-303">`NuspecBasePath`: Caminho base para o `.nuspec` arquivo.</span><span class="sxs-lookup"><span data-stu-id="37daf-303">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="37daf-304">Se estiver usando `dotnet.exe` para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="37daf-304">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="37daf-305">Se estiver usando o MSBuild para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="37daf-305">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="37daf-306">Observe que um nuspec de remessa usando dotnet.exe ou msbuild também leva para compilar o projeto por padrão.</span><span class="sxs-lookup"><span data-stu-id="37daf-306">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="37daf-307">Isso pode ser evitado, passando ```--no-build``` dotnet.exe, que é o equivalente da configuração de propriedade ```<NoBuild>true</NoBuild> ``` em seu arquivo de projeto, juntamente com a configuração ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` no arquivo de projeto</span><span class="sxs-lookup"><span data-stu-id="37daf-307">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="37daf-308">Um exemplo de um arquivo csproj para empacotar um arquivo nuspec é:</span><span class="sxs-lookup"><span data-stu-id="37daf-308">An example of a csproj file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="37daf-309">Advanced pontos de extensão para criar pacote personalizado</span><span class="sxs-lookup"><span data-stu-id="37daf-309">Advanced extension points to create customized package</span></span>

<span data-ttu-id="37daf-310">O `pack` destino fornece dois pontos de extensão que são executados na interna, target framework compilação específica.</span><span class="sxs-lookup"><span data-stu-id="37daf-310">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="37daf-311">Suportam os pontos de extensão incluindo conteúdo específico do framework de destino e assemblies em um pacote:</span><span class="sxs-lookup"><span data-stu-id="37daf-311">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="37daf-312">`TargetsForTfmSpecificBuildOutput` destino: Use arquivos de dentro de `lib` pasta ou uma pasta especificada usando `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="37daf-312">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="37daf-313">`TargetsForTfmSpecificContentInPackage` destino: Use para arquivos fora do `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="37daf-313">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="37daf-314">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="37daf-314">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="37daf-315">Escrever um destino personalizado e especificá-lo como o valor da `$(TargetsForTfmSpecificBuildOutput)` propriedade.</span><span class="sxs-lookup"><span data-stu-id="37daf-315">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="37daf-316">Para todos os arquivos que precisam ir para o `BuildOutputTargetFolder` lib (por padrão), o destino deve gravar esses arquivos no ItemGroup `BuildOutputInPackage` e defina os seguintes dois valores de metadados:</span><span class="sxs-lookup"><span data-stu-id="37daf-316">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="37daf-317">`FinalOutputPath`: O caminho absoluto do arquivo. Se não for fornecido, a identidade é usada para avaliar o caminho de origem.</span><span class="sxs-lookup"><span data-stu-id="37daf-317">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="37daf-318">`TargetPath`:  (Opcional) Definido quando o arquivo deve ir para uma subpasta dentro do `lib\<TargetFramework>` , como assemblies de satélite que vão em suas pastas de cultura respectivo.</span><span class="sxs-lookup"><span data-stu-id="37daf-318">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="37daf-319">O padrão é o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="37daf-319">Defaults to the name of the file.</span></span>

<span data-ttu-id="37daf-320">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="37daf-320">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="37daf-321">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="37daf-321">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="37daf-322">Escrever um destino personalizado e especificá-lo como o valor da `$(TargetsForTfmSpecificContentInPackage)` propriedade.</span><span class="sxs-lookup"><span data-stu-id="37daf-322">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="37daf-323">Para todos os arquivos incluir no pacote, o destino deve gravar esses arquivos no ItemGroup `TfmSpecificPackageFile` e defina os seguintes metadados opcionais:</span><span class="sxs-lookup"><span data-stu-id="37daf-323">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="37daf-324">`PackagePath`: Caminho onde o arquivo deve ser gerado no pacote.</span><span class="sxs-lookup"><span data-stu-id="37daf-324">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="37daf-325">O NuGet emitirá um aviso se mais de um arquivo for adicionado no mesmo caminho de pacote.</span><span class="sxs-lookup"><span data-stu-id="37daf-325">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="37daf-326">`BuildAction`: A ação de compilação a ser atribuído ao arquivo, é necessário somente se o caminho do pacote está no `contentFiles` pasta.</span><span class="sxs-lookup"><span data-stu-id="37daf-326">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="37daf-327">O padrão é "None".</span><span class="sxs-lookup"><span data-stu-id="37daf-327">Defaults to "None".</span></span>

<span data-ttu-id="37daf-328">Um exemplo:</span><span class="sxs-lookup"><span data-stu-id="37daf-328">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="37daf-329">restore target</span><span class="sxs-lookup"><span data-stu-id="37daf-329">restore target</span></span>

<span data-ttu-id="37daf-330">`MSBuild -t:restore` (que `nuget restore` e `dotnet restore` usam com projetos do .NET Core), restaura pacotes referenciados no arquivo de projeto da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="37daf-330">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="37daf-331">Ler todas as referências projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="37daf-331">Read all project to project references</span></span>
1. <span data-ttu-id="37daf-332">Ler as propriedades do projeto para localizar a pasta intermediária e as estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="37daf-332">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="37daf-333">Passar dados do msbuild para NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="37daf-333">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="37daf-334">Executar restauração</span><span class="sxs-lookup"><span data-stu-id="37daf-334">Run restore</span></span>
1. <span data-ttu-id="37daf-335">Baixar os pacotes</span><span class="sxs-lookup"><span data-stu-id="37daf-335">Download packages</span></span>
1. <span data-ttu-id="37daf-336">Gravar arquivo de ativos, destinos e objetos</span><span class="sxs-lookup"><span data-stu-id="37daf-336">Write assets file, targets, and props</span></span>

<span data-ttu-id="37daf-337">O `restore` destino works **somente** para projetos que usam o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="37daf-337">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="37daf-338">Ele faz **não** funcionam para projetos que usam o `packages.config` formato; use [restauração do nuget](../tools/cli-ref-restore.md) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="37daf-338">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="37daf-339">Restaurar propriedades</span><span class="sxs-lookup"><span data-stu-id="37daf-339">Restore properties</span></span>

<span data-ttu-id="37daf-340">Configurações de restauração adicionais podem vir de propriedades MSBuild no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="37daf-340">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="37daf-341">Os valores também podem ser definidos na linha de comando usando a opção `-p:` (consulte os Exemplos abaixo).</span><span class="sxs-lookup"><span data-stu-id="37daf-341">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="37daf-342">Propriedade</span><span class="sxs-lookup"><span data-stu-id="37daf-342">Property</span></span> | <span data-ttu-id="37daf-343">Descrição</span><span class="sxs-lookup"><span data-stu-id="37daf-343">Description</span></span> |
|--------|--------|
| <span data-ttu-id="37daf-344">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="37daf-344">RestoreSources</span></span> | <span data-ttu-id="37daf-345">Uma lista delimitada por ponto e vírgula de origens de pacote.</span><span class="sxs-lookup"><span data-stu-id="37daf-345">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="37daf-346">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="37daf-346">RestorePackagesPath</span></span> | <span data-ttu-id="37daf-347">Caminho da pasta dos pacotes do usuário.</span><span class="sxs-lookup"><span data-stu-id="37daf-347">User packages folder path.</span></span> |
| <span data-ttu-id="37daf-348">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="37daf-348">RestoreDisableParallel</span></span> | <span data-ttu-id="37daf-349">Limite os downloads para um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="37daf-349">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="37daf-350">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="37daf-350">RestoreConfigFile</span></span> | <span data-ttu-id="37daf-351">Caminho para um arquivo `Nuget.Config` a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="37daf-351">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="37daf-352">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="37daf-352">RestoreNoCache</span></span> | <span data-ttu-id="37daf-353">Se verdadeiro, evita o uso de pacotes armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="37daf-353">If true, avoids using cached packages.</span></span> <span data-ttu-id="37daf-354">Ver [gerenciar as pastas de cache e de pacotes globais](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="37daf-354">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="37daf-355">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="37daf-355">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="37daf-356">Se verdadeiro, ignora origens de pacote com falha ou ausentes.</span><span class="sxs-lookup"><span data-stu-id="37daf-356">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="37daf-357">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="37daf-357">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="37daf-358">Caminho para `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="37daf-358">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="37daf-359">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="37daf-359">RestoreGraphProjectInput</span></span> | <span data-ttu-id="37daf-360">Lista separada por ponto e vírgula de projetos a serem restaurados, que devem conter caminhos absolutos.</span><span class="sxs-lookup"><span data-stu-id="37daf-360">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="37daf-361">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="37daf-361">RestoreOutputPath</span></span> | <span data-ttu-id="37daf-362">Pasta de saída que usa a pasta `obj` como padrão.</span><span class="sxs-lookup"><span data-stu-id="37daf-362">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="37daf-363">Exemplos</span><span class="sxs-lookup"><span data-stu-id="37daf-363">Examples</span></span>

<span data-ttu-id="37daf-364">Linha de comando:</span><span class="sxs-lookup"><span data-stu-id="37daf-364">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="37daf-365">Arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="37daf-365">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="37daf-366">Restaurar saídas</span><span class="sxs-lookup"><span data-stu-id="37daf-366">Restore outputs</span></span>

<span data-ttu-id="37daf-367">A restauração cria os seguintes arquivos na pasta `obj` de build:</span><span class="sxs-lookup"><span data-stu-id="37daf-367">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="37daf-368">Arquivo</span><span class="sxs-lookup"><span data-stu-id="37daf-368">File</span></span> | <span data-ttu-id="37daf-369">Descrição</span><span class="sxs-lookup"><span data-stu-id="37daf-369">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="37daf-370">Contém o grafo de dependência de todas as referências de pacote.</span><span class="sxs-lookup"><span data-stu-id="37daf-370">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="37daf-371">Referências a objetos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="37daf-371">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="37daf-372">Referências a destinos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="37daf-372">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="37daf-373">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="37daf-373">PackageTargetFallback</span></span>

<span data-ttu-id="37daf-374">O elemento `PackageTargetFallback` permite especificar um conjunto de destinos compatíveis a serem usados ao restaurar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="37daf-374">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="37daf-375">Ele foi desenvolvido para permitir que os pacotes que usam o dotnet [TxM](../reference/target-frameworks.md) funcionem com pacotes compatíveis que não declaram um dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="37daf-375">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="37daf-376">Ou seja, se o projeto usar o dotnet TxM, todos os pacotes dos quais ele depende também deverão ter um dotnet TxM, a menos que você adicione o `<PackageTargetFallback>` ao projeto para permitir que plataformas não dotnet sejam compatíveis com o dotnet.</span><span class="sxs-lookup"><span data-stu-id="37daf-376">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="37daf-377">Por exemplo, se o projeto está usando o `netstandard1.6` TxM e um pacote dependente contém apenas `lib/net45/a.dll` e `lib/portable-net45+win81/a.dll`, o projeto não será compilado.</span><span class="sxs-lookup"><span data-stu-id="37daf-377">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="37daf-378">Se a DLL que você deseja colocar é esta última, é possível adicionar um `PackageTargetFallback` como mostrado a seguir para dizer que a DLL `portable-net45+win81` é compatível:</span><span class="sxs-lookup"><span data-stu-id="37daf-378">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="37daf-379">Para declarar um fallback para todos os destinos em seu projeto, deixe o atributo `Condition` de fora.</span><span class="sxs-lookup"><span data-stu-id="37daf-379">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="37daf-380">Você também pode estender qualquer `PackageTargetFallback` existente incluindo `$(PackageTargetFallback)` conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="37daf-380">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="37daf-381">Substituindo uma biblioteca de um grafo de restauração</span><span class="sxs-lookup"><span data-stu-id="37daf-381">Replacing one library from a restore graph</span></span>

<span data-ttu-id="37daf-382">Se uma restauração está trazendo o assembly errado, é possível excluir a escolha padrão do pacote e substituí-lo por outro de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="37daf-382">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="37daf-383">Primeiro com um `PackageReference` de nível superior, exclua todos os ativos:</span><span class="sxs-lookup"><span data-stu-id="37daf-383">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="37daf-384">Em seguida, adicione sua própria referência à cópia local apropriada da DLL:</span><span class="sxs-lookup"><span data-stu-id="37daf-384">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
