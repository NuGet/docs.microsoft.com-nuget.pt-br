---
title: Referência de arquivo. nuspec para NuGet
description: O arquivo .nuspec contém metadados de pacote usados ao compilar um pacote e para fornecer informações para os consumidores do pacote.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6bd730db16d8e8783f0d949bb04cf3b52c642cd0
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380549"
---
# <a name="nuspec-reference"></a><span data-ttu-id="57cc4-103">Referência do .nuspec</span><span class="sxs-lookup"><span data-stu-id="57cc4-103">.nuspec reference</span></span>

<span data-ttu-id="57cc4-104">Um arquivo `.nuspec` é um manifesto XML que contém metadados do pacote.</span><span class="sxs-lookup"><span data-stu-id="57cc4-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="57cc4-105">Esse manifesto é usado para compilar o pacote e fornecer informações aos consumidores.</span><span class="sxs-lookup"><span data-stu-id="57cc4-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="57cc4-106">O manifesto sempre é incluído em um pacote.</span><span class="sxs-lookup"><span data-stu-id="57cc4-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="57cc4-107">Neste tópico:</span><span class="sxs-lookup"><span data-stu-id="57cc4-107">In this topic:</span></span>

- [<span data-ttu-id="57cc4-108">Formato e esquema geral</span><span class="sxs-lookup"><span data-stu-id="57cc4-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="57cc4-109">[Tokens de substituição](#replacement-tokens) (quando usados com um projeto do Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="57cc4-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="57cc4-110">Dependências</span><span class="sxs-lookup"><span data-stu-id="57cc4-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="57cc4-111">Referências de assembly explícitas</span><span class="sxs-lookup"><span data-stu-id="57cc4-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="57cc4-112">Referências de assembly de estrutura</span><span class="sxs-lookup"><span data-stu-id="57cc4-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="57cc4-113">Incluindo arquivos do assembly</span><span class="sxs-lookup"><span data-stu-id="57cc4-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="57cc4-114">Incluindo arquivos de conteúdo</span><span class="sxs-lookup"><span data-stu-id="57cc4-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="57cc4-115">Arquivos nuspec de exemplo</span><span class="sxs-lookup"><span data-stu-id="57cc4-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="57cc4-116">Compatibilidade de tipo de projeto</span><span class="sxs-lookup"><span data-stu-id="57cc4-116">Project type compatibility</span></span>

- <span data-ttu-id="57cc4-117">Use `.nuspec` com `nuget.exe pack` para projetos de estilo não-SDK que usam `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="57cc4-118">Um arquivo `.nuspec` não é necessário para criar pacotes para [projetos em estilo SDK](../resources/check-project-format.md) (normalmente .NET Core e .net Standard projetos que usam o [atributo SDK](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="57cc4-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="57cc4-119">(Observe que um `.nuspec` é gerado quando você cria o pacote.)</span><span class="sxs-lookup"><span data-stu-id="57cc4-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="57cc4-120">Se você estiver criando um pacote usando `dotnet.exe pack` ou `msbuild pack target`, é recomendável [incluir todas as propriedades](../reference/msbuild-targets.md#pack-target) que geralmente estão no arquivo `.nuspec` no arquivo de projeto em vez disso.</span><span class="sxs-lookup"><span data-stu-id="57cc4-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="57cc4-121">No entanto, em vez disso, você pode optar por [usar um arquivo `.nuspec` para empacotar usando `dotnet.exe` ou `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="57cc4-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="57cc4-122">Para projetos migrados do `packages.config` para [PackageReference](../consume-packages/package-references-in-project-files.md), um arquivo `.nuspec` não é necessário para criar o pacote.</span><span class="sxs-lookup"><span data-stu-id="57cc4-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="57cc4-123">Em vez disso, use o [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="57cc4-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="57cc4-124">Formato e esquema geral</span><span class="sxs-lookup"><span data-stu-id="57cc4-124">General form and schema</span></span>

<span data-ttu-id="57cc4-125">O arquivo de esquema `nuspec.xsd` atual pode ser encontrado no [repositório GitHub do NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="57cc4-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="57cc4-126">Dentro desse esquema, um arquivo `.nuspec` tem o seguinte formato geral:</span><span class="sxs-lookup"><span data-stu-id="57cc4-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="57cc4-127">Para obter uma representação visual do esquema, abra o arquivo de esquema no Visual Studio no modo de Design e clique no link **Gerenciador de Esquema XML**.</span><span class="sxs-lookup"><span data-stu-id="57cc4-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="57cc4-128">Como alternativa, abra o arquivo como código, clique com o botão direito do mouse no editor e selecione **Mostrar Gerenciador de Esquema XML**.</span><span class="sxs-lookup"><span data-stu-id="57cc4-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="57cc4-129">De qualquer forma, você receberá uma exibição como a mostrada abaixo (quando expandido):</span><span class="sxs-lookup"><span data-stu-id="57cc4-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Gerenciador de Esquema do Visual Studio com o nuspec.xsd aberto](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="57cc4-131">Elementos de metadados necessários</span><span class="sxs-lookup"><span data-stu-id="57cc4-131">Required metadata elements</span></span>

<span data-ttu-id="57cc4-132">Embora os elementos a seguir sejam os requisitos mínimos para um pacote, considere adicionar os [elementos de metadados opcionais](#optional-metadata-elements) para melhorar a experiência geral que os desenvolvedores têm com o pacote.</span><span class="sxs-lookup"><span data-stu-id="57cc4-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="57cc4-133">Esses elementos precisam aparecer dentro de um elemento `<metadata>`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="57cc4-134">id</span><span class="sxs-lookup"><span data-stu-id="57cc4-134">id</span></span> 
<span data-ttu-id="57cc4-135">O identificador de pacote que não diferencia maiúsculas de minúsculas, o qual deve ser exclusivo no nuget.org ou em qualquer galeria na qual o pacote reside.</span><span class="sxs-lookup"><span data-stu-id="57cc4-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="57cc4-136">IDs podem não conter espaços nem caracteres que não sejam válidos para uma URL e geralmente seguem as regras de namespace do .NET.</span><span class="sxs-lookup"><span data-stu-id="57cc4-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="57cc4-137">Consulte [Escolhendo um identificador de pacote exclusivo](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) para ver diretrizes.</span><span class="sxs-lookup"><span data-stu-id="57cc4-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="57cc4-138">version</span><span class="sxs-lookup"><span data-stu-id="57cc4-138">version</span></span>
<span data-ttu-id="57cc4-139">A versão do pacote, seguindo o padrão *principal.secundária.patch*.</span><span class="sxs-lookup"><span data-stu-id="57cc4-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="57cc4-140">Os números de versão podem incluir um sufixo de pré-lançamento, conforme descrito em [Controle de versões de pré-lançamento](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="57cc4-140">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="57cc4-141">descrição</span><span class="sxs-lookup"><span data-stu-id="57cc4-141">description</span></span>
<span data-ttu-id="57cc4-142">Uma descrição do pacote para exibição da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="57cc4-142">A description of the package for UI display.</span></span>
#### <a name="authors"></a><span data-ttu-id="57cc4-143">authors</span><span class="sxs-lookup"><span data-stu-id="57cc4-143">authors</span></span>
<span data-ttu-id="57cc4-144">Uma lista separada por vírgulas de autores de pacotes, que correspondem aos nomes de perfil em nuget.org. Eles são exibidos na galeria do NuGet em nuget.org e são usados para fazer referência cruzada de pacotes pelos mesmos autores.</span><span class="sxs-lookup"><span data-stu-id="57cc4-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="57cc4-145">Elementos de metadados opcionais</span><span class="sxs-lookup"><span data-stu-id="57cc4-145">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="57cc4-146">owners</span><span class="sxs-lookup"><span data-stu-id="57cc4-146">owners</span></span>
<span data-ttu-id="57cc4-147">Uma lista separada por vírgulas dos criadores de pacote usando nomes de perfil em nuget.org. Geralmente, essa é a mesma lista que no `authors` e é ignorada ao carregar o pacote em nuget.org. Consulte [Gerenciando proprietários de pacotes em NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="57cc4-147">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="57cc4-148">projectUrl</span><span class="sxs-lookup"><span data-stu-id="57cc4-148">projectUrl</span></span>
<span data-ttu-id="57cc4-149">Uma URL para a home page do pacote, geralmente mostrada em exibições de interface do usuário, bem como em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="57cc4-149">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

#### <a name="licenseurl"></a><span data-ttu-id="57cc4-150">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="57cc4-150">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="57cc4-151">licenseUrl foi preterido.</span><span class="sxs-lookup"><span data-stu-id="57cc4-151">licenseUrl is deprecated.</span></span> <span data-ttu-id="57cc4-152">Use a licença em vez disso.</span><span class="sxs-lookup"><span data-stu-id="57cc4-152">Use license instead.</span></span>

<span data-ttu-id="57cc4-153">Uma URL para a licença do pacote, geralmente mostrada em interfaces do tipo nuget.org.</span><span class="sxs-lookup"><span data-stu-id="57cc4-153">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

#### <a name="license"></a><span data-ttu-id="57cc4-154">carteira</span><span class="sxs-lookup"><span data-stu-id="57cc4-154">license</span></span>
<span data-ttu-id="57cc4-155">Uma expressão de licença SPDX ou um caminho para um arquivo de licença dentro do pacote, geralmente mostrado em interfaces de grupo como nuget.org. Se você estiver licenciando o pacote em uma licença comum, como MIT ou BSD-2-cláusula, use o [identificador de licença SPDX](https://spdx.org/licenses/)associado.</span><span class="sxs-lookup"><span data-stu-id="57cc4-155">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="57cc4-156">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="57cc4-156">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="57cc4-157">O NuGet.org só aceita expressões de licença que são aprovadas pela iniciativa de software livre ou pela base de softwares gratuita.</span><span class="sxs-lookup"><span data-stu-id="57cc4-157">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="57cc4-158">Se o pacote for licenciado sob várias licenças comuns, você poderá especificar uma licença composta usando a [sintaxe de expressão SPDX versão 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="57cc4-158">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="57cc4-159">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="57cc4-159">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="57cc4-160">Se você usar uma licença personalizada que não é suportada por expressões de licença, poderá empacotar um arquivo `.txt` ou `.md` com o texto da licença.</span><span class="sxs-lookup"><span data-stu-id="57cc4-160">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="57cc4-161">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="57cc4-161">For example:</span></span>

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

<span data-ttu-id="57cc4-162">Para o equivalente do MSBuild, dê uma olhada no [empacotamento de uma expressão de licença ou um arquivo de licença](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="57cc4-162">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="57cc4-163">A sintaxe exata das expressões de licença do NuGet é descrita abaixo em [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="57cc4-163">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="57cc4-164">iconUrl</span><span class="sxs-lookup"><span data-stu-id="57cc4-164">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="57cc4-165">iconUrl foi preterido.</span><span class="sxs-lookup"><span data-stu-id="57cc4-165">iconUrl is deprecated.</span></span> <span data-ttu-id="57cc4-166">Use o ícone em vez disso.</span><span class="sxs-lookup"><span data-stu-id="57cc4-166">Use icon instead.</span></span>

<span data-ttu-id="57cc4-167">Uma URL para uma imagem 64x64 com a tela de fundo transparente a ser usada como o ícone do pacote na exibição de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="57cc4-167">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="57cc4-168">Verifique se esse elemento contém a *URL direta da imagem* e não a URL de uma página da Web que contém a imagem.</span><span class="sxs-lookup"><span data-stu-id="57cc4-168">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="57cc4-169">Por exemplo, para usar uma imagem do GitHub, use a URL do arquivo bruto como <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="57cc4-169">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 
   
#### <a name="icon"></a><span data-ttu-id="57cc4-170">Cone</span><span class="sxs-lookup"><span data-stu-id="57cc4-170">icon</span></span>

<span data-ttu-id="57cc4-171">É um caminho para um arquivo de imagem dentro do pacote, geralmente mostrado em UIs como nuget.org como o ícone do pacote.</span><span class="sxs-lookup"><span data-stu-id="57cc4-171">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="57cc4-172">O tamanho do arquivo de imagem é limitado a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="57cc4-172">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="57cc4-173">Os formatos de arquivo com suporte incluem JPEG e PNG.</span><span class="sxs-lookup"><span data-stu-id="57cc4-173">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="57cc4-174">Recomendamos uma resoulution de imagem de 64 x 64.</span><span class="sxs-lookup"><span data-stu-id="57cc4-174">We recommend an image resoulution of 64x64.</span></span>

<span data-ttu-id="57cc4-175">Por exemplo, você adicionaria o seguinte ao seu nuspec ao criar um pacote usando NuGet. exe:</span><span class="sxs-lookup"><span data-stu-id="57cc4-175">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

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

[<span data-ttu-id="57cc4-176">Ícone de pacote exemplo de nuspec.</span><span class="sxs-lookup"><span data-stu-id="57cc4-176">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/master/PackageIconNuspecExample)

<span data-ttu-id="57cc4-177">Para o equivalente do MSBuild, dê uma olhada no [empacotamento de um arquivo de imagem de ícone](msbuild-targets.md#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="57cc4-177">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="57cc4-178">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="57cc4-178">requireLicenseAcceptance</span></span>
<span data-ttu-id="57cc4-179">Um valor booliano que especifica se o cliente precisa solicitar que o consumidor aceite a licença do pacote antes de instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="57cc4-179">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="57cc4-180">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="57cc4-180">developmentDependency</span></span>
<span data-ttu-id="57cc4-181">*(2.8 ou superior)* Um valor booliano que especifica se o pacote está marcado como uma dependência somente de desenvolvimento, que impede que o pacote seja incluído como uma dependência em outros pacotes.</span><span class="sxs-lookup"><span data-stu-id="57cc4-181">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="57cc4-182">Com PackageReference (NuGet 4.8 +), esse sinalizador também significa que ele excluirá os ativos de tempo de compilação da compilação.</span><span class="sxs-lookup"><span data-stu-id="57cc4-182">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="57cc4-183">Consulte [suporte do DevelopmentDependency para PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="57cc4-183">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="57cc4-184">resumo</span><span class="sxs-lookup"><span data-stu-id="57cc4-184">summary</span></span>
> [!Important]
> <span data-ttu-id="57cc4-185">`summary` está sendo preterido.</span><span class="sxs-lookup"><span data-stu-id="57cc4-185">`summary` is being deprecated.</span></span> <span data-ttu-id="57cc4-186">Use `description` em seu lugar.</span><span class="sxs-lookup"><span data-stu-id="57cc4-186">Use `description` instead.</span></span>

<span data-ttu-id="57cc4-187">Uma breve descrição do pacote para exibição de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="57cc4-187">A short description of the package for UI display.</span></span> <span data-ttu-id="57cc4-188">Se omitido, uma versão truncada do `description` é usada.</span><span class="sxs-lookup"><span data-stu-id="57cc4-188">If omitted, a truncated version of `description` is used.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="57cc4-189">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="57cc4-189">releaseNotes</span></span>
<span data-ttu-id="57cc4-190">*(1.5 ou superior)* Uma descrição das alterações feitas nesta versão do pacote, frequentemente usado na interface do usuário como a guia **Atualizações** do Gerenciador de Pacotes do Visual Studio em vez da descrição do pacote.</span><span class="sxs-lookup"><span data-stu-id="57cc4-190">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

#### <a name="copyright"></a><span data-ttu-id="57cc4-191">direitos autorais</span><span class="sxs-lookup"><span data-stu-id="57cc4-191">copyright</span></span>
<span data-ttu-id="57cc4-192">*(1.5 ou superior)* Detalhes sobre direitos autorais do pacote.</span><span class="sxs-lookup"><span data-stu-id="57cc4-192">*(1.5+)* Copyright details for the package.</span></span>

#### <a name="language"></a><span data-ttu-id="57cc4-193">linguagem</span><span class="sxs-lookup"><span data-stu-id="57cc4-193">language</span></span>
<span data-ttu-id="57cc4-194">A identificação de localidade para o pacote.</span><span class="sxs-lookup"><span data-stu-id="57cc4-194">The locale ID for the package.</span></span> <span data-ttu-id="57cc4-195">Consulte [Criando pacotes localizados](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="57cc4-195">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="57cc4-196">marcações</span><span class="sxs-lookup"><span data-stu-id="57cc4-196">tags</span></span>
<span data-ttu-id="57cc4-197">Uma lista delimitada por espaço de marcas e palavras-chave que descrevem o pacote e auxiliam na descoberta de pacotes por meio de pesquisa e filtragem.</span><span class="sxs-lookup"><span data-stu-id="57cc4-197">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

#### <a name="serviceable"></a><span data-ttu-id="57cc4-198">peça operada pelo</span><span class="sxs-lookup"><span data-stu-id="57cc4-198">serviceable</span></span> 
<span data-ttu-id="57cc4-199">*(3.3 ou superior)* Somente para uso interno do NuGet.</span><span class="sxs-lookup"><span data-stu-id="57cc4-199">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="57cc4-200">repositório</span><span class="sxs-lookup"><span data-stu-id="57cc4-200">repository</span></span>
<span data-ttu-id="57cc4-201">Metadados de repositório, que consistem em quatro atributos opcionais: `type` e `url` *(4.0 +)* e `branch` e `commit` *(4.6 +)* .</span><span class="sxs-lookup"><span data-stu-id="57cc4-201">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="57cc4-202">Esses atributos permitem mapear o `.nupkg` para o repositório que o criou, com o potencial de ser detalhado como o nome da ramificação individual e/ou confirmar o hash SHA-1 que criou o pacote.</span><span class="sxs-lookup"><span data-stu-id="57cc4-202">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="57cc4-203">Essa deve ser uma URL disponível publicamente que pode ser invocada diretamente por um software de controle de versão.</span><span class="sxs-lookup"><span data-stu-id="57cc4-203">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="57cc4-204">Ele não deve ser uma página HTML, pois isso é destinado ao computador.</span><span class="sxs-lookup"><span data-stu-id="57cc4-204">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="57cc4-205">Para vincular à página do projeto, use o campo `projectUrl`, em vez disso.</span><span class="sxs-lookup"><span data-stu-id="57cc4-205">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="57cc4-206">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="57cc4-206">For example:</span></span>
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2016/06/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

#### <a name="title"></a><span data-ttu-id="57cc4-207">título</span><span class="sxs-lookup"><span data-stu-id="57cc4-207">title</span></span>
<span data-ttu-id="57cc4-208">Um título amigável do pacote que pode ser usado em algumas exibições da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="57cc4-208">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="57cc4-209">(nuget.org e o Gerenciador de pacotes no Visual Studio não mostram título)</span><span class="sxs-lookup"><span data-stu-id="57cc4-209">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="57cc4-210">Elementos de coleção</span><span class="sxs-lookup"><span data-stu-id="57cc4-210">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="57cc4-211">packageTypes</span><span class="sxs-lookup"><span data-stu-id="57cc4-211">packageTypes</span></span>
<span data-ttu-id="57cc4-212">*(3.5 ou superior)* Uma coleção de zero ou mais elementos `<packageType>` que especificam o tipo do pacote se for diferente de um pacote de dependência tradicional.</span><span class="sxs-lookup"><span data-stu-id="57cc4-212">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="57cc4-213">Cada packageType tem os atributos de *name* e *version*.</span><span class="sxs-lookup"><span data-stu-id="57cc4-213">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="57cc4-214">Consulte [Definindo um tipo de pacote](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="57cc4-214">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="57cc4-215">dependências</span><span class="sxs-lookup"><span data-stu-id="57cc4-215">dependencies</span></span>
<span data-ttu-id="57cc4-216">Uma coleção de zero ou mais elementos `<dependency>` que especificam as dependências do pacote.</span><span class="sxs-lookup"><span data-stu-id="57cc4-216">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="57cc4-217">Cada dependência tem atributos de *id*, *version*, *include* (3.x ou superior) e *exclude* (3.x ou superior).</span><span class="sxs-lookup"><span data-stu-id="57cc4-217">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="57cc4-218">Consulte [Dependências](#dependencies-element) abaixo.</span><span class="sxs-lookup"><span data-stu-id="57cc4-218">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="57cc4-219">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="57cc4-219">frameworkAssemblies</span></span>
<span data-ttu-id="57cc4-220">*(1.2 ou superior)* Uma coleção de zero ou mais elementos `<frameworkAssembly>` identifica as referências de assembly do .NET Framework que este pacote requer, o que garante que elas sejam adicionadas aos projetos que consomem o pacote.</span><span class="sxs-lookup"><span data-stu-id="57cc4-220">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="57cc4-221">Cada frameworkAssembly tem os atributos *assemblyName* e *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="57cc4-221">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="57cc4-222">Consulte [Especificando as referências GAC de assembly do framework](#specifying-framework-assembly-references-gac) abaixo.</span><span class="sxs-lookup"><span data-stu-id="57cc4-222">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>
#### <a name="references"></a><span data-ttu-id="57cc4-223">referências</span><span class="sxs-lookup"><span data-stu-id="57cc4-223">references</span></span>
<span data-ttu-id="57cc4-224">*(1.5 ou superior)* Uma coleção de zero ou mais assemblies de nomenclatura de elementos `<reference>` na pasta `lib` do pacote que são adicionados como referências de projeto.</span><span class="sxs-lookup"><span data-stu-id="57cc4-224">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="57cc4-225">Cada referência tem um atributo *file*.</span><span class="sxs-lookup"><span data-stu-id="57cc4-225">Each reference has a *file* attribute.</span></span> <span data-ttu-id="57cc4-226">`<references>` também pode conter um elemento `<group>` com um atributo *targetFramework*, que contém elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-226">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="57cc4-227">Se omitido, todas as referências no `lib` são incluídas.</span><span class="sxs-lookup"><span data-stu-id="57cc4-227">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="57cc4-228">Consulte [Especificando referências de assembly explícitas](#specifying-explicit-assembly-references) abaixo.</span><span class="sxs-lookup"><span data-stu-id="57cc4-228">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="57cc4-229">contentFiles</span><span class="sxs-lookup"><span data-stu-id="57cc4-229">contentFiles</span></span>
<span data-ttu-id="57cc4-230">*(3.3 ou superior)* Uma coleção de elementos `<files>` que identificam os arquivos de conteúdo para incluir o projeto consumidor.</span><span class="sxs-lookup"><span data-stu-id="57cc4-230">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="57cc4-231">Esses arquivos são especificados com um conjunto de atributos que descrevem como eles devem ser usados dentro do sistema de projeto.</span><span class="sxs-lookup"><span data-stu-id="57cc4-231">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="57cc4-232">Consulte [Especificando arquivos a serem incluídos no pacote](#specifying-files-to-include-in-the-package) abaixo.</span><span class="sxs-lookup"><span data-stu-id="57cc4-232">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="57cc4-233">arquivos</span><span class="sxs-lookup"><span data-stu-id="57cc4-233">files</span></span> 
<span data-ttu-id="57cc4-234">O nó `<package>` pode conter um nó `<files>` como um irmão para `<metadata>` e um filho `<contentFiles>` em `<metadata>`, para especificar quais arquivos de assembly e conteúdo devem ser incluídos no pacote.</span><span class="sxs-lookup"><span data-stu-id="57cc4-234">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="57cc4-235">Consulte [Incluindo arquivos do assembly](#including-assembly-files) e [Incluindo arquivos de conteúdo](#including-content-files) mais adiante neste tópico para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="57cc4-235">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="57cc4-236">atributos de metadados</span><span class="sxs-lookup"><span data-stu-id="57cc4-236">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="57cc4-237">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="57cc4-237">minClientVersion</span></span>
<span data-ttu-id="57cc4-238">Especifica a versão mínima do cliente NuGet que pode instalar esse pacote, imposta pelo nuget.exe e pelo Gerenciador de Pacotes do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="57cc4-238">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="57cc4-239">Isso é usado sempre que o pacote depender de recursos específicos do arquivo `.nuspec` que foram adicionados em uma versão específica do cliente do NuGet.</span><span class="sxs-lookup"><span data-stu-id="57cc4-239">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="57cc4-240">Por exemplo, um pacote usando o atributo `developmentDependency` deve especificar “2.8” para `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-240">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="57cc4-241">Da mesma forma, um pacote usando o elemento `contentFiles` (consulte a próxima seção) deve definir `minClientVersion` para “3.3”.</span><span class="sxs-lookup"><span data-stu-id="57cc4-241">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="57cc4-242">Observe também que, como os clientes do NuGet antes de 2.5 não reconhecem esse sinalizador, eles *sempre* recusam instalar o pacote, não importando o que `minClientVersion` contém.</span><span class="sxs-lookup"><span data-stu-id="57cc4-242">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/01/nuspec.xsd">
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

## <a name="replacement-tokens"></a><span data-ttu-id="57cc4-243">Tokens de substituição</span><span class="sxs-lookup"><span data-stu-id="57cc4-243">Replacement tokens</span></span>

<span data-ttu-id="57cc4-244">Ao criar um pacote, o comando [`nuget pack`](../reference/cli-reference/cli-ref-pack.md) substitui tokens delimitados por $ no nó `<metadata>` do arquivo `.nuspec` com valores que vêm de um arquivo de projeto ou a opção `-properties` do comando `pack`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-244">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="57cc4-245">Na linha de comando, você especifica os valores de token com `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-245">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="57cc4-246">Por exemplo, você pode usar um token como `$owners$` e `$desc$` no `.nuspec` e fornecer os valores no tempo de empacotamento da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="57cc4-246">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="57cc4-247">Para usar valores de um projeto, especifique os tokens descritos na tabela a seguir (AssemblyInfo refere-se ao arquivo em `Properties` como `AssemblyInfo.cs` ou `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="57cc4-247">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="57cc4-248">Para usar esses tokens, execute `nuget pack` com o arquivo de projeto em vez de apenas o `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-248">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="57cc4-249">Por exemplo, ao usar o comando a seguir, os tokens `$id$` e `$version$` em um arquivo `.nuspec` são substituídos pelos valores `AssemblyName` e `AssemblyVersion` do projeto:</span><span class="sxs-lookup"><span data-stu-id="57cc4-249">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="57cc4-250">Normalmente, quando você tem um projeto, você cria o `.nuspec` inicialmente usando `nuget spec MyProject.csproj`, o que inclui alguns desses tokens padrão automaticamente.</span><span class="sxs-lookup"><span data-stu-id="57cc4-250">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="57cc4-251">No entanto, se um projeto não tiver valores para os elementos `.nuspec` necessários, `nuget pack` falhará.</span><span class="sxs-lookup"><span data-stu-id="57cc4-251">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="57cc4-252">Além disso, se você alterar os valores de projeto, lembre-se de recompilá-lo antes de criar o pacote. Isso pode ser feito convenientemente com a opção `build` do comando do pacote.</span><span class="sxs-lookup"><span data-stu-id="57cc4-252">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="57cc4-253">Com exceção de `$configuration$`, os valores do projeto são usados como preferenciais sobre qualquer um com o mesmo token na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="57cc4-253">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="57cc4-254">Token</span><span class="sxs-lookup"><span data-stu-id="57cc4-254">Token</span></span> | <span data-ttu-id="57cc4-255">Origem do valor</span><span class="sxs-lookup"><span data-stu-id="57cc4-255">Value source</span></span> | <span data-ttu-id="57cc4-256">Valor</span><span class="sxs-lookup"><span data-stu-id="57cc4-256">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="57cc4-257">**$id$**</span><span class="sxs-lookup"><span data-stu-id="57cc4-257">**$id$**</span></span> | <span data-ttu-id="57cc4-258">Arquivo de projeto</span><span class="sxs-lookup"><span data-stu-id="57cc4-258">Project file</span></span> | <span data-ttu-id="57cc4-259">AssemblyName (título) do arquivo de projeto</span><span class="sxs-lookup"><span data-stu-id="57cc4-259">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="57cc4-260">**$version$**</span><span class="sxs-lookup"><span data-stu-id="57cc4-260">**$version$**</span></span> | <span data-ttu-id="57cc4-261">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="57cc4-261">AssemblyInfo</span></span> | <span data-ttu-id="57cc4-262">AssemblyInformationalVersion se existir, caso contrário AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="57cc4-262">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="57cc4-263">**$author$**</span><span class="sxs-lookup"><span data-stu-id="57cc4-263">**$author$**</span></span> | <span data-ttu-id="57cc4-264">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="57cc4-264">AssemblyInfo</span></span> | <span data-ttu-id="57cc4-265">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="57cc4-265">AssemblyCompany</span></span> |
| <span data-ttu-id="57cc4-266">**$title $**</span><span class="sxs-lookup"><span data-stu-id="57cc4-266">**$title$**</span></span> | <span data-ttu-id="57cc4-267">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="57cc4-267">AssemblyInfo</span></span> | <span data-ttu-id="57cc4-268">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="57cc4-268">AssemblyTitle</span></span> |
| <span data-ttu-id="57cc4-269">**$description$**</span><span class="sxs-lookup"><span data-stu-id="57cc4-269">**$description$**</span></span> | <span data-ttu-id="57cc4-270">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="57cc4-270">AssemblyInfo</span></span> | <span data-ttu-id="57cc4-271">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="57cc4-271">AssemblyDescription</span></span> |
| <span data-ttu-id="57cc4-272">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="57cc4-272">**$copyright$**</span></span> | <span data-ttu-id="57cc4-273">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="57cc4-273">AssemblyInfo</span></span> | <span data-ttu-id="57cc4-274">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="57cc4-274">AssemblyCopyright</span></span> |
| <span data-ttu-id="57cc4-275">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="57cc4-275">**$configuration$**</span></span> | <span data-ttu-id="57cc4-276">DLL de assembly</span><span class="sxs-lookup"><span data-stu-id="57cc4-276">Assembly DLL</span></span> | <span data-ttu-id="57cc4-277">Configuração usada para compilar o assembly, com Depuração como padrão.</span><span class="sxs-lookup"><span data-stu-id="57cc4-277">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="57cc4-278">Observe que, para criar um pacote usando uma configuração de Versão, você sempre usará `-properties Configuration=Release` na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="57cc4-278">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="57cc4-279">Tokens também podem ser usados para resolver caminhos quando você incluir [arquivos do assembly](#including-assembly-files) e [arquivos de conteúdo](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="57cc4-279">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="57cc4-280">Os tokens têm os mesmos nomes que as propriedades do MSBuild, tornando possível selecionar os arquivos a serem incluídos, dependendo da configuração de build atual.</span><span class="sxs-lookup"><span data-stu-id="57cc4-280">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="57cc4-281">Por exemplo, se você usar os seguintes tokens no arquivo `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="57cc4-281">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="57cc4-282">E você compila um assembly cujo `AssemblyName` é `LoggingLibrary` com a configuração `Release` no MSBuild, as linhas resultantes no arquivo `.nuspec` do pacote são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="57cc4-282">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="57cc4-283">Elemento Dependencies</span><span class="sxs-lookup"><span data-stu-id="57cc4-283">Dependencies element</span></span>

<span data-ttu-id="57cc4-284">O elemento `<dependencies>` dentro do `<metadata>` contém diversos elementos `<dependency>` que identificam os outros pacotes dos quais o pacote de nível superior depende.</span><span class="sxs-lookup"><span data-stu-id="57cc4-284">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="57cc4-285">Os atributos para cada `<dependency>` são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="57cc4-285">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="57cc4-286">Atributo</span><span class="sxs-lookup"><span data-stu-id="57cc4-286">Attribute</span></span> | <span data-ttu-id="57cc4-287">Descrição</span><span class="sxs-lookup"><span data-stu-id="57cc4-287">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="57cc4-288">(Obrigatório) A ID do pacote de dependência, como "EntityFramework" e "NUnit", que é o nome do pacote nuget.org mostrado em uma página do pacote.</span><span class="sxs-lookup"><span data-stu-id="57cc4-288">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="57cc4-289">(Obrigatório) O intervalo de versões aceitáveis como uma dependência.</span><span class="sxs-lookup"><span data-stu-id="57cc4-289">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="57cc4-290">Consulte [Controle de versão do pacote](../concepts/package-versioning.md#version-ranges-and-wildcards) para ver a sintaxe exata.</span><span class="sxs-lookup"><span data-stu-id="57cc4-290">See [Package versioning](../concepts/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> <span data-ttu-id="57cc4-291">Não há suporte para versões curinga (flutuante).</span><span class="sxs-lookup"><span data-stu-id="57cc4-291">Wildcard (floating) versions are not supported.</span></span> |
| <span data-ttu-id="57cc4-292">include</span><span class="sxs-lookup"><span data-stu-id="57cc4-292">include</span></span> | <span data-ttu-id="57cc4-293">Uma lista delimitada por vírgulas de marcas de inclusão/exclusão (veja abaixo) que indicam a dependência a ser incluída no pacote final.</span><span class="sxs-lookup"><span data-stu-id="57cc4-293">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="57cc4-294">O valor padrão é `all`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-294">The default value is `all`.</span></span> |
| <span data-ttu-id="57cc4-295">exclude</span><span class="sxs-lookup"><span data-stu-id="57cc4-295">exclude</span></span> | <span data-ttu-id="57cc4-296">Uma lista delimitada por vírgulas de marcas de inclusão/exclusão (veja abaixo) que indicam a dependência a ser excluída do pacote final.</span><span class="sxs-lookup"><span data-stu-id="57cc4-296">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="57cc4-297">O valor padrão é `build,analyzers`, que pode ser sobrescrito.</span><span class="sxs-lookup"><span data-stu-id="57cc4-297">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="57cc4-298">Mas `content/ ContentFiles` também são excluídos implicitamente no pacote final que não pode ser substituído.</span><span class="sxs-lookup"><span data-stu-id="57cc4-298">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="57cc4-299">Marcas especificadas com `exclude` têm precedência sobre aquelas especificadas com `include`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-299">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="57cc4-300">Por exemplo, `include="runtime, compile" exclude="compile"` é o mesmo que `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-300">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="57cc4-301">Marca Incluir/Excluir</span><span class="sxs-lookup"><span data-stu-id="57cc4-301">Include/Exclude tag</span></span> | <span data-ttu-id="57cc4-302">Pastas afetadas do destino</span><span class="sxs-lookup"><span data-stu-id="57cc4-302">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="57cc4-303">contentFiles</span><span class="sxs-lookup"><span data-stu-id="57cc4-303">contentFiles</span></span> | <span data-ttu-id="57cc4-304">Conteúdo</span><span class="sxs-lookup"><span data-stu-id="57cc4-304">Content</span></span> |
| <span data-ttu-id="57cc4-305">tempo de execução</span><span class="sxs-lookup"><span data-stu-id="57cc4-305">runtime</span></span> | <span data-ttu-id="57cc4-306">Runtime, Resources e FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="57cc4-306">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="57cc4-307">compilar</span><span class="sxs-lookup"><span data-stu-id="57cc4-307">compile</span></span> | <span data-ttu-id="57cc4-308">lib</span><span class="sxs-lookup"><span data-stu-id="57cc4-308">lib</span></span> |
| <span data-ttu-id="57cc4-309">build</span><span class="sxs-lookup"><span data-stu-id="57cc4-309">build</span></span> | <span data-ttu-id="57cc4-310">build (objetos e destinos do MSBuild)</span><span class="sxs-lookup"><span data-stu-id="57cc4-310">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="57cc4-311">nativa</span><span class="sxs-lookup"><span data-stu-id="57cc4-311">native</span></span> | <span data-ttu-id="57cc4-312">nativa</span><span class="sxs-lookup"><span data-stu-id="57cc4-312">native</span></span> |
| <span data-ttu-id="57cc4-313">nenhum</span><span class="sxs-lookup"><span data-stu-id="57cc4-313">none</span></span> | <span data-ttu-id="57cc4-314">Nenhuma pasta</span><span class="sxs-lookup"><span data-stu-id="57cc4-314">No folders</span></span> |
| <span data-ttu-id="57cc4-315">all</span><span class="sxs-lookup"><span data-stu-id="57cc4-315">all</span></span> | <span data-ttu-id="57cc4-316">Todas as pastas</span><span class="sxs-lookup"><span data-stu-id="57cc4-316">All folders</span></span> |

<span data-ttu-id="57cc4-317">Por exemplo, as linhas a seguir indicam as dependências no `PackageA` versão 1.1.0 ou superior e `PackageB` versão 1.x.</span><span class="sxs-lookup"><span data-stu-id="57cc4-317">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="57cc4-318">As linhas a seguir indicam dependências nos mesmos pacotes, mas especificam a inclusão de pastas `contentFiles` e `build` de `PackageA` tudo, mas as pastas `native` e `compile` de `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="57cc4-318">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="57cc4-319">Ao criar um `.nuspec` de um projeto usando `nuget spec`, as dependências que existem nesse projeto não são incluídas automaticamente no arquivo `.nuspec` resultante.</span><span class="sxs-lookup"><span data-stu-id="57cc4-319">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="57cc4-320">Em vez disso, use `nuget pack myproject.csproj` e obtenha o arquivo *. nuspec* de dentro do arquivo *. nupkg* gerado.</span><span class="sxs-lookup"><span data-stu-id="57cc4-320">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="57cc4-321">Esse *. nuspec* contém as dependências.</span><span class="sxs-lookup"><span data-stu-id="57cc4-321">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="57cc4-322">Grupos de dependência</span><span class="sxs-lookup"><span data-stu-id="57cc4-322">Dependency groups</span></span>

<span data-ttu-id="57cc4-323">*Versão 2.0 ou superior*</span><span class="sxs-lookup"><span data-stu-id="57cc4-323">*Version 2.0+*</span></span>

<span data-ttu-id="57cc4-324">Como alternativa a uma única lista simples, as dependências podem ser especificadas de acordo com o perfil da estrutura do projeto de destino usando elementos `<group>` dentro de `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-324">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="57cc4-325">Cada grupo tem um atributo chamado `targetFramework` e contém zero ou mais elementos `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-325">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="57cc4-326">Essas referências são instaladas juntas quando a estrutura de destino é compatível com o perfil da estrutura do projeto.</span><span class="sxs-lookup"><span data-stu-id="57cc4-326">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="57cc4-327">O elemento `<group>` sem um atributo `targetFramework` será usado como a lista de dependências padrão ou de fallback.</span><span class="sxs-lookup"><span data-stu-id="57cc4-327">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="57cc4-328">Consulte [Estruturas de destino](../reference/target-frameworks.md) para ver os identificadores de estrutura exatos.</span><span class="sxs-lookup"><span data-stu-id="57cc4-328">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="57cc4-329">O formato do grupo não pode ser combinado com uma lista simples.</span><span class="sxs-lookup"><span data-stu-id="57cc4-329">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="57cc4-330">O exemplo a seguir mostra diferentes variações do elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="57cc4-330">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="57cc4-331">Referências de assembly explícitas</span><span class="sxs-lookup"><span data-stu-id="57cc4-331">Explicit assembly references</span></span>

<span data-ttu-id="57cc4-332">O elemento `<references>` é usado por projetos que usam `packages.config` para especificar explicitamente os assemblies que o projeto de destino deve referenciar ao usar o pacote.</span><span class="sxs-lookup"><span data-stu-id="57cc4-332">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="57cc4-333">Referências explícitas são geralmente usadas apenas para assemblies de tempo de design.</span><span class="sxs-lookup"><span data-stu-id="57cc4-333">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="57cc4-334">Para obter mais informações, consulte a página sobre como [selecionar assemblies referenciados por projetos](../create-packages/select-assemblies-referenced-by-projects.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="57cc4-334">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="57cc4-335">Por exemplo, o elemento `<references>` a seguir instrui o NuGet a adicionar referências a apenas `xunit.dll` e `xunit.extensions.dll`, mesmo se houver assemblies adicionais no pacote:</span><span class="sxs-lookup"><span data-stu-id="57cc4-335">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="57cc4-336">Grupos de referência</span><span class="sxs-lookup"><span data-stu-id="57cc4-336">Reference groups</span></span>

<span data-ttu-id="57cc4-337">Como alternativa a uma única lista simples, as referências podem ser especificadas de acordo com o perfil da estrutura do projeto de destino usando elementos `<group>` dentro de `<references>`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-337">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="57cc4-338">Cada grupo tem um atributo chamado `targetFramework` e contém zero ou mais elementos `<reference>`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-338">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="57cc4-339">Essas referências são adicionadas a um projeto quando a estrutura de destino é compatível com o perfil de estrutura do projeto.</span><span class="sxs-lookup"><span data-stu-id="57cc4-339">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="57cc4-340">O elemento `<group>` sem um atributo `targetFramework` será usado como a lista de referências padrão ou de fallback.</span><span class="sxs-lookup"><span data-stu-id="57cc4-340">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="57cc4-341">Consulte [Estruturas de destino](../reference/target-frameworks.md) para ver os identificadores de estrutura exatos.</span><span class="sxs-lookup"><span data-stu-id="57cc4-341">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="57cc4-342">O formato do grupo não pode ser combinado com uma lista simples.</span><span class="sxs-lookup"><span data-stu-id="57cc4-342">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="57cc4-343">O exemplo a seguir mostra diferentes variações do elemento `<group>`:</span><span class="sxs-lookup"><span data-stu-id="57cc4-343">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="57cc4-344">Referências de assembly de estrutura</span><span class="sxs-lookup"><span data-stu-id="57cc4-344">Framework assembly references</span></span>

<span data-ttu-id="57cc4-345">Assemblies do Framework são aqueles que fazem parte do .NET Framework e já devem estar no GAC (cache de assembly global) para qualquer computador especificado.</span><span class="sxs-lookup"><span data-stu-id="57cc4-345">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="57cc4-346">Ao identificar assemblies dentro do elemento `<frameworkAssemblies>`, um pacote pode garantir que as referências necessárias sejam adicionadas a um projeto caso este já não tenha essas referências.</span><span class="sxs-lookup"><span data-stu-id="57cc4-346">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="57cc4-347">Tais assemblies, obviamente, não são incluídos em um pacote diretamente.</span><span class="sxs-lookup"><span data-stu-id="57cc4-347">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="57cc4-348">O elemento `<frameworkAssemblies>` contém zero ou mais elementos `<frameworkAssembly>`, cada um deles especifica os seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="57cc4-348">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="57cc4-349">Atributo</span><span class="sxs-lookup"><span data-stu-id="57cc4-349">Attribute</span></span> | <span data-ttu-id="57cc4-350">Descrição</span><span class="sxs-lookup"><span data-stu-id="57cc4-350">Description</span></span> |
| --- | --- |
| <span data-ttu-id="57cc4-351">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="57cc4-351">**assemblyName**</span></span> | <span data-ttu-id="57cc4-352">(Obrigatório) O nome totalmente qualificado do assembly.</span><span class="sxs-lookup"><span data-stu-id="57cc4-352">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="57cc4-353">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="57cc4-353">**targetFramework**</span></span> | <span data-ttu-id="57cc4-354">(Opcional) Especifica a estrutura de destino à qual esta referência se aplica.</span><span class="sxs-lookup"><span data-stu-id="57cc4-354">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="57cc4-355">Se omitido, indica que a referência se aplica a todas as estruturas.</span><span class="sxs-lookup"><span data-stu-id="57cc4-355">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="57cc4-356">Consulte [Estruturas de destino](../reference/target-frameworks.md) para ver os identificadores de estrutura exatos.</span><span class="sxs-lookup"><span data-stu-id="57cc4-356">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="57cc4-357">O exemplo a seguir mostra uma referência a `System.Net` todas as estruturas de destino e uma referência a `System.ServiceModel` apenas para o .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="57cc4-357">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="57cc4-358">Incluindo arquivos do assembly</span><span class="sxs-lookup"><span data-stu-id="57cc4-358">Including assembly files</span></span>

<span data-ttu-id="57cc4-359">Se você seguir as convenções descritas em [Criando um pacote](../create-packages/creating-a-package.md), não será necessário especificar explicitamente uma lista de arquivos no arquivo `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-359">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="57cc4-360">O comando `nuget pack` escolherá automaticamente os arquivos necessários.</span><span class="sxs-lookup"><span data-stu-id="57cc4-360">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="57cc4-361">Quando um pacote é instalado em um projeto, o NuGet adiciona automaticamente as referências de assembly às DLLs do pacote, *excluindo* aquelas que são nomeados `.resources.dll` porque são considerados assemblies satélites.</span><span class="sxs-lookup"><span data-stu-id="57cc4-361">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="57cc4-362">Por esse motivo, evite usar `.resources.dll` para arquivos que contêm código de pacote essencial.</span><span class="sxs-lookup"><span data-stu-id="57cc4-362">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="57cc4-363">Para ignorar esse comportamento automático e controlar explicitamente quais arquivos são incluídos em um pacote, coloque uma elemento `<files>` como um filho de `<package>` (e um irmão de `<metadata>`), identificando cada arquivo com um elemento `<file>` separado.</span><span class="sxs-lookup"><span data-stu-id="57cc4-363">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="57cc4-364">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="57cc4-364">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="57cc4-365">Com o NuGet 2.x e anteriores, e em projetos que usam `packages.config`, o elemento `<files>` também é usado para incluir arquivos de conteúdo imutáveis quando um pacote é instalado.</span><span class="sxs-lookup"><span data-stu-id="57cc4-365">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="57cc4-366">Com o NuGet 3.3 ou superior e projetos PackageReference, o elemento `<contentFiles>` é usado.</span><span class="sxs-lookup"><span data-stu-id="57cc4-366">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="57cc4-367">Consulte [Incluindo arquivos de conteúdo](#including-content-files) abaixo para ver os detalhes.</span><span class="sxs-lookup"><span data-stu-id="57cc4-367">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="57cc4-368">Atributos do elemento de arquivo</span><span class="sxs-lookup"><span data-stu-id="57cc4-368">File element attributes</span></span>

<span data-ttu-id="57cc4-369">Cada elemento `<file>` especifica os seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="57cc4-369">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="57cc4-370">Atributo</span><span class="sxs-lookup"><span data-stu-id="57cc4-370">Attribute</span></span> | <span data-ttu-id="57cc4-371">Descrição</span><span class="sxs-lookup"><span data-stu-id="57cc4-371">Description</span></span> |
| --- | --- |
| <span data-ttu-id="57cc4-372">**src**</span><span class="sxs-lookup"><span data-stu-id="57cc4-372">**src**</span></span> | <span data-ttu-id="57cc4-373">O local do arquivo ou arquivos a serem incluídos, sujeito a exclusões especificadas pelo atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-373">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="57cc4-374">O caminho é relativo ao arquivo `.nuspec`, a menos que um caminho absoluto seja especificado.</span><span class="sxs-lookup"><span data-stu-id="57cc4-374">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="57cc4-375">O caractere curinga `*` é permitido e o caractere curinga duplo `**` sugere uma pesquisa de pastas recursiva.</span><span class="sxs-lookup"><span data-stu-id="57cc4-375">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="57cc4-376">**target**</span><span class="sxs-lookup"><span data-stu-id="57cc4-376">**target**</span></span> | <span data-ttu-id="57cc4-377">O caminho relativo para a pasta dentro do pacote em que os arquivos de origem são colocados, os quais devem começar com `lib`, `content`, `build` ou `tools`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-377">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="57cc4-378">Consulte [Criando um .nuspec de um diretório de trabalho baseado em convenção](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="57cc4-378">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="57cc4-379">**exclude**</span><span class="sxs-lookup"><span data-stu-id="57cc4-379">**exclude**</span></span> | <span data-ttu-id="57cc4-380">Uma lista separada por ponto-e-vírgula de arquivos ou padrões de arquivo para excluir o local `src`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-380">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="57cc4-381">O caractere curinga `*` é permitido e o caractere curinga duplo `**` sugere uma pesquisa de pastas recursiva.</span><span class="sxs-lookup"><span data-stu-id="57cc4-381">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="57cc4-382">Exemplos</span><span class="sxs-lookup"><span data-stu-id="57cc4-382">Examples</span></span>

<span data-ttu-id="57cc4-383">**Assembly único**</span><span class="sxs-lookup"><span data-stu-id="57cc4-383">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="57cc4-384">**Assembly único específico para uma estrutura de destino**</span><span class="sxs-lookup"><span data-stu-id="57cc4-384">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="57cc4-385">**Conjunto de DLLs que usam um caractere curinga**</span><span class="sxs-lookup"><span data-stu-id="57cc4-385">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="57cc4-386">**DLLs de estruturas diferentes**</span><span class="sxs-lookup"><span data-stu-id="57cc4-386">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="57cc4-387">**Excluindo arquivos**</span><span class="sxs-lookup"><span data-stu-id="57cc4-387">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="57cc4-388">Incluindo arquivos de conteúdo</span><span class="sxs-lookup"><span data-stu-id="57cc4-388">Including content files</span></span>

<span data-ttu-id="57cc4-389">Arquivos de conteúdo são arquivos imutáveis que um pacote incluir em um projeto.</span><span class="sxs-lookup"><span data-stu-id="57cc4-389">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="57cc4-390">Sendo imutáveis, eles não foram projetados para serem modificados pelo projeto consumidor.</span><span class="sxs-lookup"><span data-stu-id="57cc4-390">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="57cc4-391">Alguns exemplos de arquivos de conteúdo:</span><span class="sxs-lookup"><span data-stu-id="57cc4-391">Example content files include:</span></span>

- <span data-ttu-id="57cc4-392">Imagens que são inseridas como recursos</span><span class="sxs-lookup"><span data-stu-id="57cc4-392">Images that are embedded as resources</span></span>
- <span data-ttu-id="57cc4-393">Arquivos de origem que já são compilados</span><span class="sxs-lookup"><span data-stu-id="57cc4-393">Source files that are already compiled</span></span>
- <span data-ttu-id="57cc4-394">Scripts que precisam ser incluídos na saída de build do projeto</span><span class="sxs-lookup"><span data-stu-id="57cc4-394">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="57cc4-395">Arquivos de configuração para o pacote que precisam ser incluídos no projeto, mas não precisam de nenhuma alteração específica do projeto</span><span class="sxs-lookup"><span data-stu-id="57cc4-395">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="57cc4-396">Arquivos de conteúdo são incluídos em um pacote usando o elemento `<files>`, especificando a pasta `content` no atributo `target`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-396">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="57cc4-397">No entanto, esses arquivos são ignorados quando o pacote é instalado em um projeto usando PackageReference, que usa o elemento `<contentFiles>`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-397">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="57cc4-398">Para máxima compatibilidade com projetos de consumo, é ideal que um pacote especifique os arquivos de conteúdo em ambos os elementos.</span><span class="sxs-lookup"><span data-stu-id="57cc4-398">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="57cc4-399">Usando o elemento de arquivos para arquivos de conteúdo</span><span class="sxs-lookup"><span data-stu-id="57cc4-399">Using the files element for content files</span></span>

<span data-ttu-id="57cc4-400">Para arquivos de conteúdo, basta usar o mesmo formato que os arquivos do assembly, porém especifique `content` como a pasta base no atributo `target` conforme mostrado nos exemplos a seguir.</span><span class="sxs-lookup"><span data-stu-id="57cc4-400">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="57cc4-401">**Arquivos de conteúdo básico**</span><span class="sxs-lookup"><span data-stu-id="57cc4-401">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="57cc4-402">**Arquivos de conteúdo com a estrutura de diretório**</span><span class="sxs-lookup"><span data-stu-id="57cc4-402">**Content files with directory structure**</span></span>

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

<span data-ttu-id="57cc4-403">**Arquivo de conteúdo específico para uma estrutura de destino**</span><span class="sxs-lookup"><span data-stu-id="57cc4-403">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="57cc4-404">**Arquivo de conteúdo copiado para uma pasta com ponto no nome**</span><span class="sxs-lookup"><span data-stu-id="57cc4-404">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="57cc4-405">Nesse caso, o NuGet vê que a extensão em `target` não corresponde à extensão em `src` e, portanto, trata essa parte do nome no `target` como uma pasta:</span><span class="sxs-lookup"><span data-stu-id="57cc4-405">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="57cc4-406">**Arquivos de conteúdo sem extensões**</span><span class="sxs-lookup"><span data-stu-id="57cc4-406">**Content files without extensions**</span></span>

<span data-ttu-id="57cc4-407">Para incluir arquivos sem extensão, use os curingas `*` ou `**`:</span><span class="sxs-lookup"><span data-stu-id="57cc4-407">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="57cc4-408">**Arquivos de conteúdo com caminho e destino profundos**</span><span class="sxs-lookup"><span data-stu-id="57cc4-408">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="57cc4-409">Nesse caso, como as extensões de arquivo de origem e de destino correspondem, o NuGet pressupõe que o destino é um nome de arquivo e não uma pasta:</span><span class="sxs-lookup"><span data-stu-id="57cc4-409">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="57cc4-410">**Renomeando um arquivo de conteúdo no pacote**</span><span class="sxs-lookup"><span data-stu-id="57cc4-410">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="57cc4-411">**Excluindo arquivos**</span><span class="sxs-lookup"><span data-stu-id="57cc4-411">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="57cc4-412">Usando o elemento contentFiles para arquivos de conteúdo</span><span class="sxs-lookup"><span data-stu-id="57cc4-412">Using the contentFiles element for content files</span></span>

<span data-ttu-id="57cc4-413">*NuGet 4.0 e posteriores com PackageReference*</span><span class="sxs-lookup"><span data-stu-id="57cc4-413">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="57cc4-414">Por padrão, um pacote coloca o conteúdo em uma pasta `contentFiles` (veja abaixo) e `nuget pack` incluiu todos os arquivos nessa pasta usando os atributos padrão.</span><span class="sxs-lookup"><span data-stu-id="57cc4-414">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="57cc4-415">Nesse caso, não é necessário incluir um nó `contentFiles` no `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-415">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="57cc4-416">Para controlar quais arquivos são incluídos, o elemento `<contentFiles>` especifica uma coleção de elementos `<files>` que identificam as inclusões dos arquivos exatos.</span><span class="sxs-lookup"><span data-stu-id="57cc4-416">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="57cc4-417">Esses arquivos são especificados com um conjunto de atributos que descrevem como eles devem ser usados dentro do sistema de projeto:</span><span class="sxs-lookup"><span data-stu-id="57cc4-417">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="57cc4-418">Atributo</span><span class="sxs-lookup"><span data-stu-id="57cc4-418">Attribute</span></span> | <span data-ttu-id="57cc4-419">Descrição</span><span class="sxs-lookup"><span data-stu-id="57cc4-419">Description</span></span> |
| --- | --- |
| <span data-ttu-id="57cc4-420">**include**</span><span class="sxs-lookup"><span data-stu-id="57cc4-420">**include**</span></span> | <span data-ttu-id="57cc4-421">(Obrigatório) O local do arquivo ou arquivos a serem incluídos, sujeito a exclusões especificadas pelo atributo `exclude`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-421">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="57cc4-422">O caminho é relativo à pasta `contentFiles`, a menos que um caminho absoluto seja especificado.</span><span class="sxs-lookup"><span data-stu-id="57cc4-422">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="57cc4-423">O caractere curinga `*` é permitido e o caractere curinga duplo `**` sugere uma pesquisa de pastas recursiva.</span><span class="sxs-lookup"><span data-stu-id="57cc4-423">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="57cc4-424">**exclude**</span><span class="sxs-lookup"><span data-stu-id="57cc4-424">**exclude**</span></span> | <span data-ttu-id="57cc4-425">Uma lista separada por ponto-e-vírgula de arquivos ou padrões de arquivo para excluir o local `src`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-425">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="57cc4-426">O caractere curinga `*` é permitido e o caractere curinga duplo `**` sugere uma pesquisa de pastas recursiva.</span><span class="sxs-lookup"><span data-stu-id="57cc4-426">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="57cc4-427">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="57cc4-427">**buildAction**</span></span> | <span data-ttu-id="57cc4-428">A ação de compilação a ser atribuída ao item de conteúdo para MSBuild, como `Content`, `None`, `Embedded Resource`, `Compile`, etc. O padrão é `Compile`.</span><span class="sxs-lookup"><span data-stu-id="57cc4-428">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="57cc4-429">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="57cc4-429">**copyToOutput**</span></span> | <span data-ttu-id="57cc4-430">Um booliano que indica se os itens de conteúdo devem ser copiados para a pasta de saída Build (ou Publish).</span><span class="sxs-lookup"><span data-stu-id="57cc4-430">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="57cc4-431">O padrão é falso.</span><span class="sxs-lookup"><span data-stu-id="57cc4-431">The default is false.</span></span> |
| <span data-ttu-id="57cc4-432">**flatten**</span><span class="sxs-lookup"><span data-stu-id="57cc4-432">**flatten**</span></span> | <span data-ttu-id="57cc4-433">Um valor booliano que indica se os itens de conteúdo devem ser copiados para uma única pasta na saída do build (verdadeiro) ou preservar a estrutura de pasta no pacote (falso).</span><span class="sxs-lookup"><span data-stu-id="57cc4-433">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="57cc4-434">Esse sinalizador só funciona quando o sinalizador copyToOutput está definido como true.</span><span class="sxs-lookup"><span data-stu-id="57cc4-434">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="57cc4-435">O padrão é falso.</span><span class="sxs-lookup"><span data-stu-id="57cc4-435">The default is false.</span></span> |

<span data-ttu-id="57cc4-436">Ao instalar um pacote, o NuGet aplicará os elementos filho de `<contentFiles>` de cima para baixo.</span><span class="sxs-lookup"><span data-stu-id="57cc4-436">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="57cc4-437">Se várias entradas corresponderem ao mesmo arquivo, todas as entradas serão aplicadas.</span><span class="sxs-lookup"><span data-stu-id="57cc4-437">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="57cc4-438">A entrada superior substitui as entradas mais baixas em caso de conflito para o mesmo atributo.</span><span class="sxs-lookup"><span data-stu-id="57cc4-438">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="57cc4-439">Estrutura de pastas do pacote</span><span class="sxs-lookup"><span data-stu-id="57cc4-439">Package folder structure</span></span>

<span data-ttu-id="57cc4-440">O projeto do pacote deve estruturar o conteúdo usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="57cc4-440">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="57cc4-441">`codeLanguages` pode ser `cs`, `vb`, `fs`, `any` ou o equivalente em letras minúsculas de determinado `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="57cc4-441">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="57cc4-442">`TxM` é qualquer moniker da estrutura de destino legal compatível com o NuGet (consulte [Estruturas de destino](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="57cc4-442">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="57cc4-443">Qualquer estrutura de pasta pode ser acrescentada ao final dessa sintaxe.</span><span class="sxs-lookup"><span data-stu-id="57cc4-443">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="57cc4-444">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="57cc4-444">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="57cc4-445">As pastas vazias podem usar `.` para recusar o fornecimento de conteúdo para certas combinações de idioma e TxM, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="57cc4-445">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="57cc4-446">Exemplo da seção contentFiles</span><span class="sxs-lookup"><span data-stu-id="57cc4-446">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="57cc4-447">Arquivos nuspec de exemplo</span><span class="sxs-lookup"><span data-stu-id="57cc4-447">Example nuspec files</span></span>

<span data-ttu-id="57cc4-448">**Um simples `.nuspec` que não especifica dependências ou arquivos**</span><span class="sxs-lookup"><span data-stu-id="57cc4-448">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="57cc4-449">**Um `.nuspec` com dependências**</span><span class="sxs-lookup"><span data-stu-id="57cc4-449">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="57cc4-450">**Um `.nuspec` com arquivos**</span><span class="sxs-lookup"><span data-stu-id="57cc4-450">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="57cc4-451">**Um `.nuspec` com assemblies de estrutura**</span><span class="sxs-lookup"><span data-stu-id="57cc4-451">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="57cc4-452">Neste exemplo, os seguintes itens são instalados em destinos específicos do projeto:</span><span class="sxs-lookup"><span data-stu-id="57cc4-452">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="57cc4-453">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="57cc4-453">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="57cc4-454">Perfil de Cliente do .NET4 -> `System.Net`</span><span class="sxs-lookup"><span data-stu-id="57cc4-454">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="57cc4-455">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="57cc4-455">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="57cc4-456">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="57cc4-456">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
