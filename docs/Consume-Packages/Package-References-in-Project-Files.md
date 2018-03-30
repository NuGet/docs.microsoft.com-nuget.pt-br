---
title: Formato PackageReference do NuGet (referências de pacote em arquivos de projeto) | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Veja detalhes sobre o PackageReference de NuGet em arquivos de projeto compatível com o NuGet 4.0 e posterior e o VS2017 e .Net Core 2.0
keywords: Dependências de pacote NuGet, referências de pacote, arquivos de projeto, PackageReference, packages.config, VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 99caf371ca1bd85e6af4e879741e3e2caab6e860
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="120fc-104">Referências de pacote (PackageReference) em arquivos de projeto</span><span class="sxs-lookup"><span data-stu-id="120fc-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="120fc-105">As referências de pacote, usando o nó `PackageReference`, gerenciam as dependências do NuGet diretamente nos arquivos de projeto (em vez de precisar de um arquivo `packages.config` separado).</span><span class="sxs-lookup"><span data-stu-id="120fc-105">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="120fc-106">Usar o PackageReference, como ele é chamado, não afeta os outros aspectos do NuGet; por exemplo, as configurações nos arquivos `NuGet.Config` (inclusive nas origens de pacote) ainda são aplicadas, conforme explicado em [Configurando o comportamento do NuGet](configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="120fc-106">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="120fc-107">Com o PackageReference, você também pode usar condições do MSBuild para escolher as referências de pacote por estrutura de destino, por configuração, por plataforma ou por outros agrupamentos.</span><span class="sxs-lookup"><span data-stu-id="120fc-107">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="120fc-108">Ele também proporciona um controle refinado sobre as dependências e o fluxo de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="120fc-108">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="120fc-109">(Para obter mais detalhes, veja [Empacotamento e restauração do NuGet como destinos do MSBuild](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="120fc-109">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="120fc-110">Por padrão, o PackageReference é usado para projetos do .NET Core, para projetos do .NET Standard e para projetos da UWP direcionados ao Windows 10 Build 15063 (Atualização para Criadores) e posterior, com exceção dos projetos da C ++ UWP.</span><span class="sxs-lookup"><span data-stu-id="120fc-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="120fc-111">Os projetos com estrutura completa do .NET são compatíveis com o PackageReference, mas no momento contam com `packages.config` como padrão.</span><span class="sxs-lookup"><span data-stu-id="120fc-111">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="120fc-112">Para usar PackageReference, migre as dependências de `packages.config` para o arquivo de projeto e remova packages.config.</span><span class="sxs-lookup"><span data-stu-id="120fc-112">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="120fc-113">Adicionar um PackageReference</span><span class="sxs-lookup"><span data-stu-id="120fc-113">Adding a PackageReference</span></span>

<span data-ttu-id="120fc-114">Adicione uma dependência ao arquivo de projeto usando a seguinte sintaxe:</span><span class="sxs-lookup"><span data-stu-id="120fc-114">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="120fc-115">Controlar a versão de dependência</span><span class="sxs-lookup"><span data-stu-id="120fc-115">Controlling dependency version</span></span>

