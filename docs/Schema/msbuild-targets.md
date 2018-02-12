---
title: "Empacotamento e restauração do NuGet como destinos do MSBuild | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: O pack e restore do NuGet podem funcionar diretamente como destinos do MSBuild com o NuGet 4.0 e superior.
keywords: NuGet e MSBuild, NuGet pack target, NuGet restore target
ms.reviewer:
- karann-msft
ms.openlocfilehash: 169d73709eeb17aade7d99da66bbb4f346f8093f
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="99fd0-104">Empacotamento e restauração do NuGet como destinos do MSBuild</span><span class="sxs-lookup"><span data-stu-id="99fd0-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="99fd0-105">*NuGet 4.0 ou superior*</span><span class="sxs-lookup"><span data-stu-id="99fd0-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="99fd0-106">Com o formato PackageReference, o NuGet 4.0 e posterior pode armazenar todos os metadados de manifesto diretamente dentro de um arquivo de projeto em vez de usar um arquivo `.nuspec` separado.</span><span class="sxs-lookup"><span data-stu-id="99fd0-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="99fd0-107">Com o MSBuild 15.1 ou superior, o NuGet também é um cidadão de primeira classe do MSBuild com os destinos `pack` e `restore`, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="99fd0-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="99fd0-108">Esses destinos permitem que você trabalhe com o NuGet como faria com qualquer outra tarefa ou destino do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="99fd0-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="99fd0-109">(Para NuGet 3.x e anteriores, use os comandos [pack](../tools/cli-ref-pack.md) e [restore](../tools/cli-ref-restore.md) na CLI do NuGet.)</span><span class="sxs-lookup"><span data-stu-id="99fd0-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="99fd0-110">Ordem de build de destino</span><span class="sxs-lookup"><span data-stu-id="99fd0-110">Target build order</span></span>

<span data-ttu-id="99fd0-111">Como `pack` e `restore` são os destinos do MSBuild, você pode acessá-los para melhorar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="99fd0-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="99fd0-112">Por exemplo, digamos que você deseja copiar o pacote para um compartilhamento de rede após empacotá-lo.</span><span class="sxs-lookup"><span data-stu-id="99fd0-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="99fd0-113">Você pode fazer isso adicionando o seguinte ao seu arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="99fd0-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="99fd0-114">Da mesma forma, você pode gravar uma tarefa do MSBuild, escrever seu próprio destino e consumir propriedades do NuGet na tarefa de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="99fd0-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="99fd0-115">pack target</span><span class="sxs-lookup"><span data-stu-id="99fd0-115">pack target</span></span>

