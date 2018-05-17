---
title: Empacotamento e restauração do NuGet como destinos do MSBuild
description: O pack e restore do NuGet podem funcionar diretamente como destinos do MSBuild com o NuGet 4.0 e superior.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 00d763bcfdd2f3db50378a1e7774eae7a2e1fcd1
ms.sourcegitcommit: 00c4c809c69c16fcf4d81012eb53ea22f0691d0b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="0ee1b-103">Empacotamento e restauração do NuGet como destinos do MSBuild</span><span class="sxs-lookup"><span data-stu-id="0ee1b-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="0ee1b-104">*NuGet 4.0 ou superior*</span><span class="sxs-lookup"><span data-stu-id="0ee1b-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="0ee1b-105">Com o formato PackageReference, o NuGet 4.0 e posterior pode armazenar todos os metadados de manifesto diretamente dentro de um arquivo de projeto em vez de usar um arquivo `.nuspec` separado.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="0ee1b-106">Com o MSBuild 15.1 ou superior, o NuGet também é um cidadão de primeira classe do MSBuild com os destinos `pack` e `restore`, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="0ee1b-107">Esses destinos permitem que você trabalhe com o NuGet como faria com qualquer outra tarefa ou destino do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="0ee1b-108">(Para NuGet 3.x e anteriores, use os comandos [pack](../tools/cli-ref-pack.md) e [restore](../tools/cli-ref-restore.md) na CLI do NuGet.)</span><span class="sxs-lookup"><span data-stu-id="0ee1b-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="0ee1b-109">Ordem de build de destino</span><span class="sxs-lookup"><span data-stu-id="0ee1b-109">Target build order</span></span>

<span data-ttu-id="0ee1b-110">Como `pack` e `restore` são os destinos do MSBuild, você pode acessá-los para melhorar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="0ee1b-111">Por exemplo, digamos que você deseja copiar o pacote para um compartilhamento de rede após empacotá-lo.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="0ee1b-112">Você pode fazer isso adicionando o seguinte ao seu arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="0ee1b-113">Da mesma forma, você pode gravar uma tarefa do MSBuild, escrever seu próprio destino e consumir propriedades do NuGet na tarefa de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="0ee1b-114">pack target</span><span class="sxs-lookup"><span data-stu-id="0ee1b-114">pack target</span></span>

