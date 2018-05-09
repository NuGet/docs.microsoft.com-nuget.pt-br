---
title: Formato PackageReference do NuGet (referências de pacote em arquivos de projeto)
description: Veja detalhes sobre o PackageReference de NuGet em arquivos de projeto compatível com o NuGet 4.0 e posterior e o VS2017 e .Net Core 2.0
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 8f277a8af7f988d6fdcfa75c43a10b3792c2ae22
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="39b58-103">Referências de pacote (PackageReference) em arquivos de projeto</span><span class="sxs-lookup"><span data-stu-id="39b58-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="39b58-104">As referências de pacote, usando o nó `PackageReference`, gerenciam as dependências do NuGet diretamente nos arquivos de projeto (em vez de precisar de um arquivo `packages.config` separado).</span><span class="sxs-lookup"><span data-stu-id="39b58-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="39b58-105">Usar o PackageReference, como ele é chamado, não afeta os outros aspectos do NuGet; por exemplo, as configurações nos arquivos `NuGet.Config` (inclusive nas origens de pacote) ainda são aplicadas, conforme explicado em [Configurando o comportamento do NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="39b58-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="39b58-106">Com o PackageReference, você também pode usar condições do MSBuild para escolher as referências de pacote por estrutura de destino, por configuração, por plataforma ou por outros agrupamentos.</span><span class="sxs-lookup"><span data-stu-id="39b58-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="39b58-107">Ele também proporciona um controle refinado sobre as dependências e o fluxo de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="39b58-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="39b58-108">(Para obter mais detalhes, veja [Empacotamento e restauração do NuGet como destinos do MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="39b58-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="39b58-109">Por padrão, o PackageReference é usado para projetos do .NET Core, para projetos do .NET Standard e para projetos da UWP direcionados ao Windows 10 Build 15063 (Atualização para Criadores) e posterior, com exceção dos projetos da C ++ UWP.</span><span class="sxs-lookup"><span data-stu-id="39b58-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="39b58-110">Os projetos com estrutura completa do .NET são compatíveis com o PackageReference, mas no momento contam com `packages.config` como padrão.</span><span class="sxs-lookup"><span data-stu-id="39b58-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="39b58-111">Para usar PackageReference, migre as dependências de `packages.config` para o arquivo de projeto e remova packages.config.</span><span class="sxs-lookup"><span data-stu-id="39b58-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="39b58-112">Adicionar um PackageReference</span><span class="sxs-lookup"><span data-stu-id="39b58-112">Adding a PackageReference</span></span>

<span data-ttu-id="39b58-113">Adicione uma dependência ao arquivo de projeto usando a seguinte sintaxe:</span><span class="sxs-lookup"><span data-stu-id="39b58-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="39b58-114">Controlar a versão de dependência</span><span class="sxs-lookup"><span data-stu-id="39b58-114">Controlling dependency version</span></span>

<span data-ttu-id="39b58-115">A convenção para especificar a versão de um pacote é a mesma que usar `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="39b58-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="39b58-116">No exemplo acima, 3.6.0 significa qualquer versão que é >=3.6.0 com preferência para a versão mais antiga, conforme descrito em [Controle de versão do pacote](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="39b58-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="39b58-117">Versões flutuantes</span><span class="sxs-lookup"><span data-stu-id="39b58-117">Floating Versions</span></span>

<span data-ttu-id="39b58-118">[Versões flutuante](../consume-packages/dependency-resolution.md#floating-versions) são compatíveis com `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="39b58-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="39b58-119">Controlar ativos de dependência</span><span class="sxs-lookup"><span data-stu-id="39b58-119">Controlling dependency assets</span></span>

<span data-ttu-id="39b58-120">Você pode estar usando uma dependência puramente como uma estrutura de desenvolvimento e pode não querer expor isso aos projetos que consumirão o pacote.</span><span class="sxs-lookup"><span data-stu-id="39b58-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="39b58-121">Nesse cenário, você pode usar os metadados do `PrivateAssets` para controlar esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="39b58-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="39b58-122">As seguintes marcas de metadados controlam ativos de dependência:</span><span class="sxs-lookup"><span data-stu-id="39b58-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="39b58-123">Marca</span><span class="sxs-lookup"><span data-stu-id="39b58-123">Tag</span></span> | <span data-ttu-id="39b58-124">Descrição</span><span class="sxs-lookup"><span data-stu-id="39b58-124">Description</span></span> | <span data-ttu-id="39b58-125">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="39b58-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39b58-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="39b58-126">IncludeAssets</span></span> | <span data-ttu-id="39b58-127">Esses ativos serão consumidos</span><span class="sxs-lookup"><span data-stu-id="39b58-127">These assets will be consumed</span></span> | <span data-ttu-id="39b58-128">all</span><span class="sxs-lookup"><span data-stu-id="39b58-128">all</span></span> |
| <span data-ttu-id="39b58-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="39b58-129">ExcludeAssets</span></span> | <span data-ttu-id="39b58-130">Esses ativos não serão consumidos</span><span class="sxs-lookup"><span data-stu-id="39b58-130">These assets will not be consumed</span></span> | <span data-ttu-id="39b58-131">nenhum</span><span class="sxs-lookup"><span data-stu-id="39b58-131">none</span></span> |
| <span data-ttu-id="39b58-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="39b58-132">PrivateAssets</span></span> | <span data-ttu-id="39b58-133">Esses ativos serão consumidos, mas não fluem para o projeto pai</span><span class="sxs-lookup"><span data-stu-id="39b58-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="39b58-134">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="39b58-134">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="39b58-135">Os valores permitidos para essas marcas são os seguintes, com vários valores separados por ponto e vírgula, exceto com `all` e `none`, que devem aparecer sozinhos:</span><span class="sxs-lookup"><span data-stu-id="39b58-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="39b58-136">Valor</span><span class="sxs-lookup"><span data-stu-id="39b58-136">Value</span></span> | <span data-ttu-id="39b58-137">Descrição</span><span class="sxs-lookup"><span data-stu-id="39b58-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="39b58-138">compilar</span><span class="sxs-lookup"><span data-stu-id="39b58-138">compile</span></span> | <span data-ttu-id="39b58-139">Conteúdo da pasta `lib` e controles se seu projeto puder compilar em relação aos assemblies dentro da pasta</span><span class="sxs-lookup"><span data-stu-id="39b58-139">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="39b58-140">tempo de execução</span><span class="sxs-lookup"><span data-stu-id="39b58-140">runtime</span></span> | <span data-ttu-id="39b58-141">Conteúdo da pasta `lib` e `runtimes` pasta e controles se esses assemblies forem copiados para o diretório de saída de compilação</span><span class="sxs-lookup"><span data-stu-id="39b58-141">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="39b58-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="39b58-142">contentFiles</span></span> | <span data-ttu-id="39b58-143">O conteúdo da pasta `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="39b58-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="39b58-144">build</span><span class="sxs-lookup"><span data-stu-id="39b58-144">build</span></span> | <span data-ttu-id="39b58-145">Objetos e propriedades na pasta `build`</span><span class="sxs-lookup"><span data-stu-id="39b58-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="39b58-146">analisadores</span><span class="sxs-lookup"><span data-stu-id="39b58-146">analyzers</span></span> | <span data-ttu-id="39b58-147">Analisadores de .NET</span><span class="sxs-lookup"><span data-stu-id="39b58-147">.NET analyzers</span></span> |
| <span data-ttu-id="39b58-148">nativa</span><span class="sxs-lookup"><span data-stu-id="39b58-148">native</span></span> | <span data-ttu-id="39b58-149">O conteúdo da pasta `native`</span><span class="sxs-lookup"><span data-stu-id="39b58-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="39b58-150">nenhum</span><span class="sxs-lookup"><span data-stu-id="39b58-150">none</span></span> | <span data-ttu-id="39b58-151">Nenhuma das opções acima é usada.</span><span class="sxs-lookup"><span data-stu-id="39b58-151">None of the above are used.</span></span> |
| <span data-ttu-id="39b58-152">all</span><span class="sxs-lookup"><span data-stu-id="39b58-152">all</span></span> | <span data-ttu-id="39b58-153">Todas as anteriores (exceto `none`)</span><span class="sxs-lookup"><span data-stu-id="39b58-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="39b58-154">No exemplo a seguir, tudo, exceto os arquivos de conteúdo do pacote, poderia ser consumido pelo projeto e tudo, exceto analisadores e arquivos de conteúdo, fluiria para o projeto pai.</span><span class="sxs-lookup"><span data-stu-id="39b58-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="39b58-155">Observe que, como `build` não está incluído em `PrivateAssets`, destino e objetos *fluirão* para o projeto pai.</span><span class="sxs-lookup"><span data-stu-id="39b58-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="39b58-156">Considere, por exemplo, que a referência acima é usada em um projeto que compila um pacote do NuGet chamado AppLogger.</span><span class="sxs-lookup"><span data-stu-id="39b58-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="39b58-157">O AppLogger pode consumir os destinos e objetos de `Contoso.Utility.UsefulStuff`, bem como projetos que consomem AppLogger.</span><span class="sxs-lookup"><span data-stu-id="39b58-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="39b58-158">Adicionar uma condição de PackageReference</span><span class="sxs-lookup"><span data-stu-id="39b58-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="39b58-159">É possível usar uma condição para controlar se um pacote está incluído, em que as condições podem usar qualquer variável MSBuild ou uma variável definida no arquivo de destinos ou objetos.</span><span class="sxs-lookup"><span data-stu-id="39b58-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="39b58-160">No entanto, no momento, somente a variável `TargetFramework` é compatível.</span><span class="sxs-lookup"><span data-stu-id="39b58-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="39b58-161">Por exemplo, digamos que seu destino é `netstandard1.4` e `net452`, mas tem uma dependência que é aplicável somente para `net452`.</span><span class="sxs-lookup"><span data-stu-id="39b58-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="39b58-162">Nesse caso, não é aconselhável ter um projeto `netstandard1.4` que está consumindo seu pacote para adicionar essa dependência desnecessária.</span><span class="sxs-lookup"><span data-stu-id="39b58-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="39b58-163">Para evitar isso, você deve especificar uma condição no `PackageReference` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="39b58-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="39b58-164">Um pacote compilado usando este projeto mostrará que Newtonsoft.json está incluído como uma dependência somente para um destino `net452`:</span><span class="sxs-lookup"><span data-stu-id="39b58-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![O resultado da aplicação de uma condição em PackageReference com o VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="39b58-166">As condições também podem ser aplicadas no nível de `ItemGroup` e serão aplicadas a todos os elementos `PackageReference` filhos:</span><span class="sxs-lookup"><span data-stu-id="39b58-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