<span data-ttu-id="99fd0-116">Ao usar pack target, ou seja, `msbuild /t:pack`, o MSBuild extrai suas entradas do arquivo do projeto.</span><span class="sxs-lookup"><span data-stu-id="99fd0-116">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the project file.</span></span> <span data-ttu-id="99fd0-117">A tabela abaixo descreve as propriedades do MSBuild que podem ser adicionadas a um arquivo do projeto dentro do primeiro nó `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="99fd0-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="99fd0-118">Você pode fazer essas edições facilmente no Visual Studio 2017 e posterior clicando com o botão direito do mouse no projeto e selecionando **Editar {project_name}** no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="99fd0-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="99fd0-119">Para sua conveniência, a tabela é organizada pela propriedade equivalente em um arquivo [`.nuspec` ](../schema/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="99fd0-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../schema/nuspec.md).</span></span>

<span data-ttu-id="99fd0-120">Observe que as propriedades `Owners` e `Summary` de `.nuspec` não são compatíveis com o MSBuild.</span><span class="sxs-lookup"><span data-stu-id="99fd0-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="99fd0-121">Valor de atributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="99fd0-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="99fd0-122">Propriedade do MSBuild</span><span class="sxs-lookup"><span data-stu-id="99fd0-122">MSBuild Property</span></span> | <span data-ttu-id="99fd0-123">Padrão</span><span class="sxs-lookup"><span data-stu-id="99fd0-123">Default</span></span> | <span data-ttu-id="99fd0-124">Observações</span><span class="sxs-lookup"><span data-stu-id="99fd0-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="99fd0-125">Id</span><span class="sxs-lookup"><span data-stu-id="99fd0-125">Id</span></span> | <span data-ttu-id="99fd0-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="99fd0-126">PackageId</span></span> | <span data-ttu-id="99fd0-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="99fd0-127">AssemblyName</span></span> | <span data-ttu-id="99fd0-128">$(AssemblyName) do MSBuild</span><span class="sxs-lookup"><span data-stu-id="99fd0-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="99fd0-129">Versão</span><span class="sxs-lookup"><span data-stu-id="99fd0-129">Version</span></span> | <span data-ttu-id="99fd0-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="99fd0-130">PackageVersion</span></span> | <span data-ttu-id="99fd0-131">Versão</span><span class="sxs-lookup"><span data-stu-id="99fd0-131">Version</span></span> | <span data-ttu-id="99fd0-132">Isso é compatível com semver, por exemplo “1.0.0”, “1.0.0-beta” ou “1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="99fd0-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="99fd0-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="99fd0-133">VersionPrefix</span></span> | <span data-ttu-id="99fd0-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="99fd0-134">PackageVersionPrefix</span></span> | <span data-ttu-id="99fd0-135">empty</span><span class="sxs-lookup"><span data-stu-id="99fd0-135">empty</span></span> | <span data-ttu-id="99fd0-136">A configuração PackageVersion substitui PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="99fd0-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="99fd0-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="99fd0-137">VersionSuffix</span></span> | <span data-ttu-id="99fd0-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="99fd0-138">PackageVersionSuffix</span></span> | <span data-ttu-id="99fd0-139">empty</span><span class="sxs-lookup"><span data-stu-id="99fd0-139">empty</span></span> | <span data-ttu-id="99fd0-140">$(VersionSuffix) do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="99fd0-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="99fd0-141">A configuração PackageVersion substitui PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="99fd0-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="99fd0-142">Autores</span><span class="sxs-lookup"><span data-stu-id="99fd0-142">Authors</span></span> | <span data-ttu-id="99fd0-143">Autores</span><span class="sxs-lookup"><span data-stu-id="99fd0-143">Authors</span></span> | <span data-ttu-id="99fd0-144">Nome do usuário atual</span><span class="sxs-lookup"><span data-stu-id="99fd0-144">Username of the current user</span></span> | |
| <span data-ttu-id="99fd0-145">Proprietários</span><span class="sxs-lookup"><span data-stu-id="99fd0-145">Owners</span></span> | <span data-ttu-id="99fd0-146">N/D</span><span class="sxs-lookup"><span data-stu-id="99fd0-146">N/A</span></span> | <span data-ttu-id="99fd0-147">Não está presente no NuSpec</span><span class="sxs-lookup"><span data-stu-id="99fd0-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="99fd0-148">Título</span><span class="sxs-lookup"><span data-stu-id="99fd0-148">Title</span></span> | <span data-ttu-id="99fd0-149">Título</span><span class="sxs-lookup"><span data-stu-id="99fd0-149">Title</span></span> | <span data-ttu-id="99fd0-150">O PackageId</span><span class="sxs-lookup"><span data-stu-id="99fd0-150">The PackageId</span></span>| |
| <span data-ttu-id="99fd0-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="99fd0-151">Description</span></span> | <span data-ttu-id="99fd0-152">Descrição</span><span class="sxs-lookup"><span data-stu-id="99fd0-152">Description</span></span> | <span data-ttu-id="99fd0-153">“Package Description”</span><span class="sxs-lookup"><span data-stu-id="99fd0-153">"Package Description"</span></span> | |
| <span data-ttu-id="99fd0-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="99fd0-154">Copyright</span></span> | <span data-ttu-id="99fd0-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="99fd0-155">Copyright</span></span> | <span data-ttu-id="99fd0-156">empty</span><span class="sxs-lookup"><span data-stu-id="99fd0-156">empty</span></span> | |
| <span data-ttu-id="99fd0-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="99fd0-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="99fd0-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="99fd0-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="99fd0-159">false</span><span class="sxs-lookup"><span data-stu-id="99fd0-159">false</span></span> | |
| <span data-ttu-id="99fd0-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="99fd0-160">LicenseUrl</span></span> | <span data-ttu-id="99fd0-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="99fd0-161">PackageLicenseUrl</span></span> | <span data-ttu-id="99fd0-162">empty</span><span class="sxs-lookup"><span data-stu-id="99fd0-162">empty</span></span> | |
| <span data-ttu-id="99fd0-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="99fd0-163">ProjectUrl</span></span> | <span data-ttu-id="99fd0-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="99fd0-164">PackageProjectUrl</span></span> | <span data-ttu-id="99fd0-165">empty</span><span class="sxs-lookup"><span data-stu-id="99fd0-165">empty</span></span> | |
| <span data-ttu-id="99fd0-166">IconUrl</span><span class="sxs-lookup"><span data-stu-id="99fd0-166">IconUrl</span></span> | <span data-ttu-id="99fd0-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="99fd0-167">PackageIconUrl</span></span> | <span data-ttu-id="99fd0-168">empty</span><span class="sxs-lookup"><span data-stu-id="99fd0-168">empty</span></span> | |
| <span data-ttu-id="99fd0-169">Marcas</span><span class="sxs-lookup"><span data-stu-id="99fd0-169">Tags</span></span> | <span data-ttu-id="99fd0-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="99fd0-170">PackageTags</span></span> | <span data-ttu-id="99fd0-171">empty</span><span class="sxs-lookup"><span data-stu-id="99fd0-171">empty</span></span> | <span data-ttu-id="99fd0-172">Marcas são delimitadas por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="99fd0-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="99fd0-173">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="99fd0-173">ReleaseNotes</span></span> | <span data-ttu-id="99fd0-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="99fd0-174">PackageReleaseNotes</span></span> | <span data-ttu-id="99fd0-175">empty</span><span class="sxs-lookup"><span data-stu-id="99fd0-175">empty</span></span> | |
| <span data-ttu-id="99fd0-176">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="99fd0-176">RepositoryUrl</span></span> | <span data-ttu-id="99fd0-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="99fd0-177">RepositoryUrl</span></span> | <span data-ttu-id="99fd0-178">empty</span><span class="sxs-lookup"><span data-stu-id="99fd0-178">empty</span></span> | |
| <span data-ttu-id="99fd0-179">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="99fd0-179">RepositoryType</span></span> | <span data-ttu-id="99fd0-180">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="99fd0-180">RepositoryType</span></span> | <span data-ttu-id="99fd0-181">empty</span><span class="sxs-lookup"><span data-stu-id="99fd0-181">empty</span></span> | |
| <span data-ttu-id="99fd0-182">PackageType</span><span class="sxs-lookup"><span data-stu-id="99fd0-182">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="99fd0-183">Resumo</span><span class="sxs-lookup"><span data-stu-id="99fd0-183">Summary</span></span> | <span data-ttu-id="99fd0-184">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="99fd0-184">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="99fd0-185">pack target inputs</span><span class="sxs-lookup"><span data-stu-id="99fd0-185">pack target inputs</span></span>

- <span data-ttu-id="99fd0-186">IsPackable</span><span class="sxs-lookup"><span data-stu-id="99fd0-186">IsPackable</span></span>
- <span data-ttu-id="99fd0-187">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="99fd0-187">PackageVersion</span></span>
- <span data-ttu-id="99fd0-188">PackageId</span><span class="sxs-lookup"><span data-stu-id="99fd0-188">PackageId</span></span>
- <span data-ttu-id="99fd0-189">Autores</span><span class="sxs-lookup"><span data-stu-id="99fd0-189">Authors</span></span>
- <span data-ttu-id="99fd0-190">Descrição</span><span class="sxs-lookup"><span data-stu-id="99fd0-190">Description</span></span>
- <span data-ttu-id="99fd0-191">Copyright</span><span class="sxs-lookup"><span data-stu-id="99fd0-191">Copyright</span></span>
- <span data-ttu-id="99fd0-192">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="99fd0-192">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="99fd0-193">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="99fd0-193">DevelopmentDependency</span></span>
- <span data-ttu-id="99fd0-194">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="99fd0-194">PackageLicenseUrl</span></span>
- <span data-ttu-id="99fd0-195">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="99fd0-195">PackageProjectUrl</span></span>
- <span data-ttu-id="99fd0-196">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="99fd0-196">PackageIconUrl</span></span>
- <span data-ttu-id="99fd0-197">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="99fd0-197">PackageReleaseNotes</span></span>
- <span data-ttu-id="99fd0-198">PackageTags</span><span class="sxs-lookup"><span data-stu-id="99fd0-198">PackageTags</span></span>
- <span data-ttu-id="99fd0-199">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="99fd0-199">PackageOutputPath</span></span>
- <span data-ttu-id="99fd0-200">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="99fd0-200">IncludeSymbols</span></span>
- <span data-ttu-id="99fd0-201">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="99fd0-201">IncludeSource</span></span>
- <span data-ttu-id="99fd0-202">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="99fd0-202">PackageTypes</span></span>
- <span data-ttu-id="99fd0-203">IsTool</span><span class="sxs-lookup"><span data-stu-id="99fd0-203">IsTool</span></span>
- <span data-ttu-id="99fd0-204">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="99fd0-204">RepositoryUrl</span></span>
- <span data-ttu-id="99fd0-205">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="99fd0-205">RepositoryType</span></span>
- <span data-ttu-id="99fd0-206">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="99fd0-206">NoPackageAnalysis</span></span>
- <span data-ttu-id="99fd0-207">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="99fd0-207">MinClientVersion</span></span>
- <span data-ttu-id="99fd0-208">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="99fd0-208">IncludeBuildOutput</span></span>
- <span data-ttu-id="99fd0-209">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="99fd0-209">IncludeContentInPack</span></span>
- <span data-ttu-id="99fd0-210">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="99fd0-210">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="99fd0-211">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="99fd0-211">ContentTargetFolders</span></span>
- <span data-ttu-id="99fd0-212">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="99fd0-212">NuspecFile</span></span>
- <span data-ttu-id="99fd0-213">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="99fd0-213">NuspecBasePath</span></span>
- <span data-ttu-id="99fd0-214">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="99fd0-214">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="99fd0-215">pack scenarios</span><span class="sxs-lookup"><span data-stu-id="99fd0-215">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="99fd0-216">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="99fd0-216">PackageIconUrl</span></span>

<span data-ttu-id="99fd0-217">Como parte da alteração para o [Problema do NuGet 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` eventualmente será alterado para `PackageIconUri` e pode ser um caminho relativo para um arquivo de ícone que será incluído na raiz do pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="99fd0-217">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="99fd0-218">Assemblies de saída</span><span class="sxs-lookup"><span data-stu-id="99fd0-218">Output assemblies</span></span>

