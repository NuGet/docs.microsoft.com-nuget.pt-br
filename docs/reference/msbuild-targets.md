---
title: Empacotamento e restauração do NuGet como destinos do MSBuild
description: O pack e restore do NuGet podem funcionar diretamente como destinos do MSBuild com o NuGet 4.0 e superior.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 7de3f0f1133a89848e9268d489751293fb3cbf25
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235692"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="872d7-103">Empacotamento e restauração do NuGet como destinos do MSBuild</span><span class="sxs-lookup"><span data-stu-id="872d7-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="872d7-104">*NuGet 4.0 ou superior*</span><span class="sxs-lookup"><span data-stu-id="872d7-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="872d7-105">Com o formato [PackageReference](../consume-packages/package-references-in-project-files.md) , o NuGet 4.0 + pode armazenar todos os metadados do manifesto diretamente dentro de um arquivo de projeto em vez de usar um `.nuspec` arquivo separado.</span><span class="sxs-lookup"><span data-stu-id="872d7-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="872d7-106">Com o MSBuild 15.1 ou superior, o NuGet também é um cidadão de primeira classe do MSBuild com os destinos `pack` e `restore`, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="872d7-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="872d7-107">Esses destinos permitem que você trabalhe com o NuGet como faria com qualquer outra tarefa ou destino do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="872d7-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="872d7-108">Para obter instruções sobre como criar um pacote NuGet usando o MSBuild, consulte [criar um pacote NuGet usando o MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="872d7-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="872d7-109">(Para NuGet 3.x e anteriores, use os comandos [pack](../reference/cli-reference/cli-ref-pack.md) e [restore](../reference/cli-reference/cli-ref-restore.md) na CLI do NuGet.)</span><span class="sxs-lookup"><span data-stu-id="872d7-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="872d7-110">Ordem de build de destino</span><span class="sxs-lookup"><span data-stu-id="872d7-110">Target build order</span></span>

<span data-ttu-id="872d7-111">Como `pack` e `restore` são os destinos do MSBuild, você pode acessá-los para melhorar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="872d7-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="872d7-112">Por exemplo, digamos que você deseja copiar o pacote para um compartilhamento de rede após empacotá-lo.</span><span class="sxs-lookup"><span data-stu-id="872d7-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="872d7-113">Você pode fazer isso adicionando o seguinte ao seu arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="872d7-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="872d7-114">Da mesma forma, você pode gravar uma tarefa do MSBuild, escrever seu próprio destino e consumir propriedades do NuGet na tarefa de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="872d7-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="872d7-115">`$(OutputPath)` é relativo e espera que você esteja executando o comando da raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="872d7-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="872d7-116">pack target</span><span class="sxs-lookup"><span data-stu-id="872d7-116">pack target</span></span>

<span data-ttu-id="872d7-117">Para projetos de .NET Standard usando o formato PackageReference, o uso `msbuild -t:pack` de desenha entradas do arquivo de projeto para usar na criação de um pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="872d7-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="872d7-118">A tabela abaixo descreve as propriedades do MSBuild que podem ser adicionadas a um arquivo do projeto dentro do primeiro nó `<PropertyGroup>`.</span><span class="sxs-lookup"><span data-stu-id="872d7-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="872d7-119">Você pode fazer essas edições facilmente no Visual Studio 2017 e posterior clicando com o botão direito do mouse no projeto e selecionando **Editar {project_name}** no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="872d7-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="872d7-120">Para sua conveniência, a tabela é organizada pela propriedade equivalente em um [ `.nuspec` arquivo](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="872d7-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="872d7-121">Observe que as propriedades `Owners` e `Summary` de `.nuspec` não são compatíveis com o MSBuild.</span><span class="sxs-lookup"><span data-stu-id="872d7-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="872d7-122">Valor de atributo/NuSpec</span><span class="sxs-lookup"><span data-stu-id="872d7-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="872d7-123">Propriedade do MSBuild</span><span class="sxs-lookup"><span data-stu-id="872d7-123">MSBuild Property</span></span> | <span data-ttu-id="872d7-124">Padrão</span><span class="sxs-lookup"><span data-stu-id="872d7-124">Default</span></span> | <span data-ttu-id="872d7-125">Observações</span><span class="sxs-lookup"><span data-stu-id="872d7-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="872d7-126">Id</span><span class="sxs-lookup"><span data-stu-id="872d7-126">Id</span></span> | <span data-ttu-id="872d7-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="872d7-127">PackageId</span></span> | <span data-ttu-id="872d7-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="872d7-128">AssemblyName</span></span> | <span data-ttu-id="872d7-129">$(AssemblyName) do MSBuild</span><span class="sxs-lookup"><span data-stu-id="872d7-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="872d7-130">Versão</span><span class="sxs-lookup"><span data-stu-id="872d7-130">Version</span></span> | <span data-ttu-id="872d7-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="872d7-131">PackageVersion</span></span> | <span data-ttu-id="872d7-132">Versão</span><span class="sxs-lookup"><span data-stu-id="872d7-132">Version</span></span> | <span data-ttu-id="872d7-133">Isso é compatível com semver, por exemplo “1.0.0”, “1.0.0-beta” ou “1.0.0-beta-00345”</span><span class="sxs-lookup"><span data-stu-id="872d7-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="872d7-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="872d7-134">VersionPrefix</span></span> | <span data-ttu-id="872d7-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="872d7-135">PackageVersionPrefix</span></span> | <span data-ttu-id="872d7-136">vazio</span><span class="sxs-lookup"><span data-stu-id="872d7-136">empty</span></span> | <span data-ttu-id="872d7-137">A configuração PackageVersion substitui PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="872d7-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="872d7-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="872d7-138">VersionSuffix</span></span> | <span data-ttu-id="872d7-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="872d7-139">PackageVersionSuffix</span></span> | <span data-ttu-id="872d7-140">vazio</span><span class="sxs-lookup"><span data-stu-id="872d7-140">empty</span></span> | <span data-ttu-id="872d7-141">$(VersionSuffix) do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="872d7-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="872d7-142">A configuração PackageVersion substitui PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="872d7-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="872d7-143">Autores</span><span class="sxs-lookup"><span data-stu-id="872d7-143">Authors</span></span> | <span data-ttu-id="872d7-144">Autores</span><span class="sxs-lookup"><span data-stu-id="872d7-144">Authors</span></span> | <span data-ttu-id="872d7-145">Nome do usuário atual</span><span class="sxs-lookup"><span data-stu-id="872d7-145">Username of the current user</span></span> | |
| <span data-ttu-id="872d7-146">Proprietários</span><span class="sxs-lookup"><span data-stu-id="872d7-146">Owners</span></span> | <span data-ttu-id="872d7-147">N/D</span><span class="sxs-lookup"><span data-stu-id="872d7-147">N/A</span></span> | <span data-ttu-id="872d7-148">Não está presente no NuSpec</span><span class="sxs-lookup"><span data-stu-id="872d7-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="872d7-149">Título</span><span class="sxs-lookup"><span data-stu-id="872d7-149">Title</span></span> | <span data-ttu-id="872d7-150">Título</span><span class="sxs-lookup"><span data-stu-id="872d7-150">Title</span></span> | <span data-ttu-id="872d7-151">O PackageId</span><span class="sxs-lookup"><span data-stu-id="872d7-151">The PackageId</span></span>| |
| <span data-ttu-id="872d7-152">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="872d7-152">Description</span></span> | <span data-ttu-id="872d7-153">Descrição</span><span class="sxs-lookup"><span data-stu-id="872d7-153">Description</span></span> | <span data-ttu-id="872d7-154">“Package Description”</span><span class="sxs-lookup"><span data-stu-id="872d7-154">"Package Description"</span></span> | |
| <span data-ttu-id="872d7-155">Direitos autorais</span><span class="sxs-lookup"><span data-stu-id="872d7-155">Copyright</span></span> | <span data-ttu-id="872d7-156">Direitos autorais</span><span class="sxs-lookup"><span data-stu-id="872d7-156">Copyright</span></span> | <span data-ttu-id="872d7-157">vazio</span><span class="sxs-lookup"><span data-stu-id="872d7-157">empty</span></span> | |
| <span data-ttu-id="872d7-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="872d7-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="872d7-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="872d7-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="872d7-160">false</span><span class="sxs-lookup"><span data-stu-id="872d7-160">false</span></span> | |
| <span data-ttu-id="872d7-161">license</span><span class="sxs-lookup"><span data-stu-id="872d7-161">license</span></span> | <span data-ttu-id="872d7-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="872d7-162">PackageLicenseExpression</span></span> | <span data-ttu-id="872d7-163">vazio</span><span class="sxs-lookup"><span data-stu-id="872d7-163">empty</span></span> | <span data-ttu-id="872d7-164">Corresponde a `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="872d7-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="872d7-165">license</span><span class="sxs-lookup"><span data-stu-id="872d7-165">license</span></span> | <span data-ttu-id="872d7-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="872d7-166">PackageLicenseFile</span></span> | <span data-ttu-id="872d7-167">vazio</span><span class="sxs-lookup"><span data-stu-id="872d7-167">empty</span></span> | <span data-ttu-id="872d7-168">Corresponde ao `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="872d7-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="872d7-169">Você precisa empacotar explicitamente o arquivo de licença referenciado.</span><span class="sxs-lookup"><span data-stu-id="872d7-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="872d7-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="872d7-170">LicenseUrl</span></span> | <span data-ttu-id="872d7-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="872d7-171">PackageLicenseUrl</span></span> | <span data-ttu-id="872d7-172">vazio</span><span class="sxs-lookup"><span data-stu-id="872d7-172">empty</span></span> | <span data-ttu-id="872d7-173">`PackageLicenseUrl` é preterido, use a propriedade PackageLicenseExpression ou PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="872d7-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="872d7-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="872d7-174">ProjectUrl</span></span> | <span data-ttu-id="872d7-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="872d7-175">PackageProjectUrl</span></span> | <span data-ttu-id="872d7-176">vazio</span><span class="sxs-lookup"><span data-stu-id="872d7-176">empty</span></span> | |
| <span data-ttu-id="872d7-177">ícone</span><span class="sxs-lookup"><span data-stu-id="872d7-177">Icon</span></span> | <span data-ttu-id="872d7-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="872d7-178">PackageIcon</span></span> | <span data-ttu-id="872d7-179">vazio</span><span class="sxs-lookup"><span data-stu-id="872d7-179">empty</span></span> | <span data-ttu-id="872d7-180">Você precisa empacotar explicitamente o arquivo de imagem do ícone referenciado.</span><span class="sxs-lookup"><span data-stu-id="872d7-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="872d7-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="872d7-181">IconUrl</span></span> | <span data-ttu-id="872d7-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="872d7-182">PackageIconUrl</span></span> | <span data-ttu-id="872d7-183">vazio</span><span class="sxs-lookup"><span data-stu-id="872d7-183">empty</span></span> | <span data-ttu-id="872d7-184">Para obter a melhor experiência de nível inferior, `PackageIconUrl` deve ser especificado além de `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="872d7-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="872d7-185">Período mais longo, `PackageIconUrl` será preterido.</span><span class="sxs-lookup"><span data-stu-id="872d7-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="872d7-186">Marcações</span><span class="sxs-lookup"><span data-stu-id="872d7-186">Tags</span></span> | <span data-ttu-id="872d7-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="872d7-187">PackageTags</span></span> | <span data-ttu-id="872d7-188">vazio</span><span class="sxs-lookup"><span data-stu-id="872d7-188">empty</span></span> | <span data-ttu-id="872d7-189">Marcas são delimitadas por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="872d7-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="872d7-190">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="872d7-190">ReleaseNotes</span></span> | <span data-ttu-id="872d7-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="872d7-191">PackageReleaseNotes</span></span> | <span data-ttu-id="872d7-192">vazio</span><span class="sxs-lookup"><span data-stu-id="872d7-192">empty</span></span> | |
| <span data-ttu-id="872d7-193">Repositório/URL</span><span class="sxs-lookup"><span data-stu-id="872d7-193">Repository/Url</span></span> | <span data-ttu-id="872d7-194">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="872d7-194">RepositoryUrl</span></span> | <span data-ttu-id="872d7-195">vazio</span><span class="sxs-lookup"><span data-stu-id="872d7-195">empty</span></span> | <span data-ttu-id="872d7-196">URL do repositório usada para clonar ou recuperar o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="872d7-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="872d7-197">Exemplo *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="872d7-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="872d7-198">Repositório/tipo</span><span class="sxs-lookup"><span data-stu-id="872d7-198">Repository/Type</span></span> | <span data-ttu-id="872d7-199">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="872d7-199">RepositoryType</span></span> | <span data-ttu-id="872d7-200">vazio</span><span class="sxs-lookup"><span data-stu-id="872d7-200">empty</span></span> | <span data-ttu-id="872d7-201">Tipo de repositório.</span><span class="sxs-lookup"><span data-stu-id="872d7-201">Repository type.</span></span> <span data-ttu-id="872d7-202">Exemplos: *git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="872d7-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="872d7-203">Repositório/Branch</span><span class="sxs-lookup"><span data-stu-id="872d7-203">Repository/Branch</span></span> | <span data-ttu-id="872d7-204">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="872d7-204">RepositoryBranch</span></span> | <span data-ttu-id="872d7-205">vazio</span><span class="sxs-lookup"><span data-stu-id="872d7-205">empty</span></span> | <span data-ttu-id="872d7-206">Informações opcionais da ramificação do repositório.</span><span class="sxs-lookup"><span data-stu-id="872d7-206">Optional repository branch information.</span></span> <span data-ttu-id="872d7-207">*RepositoryUrl* também deve ser especificado para que essa propriedade seja incluída.</span><span class="sxs-lookup"><span data-stu-id="872d7-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="872d7-208">Exemplo: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="872d7-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="872d7-209">Repositório/confirmação</span><span class="sxs-lookup"><span data-stu-id="872d7-209">Repository/Commit</span></span> | <span data-ttu-id="872d7-210">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="872d7-210">RepositoryCommit</span></span> | <span data-ttu-id="872d7-211">vazio</span><span class="sxs-lookup"><span data-stu-id="872d7-211">empty</span></span> | <span data-ttu-id="872d7-212">Confirmação opcional do repositório ou conjunto de alterações para indicar de qual fonte o pacote foi criado.</span><span class="sxs-lookup"><span data-stu-id="872d7-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="872d7-213">*RepositoryUrl* também deve ser especificado para que essa propriedade seja incluída.</span><span class="sxs-lookup"><span data-stu-id="872d7-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="872d7-214">Exemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="872d7-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="872d7-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="872d7-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="872d7-216">Resumo</span><span class="sxs-lookup"><span data-stu-id="872d7-216">Summary</span></span> | <span data-ttu-id="872d7-217">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="872d7-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="872d7-218">pack target inputs</span><span class="sxs-lookup"><span data-stu-id="872d7-218">pack target inputs</span></span>

- <span data-ttu-id="872d7-219">IsPackable</span><span class="sxs-lookup"><span data-stu-id="872d7-219">IsPackable</span></span>
- <span data-ttu-id="872d7-220">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="872d7-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="872d7-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="872d7-221">PackageVersion</span></span>
- <span data-ttu-id="872d7-222">PackageId</span><span class="sxs-lookup"><span data-stu-id="872d7-222">PackageId</span></span>
- <span data-ttu-id="872d7-223">Autores</span><span class="sxs-lookup"><span data-stu-id="872d7-223">Authors</span></span>
- <span data-ttu-id="872d7-224">Descrição</span><span class="sxs-lookup"><span data-stu-id="872d7-224">Description</span></span>
- <span data-ttu-id="872d7-225">Direitos autorais</span><span class="sxs-lookup"><span data-stu-id="872d7-225">Copyright</span></span>
- <span data-ttu-id="872d7-226">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="872d7-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="872d7-227">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="872d7-227">DevelopmentDependency</span></span>
- <span data-ttu-id="872d7-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="872d7-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="872d7-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="872d7-229">PackageLicenseFile</span></span>
- <span data-ttu-id="872d7-230">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="872d7-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="872d7-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="872d7-231">PackageProjectUrl</span></span>
- <span data-ttu-id="872d7-232">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="872d7-232">PackageIconUrl</span></span>
- <span data-ttu-id="872d7-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="872d7-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="872d7-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="872d7-234">PackageTags</span></span>
- <span data-ttu-id="872d7-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="872d7-235">PackageOutputPath</span></span>
- <span data-ttu-id="872d7-236">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="872d7-236">IncludeSymbols</span></span>
- <span data-ttu-id="872d7-237">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="872d7-237">IncludeSource</span></span>
- <span data-ttu-id="872d7-238">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="872d7-238">PackageTypes</span></span>
- <span data-ttu-id="872d7-239">IsTool</span><span class="sxs-lookup"><span data-stu-id="872d7-239">IsTool</span></span>
- <span data-ttu-id="872d7-240">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="872d7-240">RepositoryUrl</span></span>
- <span data-ttu-id="872d7-241">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="872d7-241">RepositoryType</span></span>
- <span data-ttu-id="872d7-242">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="872d7-242">RepositoryBranch</span></span>
- <span data-ttu-id="872d7-243">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="872d7-243">RepositoryCommit</span></span>
- <span data-ttu-id="872d7-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="872d7-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="872d7-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="872d7-245">MinClientVersion</span></span>
- <span data-ttu-id="872d7-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="872d7-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="872d7-247">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="872d7-247">IncludeContentInPack</span></span>
- <span data-ttu-id="872d7-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="872d7-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="872d7-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="872d7-249">ContentTargetFolders</span></span>
- <span data-ttu-id="872d7-250">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="872d7-250">NuspecFile</span></span>
- <span data-ttu-id="872d7-251">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="872d7-251">NuspecBasePath</span></span>
- <span data-ttu-id="872d7-252">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="872d7-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="872d7-253">pack scenarios</span><span class="sxs-lookup"><span data-stu-id="872d7-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="872d7-254">Suprimir dependências</span><span class="sxs-lookup"><span data-stu-id="872d7-254">Suppress dependencies</span></span>

<span data-ttu-id="872d7-255">Para suprimir dependências de pacote do pacote NuGet gerado, defina `SuppressDependenciesWhenPacking` como `true` que permitirá ignorar todas as dependências do arquivo nupkg gerado.</span><span class="sxs-lookup"><span data-stu-id="872d7-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="872d7-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="872d7-256">PackageIconUrl</span></span>

<span data-ttu-id="872d7-257">`PackageIconUrl` será preterido em favor da nova [`PackageIcon`](#packageicon) propriedade.</span><span class="sxs-lookup"><span data-stu-id="872d7-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="872d7-258">A partir do NuGet 5,3 & o Visual Studio 2019 versão 16,3, `pack` o gerará um aviso [NU5048](./errors-and-warnings/nu5048.md) se os metadados do pacote especificarem apenas `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="872d7-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="872d7-259">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="872d7-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="872d7-260">Você deve especificar o `PackageIcon` e o `PackageIconUrl` para manter a compatibilidade com versões anteriores com clientes e fontes que ainda não dão suporte `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="872d7-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="872d7-261">O Visual Studio dará suporte a `PackageIcon` pacotes provenientes de uma fonte baseada em pasta em uma versão futura.</span><span class="sxs-lookup"><span data-stu-id="872d7-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="872d7-262">Empacotando um arquivo de imagem de ícone</span><span class="sxs-lookup"><span data-stu-id="872d7-262">Packing an icon image file</span></span>

<span data-ttu-id="872d7-263">Ao empacotar um arquivo de imagem de ícone, você precisa usar a `PackageIcon` propriedade para especificar o caminho do pacote, em relação à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="872d7-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="872d7-264">Além disso, você precisa certificar-se de que o arquivo está incluído no pacote.</span><span class="sxs-lookup"><span data-stu-id="872d7-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="872d7-265">O tamanho do arquivo de imagem é limitado a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="872d7-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="872d7-266">Os formatos de arquivo com suporte incluem JPEG e PNG.</span><span class="sxs-lookup"><span data-stu-id="872d7-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="872d7-267">Recomendamos uma resolução de imagem de 128x128.</span><span class="sxs-lookup"><span data-stu-id="872d7-267">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="872d7-268">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="872d7-268">For example:</span></span>

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

<span data-ttu-id="872d7-269">[Exemplo de ícone de pacote](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="872d7-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="872d7-270">Para obter o equivalente do nuspec, dê uma olhada na [referência do nuspec para o ícone](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="872d7-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="872d7-271">Assemblies de saída</span><span class="sxs-lookup"><span data-stu-id="872d7-271">Output assemblies</span></span>

<span data-ttu-id="872d7-272">O `nuget pack` copia arquivos de saída com extensões `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="872d7-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="872d7-273">Os arquivos de saída que são copiados dependem do que o MSBuild fornece do destino `BuiltOutputProjectGroup`.</span><span class="sxs-lookup"><span data-stu-id="872d7-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="872d7-274">Há duas propriedades de MSBuild que você pode usar em seu arquivo de projeto ou a linha de comando para controlar onde ficam os assemblies de saída:</span><span class="sxs-lookup"><span data-stu-id="872d7-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="872d7-275">`IncludeBuildOutput`: um valor booliano que determina se os assemblies de saída de build devem ser incluídos no pacote.</span><span class="sxs-lookup"><span data-stu-id="872d7-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="872d7-276">`BuildOutputTargetFolder`: especifica a pasta na qual os assemblies de saída devem ser colocados.</span><span class="sxs-lookup"><span data-stu-id="872d7-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="872d7-277">Os assemblies de saída (e outros arquivos de saída) são copiados para suas respectivas pastas de estrutura.</span><span class="sxs-lookup"><span data-stu-id="872d7-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="872d7-278">Referências de pacote</span><span class="sxs-lookup"><span data-stu-id="872d7-278">Package references</span></span>

<span data-ttu-id="872d7-279">Consulte [Referências de pacote em arquivos de projeto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="872d7-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="872d7-280">Referências de projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="872d7-280">Project to project references</span></span>

<span data-ttu-id="872d7-281">As referências projeto a projeto são consideradas como referências de pacote do nuget por padrão, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="872d7-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="872d7-282">Você também pode adicionar os seguintes metadados à referência de projeto:</span><span class="sxs-lookup"><span data-stu-id="872d7-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="872d7-283">Incluindo o conteúdo em um pacote</span><span class="sxs-lookup"><span data-stu-id="872d7-283">Including content in a package</span></span>

<span data-ttu-id="872d7-284">Para incluir o conteúdo, adicione metadados extras ao item `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="872d7-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="872d7-285">Por padrão, tudo que pertencer ao tipo “Conteúdo” é incluído no pacote, a menos que seja substituído por entradas como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="872d7-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="872d7-286">Por padrão, tudo é adicionado à raiz da pasta `content` e `contentFiles\any\<target_framework>` dentro de um pacote e preserva a estrutura e pasta relativa, a menos que você especifique um caminho de pacote:</span><span class="sxs-lookup"><span data-stu-id="872d7-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="872d7-287">Se você quiser copiar todo o conteúdo somente para determinadas pastas raiz (em vez de para `content` e `contentFiles`), será possível usar a propriedade `ContentTargetFolders` do MSBuild, que assume como padrão "content;contentFiles", mas pode ser definida como qualquer outro nome de pasta.</span><span class="sxs-lookup"><span data-stu-id="872d7-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="872d7-288">Observe que só especificar “contentFiles” em `ContentTargetFolders` coloca os arquivos em `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` com base em `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="872d7-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="872d7-289">`PackagePath` pode ser um conjunto de caminhos de destino separados por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="872d7-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="872d7-290">Especificar um caminho de pacote vazio adicionaria o arquivo à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="872d7-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="872d7-291">Por exemplo, o seguinte adiciona `libuv.txt` a `content\myfiles`, `content\samples` e a raiz do pacote:</span><span class="sxs-lookup"><span data-stu-id="872d7-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="872d7-292">Há também uma propriedade de MSBuild `$(IncludeContentInPack)`, que assume o padrão `true`.</span><span class="sxs-lookup"><span data-stu-id="872d7-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="872d7-293">Se isso for definido como `false` em qualquer projeto, o conteúdo desse projeto não está incluso no pacote do nuget.</span><span class="sxs-lookup"><span data-stu-id="872d7-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="872d7-294">Outros metadados específicos do pacote que pode ser definido em qualquer um dos itens acima ```<PackageCopyToOutput>``` e ```<PackageFlatten>```, que define os valores ```CopyToOutput``` e ```Flatten``` na entrada ```contentFiles``` no nuspec de saída.</span><span class="sxs-lookup"><span data-stu-id="872d7-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="872d7-295">Além de itens de Conteúdo, os metadados `<Pack>` e `<PackagePath>` também podem ser definidos em arquivos com uma ação de Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.</span><span class="sxs-lookup"><span data-stu-id="872d7-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="872d7-296">Para o pacote acrescentar o nome de arquivo ao caminho do pacote ao usar padrões glob, seu caminho de pacote deve terminar com o caractere separador de pasta, caso contrário, o caminho do pacote será tratado como o caminho completo, incluindo o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="872d7-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="872d7-297">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="872d7-297">IncludeSymbols</span></span>

<span data-ttu-id="872d7-298">Ao usar o `MSBuild -t:pack -p:IncludeSymbols=true`, os arquivos `.pdb` correspondentes são copiados junto com outros arquivos de saída (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="872d7-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="872d7-299">Observe que a configuração `IncludeSymbols=true` cria um pacote regular *e* um pacote de símbolos.</span><span class="sxs-lookup"><span data-stu-id="872d7-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="872d7-300">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="872d7-300">IncludeSource</span></span>

<span data-ttu-id="872d7-301">Isso é o mesmo que `IncludeSymbols`, exceto que também copia os arquivos de origem com arquivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="872d7-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="872d7-302">Todos os arquivos do tipo `Compile` são copiadas para `src\<ProjectName>\`, preservando a estrutura de pastas do caminho relativo no pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="872d7-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="872d7-303">O mesmo também ocorre para arquivos de origem de qualquer `ProjectReference` que tem `TreatAsPackageReference` definido como `false`.</span><span class="sxs-lookup"><span data-stu-id="872d7-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="872d7-304">Se um arquivo do tipo Compilação estiver fora da pasta de projeto, ele será adicionado apenas a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="872d7-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="872d7-305">Empacotando uma expressão de licença ou um arquivo de licença</span><span class="sxs-lookup"><span data-stu-id="872d7-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="872d7-306">Ao usar uma expressão de licença, a propriedade PackageLicenseExpression deve ser usada.</span><span class="sxs-lookup"><span data-stu-id="872d7-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="872d7-307">[Exemplo de expressão de licença](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="872d7-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="872d7-308">[Saiba mais sobre as expressões de licença e as licenças que são aceitas pelo NuGet.org](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="872d7-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="872d7-309">Ao empacotar um arquivo de licença, você precisa usar a propriedade PackageLicenseFile para especificar o caminho do pacote, em relação à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="872d7-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="872d7-310">Além disso, você precisa certificar-se de que o arquivo está incluído no pacote.</span><span class="sxs-lookup"><span data-stu-id="872d7-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="872d7-311">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="872d7-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="872d7-312">[Exemplo de arquivo de licença](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="872d7-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="872d7-313">Empacotando um arquivo sem uma extensão</span><span class="sxs-lookup"><span data-stu-id="872d7-313">Packing a file without an extension</span></span>

<span data-ttu-id="872d7-314">Em alguns cenários, como ao empacotar um arquivo de licença, talvez você queira incluir um arquivo sem uma extensão.</span><span class="sxs-lookup"><span data-stu-id="872d7-314">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="872d7-315">Por motivos históricos, o NuGet & MSBuild trata caminhos sem uma extensão como diretórios.</span><span class="sxs-lookup"><span data-stu-id="872d7-315">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="872d7-316">[Arquivo sem um exemplo de extensão](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="872d7-316">[File without an extension sample](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span></span>
### <a name="istool"></a><span data-ttu-id="872d7-317">IsTool</span><span class="sxs-lookup"><span data-stu-id="872d7-317">IsTool</span></span>

<span data-ttu-id="872d7-318">Ao usar `MSBuild -t:pack -p:IsTool=true`, todos os arquivos de saída, conforme especificado no cenário [Assemblies de saída](#output-assemblies), são copiados para a pasta `tools` em vez da pasta `lib`.</span><span class="sxs-lookup"><span data-stu-id="872d7-318">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="872d7-319">Observe que isso é diferente de um `DotNetCliTool` que é especificado pela configuração do `PackageType` no arquivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="872d7-319">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="872d7-320">Empacotamento usando um .nuspec</span><span class="sxs-lookup"><span data-stu-id="872d7-320">Packing using a .nuspec</span></span>

<span data-ttu-id="872d7-321">Embora seja recomendável [incluir todas as propriedades](../reference/msbuild-targets.md#pack-target) que normalmente estão no `.nuspec` arquivo no arquivo de projeto, você pode optar por usar um `.nuspec` arquivo para empacotar seu projeto.</span><span class="sxs-lookup"><span data-stu-id="872d7-321">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="872d7-322">Para um projeto de estilo não-SDK que usa `PackageReference` o, você deve importar `NuGet.Build.Tasks.Pack.targets` para que a tarefa de pacote possa ser executada.</span><span class="sxs-lookup"><span data-stu-id="872d7-322">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="872d7-323">Você ainda precisa restaurar o projeto antes de poder empacotar um arquivo nuspec.</span><span class="sxs-lookup"><span data-stu-id="872d7-323">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="872d7-324">(Um projeto no estilo SDK inclui os destinos do pacote por padrão.)</span><span class="sxs-lookup"><span data-stu-id="872d7-324">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="872d7-325">A estrutura de destino do arquivo de projeto é irrelevante e não é usada ao empacotar um nuspec.</span><span class="sxs-lookup"><span data-stu-id="872d7-325">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="872d7-326">As três propriedades MSBuild a seguir são relevantes para empacotamento usando um `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="872d7-326">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="872d7-327">`NuspecFile`: caminho relativo ou absoluto para o arquivo `.nuspec` que está sendo usado para o empacotamento.</span><span class="sxs-lookup"><span data-stu-id="872d7-327">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="872d7-328">`NuspecProperties`: uma lista separada por ponto e vírgula de pares chave/valor.</span><span class="sxs-lookup"><span data-stu-id="872d7-328">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="872d7-329">Devido à maneira como a análise de linha de comando do MSBuild funciona, várias propriedades precisam ser especificadas da seguinte maneira: `-p:NuspecProperties="key1=value1;key2=value2"`.</span><span class="sxs-lookup"><span data-stu-id="872d7-329">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="872d7-330">`NuspecBasePath`: o caminho base para o arquivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="872d7-330">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="872d7-331">Se estiver usando `dotnet.exe` para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="872d7-331">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="872d7-332">Se estiver usando o MSBuild para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="872d7-332">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="872d7-333">Observe que a compactação de um nuspec usando dotnet.exe ou MSBuild também leva a criar o projeto por padrão.</span><span class="sxs-lookup"><span data-stu-id="872d7-333">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="872d7-334">Isso pode ser evitado passando ```--no-build``` a propriedade para dotnet.exe, que é o equivalente à configuração ```<NoBuild>true</NoBuild> ``` em seu arquivo de projeto, juntamente com ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` a configuração no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="872d7-334">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="872d7-335">Um exemplo de um arquivo *. csproj* para empacotar um arquivo nuspec é:</span><span class="sxs-lookup"><span data-stu-id="872d7-335">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="872d7-336">Pontos de extensão avançados para criar pacote personalizado</span><span class="sxs-lookup"><span data-stu-id="872d7-336">Advanced extension points to create customized package</span></span>

<span data-ttu-id="872d7-337">O `pack` destino fornece dois pontos de extensão que são executados na compilação interna, específica da estrutura de destino.</span><span class="sxs-lookup"><span data-stu-id="872d7-337">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="872d7-338">Os pontos de extensão dão suporte à inclusão de conteúdo específico da estrutura de destino e assemblies em um pacote:</span><span class="sxs-lookup"><span data-stu-id="872d7-338">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="872d7-339">`TargetsForTfmSpecificBuildOutput` destino: Use para arquivos dentro da `lib` pasta ou de uma pasta especificada usando `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="872d7-339">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="872d7-340">`TargetsForTfmSpecificContentInPackage` destino: Use para arquivos fora do `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="872d7-340">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="872d7-341">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="872d7-341">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="872d7-342">Escreva um destino personalizado e especifique-o como o valor da `$(TargetsForTfmSpecificBuildOutput)` propriedade.</span><span class="sxs-lookup"><span data-stu-id="872d7-342">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="872d7-343">Para todos os arquivos que precisam entrar em `BuildOutputTargetFolder` (lib por padrão), o destino deve gravar esses arquivos no grupo de `BuildOutputInPackage` itens e definir os dois valores de metadados a seguir:</span><span class="sxs-lookup"><span data-stu-id="872d7-343">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="872d7-344">`FinalOutputPath`: O caminho absoluto do arquivo; Se não for fornecido, a identidade será usada para avaliar o caminho de origem.</span><span class="sxs-lookup"><span data-stu-id="872d7-344">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="872d7-345">`TargetPath`: (Opcional) defina quando o arquivo precisa entrar em uma subpasta no `lib\<TargetFramework>` , como assemblies satélite que estão em suas respectivas pastas de cultura.</span><span class="sxs-lookup"><span data-stu-id="872d7-345">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="872d7-346">O padrão é o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="872d7-346">Defaults to the name of the file.</span></span>

<span data-ttu-id="872d7-347">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="872d7-347">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="872d7-348">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="872d7-348">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="872d7-349">Escreva um destino personalizado e especifique-o como o valor da `$(TargetsForTfmSpecificContentInPackage)` propriedade.</span><span class="sxs-lookup"><span data-stu-id="872d7-349">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="872d7-350">Para todos os arquivos a serem incluídos no pacote, o destino deve gravar esses arquivos no grupo de `TfmSpecificPackageFile` itens e definir os seguintes metadados opcionais:</span><span class="sxs-lookup"><span data-stu-id="872d7-350">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="872d7-351">`PackagePath`: Caminho em que o arquivo deve ser apresentado no pacote.</span><span class="sxs-lookup"><span data-stu-id="872d7-351">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="872d7-352">O NuGet emitirá um aviso se mais de um arquivo for adicionado ao mesmo caminho de pacote.</span><span class="sxs-lookup"><span data-stu-id="872d7-352">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="872d7-353">`BuildAction`: A ação de compilação a ser atribuída ao arquivo, necessária somente se o caminho do pacote estiver na `contentFiles` pasta.</span><span class="sxs-lookup"><span data-stu-id="872d7-353">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="872d7-354">O padrão é "None".</span><span class="sxs-lookup"><span data-stu-id="872d7-354">Defaults to "None".</span></span>

<span data-ttu-id="872d7-355">Um exemplo:</span><span class="sxs-lookup"><span data-stu-id="872d7-355">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="872d7-356">restore target</span><span class="sxs-lookup"><span data-stu-id="872d7-356">restore target</span></span>

<span data-ttu-id="872d7-357">`MSBuild -t:restore` (que `nuget restore` e `dotnet restore` usam com projetos do .NET Core), restaura pacotes referenciados no arquivo de projeto da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="872d7-357">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="872d7-358">Ler todas as referências projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="872d7-358">Read all project to project references</span></span>
1. <span data-ttu-id="872d7-359">Ler as propriedades do projeto para localizar a pasta intermediária e as estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="872d7-359">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="872d7-360">Passar dados do MSBuild para NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="872d7-360">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="872d7-361">Executar restauração</span><span class="sxs-lookup"><span data-stu-id="872d7-361">Run restore</span></span>
1. <span data-ttu-id="872d7-362">Baixar os pacotes</span><span class="sxs-lookup"><span data-stu-id="872d7-362">Download packages</span></span>
1. <span data-ttu-id="872d7-363">Gravar arquivo de ativos, destinos e objetos</span><span class="sxs-lookup"><span data-stu-id="872d7-363">Write assets file, targets, and props</span></span>

<span data-ttu-id="872d7-364">O `restore` destino funciona para projetos que usam o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="872d7-364">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="872d7-365">`MSBuild 16.5+` também tem [suporte opcional](#restoring-packagereference-and-packagesconfig-with-msbuild) para o `packages.config` formato.</span><span class="sxs-lookup"><span data-stu-id="872d7-365">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="872d7-366">O `restore` destino [não deve ser executado](#restoring-and-building-with-one-msbuild-command) em combinação com o `build` destino.</span><span class="sxs-lookup"><span data-stu-id="872d7-366">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="872d7-367">Restaurar propriedades</span><span class="sxs-lookup"><span data-stu-id="872d7-367">Restore properties</span></span>

<span data-ttu-id="872d7-368">Configurações de restauração adicionais podem vir de propriedades MSBuild no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="872d7-368">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="872d7-369">Os valores também podem ser definidos na linha de comando usando a opção `-p:` (consulte os Exemplos abaixo).</span><span class="sxs-lookup"><span data-stu-id="872d7-369">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="872d7-370">Propriedade</span><span class="sxs-lookup"><span data-stu-id="872d7-370">Property</span></span> | <span data-ttu-id="872d7-371">Descrição</span><span class="sxs-lookup"><span data-stu-id="872d7-371">Description</span></span> |
|--------|--------|
| <span data-ttu-id="872d7-372">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="872d7-372">RestoreSources</span></span> | <span data-ttu-id="872d7-373">Uma lista delimitada por ponto e vírgula de origens de pacote.</span><span class="sxs-lookup"><span data-stu-id="872d7-373">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="872d7-374">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="872d7-374">RestorePackagesPath</span></span> | <span data-ttu-id="872d7-375">Caminho da pasta dos pacotes do usuário.</span><span class="sxs-lookup"><span data-stu-id="872d7-375">User packages folder path.</span></span> |
| <span data-ttu-id="872d7-376">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="872d7-376">RestoreDisableParallel</span></span> | <span data-ttu-id="872d7-377">Limite os downloads para um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="872d7-377">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="872d7-378">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="872d7-378">RestoreConfigFile</span></span> | <span data-ttu-id="872d7-379">Caminho para um arquivo `Nuget.Config` a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="872d7-379">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="872d7-380">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="872d7-380">RestoreNoCache</span></span> | <span data-ttu-id="872d7-381">Se for true, evita o uso de pacotes armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="872d7-381">If true, avoids using cached packages.</span></span> <span data-ttu-id="872d7-382">Consulte [Gerenciando os pacotes globais e as pastas de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="872d7-382">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="872d7-383">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="872d7-383">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="872d7-384">Se verdadeiro, ignora origens de pacote com falha ou ausentes.</span><span class="sxs-lookup"><span data-stu-id="872d7-384">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="872d7-385">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="872d7-385">RestoreFallbackFolders</span></span> | <span data-ttu-id="872d7-386">Pastas de fallback, usadas da mesma maneira que a pasta pacotes de usuário é usada.</span><span class="sxs-lookup"><span data-stu-id="872d7-386">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="872d7-387">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="872d7-387">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="872d7-388">Fontes adicionais a serem usadas durante a restauração.</span><span class="sxs-lookup"><span data-stu-id="872d7-388">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="872d7-389">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="872d7-389">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="872d7-390">Pastas de fallback adicionais a serem usadas durante a restauração.</span><span class="sxs-lookup"><span data-stu-id="872d7-390">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="872d7-391">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="872d7-391">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="872d7-392">Exclui as pastas de fallback especificadas em `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="872d7-392">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="872d7-393">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="872d7-393">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="872d7-394">Caminho para `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="872d7-394">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="872d7-395">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="872d7-395">RestoreGraphProjectInput</span></span> | <span data-ttu-id="872d7-396">Lista separada por ponto e vírgula de projetos a serem restaurados, que devem conter caminhos absolutos.</span><span class="sxs-lookup"><span data-stu-id="872d7-396">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="872d7-397">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="872d7-397">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="872d7-398">Quando os projetos são coletados via MSBuild, ele determina se eles são coletados usando a `SkipNonexistentTargets` otimização.</span><span class="sxs-lookup"><span data-stu-id="872d7-398">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="872d7-399">Quando não definido, o padrão é `true` .</span><span class="sxs-lookup"><span data-stu-id="872d7-399">When not set, defaults to `true`.</span></span> <span data-ttu-id="872d7-400">A conseqüência é um comportamento com falha rápida quando os destinos de um projeto não podem ser importados.</span><span class="sxs-lookup"><span data-stu-id="872d7-400">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="872d7-401">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="872d7-401">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="872d7-402">Pasta de saída, padronizando para `BaseIntermediateOutputPath` e a `obj` pasta.</span><span class="sxs-lookup"><span data-stu-id="872d7-402">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="872d7-403">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="872d7-403">RestoreForce</span></span> | <span data-ttu-id="872d7-404">Em projetos baseados em PackageReference, o forçará a resolução de todas as dependências, mesmo que a última restauração tenha sido bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="872d7-404">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="872d7-405">A especificação desse sinalizador é semelhante à exclusão do `project.assets.json` arquivo.</span><span class="sxs-lookup"><span data-stu-id="872d7-405">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="872d7-406">Isso não ignora o cache http.</span><span class="sxs-lookup"><span data-stu-id="872d7-406">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="872d7-407">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="872d7-407">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="872d7-408">Opta pelo uso de um arquivo de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="872d7-408">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="872d7-409">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="872d7-409">RestoreLockedMode</span></span> | <span data-ttu-id="872d7-410">Execute RESTORE no modo bloqueado.</span><span class="sxs-lookup"><span data-stu-id="872d7-410">Run restore in locked mode.</span></span> <span data-ttu-id="872d7-411">Isso significa que a restauração não reavaliará as dependências.</span><span class="sxs-lookup"><span data-stu-id="872d7-411">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="872d7-412">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="872d7-412">NuGetLockFilePath</span></span> | <span data-ttu-id="872d7-413">Um local personalizado para o arquivo de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="872d7-413">A custom location for the lock file.</span></span> <span data-ttu-id="872d7-414">O local padrão é ao lado do projeto e é nomeado `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="872d7-414">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="872d7-415">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="872d7-415">RestoreForceEvaluate</span></span> | <span data-ttu-id="872d7-416">Força a restauração a recalcular as dependências e atualizar o arquivo de bloqueio sem nenhum aviso.</span><span class="sxs-lookup"><span data-stu-id="872d7-416">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="872d7-417">RestorePackagesConfig</span><span class="sxs-lookup"><span data-stu-id="872d7-417">RestorePackagesConfig</span></span> | <span data-ttu-id="872d7-418">Uma opção opcional que restaura projetos com packages.config. Suporte `MSBuild -t:restore` apenas com.</span><span class="sxs-lookup"><span data-stu-id="872d7-418">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| <span data-ttu-id="872d7-419">RestoreUseStaticGraphEvaluation</span><span class="sxs-lookup"><span data-stu-id="872d7-419">RestoreUseStaticGraphEvaluation</span></span> | <span data-ttu-id="872d7-420">Uma opção de aceitação para usar a avaliação do MSBuild do grafo estático em vez da avaliação padrão.</span><span class="sxs-lookup"><span data-stu-id="872d7-420">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="872d7-421">A avaliação estática do grafo é um recurso experimental que é significativamente mais rápido para repositórios e soluções grandes.</span><span class="sxs-lookup"><span data-stu-id="872d7-421">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="872d7-422">Exemplos</span><span class="sxs-lookup"><span data-stu-id="872d7-422">Examples</span></span>

<span data-ttu-id="872d7-423">Linha de comando:</span><span class="sxs-lookup"><span data-stu-id="872d7-423">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="872d7-424">Arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="872d7-424">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="872d7-425">Restaurar saídas</span><span class="sxs-lookup"><span data-stu-id="872d7-425">Restore outputs</span></span>

<span data-ttu-id="872d7-426">A restauração cria os seguintes arquivos na pasta `obj` de build:</span><span class="sxs-lookup"><span data-stu-id="872d7-426">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="872d7-427">Arquivo</span><span class="sxs-lookup"><span data-stu-id="872d7-427">File</span></span> | <span data-ttu-id="872d7-428">Descrição</span><span class="sxs-lookup"><span data-stu-id="872d7-428">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="872d7-429">Contém o grafo de dependência de todas as referências de pacote.</span><span class="sxs-lookup"><span data-stu-id="872d7-429">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="872d7-430">Referências a objetos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="872d7-430">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="872d7-431">Referências a destinos do MSBuild contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="872d7-431">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="872d7-432">Restaurando e compilando com um comando do MSBuild</span><span class="sxs-lookup"><span data-stu-id="872d7-432">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="872d7-433">Devido ao fato de que o NuGet pode restaurar pacotes que desativam destinos e props do MSBuild, as avaliações de restauração e compilação são executadas com propriedades globais diferentes.</span><span class="sxs-lookup"><span data-stu-id="872d7-433">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="872d7-434">Isso significa que o seguinte terá um comportamento imprevisível e geralmente incorreto.</span><span class="sxs-lookup"><span data-stu-id="872d7-434">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="872d7-435">Em vez disso, a abordagem recomendada é:</span><span class="sxs-lookup"><span data-stu-id="872d7-435">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="872d7-436">A mesma lógica se aplica a outros destinos semelhantes a `build` .</span><span class="sxs-lookup"><span data-stu-id="872d7-436">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="872d7-437">Restaurando PackageReference e packages.config com o MSBuild</span><span class="sxs-lookup"><span data-stu-id="872d7-437">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="872d7-438">Com o MSBuild los +, também há suporte para packages.config para `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="872d7-438">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="872d7-439">`packages.config` a restauração está disponível apenas com o `MSBuild 16.5+` , e não com `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="872d7-439">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="872d7-440">Restaurando com a avaliação de grafo estático do MSBuild</span><span class="sxs-lookup"><span data-stu-id="872d7-440">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="872d7-441">Com o MSBuild 16.6 +, o NuGet adicionou um recurso experimental para usar a avaliação estática de grafo a partir da linha de comando que melhora significativamente o tempo de restauração para repositórios grandes.</span><span class="sxs-lookup"><span data-stu-id="872d7-441">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="872d7-442">Como alternativa, você pode habilitá-lo definindo a propriedade em um diretório. Build. props.</span><span class="sxs-lookup"><span data-stu-id="872d7-442">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="872d7-443">A partir do Visual Studio 2019. x e do NuGet 5. x, esse recurso é considerado experimental e opcional.</span><span class="sxs-lookup"><span data-stu-id="872d7-443">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="872d7-444">Siga o [NuGet/Home # 9803](https://github.com/NuGet/Home/issues/9803) para obter detalhes sobre quando esse recurso será habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="872d7-444">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="872d7-445">A restauração estática do grafo altera a parte do MSBuild da restauração, a leitura e a avaliação do projeto, mas não o algoritmo de restauração!</span><span class="sxs-lookup"><span data-stu-id="872d7-445">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="872d7-446">O algoritmo de restauração é o mesmo em todas as ferramentas do NuGet (NuGet.exe, MSBuild.exe, dotnet.exe e Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="872d7-446">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="872d7-447">Em poucos cenários, a restauração estática do grafo pode se comportar de forma diferente da restauração atual e determinados PackageReferences ou ProjectReferences declarados podem estar ausentes.</span><span class="sxs-lookup"><span data-stu-id="872d7-447">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="872d7-448">Para facilitar sua ideia, como uma verificação única, ao migrar para a restauração estática do grafo, considere a execução:</span><span class="sxs-lookup"><span data-stu-id="872d7-448">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="872d7-449">O NuGet *não* deve relatar nenhuma alteração.</span><span class="sxs-lookup"><span data-stu-id="872d7-449">NuGet should *not* report any changes.</span></span> <span data-ttu-id="872d7-450">Se você vir uma discrepância, registre um problema em [NuGet/Home](https://github.com/nuget/home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="872d7-450">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="872d7-451">Substituindo uma biblioteca de um grafo de restauração</span><span class="sxs-lookup"><span data-stu-id="872d7-451">Replacing one library from a restore graph</span></span>

<span data-ttu-id="872d7-452">Se uma restauração está trazendo o assembly errado, é possível excluir a escolha padrão do pacote e substituí-lo por outro de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="872d7-452">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="872d7-453">Primeiro com um `PackageReference` de nível superior, exclua todos os ativos:</span><span class="sxs-lookup"><span data-stu-id="872d7-453">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="872d7-454">Em seguida, adicione sua própria referência à cópia local apropriada da DLL:</span><span class="sxs-lookup"><span data-stu-id="872d7-454">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
