---
title: Formato PackageReference do NuGet (referências de pacote em arquivos de projeto)
description: Veja detalhes sobre o PackageReference de NuGet em arquivos de projeto compatível com o NuGet 4.0 e posterior e o VS2017 e .Net Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 16a14a72f8bb2e5d5a56f6c3c277f0988869273d
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426691"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="a2f28-103">Referências de pacote (PackageReference) em arquivos de projeto</span><span class="sxs-lookup"><span data-stu-id="a2f28-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="a2f28-104">As referências de pacote, usando o nó `PackageReference`, gerenciam as dependências do NuGet diretamente nos arquivos de projeto (em vez de precisar de um arquivo `packages.config` separado).</span><span class="sxs-lookup"><span data-stu-id="a2f28-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="a2f28-105">O uso de PackageReference, como ele é chamado, não afeta outros aspectos do NuGet; por exemplo, as configurações nos arquivos `NuGet.config` (incluindo as origens do pacote) ainda são aplicadas, conforme explicado em [Configurações comuns do NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="a2f28-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="a2f28-106">Com o PackageReference, você também pode usar condições do MSBuild para escolher as referências de pacote por estrutura de destino, por configuração, por plataforma ou por outros agrupamentos.</span><span class="sxs-lookup"><span data-stu-id="a2f28-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="a2f28-107">Ele também proporciona um controle refinado sobre as dependências e o fluxo de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="a2f28-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="a2f28-108">(Para obter mais detalhes, veja [Empacotamento e restauração do NuGet como destinos do MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="a2f28-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="a2f28-109">Suporte do tipo de projeto</span><span class="sxs-lookup"><span data-stu-id="a2f28-109">Project type support</span></span>

<span data-ttu-id="a2f28-110">Por padrão, o PackageReference é usado para projetos do .NET Core, para projetos do .NET Standard e para projetos da UWP direcionados ao Windows 10 Build 15063 (Atualização para Criadores) e posterior, com exceção dos projetos da C ++ UWP.</span><span class="sxs-lookup"><span data-stu-id="a2f28-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="a2f28-111">Os projetos do .NET Framework são compatíveis com o PackageReference, mas, no momento, contam com `packages.config` como padrão.</span><span class="sxs-lookup"><span data-stu-id="a2f28-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="a2f28-112">Para usar PackageReference, [migre](../reference/migrate-packages-config-to-package-reference.md) as dependências de `packages.config` para o arquivo de projeto e remova packages.config.</span><span class="sxs-lookup"><span data-stu-id="a2f28-112">To use PackageReference, [migrate](../reference/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="a2f28-113">Os aplicativos ASP.NET do .NET Framework completo incluem apenas [suporte limitado](https://github.com/NuGet/Home/issues/5877) para PackageReference.</span><span class="sxs-lookup"><span data-stu-id="a2f28-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="a2f28-114">Não há suporte para tipos de projeto C++ e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="a2f28-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="a2f28-115">Adicionar um PackageReference</span><span class="sxs-lookup"><span data-stu-id="a2f28-115">Adding a PackageReference</span></span>

<span data-ttu-id="a2f28-116">Adicione uma dependência ao arquivo de projeto usando a seguinte sintaxe:</span><span class="sxs-lookup"><span data-stu-id="a2f28-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="a2f28-117">Controlar a versão de dependência</span><span class="sxs-lookup"><span data-stu-id="a2f28-117">Controlling dependency version</span></span>

<span data-ttu-id="a2f28-118">A convenção para especificar a versão de um pacote é a mesma que usar `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="a2f28-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="a2f28-119">No exemplo acima, 3.6.0 significa qualquer versão que é >=3.6.0 com preferência para a versão mais antiga, conforme descrito em [Controle de versão do pacote](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="a2f28-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="a2f28-120">Usando PackageReference para um projeto sem PackageReferences</span><span class="sxs-lookup"><span data-stu-id="a2f28-120">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="a2f28-121">Avançado: Se você não tem pacotes instalados em um projeto (não tem PackageReferences no arquivo de projeto nem um arquivo packages.config), mas deseja que o projeto seja restaurado como o estilo PackageReference, você pode definir uma propriedade de projeto RestoreProjectStyle como PackageReference em seu arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="a2f28-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="a2f28-122">Isso poderá ser útil se você fizer referência a projetos que são do estilo PackageReference (projetos de estilo csproj ou SDK existentes).</span><span class="sxs-lookup"><span data-stu-id="a2f28-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="a2f28-123">Isso permitirá que os pacotes aos quais esses projetos fazem referência sejam referenciados "transitivamente" pelo seu projeto.</span><span class="sxs-lookup"><span data-stu-id="a2f28-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="a2f28-124">Versões flutuantes</span><span class="sxs-lookup"><span data-stu-id="a2f28-124">Floating Versions</span></span>

<span data-ttu-id="a2f28-125">[Versões flutuante](../consume-packages/dependency-resolution.md#floating-versions) são compatíveis com `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="a2f28-125">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="a2f28-126">Controlar ativos de dependência</span><span class="sxs-lookup"><span data-stu-id="a2f28-126">Controlling dependency assets</span></span>

<span data-ttu-id="a2f28-127">Você pode estar usando uma dependência puramente como uma estrutura de desenvolvimento e pode não querer expor isso aos projetos que consumirão o pacote.</span><span class="sxs-lookup"><span data-stu-id="a2f28-127">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="a2f28-128">Nesse cenário, você pode usar os metadados do `PrivateAssets` para controlar esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="a2f28-128">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="a2f28-129">As seguintes marcas de metadados controlam ativos de dependência:</span><span class="sxs-lookup"><span data-stu-id="a2f28-129">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="a2f28-130">Marca</span><span class="sxs-lookup"><span data-stu-id="a2f28-130">Tag</span></span> | <span data-ttu-id="a2f28-131">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="a2f28-131">Description</span></span> | <span data-ttu-id="a2f28-132">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="a2f28-132">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a2f28-133">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="a2f28-133">IncludeAssets</span></span> | <span data-ttu-id="a2f28-134">Esses ativos serão consumidos</span><span class="sxs-lookup"><span data-stu-id="a2f28-134">These assets will be consumed</span></span> | <span data-ttu-id="a2f28-135">all</span><span class="sxs-lookup"><span data-stu-id="a2f28-135">all</span></span> |
| <span data-ttu-id="a2f28-136">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="a2f28-136">ExcludeAssets</span></span> | <span data-ttu-id="a2f28-137">Esses ativos não serão consumidos</span><span class="sxs-lookup"><span data-stu-id="a2f28-137">These assets will not be consumed</span></span> | <span data-ttu-id="a2f28-138">nenhum</span><span class="sxs-lookup"><span data-stu-id="a2f28-138">none</span></span> |
| <span data-ttu-id="a2f28-139">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="a2f28-139">PrivateAssets</span></span> | <span data-ttu-id="a2f28-140">Esses ativos serão consumidos, mas não fluem para o projeto pai</span><span class="sxs-lookup"><span data-stu-id="a2f28-140">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="a2f28-141">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="a2f28-141">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="a2f28-142">Os valores permitidos para essas marcas são os seguintes, com vários valores separados por ponto e vírgula, exceto com `all` e `none`, que devem aparecer sozinhos:</span><span class="sxs-lookup"><span data-stu-id="a2f28-142">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="a2f28-143">Valor</span><span class="sxs-lookup"><span data-stu-id="a2f28-143">Value</span></span> | <span data-ttu-id="a2f28-144">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="a2f28-144">Description</span></span> |
| --- | ---
| <span data-ttu-id="a2f28-145">compilar</span><span class="sxs-lookup"><span data-stu-id="a2f28-145">compile</span></span> | <span data-ttu-id="a2f28-146">Conteúdo da pasta `lib` e controles se seu projeto puder compilar em relação aos assemblies dentro da pasta</span><span class="sxs-lookup"><span data-stu-id="a2f28-146">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="a2f28-147">tempo de execução</span><span class="sxs-lookup"><span data-stu-id="a2f28-147">runtime</span></span> | <span data-ttu-id="a2f28-148">Conteúdo da pasta `lib` e `runtimes` pasta e controles se esses assemblies forem copiados para o diretório de saída de compilação</span><span class="sxs-lookup"><span data-stu-id="a2f28-148">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="a2f28-149">contentFiles</span><span class="sxs-lookup"><span data-stu-id="a2f28-149">contentFiles</span></span> | <span data-ttu-id="a2f28-150">O conteúdo da pasta `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="a2f28-150">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="a2f28-151">build</span><span class="sxs-lookup"><span data-stu-id="a2f28-151">build</span></span> | <span data-ttu-id="a2f28-152">Objetos e propriedades na pasta `build`</span><span class="sxs-lookup"><span data-stu-id="a2f28-152">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="a2f28-153">analisadores</span><span class="sxs-lookup"><span data-stu-id="a2f28-153">analyzers</span></span> | <span data-ttu-id="a2f28-154">Analisadores de .NET</span><span class="sxs-lookup"><span data-stu-id="a2f28-154">.NET analyzers</span></span> |
| <span data-ttu-id="a2f28-155">nativa</span><span class="sxs-lookup"><span data-stu-id="a2f28-155">native</span></span> | <span data-ttu-id="a2f28-156">O conteúdo da pasta `native`</span><span class="sxs-lookup"><span data-stu-id="a2f28-156">Contents of the `native` folder</span></span> |
| <span data-ttu-id="a2f28-157">nenhum</span><span class="sxs-lookup"><span data-stu-id="a2f28-157">none</span></span> | <span data-ttu-id="a2f28-158">Nenhuma das opções acima é usada.</span><span class="sxs-lookup"><span data-stu-id="a2f28-158">None of the above are used.</span></span> |
| <span data-ttu-id="a2f28-159">all</span><span class="sxs-lookup"><span data-stu-id="a2f28-159">all</span></span> | <span data-ttu-id="a2f28-160">Todas as anteriores (exceto `none`)</span><span class="sxs-lookup"><span data-stu-id="a2f28-160">All of the above (except `none`)</span></span> |

<span data-ttu-id="a2f28-161">No exemplo a seguir, tudo, exceto os arquivos de conteúdo do pacote, poderia ser consumido pelo projeto e tudo, exceto analisadores e arquivos de conteúdo, fluiria para o projeto pai.</span><span class="sxs-lookup"><span data-stu-id="a2f28-161">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="a2f28-162">Observe que, como `build` não está incluído em `PrivateAssets`, destino e objetos *fluirão* para o projeto pai.</span><span class="sxs-lookup"><span data-stu-id="a2f28-162">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="a2f28-163">Considere, por exemplo, que a referência acima é usada em um projeto que compila um pacote do NuGet chamado AppLogger.</span><span class="sxs-lookup"><span data-stu-id="a2f28-163">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="a2f28-164">O AppLogger pode consumir os destinos e objetos de `Contoso.Utility.UsefulStuff`, bem como projetos que consomem AppLogger.</span><span class="sxs-lookup"><span data-stu-id="a2f28-164">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="a2f28-165">Adicionar uma condição de PackageReference</span><span class="sxs-lookup"><span data-stu-id="a2f28-165">Adding a PackageReference condition</span></span>

<span data-ttu-id="a2f28-166">É possível usar uma condição para controlar se um pacote está incluído, em que as condições podem usar qualquer variável MSBuild ou uma variável definida no arquivo de destinos ou objetos.</span><span class="sxs-lookup"><span data-stu-id="a2f28-166">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="a2f28-167">No entanto, no momento, somente a variável `TargetFramework` é compatível.</span><span class="sxs-lookup"><span data-stu-id="a2f28-167">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="a2f28-168">Por exemplo, digamos que seu destino é `netstandard1.4` e `net452`, mas tem uma dependência que é aplicável somente para `net452`.</span><span class="sxs-lookup"><span data-stu-id="a2f28-168">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="a2f28-169">Nesse caso, não é aconselhável ter um projeto `netstandard1.4` que está consumindo seu pacote para adicionar essa dependência desnecessária.</span><span class="sxs-lookup"><span data-stu-id="a2f28-169">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="a2f28-170">Para evitar isso, você deve especificar uma condição no `PackageReference` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a2f28-170">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="a2f28-171">Um pacote compilado usando este projeto mostrará que Newtonsoft.Json está incluído como uma dependência somente para um destino `net452`:</span><span class="sxs-lookup"><span data-stu-id="a2f28-171">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![O resultado da aplicação de uma condição em PackageReference com o VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="a2f28-173">As condições também podem ser aplicadas no nível de `ItemGroup` e serão aplicadas a todos os elementos `PackageReference` filhos:</span><span class="sxs-lookup"><span data-stu-id="a2f28-173">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="a2f28-174">Bloqueio de dependências</span><span class="sxs-lookup"><span data-stu-id="a2f28-174">Locking dependencies</span></span>
<span data-ttu-id="a2f28-175">*Esse recurso está disponível no NuGet **4.9** ou superior e no Visual Studio 2017 **15.9** ou superior.*</span><span class="sxs-lookup"><span data-stu-id="a2f28-175">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="a2f28-176">A entrada da restauração do NuGet é um conjunto de Referências de pacote do arquivo de projeto (dependências de nível superior ou diretas), e a saída é um fechamento completo de todas as dependências do pacote, incluindo as dependências transitivas.</span><span class="sxs-lookup"><span data-stu-id="a2f28-176">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="a2f28-177">Se a lista PackageReference de entrada não tiver sido alterada, o NuGet tenta sempre produzir o mesmo fechamento completo das dependências de pacotes.</span><span class="sxs-lookup"><span data-stu-id="a2f28-177">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="a2f28-178">No entanto, em alguns cenários, isso não poderá ser feito.</span><span class="sxs-lookup"><span data-stu-id="a2f28-178">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="a2f28-179">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a2f28-179">For example:</span></span>

* <span data-ttu-id="a2f28-180">Quando você usa versões flutuantes como `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="a2f28-180">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="a2f28-181">Embora a intenção aqui seja derivar para a versão mais recente sempre que uma restauração de pacotes ocorrer, há cenários em que os usuários exigem que o grafo seja bloqueado em uma determinada versão mais recente e derive para uma versão posterior, se disponível, mediante um gesto explícito.</span><span class="sxs-lookup"><span data-stu-id="a2f28-181">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="a2f28-182">Uma versão mais recente do pacote que corresponde aos requisitos de versão do PackageReference é publicada.</span><span class="sxs-lookup"><span data-stu-id="a2f28-182">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="a2f28-183">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="a2f28-183">E.g.</span></span> 

  * <span data-ttu-id="a2f28-184">Dia 1: se você tiver especificado `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`, mas as versões disponíveis nos repositórios do NuGet forem 4.1.0, 4.2.0 e 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="a2f28-184">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="a2f28-185">Nesse caso, o NuGet teria que ser resolvido como 4.1.0 (mais próximo da versão mínima)</span><span class="sxs-lookup"><span data-stu-id="a2f28-185">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="a2f28-186">Dia 2: A versão 4.0.0 é publicada.</span><span class="sxs-lookup"><span data-stu-id="a2f28-186">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="a2f28-187">O NuGet agora encontrará a correspondência exata e iniciará a resolução como 4.0.0</span><span class="sxs-lookup"><span data-stu-id="a2f28-187">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="a2f28-188">Uma determinada versão de pacote é removida do repositório.</span><span class="sxs-lookup"><span data-stu-id="a2f28-188">A given package version is removed from the repository.</span></span> <span data-ttu-id="a2f28-189">Embora nuget.org não permita exclusões de pacotes, nem todos os repositórios de pacotes possuem essas restrições.</span><span class="sxs-lookup"><span data-stu-id="a2f28-189">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="a2f28-190">Isso faz com que o NuGet encontre a melhor correspondência quando não puder resolver a versão excluída.</span><span class="sxs-lookup"><span data-stu-id="a2f28-190">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="a2f28-191">Habilitar o arquivo de bloqueio</span><span class="sxs-lookup"><span data-stu-id="a2f28-191">Enabling lock file</span></span>
<span data-ttu-id="a2f28-192">Para persistir o fechamento completo das dependências de pacotes, você pode optar pelo recurso de bloqueio de arquivos definindo a propriedade `RestorePackagesWithLockFile` do MSBuild para seu projeto:</span><span class="sxs-lookup"><span data-stu-id="a2f28-192">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="a2f28-193">Se essa propriedade for definida, a restauração do NuGet gerará um arquivo de bloqueio – arquivo `packages.lock.json` no diretório raiz do projeto que lista todas as dependências do pacote.</span><span class="sxs-lookup"><span data-stu-id="a2f28-193">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="a2f28-194">Se um projeto tiver o arquivo `packages.lock.json` no diretório raiz, o arquivo de bloqueio sempre será usado com a restauração, mesmo que a propriedade `RestorePackagesWithLockFile` não esteja definida.</span><span class="sxs-lookup"><span data-stu-id="a2f28-194">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="a2f28-195">Portanto, outra maneira de optar por esse recurso é através da criação um arquivo `packages.lock.json` fictício em branco no diretório raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="a2f28-195">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="a2f28-196">Comportamento `restore` com o arquivo de bloqueio</span><span class="sxs-lookup"><span data-stu-id="a2f28-196">`restore` behavior with lock file</span></span>
<span data-ttu-id="a2f28-197">Se houver um arquivo de bloqueio para o projeto, o NuGet usará esse arquivo de bloqueio para executar `restore`.</span><span class="sxs-lookup"><span data-stu-id="a2f28-197">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="a2f28-198">O NuGet faz uma verificação rápida para ver se houve alguma alteração nas dependências do pacote, conforme mencionado no arquivo do projeto (ou nos arquivos dependentes dos projetos) e, se não houver alterações, ele apenas restaurará os pacotes mencionados no arquivo de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="a2f28-198">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="a2f28-199">Não há reavaliações das dependências do pacote.</span><span class="sxs-lookup"><span data-stu-id="a2f28-199">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="a2f28-200">Se o NuGet detectar uma alteração nas dependências definidas, conforme mencionado nos arquivos de projeto, ele reavaliará o grafo do pacote e atualizará o arquivo de bloqueio para refletir o novo fechamento do pacote para o projeto.</span><span class="sxs-lookup"><span data-stu-id="a2f28-200">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="a2f28-201">Para CI/CD e outros cenários, em que você não deseja alterar as dependências de pacote rapidamente, é possível configurar o `lockedmode` como `true`:</span><span class="sxs-lookup"><span data-stu-id="a2f28-201">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="a2f28-202">Para dotnet.exe, execute:</span><span class="sxs-lookup"><span data-stu-id="a2f28-202">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="a2f28-203">Para msbuild.exe, execute:</span><span class="sxs-lookup"><span data-stu-id="a2f28-203">For msbuild.exe, run:</span></span>
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="a2f28-204">Você também pode definir essa propriedade condicional do MSBuild em seu arquivo de projeto:</span><span class="sxs-lookup"><span data-stu-id="a2f28-204">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="a2f28-205">Se o modo de bloqueio for `true`, a restauração ocorrerá nos pacotes exatos conforme listado no arquivo de bloqueio ou não ocorrerá se você tiver atualizado as dependências de pacote definidas para o projeto após a criação do arquivo de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="a2f28-205">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="a2f28-206">Tornar o arquivo de bloqueio parte de seu repositório de origem</span><span class="sxs-lookup"><span data-stu-id="a2f28-206">Make lock file part of your source repository</span></span>
<span data-ttu-id="a2f28-207">Se você estiver compilando um aplicativo, um executável e o projeto em questão estarão no início da cadeia da dependência, portanto, verifique o arquivo de bloqueio no repositório do código-fonte para que o NuGet possa utilizá-lo durante a restauração.</span><span class="sxs-lookup"><span data-stu-id="a2f28-207">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="a2f28-208">No entanto, se seu projeto for um projeto de biblioteca que não é enviado ou um projeto de código comum do qual outros projetos dependem, você **não deverá** fazer check-in do arquivo de bloqueio como parte de seu código-fonte.</span><span class="sxs-lookup"><span data-stu-id="a2f28-208">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="a2f28-209">Não há mal nenhum em manter o arquivo de bloqueio. No entanto, as dependências do pacote bloqueado do projeto de código comum não podem ser usadas, conforme listado no arquivo de bloqueio, durante a restauração/compilação de um projeto que depende desse projeto de código comum.</span><span class="sxs-lookup"><span data-stu-id="a2f28-209">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="a2f28-210">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a2f28-210">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="a2f28-211">Se `ProjectA` tiver uma dependência em uma versão `2.0.0` do `PackageX`, além de referências `ProjectB` que dependem da versão `1.0.0` do `PackageX`, o arquivo de bloqueio de `ProjectB` listará uma dependência na versão `1.0.0` do `PackageX`.</span><span class="sxs-lookup"><span data-stu-id="a2f28-211">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="a2f28-212">No entanto, quando `ProjectA` for criado, seu arquivo de bloqueio conterá uma dependência na versão **`2.0.0`** do `PackageX` e **não** na versão `1.0.0`, conforme listado no arquivo de bloqueio de `ProjectB`.</span><span class="sxs-lookup"><span data-stu-id="a2f28-212">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="a2f28-213">Portanto, o arquivo de bloqueio de um projeto de código comum tem pouco a dizer sobre os pacotes resolvidos de projetos que dependem dele.</span><span class="sxs-lookup"><span data-stu-id="a2f28-213">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="a2f28-214">Extensibilidade do arquivo de bloqueio</span><span class="sxs-lookup"><span data-stu-id="a2f28-214">Lock file extensibility</span></span>
<span data-ttu-id="a2f28-215">Você pode controlar vários comportamentos de restauração com o arquivo de bloqueio conforme descrito abaixo:</span><span class="sxs-lookup"><span data-stu-id="a2f28-215">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="a2f28-216">Opção</span><span class="sxs-lookup"><span data-stu-id="a2f28-216">Option</span></span> | <span data-ttu-id="a2f28-217">Opção equivalente do MSBuild</span><span class="sxs-lookup"><span data-stu-id="a2f28-217">MSBuild equivalent option</span></span> | 
|:---  |:--- |
| `--use-lock-file` | <span data-ttu-id="a2f28-218">Uso do arquivo de bloqueio de um projeto pelas inicializações.</span><span class="sxs-lookup"><span data-stu-id="a2f28-218">Bootstraps use of lock file for a project.</span></span> <span data-ttu-id="a2f28-219">Como alternativa, você pode definir a propriedade `RestorePackagesWithLockFile` no arquivo de projeto</span><span class="sxs-lookup"><span data-stu-id="a2f28-219">You can alternatively set `RestorePackagesWithLockFile` property in the project file</span></span> | 
| `--locked-mode` | <span data-ttu-id="a2f28-220">Habilita o modo de bloqueio para a restauração.</span><span class="sxs-lookup"><span data-stu-id="a2f28-220">Enables locked mode for restore.</span></span> <span data-ttu-id="a2f28-221">Isso é útil em cenários de CI/CD em que você gostaria de obter os builds repetidos.</span><span class="sxs-lookup"><span data-stu-id="a2f28-221">This is useful in CI/CD scenarios where you would like to get the repeatable builds.</span></span> <span data-ttu-id="a2f28-222">Isso também pode ser feito através da definição da propriedade `RestoreLockedMode` do MSBuild como `true`</span><span class="sxs-lookup"><span data-stu-id="a2f28-222">This can be also by setting the `RestoreLockedMode` MSBuild property to `true`</span></span> |  
| `--force-evaluate` | <span data-ttu-id="a2f28-223">Esta opção é útil com pacotes que têm a versão flutuante definida no projeto.</span><span class="sxs-lookup"><span data-stu-id="a2f28-223">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="a2f28-224">Por padrão, a restauração do NuGet não atualizará automaticamente a versão do pacote em cada restauração, a menos que você execute a restauração com a opção `--force-evaluate`.</span><span class="sxs-lookup"><span data-stu-id="a2f28-224">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with `--force-evaluate` option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="a2f28-225">Define o local de um arquivo de bloqueio personalizado para um projeto.</span><span class="sxs-lookup"><span data-stu-id="a2f28-225">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="a2f28-226">Isso também pode ser feito através da definição da propriedade `NuGetLockFilePath` do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="a2f28-226">This can be also achieved by setting the MSBuild property `NuGetLockFilePath`.</span></span> <span data-ttu-id="a2f28-227">Por padrão, o NuGet é compatível com `packages.lock.json` no diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="a2f28-227">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="a2f28-228">Se você tiver vários projetos no mesmo diretório, o NuGet oferecerá suporte ao arquivo de bloqueio `packages.<project_name>.lock.json` específico do projeto</span><span class="sxs-lookup"><span data-stu-id="a2f28-228">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