<span data-ttu-id="99fd0-219">O `nuget pack` copia arquivos de saída com extensões `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="99fd0-219">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="99fd0-220">Os arquivos de saída que são copiados dependem do que o MSBuild fornece do destino `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="99fd0-220">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="99fd0-221">Há duas propriedades de MSBuild que você pode usar em seu arquivo de projeto ou a linha de comando para controlar onde ficam os assemblies de saída:</span><span class="sxs-lookup"><span data-stu-id="99fd0-221">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="99fd0-222">`IncludeBuildOutput`: um valor booliano que determina se os assemblies de saída de build devem ser incluídos no pacote.</span><span class="sxs-lookup"><span data-stu-id="99fd0-222">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="99fd0-223">`BuildOutputTargetFolder`: especifica a pasta na qual os assemblies de saída devem ser colocados.</span><span class="sxs-lookup"><span data-stu-id="99fd0-223">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="99fd0-224">Os assemblies de saída (e outros arquivos de saída) são copiados para suas respectivas pastas de estrutura.</span><span class="sxs-lookup"><span data-stu-id="99fd0-224">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="99fd0-225">Referências de pacote</span><span class="sxs-lookup"><span data-stu-id="99fd0-225">Package references</span></span>

<span data-ttu-id="99fd0-226">Consulte [Referências de pacote em arquivos de projeto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="99fd0-226">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="99fd0-227">Referências de projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="99fd0-227">Project to project references</span></span>

<span data-ttu-id="99fd0-228">As referências projeto a projeto são consideradas como referências de pacote do nuget por padrão, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="99fd0-228">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="99fd0-229">Você também pode adicionar os seguintes metadados à referência de projeto:</span><span class="sxs-lookup"><span data-stu-id="99fd0-229">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="99fd0-230">Incluindo o conteúdo em um pacote</span><span class="sxs-lookup"><span data-stu-id="99fd0-230">Including content in a package</span></span>

<span data-ttu-id="99fd0-231">Para incluir o conteúdo, adicione metadados extras ao item `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="99fd0-231">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="99fd0-232">Por padrão, tudo que pertencer ao tipo “Conteúdo” é incluído no pacote, a menos que seja substituído por entradas como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="99fd0-232">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="99fd0-233">Por padrão, tudo é adicionado à raiz da pasta `content` e `contentFiles\any\<target_framework>` dentro de um pacote e preserva a estrutura e pasta relativa, a menos que você especifique um caminho de pacote:</span><span class="sxs-lookup"><span data-stu-id="99fd0-233">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="99fd0-234">Se você quiser copiar todo o conteúdo somente para determinadas pastas raiz (em vez de para `content` e `contentFiles`), será possível usar a propriedade `ContentTargetFolders` do MSBuild, que assume como padrão "content;contentFiles", mas pode ser definida como qualquer outro nome de pasta.</span><span class="sxs-lookup"><span data-stu-id="99fd0-234">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="99fd0-235">Observe que só especificar “contentFiles” em `ContentTargetFolders` coloca os arquivos em `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` com base em `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="99fd0-235">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="99fd0-236">`PackagePath` pode ser um conjunto de caminhos de destino separados por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="99fd0-236">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="99fd0-237">Especificar um caminho de pacote vazio adicionaria o arquivo à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="99fd0-237">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="99fd0-238">Por exemplo, o seguinte adiciona `libuv.txt` a `content\myfiles`, `content\samples` e a raiz do pacote:</span><span class="sxs-lookup"><span data-stu-id="99fd0-238">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="99fd0-239">Há também uma propriedade de MSBuild `$(IncludeContentInPack)`, que assume o padrão `true`.</span><span class="sxs-lookup"><span data-stu-id="99fd0-239">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="99fd0-240">Se isso for definido como `false` em qualquer projeto, o conteúdo desse projeto não está incluso no pacote do nuget.</span><span class="sxs-lookup"><span data-stu-id="99fd0-240">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="99fd0-241">Outros metadados específicos do pacote que pode ser definido em qualquer um dos itens acima ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, que define os valores ```CopyToOutput``` e ```Flatten``` na entrada ```contentFiles``` no nuspec de saída.</span><span class="sxs-lookup"><span data-stu-id="99fd0-241">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="99fd0-242">Além de itens de Conteúdo, os metadados `<Pack>` e `<PackagePath>` também podem ser definidos em arquivos com uma ação de Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.</span><span class="sxs-lookup"><span data-stu-id="99fd0-242">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="99fd0-243">Para o pacote acrescentar o nome de arquivo ao caminho do pacote ao usar padrões glob, seu caminho de pacote deve terminar com o caractere separador de pasta, caso contrário, o caminho do pacote será tratado como o caminho completo, incluindo o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="99fd0-243">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="99fd0-244">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="99fd0-244">IncludeSymbols</span></span>

<span data-ttu-id="99fd0-245">Ao usar o `MSBuild /t:pack /p:IncludeSymbols=true`, os arquivos `.pdb` correspondentes são copiados junto com outros arquivos de saída (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="99fd0-245">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="99fd0-246">Observe que a configuração `IncludeSymbols=true` cria um pacote regular *e* um pacote de símbolos.</span><span class="sxs-lookup"><span data-stu-id="99fd0-246">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="99fd0-247">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="99fd0-247">IncludeSource</span></span>

<span data-ttu-id="99fd0-248">Isso é o mesmo que `IncludeSymbols`, exceto que também copia os arquivos de origem com arquivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="99fd0-248">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="99fd0-249">Todos os arquivos do tipo `Compile` são copiadas para `src\<ProjectName>\`, preservando a estrutura de pastas do caminho relativo no pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="99fd0-249">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="99fd0-250">O mesmo também ocorre para arquivos de origem de qualquer `ProjectReference` que tem `TreatAsPackageReference` definido como `false`.</span><span class="sxs-lookup"><span data-stu-id="99fd0-250">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="99fd0-251">Se um arquivo do tipo Compilação estiver fora da pasta de projeto, ele será adicionado apenas a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="99fd0-251">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="99fd0-252">IsTool</span><span class="sxs-lookup"><span data-stu-id="99fd0-252">IsTool</span></span>

<span data-ttu-id="99fd0-253">Ao usar `MSBuild /t:pack /p:IsTool=true`, todos os arquivos de saída, conforme especificado no cenário [Assemblies de saída](#output-assemblies), são copiados para a pasta `tools` em vez da pasta `lib`.</span><span class="sxs-lookup"><span data-stu-id="99fd0-253">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="99fd0-254">Observe que isso é diferente de um `DotNetCliTool` que é especificado pela configuração do `PackageType` no arquivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="99fd0-254">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="99fd0-255">Empacotamento usando um .nuspec</span><span class="sxs-lookup"><span data-stu-id="99fd0-255">Packing using a .nuspec</span></span>

<span data-ttu-id="99fd0-256">Você pode usar um arquivo `.nuspec` para empacotar seu projeto desde que tenha um arquivo de projeto para importar `NuGet.Build.Tasks.Pack.targets` a fim de executar a tarefa de empacotamento.</span><span class="sxs-lookup"><span data-stu-id="99fd0-256">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="99fd0-257">As três propriedades MSBuild a seguir são relevantes para empacotamento usando um `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="99fd0-257">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="99fd0-258">`NuspecFile`: caminho relativo ou absoluto para o arquivo `.nuspec` que está sendo usado para o empacotamento.</span><span class="sxs-lookup"><span data-stu-id="99fd0-258">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="99fd0-259">`NuspecProperties`: uma lista separada por ponto e vírgula de pares chave/valor.</span><span class="sxs-lookup"><span data-stu-id="99fd0-259">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="99fd0-260">Devido à maneira como a análise de linha de comando do MSBuild funciona, várias propriedades precisam ser especificadas da seguinte maneira: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="99fd0-260">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="99fd0-261">`NuspecBasePath`: o caminho base para o arquivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="99fd0-261">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="99fd0-262">Se estiver usando `dotnet.exe` para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="99fd0-262">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="99fd0-263">Se estiver usando o MSBuild para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="99fd0-263">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="99fd0-264">restore target</span><span class="sxs-lookup"><span data-stu-id="99fd0-264">restore target</span></span>

<span data-ttu-id="99fd0-265">`MSBuild /t:restore` (que `nuget restore` e `dotnet restore` usam com projetos do .NET Core), restaura pacotes referenciados no arquivo de projeto da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="99fd0-265">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="99fd0-266">Ler todas as referências projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="99fd0-266">Read all project to project references</span></span>
1. <span data-ttu-id="99fd0-267">Ler as propriedades do projeto para localizar a pasta intermediária e as estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="99fd0-267">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="99fd0-268">Passar dados do msbuild para NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="99fd0-268">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="99fd0-269">Executar restauração</span><span class="sxs-lookup"><span data-stu-id="99fd0-269">Run restore</span></span>
1. <span data-ttu-id="99fd0-270">Baixar os pacotes</span><span class="sxs-lookup"><span data-stu-id="99fd0-270">Download packages</span></span>
1. <span data-ttu-id="99fd0-271">Gravar arquivo de ativos, destinos e objetos</span><span class="sxs-lookup"><span data-stu-id="99fd0-271">Write assets file, targets, and props</span></span>

### <a name="restore-properties"></a><span data-ttu-id="99fd0-272">Restaurar propriedades</span><span class="sxs-lookup"><span data-stu-id="99fd0-272">Restore properties</span></span>

<span data-ttu-id="99fd0-273">Configurações de restauração adicionais podem vir de propriedades MSBuild no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="99fd0-273">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="99fd0-274">Os valores também podem ser definidos na linha de comando usando a opção `/p:` (consulte os Exemplos abaixo).</span><span class="sxs-lookup"><span data-stu-id="99fd0-274">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="99fd0-275">propriedade</span><span class="sxs-lookup"><span data-stu-id="99fd0-275">Property</span></span> | <span data-ttu-id="99fd0-276">Descrição</span><span class="sxs-lookup"><span data-stu-id="99fd0-276">Description</span></span> |
|--------|--------|
| <span data-ttu-id="99fd0-277">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="99fd0-277">RestoreSources</span></span> | <span data-ttu-id="99fd0-278">Uma lista delimitada por ponto e vírgula de origens de pacote.</span><span class="sxs-lookup"><span data-stu-id="99fd0-278">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="99fd0-279">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="99fd0-279">RestorePackagesPath</span></span> | <span data-ttu-id="99fd0-280">Caminho da pasta dos pacotes do usuário.</span><span class="sxs-lookup"><span data-stu-id="99fd0-280">User packages folder path.</span></span> |
| <span data-ttu-id="99fd0-281">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="99fd0-281">RestoreDisableParallel</span></span> | <span data-ttu-id="99fd0-282">Limite os downloads para um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="99fd0-282">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="99fd0-283">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="99fd0-283">RestoreConfigFile</span></span> | <span data-ttu-id="99fd0-284">Caminho para um arquivo `Nuget.Config` a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="99fd0-284">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="99fd0-285">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="99fd0-285">RestoreNoCache</span></span> | <span data-ttu-id="99fd0-286">Se verdadeiro, evita o uso de cache da Web.</span><span class="sxs-lookup"><span data-stu-id="99fd0-286">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="99fd0-287">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="99fd0-287">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="99fd0-288">Se verdadeiro, ignora origens de pacote com falha ou ausentes.</span><span class="sxs-lookup"><span data-stu-id="99fd0-288">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="99fd0-289">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="99fd0-289">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="99fd0-290">Caminho para `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="99fd0-290">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="99fd0-291">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="99fd0-291">RestoreGraphProjectInput</span></span> | <span data-ttu-id="99fd0-292">Lista separada por ponto e vírgula de projetos a serem restaurados, que devem conter caminhos absolutos.</span><span class="sxs-lookup"><span data-stu-id="99fd0-292">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="99fd0-293">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="99fd0-293">RestoreOutputPath</span></span> | <span data-ttu-id="99fd0-294">Pasta de saída que usa a pasta `obj` como padrão.</span><span class="sxs-lookup"><span data-stu-id="99fd0-294">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="99fd0-295">Exemplos</span><span class="sxs-lookup"><span data-stu-id="99fd0-295">Examples</span></span>

<span data-ttu-id="99fd0-296">Linha de comando:</span><span class="sxs-lookup"><span data-stu-id="99fd0-296">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="99fd0-297">Arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="99fd0-297">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="99fd0-298">Restaurar saídas</span><span class="sxs-lookup"><span data-stu-id="99fd0-298">Restore outputs</span></span>

<span data-ttu-id="99fd0-299">A restauração cria os seguintes arquivos na pasta `obj` de build:</span><span class="sxs-lookup"><span data-stu-id="99fd0-299">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="99fd0-300">Arquivo</span><span class="sxs-lookup"><span data-stu-id="99fd0-300">File</span></span> | <span data-ttu-id="99fd0-301">Descrição</span><span class="sxs-lookup"><span data-stu-id="99fd0-301">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="99fd0-302">Anteriormente `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="99fd0-302">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="99fd0-303">Referências a objetos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="99fd0-303">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="99fd0-304">Referências a destinos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="99fd0-304">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="99fd0-305">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="99fd0-305">PackageTargetFallback</span></span>

<span data-ttu-id="99fd0-306">O elemento `PackageTargetFallback` permite especificar um conjunto de destinos compatíveis a serem usados ao restaurar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="99fd0-306">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="99fd0-307">Ele foi desenvolvido para permitir que os pacotes que usam o dotnet [TxM](../schema/target-frameworks.md) funcionem com pacotes compatíveis que não declaram um dotnet TxM.</span><span class="sxs-lookup"><span data-stu-id="99fd0-307">It's designed to allow packages that use a dotnet [TxM](../schema/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="99fd0-308">Ou seja, se o projeto usar o dotnet TxM, todos os pacotes dos quais ele depende também deverão ter um dotnet TxM, a menos que você adicione o `<PackageTargetFallback>` ao projeto para permitir que plataformas não dotnet sejam compatíveis com o dotnet.</span><span class="sxs-lookup"><span data-stu-id="99fd0-308">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="99fd0-309">Por exemplo, se o projeto está usando o `netstandard1.6` TxM e um pacote dependente contém apenas `lib/net45/a.dll` e `lib/portable-net45+win81/a.dll`, o projeto não será compilado.</span><span class="sxs-lookup"><span data-stu-id="99fd0-309">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="99fd0-310">Se a DLL que você deseja colocar é esta última, é possível adicionar um `PackageTargetFallback` como mostrado a seguir para dizer que a DLL `portable-net45+win81` é compatível:</span><span class="sxs-lookup"><span data-stu-id="99fd0-310">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="99fd0-311">Para declarar um fallback para todos os destinos em seu projeto, deixe o atributo `Condition` de fora.</span><span class="sxs-lookup"><span data-stu-id="99fd0-311">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="99fd0-312">Você também pode estender qualquer `PackageTargetFallback` existente incluindo `$(PackageTargetFallback)` conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="99fd0-312">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="99fd0-313">Substituindo uma biblioteca de um grafo de restauração</span><span class="sxs-lookup"><span data-stu-id="99fd0-313">Replacing one library from a restore graph</span></span>

<span data-ttu-id="99fd0-314">Se uma restauração está trazendo o assembly errado, é possível excluir a escolha padrão do pacote e substituí-lo por outro de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="99fd0-314">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="99fd0-315">Primeiro com um `PackageReference` de nível superior, exclua todos os ativos:</span><span class="sxs-lookup"><span data-stu-id="99fd0-315">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="99fd0-316">Em seguida, adicione sua própria referência à cópia local apropriada da DLL:</span><span class="sxs-lookup"><span data-stu-id="99fd0-316">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
