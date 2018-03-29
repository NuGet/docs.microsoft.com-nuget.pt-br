---
title: Empacotamento e restauração do NuGet como destinos do MSBuild | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: O pack e restore do NuGet podem funcionar diretamente como destinos do MSBuild com o NuGet 4.0 e superior.
keywords: NuGet e MSBuild, NuGet pack target, NuGet restore target
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: a9c2c2229d717dff8472dce0ba568e4a21900b19
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="f9ddb-104">Empacotamento e restauração do NuGet como destinos do MSBuild</span><span class="sxs-lookup"><span data-stu-id="f9ddb-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="f9ddb-105">*NuGet 4.0 ou superior*</span><span class="sxs-lookup"><span data-stu-id="f9ddb-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="f9ddb-106">Com o formato PackageReference, o NuGet 4.0 e posterior pode armazenar todos os metadados de manifesto diretamente dentro de um arquivo de projeto em vez de usar um arquivo `.nuspec` separado.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="f9ddb-107">Com o MSBuild 15.1 ou superior, o NuGet também é um cidadão de primeira classe do MSBuild com os destinos `pack` e `restore`, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="f9ddb-108">Esses destinos permitem que você trabalhe com o NuGet como faria com qualquer outra tarefa ou destino do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="f9ddb-109">(Para NuGet 3.x e anteriores, use os comandos [pack](../tools/cli-ref-pack.md) e [restore](../tools/cli-ref-restore.md) na CLI do NuGet.)</span><span class="sxs-lookup"><span data-stu-id="f9ddb-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="f9ddb-110">Ordem de build de destino</span><span class="sxs-lookup"><span data-stu-id="f9ddb-110">Target build order</span></span>

<span data-ttu-id="f9ddb-111">Como `pack` e `restore` são os destinos do MSBuild, você pode acessá-los para melhorar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="f9ddb-112">Por exemplo, digamos que você deseja copiar o pacote para um compartilhamento de rede após empacotá-lo.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="f9ddb-113">Você pode fazer isso adicionando o seguinte ao seu arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="f9ddb-114">Da mesma forma, você pode gravar uma tarefa do MSBuild, escrever seu próprio destino e consumir propriedades do NuGet na tarefa de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="f9ddb-115">pack target</span><span class="sxs-lookup"><span data-stu-id="f9ddb-115">pack target</span></span>

