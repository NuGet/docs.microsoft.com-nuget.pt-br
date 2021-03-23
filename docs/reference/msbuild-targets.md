---
title: NuGet empacotar e restaurar como MSBuild destinos
description: NuGet o pacote e a restauração podem funcionar diretamente como MSBuild destinos com NuGet 4.0 +.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 9d40d43d972537ee1cb11d54194ed6450ccd0b6e
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104858960"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="6aeb8-103">NuGet empacotar e restaurar como MSBuild destinos</span><span class="sxs-lookup"><span data-stu-id="6aeb8-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="6aeb8-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="6aeb8-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="6aeb8-105">Com o formato [PackageReference](../consume-packages/package-references-in-project-files.md) , o NuGet 4.0 + pode armazenar todos os metadados do manifesto diretamente dentro de um arquivo de projeto em vez de usar um `.nuspec` arquivo separado.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="6aeb8-106">Com MSBuild o 15.1 +, NuGet também é um cidadão de primeira classe MSBuild com `pack` os `restore` destinos e, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="6aeb8-107">Esses destinos permitem que você trabalhe com NuGet como faria com qualquer outra MSBuild tarefa ou destino.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="6aeb8-108">Para obter instruções sobre como criar um NuGet pacote usando o MSBuild , consulte [criar um NuGet pacote usando MSBuild o ](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="6aeb8-109">(Para NuGet 3. x e anteriores, você usará os comandos [Pack](../reference/cli-reference/cli-ref-pack.md) e [Restore](../reference/cli-reference/cli-ref-restore.md) por meio da NuGet CLI.)</span><span class="sxs-lookup"><span data-stu-id="6aeb8-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="6aeb8-110">Ordem de build de destino</span><span class="sxs-lookup"><span data-stu-id="6aeb8-110">Target build order</span></span>

<span data-ttu-id="6aeb8-111">Como `pack` e `restore` são  MSBuild destinos, você pode acessá-los para aprimorar seu fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="6aeb8-112">Por exemplo, digamos que você deseja copiar o pacote para um compartilhamento de rede depois de empacotá-lo.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-112">For example, let's say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="6aeb8-113">Você pode fazer isso adicionando o seguinte ao seu arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="6aeb8-114">Da mesma forma, você pode escrever uma MSBuild tarefa, escrever seu próprio destino e consumir NuGet as propriedades na MSBuild tarefa.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="6aeb8-115">`$(OutputPath)` é relativo e espera que você esteja executando o comando da raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="6aeb8-116">pack target</span><span class="sxs-lookup"><span data-stu-id="6aeb8-116">pack target</span></span>

<span data-ttu-id="6aeb8-117">Para projetos .NET que usam o `PackageReference` formato, o uso de `msbuild -t:pack` desenha entradas do arquivo de projeto a ser usado na criação de um NuGet pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="6aeb8-118">A tabela a seguir descreve as MSBuild Propriedades que podem ser adicionadas a um arquivo de projeto dentro do primeiro `<PropertyGroup>` nó.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="6aeb8-119">Você pode fazer essas edições facilmente no Visual Studio 2017 e posterior clicando com o botão direito do mouse no projeto e selecionando **Editar {project_name}** no menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="6aeb8-120">Para sua conveniência, a tabela é organizada pela propriedade equivalente em um [ `.nuspec` arquivo](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6aeb8-121">`Owners``Summary`as propriedades e de `.nuspec` não têm suporte com MSBuild .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-121">`Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="6aeb8-122">Atributo/ nuspec valor</span><span class="sxs-lookup"><span data-stu-id="6aeb8-122">Attribute/nuspec Value</span></span> | <span data-ttu-id="6aeb8-123">MSBuild Propriedade</span><span class="sxs-lookup"><span data-stu-id="6aeb8-123">MSBuild Property</span></span> | <span data-ttu-id="6aeb8-124">Padrão</span><span class="sxs-lookup"><span data-stu-id="6aeb8-124">Default</span></span> | <span data-ttu-id="6aeb8-125">Observações</span><span class="sxs-lookup"><span data-stu-id="6aeb8-125">Notes</span></span> |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | <span data-ttu-id="6aeb8-126">`$(AssemblyName)` de MSBuild</span><span class="sxs-lookup"><span data-stu-id="6aeb8-126">`$(AssemblyName)` from MSBuild</span></span> |
| `Version` | `PackageVersion` | <span data-ttu-id="6aeb8-127">Versão</span><span class="sxs-lookup"><span data-stu-id="6aeb8-127">Version</span></span> | <span data-ttu-id="6aeb8-128">Isso é compatível com semver, por exemplo, `1.0.0` `1.0.0-beta` ou `1.0.0-beta-00345`</span><span class="sxs-lookup"><span data-stu-id="6aeb8-128">This is semver compatible, for example `1.0.0`, `1.0.0-beta`, or `1.0.0-beta-00345`</span></span> |
| `VersionPrefix` | `PackageVersionPrefix` | <span data-ttu-id="6aeb8-129">vazio</span><span class="sxs-lookup"><span data-stu-id="6aeb8-129">empty</span></span> | <span data-ttu-id="6aeb8-130">Configurando `PackageVersion` substituições `PackageVersionPrefix`</span><span class="sxs-lookup"><span data-stu-id="6aeb8-130">Setting `PackageVersion` overwrites `PackageVersionPrefix`</span></span> |
| `VersionSuffix` | `PackageVersionSuffix` | <span data-ttu-id="6aeb8-131">vazio</span><span class="sxs-lookup"><span data-stu-id="6aeb8-131">empty</span></span> | <span data-ttu-id="6aeb8-132">`$(VersionSuffix)` de MSBuild .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-132">`$(VersionSuffix)` from MSBuild.</span></span> <span data-ttu-id="6aeb8-133">Configurando `PackageVersion` substituições `PackageVersionSuffix`</span><span class="sxs-lookup"><span data-stu-id="6aeb8-133">Setting `PackageVersion` overwrites `PackageVersionSuffix`</span></span> |
| `Authors` | `Authors` | <span data-ttu-id="6aeb8-134">Nome do usuário atual</span><span class="sxs-lookup"><span data-stu-id="6aeb8-134">Username of the current user</span></span> | <span data-ttu-id="6aeb8-135">Uma lista separada por ponto-e-vírgula de autores de pacotes, que correspondem aos nomes de perfil em nuget.org. Eles são exibidos na NuGet Galeria no NuGet.org e são usados para fazer referência cruzada de pacotes pelos mesmos autores.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-135">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Owners` | <span data-ttu-id="6aeb8-136">N/D</span><span class="sxs-lookup"><span data-stu-id="6aeb8-136">N/A</span></span> | <span data-ttu-id="6aeb8-137">Não presente em nuspec</span><span class="sxs-lookup"><span data-stu-id="6aeb8-137">Not present in nuspec</span></span> | |
| `Title` | `Title` | <span data-ttu-id="6aeb8-138">O `PackageId`</span><span class="sxs-lookup"><span data-stu-id="6aeb8-138">The `PackageId`</span></span> | <span data-ttu-id="6aeb8-139">Um título amigável do pacote, geralmente usado em exibições de interface do usuário como em nuget.org e no Gerenciador de Pacotes do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| `Description` | `Description` | <span data-ttu-id="6aeb8-140">“Package Description”</span><span class="sxs-lookup"><span data-stu-id="6aeb8-140">"Package Description"</span></span> | <span data-ttu-id="6aeb8-141">Uma descrição longa para o manifesto do assembly.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-141">A long description for the assembly.</span></span> <span data-ttu-id="6aeb8-142">Se `PackageDescription` não for especificado, essa propriedade também será usada como a descrição do pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-142">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | `Copyright` | <span data-ttu-id="6aeb8-143">vazio</span><span class="sxs-lookup"><span data-stu-id="6aeb8-143">empty</span></span> | <span data-ttu-id="6aeb8-144">Detalhes sobre direitos autorais do pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-144">Copyright details for the package.</span></span> |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | <span data-ttu-id="6aeb8-145">Um valor booliano que especifica se o cliente deve solicitar que o consumidor aceite a licença do pacote antes de instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-145">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| `license` | `PackageLicenseExpression` | <span data-ttu-id="6aeb8-146">vazio</span><span class="sxs-lookup"><span data-stu-id="6aeb8-146">empty</span></span> | <span data-ttu-id="6aeb8-147">Corresponde ao `<license type="expression">`.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-147">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="6aeb8-148">Consulte [empacotando uma expressão de licença ou um arquivo de licença](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-148">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `license` | `PackageLicenseFile` | <span data-ttu-id="6aeb8-149">vazio</span><span class="sxs-lookup"><span data-stu-id="6aeb8-149">empty</span></span> | <span data-ttu-id="6aeb8-150">Caminho para um arquivo de licença dentro do pacote se você estiver usando uma licença personalizada ou uma licença que não tenha sido atribuída a um identificador SPDX.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-150">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="6aeb8-151">Você precisa empacotar explicitamente o arquivo de licença referenciado.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-151">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="6aeb8-152">Corresponde ao `<license type="file">`.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-152">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="6aeb8-153">Consulte [empacotando uma expressão de licença ou um arquivo de licença](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-153">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `LicenseUrl` | `PackageLicenseUrl` | <span data-ttu-id="6aeb8-154">vazio</span><span class="sxs-lookup"><span data-stu-id="6aeb8-154">empty</span></span> | <span data-ttu-id="6aeb8-155">O `PackageLicenseUrl` foi preterido.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-155">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="6aeb8-156">Use `PackageLicenseExpression` ou `PackageLicenseFile` em vez disso.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-156">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `ProjectUrl` | `PackageProjectUrl` | <span data-ttu-id="6aeb8-157">vazio</span><span class="sxs-lookup"><span data-stu-id="6aeb8-157">empty</span></span> | |
| `Icon` | `PackageIcon` | <span data-ttu-id="6aeb8-158">vazio</span><span class="sxs-lookup"><span data-stu-id="6aeb8-158">empty</span></span> | <span data-ttu-id="6aeb8-159">Um caminho para uma imagem no pacote a ser usado como um ícone de pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-159">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="6aeb8-160">Você precisa empacotar explicitamente o arquivo de imagem do ícone referenciado.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-160">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="6aeb8-161">Para obter mais informações, consulte [empacotando um arquivo de imagem de ícone](#packing-an-icon-image-file) e [ `icon` metadados](/nuget/reference/nuspec#icon).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-161">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](/nuget/reference/nuspec#icon).</span></span> |
| `IconUrl` | `PackageIconUrl` | <span data-ttu-id="6aeb8-162">vazio</span><span class="sxs-lookup"><span data-stu-id="6aeb8-162">empty</span></span> | <span data-ttu-id="6aeb8-163">`PackageIconUrl` é preterido em favor do `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-163">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="6aeb8-164">No entanto, para obter a melhor experiência de nível inferior, você deve especificar, `PackageIconUrl` além do `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-164">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| `Tags` | `PackageTags` | <span data-ttu-id="6aeb8-165">vazio</span><span class="sxs-lookup"><span data-stu-id="6aeb8-165">empty</span></span> | <span data-ttu-id="6aeb8-166">Uma lista delimitada por ponto e vírgula de marcas que designam o pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-166">A semicolon-delimited list of tags that designates the package.</span></span> |
| `ReleaseNotes` | `PackageReleaseNotes` | <span data-ttu-id="6aeb8-167">vazio</span><span class="sxs-lookup"><span data-stu-id="6aeb8-167">empty</span></span> | <span data-ttu-id="6aeb8-168">Notas de versão do projeto.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-168">Release notes for the package.</span></span> |
| `Repository/Url` | `RepositoryUrl` | <span data-ttu-id="6aeb8-169">vazio</span><span class="sxs-lookup"><span data-stu-id="6aeb8-169">empty</span></span> | <span data-ttu-id="6aeb8-170">URL do repositório usada para clonar ou recuperar o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-170">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="6aeb8-171">Exemplo: *https://github.com/ NuGet / NuGet . Client. git*.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-171">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `Repository/Type` | `RepositoryType` | <span data-ttu-id="6aeb8-172">vazio</span><span class="sxs-lookup"><span data-stu-id="6aeb8-172">empty</span></span> | <span data-ttu-id="6aeb8-173">Tipo de repositório.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-173">Repository type.</span></span> <span data-ttu-id="6aeb8-174">Exemplos: `git` (padrão), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-174">Examples: `git` (default), `tfs`.</span></span> |
| `Repository/Branch` | `RepositoryBranch` | <span data-ttu-id="6aeb8-175">vazio</span><span class="sxs-lookup"><span data-stu-id="6aeb8-175">empty</span></span> | <span data-ttu-id="6aeb8-176">Informações opcionais da ramificação do repositório.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-176">Optional repository branch information.</span></span> <span data-ttu-id="6aeb8-177">`RepositoryUrl` também deve ser especificado para que essa propriedade seja incluída.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-177">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="6aeb8-178">Exemplo: *Master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-178">Example: *master* (NuGet 4.7.0+).</span></span> |
| `Repository/Commit` | `RepositoryCommit` | <span data-ttu-id="6aeb8-179">vazio</span><span class="sxs-lookup"><span data-stu-id="6aeb8-179">empty</span></span> | <span data-ttu-id="6aeb8-180">Confirmação opcional do repositório ou conjunto de alterações para indicar de qual fonte o pacote foi criado.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-180">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="6aeb8-181">`RepositoryUrl` também deve ser especificado para que essa propriedade seja incluída.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-181">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="6aeb8-182">Exemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-182">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | <span data-ttu-id="6aeb8-183">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="6aeb8-183">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="6aeb8-184">pack target inputs</span><span class="sxs-lookup"><span data-stu-id="6aeb8-184">pack target inputs</span></span>

| <span data-ttu-id="6aeb8-185">Propriedade</span><span class="sxs-lookup"><span data-stu-id="6aeb8-185">Property</span></span> | <span data-ttu-id="6aeb8-186">Descrição</span><span class="sxs-lookup"><span data-stu-id="6aeb8-186">Description</span></span> |
| - | - |
| `IsPackable` | <span data-ttu-id="6aeb8-187">Um valor booliano que especifica se o projeto pode ser empacotado.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-187">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="6aeb8-188">O valor padrão é `true`.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-188">The default value is `true`.</span></span> |
| `SuppressDependenciesWhenPacking` | <span data-ttu-id="6aeb8-189">Defina como `true` para suprimir as dependências de pacote do NuGet pacote gerado.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-189">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| `PackageVersion` | <span data-ttu-id="6aeb8-190">Especifica a versão que o pacote resultante terá.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-190">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="6aeb8-191">Aceita todas as formas de NuGet cadeia de caracteres de versão.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-191">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="6aeb8-192">O padrão é o valor `$(Version)`, ou seja, da propriedade `Version` no projeto.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-192">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| `PackageId` | <span data-ttu-id="6aeb8-193">Especifica o nome para o pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-193">Specifies the name for the resulting package.</span></span> <span data-ttu-id="6aeb8-194">Se não for especificado, a operação `pack` usará como padrão o `AssemblyName` ou o nome do diretório como o nome do pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-194">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| `PackageDescription` | <span data-ttu-id="6aeb8-195">Uma descrição longa do pacote para exibição de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-195">A long description of the package for UI display.</span></span> |
| `Authors` | <span data-ttu-id="6aeb8-196">Uma lista separada por ponto-e-vírgula de autores de pacotes, que correspondem aos nomes de perfil em nuget.org. Eles são exibidos na NuGet Galeria no NuGet.org e são usados para fazer referência cruzada de pacotes pelos mesmos autores.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-196">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Description` | <span data-ttu-id="6aeb8-197">Uma descrição longa para o manifesto do assembly.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-197">A long description for the assembly.</span></span> <span data-ttu-id="6aeb8-198">Se `PackageDescription` não for especificado, essa propriedade também será usada como a descrição do pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-198">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | <span data-ttu-id="6aeb8-199">Detalhes sobre direitos autorais do pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-199">Copyright details for the package.</span></span> |
| `PackageRequireLicenseAcceptance` | <span data-ttu-id="6aeb8-200">Um valor booliano que especifica se o cliente deve solicitar que o consumidor aceite a licença do pacote antes de instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-200">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="6aeb8-201">O padrão é `false`.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-201">The default is `false`.</span></span> |
| `DevelopmentDependency` | <span data-ttu-id="6aeb8-202">Um valor booliano que especifica se o pacote está marcado como uma dependência somente de desenvolvimento, o que impede que o pacote seja incluído como uma dependência em outros pacotes.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-202">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="6aeb8-203">Com `PackageReference` ( NuGet 4.8 +), esse sinalizador também significa que os ativos de tempo de compilação são excluídos da compilação.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-203">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="6aeb8-204">Para obter mais informações, confira [Suporte do DevelopmentDependency para PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-204">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| `PackageLicenseExpression` | <span data-ttu-id="6aeb8-205">Uma expressão ou um [identificador de licença SPDX](https://spdx.org/licenses/) , por exemplo, `Apache-2.0` .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-205">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="6aeb8-206">Para obter mais informações, consulte [empacotando uma expressão de licença ou um arquivo de licença](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-206">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `PackageLicenseFile` | <span data-ttu-id="6aeb8-207">Caminho para um arquivo de licença dentro do pacote se você estiver usando uma licença personalizada ou uma licença que não tenha sido atribuída a um identificador SPDX.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-207">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| `PackageLicenseUrl` | <span data-ttu-id="6aeb8-208">O `PackageLicenseUrl` foi preterido.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-208">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="6aeb8-209">Use `PackageLicenseExpression` ou `PackageLicenseFile` em vez disso.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-209">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `PackageProjectUrl` | |
| `PackageIcon` | <span data-ttu-id="6aeb8-210">Especifica o caminho do ícone de pacote, relativo à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-210">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="6aeb8-211">Para obter mais informações, consulte [empacotando um arquivo de imagem de ícone](#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-211">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| `PackageReleaseNotes` | <span data-ttu-id="6aeb8-212">Notas de versão do projeto.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-212">Release notes for the package.</span></span> |
| `PackageTags` | <span data-ttu-id="6aeb8-213">Uma lista delimitada por ponto e vírgula de marcas que designam o pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-213">A semicolon-delimited list of tags that designates the package.</span></span> |
| `PackageOutputPath` | <span data-ttu-id="6aeb8-214">Determina o caminho de saída no qual o pacote empacotado será solto.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-214">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="6aeb8-215">O padrão é `$(OutputPath)`.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-215">Default is `$(OutputPath)`.</span></span> |
| `IncludeSymbols` | <span data-ttu-id="6aeb8-216">Esse valor booliano indica se o pacote deve criar um pacote de símbolos adicionais quando o projeto é empacotado.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-216">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="6aeb8-217">O formato do pacote de símbolos é controlado pela propriedade `SymbolPackageFormat`.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-217">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="6aeb8-218">Para obter mais informações, consulte [IncludeSymbols](#includesymbols).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-218">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| `IncludeSource` | <span data-ttu-id="6aeb8-219">Esse valor booliano indica se o processo do pacote deve criar um pacote de origem.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-219">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="6aeb8-220">O pacote de origem contém o código-fonte da biblioteca, bem como arquivos PDB.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-220">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="6aeb8-221">Os arquivos de origem são colocados no diretório `src/ProjectName`, no arquivo de pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-221">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="6aeb8-222">Para obter mais informações, consulte [includename](#includesource).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-222">For more information, see [IncludeSource](#includesource).</span></span> |
| `PackageType` | |
| `IsTool` | <span data-ttu-id="6aeb8-223">Especifica se todos os arquivos de saída são copiados para a pasta *tools* em vez da pasta *lib*.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-223">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="6aeb8-224">Para obter mais informações, consulte [istool](#istool).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-224">For more information, see [IsTool](#istool).</span></span> |
| `RepositoryUrl` | <span data-ttu-id="6aeb8-225">URL do repositório usada para clonar ou recuperar o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-225">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="6aeb8-226">Exemplo: *https://github.com/ NuGet / NuGet . Client. git*.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-226">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `RepositoryType` | <span data-ttu-id="6aeb8-227">Tipo de repositório.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-227">Repository type.</span></span> <span data-ttu-id="6aeb8-228">Exemplos: `git` (padrão), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-228">Examples: `git` (default), `tfs`.</span></span> |
| `RepositoryBranch` | <span data-ttu-id="6aeb8-229">Informações opcionais da ramificação do repositório.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-229">Optional repository branch information.</span></span> <span data-ttu-id="6aeb8-230">`RepositoryUrl` também deve ser especificado para que essa propriedade seja incluída.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-230">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="6aeb8-231">Exemplo: *Master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-231">Example: *master* (NuGet 4.7.0+).</span></span> |
| `RepositoryCommit` | <span data-ttu-id="6aeb8-232">Confirmação opcional do repositório ou conjunto de alterações para indicar de qual fonte o pacote foi criado.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-232">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="6aeb8-233">`RepositoryUrl` também deve ser especificado para que essa propriedade seja incluída.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-233">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="6aeb8-234">Exemplo: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-234">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `SymbolPackageFormat` | <span data-ttu-id="6aeb8-235">Especifica o formato do pacote de símbolos.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-235">Specifies the format of the symbols package.</span></span> <span data-ttu-id="6aeb8-236">Se "Symbols. nupkg", um pacote de símbolos herdados será criado com uma extensão *. Symbols. nupkg* contendo PDBs, DLLs e outros arquivos de saída.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-236">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="6aeb8-237">Se "snupkg", um pacote de símbolos snupkg será criado contendo os PDBs portáteis.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-237">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="6aeb8-238">O padrão é "Symbols. nupkg".</span><span class="sxs-lookup"><span data-stu-id="6aeb8-238">The default is "symbols.nupkg".</span></span> |
| `NoPackageAnalysis` | <span data-ttu-id="6aeb8-239">Especifica que o `pack` não deve executar a análise de pacote depois de criar o pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-239">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| `MinClientVersion` | <span data-ttu-id="6aeb8-240">Especifica a versão mínima do NuGet cliente que pode instalar este pacote, imposta por nuget.exe e o Gerenciador de pacotes do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-240">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| `IncludeBuildOutput` | <span data-ttu-id="6aeb8-241">Esse valor booliano especifica se os assemblies de saída da compilação devem ser empacotados no arquivo *. nupkg* ou não.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-241">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| `IncludeContentInPack` | <span data-ttu-id="6aeb8-242">Esse valor booliano especifica se os itens que têm um tipo de `Content` são incluídos automaticamente no pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-242">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="6aeb8-243">O padrão é `true`.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-243">The default is `true`.</span></span> |
| `BuildOutputTargetFolder` | <span data-ttu-id="6aeb8-244">Especifica a pasta para colocar os assemblies de saída.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-244">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="6aeb8-245">Os assemblies de saída (e outros arquivos de saída) são copiados para suas respectivas pastas de estrutura.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-245">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="6aeb8-246">Para obter mais informações, consulte [assemblies de saída](#output-assemblies).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-246">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| `ContentTargetFolders` | <span data-ttu-id="6aeb8-247">Especifica o local padrão de onde todos os arquivos de conteúdo devem ir se `PackagePath` não forem especificados para eles.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-247">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="6aeb8-248">O valor padrão é “content;contentFiles”.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-248">The default value is "content;contentFiles".</span></span> <span data-ttu-id="6aeb8-249">Para obter mais informações, consulte [Incluindo conteúdo em um pacote](#including-content-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-249">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| `NuspecFile` | <span data-ttu-id="6aeb8-250">Caminho relativo ou absoluto para o *.nuspec* arquivo que está sendo usado para empacotamento.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-250">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="6aeb8-251">Se especificado, ele será usado **exclusivamente** para informações de empacotamento e quaisquer informações nos projetos não serão usadas.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-251">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="6aeb8-252">Para obter mais informações, consulte [empacotando .nuspec usando um ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-252">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecBasePath` | <span data-ttu-id="6aeb8-253">Caminho base do *.nuspec* arquivo.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-253">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="6aeb8-254">Para obter mais informações, consulte [empacotando .nuspec usando um ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-254">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecProperties` | <span data-ttu-id="6aeb8-255">Lista separada por ponto e vírgula de pares chave-valor.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-255">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="6aeb8-256">Para obter mais informações, consulte [empacotando .nuspec usando um ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-256">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="6aeb8-257">pack scenarios</span><span class="sxs-lookup"><span data-stu-id="6aeb8-257">pack scenarios</span></span>

### <a name="suppressing-dependencies"></a><span data-ttu-id="6aeb8-258">Suprimindo dependências</span><span class="sxs-lookup"><span data-stu-id="6aeb8-258">Suppressing dependencies</span></span>

<span data-ttu-id="6aeb8-259">Para suprimir as dependências de pacote do NuGet pacote gerado, defina `SuppressDependenciesWhenPacking` como `true` que permitirá ignorar todas as dependências do arquivo nupkg gerado.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-259">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### `PackageIconUrl`

<span data-ttu-id="6aeb8-260">`PackageIconUrl` é preterido em favor da [`PackageIcon`](#packageicon) propriedade.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-260">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="6aeb8-261">A partir NuGet do 5,3 e do Visual Studio 2019 versão 16,3, `pack` o gerará o aviso [NU5048](./errors-and-warnings/nu5048.md) se os metadados do pacote especificarem apenas `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-261">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### `PackageIcon`

> [!Tip]
> <span data-ttu-id="6aeb8-262">Para manter a compatibilidade com versões anteriores com clientes e fontes que ainda não dão suporte `PackageIcon` , especifique `PackageIcon` e `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-262">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="6aeb8-263">O Visual Studio dá suporte a `PackageIcon` pacotes provenientes de uma fonte baseada em pasta.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-263">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="6aeb8-264">Empacotando um arquivo de imagem de ícone</span><span class="sxs-lookup"><span data-stu-id="6aeb8-264">Packing an icon image file</span></span>

<span data-ttu-id="6aeb8-265">Ao empacotar um arquivo de imagem de ícone, use `PackageIcon` a propriedade para especificar o caminho do arquivo de ícone, em relação à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-265">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="6aeb8-266">Além disso, certifique-se de que o arquivo está incluído no pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-266">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="6aeb8-267">O tamanho do arquivo de imagem é limitado a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-267">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="6aeb8-268">Os formatos de arquivo com suporte incluem JPEG e PNG.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-268">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="6aeb8-269">Recomendamos uma resolução de imagem de 128x128.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-269">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="6aeb8-270">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-270">For example:</span></span>

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

<span data-ttu-id="6aeb8-271">[Exemplo de ícone de pacote](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-271">[Package Icon sample](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span></span>

<span data-ttu-id="6aeb8-272">Para o nuspec equivalente, dê uma olhada na [ nuspec referência para o ícone](nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-272">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="6aeb8-273">Assemblies de saída</span><span class="sxs-lookup"><span data-stu-id="6aeb8-273">Output assemblies</span></span>

<span data-ttu-id="6aeb8-274">O `nuget pack` copia arquivos de saída com extensões `.exe`, `.dll`, `.xml`, `.winmd`, `.json` e `.pri`.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-274">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="6aeb8-275">Os arquivos de saída copiados dependem do que o MSBuild fornece do `BuiltOutputProjectGroup` destino.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-275">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="6aeb8-276">Há duas MSBuild  Propriedades que você pode usar em seu arquivo de projeto ou linha de comando para controlar onde os assemblies de saída vão:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-276">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="6aeb8-277">`IncludeBuildOutput`: um valor booliano que determina se os assemblies de saída de build devem ser incluídos no pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-277">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="6aeb8-278">`BuildOutputTargetFolder`: especifica a pasta na qual os assemblies de saída devem ser colocados.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-278">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="6aeb8-279">Os assemblies de saída (e outros arquivos de saída) são copiados para suas respectivas pastas de estrutura.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-279">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="6aeb8-280">Referências de pacote</span><span class="sxs-lookup"><span data-stu-id="6aeb8-280">Package references</span></span>

<span data-ttu-id="6aeb8-281">Consulte [Referências de pacote em arquivos de projeto](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-281">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="6aeb8-282">Referências de projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="6aeb8-282">Project to project references</span></span>

<span data-ttu-id="6aeb8-283">As referências de projeto para projeto são consideradas por padrão como NuGet referências de pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-283">Project to project references are considered by default as NuGet package references.</span></span> <span data-ttu-id="6aeb8-284">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-284">For example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="6aeb8-285">Você também pode adicionar os seguintes metadados à referência de projeto:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-285">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="6aeb8-286">Incluindo o conteúdo em um pacote</span><span class="sxs-lookup"><span data-stu-id="6aeb8-286">Including content in a package</span></span>

<span data-ttu-id="6aeb8-287">Para incluir o conteúdo, adicione metadados extras ao item `<Content>` existente.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-287">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="6aeb8-288">Por padrão, tudo que pertencer ao tipo “Conteúdo” é incluído no pacote, a menos que seja substituído por entradas como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-288">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="6aeb8-289">Por padrão, tudo é adicionado à raiz da pasta `content` e `contentFiles\any\<target_framework>` dentro de um pacote e preserva a estrutura e pasta relativa, a menos que você especifique um caminho de pacote:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-289">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="6aeb8-290">Se você quiser copiar todo o conteúdo para apenas uma pasta (s) raiz específica (em vez de `content` e `contentFiles` ambos), poderá usar a MSBuild propriedade `ContentTargetFolders` , que usa como padrão "Content; contentFiles", mas pode ser definida como qualquer outro nome de pasta.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-290">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="6aeb8-291">Observe que só especificar “contentFiles” em `ContentTargetFolders` coloca os arquivos em `contentFiles\any\<target_framework>` ou `contentFiles\<language>\<target_framework>` com base em `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-291">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="6aeb8-292">`PackagePath` pode ser um conjunto de caminhos de destino separados por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-292">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="6aeb8-293">Especificar um caminho de pacote vazio adicionaria o arquivo à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-293">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="6aeb8-294">Por exemplo, o seguinte adiciona `libuv.txt` a `content\myfiles`, `content\samples` e a raiz do pacote:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-294">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="6aeb8-295">Há também uma MSBuild propriedade `$(IncludeContentInPack)` , que usa como padrão `true` .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-295">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="6aeb8-296">Se isso for definido como `false` em qualquer projeto, o conteúdo desse projeto não está incluso no pacote do nuget.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-296">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="6aeb8-297">Outros metadados específicos do pacote que você pode definir em qualquer um dos itens acima incluem ```<PackageCopyToOutput>``` e ```<PackageFlatten>``` quais conjuntos ```CopyToOutput``` e ```Flatten``` valores na ```contentFiles``` entrada na saída nuspec .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-297">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="6aeb8-298">Além de itens de Conteúdo, os metadados `<Pack>` e `<PackagePath>` também podem ser definidos em arquivos com uma ação de Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource ou None.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-298">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="6aeb8-299">Para o pacote acrescentar o nome de arquivo ao caminho do pacote ao usar padrões glob, seu caminho de pacote deve terminar com o caractere separador de pasta, caso contrário, o caminho do pacote será tratado como o caminho completo, incluindo o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-299">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="6aeb8-300">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="6aeb8-300">IncludeSymbols</span></span>

<span data-ttu-id="6aeb8-301">Ao usar o `MSBuild -t:pack -p:IncludeSymbols=true`, os arquivos `.pdb` correspondentes são copiados junto com outros arquivos de saída (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-301">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="6aeb8-302">Observe que a configuração `IncludeSymbols=true` cria um pacote regular *e* um pacote de símbolos.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-302">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="6aeb8-303">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="6aeb8-303">IncludeSource</span></span>

<span data-ttu-id="6aeb8-304">Isso é o mesmo que `IncludeSymbols`, exceto que também copia os arquivos de origem com arquivos `.pdb`.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-304">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="6aeb8-305">Todos os arquivos do tipo `Compile` são copiadas para `src\<ProjectName>\`, preservando a estrutura de pastas do caminho relativo no pacote resultante.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-305">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="6aeb8-306">O mesmo também ocorre para arquivos de origem de qualquer `ProjectReference` que tem `TreatAsPackageReference` definido como `false`.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-306">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="6aeb8-307">Se um arquivo do tipo Compilação estiver fora da pasta de projeto, ele será adicionado apenas a `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-307">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="6aeb8-308">Empacotando uma expressão de licença ou um arquivo de licença</span><span class="sxs-lookup"><span data-stu-id="6aeb8-308">Packing a license expression or a license file</span></span>

<span data-ttu-id="6aeb8-309">Ao usar uma expressão de licença, use a `PackageLicenseExpression` propriedade.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-309">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="6aeb8-310">Para obter um exemplo, consulte [exemplo de expressão de licença](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-310">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="6aeb8-311">Para saber mais sobre as expressões de licença e as licenças que são aceitas pelo NuGet . org, consulte [metadados de licença](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-311">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="6aeb8-312">Ao empacotar um arquivo de licença, use `PackageLicenseFile` a propriedade para especificar o caminho do pacote, em relação à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-312">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="6aeb8-313">Além disso, certifique-se de que o arquivo está incluído no pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-313">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="6aeb8-314">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-314">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="6aeb8-315">Para obter um exemplo, consulte [exemplo de arquivo de licença](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-315">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="6aeb8-316">Somente um de `PackageLicenseExpression` , `PackageLicenseFile` e `PackageLicenseUrl` pode ser especificado por vez.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-316">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="6aeb8-317">Empacotando um arquivo sem uma extensão</span><span class="sxs-lookup"><span data-stu-id="6aeb8-317">Packing a file without an extension</span></span>

<span data-ttu-id="6aeb8-318">Em alguns cenários, como ao empacotar um arquivo de licença, talvez você queira incluir um arquivo sem uma extensão.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-318">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="6aeb8-319">Por motivos históricos, NuGet  &  MSBuild trate os caminhos sem uma extensão como diretórios.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-319">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="6aeb8-320">[Arquivo sem um exemplo de extensão](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-320">[File without an extension sample](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span></span>

### <a name="istool"></a><span data-ttu-id="6aeb8-321">IsTool</span><span class="sxs-lookup"><span data-stu-id="6aeb8-321">IsTool</span></span>

<span data-ttu-id="6aeb8-322">Ao usar `MSBuild -t:pack -p:IsTool=true`, todos os arquivos de saída, conforme especificado no cenário [Assemblies de saída](#output-assemblies), são copiados para a pasta `tools` em vez da pasta `lib`.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-322">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="6aeb8-323">Observe que isso é diferente de um `DotNetCliTool` que é especificado pela configuração do `PackageType` no arquivo `.csproj`.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-323">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec-file"></a><span data-ttu-id="6aeb8-324">Empacotamento usando um `.nuspec` arquivo</span><span class="sxs-lookup"><span data-stu-id="6aeb8-324">Packing using a `.nuspec` file</span></span>

<span data-ttu-id="6aeb8-325">Embora seja recomendável [incluir todas as propriedades](../reference/msbuild-targets.md#pack-target) que normalmente estão no `.nuspec` arquivo no arquivo de projeto, você pode optar por usar um `.nuspec` arquivo para empacotar seu projeto.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-325">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="6aeb8-326">Para um projeto de estilo não-SDK que usa `PackageReference` o, você deve importar `NuGet.Build.Tasks.Pack.targets` para que a tarefa de pacote possa ser executada.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-326">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="6aeb8-327">Você ainda precisa restaurar o projeto antes de poder empacotar um nuspec arquivo.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-327">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="6aeb8-328">(Um projeto no estilo SDK inclui os destinos do pacote por padrão.)</span><span class="sxs-lookup"><span data-stu-id="6aeb8-328">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="6aeb8-329">A estrutura de destino do arquivo de projeto é irrelevante e não é usada ao empacotar um nuspec .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-329">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="6aeb8-330">As três propriedades a seguir MSBuild são relevantes para empacotamento usando um `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="6aeb8-330">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="6aeb8-331">`NuspecFile`: caminho relativo ou absoluto para o arquivo `.nuspec` que está sendo usado para o empacotamento.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-331">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="6aeb8-332">`NuspecProperties`: uma lista separada por ponto e vírgula de pares chave/valor.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-332">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="6aeb8-333">Devido à maneira como a MSBuild análise da linha de comando funciona, várias propriedades devem ser especificadas da seguinte maneira: `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-333">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="6aeb8-334">`NuspecBasePath`: o caminho base para o arquivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-334">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="6aeb8-335">Se estiver usando `dotnet.exe` para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-335">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="6aeb8-336">Se estiver usando MSBuild para empacotar seu projeto, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-336">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="6aeb8-337">Observe que empacotar um nuspec usando dotnet.exe ou o MSBuild também leva a criar o projeto por padrão.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-337">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="6aeb8-338">Isso pode ser evitado passando ```--no-build``` a propriedade para dotnet.exe, que é o equivalente à configuração ```<NoBuild>true</NoBuild> ``` em seu arquivo de projeto, juntamente com ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` a configuração no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-338">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="6aeb8-339">Um exemplo de um arquivo *. csproj* para empacotar um nuspec arquivo é:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-339">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="6aeb8-340">Pontos de extensão avançados para criar pacote personalizado</span><span class="sxs-lookup"><span data-stu-id="6aeb8-340">Advanced extension points to create customized package</span></span>

<span data-ttu-id="6aeb8-341">O `pack` destino fornece dois pontos de extensão que são executados na compilação interna, específica da estrutura de destino.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-341">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="6aeb8-342">Os pontos de extensão dão suporte à inclusão de conteúdo específico da estrutura de destino e assemblies em um pacote:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-342">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="6aeb8-343">`TargetsForTfmSpecificBuildOutput` destino: Use para arquivos dentro da `lib` pasta ou de uma pasta especificada usando `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-343">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="6aeb8-344">`TargetsForTfmSpecificContentInPackage` destino: Use para arquivos fora do `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-344">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### `TargetsForTfmSpecificBuildOutput`

<span data-ttu-id="6aeb8-345">Escreva um destino personalizado e especifique-o como o valor da `$(TargetsForTfmSpecificBuildOutput)` propriedade.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-345">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="6aeb8-346">Para todos os arquivos que precisam entrar em `BuildOutputTargetFolder` (lib por padrão), o destino deve gravar esses arquivos no grupo de `BuildOutputInPackage` itens e definir os dois valores de metadados a seguir:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-346">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="6aeb8-347">`FinalOutputPath`: O caminho absoluto do arquivo; Se não for fornecido, a identidade será usada para avaliar o caminho de origem.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-347">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="6aeb8-348">`TargetPath`: (Opcional) defina quando o arquivo precisa entrar em uma subpasta no `lib\<TargetFramework>` , como assemblies satélite que estão em suas respectivas pastas de cultura.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-348">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="6aeb8-349">O padrão é o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-349">Defaults to the name of the file.</span></span>

<span data-ttu-id="6aeb8-350">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-350">Example:</span></span>

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

#### `TargetsForTfmSpecificContentInPackage`

<span data-ttu-id="6aeb8-351">Escreva um destino personalizado e especifique-o como o valor da `$(TargetsForTfmSpecificContentInPackage)` propriedade.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-351">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="6aeb8-352">Para todos os arquivos a serem incluídos no pacote, o destino deve gravar esses arquivos no grupo de `TfmSpecificPackageFile` itens e definir os seguintes metadados opcionais:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-352">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="6aeb8-353">`PackagePath`: Caminho em que o arquivo deve ser apresentado no pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-353">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="6aeb8-354">NuGet emite um aviso se mais de um arquivo for adicionado ao mesmo caminho de pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-354">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="6aeb8-355">`BuildAction`: A ação de compilação a ser atribuída ao arquivo, necessária somente se o caminho do pacote estiver na `contentFiles` pasta.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-355">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="6aeb8-356">O padrão é "None".</span><span class="sxs-lookup"><span data-stu-id="6aeb8-356">Defaults to "None".</span></span>

<span data-ttu-id="6aeb8-357">Um exemplo:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-357">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="6aeb8-358">restore target</span><span class="sxs-lookup"><span data-stu-id="6aeb8-358">restore target</span></span>

<span data-ttu-id="6aeb8-359">`MSBuild -t:restore` (que `nuget restore` e `dotnet restore` usam com projetos do .NET Core), restaura pacotes referenciados no arquivo de projeto da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-359">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="6aeb8-360">Ler todas as referências projeto a projeto</span><span class="sxs-lookup"><span data-stu-id="6aeb8-360">Read all project to project references</span></span>
1. <span data-ttu-id="6aeb8-361">Ler as propriedades do projeto para localizar a pasta intermediária e as estruturas de destino</span><span class="sxs-lookup"><span data-stu-id="6aeb8-361">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="6aeb8-362">Passar MSBuild dados para NuGet.Build.Tasks.dll</span><span class="sxs-lookup"><span data-stu-id="6aeb8-362">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="6aeb8-363">Executar restauração</span><span class="sxs-lookup"><span data-stu-id="6aeb8-363">Run restore</span></span>
1. <span data-ttu-id="6aeb8-364">Baixar os pacotes</span><span class="sxs-lookup"><span data-stu-id="6aeb8-364">Download packages</span></span>
1. <span data-ttu-id="6aeb8-365">Gravar arquivo de ativos, destinos e objetos</span><span class="sxs-lookup"><span data-stu-id="6aeb8-365">Write assets file, targets, and props</span></span>

<span data-ttu-id="6aeb8-366">O `restore` destino funciona para projetos que usam o formato PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-366">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="6aeb8-367">`MSBuild 16.5+` também tem [suporte opcional](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) para o `packages.config` formato.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-367">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="6aeb8-368">O `restore` destino [não deve ser executado](#restoring-and-building-with-one-msbuild-command) em combinação com o `build` destino.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-368">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="6aeb8-369">Restaurar propriedades</span><span class="sxs-lookup"><span data-stu-id="6aeb8-369">Restore properties</span></span>

<span data-ttu-id="6aeb8-370">As configurações de restauração adicionais podem vir de MSBuild Propriedades no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-370">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="6aeb8-371">Os valores também podem ser definidos na linha de comando usando a opção `-p:` (consulte os Exemplos abaixo).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-371">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="6aeb8-372">Propriedade</span><span class="sxs-lookup"><span data-stu-id="6aeb8-372">Property</span></span> | <span data-ttu-id="6aeb8-373">Descrição</span><span class="sxs-lookup"><span data-stu-id="6aeb8-373">Description</span></span> |
|--------|--------|
| `RestoreSources` | <span data-ttu-id="6aeb8-374">Uma lista delimitada por ponto e vírgula de origens de pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-374">Semicolon-delimited list of package sources.</span></span> |
| `RestorePackagesPath` | <span data-ttu-id="6aeb8-375">Caminho da pasta dos pacotes do usuário.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-375">User packages folder path.</span></span> |
| `RestoreDisableParallel` | <span data-ttu-id="6aeb8-376">Limite os downloads para um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-376">Limit downloads to one at a time.</span></span> |
| `RestoreConfigFile` | <span data-ttu-id="6aeb8-377">Caminho para um arquivo `Nuget.Config` a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-377">Path to a `Nuget.Config` file to apply.</span></span> |
| `RestoreNoCache` | <span data-ttu-id="6aeb8-378">Se for true, evita o uso de pacotes armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-378">If true, avoids using cached packages.</span></span> <span data-ttu-id="6aeb8-379">Consulte [Gerenciando os pacotes globais e as pastas de cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-379">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| `RestoreIgnoreFailedSources` | <span data-ttu-id="6aeb8-380">Se verdadeiro, ignora origens de pacote com falha ou ausentes.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-380">If true, ignores failing or missing package sources.</span></span> |
| `RestoreFallbackFolders` | <span data-ttu-id="6aeb8-381">Pastas de fallback, usadas da mesma maneira que a pasta pacotes de usuário é usada.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-381">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| `RestoreAdditionalProjectSources` | <span data-ttu-id="6aeb8-382">Fontes adicionais a serem usadas durante a restauração.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-382">Additional sources to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFolders` | <span data-ttu-id="6aeb8-383">Pastas de fallback adicionais a serem usadas durante a restauração.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-383">Additional fallback folders to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | <span data-ttu-id="6aeb8-384">Exclui as pastas de fallback especificadas em `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="6aeb8-384">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| `RestoreTaskAssemblyFile` | <span data-ttu-id="6aeb8-385">Caminho para `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-385">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| `RestoreGraphProjectInput` | <span data-ttu-id="6aeb8-386">Lista separada por ponto e vírgula de projetos a serem restaurados, que devem conter caminhos absolutos.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-386">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| `RestoreUseSkipNonexistentTargets`  | <span data-ttu-id="6aeb8-387">Quando os projetos são coletados por meio MSBuild dele, ele determina se eles são coletados usando a `SkipNonexistentTargets` otimização.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-387">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="6aeb8-388">Quando não definido, o padrão é `true` .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-388">When not set, defaults to `true`.</span></span> <span data-ttu-id="6aeb8-389">A conseqüência é um comportamento com falha rápida quando os destinos de um projeto não podem ser importados.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-389">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| `MSBuildProjectExtensionsPath` | <span data-ttu-id="6aeb8-390">Pasta de saída, padronizando para `BaseIntermediateOutputPath` e a `obj` pasta.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-390">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| `RestoreForce` | <span data-ttu-id="6aeb8-391">Em projetos baseados em PackageReference, o forçará a resolução de todas as dependências, mesmo que a última restauração tenha sido bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-391">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="6aeb8-392">A especificação desse sinalizador é semelhante à exclusão do `project.assets.json` arquivo.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-392">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="6aeb8-393">Isso não ignora o cache http.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-393">This does not bypass the http-cache.</span></span> |
| `RestorePackagesWithLockFile` | <span data-ttu-id="6aeb8-394">Opta pelo uso de um arquivo de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-394">Opts into the usage of a lock file.</span></span> |
| `RestoreLockedMode` | <span data-ttu-id="6aeb8-395">Execute RESTORE no modo bloqueado.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-395">Run restore in locked mode.</span></span> <span data-ttu-id="6aeb8-396">Isso significa que a restauração não reavaliará as dependências.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-396">This means that restore will not reevaluate the dependencies.</span></span> |
| `NuGetLockFilePath` | <span data-ttu-id="6aeb8-397">Um local personalizado para o arquivo de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-397">A custom location for the lock file.</span></span> <span data-ttu-id="6aeb8-398">O local padrão é ao lado do projeto e é nomeado `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-398">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| `RestoreForceEvaluate` | <span data-ttu-id="6aeb8-399">Força a restauração a recalcular as dependências e atualizar o arquivo de bloqueio sem nenhum aviso.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-399">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| `RestorePackagesConfig` | <span data-ttu-id="6aeb8-400">Uma opção opcional que restaura projetos com packages.config. Suporte `MSBuild -t:restore` apenas com.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-400">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| `RestoreUseStaticGraphEvaluation` | <span data-ttu-id="6aeb8-401">Uma opção opcional para usar a MSBuild avaliação estática do grafo em vez da avaliação padrão.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-401">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="6aeb8-402">A avaliação estática do grafo é um recurso experimental que é significativamente mais rápido para repositórios e soluções grandes.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-402">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="6aeb8-403">Exemplos</span><span class="sxs-lookup"><span data-stu-id="6aeb8-403">Examples</span></span>

<span data-ttu-id="6aeb8-404">Linha de comando:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-404">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="6aeb8-405">Arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-405">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="6aeb8-406">Restaurar saídas</span><span class="sxs-lookup"><span data-stu-id="6aeb8-406">Restore outputs</span></span>

<span data-ttu-id="6aeb8-407">A restauração cria os seguintes arquivos na pasta `obj` de build:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-407">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="6aeb8-408">Arquivo</span><span class="sxs-lookup"><span data-stu-id="6aeb8-408">File</span></span> | <span data-ttu-id="6aeb8-409">Descrição</span><span class="sxs-lookup"><span data-stu-id="6aeb8-409">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="6aeb8-410">Contém o grafo de dependência de todas as referências de pacote.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-410">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="6aeb8-411">Referências a MSBuild props contidas em pacotes</span><span class="sxs-lookup"><span data-stu-id="6aeb8-411">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="6aeb8-412">Referências a MSBuild destinos contidos em pacotes</span><span class="sxs-lookup"><span data-stu-id="6aeb8-412">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="6aeb8-413">Restaurando e compilando com um MSBuild comando</span><span class="sxs-lookup"><span data-stu-id="6aeb8-413">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="6aeb8-414">Devido ao fato de que o NuGet pode restaurar pacotes que trazem MSBuild destinos e props, as avaliações de restauração e de compilação são executadas com propriedades globais diferentes.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-414">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="6aeb8-415">Isso significa que o seguinte terá um comportamento imprevisível e geralmente incorreto.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-415">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="6aeb8-416">Em vez disso, a abordagem recomendada é:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-416">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="6aeb8-417">A mesma lógica se aplica a outros destinos semelhantes a `build` .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-417">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a><span data-ttu-id="6aeb8-418">Restaurando projetos PackageReference e packages.config com MSBuild</span><span class="sxs-lookup"><span data-stu-id="6aeb8-418">Restoring PackageReference and packages.config projects with MSBuild</span></span>

<span data-ttu-id="6aeb8-419">Com o MSBuild packages.config de los +, também há suporte para o `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="6aeb8-419">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="6aeb8-420">`packages.config` a restauração está disponível apenas com o `MSBuild 16.5+` , e não com `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="6aeb8-420">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="6aeb8-421">Restaurando com a MSBuild avaliação estática do grafo</span><span class="sxs-lookup"><span data-stu-id="6aeb8-421">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="6aeb8-422">Com MSBuild o 16.6 +, NuGet adicionou um recurso experimental para usar a avaliação estática do grafo na linha de comando que melhora significativamente o tempo de restauração para repositórios grandes.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-422">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="6aeb8-423">Como alternativa, você pode habilitá-lo definindo a propriedade em um diretório. Build. props.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-423">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="6aeb8-424">A partir do Visual Studio 2019. x e NuGet 5. x, esse recurso é considerado experimental e opcional.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-424">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="6aeb8-425">Siga [ NuGet /Home # 9803](https://github.com/NuGet/Home/issues/9803) para obter detalhes sobre quando esse recurso será habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-425">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="6aeb8-426">A restauração estática do grafo altera a parte do MSBuild da restauração, a leitura e a avaliação do projeto, mas não o algoritmo de restauração!</span><span class="sxs-lookup"><span data-stu-id="6aeb8-426">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="6aeb8-427">O algoritmo de restauração é o mesmo em todas as NuGet ferramentas ( NuGet . exe, MSBuild . exe, dotnet.exe e Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-427">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="6aeb8-428">Em poucos cenários, a restauração estática do grafo pode se comportar de forma diferente da restauração atual e determinados PackageReferences ou ProjectReferences declarados podem estar ausentes.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-428">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="6aeb8-429">Para facilitar sua ideia, como uma verificação única, ao migrar para a restauração estática do grafo, considere a execução:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-429">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="6aeb8-430">NuGet*não* deve relatar nenhuma alteração.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-430">NuGet should *not* report any changes.</span></span> <span data-ttu-id="6aeb8-431">Se você vir uma discrepância, registre um problema em [ NuGet /Home](https://github.com/nuget/home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="6aeb8-431">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="6aeb8-432">Substituindo uma biblioteca de um grafo de restauração</span><span class="sxs-lookup"><span data-stu-id="6aeb8-432">Replacing one library from a restore graph</span></span>

<span data-ttu-id="6aeb8-433">Se uma restauração está trazendo o assembly errado, é possível excluir a escolha padrão do pacote e substituí-lo por outro de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="6aeb8-433">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="6aeb8-434">Primeiro com um `PackageReference` de nível superior, exclua todos os ativos:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-434">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="6aeb8-435">Em seguida, adicione sua própria referência à cópia local apropriada da DLL:</span><span class="sxs-lookup"><span data-stu-id="6aeb8-435">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