<span data-ttu-id="0ee1b-115">Para projetos padrão do .NET usando o formato PackageReference, usando `msbuild /t:pack` desenha entradas do arquivo de projeto para usar na criação de um pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-115">For .NET Standard projects using the PackageReference format, using `msbuild /t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="0ee1b-116">A tabela abaixo descreve as propriedades do MSBuild que podem ser adicionadas a um arquivo do projeto dentro do primeiro nó `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="0ee1b-117">Você pode fazer essas edições facilmente no Visual Studio 2017 e posterior clicando com o botão direito do mouse no projeto e selecionando **Editar {project_name}** no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="0ee1b-118">Para sua conveniência, a tabela é organizada pela propriedade equivalente em um arquivo [`.nuspec` ](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="0ee1b-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="0ee1b-119">Observe que as propriedades `Owners` e `Summary` de `.nuspec` não são compatíveis com o MSBuild.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="0ee1b-120">Valor de atributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="0ee1b-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="0ee1b-121">Propriedade do MSBuild</span><span class="sxs-lookup"><span data-stu-id="0ee1b-121">MSBuild Property</span></span> | <span data-ttu-id="0ee1b-122">Padrão</span><span class="sxs-lookup"><span data-stu-id="0ee1b-122">Default</span></span> | <span data-ttu-id="0ee1b-123">Observações</span><span class="sxs-lookup"><span data-stu-id="0ee1b-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="0ee1b-124">Id</span><span class="sxs-lookup"><span data-stu-id="0ee1b-124">Id</span></span> | <span data-ttu-id="0ee1b-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="0ee1b-125">PackageId</span></span> | <span data-ttu-id="0ee1b-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="0ee1b-126">AssemblyName</span></span> | <span data-ttu-id="0ee1b-127">$(AssemblyName) do MSBuild</span><span class="sxs-lookup"><span data-stu-id="0ee1b-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="0ee1b-128">Versão</span><span class="sxs-lookup"><span data-stu-id="0ee1b-128">Version</span></span> | <span data-ttu-id="0ee1b-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="0ee1b-129">PackageVersion</span></span> | <span data-ttu-id="0ee1b-130">Versão</span><span class="sxs-lookup"><span data-stu-id="0ee1b-130">Version</span></span> | <span data-ttu-id="0ee1b-131">Isso é compatível com semver, por exemplo “1.0.0”, “1.0.0-beta” ou “1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="0ee1b-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="0ee1b-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="0ee1b-132">VersionPrefix</span></span> | <span data-ttu-id="0ee1b-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="0ee1b-133">PackageVersionPrefix</span></span> | <span data-ttu-id="0ee1b-134">empty</span><span class="sxs-lookup"><span data-stu-id="0ee1b-134">empty</span></span> | <span data-ttu-id="0ee1b-135">A configuração PackageVersion substitui PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="0ee1b-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="0ee1b-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="0ee1b-136">VersionSuffix</span></span> | <span data-ttu-id="0ee1b-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="0ee1b-137">PackageVersionSuffix</span></span> | <span data-ttu-id="0ee1b-138">empty</span><span class="sxs-lookup"><span data-stu-id="0ee1b-138">empty</span></span> | <span data-ttu-id="0ee1b-139">$(VersionSuffix) do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="0ee1b-140">A configuração PackageVersion substitui PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="0ee1b-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="0ee1b-141">Autores</span><span class="sxs-lookup"><span data-stu-id="0ee1b-141">Authors</span></span> | <span data-ttu-id="0ee1b-142">Autores</span><span class="sxs-lookup"><span data-stu-id="0ee1b-142">Authors</span></span> | <span data-ttu-id="0ee1b-143">Nome do usuário atual</span><span class="sxs-lookup"><span data-stu-id="0ee1b-143">Username of the current user</span></span> | |
| <span data-ttu-id="0ee1b-144">Proprietários</span><span class="sxs-lookup"><span data-stu-id="0ee1b-144">Owners</span></span> | <span data-ttu-id="0ee1b-145">N/D</span><span class="sxs-lookup"><span data-stu-id="0ee1b-145">N/A</span></span> | <span data-ttu-id="0ee1b-146">Não está presente no NuSpec</span><span class="sxs-lookup"><span data-stu-id="0ee1b-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="0ee1b-147">Título</span><span class="sxs-lookup"><span data-stu-id="0ee1b-147">Title</span></span> | <span data-ttu-id="0ee1b-148">Título</span><span class="sxs-lookup"><span data-stu-id="0ee1b-148">Title</span></span> | <span data-ttu-id="0ee1b-149">O PackageId</span><span class="sxs-lookup"><span data-stu-id="0ee1b-149">The PackageId</span></span>| |
| <span data-ttu-id="0ee1b-150">Descrição</span><span class="sxs-lookup"><span data-stu-id="0ee1b-150">Description</span></span> | <span data-ttu-id="0ee1b-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="0ee1b-151">Description</span></span> | <span data-ttu-id="0ee1b-152">“Package Description”</span><span class="sxs-lookup"><span data-stu-id="0ee1b-152">"Package Description"</span></span> | |
| <span data-ttu-id="0ee1b-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="0ee1b-153">Copyright</span></span> | <span data-ttu-id="0ee1b-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="0ee1b-154">Copyright</span></span> | <span data-ttu-id="0ee1b-155">empty</span><span class="sxs-lookup"><span data-stu-id="0ee1b-155">empty</span></span> | |
| <span data-ttu-id="0ee1b-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="0ee1b-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="0ee1b-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="0ee1b-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="0ee1b-158">false</span><span class="sxs-lookup"><span data-stu-id="0ee1b-158">false</span></span> | |
| <span data-ttu-id="0ee1b-159">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="0ee1b-159">LicenseUrl</span></span> | <span data-ttu-id="0ee1b-160">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="0ee1b-160">PackageLicenseUrl</span></span> | <span data-ttu-id="0ee1b-161">empty</span><span class="sxs-lookup"><span data-stu-id="0ee1b-161">empty</span></span> | |
| <span data-ttu-id="0ee1b-162">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="0ee1b-162">ProjectUrl</span></span> | <span data-ttu-id="0ee1b-163">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="0ee1b-163">PackageProjectUrl</span></span> | <span data-ttu-id="0ee1b-164">empty</span><span class="sxs-lookup"><span data-stu-id="0ee1b-164">empty</span></span> | |
| <span data-ttu-id="0ee1b-165">IconUrl</span><span class="sxs-lookup"><span data-stu-id="0ee1b-165">IconUrl</span></span> | <span data-ttu-id="0ee1b-166">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="0ee1b-166">PackageIconUrl</span></span> | <span data-ttu-id="0ee1b-167">empty</span><span class="sxs-lookup"><span data-stu-id="0ee1b-167">empty</span></span> | |
| <span data-ttu-id="0ee1b-168">Marcas</span><span class="sxs-lookup"><span data-stu-id="0ee1b-168">Tags</span></span> | <span data-ttu-id="0ee1b-169">PackageTags</span><span class="sxs-lookup"><span data-stu-id="0ee1b-169">PackageTags</span></span> | <span data-ttu-id="0ee1b-170">empty</span><span class="sxs-lookup"><span data-stu-id="0ee1b-170">empty</span></span> | <span data-ttu-id="0ee1b-171">Marcas são delimitadas por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-171">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="0ee1b-172">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="0ee1b-172">ReleaseNotes</span></span> | <span data-ttu-id="0ee1b-173">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="0ee1b-173">PackageReleaseNotes</span></span> | <span data-ttu-id="0ee1b-174">empty</span><span class="sxs-lookup"><span data-stu-id="0ee1b-174">empty</span></span> | |
| <span data-ttu-id="0ee1b-175">Url do repositório</span><span class="sxs-lookup"><span data-stu-id="0ee1b-175">Repository/Url</span></span> | <span data-ttu-id="0ee1b-176">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="0ee1b-176">RepositoryUrl</span></span> | <span data-ttu-id="0ee1b-177">empty</span><span class="sxs-lookup"><span data-stu-id="0ee1b-177">empty</span></span> | <span data-ttu-id="0ee1b-178">URL do repositório usado para clonar ou recuperar o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-178">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="0ee1b-179">Exemplo: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="0ee1b-179">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="0ee1b-180">Tipo do repositório</span><span class="sxs-lookup"><span data-stu-id="0ee1b-180">Repository/Type</span></span> | <span data-ttu-id="0ee1b-181">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="0ee1b-181">RepositoryType</span></span> | <span data-ttu-id="0ee1b-182">empty</span><span class="sxs-lookup"><span data-stu-id="0ee1b-182">empty</span></span> | <span data-ttu-id="0ee1b-183">Tipo de repositório.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-183">Repository type.</span></span> <span data-ttu-id="0ee1b-184">Exemplos: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-184">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="0ee1b-185">Ramificação do repositório</span><span class="sxs-lookup"><span data-stu-id="0ee1b-185">Repository/Branch</span></span> | <span data-ttu-id="0ee1b-186">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="0ee1b-186">RepositoryBranch</span></span> | <span data-ttu-id="0ee1b-187">empty</span><span class="sxs-lookup"><span data-stu-id="0ee1b-187">empty</span></span> | <span data-ttu-id="0ee1b-188">Informações de ramificação do repositório opcional.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-188">Optional repository branch information.</span></span> <span data-ttu-id="0ee1b-189">*RepositoryUrl* também deve ser especificado para essa propriedade a ser incluído.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-189">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="0ee1b-190">Exemplo: *mestre* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="0ee1b-190">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="0ee1b-191">Repositório/confirmação</span><span class="sxs-lookup"><span data-stu-id="0ee1b-191">Repository/Commit</span></span> | <span data-ttu-id="0ee1b-192">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="0ee1b-192">RepositoryCommit</span></span> | <span data-ttu-id="0ee1b-193">empty</span><span class="sxs-lookup"><span data-stu-id="0ee1b-193">empty</span></span> | <span data-ttu-id="0ee1b-194">Confirmação de repositório opcional ou conjunto de alterações para indicar que o pacote de origem foi desenvolvido com.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-194">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="0ee1b-195">*RepositoryUrl* também deve ser especificado para essa propriedade a ser incluído.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-195">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="0ee1b-196">Exemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="0ee1b-196">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="0ee1b-197">PackageType</span><span class="sxs-lookup"><span data-stu-id="0ee1b-197">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="0ee1b-198">Resumo</span><span class="sxs-lookup"><span data-stu-id="0ee1b-198">Summary</span></span> | <span data-ttu-id="0ee1b-199">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="0ee1b-199">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="0ee1b-200">pack target inputs</span><span class="sxs-lookup"><span data-stu-id="0ee1b-200">pack target inputs</span></span>