<span data-ttu-id="f9ddb-116">Para projetos padrão do .NET usando o formato PackageReference, usando `msbuild /t:pack` desenha entradas do arquivo de projeto para usar na criação de um pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-116">For .NET Standard projects using the PackageReference format, using `msbuild /t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="f9ddb-117">A tabela abaixo descreve as propriedades do MSBuild que podem ser adicionadas a um arquivo do projeto dentro do primeiro nó `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="f9ddb-118">Você pode fazer essas edições facilmente no Visual Studio 2017 e posterior clicando com o botão direito do mouse no projeto e selecionando **Editar {project_name}** no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="f9ddb-119">Para sua conveniência, a tabela é organizada pela propriedade equivalente em um arquivo [`.nuspec` ](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="f9ddb-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="f9ddb-120">Observe que as propriedades `Owners` e `Summary` de `.nuspec` não são compatíveis com o MSBuild.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="f9ddb-121">Valor de atributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="f9ddb-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="f9ddb-122">Propriedade do MSBuild</span><span class="sxs-lookup"><span data-stu-id="f9ddb-122">MSBuild Property</span></span> | <span data-ttu-id="f9ddb-123">Padrão</span><span class="sxs-lookup"><span data-stu-id="f9ddb-123">Default</span></span> | <span data-ttu-id="f9ddb-124">Observações</span><span class="sxs-lookup"><span data-stu-id="f9ddb-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="f9ddb-125">Id</span><span class="sxs-lookup"><span data-stu-id="f9ddb-125">Id</span></span> | <span data-ttu-id="f9ddb-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="f9ddb-126">PackageId</span></span> | <span data-ttu-id="f9ddb-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="f9ddb-127">AssemblyName</span></span> | <span data-ttu-id="f9ddb-128">$(AssemblyName) do MSBuild</span><span class="sxs-lookup"><span data-stu-id="f9ddb-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="f9ddb-129">Versão</span><span class="sxs-lookup"><span data-stu-id="f9ddb-129">Version</span></span> | <span data-ttu-id="f9ddb-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="f9ddb-130">PackageVersion</span></span> | <span data-ttu-id="f9ddb-131">Versão</span><span class="sxs-lookup"><span data-stu-id="f9ddb-131">Version</span></span> | <span data-ttu-id="f9ddb-132">Isso é compatível com semver, por exemplo “1.0.0”, “1.0.0-beta” ou “1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="f9ddb-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="f9ddb-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="f9ddb-133">VersionPrefix</span></span> | <span data-ttu-id="f9ddb-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="f9ddb-134">PackageVersionPrefix</span></span> | <span data-ttu-id="f9ddb-135">empty</span><span class="sxs-lookup"><span data-stu-id="f9ddb-135">empty</span></span> | <span data-ttu-id="f9ddb-136">A configuração PackageVersion substitui PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="f9ddb-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="f9ddb-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="f9ddb-137">VersionSuffix</span></span> | <span data-ttu-id="f9ddb-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="f9ddb-138">PackageVersionSuffix</span></span> | <span data-ttu-id="f9ddb-139">empty</span><span class="sxs-lookup"><span data-stu-id="f9ddb-139">empty</span></span> | <span data-ttu-id="f9ddb-140">$(VersionSuffix) do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="f9ddb-141">A configuração PackageVersion substitui PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="f9ddb-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="f9ddb-142">Autores</span><span class="sxs-lookup"><span data-stu-id="f9ddb-142">Authors</span></span> | <span data-ttu-id="f9ddb-143">Autores</span><span class="sxs-lookup"><span data-stu-id="f9ddb-143">Authors</span></span> | <span data-ttu-id="f9ddb-144">Nome do usuário atual</span><span class="sxs-lookup"><span data-stu-id="f9ddb-144">Username of the current user</span></span> | |
| <span data-ttu-id="f9ddb-145">Proprietários</span><span class="sxs-lookup"><span data-stu-id="f9ddb-145">Owners</span></span> | <span data-ttu-id="f9ddb-146">N/D</span><span class="sxs-lookup"><span data-stu-id="f9ddb-146">N/A</span></span> | <span data-ttu-id="f9ddb-147">Não está presente no NuSpec</span><span class="sxs-lookup"><span data-stu-id="f9ddb-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="f9ddb-148">Título</span><span class="sxs-lookup"><span data-stu-id="f9ddb-148">Title</span></span> | <span data-ttu-id="f9ddb-149">Título</span><span class="sxs-lookup"><span data-stu-id="f9ddb-149">Title</span></span> | <span data-ttu-id="f9ddb-150">O PackageId</span><span class="sxs-lookup"><span data-stu-id="f9ddb-150">The PackageId</span></span>| |
| <span data-ttu-id="f9ddb-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="f9ddb-151">Description</span></span> | <span data-ttu-id="f9ddb-152">PackageDescription</span><span class="sxs-lookup"><span data-stu-id="f9ddb-152">PackageDescription</span></span> | <span data-ttu-id="f9ddb-153">“Package Description”</span><span class="sxs-lookup"><span data-stu-id="f9ddb-153">"Package Description"</span></span> | |
| <span data-ttu-id="f9ddb-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="f9ddb-154">Copyright</span></span> | <span data-ttu-id="f9ddb-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="f9ddb-155">Copyright</span></span> | <span data-ttu-id="f9ddb-156">empty</span><span class="sxs-lookup"><span data-stu-id="f9ddb-156">empty</span></span> | |
| <span data-ttu-id="f9ddb-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="f9ddb-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="f9ddb-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="f9ddb-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="f9ddb-159">false</span><span class="sxs-lookup"><span data-stu-id="f9ddb-159">false</span></span> | |
| <span data-ttu-id="f9ddb-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="f9ddb-160">LicenseUrl</span></span> | <span data-ttu-id="f9ddb-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="f9ddb-161">PackageLicenseUrl</span></span> | <span data-ttu-id="f9ddb-162">empty</span><span class="sxs-lookup"><span data-stu-id="f9ddb-162">empty</span></span> | |
| <span data-ttu-id="f9ddb-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="f9ddb-163">ProjectUrl</span></span> | <span data-ttu-id="f9ddb-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="f9ddb-164">PackageProjectUrl</span></span> | <span data-ttu-id="f9ddb-165">empty</span><span class="sxs-lookup"><span data-stu-id="f9ddb-165">empty</span></span> | |
| <span data-ttu-id="f9ddb-166">IconUrl</span><span class="sxs-lookup"><span data-stu-id="f9ddb-166">IconUrl</span></span> | <span data-ttu-id="f9ddb-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="f9ddb-167">PackageIconUrl</span></span> | <span data-ttu-id="f9ddb-168">empty</span><span class="sxs-lookup"><span data-stu-id="f9ddb-168">empty</span></span> | |
| <span data-ttu-id="f9ddb-169">Marcas</span><span class="sxs-lookup"><span data-stu-id="f9ddb-169">Tags</span></span> | <span data-ttu-id="f9ddb-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="f9ddb-170">PackageTags</span></span> | <span data-ttu-id="f9ddb-171">empty</span><span class="sxs-lookup"><span data-stu-id="f9ddb-171">empty</span></span> | <span data-ttu-id="f9ddb-172">Marcas são delimitadas por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="f9ddb-173">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="f9ddb-173">ReleaseNotes</span></span> | <span data-ttu-id="f9ddb-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="f9ddb-174">PackageReleaseNotes</span></span> | <span data-ttu-id="f9ddb-175">empty</span><span class="sxs-lookup"><span data-stu-id="f9ddb-175">empty</span></span> | |
| <span data-ttu-id="f9ddb-176">Url do repositório</span><span class="sxs-lookup"><span data-stu-id="f9ddb-176">Repository/Url</span></span> | <span data-ttu-id="f9ddb-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="f9ddb-177">RepositoryUrl</span></span> | <span data-ttu-id="f9ddb-178">empty</span><span class="sxs-lookup"><span data-stu-id="f9ddb-178">empty</span></span> | <span data-ttu-id="f9ddb-179">URL do repositório usado para clonar ou recuperar o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-179">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="f9ddb-180">Exemplo: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="f9ddb-180">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="f9ddb-181">Tipo do repositório</span><span class="sxs-lookup"><span data-stu-id="f9ddb-181">Repository/Type</span></span> | <span data-ttu-id="f9ddb-182">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="f9ddb-182">RepositoryType</span></span> | <span data-ttu-id="f9ddb-183">empty</span><span class="sxs-lookup"><span data-stu-id="f9ddb-183">empty</span></span> | <span data-ttu-id="f9ddb-184">Tipo de repositório.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-184">Repository type.</span></span> <span data-ttu-id="f9ddb-185">Exemplos: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-185">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="f9ddb-186">Ramificação do repositório</span><span class="sxs-lookup"><span data-stu-id="f9ddb-186">Repository/Branch</span></span> | <span data-ttu-id="f9ddb-187">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="f9ddb-187">RepositoryBranch</span></span> | <span data-ttu-id="f9ddb-188">empty</span><span class="sxs-lookup"><span data-stu-id="f9ddb-188">empty</span></span> | <span data-ttu-id="f9ddb-189">Informações de ramificação do repositório opcional.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-189">Optional repository branch information.</span></span> <span data-ttu-id="f9ddb-190">*RepositoryUrl* também deve ser especificado para essa propriedade a ser incluído.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-190">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="f9ddb-191">Exemplo: *mestre* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="f9ddb-191">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="f9ddb-192">Repositório/confirmação</span><span class="sxs-lookup"><span data-stu-id="f9ddb-192">Repository/Commit</span></span> | <span data-ttu-id="f9ddb-193">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="f9ddb-193">RepositoryCommit</span></span> | <span data-ttu-id="f9ddb-194">empty</span><span class="sxs-lookup"><span data-stu-id="f9ddb-194">empty</span></span> | <span data-ttu-id="f9ddb-195">Confirmação de repositório opcional ou conjunto de alterações para indicar que o pacote de origem foi desenvolvido com.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-195">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="f9ddb-196">*RepositoryUrl* também deve ser especificado para essa propriedade a ser incluído.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-196">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="f9ddb-197">Exemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="f9ddb-197">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="f9ddb-198">PackageType</span><span class="sxs-lookup"><span data-stu-id="f9ddb-198">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="f9ddb-199">Resumo</span><span class="sxs-lookup"><span data-stu-id="f9ddb-199">Summary</span></span> | <span data-ttu-id="f9ddb-200">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="f9ddb-200">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="f9ddb-201">pack target inputs</span><span class="sxs-lookup"><span data-stu-id="f9ddb-201">pack target inputs</span></span>

