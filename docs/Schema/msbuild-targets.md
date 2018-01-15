---
title: "Empacotamento e restauração do NuGet como destinos do MSBuild | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/3/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 86f7e724-2509-4d7d-aa8d-4a3fb913ded6
description: O pack e restore do NuGet podem funcionar diretamente como destinos do MSBuild com o NuGet 4.0 e superior.
keywords: NuGet e MSBuild, NuGet pack target, NuGet restore target
ms.reviewer: karann-msft
ms.openlocfilehash: d4778a21a96de6d76d7a20ff9a305960dd6c2bf1
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="a2ad8-104">Empacotamento e restauração do NuGet como destinos do MSBuild</span><span class="sxs-lookup"><span data-stu-id="a2ad8-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="a2ad8-105">*NuGet 4.0 ou superior*</span><span class="sxs-lookup"><span data-stu-id="a2ad8-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="a2ad8-106">O NuGet 4.0 e superior pode trabalhar diretamente com as informações em um arquivo `.csproj` sem a necessidade de um arquivo `.nuspec` ou `project.json` separado.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-106">NuGet 4.0+ can work directly with the information in a `.csproj` file without requiring a separate `.nuspec` or `project.json` file.</span></span> <span data-ttu-id="a2ad8-107">Todos os metadados anteriormente armazenados nesses arquivos de configuração podem ser armazenados no arquivo `.csproj` diretamente em vez disso, conforme descrito aqui.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-107">All the metadata that was previously stored in those configuration files can be instead stored in the `.csproj` file directly, as described here.</span></span>

<span data-ttu-id="a2ad8-108">Com o MSBuild 15.1 ou superior, o NuGet também é um cidadão de primeira classe do MSBuild com os destinos `pack` e `restore`, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-108">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="a2ad8-109">Esses destinos permitem que você trabalhe com o NuGet como faria com qualquer outra tarefa ou destino do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-109">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="a2ad8-110">(Para NuGet 3.x e anteriores, use os comandos [pack](../tools/cli-ref-pack.md) e [restore](../tools/cli-ref-restore.md) na CLI do NuGet.)</span><span class="sxs-lookup"><span data-stu-id="a2ad8-110">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

<span data-ttu-id="a2ad8-111">Neste tópico:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-111">In this topic:</span></span>