- <span data-ttu-id="0ee1b-201">IsPackable</span><span class="sxs-lookup"><span data-stu-id="0ee1b-201">IsPackable</span></span>
- <span data-ttu-id="0ee1b-202">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="0ee1b-202">PackageVersion</span></span>
- <span data-ttu-id="0ee1b-203">PackageId</span><span class="sxs-lookup"><span data-stu-id="0ee1b-203">PackageId</span></span>
- <span data-ttu-id="0ee1b-204">Autores</span><span class="sxs-lookup"><span data-stu-id="0ee1b-204">Authors</span></span>
- <span data-ttu-id="0ee1b-205">Descrição</span><span class="sxs-lookup"><span data-stu-id="0ee1b-205">Description</span></span>
- <span data-ttu-id="0ee1b-206">Copyright</span><span class="sxs-lookup"><span data-stu-id="0ee1b-206">Copyright</span></span>
- <span data-ttu-id="0ee1b-207">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="0ee1b-207">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="0ee1b-208">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="0ee1b-208">DevelopmentDependency</span></span>
- <span data-ttu-id="0ee1b-209">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="0ee1b-209">PackageLicenseUrl</span></span>
- <span data-ttu-id="0ee1b-210">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="0ee1b-210">PackageProjectUrl</span></span>
- <span data-ttu-id="0ee1b-211">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="0ee1b-211">PackageIconUrl</span></span>
- <span data-ttu-id="0ee1b-212">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="0ee1b-212">PackageReleaseNotes</span></span>
- <span data-ttu-id="0ee1b-213">PackageTags</span><span class="sxs-lookup"><span data-stu-id="0ee1b-213">PackageTags</span></span>
- <span data-ttu-id="0ee1b-214">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="0ee1b-214">PackageOutputPath</span></span>
- <span data-ttu-id="0ee1b-215">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="0ee1b-215">IncludeSymbols</span></span>
- <span data-ttu-id="0ee1b-216">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="0ee1b-216">IncludeSource</span></span>
- <span data-ttu-id="0ee1b-217">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="0ee1b-217">PackageTypes</span></span>
- <span data-ttu-id="0ee1b-218">IsTool</span><span class="sxs-lookup"><span data-stu-id="0ee1b-218">IsTool</span></span>
- <span data-ttu-id="0ee1b-219">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="0ee1b-219">RepositoryUrl</span></span>
- <span data-ttu-id="0ee1b-220">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="0ee1b-220">RepositoryType</span></span>
- <span data-ttu-id="0ee1b-221">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="0ee1b-221">RepositoryBranch</span></span>
- <span data-ttu-id="0ee1b-222">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="0ee1b-222">RepositoryCommit</span></span>
- <span data-ttu-id="0ee1b-223">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="0ee1b-223">NoPackageAnalysis</span></span>
- <span data-ttu-id="0ee1b-224">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="0ee1b-224">MinClientVersion</span></span>
- <span data-ttu-id="0ee1b-225">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="0ee1b-225">IncludeBuildOutput</span></span>
- <span data-ttu-id="0ee1b-226">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="0ee1b-226">IncludeContentInPack</span></span>
- <span data-ttu-id="0ee1b-227">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="0ee1b-227">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="0ee1b-228">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="0ee1b-228">ContentTargetFolders</span></span>
- <span data-ttu-id="0ee1b-229">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="0ee1b-229">NuspecFile</span></span>
- <span data-ttu-id="0ee1b-230">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="0ee1b-230">NuspecBasePath</span></span>
- <span data-ttu-id="0ee1b-231">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="0ee1b-231">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="0ee1b-232">pack scenarios</span><span class="sxs-lookup"><span data-stu-id="0ee1b-232">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="0ee1b-233">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="0ee1b-233">PackageIconUrl</span></span>