<span data-ttu-id="120fc-116">A convenção para especificar a versão de um pacote é a mesma que usar `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="120fc-116">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="120fc-117">No exemplo acima, 3.6.0 significa qualquer versão que é >=3.6.0 com preferência para a versão mais antiga, conforme descrito em [Controle de versão do pacote](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="120fc-117">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="120fc-118">Versões flutuantes</span><span class="sxs-lookup"><span data-stu-id="120fc-118">Floating Versions</span></span>

<span data-ttu-id="120fc-119">[Versões flutuante](../consume-packages/dependency-resolution.md#floating-versions) são compatíveis com `PackageReference`:</span><span class="sxs-lookup"><span data-stu-id="120fc-119">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="120fc-120">Controlar ativos de dependência</span><span class="sxs-lookup"><span data-stu-id="120fc-120">Controlling dependency assets</span></span>

<span data-ttu-id="120fc-121">Você pode estar usando uma dependência puramente como uma estrutura de desenvolvimento e pode não querer expor isso aos projetos que consumirão o pacote.</span><span class="sxs-lookup"><span data-stu-id="120fc-121">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="120fc-122">Nesse cenário, você pode usar os metadados do `PrivateAssets` para controlar esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="120fc-122">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="120fc-123">As seguintes marcas de metadados controlam ativos de dependência:</span><span class="sxs-lookup"><span data-stu-id="120fc-123">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="120fc-124">Marca</span><span class="sxs-lookup"><span data-stu-id="120fc-124">Tag</span></span> | <span data-ttu-id="120fc-125">Descrição</span><span class="sxs-lookup"><span data-stu-id="120fc-125">Description</span></span> | <span data-ttu-id="120fc-126">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="120fc-126">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="120fc-127">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="120fc-127">IncludeAssets</span></span> | <span data-ttu-id="120fc-128">Esses ativos serão consumidos</span><span class="sxs-lookup"><span data-stu-id="120fc-128">These assets will be consumed</span></span> | <span data-ttu-id="120fc-129">all</span><span class="sxs-lookup"><span data-stu-id="120fc-129">all</span></span> |
| <span data-ttu-id="120fc-130">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="120fc-130">ExcludeAssets</span></span> | <span data-ttu-id="120fc-131">Esses ativos não serão consumidos</span><span class="sxs-lookup"><span data-stu-id="120fc-131">These assets will not be consumed</span></span> | <span data-ttu-id="120fc-132">nenhum</span><span class="sxs-lookup"><span data-stu-id="120fc-132">none</span></span> |
| <span data-ttu-id="120fc-133">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="120fc-133">PrivateAssets</span></span> | <span data-ttu-id="120fc-134">Esses ativos serão consumidos, mas não fluem para o projeto pai</span><span class="sxs-lookup"><span data-stu-id="120fc-134">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="120fc-135">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="120fc-135">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="120fc-136">Os valores permitidos para essas marcas são os seguintes, com vários valores separados por ponto e vírgula, exceto com `all` e `none`, que devem aparecer sozinhos:</span><span class="sxs-lookup"><span data-stu-id="120fc-136">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="120fc-137">Valor</span><span class="sxs-lookup"><span data-stu-id="120fc-137">Value</span></span> | <span data-ttu-id="120fc-138">Descrição</span><span class="sxs-lookup"><span data-stu-id="120fc-138">Description</span></span> |
| --- | ---
| <span data-ttu-id="120fc-139">compilar</span><span class="sxs-lookup"><span data-stu-id="120fc-139">compile</span></span> | <span data-ttu-id="120fc-140">O conteúdo da pasta `lib`</span><span class="sxs-lookup"><span data-stu-id="120fc-140">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="120fc-141">tempo de execução</span><span class="sxs-lookup"><span data-stu-id="120fc-141">runtime</span></span> | <span data-ttu-id="120fc-142">O conteúdo da pasta `runtimes`</span><span class="sxs-lookup"><span data-stu-id="120fc-142">Contents of the `runtimes` folder</span></span> |
| <span data-ttu-id="120fc-143">contentFiles</span><span class="sxs-lookup"><span data-stu-id="120fc-143">contentFiles</span></span> | <span data-ttu-id="120fc-144">O conteúdo da pasta `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="120fc-144">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="120fc-145">build</span><span class="sxs-lookup"><span data-stu-id="120fc-145">build</span></span> | <span data-ttu-id="120fc-146">Objetos e propriedades na pasta `build`</span><span class="sxs-lookup"><span data-stu-id="120fc-146">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="120fc-147">analisadores</span><span class="sxs-lookup"><span data-stu-id="120fc-147">analyzers</span></span> | <span data-ttu-id="120fc-148">Analisadores de .NET</span><span class="sxs-lookup"><span data-stu-id="120fc-148">.NET analyzers</span></span> |
| <span data-ttu-id="120fc-149">nativa</span><span class="sxs-lookup"><span data-stu-id="120fc-149">native</span></span> | <span data-ttu-id="120fc-150">O conteúdo da pasta `native`</span><span class="sxs-lookup"><span data-stu-id="120fc-150">Contents of the `native` folder</span></span> |
| <span data-ttu-id="120fc-151">nenhum</span><span class="sxs-lookup"><span data-stu-id="120fc-151">none</span></span> | <span data-ttu-id="120fc-152">Nenhuma das opções acima é usada.</span><span class="sxs-lookup"><span data-stu-id="120fc-152">None of the above are used.</span></span> |
| <span data-ttu-id="120fc-153">all</span><span class="sxs-lookup"><span data-stu-id="120fc-153">all</span></span> | <span data-ttu-id="120fc-154">Todas as anteriores (exceto `none`)</span><span class="sxs-lookup"><span data-stu-id="120fc-154">All of the above (except `none`)</span></span> |

<span data-ttu-id="120fc-155">No exemplo a seguir, tudo, exceto os arquivos de conteúdo do pacote, poderia ser consumido pelo projeto e tudo, exceto analisadores e arquivos de conteúdo, fluiria para o projeto pai.</span><span class="sxs-lookup"><span data-stu-id="120fc-155">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="120fc-156">Observe que, como `build` não está incluído em `PrivateAssets`, destino e objetos *fluirão* para o projeto pai.</span><span class="sxs-lookup"><span data-stu-id="120fc-156">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="120fc-157">Considere, por exemplo, que a referência acima é usada em um projeto que compila um pacote do NuGet chamado AppLogger.</span><span class="sxs-lookup"><span data-stu-id="120fc-157">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="120fc-158">O AppLogger pode consumir os destinos e objetos de `Contoso.Utility.UsefulStuff`, bem como projetos que consomem AppLogger.</span><span class="sxs-lookup"><span data-stu-id="120fc-158">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="120fc-159">Adicionar uma condição de PackageReference</span><span class="sxs-lookup"><span data-stu-id="120fc-159">Adding a PackageReference condition</span></span>

<span data-ttu-id="120fc-160">É possível usar uma condição para controlar se um pacote está incluído, em que as condições podem usar qualquer variável MSBuild ou uma variável definida no arquivo de destinos ou objetos.</span><span class="sxs-lookup"><span data-stu-id="120fc-160">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="120fc-161">No entanto, no momento, somente a variável `TargetFramework` é compatível.</span><span class="sxs-lookup"><span data-stu-id="120fc-161">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="120fc-162">Por exemplo, digamos que seu destino é `netstandard1.4` e `net452`, mas tem uma dependência que é aplicável somente para `net452`.</span><span class="sxs-lookup"><span data-stu-id="120fc-162">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="120fc-163">Nesse caso, não é aconselhável ter um projeto `netstandard1.4` que está consumindo seu pacote para adicionar essa dependência desnecessária.</span><span class="sxs-lookup"><span data-stu-id="120fc-163">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="120fc-164">Para evitar isso, você deve especificar uma condição no `PackageReference` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="120fc-164">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="120fc-165">Um pacote compilado usando este projeto mostrará que Newtonsoft.json está incluído como uma dependência somente para um destino `net452`:</span><span class="sxs-lookup"><span data-stu-id="120fc-165">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![O resultado da aplicação de uma condição em PackageReference com o VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="120fc-167">As condições também podem ser aplicadas no nível de `ItemGroup` e serão aplicadas a todos os elementos `PackageReference` filhos:</span><span class="sxs-lookup"><span data-stu-id="120fc-167">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
