---
title: Referência de arquivo. nuspec para NuGet
description: O arquivo .nuspec contém metadados de pacote usados ao compilar um pacote e para fornecer informações para os consumidores do pacote.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: f91d47bdf9b957b512d3d83434693ee93de07afb
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623130"
---
# <a name="nuspec-reference"></a><span data-ttu-id="6eca0-103">Referência do .nuspec</span><span class="sxs-lookup"><span data-stu-id="6eca0-103">.nuspec reference</span></span>

<span data-ttu-id="6eca0-104">Um arquivo `.nuspec` é um manifesto XML que contém metadados do pacote.</span><span class="sxs-lookup"><span data-stu-id="6eca0-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="6eca0-105">Esse manifesto é usado para compilar o pacote e fornecer informações aos consumidores.</span><span class="sxs-lookup"><span data-stu-id="6eca0-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="6eca0-106">O manifesto sempre é incluído em um pacote.</span><span class="sxs-lookup"><span data-stu-id="6eca0-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="6eca0-107">Neste tópico:</span><span class="sxs-lookup"><span data-stu-id="6eca0-107">In this topic:</span></span>

- [<span data-ttu-id="6eca0-108">Formato e esquema geral</span><span class="sxs-lookup"><span data-stu-id="6eca0-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="6eca0-109">[Tokens de substituição](#replacement-tokens) (quando usados com um projeto do Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="6eca0-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="6eca0-110">Dependências</span><span class="sxs-lookup"><span data-stu-id="6eca0-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="6eca0-111">Referências de assembly explícitas</span><span class="sxs-lookup"><span data-stu-id="6eca0-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="6eca0-112">Referências de assembly de estrutura</span><span class="sxs-lookup"><span data-stu-id="6eca0-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="6eca0-113">Incluindo arquivos do assembly</span><span class="sxs-lookup"><span data-stu-id="6eca0-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="6eca0-114">Incluindo arquivos de conteúdo</span><span class="sxs-lookup"><span data-stu-id="6eca0-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="6eca0-115">Arquivos nuspec de exemplo</span><span class="sxs-lookup"><span data-stu-id="6eca0-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="6eca0-116">Compatibilidade de tipo de projeto</span><span class="sxs-lookup"><span data-stu-id="6eca0-116">Project type compatibility</span></span>

- <span data-ttu-id="6eca0-117">Use o `.nuspec` com `nuget.exe pack` para projetos de estilo não-SDK que usam o `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="6eca0-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="6eca0-118">Um `.nuspec` arquivo não é necessário para criar pacotes para [projetos de estilo SDK](../resources/check-project-format.md) (normalmente .net Core e .net Standard projetos que usam o [atributo SDK](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="6eca0-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="6eca0-119">(Observe que um `.nuspec` é gerado quando você cria o pacote.)</span><span class="sxs-lookup"><span data-stu-id="6eca0-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="6eca0-120">Se você estiver criando um pacote usando `dotnet.exe pack` ou `msbuild pack target` , recomendamos que [inclua todas as propriedades](../reference/msbuild-targets.md#pack-target) que normalmente estão no `.nuspec` arquivo no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="6eca0-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="6eca0-121">No entanto, você pode optar por [usar um `.nuspec` arquivo para empacotar usando o `dotnet.exe` ou `msbuild pack target` o ](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="6eca0-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="6eca0-122">Para projetos migrados do `packages.config` para o [PackageReference](../consume-packages/package-references-in-project-files.md), um `.nuspec` arquivo não é necessário para criar o pacote.</span><span class="sxs-lookup"><span data-stu-id="6eca0-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="6eca0-123">Em vez disso, use o [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="6eca0-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="6eca0-124">Formato e esquema geral</span><span class="sxs-lookup"><span data-stu-id="6eca0-124">General form and schema</span></span>

<span data-ttu-id="6eca0-125">O arquivo de esquema `nuspec.xsd` atual pode ser encontrado no [repositório GitHub do NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="6eca0-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="6eca0-126">Dentro desse esquema, um arquivo `.nuspec` tem o seguinte formato geral:</span><span class="sxs-lookup"><span data-stu-id="6eca0-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="6eca0-127">Para obter uma representação visual do esquema, abra o arquivo de esquema no Visual Studio no modo de Design e clique no link **Gerenciador de Esquema XML**.</span><span class="sxs-lookup"><span data-stu-id="6eca0-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="6eca0-128">Como alternativa, abra o arquivo como código, clique com o botão direito do mouse no editor e selecione **Mostrar Gerenciador de Esquema XML**.</span><span class="sxs-lookup"><span data-stu-id="6eca0-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="6eca0-129">De qualquer forma, você receberá uma exibição como a mostrada abaixo (quando expandido):</span><span class="sxs-lookup"><span data-stu-id="6eca0-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Gerenciador de Esquema do Visual Studio com o nuspec.xsd aberto](media/SchemaExplorer.png)

<span data-ttu-id="6eca0-131">Todos os nomes de elementos XML no arquivo. nuspec diferenciam maiúsculas de minúsculas, como é o caso de XML em geral.</span><span class="sxs-lookup"><span data-stu-id="6eca0-131">All XML element names in the .nuspec file are case-sensitive, as is the case for XML in general.</span></span> <span data-ttu-id="6eca0-132">Por exemplo, o uso do elemento de metadados `<description>` está correto e `<Description>` não está correto.</span><span class="sxs-lookup"><span data-stu-id="6eca0-132">For example, using the metadata element `<description>` is correct and `<Description>` is not correct.</span></span> <span data-ttu-id="6eca0-133">A capitalização correta para cada nome de elemento está documentada abaixo.</span><span class="sxs-lookup"><span data-stu-id="6eca0-133">The proper casing for each element name is documented below.</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="6eca0-134">Elementos de metadados necessários</span><span class="sxs-lookup"><span data-stu-id="6eca0-134">Required metadata elements</span></span>

<span data-ttu-id="6eca0-135">Embora os elementos a seguir sejam os requisitos mínimos para um pacote, considere adicionar os [elementos de metadados opcionais](#optional-metadata-elements) para melhorar a experiência geral que os desenvolvedores têm com o pacote.</span><span class="sxs-lookup"><span data-stu-id="6eca0-135">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="6eca0-136">Esses elementos precisam aparecer dentro de um elemento `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-136">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="6eca0-137">id</span><span class="sxs-lookup"><span data-stu-id="6eca0-137">id</span></span> 
<span data-ttu-id="6eca0-138">O identificador de pacote que não diferencia maiúsculas de minúsculas, o qual deve ser exclusivo no nuget.org ou em qualquer galeria na qual o pacote reside.</span><span class="sxs-lookup"><span data-stu-id="6eca0-138">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="6eca0-139">IDs podem não conter espaços nem caracteres que não sejam válidos para uma URL e geralmente seguem as regras de namespace do .NET.</span><span class="sxs-lookup"><span data-stu-id="6eca0-139">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="6eca0-140">Consulte [Escolhendo um identificador de pacote exclusivo](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) para ver diretrizes.</span><span class="sxs-lookup"><span data-stu-id="6eca0-140">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>

<span data-ttu-id="6eca0-141">Ao carregar um pacote no nuget.org, o `id` campo é limitado a 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6eca0-141">When uploading a package to nuget.org, the `id` field is limited to 128 characters.</span></span>

#### <a name="version"></a><span data-ttu-id="6eca0-142">version</span><span class="sxs-lookup"><span data-stu-id="6eca0-142">version</span></span>
<span data-ttu-id="6eca0-143">A versão do pacote, seguindo o padrão *principal.secundária.patch*.</span><span class="sxs-lookup"><span data-stu-id="6eca0-143">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="6eca0-144">Os números de versão podem incluir um sufixo de pré-lançamento, conforme descrito em [Controle de versões de pré-lançamento](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="6eca0-144">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 

<span data-ttu-id="6eca0-145">Ao carregar um pacote no nuget.org, o `version` campo é limitado a 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6eca0-145">When uploading a package to nuget.org, the `version` field is limited to 64 characters.</span></span>

#### <a name="description"></a><span data-ttu-id="6eca0-146">descrição</span><span class="sxs-lookup"><span data-stu-id="6eca0-146">description</span></span>
<span data-ttu-id="6eca0-147">Uma descrição do pacote para exibição da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="6eca0-147">A description of the package for UI display.</span></span>

<span data-ttu-id="6eca0-148">Ao carregar um pacote no nuget.org, o `description` campo é limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6eca0-148">When uploading a package to nuget.org, the `description` field is limited to 4000 characters.</span></span>

#### <a name="authors"></a><span data-ttu-id="6eca0-149">authors</span><span class="sxs-lookup"><span data-stu-id="6eca0-149">authors</span></span>
<span data-ttu-id="6eca0-150">Uma lista separada por vírgulas de autores de pacotes, que correspondem aos nomes de perfil em nuget.org. Eles são exibidos na galeria do NuGet em nuget.org e são usados para fazer referência cruzada de pacotes pelos mesmos autores.</span><span class="sxs-lookup"><span data-stu-id="6eca0-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

<span data-ttu-id="6eca0-151">Ao carregar um pacote no nuget.org, o `authors` campo é limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6eca0-151">When uploading a package to nuget.org, the `authors` field is limited to 4000 characters.</span></span>

### <a name="optional-metadata-elements"></a><span data-ttu-id="6eca0-152">Elementos de metadados opcionais</span><span class="sxs-lookup"><span data-stu-id="6eca0-152">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="6eca0-153">owners</span><span class="sxs-lookup"><span data-stu-id="6eca0-153">owners</span></span>
<span data-ttu-id="6eca0-154">Uma lista separada por vírgulas dos criadores de pacote usando nomes de perfil em nuget.org. Isso geralmente é a mesma lista que em `authors` e é ignorado ao carregar o pacote para o NuGet.org. Consulte [Gerenciando proprietários de pacotes em NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="6eca0-154">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="6eca0-155">projectUrl</span><span class="sxs-lookup"><span data-stu-id="6eca0-155">projectUrl</span></span>
<span data-ttu-id="6eca0-156">Uma URL para a home page do pacote, geralmente mostrada em exibições de interface do usuário, bem como em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="6eca0-156">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

<span data-ttu-id="6eca0-157">Ao carregar um pacote no nuget.org, o `projectUrl` campo é limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6eca0-157">When uploading a package to nuget.org, the `projectUrl` field is limited to 4000 characters.</span></span>

#### <a name="licenseurl"></a><span data-ttu-id="6eca0-158">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="6eca0-158">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="6eca0-159">licenseUrl foi preterido.</span><span class="sxs-lookup"><span data-stu-id="6eca0-159">licenseUrl is deprecated.</span></span> <span data-ttu-id="6eca0-160">Use a licença em vez disso.</span><span class="sxs-lookup"><span data-stu-id="6eca0-160">Use license instead.</span></span>

<span data-ttu-id="6eca0-161">Uma URL para a licença do pacote, geralmente mostrada em interfaces do tipo nuget.org.</span><span class="sxs-lookup"><span data-stu-id="6eca0-161">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

<span data-ttu-id="6eca0-162">Ao carregar um pacote no nuget.org, o `licenseUrl` campo é limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6eca0-162">When uploading a package to nuget.org, the `licenseUrl` field is limited to 4000 characters.</span></span>

#### <a name="license"></a><span data-ttu-id="6eca0-163">license</span><span class="sxs-lookup"><span data-stu-id="6eca0-163">license</span></span>

<span data-ttu-id="6eca0-164">*Com suporte com **NuGet 4.9.0** e superior*</span><span class="sxs-lookup"><span data-stu-id="6eca0-164">*Supported with **NuGet 4.9.0** and above*</span></span>

<span data-ttu-id="6eca0-165">Uma expressão de licença SPDX ou um caminho para um arquivo de licença dentro do pacote, geralmente mostrado em interfaces de grupo como nuget.org. Se você estiver licenciando o pacote em uma licença comum, como MIT ou BSD-2-cláusula, use o [identificador de licença SPDX](https://spdx.org/licenses/)associado.</span><span class="sxs-lookup"><span data-stu-id="6eca0-165">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="6eca0-166">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6eca0-166">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="6eca0-167">O NuGet.org só aceita expressões de licença que são aprovadas pela iniciativa de software livre ou pela base de softwares gratuita.</span><span class="sxs-lookup"><span data-stu-id="6eca0-167">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="6eca0-168">Se o pacote for licenciado sob várias licenças comuns, você poderá especificar uma licença composta usando a [sintaxe de expressão SPDX versão 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="6eca0-168">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="6eca0-169">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6eca0-169">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="6eca0-170">Se você usar uma licença personalizada que não é suportada por expressões de licença, poderá empacotar um `.txt` `.md` arquivo ou com o texto da licença.</span><span class="sxs-lookup"><span data-stu-id="6eca0-170">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="6eca0-171">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6eca0-171">For example:</span></span>

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

<span data-ttu-id="6eca0-172">Para o equivalente do MSBuild, dê uma olhada no [empacotamento de uma expressão de licença ou um arquivo de licença](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="6eca0-172">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="6eca0-173">A sintaxe exata das expressões de licença do NuGet é descrita abaixo em [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="6eca0-173">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="6eca0-174">iconUrl</span><span class="sxs-lookup"><span data-stu-id="6eca0-174">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="6eca0-175">iconUrl foi preterido.</span><span class="sxs-lookup"><span data-stu-id="6eca0-175">iconUrl is deprecated.</span></span> <span data-ttu-id="6eca0-176">Use o ícone em vez disso.</span><span class="sxs-lookup"><span data-stu-id="6eca0-176">Use icon instead.</span></span>

<span data-ttu-id="6eca0-177">Uma URL para uma imagem 128x128 com tela de fundo de transparência a ser usada como o ícone para o pacote na exibição da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="6eca0-177">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="6eca0-178">Verifique se esse elemento contém a *URL direta da imagem* e não a URL de uma página da Web que contém a imagem.</span><span class="sxs-lookup"><span data-stu-id="6eca0-178">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="6eca0-179">Por exemplo, para usar uma imagem do GitHub, use a URL do arquivo bruto como <em> https://github.com/ \<username\> / \<repository\> /RAW/ \<branch\> / \<logo.png\> </em>.</span><span class="sxs-lookup"><span data-stu-id="6eca0-179">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 
   
<span data-ttu-id="6eca0-180">Ao carregar um pacote no nuget.org, o `iconUrl` campo é limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6eca0-180">When uploading a package to nuget.org, the `iconUrl` field is limited to 4000 characters.</span></span>

#### <a name="icon"></a><span data-ttu-id="6eca0-181">ícone</span><span class="sxs-lookup"><span data-stu-id="6eca0-181">icon</span></span>

<span data-ttu-id="6eca0-182">*Com suporte com **NuGet 5.3.0** e superior*</span><span class="sxs-lookup"><span data-stu-id="6eca0-182">*Supported with **NuGet 5.3.0** and above*</span></span>

<span data-ttu-id="6eca0-183">É um caminho para um arquivo de imagem dentro do pacote, geralmente mostrado em UIs como nuget.org como o ícone do pacote.</span><span class="sxs-lookup"><span data-stu-id="6eca0-183">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="6eca0-184">O tamanho do arquivo de imagem é limitado a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="6eca0-184">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="6eca0-185">Os formatos de arquivo com suporte incluem JPEG e PNG.</span><span class="sxs-lookup"><span data-stu-id="6eca0-185">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="6eca0-186">Recomendamos uma resolução de imagem de 128x128.</span><span class="sxs-lookup"><span data-stu-id="6eca0-186">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="6eca0-187">Por exemplo, você adicionaria o seguinte ao seu nuspec ao criar um pacote usando nuget.exe:</span><span class="sxs-lookup"><span data-stu-id="6eca0-187">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

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

[<span data-ttu-id="6eca0-188">Ícone de pacote exemplo de nuspec.</span><span class="sxs-lookup"><span data-stu-id="6eca0-188">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/master/PackageIconNuspecExample)

<span data-ttu-id="6eca0-189">Para o equivalente do MSBuild, dê uma olhada no [empacotamento de um arquivo de imagem de ícone](msbuild-targets.md#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="6eca0-189">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="6eca0-190">Você pode especificar o `icon` e o `iconUrl` para manter a compatibilidade com versões anteriores com fontes que não dão suporte ao `icon` .</span><span class="sxs-lookup"><span data-stu-id="6eca0-190">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="6eca0-191">O Visual Studio dará suporte a `icon` pacotes provenientes de uma fonte baseada em pasta em uma versão futura.</span><span class="sxs-lookup"><span data-stu-id="6eca0-191">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="6eca0-192">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="6eca0-192">requireLicenseAcceptance</span></span>
<span data-ttu-id="6eca0-193">Um valor booliano que especifica se o cliente precisa solicitar que o consumidor aceite a licença do pacote antes de instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="6eca0-193">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="6eca0-194">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="6eca0-194">developmentDependency</span></span>
<span data-ttu-id="6eca0-195">*(2.8 ou superior)* Um valor booliano que especifica se o pacote está marcado como uma dependência somente de desenvolvimento, que impede que o pacote seja incluído como uma dependência em outros pacotes.</span><span class="sxs-lookup"><span data-stu-id="6eca0-195">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="6eca0-196">Com PackageReference (NuGet 4.8+), esse sinalizador também significa que ele excluirá os recursos em tempo de compilação.</span><span class="sxs-lookup"><span data-stu-id="6eca0-196">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="6eca0-197">Consulte [suporte do DevelopmentDependency para PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="6eca0-197">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="6eca0-198">resumo</span><span class="sxs-lookup"><span data-stu-id="6eca0-198">summary</span></span>
> [!Important]
> <span data-ttu-id="6eca0-199">`summary` está sendo preterido.</span><span class="sxs-lookup"><span data-stu-id="6eca0-199">`summary` is being deprecated.</span></span> <span data-ttu-id="6eca0-200">Use `description` em vez disso.</span><span class="sxs-lookup"><span data-stu-id="6eca0-200">Use `description` instead.</span></span>

<span data-ttu-id="6eca0-201">Uma breve descrição do pacote para exibição de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="6eca0-201">A short description of the package for UI display.</span></span> <span data-ttu-id="6eca0-202">Se omitido, uma versão truncada do `description` é usada.</span><span class="sxs-lookup"><span data-stu-id="6eca0-202">If omitted, a truncated version of `description` is used.</span></span>

<span data-ttu-id="6eca0-203">Ao carregar um pacote no nuget.org, o `summary` campo é limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6eca0-203">When uploading a package to nuget.org, the `summary` field is limited to 4000 characters.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="6eca0-204">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="6eca0-204">releaseNotes</span></span>
<span data-ttu-id="6eca0-205">*(1.5 ou superior)* Uma descrição das alterações feitas nesta versão do pacote, frequentemente usado na interface do usuário como a guia **Atualizações** do Gerenciador de Pacotes do Visual Studio em vez da descrição do pacote.</span><span class="sxs-lookup"><span data-stu-id="6eca0-205">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

<span data-ttu-id="6eca0-206">Ao carregar um pacote no nuget.org, o `releaseNotes` campo é limitado a 35.000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6eca0-206">When uploading a package to nuget.org, the `releaseNotes` field is limited to 35,000 characters.</span></span>

#### <a name="copyright"></a><span data-ttu-id="6eca0-207">copyright</span><span class="sxs-lookup"><span data-stu-id="6eca0-207">copyright</span></span>
<span data-ttu-id="6eca0-208">*(1.5 ou superior)* Detalhes sobre direitos autorais do pacote.</span><span class="sxs-lookup"><span data-stu-id="6eca0-208">*(1.5+)* Copyright details for the package.</span></span>

<span data-ttu-id="6eca0-209">Ao carregar um pacote no nuget.org, o `copyright` campo é limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6eca0-209">When uploading a package to nuget.org, the `copyright` field is limited to 4000 characters.</span></span>

#### <a name="language"></a><span data-ttu-id="6eca0-210">Linguagem</span><span class="sxs-lookup"><span data-stu-id="6eca0-210">language</span></span>
<span data-ttu-id="6eca0-211">A identificação de localidade para o pacote.</span><span class="sxs-lookup"><span data-stu-id="6eca0-211">The locale ID for the package.</span></span> <span data-ttu-id="6eca0-212">Consulte [Criando pacotes localizados](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="6eca0-212">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="6eca0-213">marcas</span><span class="sxs-lookup"><span data-stu-id="6eca0-213">tags</span></span>
<span data-ttu-id="6eca0-214">Uma lista delimitada por espaço de marcas e palavras-chave que descrevem o pacote e auxiliam na descoberta de pacotes por meio de pesquisa e filtragem.</span><span class="sxs-lookup"><span data-stu-id="6eca0-214">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

<span data-ttu-id="6eca0-215">Ao carregar um pacote no nuget.org, o `tags` campo é limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6eca0-215">When uploading a package to nuget.org, the `tags` field is limited to 4000 characters.</span></span>

#### <a name="serviceable"></a><span data-ttu-id="6eca0-216">serviceable</span><span class="sxs-lookup"><span data-stu-id="6eca0-216">serviceable</span></span> 
<span data-ttu-id="6eca0-217">*(3.3 ou superior)* Somente para uso interno do NuGet.</span><span class="sxs-lookup"><span data-stu-id="6eca0-217">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="6eca0-218">repository</span><span class="sxs-lookup"><span data-stu-id="6eca0-218">repository</span></span>
<span data-ttu-id="6eca0-219">Metadados de repositório, que consistem em quatro atributos opcionais: `type` e `url` *(4.0 +)* e `branch` e `commit` *(4.6 +)*.</span><span class="sxs-lookup"><span data-stu-id="6eca0-219">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="6eca0-220">Esses atributos permitem mapear o `.nupkg` para o repositório que o criou, com o potencial de ser detalhado como o nome do Branch individual e/ou confirmar o hash SHA-1 que criou o pacote.</span><span class="sxs-lookup"><span data-stu-id="6eca0-220">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="6eca0-221">Essa deve ser uma URL disponível publicamente que pode ser invocada diretamente por um software de controle de versão.</span><span class="sxs-lookup"><span data-stu-id="6eca0-221">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="6eca0-222">Ele não deve ser uma página HTML, pois isso é destinado ao computador.</span><span class="sxs-lookup"><span data-stu-id="6eca0-222">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="6eca0-223">Para vincular à página do projeto, use o `projectUrl` campo, em vez disso.</span><span class="sxs-lookup"><span data-stu-id="6eca0-223">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="6eca0-224">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6eca0-224">For example:</span></span>
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

<span data-ttu-id="6eca0-225">Ao carregar um pacote no nuget.org, o `type` atributo é limitado a 100 caracteres e o `url` atributo é limitado a 4000 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6eca0-225">When uploading a package to nuget.org, the `type` attribute is limited to 100 characters and the `url` attribute is limited to 4000 characters.</span></span>

#### <a name="title"></a><span data-ttu-id="6eca0-226">título</span><span class="sxs-lookup"><span data-stu-id="6eca0-226">title</span></span>
<span data-ttu-id="6eca0-227">Um título amigável do pacote que pode ser usado em algumas exibições da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="6eca0-227">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="6eca0-228">(nuget.org e o Gerenciador de pacotes no Visual Studio não mostram título)</span><span class="sxs-lookup"><span data-stu-id="6eca0-228">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

<span data-ttu-id="6eca0-229">Ao carregar um pacote no nuget.org, o `title` campo é limitado a 256 caracteres, mas não é usado para fins de exibição.</span><span class="sxs-lookup"><span data-stu-id="6eca0-229">When uploading a package to nuget.org, the `title` field is limited to 256 characters but is not used for any display purposes.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="6eca0-230">Elementos de coleção</span><span class="sxs-lookup"><span data-stu-id="6eca0-230">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="6eca0-231">packageTypes</span><span class="sxs-lookup"><span data-stu-id="6eca0-231">packageTypes</span></span>
<span data-ttu-id="6eca0-232">*(3.5 ou superior)* Uma coleção de zero ou mais elementos `<packageType>` que especificam o tipo do pacote se for diferente de um pacote de dependência tradicional.</span><span class="sxs-lookup"><span data-stu-id="6eca0-232">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="6eca0-233">Cada packageType tem os atributos de *name* e *version*.</span><span class="sxs-lookup"><span data-stu-id="6eca0-233">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="6eca0-234">Consulte [Definindo um tipo de pacote](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="6eca0-234">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="6eca0-235">dependencies</span><span class="sxs-lookup"><span data-stu-id="6eca0-235">dependencies</span></span>
<span data-ttu-id="6eca0-236">Uma coleção de zero ou mais elementos `<dependency>` que especificam as dependências do pacote.</span><span class="sxs-lookup"><span data-stu-id="6eca0-236">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="6eca0-237">Cada dependência tem atributos de *id*, *version*, *include* (3.x ou superior) e *exclude* (3.x ou superior).</span><span class="sxs-lookup"><span data-stu-id="6eca0-237">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="6eca0-238">Consulte [Dependências](#dependencies-element) abaixo.</span><span class="sxs-lookup"><span data-stu-id="6eca0-238">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="6eca0-239">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="6eca0-239">frameworkAssemblies</span></span>
<span data-ttu-id="6eca0-240">*(1.2 ou superior)* Uma coleção de zero ou mais elementos `<frameworkAssembly>` identifica as referências de assembly do .NET Framework que este pacote requer, o que garante que elas sejam adicionadas aos projetos que consomem o pacote.</span><span class="sxs-lookup"><span data-stu-id="6eca0-240">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="6eca0-241">Cada frameworkAssembly tem os atributos *assemblyName* e *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="6eca0-241">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="6eca0-242">Consulte [Especificando as referências GAC de assembly do framework](#specifying-framework-assembly-references-gac) abaixo.</span><span class="sxs-lookup"><span data-stu-id="6eca0-242">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>
#### <a name="references"></a><span data-ttu-id="6eca0-243">referências</span><span class="sxs-lookup"><span data-stu-id="6eca0-243">references</span></span>
<span data-ttu-id="6eca0-244">*(1.5 ou superior)* Uma coleção de zero ou mais assemblies de nomenclatura de elementos `<reference>` na pasta `lib` do pacote que são adicionados como referências de projeto.</span><span class="sxs-lookup"><span data-stu-id="6eca0-244">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="6eca0-245">Cada referência tem um atributo *file*.</span><span class="sxs-lookup"><span data-stu-id="6eca0-245">Each reference has a *file* attribute.</span></span> <span data-ttu-id="6eca0-246">`<references>` também pode conter um elemento `<group>` com um atributo *targetFramework*, que contém elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-246">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="6eca0-247">Se omitido, todas as referências no `lib` são incluídas.</span><span class="sxs-lookup"><span data-stu-id="6eca0-247">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="6eca0-248">Consulte [Especificando referências de assembly explícitas](#specifying-explicit-assembly-references) abaixo.</span><span class="sxs-lookup"><span data-stu-id="6eca0-248">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="6eca0-249">contentFiles</span><span class="sxs-lookup"><span data-stu-id="6eca0-249">contentFiles</span></span>
<span data-ttu-id="6eca0-250">*(3.3 ou superior)* Uma coleção de elementos `<files>` que identificam os arquivos de conteúdo para incluir o projeto consumidor.</span><span class="sxs-lookup"><span data-stu-id="6eca0-250">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="6eca0-251">Esses arquivos são especificados com um conjunto de atributos que descrevem como eles devem ser usados dentro do sistema de projeto.</span><span class="sxs-lookup"><span data-stu-id="6eca0-251">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="6eca0-252">Consulte [Especificando arquivos a serem incluídos no pacote](#specifying-files-to-include-in-the-package) abaixo.</span><span class="sxs-lookup"><span data-stu-id="6eca0-252">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="6eca0-253">files</span><span class="sxs-lookup"><span data-stu-id="6eca0-253">files</span></span> 
<span data-ttu-id="6eca0-254">O `<package>` nó pode conter um `<files>` nó como um irmão e `<metadata>` um `<contentFiles>` filho em `<metadata>` , para especificar quais arquivos de conteúdo e assembly devem ser incluídos no pacote.</span><span class="sxs-lookup"><span data-stu-id="6eca0-254">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="6eca0-255">Consulte [Incluindo arquivos do assembly](#including-assembly-files) e [Incluindo arquivos de conteúdo](#including-content-files) mais adiante neste tópico para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="6eca0-255">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="6eca0-256">atributos de metadados</span><span class="sxs-lookup"><span data-stu-id="6eca0-256">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="6eca0-257">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="6eca0-257">minClientVersion</span></span>
<span data-ttu-id="6eca0-258">Especifica a versão mínima do cliente NuGet que pode instalar esse pacote, imposta pelo nuget.exe e pelo Gerenciador de Pacotes do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6eca0-258">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="6eca0-259">Isso é usado sempre que o pacote depender de recursos específicos do arquivo `.nuspec` que foram adicionados em uma versão específica do cliente do NuGet.</span><span class="sxs-lookup"><span data-stu-id="6eca0-259">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="6eca0-260">Por exemplo, um pacote usando o atributo `developmentDependency` deve especificar “2.8” para `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-260">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="6eca0-261">Da mesma forma, um pacote usando o elemento `contentFiles` (consulte a próxima seção) deve definir `minClientVersion` para “3.3”.</span><span class="sxs-lookup"><span data-stu-id="6eca0-261">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="6eca0-262">Observe também que, como os clientes do NuGet antes de 2.5 não reconhecem esse sinalizador, eles *sempre* recusam instalar o pacote, não importando o que `minClientVersion` contém.</span><span class="sxs-lookup"><span data-stu-id="6eca0-262">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

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

## <a name="replacement-tokens"></a><span data-ttu-id="6eca0-263">Tokens de substituição</span><span class="sxs-lookup"><span data-stu-id="6eca0-263">Replacement tokens</span></span>

<span data-ttu-id="6eca0-264">Ao criar um pacote, o [ `nuget pack` comando](../reference/cli-reference/cli-ref-pack.md) substitui tokens de $ delimitados no `.nuspec` nó do arquivo `<metadata>` por valores provenientes de um arquivo de projeto ou da `pack` opção do comando `-properties` .</span><span class="sxs-lookup"><span data-stu-id="6eca0-264">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="6eca0-265">Na linha de comando, você especifica os valores de token com `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-265">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="6eca0-266">Por exemplo, você pode usar um token como `$owners$` e `$desc$` no `.nuspec` e fornecer os valores no tempo de empacotamento da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6eca0-266">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="6eca0-267">Para usar valores de um projeto, especifique os tokens descritos na tabela a seguir (AssemblyInfo refere-se ao arquivo em `Properties` como `AssemblyInfo.cs` ou `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="6eca0-267">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="6eca0-268">Para usar esses tokens, execute `nuget pack` com o arquivo de projeto em vez de apenas o `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-268">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="6eca0-269">Por exemplo, ao usar o comando a seguir, os tokens `$id$` e `$version$` em um arquivo `.nuspec` são substituídos pelos valores `AssemblyName` e `AssemblyVersion` do projeto:</span><span class="sxs-lookup"><span data-stu-id="6eca0-269">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="6eca0-270">Normalmente, quando você tem um projeto, você cria o `.nuspec` inicialmente usando `nuget spec MyProject.csproj`, o que inclui alguns desses tokens padrão automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6eca0-270">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="6eca0-271">No entanto, se um projeto não tiver valores para os elementos `.nuspec` necessários, `nuget pack` falhará.</span><span class="sxs-lookup"><span data-stu-id="6eca0-271">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="6eca0-272">Além disso, se você alterar os valores de projeto, lembre-se de recompilá-lo antes de criar o pacote. Isso pode ser feito convenientemente com a opção `build` do comando do pacote.</span><span class="sxs-lookup"><span data-stu-id="6eca0-272">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="6eca0-273">Com exceção de `$configuration$`, os valores do projeto são usados como preferenciais sobre qualquer um com o mesmo token na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="6eca0-273">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="6eca0-274">Token</span><span class="sxs-lookup"><span data-stu-id="6eca0-274">Token</span></span> | <span data-ttu-id="6eca0-275">Origem do valor</span><span class="sxs-lookup"><span data-stu-id="6eca0-275">Value source</span></span> | <span data-ttu-id="6eca0-276">Valor</span><span class="sxs-lookup"><span data-stu-id="6eca0-276">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="6eca0-277">**$id $**</span><span class="sxs-lookup"><span data-stu-id="6eca0-277">**$id$**</span></span> | <span data-ttu-id="6eca0-278">Arquivo de projeto</span><span class="sxs-lookup"><span data-stu-id="6eca0-278">Project file</span></span> | <span data-ttu-id="6eca0-279">AssemblyName (título) do arquivo de projeto</span><span class="sxs-lookup"><span data-stu-id="6eca0-279">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="6eca0-280">**$version $**</span><span class="sxs-lookup"><span data-stu-id="6eca0-280">**$version$**</span></span> | <span data-ttu-id="6eca0-281">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="6eca0-281">AssemblyInfo</span></span> | <span data-ttu-id="6eca0-282">AssemblyInformationalVersion se existir, caso contrário AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="6eca0-282">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="6eca0-283">**$author $**</span><span class="sxs-lookup"><span data-stu-id="6eca0-283">**$author$**</span></span> | <span data-ttu-id="6eca0-284">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="6eca0-284">AssemblyInfo</span></span> | <span data-ttu-id="6eca0-285">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="6eca0-285">AssemblyCompany</span></span> |
| <span data-ttu-id="6eca0-286">**$title $**</span><span class="sxs-lookup"><span data-stu-id="6eca0-286">**$title$**</span></span> | <span data-ttu-id="6eca0-287">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="6eca0-287">AssemblyInfo</span></span> | <span data-ttu-id="6eca0-288">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="6eca0-288">AssemblyTitle</span></span> |
| <span data-ttu-id="6eca0-289">**$description $**</span><span class="sxs-lookup"><span data-stu-id="6eca0-289">**$description$**</span></span> | <span data-ttu-id="6eca0-290">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="6eca0-290">AssemblyInfo</span></span> | <span data-ttu-id="6eca0-291">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="6eca0-291">AssemblyDescription</span></span> |
| <span data-ttu-id="6eca0-292">**$copyright $**</span><span class="sxs-lookup"><span data-stu-id="6eca0-292">**$copyright$**</span></span> | <span data-ttu-id="6eca0-293">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="6eca0-293">AssemblyInfo</span></span> | <span data-ttu-id="6eca0-294">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="6eca0-294">AssemblyCopyright</span></span> |
| <span data-ttu-id="6eca0-295">**$configuration $**</span><span class="sxs-lookup"><span data-stu-id="6eca0-295">**$configuration$**</span></span> | <span data-ttu-id="6eca0-296">DLL de assembly</span><span class="sxs-lookup"><span data-stu-id="6eca0-296">Assembly DLL</span></span> | <span data-ttu-id="6eca0-297">Configuração usada para compilar o assembly, com Depuração como padrão.</span><span class="sxs-lookup"><span data-stu-id="6eca0-297">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="6eca0-298">Observe que, para criar um pacote usando uma configuração de Versão, você sempre usará `-properties Configuration=Release` na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="6eca0-298">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="6eca0-299">Tokens também podem ser usados para resolver caminhos quando você incluir [arquivos do assembly](#including-assembly-files) e [arquivos de conteúdo](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="6eca0-299">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="6eca0-300">Os tokens têm os mesmos nomes que as propriedades do MSBuild, tornando possível selecionar os arquivos a serem incluídos, dependendo da configuração de build atual.</span><span class="sxs-lookup"><span data-stu-id="6eca0-300">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="6eca0-301">Por exemplo, se você usar os seguintes tokens no arquivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="6eca0-301">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="6eca0-302">E você compila um assembly cujo `AssemblyName` é `LoggingLibrary` com a configuração `Release` no MSBuild, as linhas resultantes no arquivo `.nuspec` do pacote são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="6eca0-302">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="6eca0-303">Elemento Dependencies</span><span class="sxs-lookup"><span data-stu-id="6eca0-303">Dependencies element</span></span>

<span data-ttu-id="6eca0-304">O elemento `<dependencies>` dentro do `<metadata>` contém diversos elementos `<dependency>` que identificam os outros pacotes dos quais o pacote de nível superior depende.</span><span class="sxs-lookup"><span data-stu-id="6eca0-304">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="6eca0-305">Os atributos para cada `<dependency>` são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="6eca0-305">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="6eca0-306">Atributo</span><span class="sxs-lookup"><span data-stu-id="6eca0-306">Attribute</span></span> | <span data-ttu-id="6eca0-307">Descrição</span><span class="sxs-lookup"><span data-stu-id="6eca0-307">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="6eca0-308">(Obrigatório) A ID do pacote de dependência, como "EntityFramework" e "NUnit", que é o nome do pacote nuget.org mostrado em uma página do pacote.</span><span class="sxs-lookup"><span data-stu-id="6eca0-308">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="6eca0-309">(Obrigatório) O intervalo de versões aceitáveis como uma dependência.</span><span class="sxs-lookup"><span data-stu-id="6eca0-309">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="6eca0-310">Consulte [Controle de versão do pacote](../concepts/package-versioning.md#version-ranges) para ver a sintaxe exata.</span><span class="sxs-lookup"><span data-stu-id="6eca0-310">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="6eca0-311">Não há suporte para versões flutuantes.</span><span class="sxs-lookup"><span data-stu-id="6eca0-311">Floating versions are not supported.</span></span> |
| <span data-ttu-id="6eca0-312">include</span><span class="sxs-lookup"><span data-stu-id="6eca0-312">include</span></span> | <span data-ttu-id="6eca0-313">Uma lista delimitada por vírgulas de marcas de inclusão/exclusão (veja abaixo) que indicam a dependência a ser incluída no pacote final.</span><span class="sxs-lookup"><span data-stu-id="6eca0-313">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="6eca0-314">O valor padrão é `all`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-314">The default value is `all`.</span></span> |
| <span data-ttu-id="6eca0-315">excluir</span><span class="sxs-lookup"><span data-stu-id="6eca0-315">exclude</span></span> | <span data-ttu-id="6eca0-316">Uma lista delimitada por vírgulas de marcas de inclusão/exclusão (veja abaixo) que indicam a dependência a ser excluída do pacote final.</span><span class="sxs-lookup"><span data-stu-id="6eca0-316">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="6eca0-317">O valor padrão é o `build,analyzers` que pode ser substituído.</span><span class="sxs-lookup"><span data-stu-id="6eca0-317">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="6eca0-318">Mas `content/ ContentFiles` também são excluídos implicitamente no pacote final que não pode ser substituído.</span><span class="sxs-lookup"><span data-stu-id="6eca0-318">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="6eca0-319">Marcas especificadas com `exclude` têm precedência sobre aquelas especificadas com `include`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-319">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="6eca0-320">Por exemplo, `include="runtime, compile" exclude="compile"` é o mesmo que `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-320">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

<span data-ttu-id="6eca0-321">Ao carregar um pacote no nuget.org, cada atributo de dependência `id` é limitado a 128 caracteres e o `version` atributo é limitado a 256 caracteres.</span><span class="sxs-lookup"><span data-stu-id="6eca0-321">When uploading a package to nuget.org, each dependency's `id` attribute is limited to 128 characters and the `version` attribute is limited to 256 characters.</span></span>

| <span data-ttu-id="6eca0-322">Marca Incluir/Excluir</span><span class="sxs-lookup"><span data-stu-id="6eca0-322">Include/Exclude tag</span></span> | <span data-ttu-id="6eca0-323">Pastas afetadas do destino</span><span class="sxs-lookup"><span data-stu-id="6eca0-323">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="6eca0-324">contentFiles</span><span class="sxs-lookup"><span data-stu-id="6eca0-324">contentFiles</span></span> | <span data-ttu-id="6eca0-325">Conteúdo</span><span class="sxs-lookup"><span data-stu-id="6eca0-325">Content</span></span> |
| <span data-ttu-id="6eca0-326">runtime</span><span class="sxs-lookup"><span data-stu-id="6eca0-326">runtime</span></span> | <span data-ttu-id="6eca0-327">Runtime, Resources e FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="6eca0-327">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="6eca0-328">compilar</span><span class="sxs-lookup"><span data-stu-id="6eca0-328">compile</span></span> | <span data-ttu-id="6eca0-329">lib</span><span class="sxs-lookup"><span data-stu-id="6eca0-329">lib</span></span> |
| <span data-ttu-id="6eca0-330">compilar</span><span class="sxs-lookup"><span data-stu-id="6eca0-330">build</span></span> | <span data-ttu-id="6eca0-331">build (objetos e destinos do MSBuild)</span><span class="sxs-lookup"><span data-stu-id="6eca0-331">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="6eca0-332">nativa</span><span class="sxs-lookup"><span data-stu-id="6eca0-332">native</span></span> | <span data-ttu-id="6eca0-333">nativa</span><span class="sxs-lookup"><span data-stu-id="6eca0-333">native</span></span> |
| <span data-ttu-id="6eca0-334">nenhum</span><span class="sxs-lookup"><span data-stu-id="6eca0-334">none</span></span> | <span data-ttu-id="6eca0-335">Nenhuma pasta</span><span class="sxs-lookup"><span data-stu-id="6eca0-335">No folders</span></span> |
| <span data-ttu-id="6eca0-336">all</span><span class="sxs-lookup"><span data-stu-id="6eca0-336">all</span></span> | <span data-ttu-id="6eca0-337">Todas as pastas</span><span class="sxs-lookup"><span data-stu-id="6eca0-337">All folders</span></span> |

<span data-ttu-id="6eca0-338">Por exemplo, as linhas a seguir indicam as dependências no `PackageA` versão 1.1.0 ou superior e `PackageB` versão 1.x.</span><span class="sxs-lookup"><span data-stu-id="6eca0-338">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="6eca0-339">As linhas a seguir indicam dependências nos mesmos pacotes, mas especificam a inclusão de pastas `contentFiles` e `build` de `PackageA` tudo, mas as pastas `native` e `compile` de `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="6eca0-339">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="6eca0-340">Ao criar um `.nuspec` de um projeto usando `nuget spec` , as dependências que existem nesse projeto não são incluídas automaticamente no `.nuspec` arquivo resultante.</span><span class="sxs-lookup"><span data-stu-id="6eca0-340">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="6eca0-341">Em vez disso, use `nuget pack myproject.csproj` e obtenha o arquivo *. nuspec* de dentro do arquivo *. nupkg* gerado.</span><span class="sxs-lookup"><span data-stu-id="6eca0-341">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="6eca0-342">Esse *. nuspec* contém as dependências.</span><span class="sxs-lookup"><span data-stu-id="6eca0-342">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="6eca0-343">Grupos de dependência</span><span class="sxs-lookup"><span data-stu-id="6eca0-343">Dependency groups</span></span>

<span data-ttu-id="6eca0-344">*Versão 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="6eca0-344">*Version 2.0+*</span></span>

<span data-ttu-id="6eca0-345">Como alternativa a uma única lista simples, as dependências podem ser especificadas de acordo com o perfil da estrutura do projeto de destino usando elementos `<group>` dentro de `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-345">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="6eca0-346">Cada grupo tem um atributo chamado `targetFramework` e contém zero ou mais elementos `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-346">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="6eca0-347">Essas referências são instaladas juntas quando a estrutura de destino é compatível com o perfil da estrutura do projeto.</span><span class="sxs-lookup"><span data-stu-id="6eca0-347">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="6eca0-348">O elemento `<group>` sem um atributo `targetFramework` será usado como a lista de dependências padrão ou de fallback.</span><span class="sxs-lookup"><span data-stu-id="6eca0-348">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="6eca0-349">Consulte [Estruturas de destino](../reference/target-frameworks.md) para ver os identificadores de estrutura exatos.</span><span class="sxs-lookup"><span data-stu-id="6eca0-349">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="6eca0-350">O formato do grupo não pode ser combinado com uma lista simples.</span><span class="sxs-lookup"><span data-stu-id="6eca0-350">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="6eca0-351">O formato do [moniker da estrutura de destino (TFM)](../reference/target-frameworks.md) usado na `lib/ref` pasta é diferente quando comparado com o TFM usado em `dependency groups` .</span><span class="sxs-lookup"><span data-stu-id="6eca0-351">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="6eca0-352">Se as estruturas de destino declaradas no `dependencies group` e a `lib/ref` pasta do `.nuspec` arquivo não tiverem correspondências exatas, o `pack` comando emitirá o aviso do [NuGet NU5128](../reference/errors-and-warnings/nu5128.md).</span><span class="sxs-lookup"><span data-stu-id="6eca0-352">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="6eca0-353">O exemplo a seguir mostra diferentes variações do elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="6eca0-353">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="6eca0-354">Referências de assembly explícitas</span><span class="sxs-lookup"><span data-stu-id="6eca0-354">Explicit assembly references</span></span>

<span data-ttu-id="6eca0-355">O `<references>` elemento é usado por projetos `packages.config` que usam para especificar explicitamente os assemblies que o projeto de destino deve referenciar ao usar o pacote.</span><span class="sxs-lookup"><span data-stu-id="6eca0-355">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="6eca0-356">Referências explícitas são geralmente usadas apenas para assemblies de tempo de design.</span><span class="sxs-lookup"><span data-stu-id="6eca0-356">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="6eca0-357">Para obter mais informações, consulte a página sobre como [selecionar assemblies referenciados por projetos](../create-packages/select-assemblies-referenced-by-projects.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="6eca0-357">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="6eca0-358">Por exemplo, o elemento `<references>` a seguir instrui o NuGet a adicionar referências a apenas `xunit.dll` e `xunit.extensions.dll`, mesmo se houver assemblies adicionais no pacote:</span><span class="sxs-lookup"><span data-stu-id="6eca0-358">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="6eca0-359">Grupos de referência</span><span class="sxs-lookup"><span data-stu-id="6eca0-359">Reference groups</span></span>

<span data-ttu-id="6eca0-360">Como alternativa a uma única lista simples, as referências podem ser especificadas de acordo com o perfil da estrutura do projeto de destino usando elementos `<group>` dentro de `<references>`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-360">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="6eca0-361">Cada grupo tem um atributo chamado `targetFramework` e contém zero ou mais elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-361">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="6eca0-362">Essas referências são adicionadas a um projeto quando a estrutura de destino é compatível com o perfil de estrutura do projeto.</span><span class="sxs-lookup"><span data-stu-id="6eca0-362">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="6eca0-363">O elemento `<group>` sem um atributo `targetFramework` será usado como a lista de referências padrão ou de fallback.</span><span class="sxs-lookup"><span data-stu-id="6eca0-363">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="6eca0-364">Consulte [Estruturas de destino](../reference/target-frameworks.md) para ver os identificadores de estrutura exatos.</span><span class="sxs-lookup"><span data-stu-id="6eca0-364">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="6eca0-365">O formato do grupo não pode ser combinado com uma lista simples.</span><span class="sxs-lookup"><span data-stu-id="6eca0-365">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="6eca0-366">O exemplo a seguir mostra diferentes variações do elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="6eca0-366">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="6eca0-367">Referências de assembly de estrutura</span><span class="sxs-lookup"><span data-stu-id="6eca0-367">Framework assembly references</span></span>

<span data-ttu-id="6eca0-368">Assemblies do Framework são aqueles que fazem parte do .NET Framework e já devem estar no GAC (cache de assembly global) para qualquer computador especificado.</span><span class="sxs-lookup"><span data-stu-id="6eca0-368">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="6eca0-369">Ao identificar assemblies dentro do elemento `<frameworkAssemblies>`, um pacote pode garantir que as referências necessárias sejam adicionadas a um projeto caso este já não tenha essas referências.</span><span class="sxs-lookup"><span data-stu-id="6eca0-369">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="6eca0-370">Tais assemblies, obviamente, não são incluídos em um pacote diretamente.</span><span class="sxs-lookup"><span data-stu-id="6eca0-370">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="6eca0-371">O elemento `<frameworkAssemblies>` contém zero ou mais elementos `<frameworkAssembly>`, cada um deles especifica os seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="6eca0-371">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="6eca0-372">Atributo</span><span class="sxs-lookup"><span data-stu-id="6eca0-372">Attribute</span></span> | <span data-ttu-id="6eca0-373">Descrição</span><span class="sxs-lookup"><span data-stu-id="6eca0-373">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6eca0-374">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="6eca0-374">**assemblyName**</span></span> | <span data-ttu-id="6eca0-375">(Obrigatório) O nome totalmente qualificado do assembly.</span><span class="sxs-lookup"><span data-stu-id="6eca0-375">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="6eca0-376">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="6eca0-376">**targetFramework**</span></span> | <span data-ttu-id="6eca0-377">(Opcional) Especifica a estrutura de destino à qual esta referência se aplica.</span><span class="sxs-lookup"><span data-stu-id="6eca0-377">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="6eca0-378">Se omitido, indica que a referência se aplica a todas as estruturas.</span><span class="sxs-lookup"><span data-stu-id="6eca0-378">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="6eca0-379">Consulte [Estruturas de destino](../reference/target-frameworks.md) para ver os identificadores de estrutura exatos.</span><span class="sxs-lookup"><span data-stu-id="6eca0-379">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="6eca0-380">O exemplo a seguir mostra uma referência a `System.Net` todas as estruturas de destino e uma referência a `System.ServiceModel` apenas para o .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="6eca0-380">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="6eca0-381">Incluindo arquivos do assembly</span><span class="sxs-lookup"><span data-stu-id="6eca0-381">Including assembly files</span></span>

<span data-ttu-id="6eca0-382">Se você seguir as convenções descritas em [Criando um pacote](../create-packages/creating-a-package.md), não será necessário especificar explicitamente uma lista de arquivos no arquivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-382">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="6eca0-383">O comando `nuget pack` escolherá automaticamente os arquivos necessários.</span><span class="sxs-lookup"><span data-stu-id="6eca0-383">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="6eca0-384">Quando um pacote é instalado em um projeto, o NuGet adiciona automaticamente as referências de assembly às DLLs do pacote, *excluindo* aquelas que são nomeados `.resources.dll` porque são considerados assemblies satélites.</span><span class="sxs-lookup"><span data-stu-id="6eca0-384">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="6eca0-385">Por esse motivo, evite usar `.resources.dll` para arquivos que contêm código de pacote essencial.</span><span class="sxs-lookup"><span data-stu-id="6eca0-385">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="6eca0-386">Para ignorar esse comportamento automático e controlar explicitamente quais arquivos são incluídos em um pacote, coloque uma elemento `<files>` como um filho de `<package>` (e um irmão de `<metadata>`), identificando cada arquivo com um elemento `<file>` separado.</span><span class="sxs-lookup"><span data-stu-id="6eca0-386">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="6eca0-387">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6eca0-387">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="6eca0-388">Com o NuGet 2.x e anteriores, e em projetos que usam `packages.config`, o elemento `<files>` também é usado para incluir arquivos de conteúdo imutáveis quando um pacote é instalado.</span><span class="sxs-lookup"><span data-stu-id="6eca0-388">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="6eca0-389">Com o NuGet 3.3 ou superior e projetos PackageReference, o elemento `<contentFiles>` é usado.</span><span class="sxs-lookup"><span data-stu-id="6eca0-389">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="6eca0-390">Consulte [Incluindo arquivos de conteúdo](#including-content-files) abaixo para ver os detalhes.</span><span class="sxs-lookup"><span data-stu-id="6eca0-390">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="6eca0-391">Atributos do elemento de arquivo</span><span class="sxs-lookup"><span data-stu-id="6eca0-391">File element attributes</span></span>

<span data-ttu-id="6eca0-392">Cada elemento `<file>` especifica os seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="6eca0-392">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="6eca0-393">Atributo</span><span class="sxs-lookup"><span data-stu-id="6eca0-393">Attribute</span></span> | <span data-ttu-id="6eca0-394">Descrição</span><span class="sxs-lookup"><span data-stu-id="6eca0-394">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6eca0-395">**src**</span><span class="sxs-lookup"><span data-stu-id="6eca0-395">**src**</span></span> | <span data-ttu-id="6eca0-396">O local do arquivo ou arquivos a serem incluídos, sujeito a exclusões especificadas pelo atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-396">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="6eca0-397">O caminho é relativo ao arquivo `.nuspec`, a menos que um caminho absoluto seja especificado.</span><span class="sxs-lookup"><span data-stu-id="6eca0-397">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="6eca0-398">O caractere curinga `*` é permitido e o caractere curinga duplo `**` sugere uma pesquisa de pastas recursiva.</span><span class="sxs-lookup"><span data-stu-id="6eca0-398">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="6eca0-399">**destino**</span><span class="sxs-lookup"><span data-stu-id="6eca0-399">**target**</span></span> | <span data-ttu-id="6eca0-400">O caminho relativo para a pasta dentro do pacote em que os arquivos de origem são colocados, os quais devem começar com `lib`, `content`, `build` ou `tools`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-400">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="6eca0-401">Consulte [Criando um .nuspec de um diretório de trabalho baseado em convenção](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="6eca0-401">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="6eca0-402">**excluir**</span><span class="sxs-lookup"><span data-stu-id="6eca0-402">**exclude**</span></span> | <span data-ttu-id="6eca0-403">Uma lista separada por ponto-e-vírgula de arquivos ou padrões de arquivo para excluir o local `src`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-403">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="6eca0-404">O caractere curinga `*` é permitido e o caractere curinga duplo `**` sugere uma pesquisa de pastas recursiva.</span><span class="sxs-lookup"><span data-stu-id="6eca0-404">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="6eca0-405">Exemplos</span><span class="sxs-lookup"><span data-stu-id="6eca0-405">Examples</span></span>

<span data-ttu-id="6eca0-406">**Assembly único**</span><span class="sxs-lookup"><span data-stu-id="6eca0-406">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="6eca0-407">**Assembly único específico para uma estrutura de destino**</span><span class="sxs-lookup"><span data-stu-id="6eca0-407">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="6eca0-408">**Conjunto de DLLs que usam um caractere curinga**</span><span class="sxs-lookup"><span data-stu-id="6eca0-408">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="6eca0-409">**DLLs de estruturas diferentes**</span><span class="sxs-lookup"><span data-stu-id="6eca0-409">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="6eca0-410">**Excluindo arquivos**</span><span class="sxs-lookup"><span data-stu-id="6eca0-410">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="6eca0-411">Incluindo arquivos de conteúdo</span><span class="sxs-lookup"><span data-stu-id="6eca0-411">Including content files</span></span>

<span data-ttu-id="6eca0-412">Arquivos de conteúdo são arquivos imutáveis que um pacote incluir em um projeto.</span><span class="sxs-lookup"><span data-stu-id="6eca0-412">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="6eca0-413">Sendo imutáveis, eles não foram projetados para serem modificados pelo projeto consumidor.</span><span class="sxs-lookup"><span data-stu-id="6eca0-413">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="6eca0-414">Alguns exemplos de arquivos de conteúdo:</span><span class="sxs-lookup"><span data-stu-id="6eca0-414">Example content files include:</span></span>

- <span data-ttu-id="6eca0-415">Imagens que são inseridas como recursos</span><span class="sxs-lookup"><span data-stu-id="6eca0-415">Images that are embedded as resources</span></span>
- <span data-ttu-id="6eca0-416">Arquivos de origem que já são compilados</span><span class="sxs-lookup"><span data-stu-id="6eca0-416">Source files that are already compiled</span></span>
- <span data-ttu-id="6eca0-417">Scripts que precisam ser incluídos na saída de build do projeto</span><span class="sxs-lookup"><span data-stu-id="6eca0-417">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="6eca0-418">Arquivos de configuração para o pacote que precisam ser incluídos no projeto, mas não precisam de nenhuma alteração específica do projeto</span><span class="sxs-lookup"><span data-stu-id="6eca0-418">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="6eca0-419">Arquivos de conteúdo são incluídos em um pacote usando o elemento `<files>`, especificando a pasta `content` no atributo `target`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-419">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="6eca0-420">No entanto, esses arquivos são ignorados quando o pacote é instalado em um projeto usando PackageReference, que usa o elemento `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-420">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="6eca0-421">Para máxima compatibilidade com projetos de consumo, é ideal que um pacote especifique os arquivos de conteúdo em ambos os elementos.</span><span class="sxs-lookup"><span data-stu-id="6eca0-421">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="6eca0-422">Usando o elemento de arquivos para arquivos de conteúdo</span><span class="sxs-lookup"><span data-stu-id="6eca0-422">Using the files element for content files</span></span>

<span data-ttu-id="6eca0-423">Para arquivos de conteúdo, basta usar o mesmo formato que os arquivos do assembly, porém especifique `content` como a pasta base no atributo `target` conforme mostrado nos exemplos a seguir.</span><span class="sxs-lookup"><span data-stu-id="6eca0-423">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="6eca0-424">**Arquivos de conteúdo básico**</span><span class="sxs-lookup"><span data-stu-id="6eca0-424">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="6eca0-425">**Arquivos de conteúdo com a estrutura de diretório**</span><span class="sxs-lookup"><span data-stu-id="6eca0-425">**Content files with directory structure**</span></span>

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

<span data-ttu-id="6eca0-426">**Arquivo de conteúdo específico para uma estrutura de destino**</span><span class="sxs-lookup"><span data-stu-id="6eca0-426">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="6eca0-427">**Arquivo de conteúdo copiado para uma pasta com ponto no nome**</span><span class="sxs-lookup"><span data-stu-id="6eca0-427">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="6eca0-428">Nesse caso, o NuGet vê que a extensão em `target` não corresponde à extensão em `src` e, portanto, trata essa parte do nome no `target` como uma pasta:</span><span class="sxs-lookup"><span data-stu-id="6eca0-428">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="6eca0-429">**Arquivos de conteúdo sem extensões**</span><span class="sxs-lookup"><span data-stu-id="6eca0-429">**Content files without extensions**</span></span>

<span data-ttu-id="6eca0-430">Para incluir arquivos sem extensão, use os curingas `*` ou `**`:</span><span class="sxs-lookup"><span data-stu-id="6eca0-430">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="6eca0-431">**Arquivos de conteúdo com caminho e destino profundos**</span><span class="sxs-lookup"><span data-stu-id="6eca0-431">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="6eca0-432">Nesse caso, como as extensões de arquivo de origem e de destino correspondem, o NuGet pressupõe que o destino é um nome de arquivo e não uma pasta:</span><span class="sxs-lookup"><span data-stu-id="6eca0-432">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="6eca0-433">**Renomeando um arquivo de conteúdo no pacote**</span><span class="sxs-lookup"><span data-stu-id="6eca0-433">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="6eca0-434">**Excluindo arquivos**</span><span class="sxs-lookup"><span data-stu-id="6eca0-434">**Excluding files**</span></span>

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="6eca0-435">Usando o elemento contentFiles para arquivos de conteúdo</span><span class="sxs-lookup"><span data-stu-id="6eca0-435">Using the contentFiles element for content files</span></span>

<span data-ttu-id="6eca0-436">*NuGet 4.0 e posteriores com PackageReference*</span><span class="sxs-lookup"><span data-stu-id="6eca0-436">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="6eca0-437">Por padrão, um pacote coloca o conteúdo em uma pasta `contentFiles` (veja abaixo) e `nuget pack` incluiu todos os arquivos nessa pasta usando os atributos padrão.</span><span class="sxs-lookup"><span data-stu-id="6eca0-437">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="6eca0-438">Nesse caso, não é necessário incluir um nó `contentFiles` no `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-438">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="6eca0-439">Para controlar quais arquivos são incluídos, o elemento `<contentFiles>` especifica uma coleção de elementos `<files>` que identificam as inclusões dos arquivos exatos.</span><span class="sxs-lookup"><span data-stu-id="6eca0-439">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="6eca0-440">Esses arquivos são especificados com um conjunto de atributos que descrevem como eles devem ser usados dentro do sistema de projeto:</span><span class="sxs-lookup"><span data-stu-id="6eca0-440">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="6eca0-441">Atributo</span><span class="sxs-lookup"><span data-stu-id="6eca0-441">Attribute</span></span> | <span data-ttu-id="6eca0-442">Descrição</span><span class="sxs-lookup"><span data-stu-id="6eca0-442">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6eca0-443">**incluir**</span><span class="sxs-lookup"><span data-stu-id="6eca0-443">**include**</span></span> | <span data-ttu-id="6eca0-444">(Obrigatório) O local do arquivo ou arquivos a serem incluídos, sujeito a exclusões especificadas pelo atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-444">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="6eca0-445">O caminho é relativo à `contentFiles` pasta, a menos que um caminho absoluto seja especificado.</span><span class="sxs-lookup"><span data-stu-id="6eca0-445">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="6eca0-446">O caractere curinga `*` é permitido e o caractere curinga duplo `**` sugere uma pesquisa de pastas recursiva.</span><span class="sxs-lookup"><span data-stu-id="6eca0-446">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="6eca0-447">**excluir**</span><span class="sxs-lookup"><span data-stu-id="6eca0-447">**exclude**</span></span> | <span data-ttu-id="6eca0-448">Uma lista separada por ponto-e-vírgula de arquivos ou padrões de arquivo para excluir o local `src`.</span><span class="sxs-lookup"><span data-stu-id="6eca0-448">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="6eca0-449">O caractere curinga `*` é permitido e o caractere curinga duplo `**` sugere uma pesquisa de pastas recursiva.</span><span class="sxs-lookup"><span data-stu-id="6eca0-449">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="6eca0-450">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="6eca0-450">**buildAction**</span></span> | <span data-ttu-id="6eca0-451">A ação de compilação a ser atribuída ao item de conteúdo para o MSBuild, como,,, `Content` `None` `Embedded Resource` `Compile` etc. O padrão é `Compile` .</span><span class="sxs-lookup"><span data-stu-id="6eca0-451">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="6eca0-452">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="6eca0-452">**copyToOutput**</span></span> | <span data-ttu-id="6eca0-453">Um booliano que indica se os itens de conteúdo devem ser copiados para a pasta de saída Build (ou Publish).</span><span class="sxs-lookup"><span data-stu-id="6eca0-453">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="6eca0-454">O padrão é false.</span><span class="sxs-lookup"><span data-stu-id="6eca0-454">The default is false.</span></span> |
| <span data-ttu-id="6eca0-455">**flatten**</span><span class="sxs-lookup"><span data-stu-id="6eca0-455">**flatten**</span></span> | <span data-ttu-id="6eca0-456">Um valor booliano que indica se os itens de conteúdo devem ser copiados para uma única pasta na saída do build (verdadeiro) ou preservar a estrutura de pasta no pacote (falso).</span><span class="sxs-lookup"><span data-stu-id="6eca0-456">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="6eca0-457">Esse sinalizador só funciona quando o sinalizador copyToOutput está definido como true.</span><span class="sxs-lookup"><span data-stu-id="6eca0-457">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="6eca0-458">O padrão é false.</span><span class="sxs-lookup"><span data-stu-id="6eca0-458">The default is false.</span></span> |

<span data-ttu-id="6eca0-459">Ao instalar um pacote, o NuGet aplicará os elementos filho de `<contentFiles>` de cima para baixo.</span><span class="sxs-lookup"><span data-stu-id="6eca0-459">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="6eca0-460">Se várias entradas corresponderem ao mesmo arquivo, todas as entradas serão aplicadas.</span><span class="sxs-lookup"><span data-stu-id="6eca0-460">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="6eca0-461">A entrada superior substitui as entradas mais baixas em caso de conflito para o mesmo atributo.</span><span class="sxs-lookup"><span data-stu-id="6eca0-461">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="6eca0-462">Estrutura de pastas do pacote</span><span class="sxs-lookup"><span data-stu-id="6eca0-462">Package folder structure</span></span>

<span data-ttu-id="6eca0-463">O projeto do pacote deve estruturar o conteúdo usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="6eca0-463">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="6eca0-464">`codeLanguages` pode ser `cs`, `vb`, `fs`, `any` ou o equivalente em letras minúsculas de determinado `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="6eca0-464">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="6eca0-465">`TxM` é qualquer moniker da estrutura de destino legal compatível com o NuGet (consulte [Estruturas de destino](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="6eca0-465">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="6eca0-466">Qualquer estrutura de pasta pode ser acrescentada ao final dessa sintaxe.</span><span class="sxs-lookup"><span data-stu-id="6eca0-466">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="6eca0-467">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6eca0-467">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="6eca0-468">As pastas vazias podem usar `.` para recusar o fornecimento de conteúdo para certas combinações de idioma e TxM, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6eca0-468">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="6eca0-469">Exemplo da seção contentFiles</span><span class="sxs-lookup"><span data-stu-id="6eca0-469">Example contentFiles section</span></span>

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

## <a name="framework-reference-groups"></a><span data-ttu-id="6eca0-470">Grupos de referência do Framework</span><span class="sxs-lookup"><span data-stu-id="6eca0-470">Framework reference groups</span></span>

<span data-ttu-id="6eca0-471">*Versão 5.1 + wih PackageReference apenas*</span><span class="sxs-lookup"><span data-stu-id="6eca0-471">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="6eca0-472">As referências de estrutura são um conceito do .NET Core que representa estruturas compartilhadas, como WPF ou Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="6eca0-472">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="6eca0-473">Ao especificar uma estrutura compartilhada, o pacote garante que todas as suas dependências de estrutura sejam incluídas no projeto de referência.</span><span class="sxs-lookup"><span data-stu-id="6eca0-473">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="6eca0-474">Cada `<group>` elemento requer um `targetFramework` atributo e zero ou mais `<frameworkReference>` elementos.</span><span class="sxs-lookup"><span data-stu-id="6eca0-474">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="6eca0-475">O exemplo a seguir mostra um nuspec gerado para um projeto do WPF do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="6eca0-475">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="6eca0-476">Observe que a criação manual de nuspecs que contêm referências de estrutura não é recomendada.</span><span class="sxs-lookup"><span data-stu-id="6eca0-476">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="6eca0-477">Em vez disso, considere usar o pacote de [destinos](msbuild-targets.md) , que os inferirá automaticamente do projeto.</span><span class="sxs-lookup"><span data-stu-id="6eca0-477">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="6eca0-478">Arquivos nuspec de exemplo</span><span class="sxs-lookup"><span data-stu-id="6eca0-478">Example nuspec files</span></span>

<span data-ttu-id="6eca0-479">**Um simples `.nuspec` que não especifica dependências ou arquivos**</span><span class="sxs-lookup"><span data-stu-id="6eca0-479">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="6eca0-480">**Um `.nuspec` com dependências**</span><span class="sxs-lookup"><span data-stu-id="6eca0-480">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="6eca0-481">**Um `.nuspec` com arquivos**</span><span class="sxs-lookup"><span data-stu-id="6eca0-481">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="6eca0-482">**Um `.nuspec` com assemblies de estrutura**</span><span class="sxs-lookup"><span data-stu-id="6eca0-482">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="6eca0-483">Neste exemplo, os seguintes itens são instalados em destinos específicos do projeto:</span><span class="sxs-lookup"><span data-stu-id="6eca0-483">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="6eca0-484">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="6eca0-484">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="6eca0-485">Perfil de Cliente do .NET4 -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="6eca0-485">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="6eca0-486">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="6eca0-486">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="6eca0-487">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="6eca0-487">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