- <span data-ttu-id="f9ddb-202">IsPackable</span><span class="sxs-lookup"><span data-stu-id="f9ddb-202">IsPackable</span></span>
- <span data-ttu-id="f9ddb-203">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="f9ddb-203">PackageVersion</span></span>
- <span data-ttu-id="f9ddb-204">PackageId</span><span class="sxs-lookup"><span data-stu-id="f9ddb-204">PackageId</span></span>
- <span data-ttu-id="f9ddb-205">Autores</span><span class="sxs-lookup"><span data-stu-id="f9ddb-205">Authors</span></span>
- <span data-ttu-id="f9ddb-206">Descrição</span><span class="sxs-lookup"><span data-stu-id="f9ddb-206">Description</span></span>
- <span data-ttu-id="f9ddb-207">Copyright</span><span class="sxs-lookup"><span data-stu-id="f9ddb-207">Copyright</span></span>
- <span data-ttu-id="f9ddb-208">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="f9ddb-208">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="f9ddb-209">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="f9ddb-209">DevelopmentDependency</span></span>
- <span data-ttu-id="f9ddb-210">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="f9ddb-210">PackageLicenseUrl</span></span>
- <span data-ttu-id="f9ddb-211">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="f9ddb-211">PackageProjectUrl</span></span>
- <span data-ttu-id="f9ddb-212">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="f9ddb-212">PackageIconUrl</span></span>
- <span data-ttu-id="f9ddb-213">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="f9ddb-213">PackageReleaseNotes</span></span>
- <span data-ttu-id="f9ddb-214">PackageTags</span><span class="sxs-lookup"><span data-stu-id="f9ddb-214">PackageTags</span></span>
- <span data-ttu-id="f9ddb-215">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="f9ddb-215">PackageOutputPath</span></span>
- <span data-ttu-id="f9ddb-216">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="f9ddb-216">IncludeSymbols</span></span>
- <span data-ttu-id="f9ddb-217">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="f9ddb-217">IncludeSource</span></span>
- <span data-ttu-id="f9ddb-218">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="f9ddb-218">PackageTypes</span></span>
- <span data-ttu-id="f9ddb-219">IsTool</span><span class="sxs-lookup"><span data-stu-id="f9ddb-219">IsTool</span></span>
- <span data-ttu-id="f9ddb-220">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="f9ddb-220">RepositoryUrl</span></span>
- <span data-ttu-id="f9ddb-221">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="f9ddb-221">RepositoryType</span></span>
- <span data-ttu-id="f9ddb-222">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="f9ddb-222">RepositoryBranch</span></span>
- <span data-ttu-id="f9ddb-223">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="f9ddb-223">RepositoryCommit</span></span>
- <span data-ttu-id="f9ddb-224">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="f9ddb-224">NoPackageAnalysis</span></span>
- <span data-ttu-id="f9ddb-225">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="f9ddb-225">MinClientVersion</span></span>
- <span data-ttu-id="f9ddb-226">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="f9ddb-226">IncludeBuildOutput</span></span>
- <span data-ttu-id="f9ddb-227">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="f9ddb-227">IncludeContentInPack</span></span>
- <span data-ttu-id="f9ddb-228">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="f9ddb-228">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="f9ddb-229">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="f9ddb-229">ContentTargetFolders</span></span>
- <span data-ttu-id="f9ddb-230">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="f9ddb-230">NuspecFile</span></span>
- <span data-ttu-id="f9ddb-231">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="f9ddb-231">NuspecBasePath</span></span>
- <span data-ttu-id="f9ddb-232">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="f9ddb-232">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="f9ddb-233">pack scenarios</span><span class="sxs-lookup"><span data-stu-id="f9ddb-233">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="f9ddb-234">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="f9ddb-234">PackageIconUrl</span></span>

