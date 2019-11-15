---
title: Formato PackageReference do NuGet (referências de pacote em arquivos de projeto)
description: Veja detalhes sobre o PackageReference de NuGet em arquivos de projeto compatível com o NuGet 4.0 e posterior e o VS2017 e .Net Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 231947148295e0c06dcec5aa0e1f479d654a8803
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096868"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="b565f-103">Referências de pacote (PackageReference) em arquivos de projeto</span><span class="sxs-lookup"><span data-stu-id="b565f-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="b565f-104">As referências de pacote, usando o nó `PackageReference`, gerenciam as dependências do NuGet diretamente nos arquivos de projeto (em vez de precisar de um arquivo `packages.config` separado).</span><span class="sxs-lookup"><span data-stu-id="b565f-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="b565f-105">O uso de PackageReference, como ele é chamado, não afeta outros aspectos do NuGet; por exemplo, as configurações nos arquivos `NuGet.config` (incluindo as origens do pacote) ainda são aplicadas, conforme explicado em [Configurações comuns do NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="b565f-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="b565f-106">Com o PackageReference, você também pode usar as condições do MSBuild para escolher as referências de pacote por estrutura de destino ou outros agrupamentos.</span><span class="sxs-lookup"><span data-stu-id="b565f-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="b565f-107">Ele também proporciona um controle refinado sobre as dependências e o fluxo de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="b565f-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="b565f-108">(Para obter mais detalhes, veja [Empacotamento e restauração do NuGet como destinos do MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="b565f-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="b565f-109">Suporte do tipo de projeto</span><span class="sxs-lookup"><span data-stu-id="b565f-109">Project type support</span></span>

<span data-ttu-id="b565f-110">Por padrão, o PackageReference é usado para projetos do .NET Core, para projetos do .NET Standard e para projetos da UWP direcionados ao Windows 10 Build 15063 (Atualização para Criadores) e posterior, com exceção dos projetos da C ++ UWP.</span><span class="sxs-lookup"><span data-stu-id="b565f-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="b565f-111">Os projetos do .NET Framework são compatíveis com o PackageReference, mas, no momento, contam com `packages.config` como padrão.</span><span class="sxs-lookup"><span data-stu-id="b565f-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="b565f-112">Para usar PackageReference, [migre](../consume-packages/migrate-packages-config-to-package-reference.md) as dependências de `packages.config` para o arquivo de projeto e remova packages.config.</span><span class="sxs-lookup"><span data-stu-id="b565f-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="b565f-113">Os aplicativos ASP.NET do .NET Framework completo incluem apenas [suporte limitado](https://github.com/NuGet/Home/issues/5877) para PackageReference.</span><span class="sxs-lookup"><span data-stu-id="b565f-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="b565f-114">Não há suporte para tipos de projeto C++ e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b565f-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="b565f-115">Adicionar um PackageReference</span><span class="sxs-lookup"><span data-stu-id="b565f-115">Adding a PackageReference</span></span>

<span data-ttu-id="b565f-116">Adicione uma dependência ao arquivo de projeto usando a seguinte sintaxe:</span><span class="sxs-lookup"><span data-stu-id="b565f-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="b565f-117">Controlar a versão de dependência</span><span class="sxs-lookup"><span data-stu-id="b565f-117">Controlling dependency version</span></span>

<span data-ttu-id="b565f-118">A convenção para especificar a versão de um pacote é a mesma que usar `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="b565f-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="b565f-119">No exemplo acima, 3.6.0 significa qualquer versão que é >=3.6.0 com preferência para a versão mais antiga, conforme descrito em [Controle de versão do pacote](../concepts/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="b565f-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="b565f-120">Usando PackageReference para um projeto sem PackageReferences</span><span class="sxs-lookup"><span data-stu-id="b565f-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="b565f-121">Avançado: se você não tem pacotes instalados em um projeto (não tem PackageReferences no arquivo de projeto nem um arquivo packages.config), mas deseja que o projeto seja restaurado como o estilo PackageReference, você pode definir uma propriedade de projeto RestoreProjectStyle como PackageReference em seu arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="b565f-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="b565f-122">Isso poderá ser útil se você fizer referência a projetos que são do estilo PackageReference (projetos de estilo csproj ou SDK existentes).</span><span class="sxs-lookup"><span data-stu-id="b565f-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="b565f-123">Isso permitirá que os pacotes aos quais esses projetos fazem referência sejam referenciados "transitivamente" pelo seu projeto.</span><span class="sxs-lookup"><span data-stu-id="b565f-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="b565f-124">PackageReference e fontes</span><span class="sxs-lookup"><span data-stu-id="b565f-124">PackageReference and sources</span></span>

<span data-ttu-id="b565f-125">Em projetos PackageReference, as versões de dependência transitivas são resolvidas no momento da restauração.</span><span class="sxs-lookup"><span data-stu-id="b565f-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="b565f-126">Como tal, em projetos PackageReference, todas as fontes precisam estar disponíveis para todas as restaurações.</span><span class="sxs-lookup"><span data-stu-id="b565f-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="b565f-127">Versões flutuantes</span><span class="sxs-lookup"><span data-stu-id="b565f-127">Floating Versions</span></span>

<span data-ttu-id="b565f-128">[Versões flutuante](../concepts/dependency-resolution.md#floating-versions) são compatíveis com `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="b565f-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="b565f-129">Controlar ativos de dependência</span><span class="sxs-lookup"><span data-stu-id="b565f-129">Controlling dependency assets</span></span>

<span data-ttu-id="b565f-130">Você pode estar usando uma dependência puramente como uma estrutura de desenvolvimento e pode não querer expor isso aos projetos que consumirão o pacote.</span><span class="sxs-lookup"><span data-stu-id="b565f-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="b565f-131">Nesse cenário, você pode usar os metadados do `PrivateAssets` para controlar esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="b565f-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="b565f-132">As seguintes marcas de metadados controlam ativos de dependência:</span><span class="sxs-lookup"><span data-stu-id="b565f-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="b565f-133">Marca</span><span class="sxs-lookup"><span data-stu-id="b565f-133">Tag</span></span> | <span data-ttu-id="b565f-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="b565f-134">Description</span></span> | <span data-ttu-id="b565f-135">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="b565f-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b565f-136">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="b565f-136">IncludeAssets</span></span> | <span data-ttu-id="b565f-137">Esses ativos serão consumidos</span><span class="sxs-lookup"><span data-stu-id="b565f-137">These assets will be consumed</span></span> | <span data-ttu-id="b565f-138">all</span><span class="sxs-lookup"><span data-stu-id="b565f-138">all</span></span> |
| <span data-ttu-id="b565f-139">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="b565f-139">ExcludeAssets</span></span> | <span data-ttu-id="b565f-140">Esses ativos não serão consumidos</span><span class="sxs-lookup"><span data-stu-id="b565f-140">These assets will not be consumed</span></span> | <span data-ttu-id="b565f-141">nenhum</span><span class="sxs-lookup"><span data-stu-id="b565f-141">none</span></span> |
| <span data-ttu-id="b565f-142">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="b565f-142">PrivateAssets</span></span> | <span data-ttu-id="b565f-143">Esses ativos serão consumidos, mas não fluem para o projeto pai</span><span class="sxs-lookup"><span data-stu-id="b565f-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="b565f-144">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="b565f-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="b565f-145">Os valores permitidos para essas marcas são os seguintes, com vários valores separados por ponto e vírgula, exceto com `all` e `none`, que devem aparecer sozinhos:</span><span class="sxs-lookup"><span data-stu-id="b565f-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="b565f-146">Valor</span><span class="sxs-lookup"><span data-stu-id="b565f-146">Value</span></span> | <span data-ttu-id="b565f-147">Descrição</span><span class="sxs-lookup"><span data-stu-id="b565f-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="b565f-148">compilar</span><span class="sxs-lookup"><span data-stu-id="b565f-148">compile</span></span> | <span data-ttu-id="b565f-149">Conteúdo da pasta `lib` e controles se seu projeto puder compilar em relação aos assemblies dentro da pasta</span><span class="sxs-lookup"><span data-stu-id="b565f-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="b565f-150">runtime</span><span class="sxs-lookup"><span data-stu-id="b565f-150">runtime</span></span> | <span data-ttu-id="b565f-151">Conteúdo da pasta `lib` e `runtimes` pasta e controles se esses assemblies forem copiados para o diretório de saída de compilação</span><span class="sxs-lookup"><span data-stu-id="b565f-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="b565f-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="b565f-152">contentFiles</span></span> | <span data-ttu-id="b565f-153">O conteúdo da pasta `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="b565f-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="b565f-154">build</span><span class="sxs-lookup"><span data-stu-id="b565f-154">build</span></span> | <span data-ttu-id="b565f-155">`.props` e `.targets` na pasta `build`</span><span class="sxs-lookup"><span data-stu-id="b565f-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="b565f-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="b565f-156">buildMultitargeting</span></span> | <span data-ttu-id="b565f-157">*(4.0)* `.props` e `.targets` na pasta `buildMultitargeting`, para direcionamento entre estruturas</span><span class="sxs-lookup"><span data-stu-id="b565f-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="b565f-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="b565f-158">buildTransitive</span></span> | <span data-ttu-id="b565f-159">*(5.0+)* `.props` e `.targets` na pasta `buildTransitive`, para ativos que fluem transitivamente para qualquer projeto de consumo.</span><span class="sxs-lookup"><span data-stu-id="b565f-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="b565f-160">Confira a página de [recursos](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior).</span><span class="sxs-lookup"><span data-stu-id="b565f-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="b565f-161">analisadores</span><span class="sxs-lookup"><span data-stu-id="b565f-161">analyzers</span></span> | <span data-ttu-id="b565f-162">Analisadores de .NET</span><span class="sxs-lookup"><span data-stu-id="b565f-162">.NET analyzers</span></span> |
| <span data-ttu-id="b565f-163">nativa</span><span class="sxs-lookup"><span data-stu-id="b565f-163">native</span></span> | <span data-ttu-id="b565f-164">O conteúdo da pasta `native`</span><span class="sxs-lookup"><span data-stu-id="b565f-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="b565f-165">nenhum</span><span class="sxs-lookup"><span data-stu-id="b565f-165">none</span></span> | <span data-ttu-id="b565f-166">Nenhuma das opções acima é usada.</span><span class="sxs-lookup"><span data-stu-id="b565f-166">None of the above are used.</span></span> |
| <span data-ttu-id="b565f-167">all</span><span class="sxs-lookup"><span data-stu-id="b565f-167">all</span></span> | <span data-ttu-id="b565f-168">Todas as anteriores (exceto `none`)</span><span class="sxs-lookup"><span data-stu-id="b565f-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="b565f-169">No exemplo a seguir, tudo, exceto os arquivos de conteúdo do pacote, poderia ser consumido pelo projeto e tudo, exceto analisadores e arquivos de conteúdo, fluiria para o projeto pai.</span><span class="sxs-lookup"><span data-stu-id="b565f-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="b565f-170">Observe que, como `build` não está incluído em `PrivateAssets`, destino e objetos *fluirão* para o projeto pai.</span><span class="sxs-lookup"><span data-stu-id="b565f-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="b565f-171">Considere, por exemplo, que a referência acima é usada em um projeto que compila um pacote do NuGet chamado AppLogger.</span><span class="sxs-lookup"><span data-stu-id="b565f-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="b565f-172">O AppLogger pode consumir os destinos e objetos de `Contoso.Utility.UsefulStuff`, bem como projetos que consomem AppLogger.</span><span class="sxs-lookup"><span data-stu-id="b565f-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="b565f-173">Quando `developmentDependency` é definido como `true` em um arquivo `.nuspec`, isso marca um pacote como uma dependência somente de desenvolvimento, o que impede que o pacote seja incluído como uma dependência em outros pacotes.</span><span class="sxs-lookup"><span data-stu-id="b565f-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="b565f-174">Com PackageReference *(NuGet 4.8+)* , esse sinalizador também significa que ele excluirá os recursos em tempo de compilação.</span><span class="sxs-lookup"><span data-stu-id="b565f-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="b565f-175">Para obter mais informações, confira [Suporte do DevelopmentDependency para PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="b565f-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="b565f-176">Adicionar uma condição de PackageReference</span><span class="sxs-lookup"><span data-stu-id="b565f-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="b565f-177">É possível usar uma condição para controlar se um pacote está incluído, em que as condições podem usar qualquer variável MSBuild ou uma variável definida no arquivo de destinos ou objetos.</span><span class="sxs-lookup"><span data-stu-id="b565f-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="b565f-178">No entanto, no momento, somente a variável `TargetFramework` é compatível.</span><span class="sxs-lookup"><span data-stu-id="b565f-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="b565f-179">Por exemplo, digamos que seu destino é `netstandard1.4` e `net452`, mas tem uma dependência que é aplicável somente para `net452`.</span><span class="sxs-lookup"><span data-stu-id="b565f-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="b565f-180">Nesse caso, não é aconselhável ter um projeto `netstandard1.4` que está consumindo seu pacote para adicionar essa dependência desnecessária.</span><span class="sxs-lookup"><span data-stu-id="b565f-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="b565f-181">Para evitar isso, você deve especificar uma condição no `PackageReference` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="b565f-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="b565f-182">Um pacote compilado usando este projeto mostrará que Newtonsoft.Json está incluído como uma dependência somente para um destino `net452`:</span><span class="sxs-lookup"><span data-stu-id="b565f-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![O resultado da aplicação de uma condição em PackageReference com o VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="b565f-184">As condições também podem ser aplicadas no nível de `ItemGroup` e serão aplicadas a todos os elementos `PackageReference` filhos:</span><span class="sxs-lookup"><span data-stu-id="b565f-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="b565f-185">Bloqueio de dependências</span><span class="sxs-lookup"><span data-stu-id="b565f-185">Locking dependencies</span></span>
<span data-ttu-id="b565f-186">*Esse recurso está disponível no NuGet **4.9** ou superior e no Visual Studio 2017 **15.9** ou superior.*</span><span class="sxs-lookup"><span data-stu-id="b565f-186">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="b565f-187">A entrada da restauração do NuGet é um conjunto de Referências de pacote do arquivo de projeto (dependências de nível superior ou diretas), e a saída é um fechamento completo de todas as dependências do pacote, incluindo as dependências transitivas.</span><span class="sxs-lookup"><span data-stu-id="b565f-187">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="b565f-188">Se a lista PackageReference de entrada não tiver sido alterada, o NuGet tenta sempre produzir o mesmo fechamento completo das dependências de pacotes.</span><span class="sxs-lookup"><span data-stu-id="b565f-188">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="b565f-189">No entanto, em alguns cenários, isso não poderá ser feito.</span><span class="sxs-lookup"><span data-stu-id="b565f-189">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="b565f-190">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b565f-190">For example:</span></span>

* <span data-ttu-id="b565f-191">Quando você usa versões flutuantes como `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="b565f-191">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="b565f-192">Embora a intenção aqui seja derivar para a versão mais recente sempre que uma restauração de pacotes ocorrer, há cenários em que os usuários exigem que o grafo seja bloqueado em uma determinada versão mais recente e derive para uma versão posterior, se disponível, mediante um gesto explícito.</span><span class="sxs-lookup"><span data-stu-id="b565f-192">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="b565f-193">Uma versão mais recente do pacote que corresponde aos requisitos de versão do PackageReference é publicada.</span><span class="sxs-lookup"><span data-stu-id="b565f-193">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="b565f-194">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="b565f-194">E.g.</span></span> 

  * <span data-ttu-id="b565f-195">Dia 1: se você tiver especificado `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, mas as versões disponíveis nos repositórios do NuGet forem 4.1.0, 4.2.0 e 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="b565f-195">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="b565f-196">Nesse caso, o NuGet teria que ser resolvido como 4.1.0 (mais próximo da versão mínima)</span><span class="sxs-lookup"><span data-stu-id="b565f-196">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="b565f-197">Dia 2: a versão 4.0.0 é publicada.</span><span class="sxs-lookup"><span data-stu-id="b565f-197">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="b565f-198">O NuGet agora encontrará a correspondência exata e iniciará a resolução como 4.0.0</span><span class="sxs-lookup"><span data-stu-id="b565f-198">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="b565f-199">Uma determinada versão de pacote é removida do repositório.</span><span class="sxs-lookup"><span data-stu-id="b565f-199">A given package version is removed from the repository.</span></span> <span data-ttu-id="b565f-200">Embora nuget.org não permita exclusões de pacotes, nem todos os repositórios de pacotes possuem essas restrições.</span><span class="sxs-lookup"><span data-stu-id="b565f-200">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="b565f-201">Isso faz com que o NuGet encontre a melhor correspondência quando não puder resolver a versão excluída.</span><span class="sxs-lookup"><span data-stu-id="b565f-201">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="b565f-202">Habilitar o arquivo de bloqueio</span><span class="sxs-lookup"><span data-stu-id="b565f-202">Enabling lock file</span></span>
<span data-ttu-id="b565f-203">Para persistir o fechamento completo das dependências de pacotes, você pode optar pelo recurso de bloqueio de arquivos definindo a propriedade `RestorePackagesWithLockFile` do MSBuild para seu projeto:</span><span class="sxs-lookup"><span data-stu-id="b565f-203">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="b565f-204">Se essa propriedade for definida, a restauração do NuGet gerará um arquivo de bloqueio – arquivo `packages.lock.json` no diretório raiz do projeto que lista todas as dependências do pacote.</span><span class="sxs-lookup"><span data-stu-id="b565f-204">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="b565f-205">Se um projeto tiver o arquivo `packages.lock.json` no diretório raiz, o arquivo de bloqueio sempre será usado com a restauração, mesmo que a propriedade `RestorePackagesWithLockFile` não esteja definida.</span><span class="sxs-lookup"><span data-stu-id="b565f-205">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="b565f-206">Portanto, outra maneira de optar por esse recurso é através da criação um arquivo `packages.lock.json` fictício em branco no diretório raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="b565f-206">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="b565f-207">Comportamento `restore` com o arquivo de bloqueio</span><span class="sxs-lookup"><span data-stu-id="b565f-207">`restore` behavior with lock file</span></span>
<span data-ttu-id="b565f-208">Se houver um arquivo de bloqueio para o projeto, o NuGet usará esse arquivo de bloqueio para executar `restore`.</span><span class="sxs-lookup"><span data-stu-id="b565f-208">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="b565f-209">O NuGet faz uma verificação rápida para ver se houve alguma alteração nas dependências do pacote, conforme mencionado no arquivo do projeto (ou nos arquivos dependentes dos projetos) e, se não houver alterações, ele apenas restaurará os pacotes mencionados no arquivo de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="b565f-209">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="b565f-210">Não há reavaliações das dependências do pacote.</span><span class="sxs-lookup"><span data-stu-id="b565f-210">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="b565f-211">Se o NuGet detectar uma alteração nas dependências definidas, conforme mencionado nos arquivos de projeto, ele reavaliará o grafo do pacote e atualizará o arquivo de bloqueio para refletir o novo fechamento do pacote para o projeto.</span><span class="sxs-lookup"><span data-stu-id="b565f-211">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="b565f-212">Para CI/CD e outros cenários, em que você não deseja alterar as dependências de pacote rapidamente, é possível configurar o `lockedmode` como `true`:</span><span class="sxs-lookup"><span data-stu-id="b565f-212">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="b565f-213">Para dotnet.exe, execute:</span><span class="sxs-lookup"><span data-stu-id="b565f-213">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="b565f-214">Para msbuild.exe, execute:</span><span class="sxs-lookup"><span data-stu-id="b565f-214">For msbuild.exe, run:</span></span>
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="b565f-215">Você também pode definir essa propriedade condicional do MSBuild em seu arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="b565f-215">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="b565f-216">Se o modo de bloqueio for `true`, a restauração ocorrerá nos pacotes exatos conforme listado no arquivo de bloqueio ou não ocorrerá se você tiver atualizado as dependências de pacote definidas para o projeto após a criação do arquivo de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="b565f-216">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="b565f-217">Tornar o arquivo de bloqueio parte de seu repositório de origem</span><span class="sxs-lookup"><span data-stu-id="b565f-217">Make lock file part of your source repository</span></span>
<span data-ttu-id="b565f-218">Se você estiver compilando um aplicativo, um executável e o projeto em questão estarão no início da cadeia da dependência, portanto, verifique o arquivo de bloqueio no repositório do código-fonte para que o NuGet possa utilizá-lo durante a restauração.</span><span class="sxs-lookup"><span data-stu-id="b565f-218">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="b565f-219">No entanto, se seu projeto for um projeto de biblioteca que não é enviado ou um projeto de código comum do qual outros projetos dependem, você **não deverá** fazer check-in do arquivo de bloqueio como parte de seu código-fonte.</span><span class="sxs-lookup"><span data-stu-id="b565f-219">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="b565f-220">Não há mal nenhum em manter o arquivo de bloqueio. No entanto, as dependências do pacote bloqueado do projeto de código comum não podem ser usadas, conforme listado no arquivo de bloqueio, durante a restauração/compilação de um projeto que depende desse projeto de código comum.</span><span class="sxs-lookup"><span data-stu-id="b565f-220">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="b565f-221">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b565f-221">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="b565f-222">Se `ProjectA` tiver uma dependência em uma versão `2.0.0` do `PackageX`, além de referências `ProjectB` que dependem da versão `1.0.0` do `PackageX`, o arquivo de bloqueio de `ProjectB` listará uma dependência na versão `1.0.0` do `PackageX`.</span><span class="sxs-lookup"><span data-stu-id="b565f-222">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="b565f-223">No entanto, quando `ProjectA` for criado, seu arquivo de bloqueio conterá uma dependência na versão **`2.0.0`** do `PackageX` e **não** na versão `1.0.0`, conforme listado no arquivo de bloqueio de `ProjectB`.</span><span class="sxs-lookup"><span data-stu-id="b565f-223">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="b565f-224">Portanto, o arquivo de bloqueio de um projeto de código comum tem pouco a dizer sobre os pacotes resolvidos de projetos que dependem dele.</span><span class="sxs-lookup"><span data-stu-id="b565f-224">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="b565f-225">Extensibilidade do arquivo de bloqueio</span><span class="sxs-lookup"><span data-stu-id="b565f-225">Lock file extensibility</span></span>

<span data-ttu-id="b565f-226">Você pode controlar vários comportamentos de restauração com o arquivo de bloqueio conforme descrito abaixo:</span><span class="sxs-lookup"><span data-stu-id="b565f-226">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="b565f-227">Opção</span><span class="sxs-lookup"><span data-stu-id="b565f-227">Option</span></span> | <span data-ttu-id="b565f-228">Opção equivalente do MSBuild</span><span class="sxs-lookup"><span data-stu-id="b565f-228">MSBuild equivalent option</span></span> | <span data-ttu-id="b565f-229">Descrição</span><span class="sxs-lookup"><span data-stu-id="b565f-229">Description</span></span>|
|:---  |:--- |:--- |
| `--use-lock-file` | <span data-ttu-id="b565f-230">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="b565f-230">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="b565f-231">Opta pelo uso de um arquivo de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="b565f-231">Opts into the usage of a lock file.</span></span> | 
| `--locked-mode` | <span data-ttu-id="b565f-232">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="b565f-232">RestoreLockedMode</span></span> | <span data-ttu-id="b565f-233">Habilita o modo de bloqueio para a restauração.</span><span class="sxs-lookup"><span data-stu-id="b565f-233">Enables locked mode for restore.</span></span> <span data-ttu-id="b565f-234">Isso é útil em cenários de CI/CD em que você deseja criar compilações repetíveis.</span><span class="sxs-lookup"><span data-stu-id="b565f-234">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `--force-evaluate` | <span data-ttu-id="b565f-235">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="b565f-235">RestoreForceEvaluate</span></span> | <span data-ttu-id="b565f-236">Esta opção é útil com pacotes que têm a versão flutuante definida no projeto.</span><span class="sxs-lookup"><span data-stu-id="b565f-236">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="b565f-237">Por padrão, a restauração do NuGet não atualizará a versão do pacote automaticamente após cada restauração, a menos que você execute RESTORE com essa opção.</span><span class="sxs-lookup"><span data-stu-id="b565f-237">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="b565f-238">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="b565f-238">NuGetLockFilePath</span></span> | <span data-ttu-id="b565f-239">Define o local de um arquivo de bloqueio personalizado para um projeto.</span><span class="sxs-lookup"><span data-stu-id="b565f-239">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="b565f-240">Por padrão, o NuGet é compatível com `packages.lock.json` no diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="b565f-240">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="b565f-241">Se você tiver vários projetos no mesmo diretório, o NuGet oferecerá suporte ao arquivo de bloqueio `packages.<project_name>.lock.json` específico do projeto</span><span class="sxs-lookup"><span data-stu-id="b565f-241">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
