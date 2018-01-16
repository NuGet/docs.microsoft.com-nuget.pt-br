---
title: PackageReference do NuGet em arquivos de projeto do Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "Veja detalhes sobre o PackageReference de NuGet em arquivos de projeto compatível com o NuGet 4.0 e posterior e o VS2017"
keywords: "Dependências de pacote do NuGet, referências de pacote, arquivos de projeto, PackageReference, packages.config, project.json, VS2017, Visual Studio 2017, NuGet 4"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 275957c94e4a4bb45f359cd48816acf4f286ebad
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="706ef-104">Referências de pacote (PackageReference) em arquivos de projeto</span><span class="sxs-lookup"><span data-stu-id="706ef-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="706ef-105">Pacote de referências, usando o nó `PackageReference`, permitem que você gerencie as dependências do NuGet diretamente nos arquivos de projeto, em vez de precisar de um arquivo `packages.config` ou `project.json` separado.</span><span class="sxs-lookup"><span data-stu-id="706ef-105">Package references, using the `PackageReference` node, allow you to manage NuGet dependencies directly within project files, rather than needing a separate `packages.config` or `project.json` file.</span></span> <span data-ttu-id="706ef-106">Esse método não afeta outros aspectos do NuGet; por exemplo, as configurações nos arquivos `NuGet.Config` (inclusive origens de pacote) ainda são aplicados conforme explicado em [Configurando o comportamento do NuGet](Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="706ef-106">This method doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](Configuring-NuGet-Behavior.md).</span></span>

> [!Important]
> <span data-ttu-id="706ef-107">No momento, as referências de pacote são compatíveis somente com o Visual Studio 2017, para projetos .NET Core, projetos .NET Standard e projetos UWP voltados para o Windows 10 Build 15063 (Atualização para Criadores).</span><span class="sxs-lookup"><span data-stu-id="706ef-107">At present, package references are supported in Visual Studio 2017 only, for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update).</span></span>

<span data-ttu-id="706ef-108">A abordagem `PackageReference` permite que você use condições do MSBuild para escolher as referências de pacote por estrutura de destino, configuração, plataforma ou outros agrupamentos.</span><span class="sxs-lookup"><span data-stu-id="706ef-108">The `PackageReference` approach allows you to use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="706ef-109">Ele também proporciona um controle refinado sobre as dependências e o fluxo de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="706ef-109">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="706ef-110">Em termos de comportamento e [resolução de dependência](Dependency-Resolution.md), é o mesmo que usar `project.json`.</span><span class="sxs-lookup"><span data-stu-id="706ef-110">In terms of behavior and [dependency resolution](Dependency-Resolution.md), it's the same as using `project.json`.</span></span>

