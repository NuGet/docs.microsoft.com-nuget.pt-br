---
title: Referência de arquivo. nuspec para NuGet
description: O arquivo .nuspec contém metadados de pacote usados ao compilar um pacote e para fornecer informações para os consumidores do pacote.
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: ed865aad6f72752adcf3e3921287a20b961c4a8a
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901805"
---
# <a name="nuspec-reference"></a><span data-ttu-id="aaa4b-103">Referência do .nuspec</span><span class="sxs-lookup"><span data-stu-id="aaa4b-103">.nuspec reference</span></span>

<span data-ttu-id="aaa4b-104">Um arquivo `.nuspec` é um manifesto XML que contém metadados do pacote.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="aaa4b-105">Esse manifesto é usado para compilar o pacote e fornecer informações aos consumidores.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="aaa4b-106">O manifesto sempre é incluído em um pacote.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="aaa4b-107">Neste tópico:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-107">In this topic:</span></span>

- [<span data-ttu-id="aaa4b-108">Formato e esquema geral</span><span class="sxs-lookup"><span data-stu-id="aaa4b-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="aaa4b-109">[Tokens de substituição](#replacement-tokens) (quando usados com um projeto do Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="aaa4b-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="aaa4b-110">Dependências</span><span class="sxs-lookup"><span data-stu-id="aaa4b-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="aaa4b-111">Referências de assembly explícitas</span><span class="sxs-lookup"><span data-stu-id="aaa4b-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="aaa4b-112">Referências de assembly de estrutura</span><span class="sxs-lookup"><span data-stu-id="aaa4b-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="aaa4b-113">Incluindo arquivos do assembly</span><span class="sxs-lookup"><span data-stu-id="aaa4b-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="aaa4b-114">Incluindo arquivos de conteúdo</span><span class="sxs-lookup"><span data-stu-id="aaa4b-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="aaa4b-115">Arquivos nuspec de exemplo</span><span class="sxs-lookup"><span data-stu-id="aaa4b-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="aaa4b-116">Compatibilidade de tipo de projeto</span><span class="sxs-lookup"><span data-stu-id="aaa4b-116">Project type compatibility</span></span>

- <span data-ttu-id="aaa4b-117">Use o `.nuspec` com `nuget.exe pack` para projetos de estilo não-SDK que usam o `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="aaa4b-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="aaa4b-118">Um `.nuspec` arquivo não é necessário para criar pacotes para [projetos de estilo SDK](../resources/check-project-format.md) (normalmente .net Core e .net Standard projetos que usam o [atributo SDK](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="aaa4b-119">(Observe que um `.nuspec` é gerado quando você cria o pacote.)</span><span class="sxs-lookup"><span data-stu-id="aaa4b-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="aaa4b-120">Se você estiver criando um pacote usando `dotnet.exe pack` ou `msbuild pack target` , recomendamos que [inclua todas as propriedades](../reference/msbuild-targets.md#pack-target) que normalmente estão no `.nuspec` arquivo no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="aaa4b-121">No entanto, você pode optar por [usar um `.nuspec` arquivo para empacotar usando o `dotnet.exe` ou `msbuild pack target` o ](../reference/msbuild-targets.md#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec-file).</span></span>

- <span data-ttu-id="aaa4b-122">Para projetos migrados do `packages.config` para o [PackageReference](../consume-packages/package-references-in-project-files.md), um `.nuspec` arquivo não é necessário para criar o pacote.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="aaa4b-123">Em vez disso, use o [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="aaa4b-124">Formato e esquema geral</span><span class="sxs-lookup"><span data-stu-id="aaa4b-124">General form and schema</span></span>

<span data-ttu-id="aaa4b-125">O arquivo de esquema `nuspec.xsd` atual pode ser encontrado no [repositório GitHub do NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="aaa4b-126">Dentro desse esquema, um arquivo `.nuspec` tem o seguinte formato geral:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

<span data-ttu-id="aaa4b-127">Para obter uma representação visual do esquema, abra o arquivo de esquema no Visual Studio no modo de Design e clique no link **Gerenciador de Esquema XML**.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="aaa4b-128">Como alternativa, abra o arquivo como código, clique com o botão direito do mouse no editor e selecione **Mostrar Gerenciador de Esquema XML**.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="aaa4b-129">De qualquer forma, você receberá uma exibição como a mostrada abaixo (quando expandido):</span><span class="sxs-lookup"><span data-stu-id="aaa4b-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Gerenciador de Esquema do Visual Studio com o nuspec.xsd aberto](media/SchemaExplorer.png)

<span data-ttu-id="aaa4b-131">Todos os nomes de elementos XML no arquivo. nuspec diferenciam maiúsculas de minúsculas, como é o caso de XML em geral.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-131">All XML element names in the .nuspec file are case-sensitive, as is the case for XML in general.</span></span> <span data-ttu-id="aaa4b-132">Por exemplo, o uso do elemento de metadados `<description>` está correto e `<Description>` não está correto.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-132">For example, using the metadata element `<description>` is correct and `<Description>` is not correct.</span></span> <span data-ttu-id="aaa4b-133">A capitalização correta para cada nome de elemento está documentada abaixo.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-133">The proper casing for each element name is documented below.</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="aaa4b-134">Elementos de metadados necessários</span><span class="sxs-lookup"><span data-stu-id="aaa4b-134">Required metadata elements</span></span>

<span data-ttu-id="aaa4b-135">Embora os elementos a seguir sejam os requisitos mínimos para um pacote, considere adicionar os [elementos de metadados opcionais](#optional-metadata-elements) para melhorar a experiência geral que os desenvolvedores têm com o pacote.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-135">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="aaa4b-136">Esses elementos precisam aparecer dentro de um elemento `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-136">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="aaa4b-137">id</span><span class="sxs-lookup"><span data-stu-id="aaa4b-137">id</span></span> 
<span data-ttu-id="aaa4b-138">O identificador de pacote que não diferencia maiúsculas de minúsculas, o qual deve ser exclusivo no nuget.org ou em qualquer galeria na qual o pacote reside.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-138">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="aaa4b-139">IDs podem não conter espaços nem caracteres que não sejam válidos para uma URL e geralmente seguem as regras de namespace do .NET.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-139">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="aaa4b-140">Consulte [Escolhendo um identificador de pacote exclusivo](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) para ver diretrizes.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-140">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>

<span data-ttu-id="aaa4b-141">Ao carregar um pacote no nuget.org, o `id` campo é limitado a 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-141">When uploading a package to nuget.org, the `id` field is limited to 128 characters.</span></span>

#### <a name="version"></a><span data-ttu-id="aaa4b-142">version</span><span class="sxs-lookup"><span data-stu-id="aaa4b-142">version</span></span>
<span data-ttu-id="aaa4b-143">A versão do pacote, seguindo o padrão *principal.secundária.patch*.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-143">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="aaa4b-144">Os números de versão podem incluir um sufixo de pré-lançamento, conforme descrito em [Controle de versões de pré-lançamento](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-144">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 

<span data-ttu-id="aaa4b-145">Ao carregar um pacote no nuget.org, o `version` campo é limitado a 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-145">When uploading a package to nuget.org, the `version` field is limited to 64 characters.</span></span>

#### <a name="description"></a><span data-ttu-id="aaa4b-146">descrição</span><span class="sxs-lookup"><span data-stu-id="aaa4b-146">description</span></span>
<span data-ttu-id="aaa4b-147">Uma descrição do pacote para exibição da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-147">A description of the package for UI display.</span></span>

<span data-ttu-id="aaa4b-148">Ao carregar um pacote no nuget.org, o `description` campo é limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-148">When uploading a package to nuget.org, the `description` field is limited to 4000 characters.</span></span>

#### <a name="authors"></a><span data-ttu-id="aaa4b-149">authors</span><span class="sxs-lookup"><span data-stu-id="aaa4b-149">authors</span></span>
<span data-ttu-id="aaa4b-150">Uma lista separada por vírgulas de autores de pacotes, que correspondem aos nomes de perfil em nuget.org. Eles são exibidos na galeria do NuGet em nuget.org e são usados para fazer referência cruzada de pacotes pelos mesmos autores.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

<span data-ttu-id="aaa4b-151">Ao carregar um pacote no nuget.org, o `authors` campo é limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-151">When uploading a package to nuget.org, the `authors` field is limited to 4000 characters.</span></span>

### <a name="optional-metadata-elements"></a><span data-ttu-id="aaa4b-152">Elementos de metadados opcionais</span><span class="sxs-lookup"><span data-stu-id="aaa4b-152">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="aaa4b-153">owners</span><span class="sxs-lookup"><span data-stu-id="aaa4b-153">owners</span></span>
> [!Important]
> <span data-ttu-id="aaa4b-154">os proprietários são preteridos.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-154">owners is deprecated.</span></span> <span data-ttu-id="aaa4b-155">Em vez disso, use os autores.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-155">Use authors instead.</span></span>

<span data-ttu-id="aaa4b-156">Uma lista separada por vírgulas dos criadores de pacote usando nomes de perfil em nuget.org. Isso geralmente é a mesma lista que em `authors` e é ignorado ao carregar o pacote para o NuGet.org. Consulte [Gerenciando proprietários de pacotes em NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-156">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="aaa4b-157">projectUrl</span><span class="sxs-lookup"><span data-stu-id="aaa4b-157">projectUrl</span></span>
<span data-ttu-id="aaa4b-158">Uma URL para a home page do pacote, geralmente mostrada em exibições de interface do usuário, bem como em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-158">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

<span data-ttu-id="aaa4b-159">Ao carregar um pacote no nuget.org, o `projectUrl` campo é limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-159">When uploading a package to nuget.org, the `projectUrl` field is limited to 4000 characters.</span></span>

#### <a name="licenseurl"></a><span data-ttu-id="aaa4b-160">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="aaa4b-160">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="aaa4b-161">licenseUrl foi preterido.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-161">licenseUrl is deprecated.</span></span> <span data-ttu-id="aaa4b-162">Use a licença em vez disso.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-162">Use license instead.</span></span>

<span data-ttu-id="aaa4b-163">Uma URL para a licença do pacote, geralmente mostrada em interfaces do tipo nuget.org.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-163">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

<span data-ttu-id="aaa4b-164">Ao carregar um pacote no nuget.org, o `licenseUrl` campo é limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-164">When uploading a package to nuget.org, the `licenseUrl` field is limited to 4000 characters.</span></span>

#### <a name="license"></a><span data-ttu-id="aaa4b-165">license</span><span class="sxs-lookup"><span data-stu-id="aaa4b-165">license</span></span>

<span data-ttu-id="aaa4b-166">*Com suporte com **NuGet 4.9.0** e superior*</span><span class="sxs-lookup"><span data-stu-id="aaa4b-166">*Supported with **NuGet 4.9.0** and above*</span></span>

<span data-ttu-id="aaa4b-167">Uma expressão de licença SPDX ou um caminho para um arquivo de licença dentro do pacote, geralmente mostrado em interfaces de grupo como nuget.org. Se você estiver licenciando o pacote em uma licença comum, como MIT ou BSD-2-cláusula, use o [identificador de licença SPDX](https://spdx.org/licenses/)associado.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-167">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="aaa4b-168">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-168">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="aaa4b-169">O NuGet.org só aceita expressões de licença que são aprovadas pela iniciativa de software livre ou pela base de softwares gratuita.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-169">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="aaa4b-170">Se o pacote for licenciado sob várias licenças comuns, você poderá especificar uma licença composta usando a [sintaxe de expressão SPDX versão 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-170">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="aaa4b-171">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-171">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="aaa4b-172">Se você usar uma licença personalizada que não é suportada por expressões de licença, poderá empacotar um `.txt` `.md` arquivo ou com o texto da licença.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-172">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="aaa4b-173">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-173">For example:</span></span>

```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

<span data-ttu-id="aaa4b-174">Para o equivalente do MSBuild, dê uma olhada no [empacotamento de uma expressão de licença ou um arquivo de licença](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-174">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="aaa4b-175">A sintaxe exata das expressões de licença do NuGet é descrita abaixo em [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-175">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>

```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a><span data-ttu-id="aaa4b-176">iconUrl</span><span class="sxs-lookup"><span data-stu-id="aaa4b-176">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="aaa4b-177">iconUrl foi preterido.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-177">iconUrl is deprecated.</span></span> <span data-ttu-id="aaa4b-178">Use o ícone em vez disso.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-178">Use icon instead.</span></span>

<span data-ttu-id="aaa4b-179">Uma URL para uma imagem 128x128 com tela de fundo de transparência a ser usada como o ícone para o pacote na exibição da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-179">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="aaa4b-180">Verifique se esse elemento contém a *URL direta da imagem* e não a URL de uma página da Web que contém a imagem.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-180">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="aaa4b-181">Por exemplo, para usar uma imagem do GitHub, use a URL do arquivo bruto como <em> https://github.com/ \<username\> / \<repository\> /RAW/ \<branch\> / \<logo.png\> </em>.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-181">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

<span data-ttu-id="aaa4b-182">Ao carregar um pacote no nuget.org, o `iconUrl` campo é limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-182">When uploading a package to nuget.org, the `iconUrl` field is limited to 4000 characters.</span></span>

#### <a name="icon"></a><span data-ttu-id="aaa4b-183">ícone</span><span class="sxs-lookup"><span data-stu-id="aaa4b-183">icon</span></span>

<span data-ttu-id="aaa4b-184">*Com suporte com **NuGet 5.3.0** e superior*</span><span class="sxs-lookup"><span data-stu-id="aaa4b-184">*Supported with **NuGet 5.3.0** and above*</span></span>

<span data-ttu-id="aaa4b-185">É um caminho para um arquivo de imagem dentro do pacote, geralmente mostrado em UIs como nuget.org como o ícone do pacote.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-185">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="aaa4b-186">O tamanho do arquivo de imagem é limitado a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-186">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="aaa4b-187">Os formatos de arquivo com suporte incluem JPEG e PNG.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-187">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="aaa4b-188">Recomendamos uma resolução de imagem de 128x128.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-188">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="aaa4b-189">Por exemplo, você adicionaria o seguinte ao seu nuspec ao criar um pacote usando nuget.exe:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-189">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

```xml
<package>
  <metadata>
    ...
    <icon>images\icon.png</icon>
    ...
  </metadata>
  <files>
    ...
    <file src="..\icon.png" target="images\" />
    ...
  </files>
</package>
```

[<span data-ttu-id="aaa4b-190">Ícone de pacote exemplo de nuspec.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-190">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/main/PackageIconNuspecExample)

<span data-ttu-id="aaa4b-191">Para o equivalente do MSBuild, dê uma olhada no [empacotamento de um arquivo de imagem de ícone](msbuild-targets.md#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-191">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="aaa4b-192">Você pode especificar o `icon` e o `iconUrl` para manter a compatibilidade com versões anteriores com fontes que não dão suporte ao `icon` .</span><span class="sxs-lookup"><span data-stu-id="aaa4b-192">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="aaa4b-193">O Visual Studio dará suporte a `icon` pacotes provenientes de uma fonte baseada em pasta em uma versão futura.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-193">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="readme"></a><span data-ttu-id="aaa4b-194">leiame</span><span class="sxs-lookup"><span data-stu-id="aaa4b-194">readme</span></span>

<span data-ttu-id="aaa4b-195">*Com suporte com o **NuGet 5.10.0 Preview 2** e posterior*</span><span class="sxs-lookup"><span data-stu-id="aaa4b-195">*Supported with **NuGet 5.10.0 preview 2** and above*</span></span>

<span data-ttu-id="aaa4b-196">Ao empacotar um arquivo Leiame, você precisa usar o `readme` elemento para especificar o caminho do pacote, em relação à raiz do pacote.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-196">When packing a readme file, you need to use the `readme` element to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="aaa4b-197">Além disso, você precisa certificar-se de que o arquivo está incluído no pacote.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-197">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="aaa4b-198">Os formatos de arquivo com suporte incluem apenas redução (*. MD*).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-198">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="aaa4b-199">Por exemplo, você adicionaria o seguinte ao seu nuspec para empacotar um arquivo Leiame com seu projeto:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-199">For example, you would add the following to your nuspec in order to pack a readme file with your project:</span></span>

```xml
<package>
  <metadata>
    ...
    <readme>docs\readme.md</readme>
    ...
  </metadata>
  <files>
    ...
    <file src="..\readme.md" target="docs\" />
    ...
  </files>
</package>
```

<span data-ttu-id="aaa4b-200">Para o equivalente do MSBuild, dê uma olhada no [empacotamento de um arquivo Leiame](msbuild-targets.md#packagereadmefile).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-200">For the MSBuild equivalent, take a look at [Packing a readme file](msbuild-targets.md#packagereadmefile).</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="aaa4b-201">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="aaa4b-201">requireLicenseAcceptance</span></span>
<span data-ttu-id="aaa4b-202">Um valor booliano que especifica se o cliente precisa solicitar que o consumidor aceite a licença do pacote antes de instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-202">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="aaa4b-203">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="aaa4b-203">developmentDependency</span></span>
<span data-ttu-id="aaa4b-204">*(2.8 ou superior)* Um valor booliano que especifica se o pacote está marcado como uma dependência somente de desenvolvimento, que impede que o pacote seja incluído como uma dependência em outros pacotes.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-204">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="aaa4b-205">Com PackageReference (NuGet 4.8+), esse sinalizador também significa que ele excluirá os recursos em tempo de compilação.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-205">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="aaa4b-206">Consulte [suporte do DevelopmentDependency para PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="aaa4b-206">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="aaa4b-207">resumo</span><span class="sxs-lookup"><span data-stu-id="aaa4b-207">summary</span></span>
> [!Important]
> <span data-ttu-id="aaa4b-208">`summary` está sendo preterido.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-208">`summary` is being deprecated.</span></span> <span data-ttu-id="aaa4b-209">Use `description` em vez disso.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-209">Use `description` instead.</span></span>

<span data-ttu-id="aaa4b-210">Uma breve descrição do pacote para exibição de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-210">A short description of the package for UI display.</span></span> <span data-ttu-id="aaa4b-211">Se omitido, uma versão truncada do `description` é usada.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-211">If omitted, a truncated version of `description` is used.</span></span>

<span data-ttu-id="aaa4b-212">Ao carregar um pacote no nuget.org, o `summary` campo é limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-212">When uploading a package to nuget.org, the `summary` field is limited to 4000 characters.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="aaa4b-213">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="aaa4b-213">releaseNotes</span></span>
<span data-ttu-id="aaa4b-214">*(1.5 ou superior)* Uma descrição das alterações feitas nesta versão do pacote, frequentemente usado na interface do usuário como a guia **Atualizações** do Gerenciador de Pacotes do Visual Studio em vez da descrição do pacote.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-214">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

<span data-ttu-id="aaa4b-215">Ao carregar um pacote no nuget.org, o `releaseNotes` campo é limitado a 35.000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-215">When uploading a package to nuget.org, the `releaseNotes` field is limited to 35,000 characters.</span></span>

#### <a name="copyright"></a><span data-ttu-id="aaa4b-216">direitos autorais</span><span class="sxs-lookup"><span data-stu-id="aaa4b-216">copyright</span></span>
<span data-ttu-id="aaa4b-217">*(1.5 ou superior)* Detalhes sobre direitos autorais do pacote.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-217">*(1.5+)* Copyright details for the package.</span></span>

<span data-ttu-id="aaa4b-218">Ao carregar um pacote no nuget.org, o `copyright` campo é limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-218">When uploading a package to nuget.org, the `copyright` field is limited to 4000 characters.</span></span>

#### <a name="language"></a><span data-ttu-id="aaa4b-219">Linguagem</span><span class="sxs-lookup"><span data-stu-id="aaa4b-219">language</span></span>
<span data-ttu-id="aaa4b-220">A identificação de localidade para o pacote.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-220">The locale ID for the package.</span></span> <span data-ttu-id="aaa4b-221">Consulte [Criando pacotes localizados](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-221">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="aaa4b-222">tags</span><span class="sxs-lookup"><span data-stu-id="aaa4b-222">tags</span></span>
<span data-ttu-id="aaa4b-223">Uma lista delimitada por espaço de marcas e palavras-chave que descrevem o pacote e auxiliam na descoberta de pacotes por meio de pesquisa e filtragem.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-223">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

<span data-ttu-id="aaa4b-224">Ao carregar um pacote no nuget.org, o `tags` campo é limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-224">When uploading a package to nuget.org, the `tags` field is limited to 4000 characters.</span></span>

#### <a name="serviceable"></a><span data-ttu-id="aaa4b-225">serviceable</span><span class="sxs-lookup"><span data-stu-id="aaa4b-225">serviceable</span></span> 
<span data-ttu-id="aaa4b-226">*(3.3 ou superior)* Somente para uso interno do NuGet.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-226">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="aaa4b-227">repository</span><span class="sxs-lookup"><span data-stu-id="aaa4b-227">repository</span></span>
<span data-ttu-id="aaa4b-228">Metadados de repositório, que consistem em quatro atributos opcionais: `type` e `url` *(4.0 +)* e `branch` e `commit` *(4.6 +)*.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-228">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="aaa4b-229">Esses atributos permitem mapear o `.nupkg` para o repositório que o criou, com o potencial de ser detalhado como o nome do Branch individual e/ou confirmar o hash SHA-1 que criou o pacote.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-229">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="aaa4b-230">Essa deve ser uma URL disponível publicamente que pode ser invocada diretamente por um software de controle de versão.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-230">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="aaa4b-231">Ele não deve ser uma página HTML, pois isso é destinado ao computador.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-231">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="aaa4b-232">Para vincular à página do projeto, use o `projectUrl` campo, em vez disso.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-232">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="aaa4b-233">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-233">For example:</span></span>
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

<span data-ttu-id="aaa4b-234">Ao carregar um pacote no nuget.org, o `type` atributo é limitado a 100 caracteres e o `url` atributo é limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-234">When uploading a package to nuget.org, the `type` attribute is limited to 100 characters and the `url` attribute is limited to 4000 characters.</span></span>

#### <a name="title"></a><span data-ttu-id="aaa4b-235">título</span><span class="sxs-lookup"><span data-stu-id="aaa4b-235">title</span></span>
<span data-ttu-id="aaa4b-236">Um título amigável do pacote que pode ser usado em algumas exibições da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-236">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="aaa4b-237">(nuget.org e o Gerenciador de pacotes no Visual Studio não mostram título)</span><span class="sxs-lookup"><span data-stu-id="aaa4b-237">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

<span data-ttu-id="aaa4b-238">Ao carregar um pacote no nuget.org, o `title` campo é limitado a 256 caracteres, mas não é usado para fins de exibição.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-238">When uploading a package to nuget.org, the `title` field is limited to 256 characters but is not used for any display purposes.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="aaa4b-239">Elementos de coleção</span><span class="sxs-lookup"><span data-stu-id="aaa4b-239">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="aaa4b-240">packageTypes</span><span class="sxs-lookup"><span data-stu-id="aaa4b-240">packageTypes</span></span>
<span data-ttu-id="aaa4b-241">*(3.5 ou superior)* Uma coleção de zero ou mais elementos `<packageType>` que especificam o tipo do pacote se for diferente de um pacote de dependência tradicional.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-241">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="aaa4b-242">Cada packageType tem os atributos de *name* e *version*.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-242">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="aaa4b-243">Consulte [Definindo um tipo de pacote](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-243">See [Setting a package type](../create-packages/set-package-type.md).</span></span>

#### <a name="dependencies"></a><span data-ttu-id="aaa4b-244">dependencies</span><span class="sxs-lookup"><span data-stu-id="aaa4b-244">dependencies</span></span>
<span data-ttu-id="aaa4b-245">Uma coleção de zero ou mais elementos `<dependency>` que especificam as dependências do pacote.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-245">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="aaa4b-246">Cada dependência tem atributos de *id*, *version*, *include* (3.x ou superior) e *exclude* (3.x ou superior).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-246">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="aaa4b-247">Consulte [Dependências](#dependencies-element) abaixo.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-247">See [Dependencies](#dependencies-element) below.</span></span>

#### <a name="frameworkassemblies"></a><span data-ttu-id="aaa4b-248">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="aaa4b-248">frameworkAssemblies</span></span>
<span data-ttu-id="aaa4b-249">*(1.2 ou superior)* Uma coleção de zero ou mais elementos `<frameworkAssembly>` identifica as referências de assembly do .NET Framework que este pacote requer, o que garante que elas sejam adicionadas aos projetos que consomem o pacote.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-249">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="aaa4b-250">Cada frameworkAssembly tem os atributos *assemblyName* e *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-250">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="aaa4b-251">Consulte [Especificando as referências GAC de assembly do framework](#specifying-framework-assembly-references-gac) abaixo.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-251">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>

#### <a name="references"></a><span data-ttu-id="aaa4b-252">referências</span><span class="sxs-lookup"><span data-stu-id="aaa4b-252">references</span></span>
<span data-ttu-id="aaa4b-253">*(1.5 ou superior)* Uma coleção de zero ou mais assemblies de nomenclatura de elementos `<reference>` na pasta `lib` do pacote que são adicionados como referências de projeto.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-253">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="aaa4b-254">Cada referência tem um atributo *file*.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-254">Each reference has a *file* attribute.</span></span> <span data-ttu-id="aaa4b-255">`<references>` também pode conter um elemento `<group>` com um atributo *targetFramework*, que contém elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-255">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="aaa4b-256">Se omitido, todas as referências no `lib` são incluídas.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-256">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="aaa4b-257">Consulte [Especificando referências de assembly explícitas](#specifying-explicit-assembly-references) abaixo.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-257">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>

#### <a name="contentfiles"></a><span data-ttu-id="aaa4b-258">contentFiles</span><span class="sxs-lookup"><span data-stu-id="aaa4b-258">contentFiles</span></span>
<span data-ttu-id="aaa4b-259">*(3.3 ou superior)* Uma coleção de elementos `<files>` que identificam os arquivos de conteúdo para incluir o projeto consumidor.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-259">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="aaa4b-260">Esses arquivos são especificados com um conjunto de atributos que descrevem como eles devem ser usados dentro do sistema de projeto.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-260">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="aaa4b-261">Consulte [Especificando arquivos a serem incluídos no pacote](#specifying-files-to-include-in-the-package) abaixo.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-261">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>

#### <a name="files"></a><span data-ttu-id="aaa4b-262">files</span><span class="sxs-lookup"><span data-stu-id="aaa4b-262">files</span></span> 
<span data-ttu-id="aaa4b-263">O `<package>` nó pode conter um `<files>` nó como um irmão e `<metadata>` um `<contentFiles>` filho em `<metadata>` , para especificar quais arquivos de conteúdo e assembly devem ser incluídos no pacote.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-263">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="aaa4b-264">Consulte [Incluindo arquivos do assembly](#including-assembly-files) e [Incluindo arquivos de conteúdo](#including-content-files) mais adiante neste tópico para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-264">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="aaa4b-265">atributos de metadados</span><span class="sxs-lookup"><span data-stu-id="aaa4b-265">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="aaa4b-266">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="aaa4b-266">minClientVersion</span></span>
<span data-ttu-id="aaa4b-267">Especifica a versão mínima do cliente NuGet que pode instalar esse pacote, imposta pelo nuget.exe e pelo Gerenciador de Pacotes do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-267">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="aaa4b-268">Isso é usado sempre que o pacote depender de recursos específicos do arquivo `.nuspec` que foram adicionados em uma versão específica do cliente do NuGet.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-268">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="aaa4b-269">Por exemplo, um pacote usando o atributo `developmentDependency` deve especificar “2.8” para `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-269">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="aaa4b-270">Da mesma forma, um pacote usando o elemento `contentFiles` (consulte a próxima seção) deve definir `minClientVersion` para “3.3”.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-270">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="aaa4b-271">Observe também que, como os clientes do NuGet antes de 2.5 não reconhecem esse sinalizador, eles *sempre* recusam instalar o pacote, não importando o que `minClientVersion` contém.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-271">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata minClientVersion="100.0.0.1">
        <id>dasdas</id>
        <version>2.0.0</version>
        <title />
        <authors>dsadas</authors>
        <owners />
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>My package description.</description>
    </metadata>
    <files>
        <file src="content\one.txt" target="content\one.txt" />
    </files>
</package>
```

## <a name="replacement-tokens"></a><span data-ttu-id="aaa4b-272">Tokens de substituição</span><span class="sxs-lookup"><span data-stu-id="aaa4b-272">Replacement tokens</span></span>

<span data-ttu-id="aaa4b-273">Ao criar um pacote, o [ `nuget pack` comando](../reference/cli-reference/cli-ref-pack.md) substitui tokens de $ delimitados no `.nuspec` nó do arquivo `<metadata>` por valores provenientes de um arquivo de projeto ou da `pack` opção do comando `-properties` .</span><span class="sxs-lookup"><span data-stu-id="aaa4b-273">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="aaa4b-274">Na linha de comando, você especifica os valores de token com `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-274">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="aaa4b-275">Por exemplo, você pode usar um token como `$owners$` e `$desc$` no `.nuspec` e fornecer os valores no tempo de empacotamento da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-275">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="aaa4b-276">Para usar valores de um projeto, especifique os tokens descritos na tabela a seguir (AssemblyInfo refere-se ao arquivo em `Properties` como `AssemblyInfo.cs` ou `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-276">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="aaa4b-277">Para usar esses tokens, execute `nuget pack` com o arquivo de projeto em vez de apenas o `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-277">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="aaa4b-278">Por exemplo, ao usar o comando a seguir, os tokens `$id$` e `$version$` em um arquivo `.nuspec` são substituídos pelos valores `AssemblyName` e `AssemblyVersion` do projeto:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-278">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="aaa4b-279">Normalmente, quando você tem um projeto, você cria o `.nuspec` inicialmente usando `nuget spec MyProject.csproj`, o que inclui alguns desses tokens padrão automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-279">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="aaa4b-280">No entanto, se um projeto não tiver valores para os elementos `.nuspec` necessários, `nuget pack` falhará.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-280">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="aaa4b-281">Além disso, se você alterar os valores de projeto, lembre-se de recompilá-lo antes de criar o pacote. Isso pode ser feito convenientemente com a opção `build` do comando do pacote.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-281">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="aaa4b-282">Com exceção de `$configuration$`, os valores do projeto são usados como preferenciais sobre qualquer um com o mesmo token na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-282">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="aaa4b-283">Token</span><span class="sxs-lookup"><span data-stu-id="aaa4b-283">Token</span></span> | <span data-ttu-id="aaa4b-284">Origem do valor</span><span class="sxs-lookup"><span data-stu-id="aaa4b-284">Value source</span></span> | <span data-ttu-id="aaa4b-285">Valor</span><span class="sxs-lookup"><span data-stu-id="aaa4b-285">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="aaa4b-286">**$id $**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-286">**$id$**</span></span> | <span data-ttu-id="aaa4b-287">Arquivo de projeto</span><span class="sxs-lookup"><span data-stu-id="aaa4b-287">Project file</span></span> | <span data-ttu-id="aaa4b-288">AssemblyName (título) do arquivo de projeto</span><span class="sxs-lookup"><span data-stu-id="aaa4b-288">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="aaa4b-289">**$version $**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-289">**$version$**</span></span> | <span data-ttu-id="aaa4b-290">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="aaa4b-290">AssemblyInfo</span></span> | <span data-ttu-id="aaa4b-291">AssemblyInformationalVersion se existir, caso contrário AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="aaa4b-291">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="aaa4b-292">**$author $**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-292">**$author$**</span></span> | <span data-ttu-id="aaa4b-293">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="aaa4b-293">AssemblyInfo</span></span> | <span data-ttu-id="aaa4b-294">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="aaa4b-294">AssemblyCompany</span></span> |
| <span data-ttu-id="aaa4b-295">**$title $**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-295">**$title$**</span></span> | <span data-ttu-id="aaa4b-296">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="aaa4b-296">AssemblyInfo</span></span> | <span data-ttu-id="aaa4b-297">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="aaa4b-297">AssemblyTitle</span></span> |
| <span data-ttu-id="aaa4b-298">**$description $**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-298">**$description$**</span></span> | <span data-ttu-id="aaa4b-299">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="aaa4b-299">AssemblyInfo</span></span> | <span data-ttu-id="aaa4b-300">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="aaa4b-300">AssemblyDescription</span></span> |
| <span data-ttu-id="aaa4b-301">**$copyright $**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-301">**$copyright$**</span></span> | <span data-ttu-id="aaa4b-302">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="aaa4b-302">AssemblyInfo</span></span> | <span data-ttu-id="aaa4b-303">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="aaa4b-303">AssemblyCopyright</span></span> |
| <span data-ttu-id="aaa4b-304">**$configuration $**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-304">**$configuration$**</span></span> | <span data-ttu-id="aaa4b-305">DLL de assembly</span><span class="sxs-lookup"><span data-stu-id="aaa4b-305">Assembly DLL</span></span> | <span data-ttu-id="aaa4b-306">Configuração usada para compilar o assembly, com Depuração como padrão.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-306">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="aaa4b-307">Observe que, para criar um pacote usando uma configuração de Versão, você sempre usará `-properties Configuration=Release` na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-307">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="aaa4b-308">Tokens também podem ser usados para resolver caminhos quando você incluir [arquivos do assembly](#including-assembly-files) e [arquivos de conteúdo](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-308">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="aaa4b-309">Os tokens têm os mesmos nomes que as propriedades do MSBuild, tornando possível selecionar os arquivos a serem incluídos, dependendo da configuração de build atual.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-309">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="aaa4b-310">Por exemplo, se você usar os seguintes tokens no arquivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-310">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="aaa4b-311">E você compila um assembly cujo `AssemblyName` é `LoggingLibrary` com a configuração `Release` no MSBuild, as linhas resultantes no arquivo `.nuspec` do pacote são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-311">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="aaa4b-312">Elemento Dependencies</span><span class="sxs-lookup"><span data-stu-id="aaa4b-312">Dependencies element</span></span>

<span data-ttu-id="aaa4b-313">O elemento `<dependencies>` dentro do `<metadata>` contém diversos elementos `<dependency>` que identificam os outros pacotes dos quais o pacote de nível superior depende.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-313">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="aaa4b-314">Os atributos para cada `<dependency>` são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-314">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="aaa4b-315">Atributo</span><span class="sxs-lookup"><span data-stu-id="aaa4b-315">Attribute</span></span> | <span data-ttu-id="aaa4b-316">Descrição</span><span class="sxs-lookup"><span data-stu-id="aaa4b-316">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="aaa4b-317">(Obrigatório) A ID do pacote de dependência, como "EntityFramework" e "NUnit", que é o nome do pacote nuget.org mostrado em uma página do pacote.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-317">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="aaa4b-318">(Obrigatório) O intervalo de versões aceitáveis como uma dependência.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-318">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="aaa4b-319">Consulte [Controle de versão do pacote](../concepts/package-versioning.md#version-ranges) para ver a sintaxe exata.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-319">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="aaa4b-320">Não há suporte para versões flutuantes.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-320">Floating versions are not supported.</span></span> |
| <span data-ttu-id="aaa4b-321">include</span><span class="sxs-lookup"><span data-stu-id="aaa4b-321">include</span></span> | <span data-ttu-id="aaa4b-322">Uma lista delimitada por vírgulas de marcas de inclusão/exclusão (veja abaixo) que indicam a dependência a ser incluída no pacote final.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-322">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="aaa4b-323">O valor padrão é `all`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-323">The default value is `all`.</span></span> |
| <span data-ttu-id="aaa4b-324">excluir</span><span class="sxs-lookup"><span data-stu-id="aaa4b-324">exclude</span></span> | <span data-ttu-id="aaa4b-325">Uma lista delimitada por vírgulas de marcas de inclusão/exclusão (veja abaixo) que indicam a dependência a ser excluída do pacote final.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-325">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="aaa4b-326">O valor padrão é o `build,analyzers` que pode ser substituído.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-326">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="aaa4b-327">Mas `content/ ContentFiles` também são excluídos implicitamente no pacote final que não pode ser substituído.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-327">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="aaa4b-328">Marcas especificadas com `exclude` têm precedência sobre aquelas especificadas com `include`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-328">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="aaa4b-329">Por exemplo, `include="runtime, compile" exclude="compile"` é o mesmo que `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-329">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

<span data-ttu-id="aaa4b-330">Ao carregar um pacote no nuget.org, cada atributo de dependência `id` é limitado a 128 caracteres e o `version` atributo é limitado a 256 caracteres.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-330">When uploading a package to nuget.org, each dependency's `id` attribute is limited to 128 characters and the `version` attribute is limited to 256 characters.</span></span>

| <span data-ttu-id="aaa4b-331">Marca Incluir/Excluir</span><span class="sxs-lookup"><span data-stu-id="aaa4b-331">Include/Exclude tag</span></span> | <span data-ttu-id="aaa4b-332">Pastas afetadas do destino</span><span class="sxs-lookup"><span data-stu-id="aaa4b-332">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="aaa4b-333">contentFiles</span><span class="sxs-lookup"><span data-stu-id="aaa4b-333">contentFiles</span></span> | <span data-ttu-id="aaa4b-334">Conteúdo</span><span class="sxs-lookup"><span data-stu-id="aaa4b-334">Content</span></span> |
| <span data-ttu-id="aaa4b-335">runtime</span><span class="sxs-lookup"><span data-stu-id="aaa4b-335">runtime</span></span> | <span data-ttu-id="aaa4b-336">Runtime, Resources e FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="aaa4b-336">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="aaa4b-337">compilar</span><span class="sxs-lookup"><span data-stu-id="aaa4b-337">compile</span></span> | <span data-ttu-id="aaa4b-338">lib</span><span class="sxs-lookup"><span data-stu-id="aaa4b-338">lib</span></span> |
| <span data-ttu-id="aaa4b-339">compilar</span><span class="sxs-lookup"><span data-stu-id="aaa4b-339">build</span></span> | <span data-ttu-id="aaa4b-340">build (objetos e destinos do MSBuild)</span><span class="sxs-lookup"><span data-stu-id="aaa4b-340">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="aaa4b-341">nativa</span><span class="sxs-lookup"><span data-stu-id="aaa4b-341">native</span></span> | <span data-ttu-id="aaa4b-342">nativa</span><span class="sxs-lookup"><span data-stu-id="aaa4b-342">native</span></span> |
| <span data-ttu-id="aaa4b-343">nenhuma</span><span class="sxs-lookup"><span data-stu-id="aaa4b-343">none</span></span> | <span data-ttu-id="aaa4b-344">Nenhuma pasta</span><span class="sxs-lookup"><span data-stu-id="aaa4b-344">No folders</span></span> |
| <span data-ttu-id="aaa4b-345">all</span><span class="sxs-lookup"><span data-stu-id="aaa4b-345">all</span></span> | <span data-ttu-id="aaa4b-346">Todas as pastas</span><span class="sxs-lookup"><span data-stu-id="aaa4b-346">All folders</span></span> |

<span data-ttu-id="aaa4b-347">Por exemplo, as linhas a seguir indicam as dependências no `PackageA` versão 1.1.0 ou superior e `PackageB` versão 1.x.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-347">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="aaa4b-348">As linhas a seguir indicam dependências nos mesmos pacotes, mas especificam a inclusão de pastas `contentFiles` e `build` de `PackageA` tudo, mas as pastas `native` e `compile` de `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="aaa4b-348">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="aaa4b-349">Ao criar um `.nuspec` de um projeto usando `nuget spec` , as dependências que existem nesse projeto não são incluídas automaticamente no `.nuspec` arquivo resultante.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-349">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="aaa4b-350">Em vez disso, use `nuget pack myproject.csproj` e obtenha o arquivo *. nuspec* de dentro do arquivo *. nupkg* gerado.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-350">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="aaa4b-351">Esse *. nuspec* contém as dependências.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-351">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="aaa4b-352">Grupos de dependência</span><span class="sxs-lookup"><span data-stu-id="aaa4b-352">Dependency groups</span></span>

<span data-ttu-id="aaa4b-353">*Versão 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="aaa4b-353">*Version 2.0+*</span></span>

<span data-ttu-id="aaa4b-354">Como alternativa a uma única lista simples, as dependências podem ser especificadas de acordo com o perfil da estrutura do projeto de destino usando elementos `<group>` dentro de `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-354">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="aaa4b-355">Cada grupo tem um atributo chamado `targetFramework` e contém zero ou mais elementos `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-355">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="aaa4b-356">Essas referências são instaladas juntas quando a estrutura de destino é compatível com o perfil da estrutura do projeto.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-356">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="aaa4b-357">O elemento `<group>` sem um atributo `targetFramework` será usado como a lista de dependências padrão ou de fallback.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-357">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="aaa4b-358">Consulte [Estruturas de destino](../reference/target-frameworks.md) para ver os identificadores de estrutura exatos.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-358">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="aaa4b-359">O formato do grupo não pode ser combinado com uma lista simples.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-359">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="aaa4b-360">O formato do [moniker da estrutura de destino (TFM)](../reference/target-frameworks.md) usado na `lib/ref` pasta é diferente quando comparado com o TFM usado em `dependency groups` .</span><span class="sxs-lookup"><span data-stu-id="aaa4b-360">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="aaa4b-361">Se as estruturas de destino declaradas no `dependencies group` e a `lib/ref` pasta do `.nuspec` arquivo não tiverem correspondências exatas, o `pack` comando emitirá o aviso do [NuGet NU5128](../reference/errors-and-warnings/nu5128.md).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-361">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="aaa4b-362">O exemplo a seguir mostra diferentes variações do elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-362">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework=".NETFramework4.7.2">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="netcoreapp3.1">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="aaa4b-363">Referências de assembly explícitas</span><span class="sxs-lookup"><span data-stu-id="aaa4b-363">Explicit assembly references</span></span>

<span data-ttu-id="aaa4b-364">O `<references>` elemento é usado por projetos `packages.config` que usam para especificar explicitamente os assemblies que o projeto de destino deve referenciar ao usar o pacote.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-364">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="aaa4b-365">Referências explícitas são geralmente usadas apenas para assemblies de tempo de design.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-365">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="aaa4b-366">Para obter mais informações, consulte a página sobre como [selecionar assemblies referenciados por projetos](../create-packages/select-assemblies-referenced-by-projects.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-366">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="aaa4b-367">Por exemplo, o elemento `<references>` a seguir instrui o NuGet a adicionar referências a apenas `xunit.dll` e `xunit.extensions.dll`, mesmo se houver assemblies adicionais no pacote:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-367">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="aaa4b-368">Grupos de referência</span><span class="sxs-lookup"><span data-stu-id="aaa4b-368">Reference groups</span></span>

<span data-ttu-id="aaa4b-369">Como alternativa a uma única lista simples, as referências podem ser especificadas de acordo com o perfil da estrutura do projeto de destino usando elementos `<group>` dentro de `<references>`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-369">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="aaa4b-370">Cada grupo tem um atributo chamado `targetFramework` e contém zero ou mais elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-370">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="aaa4b-371">Essas referências são adicionadas a um projeto quando a estrutura de destino é compatível com o perfil de estrutura do projeto.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-371">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="aaa4b-372">O elemento `<group>` sem um atributo `targetFramework` será usado como a lista de referências padrão ou de fallback.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-372">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="aaa4b-373">Consulte [Estruturas de destino](../reference/target-frameworks.md) para ver os identificadores de estrutura exatos.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-373">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="aaa4b-374">O formato do grupo não pode ser combinado com uma lista simples.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-374">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="aaa4b-375">O exemplo a seguir mostra diferentes variações do elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-375">The following example shows different variations of the `<group>` element:</span></span>

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a><span data-ttu-id="aaa4b-376">Referências de assembly de estrutura</span><span class="sxs-lookup"><span data-stu-id="aaa4b-376">Framework assembly references</span></span>

<span data-ttu-id="aaa4b-377">Assemblies do Framework são aqueles que fazem parte do .NET Framework e já devem estar no GAC (cache de assembly global) para qualquer computador especificado.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-377">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="aaa4b-378">Ao identificar assemblies dentro do elemento `<frameworkAssemblies>`, um pacote pode garantir que as referências necessárias sejam adicionadas a um projeto caso este já não tenha essas referências.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-378">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="aaa4b-379">Tais assemblies, obviamente, não são incluídos em um pacote diretamente.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-379">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="aaa4b-380">O elemento `<frameworkAssemblies>` contém zero ou mais elementos `<frameworkAssembly>`, cada um deles especifica os seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-380">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="aaa4b-381">Atributo</span><span class="sxs-lookup"><span data-stu-id="aaa4b-381">Attribute</span></span> | <span data-ttu-id="aaa4b-382">Descrição</span><span class="sxs-lookup"><span data-stu-id="aaa4b-382">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aaa4b-383">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-383">**assemblyName**</span></span> | <span data-ttu-id="aaa4b-384">(Obrigatório) O nome totalmente qualificado do assembly.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-384">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="aaa4b-385">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-385">**targetFramework**</span></span> | <span data-ttu-id="aaa4b-386">(Opcional) Especifica a estrutura de destino à qual esta referência se aplica.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-386">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="aaa4b-387">Se omitido, indica que a referência se aplica a todas as estruturas.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-387">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="aaa4b-388">Consulte [Estruturas de destino](../reference/target-frameworks.md) para ver os identificadores de estrutura exatos.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-388">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="aaa4b-389">O exemplo a seguir mostra uma referência a `System.Net` todas as estruturas de destino e uma referência a `System.ServiceModel` apenas para o .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-389">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="aaa4b-390">Incluindo arquivos do assembly</span><span class="sxs-lookup"><span data-stu-id="aaa4b-390">Including assembly files</span></span>

<span data-ttu-id="aaa4b-391">Se você seguir as convenções descritas em [Criando um pacote](../create-packages/creating-a-package.md), não será necessário especificar explicitamente uma lista de arquivos no arquivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-391">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="aaa4b-392">O comando `nuget pack` escolherá automaticamente os arquivos necessários.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-392">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="aaa4b-393">Quando um pacote é instalado em um projeto, o NuGet adiciona automaticamente as referências de assembly às DLLs do pacote, *excluindo* aquelas que são nomeados `.resources.dll` porque são considerados assemblies satélites.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-393">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="aaa4b-394">Por esse motivo, evite usar `.resources.dll` para arquivos que contêm código de pacote essencial.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-394">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="aaa4b-395">Para ignorar esse comportamento automático e controlar explicitamente quais arquivos são incluídos em um pacote, coloque uma elemento `<files>` como um filho de `<package>` (e um irmão de `<metadata>`), identificando cada arquivo com um elemento `<file>` separado.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-395">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="aaa4b-396">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-396">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="aaa4b-397">Com o NuGet 2.x e anteriores, e em projetos que usam `packages.config`, o elemento `<files>` também é usado para incluir arquivos de conteúdo imutáveis quando um pacote é instalado.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-397">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="aaa4b-398">Com o NuGet 3.3 ou superior e projetos PackageReference, o elemento `<contentFiles>` é usado.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-398">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="aaa4b-399">Consulte [Incluindo arquivos de conteúdo](#including-content-files) abaixo para ver os detalhes.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-399">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="aaa4b-400">Atributos do elemento de arquivo</span><span class="sxs-lookup"><span data-stu-id="aaa4b-400">File element attributes</span></span>

<span data-ttu-id="aaa4b-401">Cada elemento `<file>` especifica os seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-401">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="aaa4b-402">Atributo</span><span class="sxs-lookup"><span data-stu-id="aaa4b-402">Attribute</span></span> | <span data-ttu-id="aaa4b-403">Descrição</span><span class="sxs-lookup"><span data-stu-id="aaa4b-403">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aaa4b-404">**src**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-404">**src**</span></span> | <span data-ttu-id="aaa4b-405">O local do arquivo ou arquivos a serem incluídos, sujeito a exclusões especificadas pelo atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-405">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="aaa4b-406">O caminho é relativo ao arquivo `.nuspec`, a menos que um caminho absoluto seja especificado.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-406">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="aaa4b-407">O caractere curinga `*` é permitido e o caractere curinga duplo `**` sugere uma pesquisa de pastas recursiva.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-407">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="aaa4b-408">**destino**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-408">**target**</span></span> | <span data-ttu-id="aaa4b-409">O caminho relativo para a pasta dentro do pacote em que os arquivos de origem são colocados, os quais devem começar com `lib`, `content`, `build` ou `tools`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-409">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="aaa4b-410">Consulte [Criando um .nuspec de um diretório de trabalho baseado em convenção](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-410">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="aaa4b-411">**excluí**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-411">**exclude**</span></span> | <span data-ttu-id="aaa4b-412">Uma lista separada por ponto-e-vírgula de arquivos ou padrões de arquivo para excluir o local `src`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-412">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="aaa4b-413">O caractere curinga `*` é permitido e o caractere curinga duplo `**` sugere uma pesquisa de pastas recursiva.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-413">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="aaa4b-414">Exemplos</span><span class="sxs-lookup"><span data-stu-id="aaa4b-414">Examples</span></span>

<span data-ttu-id="aaa4b-415">**Assembly único**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-415">**Single assembly**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="library.dll" target="lib" />

Packaged result:
    lib\library.dll
```

<span data-ttu-id="aaa4b-416">**Assembly único específico para uma estrutura de destino**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-416">**Single assembly specific to a target framework**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="assemblies\net40\library.dll" target="lib\net40" />

Packaged result:
    lib\net40\library.dll
```

<span data-ttu-id="aaa4b-417">**Conjunto de DLLs que usam um caractere curinga**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-417">**Set of DLLs using a wildcard**</span></span>

```
Source files:
    bin\release\libraryA.dll
    bin\release\libraryB.dll

.nuspec entry:
    <file src="bin\release\*.dll" target="lib" />

Packaged result:
    lib\libraryA.dll
    lib\libraryB.dll
```

<span data-ttu-id="aaa4b-418">**DLLs de estruturas diferentes**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-418">**DLLs for different frameworks**</span></span>

```
Source files:
    lib\net40\library.dll
    lib\net20\library.dll

.nuspec entry (using ** recursive search):
    <file src="lib\**" target="lib" />

Packaged result:
    lib\net40\library.dll
    lib\net20\library.dll
```

<span data-ttu-id="aaa4b-419">**Excluindo arquivos**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-419">**Excluding files**</span></span>

```
Source files:
    \tools\fileA.bak
    \tools\fileB.bak
    \tools\fileA.log
    \tools\build\fileB.log

.nuspec entries:
    <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
    <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

Package result:
    (no files)
```

## <a name="including-content-files"></a><span data-ttu-id="aaa4b-420">Incluindo arquivos de conteúdo</span><span class="sxs-lookup"><span data-stu-id="aaa4b-420">Including content files</span></span>

<span data-ttu-id="aaa4b-421">Arquivos de conteúdo são arquivos imutáveis que um pacote incluir em um projeto.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-421">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="aaa4b-422">Sendo imutáveis, eles não foram projetados para serem modificados pelo projeto consumidor.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-422">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="aaa4b-423">Alguns exemplos de arquivos de conteúdo:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-423">Example content files include:</span></span>

- <span data-ttu-id="aaa4b-424">Imagens que são inseridas como recursos</span><span class="sxs-lookup"><span data-stu-id="aaa4b-424">Images that are embedded as resources</span></span>
- <span data-ttu-id="aaa4b-425">Arquivos de origem que já são compilados</span><span class="sxs-lookup"><span data-stu-id="aaa4b-425">Source files that are already compiled</span></span>
- <span data-ttu-id="aaa4b-426">Scripts que precisam ser incluídos na saída de build do projeto</span><span class="sxs-lookup"><span data-stu-id="aaa4b-426">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="aaa4b-427">Arquivos de configuração para o pacote que precisam ser incluídos no projeto, mas não precisam de nenhuma alteração específica do projeto</span><span class="sxs-lookup"><span data-stu-id="aaa4b-427">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="aaa4b-428">Arquivos de conteúdo são incluídos em um pacote usando o elemento `<files>`, especificando a pasta `content` no atributo `target`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-428">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="aaa4b-429">No entanto, esses arquivos são ignorados quando o pacote é instalado em um projeto usando PackageReference, que usa o elemento `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-429">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="aaa4b-430">Para máxima compatibilidade com projetos de consumo, é ideal que um pacote especifique os arquivos de conteúdo em ambos os elementos.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-430">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="aaa4b-431">Usando o elemento de arquivos para arquivos de conteúdo</span><span class="sxs-lookup"><span data-stu-id="aaa4b-431">Using the files element for content files</span></span>

<span data-ttu-id="aaa4b-432">Para arquivos de conteúdo, basta usar o mesmo formato que os arquivos do assembly, porém especifique `content` como a pasta base no atributo `target` conforme mostrado nos exemplos a seguir.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-432">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="aaa4b-433">**Arquivos de conteúdo básico**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-433">**Basic content files**</span></span>

```
Source files:
    css\mobile\style1.css
    css\mobile\style2.css

.nuspec entry:
    <file src="css\mobile\*.css" target="content\css\mobile" />

Packaged result:
    content\css\mobile\style1.css
    content\css\mobile\style2.css
```

<span data-ttu-id="aaa4b-434">**Arquivos de conteúdo com a estrutura de diretório**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-434">**Content files with directory structure**</span></span>

```
Source files:
    css\mobile\style.css
    css\mobile\wp7\style.css
    css\browser\style.css

.nuspec entry:
    <file src="css\**\*.css" target="content\css" />

Packaged result:
    content\css\mobile\style.css
    content\css\mobile\wp7\style.css
    content\css\browser\style.css
```

<span data-ttu-id="aaa4b-435">**Arquivo de conteúdo específico para uma estrutura de destino**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-435">**Content file specific to a target framework**</span></span>

```
Source file:
    css\cool\style.css

.nuspec entry
    <file src="css\cool\style.css" target="Content" />

Packaged result:
    content\style.css
```

<span data-ttu-id="aaa4b-436">**Arquivo de conteúdo copiado para uma pasta com ponto no nome**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-436">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="aaa4b-437">Nesse caso, o NuGet vê que a extensão em `target` não corresponde à extensão em `src` e, portanto, trata essa parte do nome no `target` como uma pasta:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-437">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

```
Source file:
    images\picture.png

.nuspec entry:
    <file src="images\picture.png" target="Content\images\package.icons" />

Packaged result:
    content\images\package.icons\picture.png
```

<span data-ttu-id="aaa4b-438">**Arquivos de conteúdo sem extensões**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-438">**Content files without extensions**</span></span>

<span data-ttu-id="aaa4b-439">Para incluir arquivos sem extensão, use os curingas `*` ou `**`:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-439">To include files without an extension, use the `*` or `**` wildcards:</span></span>

```
Source file:
    flags\installed

.nuspec entry:
    <file src="flags\**" target="flags" />

Packaged result:
    flags\installed
```

<span data-ttu-id="aaa4b-440">**Arquivos de conteúdo com caminho e destino profundos**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-440">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="aaa4b-441">Nesse caso, como as extensões de arquivo de origem e de destino correspondem, o NuGet pressupõe que o destino é um nome de arquivo e não uma pasta:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-441">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

```
Source file:
    css\cool\style.css

.nuspec entry:
    <file src="css\cool\style.css" target="Content\css\cool" />
    or:
    <file src="css\cool\style.css" target="Content\css\cool\style.css" />

Packaged result:
    content\css\cool\style.css
```

<span data-ttu-id="aaa4b-442">**Renomeando um arquivo de conteúdo no pacote**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-442">**Renaming a content file in the package**</span></span>

```
Source file:
    ie\css\style.css

.nuspec entry:
    <file src="ie\css\style.css" target="Content\css\ie.css" />

Packaged result:
    content\css\ie.css
```

<span data-ttu-id="aaa4b-443">**Excluindo arquivos**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-443">**Excluding files**</span></span>

```
Source file:
    docs\*.txt (multiple files)

.nuspec entry:
    <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
    or
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

Packaged result:
    All .txt files from docs except admin.txt (first example)
    All .txt files from docs except admin.txt and log.txt (second example)
```

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="aaa4b-444">Usando o elemento contentFiles para arquivos de conteúdo</span><span class="sxs-lookup"><span data-stu-id="aaa4b-444">Using the contentFiles element for content files</span></span>

<span data-ttu-id="aaa4b-445">*NuGet 4.0 e posteriores com PackageReference*</span><span class="sxs-lookup"><span data-stu-id="aaa4b-445">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="aaa4b-446">Por padrão, um pacote coloca o conteúdo em uma pasta `contentFiles` (veja abaixo) e `nuget pack` incluiu todos os arquivos nessa pasta usando os atributos padrão.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-446">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="aaa4b-447">Nesse caso, não é necessário incluir um nó `contentFiles` no `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-447">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="aaa4b-448">Para controlar quais arquivos são incluídos, o elemento `<contentFiles>` especifica uma coleção de elementos `<files>` que identificam as inclusões dos arquivos exatos.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-448">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="aaa4b-449">Esses arquivos são especificados com um conjunto de atributos que descrevem como eles devem ser usados dentro do sistema de projeto:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-449">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="aaa4b-450">Atributo</span><span class="sxs-lookup"><span data-stu-id="aaa4b-450">Attribute</span></span> | <span data-ttu-id="aaa4b-451">Descrição</span><span class="sxs-lookup"><span data-stu-id="aaa4b-451">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aaa4b-452">**incluir**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-452">**include**</span></span> | <span data-ttu-id="aaa4b-453">(Obrigatório) O local do arquivo ou arquivos a serem incluídos, sujeito a exclusões especificadas pelo atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-453">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="aaa4b-454">O caminho é relativo à `contentFiles` pasta, a menos que um caminho absoluto seja especificado.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-454">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="aaa4b-455">O caractere curinga `*` é permitido e o caractere curinga duplo `**` sugere uma pesquisa de pastas recursiva.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-455">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="aaa4b-456">**excluí**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-456">**exclude**</span></span> | <span data-ttu-id="aaa4b-457">Uma lista separada por ponto-e-vírgula de arquivos ou padrões de arquivo para excluir o local `src`.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-457">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="aaa4b-458">O caractere curinga `*` é permitido e o caractere curinga duplo `**` sugere uma pesquisa de pastas recursiva.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-458">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="aaa4b-459">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-459">**buildAction**</span></span> | <span data-ttu-id="aaa4b-460">A ação de compilação a ser atribuída ao item de conteúdo para o MSBuild, como,,, `Content` `None` `Embedded Resource` `Compile` etc. O padrão é `Compile` .</span><span class="sxs-lookup"><span data-stu-id="aaa4b-460">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="aaa4b-461">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-461">**copyToOutput**</span></span> | <span data-ttu-id="aaa4b-462">Um booliano que indica se os itens de conteúdo devem ser copiados para a pasta de saída Build (ou Publish).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-462">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="aaa4b-463">O padrão é falso.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-463">The default is false.</span></span> |
| <span data-ttu-id="aaa4b-464">**flatten**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-464">**flatten**</span></span> | <span data-ttu-id="aaa4b-465">Um valor booliano que indica se os itens de conteúdo devem ser copiados para uma única pasta na saída do build (verdadeiro) ou preservar a estrutura de pasta no pacote (falso).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-465">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="aaa4b-466">Esse sinalizador só funciona quando o sinalizador copyToOutput está definido como true.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-466">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="aaa4b-467">O padrão é falso.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-467">The default is false.</span></span> |

<span data-ttu-id="aaa4b-468">Ao instalar um pacote, o NuGet aplicará os elementos filho de `<contentFiles>` de cima para baixo.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-468">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="aaa4b-469">Se várias entradas corresponderem ao mesmo arquivo, todas as entradas serão aplicadas.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-469">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="aaa4b-470">A entrada superior substitui as entradas mais baixas em caso de conflito para o mesmo atributo.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-470">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="aaa4b-471">Estrutura de pastas do pacote</span><span class="sxs-lookup"><span data-stu-id="aaa4b-471">Package folder structure</span></span>

<span data-ttu-id="aaa4b-472">O projeto do pacote deve estruturar o conteúdo usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-472">The package project should structure content using the following pattern:</span></span>

```
/contentFiles/{codeLanguage}/{TxM}/{any?}
```

- <span data-ttu-id="aaa4b-473">`codeLanguages` pode ser `cs`, `vb`, `fs`, `any` ou o equivalente em letras minúsculas de determinado `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="aaa4b-473">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="aaa4b-474">`TxM` é qualquer moniker da estrutura de destino legal compatível com o NuGet (consulte [Estruturas de destino](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="aaa4b-474">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="aaa4b-475">Qualquer estrutura de pasta pode ser acrescentada ao final dessa sintaxe.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-475">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="aaa4b-476">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-476">For example:</span></span>

```
Language- and framework-agnostic:
    /contentFiles/any/any/config.xml

net45 content for all languages
    /contentFiles/any/net45/config.xml

C#-specific content for net45 and up
    /contentFiles/cs/net45/sample.cs
```

<span data-ttu-id="aaa4b-477">As pastas vazias podem usar `.` para recusar o fornecimento de conteúdo para certas combinações de idioma e TxM, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-477">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

```
/contentFiles/vb/any/code.vb
/contentFiles/cs/any/.
```

#### <a name="example-contentfiles-section"></a><span data-ttu-id="aaa4b-478">Exemplo da seção contentFiles</span><span class="sxs-lookup"><span data-stu-id="aaa4b-478">Example contentFiles section</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <contentFiles>
            <!-- Embed image resources -->
            <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
            <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

            <!-- Embed all image resources under contentFiles/cs/ -->
            <files include="cs/**/*.png" buildAction="EmbeddedResource" />

            <!-- Copy config.xml to the root of the output folder -->
            <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

            <!-- Copy run.cmd to the output folder and keep the directory structure -->
            <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

            <!-- Include everything in the scripts folder except exe files -->
            <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
        </contentFiles>
        </metadata>
</package>
```

## <a name="framework-reference-groups"></a><span data-ttu-id="aaa4b-479">Grupos de referência do Framework</span><span class="sxs-lookup"><span data-stu-id="aaa4b-479">Framework reference groups</span></span>

<span data-ttu-id="aaa4b-480">*Versão 5.1 + wih PackageReference apenas*</span><span class="sxs-lookup"><span data-stu-id="aaa4b-480">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="aaa4b-481">As referências de estrutura são um conceito do .NET Core que representa estruturas compartilhadas, como WPF ou Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-481">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="aaa4b-482">Ao especificar uma estrutura compartilhada, o pacote garante que todas as suas dependências de estrutura sejam incluídas no projeto de referência.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-482">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="aaa4b-483">Cada `<group>` elemento requer um `targetFramework` atributo e zero ou mais `<frameworkReference>` elementos.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-483">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="aaa4b-484">O exemplo a seguir mostra um nuspec gerado para um projeto do WPF do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-484">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="aaa4b-485">Observe que a criação manual de nuspecs que contêm referências de estrutura não é recomendada.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-485">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="aaa4b-486">Em vez disso, considere usar o pacote de [destinos](msbuild-targets.md) , que os inferirá automaticamente do projeto.</span><span class="sxs-lookup"><span data-stu-id="aaa4b-486">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

```xml
<package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
  <metadata>
    <dependencies>
      <group targetFramework=".NETCoreApp3.1" />
    </dependencies>
    <frameworkReferences>
      <group targetFramework=".NETCoreApp3.1">
        <frameworkReference name="Microsoft.WindowsDesktop.App.WPF" />
      </group>
    </frameworkReferences>
  </metadata>
</package>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="aaa4b-487">Arquivos nuspec de exemplo</span><span class="sxs-lookup"><span data-stu-id="aaa4b-487">Example nuspec files</span></span>

<span data-ttu-id="aaa4b-488">**Um simples `.nuspec` que não especifica dependências ou arquivos**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-488">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

<span data-ttu-id="aaa4b-489">**Um `.nuspec` com dependências**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-489">**A `.nuspec` with dependencies**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

<span data-ttu-id="aaa4b-490">**Um `.nuspec` com arquivos**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-490">**A `.nuspec` with files**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

<span data-ttu-id="aaa4b-491">**Um `.nuspec` com assemblies de estrutura**</span><span class="sxs-lookup"><span data-stu-id="aaa4b-491">**A `.nuspec` with framework assemblies**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

<span data-ttu-id="aaa4b-492">Neste exemplo, os seguintes itens são instalados em destinos específicos do projeto:</span><span class="sxs-lookup"><span data-stu-id="aaa4b-492">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="aaa4b-493">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="aaa4b-493">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="aaa4b-494">Perfil de Cliente do .NET4 -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="aaa4b-494">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="aaa4b-495">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="aaa4b-495">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="aaa4b-496">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="aaa4b-496">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