<span data-ttu-id="f9ddb-235">Como parte da alteração de [NuGet problema 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` eventualmente será alterado para `PackageIconUri` e pode ser um caminho relativo para um arquivo de ícone que será incluído na raiz do pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-235">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="f9ddb-236">Assemblies de saída</span><span class="sxs-lookup"><span data-stu-id="f9ddb-236">Output assemblies</span></span>

<span data-ttu-id="f9ddb-237">O `nuget pack` copia arquivos de saída com extensões `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-237">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="f9ddb-238">Os arquivos de saída que são copiados dependem do que o MSBuild fornece do destino `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-238">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="f9ddb-239">Há duas propriedades de MSBuild que você pode usar em seu arquivo de projeto ou a linha de comando para controlar onde ficam os assemblies de saída:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-239">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="f9ddb-240">`IncludeBuildOutput`: um valor booliano que determina se os assemblies de saída de build devem ser incluídos no pacote.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-240">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="f9ddb-241">`BuildOutputTargetFolder`: especifica a pasta na qual os assemblies de saída devem ser colocados.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-241">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="f9ddb-242">Os assemblies de saída (e outros arquivos de saída) são copiados para suas respectivas pastas de estrutura.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-242">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="f9ddb-243">Referências de pacote</span><span class="sxs-lookup"><span data-stu-id="f9ddb-243">Package references</span></span>

<span data-ttu-id="f9ddb-244">Consulte [Referências de pacote em arquivos de projeto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="f9ddb-244">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="f9ddb-245">Referências de projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="f9ddb-245">Project to project references</span></span>

<span data-ttu-id="f9ddb-246">As referências projeto a projeto são consideradas como referências de pacote do nuget por padrão, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-246">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="f9ddb-247">Você também pode adicionar os seguintes metadados à referência de projeto:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-247">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="f9ddb-248">Incluindo o conteúdo em um pacote</span><span class="sxs-lookup"><span data-stu-id="f9ddb-248">Including content in a package</span></span>

<span data-ttu-id="f9ddb-249">Para incluir o conteúdo, adicione metadados extras ao item `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-249">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="f9ddb-250">Por padrão, tudo que pertencer ao tipo “Conteúdo” é incluído no pacote, a menos que seja substituído por entradas como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-250">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="f9ddb-251">Por padrão, tudo é adicionado à raiz da pasta `content` e `contentFiles\any\<target_framework>` dentro de um pacote e preserva a estrutura e pasta relativa, a menos que você especifique um caminho de pacote:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-251">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="f9ddb-252">Se você quiser copiar todo o conteúdo somente para determinadas pastas raiz (em vez de para `content` e `contentFiles`), será possível usar a propriedade `ContentTargetFolders` do MSBuild, que assume como padrão "content;contentFiles", mas pode ser definida como qualquer outro nome de pasta.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-252">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="f9ddb-253">Observe que só especificar “contentFiles” em `ContentTargetFolders` coloca os arquivos em `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` com base em `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-253">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="f9ddb-254">`PackagePath` pode ser um conjunto de caminhos de destino separados por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-254">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="f9ddb-255">Especificar um caminho de pacote vazio adicionaria o arquivo à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-255">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="f9ddb-256">Por exemplo, o seguinte adiciona `libuv.txt` a `content\myfiles`, `content\samples` e a raiz do pacote:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-256">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="f9ddb-257">Há também uma propriedade de MSBuild `$(IncludeContentInPack)`, que assume o padrão `true`.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-257">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="f9ddb-258">Se isso for definido como `false` em qualquer projeto, o conteúdo desse projeto não está incluso no pacote do nuget.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-258">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="f9ddb-259">Outros metadados específicos do pacote que pode ser definido em qualquer um dos itens acima ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, que define os valores ```CopyToOutput``` e ```Flatten``` na entrada ```contentFiles``` no nuspec de saída.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-259">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="f9ddb-260">Além de itens de Conteúdo, os metadados `<Pack>` e `<PackagePath>` também podem ser definidos em arquivos com uma ação de Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-260">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="f9ddb-261">Para o pacote acrescentar o nome de arquivo ao caminho do pacote ao usar padrões glob, seu caminho de pacote deve terminar com o caractere separador de pasta, caso contrário, o caminho do pacote será tratado como o caminho completo, incluindo o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-261">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="f9ddb-262">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="f9ddb-262">IncludeSymbols</span></span>

<span data-ttu-id="f9ddb-263">Ao usar o `MSBuild /t:pack /p:IncludeSymbols=true`, os arquivos `.pdb` correspondentes são copiados junto com outros arquivos de saída (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="f9ddb-263">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="f9ddb-264">Observe que a configuração `IncludeSymbols=true` cria um pacote regular *e* um pacote de símbolos.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-264">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="f9ddb-265">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="f9ddb-265">IncludeSource</span></span>

<span data-ttu-id="f9ddb-266">Isso é o mesmo que `IncludeSymbols`, exceto que também copia os arquivos de origem com arquivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-266">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="f9ddb-267">Todos os arquivos do tipo `Compile` são copiadas para `src\<ProjectName>\`, preservando a estrutura de pastas do caminho relativo no pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-267">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="f9ddb-268">O mesmo também ocorre para arquivos de origem de qualquer `ProjectReference` que tem `TreatAsPackageReference` definido como `false`.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-268">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="f9ddb-269">Se um arquivo do tipo Compilação estiver fora da pasta de projeto, ele será adicionado apenas a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-269">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="f9ddb-270">IsTool</span><span class="sxs-lookup"><span data-stu-id="f9ddb-270">IsTool</span></span>

<span data-ttu-id="f9ddb-271">Ao usar `MSBuild /t:pack /p:IsTool=true`, todos os arquivos de saída, conforme especificado no cenário [Assemblies de saída](#output-assemblies), são copiados para a pasta `tools` em vez da pasta `lib`.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-271">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="f9ddb-272">Observe que isso é diferente de um `DotNetCliTool` que é especificado pela configuração do `PackageType` no arquivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-272">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="f9ddb-273">Empacotamento usando um .nuspec</span><span class="sxs-lookup"><span data-stu-id="f9ddb-273">Packing using a .nuspec</span></span>

<span data-ttu-id="f9ddb-274">Você pode usar um `.nuspec` arquivo compactar seu projeto desde que você tenha um arquivo de projeto do SDK para importar `NuGet.Build.Tasks.Pack.targets` para que a tarefa de pacote pode ser executada.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-274">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="f9ddb-275">Você ainda precisa restaurar o projeto antes de você pode empacotar um arquivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-275">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="f9ddb-276">A estrutura de destino do arquivo do projeto é irrelevante e não é usado quando um nuspec de remessa.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-276">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="f9ddb-277">As três propriedades MSBuild a seguir são relevantes para empacotamento usando um `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-277">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="f9ddb-278">`NuspecFile`: caminho relativo ou absoluto para o arquivo `.nuspec` que está sendo usado para o empacotamento.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-278">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="f9ddb-279">`NuspecProperties`: uma lista separada por ponto e vírgula de pares chave/valor.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-279">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="f9ddb-280">Devido à maneira como a análise de linha de comando do MSBuild funciona, várias propriedades precisam ser especificadas da seguinte maneira: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-280">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="f9ddb-281">`NuspecBasePath`: o caminho base para o arquivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-281">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="f9ddb-282">Se estiver usando `dotnet.exe` para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-282">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="f9ddb-283">Se estiver usando o MSBuild para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-283">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="f9ddb-284">Observe que um nuspec de remessa usando dotnet.exe ou msbuild também leva para compilar o projeto por padrão.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-284">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="f9ddb-285">Isso pode ser evitado passando ```--no-build``` dotnet.exe, que é o equivalente da configuração de propriedade ```<NoBuild>true</NoBuild> ``` em seu arquivo de projeto, juntamente com a configuração ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` no arquivo de projeto</span><span class="sxs-lookup"><span data-stu-id="f9ddb-285">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="f9ddb-286">Um exemplo de um arquivo csproj ao empacotar um arquivo nuspec é:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-286">An example of a csproj file to pack a nuspec file is:</span></span>

```
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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="f9ddb-287">Advanced pontos de extensão para criar o pacote personalizado</span><span class="sxs-lookup"><span data-stu-id="f9ddb-287">Advanced extension points to create customized package</span></span>

<span data-ttu-id="f9ddb-288">O `pack` destino fornece dois pontos de extensão que executam o interna, compilação de destino do framework específico.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-288">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="f9ddb-289">Suportam os pontos de extensão incluindo conteúdo específico do framework de destino e assemblies em um pacote:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-289">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="f9ddb-290">`TargetsForTfmSpecificBuildOutput` destino: uso de arquivos dentro do `lib` pasta ou uma pasta especificada usando `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-290">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="f9ddb-291">`TargetsForTfmSpecificContentInPackage` destino: uso de arquivos fora do `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-291">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="f9ddb-292">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="f9ddb-292">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="f9ddb-293">Escrever um destino personalizado e especificá-lo como o valor de `$(TargetsForTfmSpecificBuildOutput)` propriedade.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-293">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="f9ddb-294">Para todos os arquivos que precisam entrar no `BuildOutputTargetFolder` lib (por padrão), o destino deve gravar os arquivos no ItemGroup `BuildOutputInPackage` e definir os dois valores de metadados a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-294">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="f9ddb-295">`FinalOutputPath`: O caminho absoluto do arquivo. Se não for fornecido, a identidade é usada para avaliar o caminho de origem.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-295">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="f9ddb-296">`TargetPath`: (Opcional) defina quando o arquivo precisa ir para uma subpasta em `lib\<TargetFramework>` , como assemblies de satélite que vão em suas pastas de cultura do respectivos.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-296">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="f9ddb-297">O padrão é o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-297">Defaults to the name of the file.</span></span>

<span data-ttu-id="f9ddb-298">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-298">Example:</span></span>

```
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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="f9ddb-299">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="f9ddb-299">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="f9ddb-300">Escrever um destino personalizado e especificá-lo como o valor de `$(TargetsForTfmSpecificContentInPackage)` propriedade.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-300">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="f9ddb-301">Para todos os arquivos incluir no pacote, o destino deve gravar os arquivos no ItemGroup `TfmSpecificPackageFile` e defina os seguintes metadados opcionais:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-301">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="f9ddb-302">`PackagePath`: O caminho onde o arquivo deve ser a saída do pacote.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-302">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="f9ddb-303">NuGet emite um aviso se mais de um arquivo é adicionado para o mesmo caminho de pacote.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-303">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="f9ddb-304">`BuildAction`: A ação de compilação para atribuir ao arquivo, é necessário somente se o caminho do pacote está no `contentFiles` pasta.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-304">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="f9ddb-305">O padrão é "None".</span><span class="sxs-lookup"><span data-stu-id="f9ddb-305">Defaults to "None".</span></span>

<span data-ttu-id="f9ddb-306">Um exemplo:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-306">An example:</span></span>
```
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

## <a name="restore-target"></a><span data-ttu-id="f9ddb-307">restore target</span><span class="sxs-lookup"><span data-stu-id="f9ddb-307">restore target</span></span>

<span data-ttu-id="f9ddb-308">`MSBuild /t:restore` (que `nuget restore` e `dotnet restore` usam com projetos do .NET Core), restaura pacotes referenciados no arquivo de projeto da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-308">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="f9ddb-309">Ler todas as referências projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="f9ddb-309">Read all project to project references</span></span>
1. <span data-ttu-id="f9ddb-310">Ler as propriedades do projeto para localizar a pasta intermediária e as estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="f9ddb-310">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="f9ddb-311">Passar dados do msbuild para NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="f9ddb-311">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="f9ddb-312">Executar restauração</span><span class="sxs-lookup"><span data-stu-id="f9ddb-312">Run restore</span></span>
1. <span data-ttu-id="f9ddb-313">Baixar os pacotes</span><span class="sxs-lookup"><span data-stu-id="f9ddb-313">Download packages</span></span>
1. <span data-ttu-id="f9ddb-314">Gravar arquivo de ativos, destinos e objetos</span><span class="sxs-lookup"><span data-stu-id="f9ddb-314">Write assets file, targets, and props</span></span>

<span data-ttu-id="f9ddb-315">O `restore` destino funciona **somente** para projetos que usam o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-315">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="f9ddb-316">Ele faz **não** para projetos usando o `packages.config` formato; use [restauração do nuget](../tools/cli-ref-restore.md) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-316">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="f9ddb-317">Restaurar propriedades</span><span class="sxs-lookup"><span data-stu-id="f9ddb-317">Restore properties</span></span>

<span data-ttu-id="f9ddb-318">Configurações de restauração adicionais podem vir de propriedades MSBuild no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-318">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="f9ddb-319">Os valores também podem ser definidos na linha de comando usando a opção `/p:` (consulte os Exemplos abaixo).</span><span class="sxs-lookup"><span data-stu-id="f9ddb-319">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="f9ddb-320">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f9ddb-320">Property</span></span> | <span data-ttu-id="f9ddb-321">Descrição</span><span class="sxs-lookup"><span data-stu-id="f9ddb-321">Description</span></span> |
|--------|--------|
| <span data-ttu-id="f9ddb-322">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="f9ddb-322">RestoreSources</span></span> | <span data-ttu-id="f9ddb-323">Uma lista delimitada por ponto e vírgula de origens de pacote.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-323">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="f9ddb-324">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="f9ddb-324">RestorePackagesPath</span></span> | <span data-ttu-id="f9ddb-325">Caminho da pasta dos pacotes do usuário.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-325">User packages folder path.</span></span> |
| <span data-ttu-id="f9ddb-326">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="f9ddb-326">RestoreDisableParallel</span></span> | <span data-ttu-id="f9ddb-327">Limite os downloads para um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-327">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="f9ddb-328">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="f9ddb-328">RestoreConfigFile</span></span> | <span data-ttu-id="f9ddb-329">Caminho para um arquivo `Nuget.Config` a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-329">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="f9ddb-330">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="f9ddb-330">RestoreNoCache</span></span> | <span data-ttu-id="f9ddb-331">Se true, evita o uso de pacotes armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-331">If true, avoids using cached packages.</span></span> <span data-ttu-id="f9ddb-332">Consulte [Gerenciando os pacotes globais e as pastas do cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="f9ddb-332">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="f9ddb-333">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="f9ddb-333">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="f9ddb-334">Se verdadeiro, ignora origens de pacote com falha ou ausentes.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-334">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="f9ddb-335">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="f9ddb-335">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="f9ddb-336">Caminho para `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-336">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="f9ddb-337">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="f9ddb-337">RestoreGraphProjectInput</span></span> | <span data-ttu-id="f9ddb-338">Lista separada por ponto e vírgula de projetos a serem restaurados, que devem conter caminhos absolutos.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-338">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="f9ddb-339">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="f9ddb-339">RestoreOutputPath</span></span> | <span data-ttu-id="f9ddb-340">Pasta de saída que usa a pasta `obj` como padrão.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-340">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="f9ddb-341">Exemplos</span><span class="sxs-lookup"><span data-stu-id="f9ddb-341">Examples</span></span>

<span data-ttu-id="f9ddb-342">Linha de comando:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-342">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="f9ddb-343">Arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-343">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="f9ddb-344">Restaurar saídas</span><span class="sxs-lookup"><span data-stu-id="f9ddb-344">Restore outputs</span></span>

<span data-ttu-id="f9ddb-345">A restauração cria os seguintes arquivos na pasta `obj` de build:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-345">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="f9ddb-346">Arquivo</span><span class="sxs-lookup"><span data-stu-id="f9ddb-346">File</span></span> | <span data-ttu-id="f9ddb-347">Descrição</span><span class="sxs-lookup"><span data-stu-id="f9ddb-347">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="f9ddb-348">Contém o gráfico de dependência de todas as referências do pacote.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-348">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="f9ddb-349">Referências a objetos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="f9ddb-349">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="f9ddb-350">Referências a destinos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="f9ddb-350">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="f9ddb-351">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="f9ddb-351">PackageTargetFallback</span></span>

<span data-ttu-id="f9ddb-352">O elemento `PackageTargetFallback` permite especificar um conjunto de destinos compatíveis a serem usados ao restaurar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-352">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="f9ddb-353">Ele foi desenvolvido para permitir que os pacotes que usam o dotnet [TxM](../reference/target-frameworks.md) funcionem com pacotes compatíveis que não declaram um dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-353">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="f9ddb-354">Ou seja, se o projeto usar o dotnet TxM, todos os pacotes dos quais ele depende também deverão ter um dotnet TxM, a menos que você adicione o `<PackageTargetFallback>` ao projeto para permitir que plataformas não dotnet sejam compatíveis com o dotnet.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-354">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="f9ddb-355">Por exemplo, se o projeto está usando o `netstandard1.6` TxM e um pacote dependente contém apenas `lib/net45/a.dll` e `lib/portable-net45+win81/a.dll`, o projeto não será compilado.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-355">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="f9ddb-356">Se a DLL que você deseja colocar é esta última, é possível adicionar um `PackageTargetFallback` como mostrado a seguir para dizer que a DLL `portable-net45+win81` é compatível:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-356">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="f9ddb-357">Para declarar um fallback para todos os destinos em seu projeto, deixe o atributo `Condition` de fora.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-357">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="f9ddb-358">Você também pode estender qualquer `PackageTargetFallback` existente incluindo `$(PackageTargetFallback)` conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-358">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="f9ddb-359">Substituindo uma biblioteca de um grafo de restauração</span><span class="sxs-lookup"><span data-stu-id="f9ddb-359">Replacing one library from a restore graph</span></span>

<span data-ttu-id="f9ddb-360">Se uma restauração está trazendo o assembly errado, é possível excluir a escolha padrão do pacote e substituí-lo por outro de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="f9ddb-360">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="f9ddb-361">Primeiro com um `PackageReference` de nível superior, exclua todos os ativos:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-361">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="f9ddb-362">Em seguida, adicione sua própria referência à cópia local apropriada da DLL:</span><span class="sxs-lookup"><span data-stu-id="f9ddb-362">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