<span data-ttu-id="706ef-111">Para obter mais detalhes sobre a integração do MSBuild com referências de pacote em arquivos de projeto, consulte [Empacotamento e restauração do NuGet como destinos do MSBuild](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="706ef-111">For more details on the integration of MSBuild with package references in project files, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="706ef-112">Adicionar um PackageReference</span><span class="sxs-lookup"><span data-stu-id="706ef-112">Adding a PackageReference</span></span>

<span data-ttu-id="706ef-113">Adicione uma dependência ao arquivo de projeto usando a seguinte sintaxe:</span><span class="sxs-lookup"><span data-stu-id="706ef-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />    
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="706ef-114">Controlar a versão de dependência</span><span class="sxs-lookup"><span data-stu-id="706ef-114">Controlling dependency version</span></span>

<span data-ttu-id="706ef-115">A convenção para especificar a versão de um pacote é a mesma que usar `packages.config` ou `project.json`:</span><span class="sxs-lookup"><span data-stu-id="706ef-115">The convention for specifying the version of a package is the same as when using `packages.config` or `project.json`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="706ef-116">No exemplo acima, 3.6.0 significa qualquer versão que é >=3.6.0 com preferência para a versão mais antiga, conforme descrito em [Controle de versão do pacote](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="706ef-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="706ef-117">Versões flutuantes</span><span class="sxs-lookup"><span data-stu-id="706ef-117">Floating Versions</span></span>

<span data-ttu-id="706ef-118">[Versões flutuante](../consume-packages/dependency-resolution.md#floating-versions) são compatíveis com `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="706ef-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="706ef-119">Controlar ativos de dependência</span><span class="sxs-lookup"><span data-stu-id="706ef-119">Controlling dependency assets</span></span>

<span data-ttu-id="706ef-120">Você pode estar usando uma dependência puramente como uma estrutura de desenvolvimento e pode não querer expor isso aos projetos que consumirão o pacote.</span><span class="sxs-lookup"><span data-stu-id="706ef-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="706ef-121">Nesse cenário, você pode usar os metadados do `PrivateAssets` para controlar esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="706ef-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="706ef-122">As seguintes marcas de metadados controlam ativos de dependência:</span><span class="sxs-lookup"><span data-stu-id="706ef-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="706ef-123">Marca</span><span class="sxs-lookup"><span data-stu-id="706ef-123">Tag</span></span> | <span data-ttu-id="706ef-124">Descrição</span><span class="sxs-lookup"><span data-stu-id="706ef-124">Description</span></span> | <span data-ttu-id="706ef-125">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="706ef-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="706ef-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="706ef-126">IncludeAssets</span></span> | <span data-ttu-id="706ef-127">Esses ativos serão consumidos</span><span class="sxs-lookup"><span data-stu-id="706ef-127">These assets will be consumed</span></span> | <span data-ttu-id="706ef-128">all</span><span class="sxs-lookup"><span data-stu-id="706ef-128">all</span></span> |
| <span data-ttu-id="706ef-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="706ef-129">ExcludeAssets</span></span> | <span data-ttu-id="706ef-130">Esses ativos não serão consumidos</span><span class="sxs-lookup"><span data-stu-id="706ef-130">These assets will not be consumed</span></span> | <span data-ttu-id="706ef-131">nenhum</span><span class="sxs-lookup"><span data-stu-id="706ef-131">none</span></span> | 
| <span data-ttu-id="706ef-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="706ef-132">PrivateAssets</span></span> | <span data-ttu-id="706ef-133">Esses ativos serão consumidos, mas não fluem para o projeto pai</span><span class="sxs-lookup"><span data-stu-id="706ef-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="706ef-134">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="706ef-134">contentfiles;analyzers;build</span></span> |


<span data-ttu-id="706ef-135">Os valores permitidos para essas marcas são os seguintes, com vários valores separados por ponto e vírgula, exceto com `all` e `none`, que devem aparecer sozinhos:</span><span class="sxs-lookup"><span data-stu-id="706ef-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="706ef-136">Valor</span><span class="sxs-lookup"><span data-stu-id="706ef-136">Value</span></span> | <span data-ttu-id="706ef-137">Descrição</span><span class="sxs-lookup"><span data-stu-id="706ef-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="706ef-138">compilar</span><span class="sxs-lookup"><span data-stu-id="706ef-138">compile</span></span> | <span data-ttu-id="706ef-139">O conteúdo da pasta `lib`</span><span class="sxs-lookup"><span data-stu-id="706ef-139">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="706ef-140">tempo de execução</span><span class="sxs-lookup"><span data-stu-id="706ef-140">runtime</span></span> | <span data-ttu-id="706ef-141">O conteúdo da pasta `runtime`</span><span class="sxs-lookup"><span data-stu-id="706ef-141">Contents of the `runtime` folder</span></span> |
| <span data-ttu-id="706ef-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="706ef-142">contentFiles</span></span> | <span data-ttu-id="706ef-143">O conteúdo da pasta `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="706ef-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="706ef-144">build</span><span class="sxs-lookup"><span data-stu-id="706ef-144">build</span></span> | <span data-ttu-id="706ef-145">Objetos e propriedades na pasta `build`</span><span class="sxs-lookup"><span data-stu-id="706ef-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="706ef-146">analisadores</span><span class="sxs-lookup"><span data-stu-id="706ef-146">analyzers</span></span> | <span data-ttu-id="706ef-147">Analisadores de .NET</span><span class="sxs-lookup"><span data-stu-id="706ef-147">.NET analyzers</span></span> |
| <span data-ttu-id="706ef-148">nativa</span><span class="sxs-lookup"><span data-stu-id="706ef-148">native</span></span> | <span data-ttu-id="706ef-149">O conteúdo da pasta `native`</span><span class="sxs-lookup"><span data-stu-id="706ef-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="706ef-150">nenhum</span><span class="sxs-lookup"><span data-stu-id="706ef-150">none</span></span> | <span data-ttu-id="706ef-151">Nenhuma das opções acima é usada.</span><span class="sxs-lookup"><span data-stu-id="706ef-151">None of the above are used.</span></span> |
| <span data-ttu-id="706ef-152">all</span><span class="sxs-lookup"><span data-stu-id="706ef-152">all</span></span> | <span data-ttu-id="706ef-153">Todas as anteriores (exceto `none`)</span><span class="sxs-lookup"><span data-stu-id="706ef-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="706ef-154">No exemplo a seguir, tudo, exceto os arquivos de conteúdo do pacote, poderia ser consumido pelo projeto e tudo, exceto analisadores e arquivos de conteúdo, fluiria para o projeto pai.</span><span class="sxs-lookup"><span data-stu-id="706ef-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="706ef-155">Observe que, como `build` não está incluído em `PrivateAssets`, destino e objetos *fluirão* para o projeto pai.</span><span class="sxs-lookup"><span data-stu-id="706ef-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="706ef-156">Considere, por exemplo, que a referência acima é usada em um projeto que compila um pacote do NuGet chamado AppLogger.</span><span class="sxs-lookup"><span data-stu-id="706ef-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="706ef-157">O AppLogger pode consumir os destinos e objetos de `Contoso.Utility.UsefulStuff`, bem como projetos que consomem AppLogger.</span><span class="sxs-lookup"><span data-stu-id="706ef-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="706ef-158">Adicionar uma condição de PackageReference</span><span class="sxs-lookup"><span data-stu-id="706ef-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="706ef-159">É possível usar uma condição para controlar se um pacote está incluído, em que as condições podem usar qualquer variável MSBuild ou uma variável definida no arquivo de destinos ou objetos.</span><span class="sxs-lookup"><span data-stu-id="706ef-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="706ef-160">No entanto, no momento, somente a variável `TargetFramework` é compatível.</span><span class="sxs-lookup"><span data-stu-id="706ef-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="706ef-161">Por exemplo, digamos que seu destino é `netstandard1.4` e `net452`, mas tem uma dependência que é aplicável somente para `net452`.</span><span class="sxs-lookup"><span data-stu-id="706ef-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="706ef-162">Nesse caso, não é aconselhável ter um projeto `netstandard1.4` que está consumindo seu pacote para adicionar essa dependência desnecessária.</span><span class="sxs-lookup"><span data-stu-id="706ef-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="706ef-163">Para evitar isso, você deve especificar uma condição no `PackageReference` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="706ef-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="706ef-164">Um pacote compilado usando este projeto mostrará que Newtonsoft.json está incluído como uma dependência somente para um destino `net452`:</span><span class="sxs-lookup"><span data-stu-id="706ef-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![O resultado da aplicação de uma condição em PackageReference com o VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="706ef-166">As condições também podem ser aplicadas no nível de `ItemGroup` e serão aplicadas a todos os elementos `PackageReference` filhos:</span><span class="sxs-lookup"><span data-stu-id="706ef-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