<span data-ttu-id="0ee1b-234">Como parte da alteração de [NuGet problema 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` eventualmente será alterado para `PackageIconUri` e pode ser um caminho relativo para um arquivo de ícone que será incluído na raiz do pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-234">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="0ee1b-235">Assemblies de saída</span><span class="sxs-lookup"><span data-stu-id="0ee1b-235">Output assemblies</span></span>

<span data-ttu-id="0ee1b-236">O `nuget pack` copia arquivos de saída com extensões `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-236">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="0ee1b-237">Os arquivos de saída que são copiados dependem do que o MSBuild fornece do destino `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-237">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="0ee1b-238">Há duas propriedades de MSBuild que você pode usar em seu arquivo de projeto ou a linha de comando para controlar onde ficam os assemblies de saída:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-238">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="0ee1b-239">`IncludeBuildOutput`: um valor booliano que determina se os assemblies de saída de build devem ser incluídos no pacote.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-239">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="0ee1b-240">`BuildOutputTargetFolder`: especifica a pasta na qual os assemblies de saída devem ser colocados.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-240">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="0ee1b-241">Os assemblies de saída (e outros arquivos de saída) são copiados para suas respectivas pastas de estrutura.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-241">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="0ee1b-242">Referências de pacote</span><span class="sxs-lookup"><span data-stu-id="0ee1b-242">Package references</span></span>

<span data-ttu-id="0ee1b-243">Consulte [Referências de pacote em arquivos de projeto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="0ee1b-243">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="0ee1b-244">Referências de projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="0ee1b-244">Project to project references</span></span>

<span data-ttu-id="0ee1b-245">As referências projeto a projeto são consideradas como referências de pacote do nuget por padrão, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-245">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="0ee1b-246">Você também pode adicionar os seguintes metadados à referência de projeto:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-246">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="0ee1b-247">Incluindo o conteúdo em um pacote</span><span class="sxs-lookup"><span data-stu-id="0ee1b-247">Including content in a package</span></span>

<span data-ttu-id="0ee1b-248">Para incluir o conteúdo, adicione metadados extras ao item `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-248">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="0ee1b-249">Por padrão, tudo que pertencer ao tipo “Conteúdo” é incluído no pacote, a menos que seja substituído por entradas como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-249">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="0ee1b-250">Por padrão, tudo é adicionado à raiz da pasta `content` e `contentFiles\any\<target_framework>` dentro de um pacote e preserva a estrutura e pasta relativa, a menos que você especifique um caminho de pacote:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-250">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="0ee1b-251">Se você quiser copiar todo o conteúdo somente para determinadas pastas raiz (em vez de para `content` e `contentFiles`), será possível usar a propriedade `ContentTargetFolders` do MSBuild, que assume como padrão "content;contentFiles", mas pode ser definida como qualquer outro nome de pasta.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-251">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="0ee1b-252">Observe que só especificar “contentFiles” em `ContentTargetFolders` coloca os arquivos em `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` com base em `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-252">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="0ee1b-253">`PackagePath` pode ser um conjunto de caminhos de destino separados por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-253">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="0ee1b-254">Especificar um caminho de pacote vazio adicionaria o arquivo à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-254">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="0ee1b-255">Por exemplo, o seguinte adiciona `libuv.txt` a `content\myfiles`, `content\samples` e a raiz do pacote:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-255">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="0ee1b-256">Há também uma propriedade de MSBuild `$(IncludeContentInPack)`, que assume o padrão `true`.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-256">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="0ee1b-257">Se isso for definido como `false` em qualquer projeto, o conteúdo desse projeto não está incluso no pacote do nuget.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-257">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="0ee1b-258">Outros metadados específicos do pacote que pode ser definido em qualquer um dos itens acima ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, que define os valores ```CopyToOutput``` e ```Flatten``` na entrada ```contentFiles``` no nuspec de saída.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-258">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="0ee1b-259">Além de itens de Conteúdo, os metadados `<Pack>` e `<PackagePath>` também podem ser definidos em arquivos com uma ação de Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-259">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="0ee1b-260">Para o pacote acrescentar o nome de arquivo ao caminho do pacote ao usar padrões glob, seu caminho de pacote deve terminar com o caractere separador de pasta, caso contrário, o caminho do pacote será tratado como o caminho completo, incluindo o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-260">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="0ee1b-261">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="0ee1b-261">IncludeSymbols</span></span>

<span data-ttu-id="0ee1b-262">Ao usar o `MSBuild /t:pack /p:IncludeSymbols=true`, os arquivos `.pdb` correspondentes são copiados junto com outros arquivos de saída (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="0ee1b-262">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="0ee1b-263">Observe que a configuração `IncludeSymbols=true` cria um pacote regular *e* um pacote de símbolos.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-263">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="0ee1b-264">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="0ee1b-264">IncludeSource</span></span>

<span data-ttu-id="0ee1b-265">Isso é o mesmo que `IncludeSymbols`, exceto que também copia os arquivos de origem com arquivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-265">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="0ee1b-266">Todos os arquivos do tipo `Compile` são copiadas para `src\<ProjectName>\`, preservando a estrutura de pastas do caminho relativo no pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-266">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="0ee1b-267">O mesmo também ocorre para arquivos de origem de qualquer `ProjectReference` que tem `TreatAsPackageReference` definido como `false`.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-267">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="0ee1b-268">Se um arquivo do tipo Compilação estiver fora da pasta de projeto, ele será adicionado apenas a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-268">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="0ee1b-269">IsTool</span><span class="sxs-lookup"><span data-stu-id="0ee1b-269">IsTool</span></span>

<span data-ttu-id="0ee1b-270">Ao usar `MSBuild /t:pack /p:IsTool=true`, todos os arquivos de saída, conforme especificado no cenário [Assemblies de saída](#output-assemblies), são copiados para a pasta `tools` em vez da pasta `lib`.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-270">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="0ee1b-271">Observe que isso é diferente de um `DotNetCliTool` que é especificado pela configuração do `PackageType` no arquivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-271">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="0ee1b-272">Empacotamento usando um .nuspec</span><span class="sxs-lookup"><span data-stu-id="0ee1b-272">Packing using a .nuspec</span></span>

<span data-ttu-id="0ee1b-273">Você pode usar um `.nuspec` arquivo compactar seu projeto desde que você tenha um arquivo de projeto do SDK para importar `NuGet.Build.Tasks.Pack.targets` para que a tarefa de pacote pode ser executada.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-273">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="0ee1b-274">Você ainda precisa restaurar o projeto antes de você pode empacotar um arquivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-274">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="0ee1b-275">A estrutura de destino do arquivo do projeto é irrelevante e não é usado quando um nuspec de remessa.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-275">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="0ee1b-276">As três propriedades MSBuild a seguir são relevantes para empacotamento usando um `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-276">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="0ee1b-277">`NuspecFile`: caminho relativo ou absoluto para o arquivo `.nuspec` que está sendo usado para o empacotamento.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-277">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="0ee1b-278">`NuspecProperties`: uma lista separada por ponto e vírgula de pares chave/valor.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-278">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="0ee1b-279">Devido à maneira como a análise de linha de comando do MSBuild funciona, várias propriedades precisam ser especificadas da seguinte maneira: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-279">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="0ee1b-280">`NuspecBasePath`: o caminho base para o arquivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-280">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="0ee1b-281">Se estiver usando `dotnet.exe` para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-281">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="0ee1b-282">Se estiver usando o MSBuild para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-282">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="0ee1b-283">Observe que um nuspec de remessa usando dotnet.exe ou msbuild também leva para compilar o projeto por padrão.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-283">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="0ee1b-284">Isso pode ser evitado passando ```--no-build``` dotnet.exe, que é o equivalente da configuração de propriedade ```<NoBuild>true</NoBuild> ``` em seu arquivo de projeto, juntamente com a configuração ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` no arquivo de projeto</span><span class="sxs-lookup"><span data-stu-id="0ee1b-284">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="0ee1b-285">Um exemplo de um arquivo csproj ao empacotar um arquivo nuspec é:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-285">An example of a csproj file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="0ee1b-286">Advanced pontos de extensão para criar o pacote personalizado</span><span class="sxs-lookup"><span data-stu-id="0ee1b-286">Advanced extension points to create customized package</span></span>

<span data-ttu-id="0ee1b-287">O `pack` destino fornece dois pontos de extensão que executam o interna, compilação de destino do framework específico.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-287">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="0ee1b-288">Suportam os pontos de extensão incluindo conteúdo específico do framework de destino e assemblies em um pacote:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-288">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="0ee1b-289">`TargetsForTfmSpecificBuildOutput` destino: uso de arquivos dentro do `lib` pasta ou uma pasta especificada usando `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-289">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="0ee1b-290">`TargetsForTfmSpecificContentInPackage` destino: uso de arquivos fora do `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-290">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="0ee1b-291">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="0ee1b-291">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="0ee1b-292">Escrever um destino personalizado e especificá-lo como o valor de `$(TargetsForTfmSpecificBuildOutput)` propriedade.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-292">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="0ee1b-293">Para todos os arquivos que precisam entrar no `BuildOutputTargetFolder` lib (por padrão), o destino deve gravar os arquivos no ItemGroup `BuildOutputInPackage` e definir os dois valores de metadados a seguir:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-293">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="0ee1b-294">`FinalOutputPath`: O caminho absoluto do arquivo. Se não for fornecido, a identidade é usada para avaliar o caminho de origem.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-294">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="0ee1b-295">`TargetPath`: (Opcional) defina quando o arquivo precisa ir para uma subpasta em `lib\<TargetFramework>` , como assemblies de satélite que vão em suas pastas de cultura do respectivos.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-295">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="0ee1b-296">O padrão é o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-296">Defaults to the name of the file.</span></span>

<span data-ttu-id="0ee1b-297">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-297">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="0ee1b-298">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="0ee1b-298">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="0ee1b-299">Escrever um destino personalizado e especificá-lo como o valor de `$(TargetsForTfmSpecificContentInPackage)` propriedade.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-299">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="0ee1b-300">Para todos os arquivos incluir no pacote, o destino deve gravar os arquivos no ItemGroup `TfmSpecificPackageFile` e defina os seguintes metadados opcionais:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-300">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="0ee1b-301">`PackagePath`: O caminho onde o arquivo deve ser a saída do pacote.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-301">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="0ee1b-302">NuGet emite um aviso se mais de um arquivo é adicionado para o mesmo caminho de pacote.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-302">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="0ee1b-303">`BuildAction`: A ação de compilação para atribuir ao arquivo, é necessário somente se o caminho do pacote está no `contentFiles` pasta.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-303">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="0ee1b-304">O padrão é "None".</span><span class="sxs-lookup"><span data-stu-id="0ee1b-304">Defaults to "None".</span></span>

<span data-ttu-id="0ee1b-305">Um exemplo:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-305">An example:</span></span>
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name=""CustomContentTarget"">
  <ItemGroup>
    <TfmSpecificPackageFile Include=""abc.txt"">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include=""Extensions/ext.txt"" Condition=""'$(TargetFramework)' == 'net46'"">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a><span data-ttu-id="0ee1b-306">restore target</span><span class="sxs-lookup"><span data-stu-id="0ee1b-306">restore target</span></span>

<span data-ttu-id="0ee1b-307">`MSBuild /t:restore` (que `nuget restore` e `dotnet restore` usam com projetos do .NET Core), restaura pacotes referenciados no arquivo de projeto da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-307">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="0ee1b-308">Ler todas as referências projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="0ee1b-308">Read all project to project references</span></span>
1. <span data-ttu-id="0ee1b-309">Ler as propriedades do projeto para localizar a pasta intermediária e as estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="0ee1b-309">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="0ee1b-310">Passar dados do msbuild para NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="0ee1b-310">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="0ee1b-311">Executar restauração</span><span class="sxs-lookup"><span data-stu-id="0ee1b-311">Run restore</span></span>
1. <span data-ttu-id="0ee1b-312">Baixar os pacotes</span><span class="sxs-lookup"><span data-stu-id="0ee1b-312">Download packages</span></span>
1. <span data-ttu-id="0ee1b-313">Gravar arquivo de ativos, destinos e objetos</span><span class="sxs-lookup"><span data-stu-id="0ee1b-313">Write assets file, targets, and props</span></span>

<span data-ttu-id="0ee1b-314">O `restore` destino funciona **somente** para projetos que usam o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-314">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="0ee1b-315">Ele faz **não** para projetos usando o `packages.config` formato; use [restauração do nuget](../tools/cli-ref-restore.md) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-315">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="0ee1b-316">Restaurar propriedades</span><span class="sxs-lookup"><span data-stu-id="0ee1b-316">Restore properties</span></span>

<span data-ttu-id="0ee1b-317">Configurações de restauração adicionais podem vir de propriedades MSBuild no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-317">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="0ee1b-318">Os valores também podem ser definidos na linha de comando usando a opção `/p:` (consulte os Exemplos abaixo).</span><span class="sxs-lookup"><span data-stu-id="0ee1b-318">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="0ee1b-319">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0ee1b-319">Property</span></span> | <span data-ttu-id="0ee1b-320">Descrição</span><span class="sxs-lookup"><span data-stu-id="0ee1b-320">Description</span></span> |
|--------|--------|
| <span data-ttu-id="0ee1b-321">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="0ee1b-321">RestoreSources</span></span> | <span data-ttu-id="0ee1b-322">Uma lista delimitada por ponto e vírgula de origens de pacote.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-322">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="0ee1b-323">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="0ee1b-323">RestorePackagesPath</span></span> | <span data-ttu-id="0ee1b-324">Caminho da pasta dos pacotes do usuário.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-324">User packages folder path.</span></span> |
| <span data-ttu-id="0ee1b-325">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="0ee1b-325">RestoreDisableParallel</span></span> | <span data-ttu-id="0ee1b-326">Limite os downloads para um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-326">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="0ee1b-327">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="0ee1b-327">RestoreConfigFile</span></span> | <span data-ttu-id="0ee1b-328">Caminho para um arquivo `Nuget.Config` a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-328">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="0ee1b-329">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="0ee1b-329">RestoreNoCache</span></span> | <span data-ttu-id="0ee1b-330">Se true, evita o uso de pacotes armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-330">If true, avoids using cached packages.</span></span> <span data-ttu-id="0ee1b-331">Consulte [Gerenciando os pacotes globais e as pastas do cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="0ee1b-331">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="0ee1b-332">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="0ee1b-332">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="0ee1b-333">Se verdadeiro, ignora origens de pacote com falha ou ausentes.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-333">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="0ee1b-334">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="0ee1b-334">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="0ee1b-335">Caminho para `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-335">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="0ee1b-336">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="0ee1b-336">RestoreGraphProjectInput</span></span> | <span data-ttu-id="0ee1b-337">Lista separada por ponto e vírgula de projetos a serem restaurados, que devem conter caminhos absolutos.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-337">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="0ee1b-338">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="0ee1b-338">RestoreOutputPath</span></span> | <span data-ttu-id="0ee1b-339">Pasta de saída que usa a pasta `obj` como padrão.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-339">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="0ee1b-340">Exemplos</span><span class="sxs-lookup"><span data-stu-id="0ee1b-340">Examples</span></span>

<span data-ttu-id="0ee1b-341">Linha de comando:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-341">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="0ee1b-342">Arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-342">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="0ee1b-343">Restaurar saídas</span><span class="sxs-lookup"><span data-stu-id="0ee1b-343">Restore outputs</span></span>

<span data-ttu-id="0ee1b-344">A restauração cria os seguintes arquivos na pasta `obj` de build:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-344">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="0ee1b-345">Arquivo</span><span class="sxs-lookup"><span data-stu-id="0ee1b-345">File</span></span> | <span data-ttu-id="0ee1b-346">Descrição</span><span class="sxs-lookup"><span data-stu-id="0ee1b-346">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="0ee1b-347">Contém o gráfico de dependência de todas as referências do pacote.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-347">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="0ee1b-348">Referências a objetos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="0ee1b-348">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="0ee1b-349">Referências a destinos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="0ee1b-349">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="0ee1b-350">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="0ee1b-350">PackageTargetFallback</span></span>

<span data-ttu-id="0ee1b-351">O elemento `PackageTargetFallback` permite especificar um conjunto de destinos compatíveis a serem usados ao restaurar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-351">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="0ee1b-352">Ele foi desenvolvido para permitir que os pacotes que usam o dotnet [TxM](../reference/target-frameworks.md) funcionem com pacotes compatíveis que não declaram um dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-352">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="0ee1b-353">Ou seja, se o projeto usar o dotnet TxM, todos os pacotes dos quais ele depende também deverão ter um dotnet TxM, a menos que você adicione o `<PackageTargetFallback>` ao projeto para permitir que plataformas não dotnet sejam compatíveis com o dotnet.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-353">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="0ee1b-354">Por exemplo, se o projeto está usando o `netstandard1.6` TxM e um pacote dependente contém apenas `lib/net45/a.dll` e `lib/portable-net45+win81/a.dll`, o projeto não será compilado.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-354">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="0ee1b-355">Se a DLL que você deseja colocar é esta última, é possível adicionar um `PackageTargetFallback` como mostrado a seguir para dizer que a DLL `portable-net45+win81` é compatível:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-355">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="0ee1b-356">Para declarar um fallback para todos os destinos em seu projeto, deixe o atributo `Condition` de fora.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-356">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="0ee1b-357">Você também pode estender qualquer `PackageTargetFallback` existente incluindo `$(PackageTargetFallback)` conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-357">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="0ee1b-358">Substituindo uma biblioteca de um grafo de restauração</span><span class="sxs-lookup"><span data-stu-id="0ee1b-358">Replacing one library from a restore graph</span></span>

<span data-ttu-id="0ee1b-359">Se uma restauração está trazendo o assembly errado, é possível excluir a escolha padrão do pacote e substituí-lo por outro de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="0ee1b-359">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="0ee1b-360">Primeiro com um `PackageReference` de nível superior, exclua todos os ativos:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-360">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="0ee1b-361">Em seguida, adicione sua própria referência à cópia local apropriada da DLL:</span><span class="sxs-lookup"><span data-stu-id="0ee1b-361">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