- [<span data-ttu-id="a2ad8-112">Ordem de build de destino</span><span class="sxs-lookup"><span data-stu-id="a2ad8-112">Target build order</span></span>](#target-build-order)
- [<span data-ttu-id="a2ad8-113">pack target</span><span class="sxs-lookup"><span data-stu-id="a2ad8-113">pack target</span></span>](#pack-target)
- [<span data-ttu-id="a2ad8-114">pack scenarios</span><span class="sxs-lookup"><span data-stu-id="a2ad8-114">pack scenarios</span></span>](#pack-scenarios)
- [<span data-ttu-id="a2ad8-115">restore target</span><span class="sxs-lookup"><span data-stu-id="a2ad8-115">restore target</span></span>](#restore-target)
- [<span data-ttu-id="a2ad8-116">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="a2ad8-116">PackageTargetFallback</span></span>](#packagetargetfallback)

## <a name="target-build-order"></a><span data-ttu-id="a2ad8-117">Ordem de build de destino</span><span class="sxs-lookup"><span data-stu-id="a2ad8-117">Target build order</span></span>

<span data-ttu-id="a2ad8-118">Como `pack` e `restore` são os destinos do MSBuild, você pode acessá-los para melhorar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-118">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="a2ad8-119">Por exemplo, digamos que você deseja copiar o pacote para um compartilhamento de rede após empacotá-lo.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-119">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="a2ad8-120">Você pode fazer isso adicionando o seguinte ao seu arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-120">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="a2ad8-121">Da mesma forma, você pode gravar uma tarefa do MSBuild, escrever seu próprio destino e consumir propriedades do NuGet na tarefa de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-121">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="a2ad8-122">pack target</span><span class="sxs-lookup"><span data-stu-id="a2ad8-122">pack target</span></span>

<span data-ttu-id="a2ad8-123">Ao usar o pack target, ou seja, `msbuild /t:pack`, o MSBuild extrai suas entradas do arquivo `.csproj` em vez dos arquivos `project.json` ou `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-123">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the `.csproj` file rather than `project.json` or `.nuspec` files.</span></span> <span data-ttu-id="a2ad8-124">A tabela abaixo descreve as propriedades do MSBuild que podem ser adicionadas a um arquivo `.csproj` no primeiro nó `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-124">The table below describes the MSBuild properties that can be added to a `.csproj` file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="a2ad8-125">Você pode fazer essas edições facilmente no Visual Studio 2017 e posterior clicando com o botão direito do mouse no projeto e selecionando **Editar {project_name}** no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-125">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="a2ad8-126">Para sua conveniência, a tabela é organizada pela propriedade equivalente em um arquivo [`.nuspec` ](../schema/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="a2ad8-126">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../schema/nuspec.md).</span></span>

<span data-ttu-id="a2ad8-127">Observe que as propriedades `Owners` e `Summary` de `.nuspec` não são compatíveis com o MSBuild.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-127">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>


| <span data-ttu-id="a2ad8-128">Valor de atributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="a2ad8-128">Attribute/NuSpec Value</span></span> | <span data-ttu-id="a2ad8-129">Propriedade do MSBuild</span><span class="sxs-lookup"><span data-stu-id="a2ad8-129">MSBuild Property</span></span> | <span data-ttu-id="a2ad8-130">Padrão</span><span class="sxs-lookup"><span data-stu-id="a2ad8-130">Default</span></span> | <span data-ttu-id="a2ad8-131">Observações</span><span class="sxs-lookup"><span data-stu-id="a2ad8-131">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="a2ad8-132">Id</span><span class="sxs-lookup"><span data-stu-id="a2ad8-132">Id</span></span> | <span data-ttu-id="a2ad8-133">PackageId</span><span class="sxs-lookup"><span data-stu-id="a2ad8-133">PackageId</span></span> | <span data-ttu-id="a2ad8-134">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="a2ad8-134">AssemblyName</span></span> | <span data-ttu-id="a2ad8-135">$(AssemblyName) do MSBuild</span><span class="sxs-lookup"><span data-stu-id="a2ad8-135">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="a2ad8-136">Versão</span><span class="sxs-lookup"><span data-stu-id="a2ad8-136">Version</span></span> | <span data-ttu-id="a2ad8-137">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="a2ad8-137">PackageVersion</span></span> | <span data-ttu-id="a2ad8-138">Versão</span><span class="sxs-lookup"><span data-stu-id="a2ad8-138">Version</span></span> | <span data-ttu-id="a2ad8-139">Isso é compatível com semver, por exemplo “1.0.0”, “1.0.0-beta” ou “1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="a2ad8-139">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="a2ad8-140">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="a2ad8-140">VersionPrefix</span></span> | <span data-ttu-id="a2ad8-141">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="a2ad8-141">PackageVersionPrefix</span></span> | <span data-ttu-id="a2ad8-142">empty</span><span class="sxs-lookup"><span data-stu-id="a2ad8-142">empty</span></span> | <span data-ttu-id="a2ad8-143">A configuração PackageVersion substituirá PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="a2ad8-143">Setting PackageVersion will overwrite PackageVersionPrefix</span></span> |
| <span data-ttu-id="a2ad8-144">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="a2ad8-144">VersionSuffix</span></span> | <span data-ttu-id="a2ad8-145">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="a2ad8-145">PackageVersionSuffix</span></span> | <span data-ttu-id="a2ad8-146">empty</span><span class="sxs-lookup"><span data-stu-id="a2ad8-146">empty</span></span> | <span data-ttu-id="a2ad8-147">$(VersionSuffix) do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-147">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="a2ad8-148">A configuração PackageVersion substituirá PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="a2ad8-148">Setting PackageVersion will overwrite PackageVersionSuffix</span></span> | 
| <span data-ttu-id="a2ad8-149">Autores</span><span class="sxs-lookup"><span data-stu-id="a2ad8-149">Authors</span></span> | <span data-ttu-id="a2ad8-150">Autores</span><span class="sxs-lookup"><span data-stu-id="a2ad8-150">Authors</span></span> | <span data-ttu-id="a2ad8-151">Nome do usuário atual</span><span class="sxs-lookup"><span data-stu-id="a2ad8-151">Username of the current user</span></span> | |
| <span data-ttu-id="a2ad8-152">Proprietários</span><span class="sxs-lookup"><span data-stu-id="a2ad8-152">Owners</span></span> | <span data-ttu-id="a2ad8-153">N/D</span><span class="sxs-lookup"><span data-stu-id="a2ad8-153">N/A</span></span> | <span data-ttu-id="a2ad8-154">Não está presente no NuSpec</span><span class="sxs-lookup"><span data-stu-id="a2ad8-154">Not present in NuSpec</span></span> | |
| <span data-ttu-id="a2ad8-155">Título</span><span class="sxs-lookup"><span data-stu-id="a2ad8-155">Title</span></span> | <span data-ttu-id="a2ad8-156">Título</span><span class="sxs-lookup"><span data-stu-id="a2ad8-156">Title</span></span> | <span data-ttu-id="a2ad8-157">O PackageId</span><span class="sxs-lookup"><span data-stu-id="a2ad8-157">The PackageId</span></span>| |
| <span data-ttu-id="a2ad8-158">Descrição</span><span class="sxs-lookup"><span data-stu-id="a2ad8-158">Description</span></span> | <span data-ttu-id="a2ad8-159">Descrição</span><span class="sxs-lookup"><span data-stu-id="a2ad8-159">Description</span></span> | <span data-ttu-id="a2ad8-160">“Package Description”</span><span class="sxs-lookup"><span data-stu-id="a2ad8-160">"Package Description"</span></span> | |
| <span data-ttu-id="a2ad8-161">Copyright</span><span class="sxs-lookup"><span data-stu-id="a2ad8-161">Copyright</span></span> | <span data-ttu-id="a2ad8-162">Copyright</span><span class="sxs-lookup"><span data-stu-id="a2ad8-162">Copyright</span></span> | <span data-ttu-id="a2ad8-163">empty</span><span class="sxs-lookup"><span data-stu-id="a2ad8-163">empty</span></span> | |
| <span data-ttu-id="a2ad8-164">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="a2ad8-164">RequireLicenseAcceptance</span></span> | <span data-ttu-id="a2ad8-165">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="a2ad8-165">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="a2ad8-166">false</span><span class="sxs-lookup"><span data-stu-id="a2ad8-166">false</span></span> | |
| <span data-ttu-id="a2ad8-167">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="a2ad8-167">LicenseUrl</span></span> | <span data-ttu-id="a2ad8-168">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="a2ad8-168">PackageLicenseUrl</span></span> | <span data-ttu-id="a2ad8-169">empty</span><span class="sxs-lookup"><span data-stu-id="a2ad8-169">empty</span></span> | |
| <span data-ttu-id="a2ad8-170">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="a2ad8-170">ProjectUrl</span></span> | <span data-ttu-id="a2ad8-171">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="a2ad8-171">PackageProjectUrl</span></span> | <span data-ttu-id="a2ad8-172">empty</span><span class="sxs-lookup"><span data-stu-id="a2ad8-172">empty</span></span> | |
| <span data-ttu-id="a2ad8-173">IconUrl</span><span class="sxs-lookup"><span data-stu-id="a2ad8-173">IconUrl</span></span> | <span data-ttu-id="a2ad8-174">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="a2ad8-174">PackageIconUrl</span></span> | <span data-ttu-id="a2ad8-175">empty</span><span class="sxs-lookup"><span data-stu-id="a2ad8-175">empty</span></span> | |
| <span data-ttu-id="a2ad8-176">Marcas</span><span class="sxs-lookup"><span data-stu-id="a2ad8-176">Tags</span></span> | <span data-ttu-id="a2ad8-177">PackageTags</span><span class="sxs-lookup"><span data-stu-id="a2ad8-177">PackageTags</span></span> | <span data-ttu-id="a2ad8-178">empty</span><span class="sxs-lookup"><span data-stu-id="a2ad8-178">empty</span></span> | <span data-ttu-id="a2ad8-179">Marcas são delimitadas por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-179">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="a2ad8-180">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="a2ad8-180">ReleaseNotes</span></span> | <span data-ttu-id="a2ad8-181">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="a2ad8-181">PackageReleaseNotes</span></span> | <span data-ttu-id="a2ad8-182">empty</span><span class="sxs-lookup"><span data-stu-id="a2ad8-182">empty</span></span> | |
| <span data-ttu-id="a2ad8-183">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="a2ad8-183">RepositoryUrl</span></span> | <span data-ttu-id="a2ad8-184">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="a2ad8-184">RepositoryUrl</span></span> | <span data-ttu-id="a2ad8-185">empty</span><span class="sxs-lookup"><span data-stu-id="a2ad8-185">empty</span></span> | |
| <span data-ttu-id="a2ad8-186">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="a2ad8-186">RepositoryType</span></span> | <span data-ttu-id="a2ad8-187">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="a2ad8-187">RepositoryType</span></span> | <span data-ttu-id="a2ad8-188">empty</span><span class="sxs-lookup"><span data-stu-id="a2ad8-188">empty</span></span> | |
| <span data-ttu-id="a2ad8-189">PackageType</span><span class="sxs-lookup"><span data-stu-id="a2ad8-189">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="a2ad8-190">Resumo</span><span class="sxs-lookup"><span data-stu-id="a2ad8-190">Summary</span></span> | <span data-ttu-id="a2ad8-191">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="a2ad8-191">Not supported</span></span> | | |


### <a name="pack-target-inputs"></a><span data-ttu-id="a2ad8-192">pack target inputs</span><span class="sxs-lookup"><span data-stu-id="a2ad8-192">pack target inputs</span></span>

- <span data-ttu-id="a2ad8-193">IsPackable</span><span class="sxs-lookup"><span data-stu-id="a2ad8-193">IsPackable</span></span>
- <span data-ttu-id="a2ad8-194">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="a2ad8-194">PackageVersion</span></span>
- <span data-ttu-id="a2ad8-195">PackageId</span><span class="sxs-lookup"><span data-stu-id="a2ad8-195">PackageId</span></span>
- <span data-ttu-id="a2ad8-196">Autores</span><span class="sxs-lookup"><span data-stu-id="a2ad8-196">Authors</span></span>
- <span data-ttu-id="a2ad8-197">Descrição</span><span class="sxs-lookup"><span data-stu-id="a2ad8-197">Description</span></span>
- <span data-ttu-id="a2ad8-198">Copyright</span><span class="sxs-lookup"><span data-stu-id="a2ad8-198">Copyright</span></span>
- <span data-ttu-id="a2ad8-199">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="a2ad8-199">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="a2ad8-200">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="a2ad8-200">DevelopmentDependency</span></span>
- <span data-ttu-id="a2ad8-201">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="a2ad8-201">PackageLicenseUrl</span></span>
- <span data-ttu-id="a2ad8-202">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="a2ad8-202">PackageProjectUrl</span></span>
- <span data-ttu-id="a2ad8-203">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="a2ad8-203">PackageIconUrl</span></span>
- <span data-ttu-id="a2ad8-204">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="a2ad8-204">PackageReleaseNotes</span></span>
- <span data-ttu-id="a2ad8-205">PackageTags</span><span class="sxs-lookup"><span data-stu-id="a2ad8-205">PackageTags</span></span>
- <span data-ttu-id="a2ad8-206">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="a2ad8-206">PackageOutputPath</span></span>
- <span data-ttu-id="a2ad8-207">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="a2ad8-207">IncludeSymbols</span></span>
- <span data-ttu-id="a2ad8-208">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="a2ad8-208">IncludeSource</span></span>
- <span data-ttu-id="a2ad8-209">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="a2ad8-209">PackageTypes</span></span>
- <span data-ttu-id="a2ad8-210">IsTool</span><span class="sxs-lookup"><span data-stu-id="a2ad8-210">IsTool</span></span>
- <span data-ttu-id="a2ad8-211">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="a2ad8-211">RepositoryUrl</span></span>
- <span data-ttu-id="a2ad8-212">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="a2ad8-212">RepositoryType</span></span>
- <span data-ttu-id="a2ad8-213">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="a2ad8-213">NoPackageAnalysis</span></span>
- <span data-ttu-id="a2ad8-214">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="a2ad8-214">MinClientVersion</span></span>
- <span data-ttu-id="a2ad8-215">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="a2ad8-215">IncludeBuildOutput</span></span>
- <span data-ttu-id="a2ad8-216">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="a2ad8-216">IncludeContentInPack</span></span>
- <span data-ttu-id="a2ad8-217">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="a2ad8-217">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="a2ad8-218">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="a2ad8-218">ContentTargetFolders</span></span>
- <span data-ttu-id="a2ad8-219">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="a2ad8-219">NuspecFile</span></span>
- <span data-ttu-id="a2ad8-220">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="a2ad8-220">NuspecBasePath</span></span>
- <span data-ttu-id="a2ad8-221">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="a2ad8-221">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="a2ad8-222">pack scenarios</span><span class="sxs-lookup"><span data-stu-id="a2ad8-222">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="a2ad8-223">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="a2ad8-223">PackageIconUrl</span></span>

<span data-ttu-id="a2ad8-224">Como parte da alteração para o [Problema do NuGet 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` eventualmente será alterado para `PackageIconUri` e pode ser um caminho relativo para um arquivo de ícone que será incluído na raiz do pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-224">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="a2ad8-225">Assemblies de saída</span><span class="sxs-lookup"><span data-stu-id="a2ad8-225">Output assemblies</span></span>

<span data-ttu-id="a2ad8-226">O `nuget pack` copia arquivos de saída com extensões `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-226">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="a2ad8-227">Os arquivos de saída que são copiados dependem do que o MSBuild fornece do destino `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-227">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="a2ad8-228">Há duas propriedades de MSBuild que você pode usar em seu arquivo de projeto ou a linha de comando para controlar onde ficam os assemblies de saída:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-228">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="a2ad8-229">`IncludeBuildOutput`: um valor booliano que determina se os assemblies de saída de build devem ser incluídos no pacote.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-229">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="a2ad8-230">`BuildOutputTargetFolder`: especifica a pasta na qual os assemblies de saída devem ser colocados.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-230">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="a2ad8-231">Os assemblies de saída (e outros arquivos de saída) são copiados para suas respectivas pastas de estrutura.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-231">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="a2ad8-232">Referências de pacote</span><span class="sxs-lookup"><span data-stu-id="a2ad8-232">Package references</span></span>

<span data-ttu-id="a2ad8-233">Consulte [Referências de pacote em arquivos de projeto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="a2ad8-233">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="a2ad8-234">Referências de projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="a2ad8-234">Project to project references</span></span>

<span data-ttu-id="a2ad8-235">As referências projeto a projeto são consideradas como referências de pacote do nuget por padrão, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-235">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="a2ad8-236">Você também pode adicionar os seguintes metadados à referência de projeto:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-236">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="a2ad8-237">Incluindo o conteúdo em um pacote</span><span class="sxs-lookup"><span data-stu-id="a2ad8-237">Including content in a package</span></span>

<span data-ttu-id="a2ad8-238">Para incluir o conteúdo, adicione metadados extras ao item `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-238">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="a2ad8-239">Por padrão, tudo que pertencer ao tipo “Conteúdo” é incluído no pacote, a menos que seja substituído por entradas como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-239">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="a2ad8-240">Por padrão, tudo é adicionado à raiz da pasta `content` e `contentFiles\any\<target_framework>` dentro de um pacote e preserva a estrutura e pasta relativa, a menos que você especifique um caminho de pacote:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-240">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">        
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="a2ad8-241">Se você quiser copiar todo o conteúdo somente para determinadas pastas raiz (em vez de para `content` e `contentFiles`), será possível usar a propriedade `ContentTargetFolders` do MSBuild, que assume como padrão "content;contentFiles", mas pode ser definida como qualquer outro nome de pasta.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-241">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="a2ad8-242">Observe que só especificar “contentFiles” em `ContentTargetFolders` coloca os arquivos em `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` com base em `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-242">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="a2ad8-243">`PackagePath` pode ser um conjunto de caminhos de destino separados por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-243">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="a2ad8-244">Especificar um caminho de pacote vazio adicionaria o arquivo à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-244">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="a2ad8-245">Por exemplo, o seguinte adiciona `libuv.txt` a `content\myfiles`, `content\samples` e a raiz do pacote:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-245">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="a2ad8-246">Há também uma propriedade de MSBuild `$(IncludeContentInPack)`, que assume o padrão `true`.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-246">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="a2ad8-247">Se isso for definido como `false` em qualquer projeto, o conteúdo desse projeto não está incluso no pacote do nuget.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-247">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="a2ad8-248">Outros metadados específicos do pacote que pode ser definido em qualquer um dos itens acima ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, que define os valores ```CopyToOutput``` e ```Flatten``` na entrada ```contentFiles``` no nuspec de saída.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-248">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>


> [!Note]
> <span data-ttu-id="a2ad8-249">Além de itens de Conteúdo, os metadados `<Pack>` e `<PackagePath>` também podem ser definidos em arquivos com uma ação de Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-249">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="a2ad8-250">Para o pacote acrescentar o nome de arquivo ao caminho do pacote ao usar padrões glob, seu caminho de pacote deve terminar com o caractere separador de pasta, caso contrário, o caminho do pacote será tratado como o caminho completo, incluindo o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-250">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="a2ad8-251">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="a2ad8-251">IncludeSymbols</span></span>

<span data-ttu-id="a2ad8-252">Ao usar o `MSBuild /t:pack /p:IncludeSymbols=true`, os arquivos `.pdb` correspondentes são copiados junto com outros arquivos de saída (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="a2ad8-252">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="a2ad8-253">Observe que a configuração `IncludeSymbols=true` cria um pacote regular *e* um pacote de símbolos.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-253">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="a2ad8-254">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="a2ad8-254">IncludeSource</span></span>

<span data-ttu-id="a2ad8-255">Isso é o mesmo que `IncludeSymbols`, exceto que também copia os arquivos de origem com arquivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-255">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="a2ad8-256">Todos os arquivos do tipo `Compile` são copiadas para `src\<ProjectName>\`, preservando a estrutura de pastas do caminho relativo no pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-256">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="a2ad8-257">O mesmo também ocorre para arquivos de origem de qualquer `ProjectReference` que tem `TreatAsPackageReference` definido como `false`.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-257">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="a2ad8-258">Se um arquivo do tipo Compilação estiver fora da pasta de projeto, ele será adicionado apenas a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-258">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="a2ad8-259">IsTool</span><span class="sxs-lookup"><span data-stu-id="a2ad8-259">IsTool</span></span>

<span data-ttu-id="a2ad8-260">Ao usar `MSBuild /t:pack /p:IsTool=true`, todos os arquivos de saída, conforme especificado no cenário [Assemblies de saída](#output-assemblies), são copiados para a pasta `tools` em vez da pasta `lib`.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-260">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="a2ad8-261">Observe que isso é diferente de um `DotNetCliTool` que é especificado pela configuração do `PackageType` no arquivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-261">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="a2ad8-262">Empacotamento usando um .nuspec</span><span class="sxs-lookup"><span data-stu-id="a2ad8-262">Packing using a .nuspec</span></span>

<span data-ttu-id="a2ad8-263">Você pode usar um arquivo `.nuspec` para empacotar seu projeto desde que tenha um arquivo de projeto para importar `NuGet.Build.Tasks.Pack.targets` a fim de executar a tarefa de empacotamento.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-263">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="a2ad8-264">As três propriedades MSBuild a seguir são relevantes para empacotamento usando um `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-264">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="a2ad8-265">`NuspecFile`: caminho relativo ou absoluto para o arquivo `.nuspec` que está sendo usado para o empacotamento.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-265">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="a2ad8-266">`NuspecProperties`: uma lista separada por ponto e vírgula de pares chave/valor.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-266">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="a2ad8-267">Devido à maneira como a análise de linha de comando do MSBuild funciona, várias propriedades precisam ser especificadas da seguinte maneira: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-267">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="a2ad8-268">`NuspecBasePath`: o caminho base para o arquivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-268">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="a2ad8-269">Se estiver usando `dotnet.exe` para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-269">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="a2ad8-270">Se estiver usando o MSBuild para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-270">If using MSBuild to pack your project, use a command like the following:</span></span>

```
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="a2ad8-271">restore target</span><span class="sxs-lookup"><span data-stu-id="a2ad8-271">restore target</span></span>

<span data-ttu-id="a2ad8-272">`MSBuild /t:restore` (que `nuget restore` e `dotnet restore` usam com projetos do .NET Core), restaura pacotes referenciados no arquivo de projeto da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-272">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="a2ad8-273">Ler todas as referências projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="a2ad8-273">Read all project to project references</span></span>
1. <span data-ttu-id="a2ad8-274">Ler as propriedades do projeto para localizar a pasta intermediária e as estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="a2ad8-274">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="a2ad8-275">Passar dados do msbuild para NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="a2ad8-275">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="a2ad8-276">Executar restauração</span><span class="sxs-lookup"><span data-stu-id="a2ad8-276">Run restore</span></span>
1. <span data-ttu-id="a2ad8-277">Baixar os pacotes</span><span class="sxs-lookup"><span data-stu-id="a2ad8-277">Download packages</span></span>
1. <span data-ttu-id="a2ad8-278">Gravar arquivo de ativos, destinos e objetos</span><span class="sxs-lookup"><span data-stu-id="a2ad8-278">Write assets file, targets, and props</span></span>


### <a name="restore-properties"></a><span data-ttu-id="a2ad8-279">Restaurar propriedades</span><span class="sxs-lookup"><span data-stu-id="a2ad8-279">Restore properties</span></span>

<span data-ttu-id="a2ad8-280">Configurações de restauração adicionais podem vir de propriedades MSBuild no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-280">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="a2ad8-281">Os valores também podem ser definidos na linha de comando usando a opção `/p:` (consulte os Exemplos abaixo).</span><span class="sxs-lookup"><span data-stu-id="a2ad8-281">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="a2ad8-282">propriedade</span><span class="sxs-lookup"><span data-stu-id="a2ad8-282">Property</span></span> | <span data-ttu-id="a2ad8-283">Descrição</span><span class="sxs-lookup"><span data-stu-id="a2ad8-283">Description</span></span> |
|--------|--------|
| <span data-ttu-id="a2ad8-284">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="a2ad8-284">RestoreSources</span></span> | <span data-ttu-id="a2ad8-285">Uma lista delimitada por ponto e vírgula de origens de pacote.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-285">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="a2ad8-286">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="a2ad8-286">RestorePackagesPath</span></span> | <span data-ttu-id="a2ad8-287">Caminho da pasta dos pacotes do usuário.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-287">User packages folder path.</span></span> |
| <span data-ttu-id="a2ad8-288">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="a2ad8-288">RestoreDisableParallel</span></span> | <span data-ttu-id="a2ad8-289">Limite os downloads para um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-289">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="a2ad8-290">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="a2ad8-290">RestoreConfigFile</span></span> | <span data-ttu-id="a2ad8-291">Caminho para um arquivo `Nuget.Config` a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-291">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="a2ad8-292">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="a2ad8-292">RestoreNoCache</span></span> | <span data-ttu-id="a2ad8-293">Se verdadeiro, evita o uso de cache da Web.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-293">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="a2ad8-294">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="a2ad8-294">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="a2ad8-295">Se verdadeiro, ignora origens de pacote com falha ou ausentes.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-295">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="a2ad8-296">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="a2ad8-296">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="a2ad8-297">Caminho para `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-297">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="a2ad8-298">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="a2ad8-298">RestoreGraphProjectInput</span></span> | <span data-ttu-id="a2ad8-299">Lista separada por ponto e vírgula de projetos a serem restaurados, que devem conter caminhos absolutos.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-299">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="a2ad8-300">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="a2ad8-300">RestoreOutputPath</span></span> | <span data-ttu-id="a2ad8-301">Pasta de saída que usa a pasta `obj` como padrão.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-301">Output folder, defaulting to the `obj` folder.</span></span> |

<span data-ttu-id="a2ad8-302">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="a2ad8-302">**Examples**</span></span>

<span data-ttu-id="a2ad8-303">Linha de comando:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-303">Command line:</span></span>

```
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="a2ad8-304">Arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-304">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="a2ad8-305">Restaurar saídas</span><span class="sxs-lookup"><span data-stu-id="a2ad8-305">Restore outputs</span></span>

<span data-ttu-id="a2ad8-306">A restauração cria os seguintes arquivos na pasta `obj` de build:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-306">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="a2ad8-307">Arquivo</span><span class="sxs-lookup"><span data-stu-id="a2ad8-307">File</span></span> | <span data-ttu-id="a2ad8-308">Descrição</span><span class="sxs-lookup"><span data-stu-id="a2ad8-308">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="a2ad8-309">Anteriormente `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="a2ad8-309">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="a2ad8-310">Referências a objetos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="a2ad8-310">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="a2ad8-311">Referências a destinos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="a2ad8-311">References to MSBuild targets contained in packages</span></span> |


### <a name="packagetargetfallback"></a><span data-ttu-id="a2ad8-312">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="a2ad8-312">PackageTargetFallback</span></span> 

<span data-ttu-id="a2ad8-313">O elemento `PackageTargetFallback` permite especificar um conjunto de destinos compatíveis a serem usados ao restaurar os pacotes (o equivalente de [`imports` em `project.json`](../schema/project-json.md#imports)).</span><span class="sxs-lookup"><span data-stu-id="a2ad8-313">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages (the equivalent of [`imports` in `project.json`](../schema/project-json.md#imports)).</span></span> <span data-ttu-id="a2ad8-314">Ele foi desenvolvido para permitir que os pacotes que usam o dotnet [TxM](../schema/target-frameworks.md) funcionem com pacotes compatíveis que não declaram um dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-314">It's designed to allow packages that use a dotnet [TxM](../schema/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="a2ad8-315">Ou seja, se o projeto usar o dotnet TxM, todos os pacotes dos quais ele depende também deverão ter um dotnet TxM, a menos que você adicione o `<PackageTargetFallback>` ao projeto para permitir que plataformas não dotnet sejam compatíveis com o dotnet.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-315">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span> 

<span data-ttu-id="a2ad8-316">Por exemplo, se o projeto está usando o `netstandard1.6` TxM e um pacote dependente contém apenas `lib/net45/a.dll` e `lib/portable-net45+win81/a.dll`, o projeto não será compilado.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-316">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="a2ad8-317">Se a DLL que você deseja colocar é esta última, é possível adicionar um `PackageTargetFallback` como mostrado a seguir para dizer que a DLL `portable-net45+win81` é compatível:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-317">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="a2ad8-318">Para declarar um fallback para todos os destinos em seu projeto, deixe o atributo `Condition` de fora.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-318">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="a2ad8-319">Você também pode estender qualquer `PackageTargetFallback` existente incluindo `$(PackageTargetFallback)` conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-319">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```


### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="a2ad8-320">Substituindo uma biblioteca de um grafo de restauração</span><span class="sxs-lookup"><span data-stu-id="a2ad8-320">Replacing one library from a restore graph</span></span>

<span data-ttu-id="a2ad8-321">Se uma restauração está trazendo o assembly errado, é possível excluir a escolha padrão do pacote e substituí-lo por outro de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="a2ad8-321">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="a2ad8-322">Primeiro com um `PackageReference` de nível superior, exclua todos os ativos:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-322">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="a2ad8-323">Em seguida, adicione sua própria referência à cópia local apropriada da DLL:</span><span class="sxs-lookup"><span data-stu-id="a2ad8-323">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
