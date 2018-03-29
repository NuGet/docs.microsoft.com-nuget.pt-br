---
title: Referência de versão do pacote do NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/23/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Informações sobre como especificar números de versão e intervalos para outros pacotes que depende de um pacote do NuGet e como as dependências estejam instaladas.
keywords: controle de versão, as dependências de pacotes do NuGet, versões de dependência NuGet, números de versão do NuGet, versão do pacote NuGet, intervalos de versão, especificações de versão, os números de versão normalizada
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 678ad79d9106a9f592ae4f47bc93cc117496e2c9
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="package-versioning"></a><span data-ttu-id="fb2e9-104">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="fb2e9-104">Package versioning</span></span>

<span data-ttu-id="fb2e9-105">Um pacote específico é sempre chamado usando seu identificador de pacote e um número de versão exata.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-105">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="fb2e9-106">Por exemplo, [do Entity Framework](https://www.nuget.org/packages/EntityFramework/) em nuget.org tem vários pacotes específicos de doze disponíveis, variando de versão *4.1.10311* versão *6.1.3* (o mais recente estável versão) e uma variedade de versões de pré-lançamento como *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-106">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="fb2e9-107">Ao criar um pacote, você pode atribuir um número de versão específico com um sufixo de texto opcional de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-107">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="fb2e9-108">Ao consumir pacotes, por outro lado, você pode especificar um número de versão exata ou um intervalo de versões aceitáveis.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-108">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="fb2e9-109">Neste tópico:</span><span class="sxs-lookup"><span data-stu-id="fb2e9-109">In this topic:</span></span>

- <span data-ttu-id="fb2e9-110">[Noções básicas de versão](#version-basics) incluindo sufixos de versão de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-110">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="fb2e9-111">Curingas e intervalos de versão</span><span class="sxs-lookup"><span data-stu-id="fb2e9-111">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="fb2e9-112">Números de versão normalizado</span><span class="sxs-lookup"><span data-stu-id="fb2e9-112">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="fb2e9-113">Noções básicas de versão</span><span class="sxs-lookup"><span data-stu-id="fb2e9-113">Version basics</span></span>

<span data-ttu-id="fb2e9-114">Um número de versão específico está no formato *Major [-sufixo]*, onde os componentes têm os seguintes significados:</span><span class="sxs-lookup"><span data-stu-id="fb2e9-114">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="fb2e9-115">*Principais*: alterações recentes</span><span class="sxs-lookup"><span data-stu-id="fb2e9-115">*Major*: Breaking changes</span></span>
- <span data-ttu-id="fb2e9-116">*Secundária*: novos recursos, mas compatível com versões anteriores</span><span class="sxs-lookup"><span data-stu-id="fb2e9-116">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="fb2e9-117">*Patch*: correções de bugs compatíveis com versões anteriores somente</span><span class="sxs-lookup"><span data-stu-id="fb2e9-117">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="fb2e9-118">*-Sufixo* (opcional): um hífen seguido por uma cadeia de caracteres que indica uma versão de pré-lançamento (seguir o [convenção de controle de versão semântico ou 1.0 SemVer](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="fb2e9-118">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="fb2e9-119">**Exemplos:**</span><span class="sxs-lookup"><span data-stu-id="fb2e9-119">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="fb2e9-120">NuGet.org rejeita qualquer upload do pacote que não tem um número de versão exata.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-120">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="fb2e9-121">A versão deve ser especificada no `.nuspec` ou arquivo de projeto usado para criar o pacote.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-121">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="fb2e9-122">As versões de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="fb2e9-122">Pre-release versions</span></span>

<span data-ttu-id="fb2e9-123">Tecnicamente, os criadores de pacote podem usar qualquer cadeia de caracteres como um sufixo a para denotar uma versão de pré-lançamento, como NuGet trata qualquer versão tal como pré-lançamento e não faz com que nenhum outra interpretação.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-123">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="fb2e9-124">Ou seja, o NuGet exibe a versão completa da cadeia de caracteres em qualquer interface de usuário estiver envolvido, deixando qualquer interpretação do significado do sufixo para o consumidor.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-124">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="fb2e9-125">Dito isso, os desenvolvedores geralmente seguem as convenções de nomenclatura reconhecidas:</span><span class="sxs-lookup"><span data-stu-id="fb2e9-125">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="fb2e9-126">`-alpha`: Versão alfa, normalmente usado para o trabalho em andamento e experimentação.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-126">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="fb2e9-127">`-beta`: versão beta, normalmente uma completa com recursos para a próxima versão planejada, mas pode conter erros conhecidos.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-127">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="fb2e9-128">`-rc`: versão Release candidate, normalmente uma versão que é potencialmente a final (estável), a menos que surjam bugs significativos.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-128">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="fb2e9-129">Oferece suporte a 4.3.0+ NuGet [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), que oferece suporte a números de versão de pré-lançamento com a notação de ponto, como em *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-129">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="fb2e9-130">A notação de ponto não e compatível com as versões do NuGet anteriores à 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-130">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="fb2e9-131">Você pode usar um formulário como *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-131">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="fb2e9-132">Ao resolver referências de pacote e várias versões de pacote são diferentes apenas pelo sufixo, NuGet escolhe uma versão sem um sufixo primeiro, em seguida, aplica-se a prioridade para as versões em ordem alfabética inversa de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-132">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="fb2e9-133">Por exemplo, as versões a seguir serão escolhidas na ordem exata mostrado:</span><span class="sxs-lookup"><span data-stu-id="fb2e9-133">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="fb2e9-134">Controle de versão semântico 2.0.0</span><span class="sxs-lookup"><span data-stu-id="fb2e9-134">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="fb2e9-135">Com o NuGet 4.3.0+ e Visual Studio 2017 versão 15,3 +, NuGet dá suporte a [o controle de versão semântico 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="fb2e9-135">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="fb2e9-136">Não há suporte para determinados semântica de v SemVer 2.0.0 em clientes mais antigos.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-136">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="fb2e9-137">NuGet considera uma versão do pacote a ser SemVer v 2.0.0 específico se qualquer uma das instruções a seguir for verdadeira:</span><span class="sxs-lookup"><span data-stu-id="fb2e9-137">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="fb2e9-138">O rótulo de pré-lançamento é separado por pontos, por exemplo, *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="fb2e9-138">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="fb2e9-139">A versão tem metadados de compilação, por exemplo, *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="fb2e9-139">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="fb2e9-140">Para nuget.org, um pacote é definido como um pacote de v 2.0.0 SemVer se qualquer uma das instruções a seguir for verdadeira:</span><span class="sxs-lookup"><span data-stu-id="fb2e9-140">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="fb2e9-141">A versão do pacote é SemVer v 2.0.0 compatível, mas não SemVer v1.0.0 compatíveis, conforme definido acima.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-141">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="fb2e9-142">Nenhum dos intervalos de versão de dependência do pacote tem uma versão mínima ou máxima é SemVer v 2.0.0 compatível, mas não SemVer v1.0.0 compatíveis, definidos acima. Por exemplo, *[1.0.0-alpha.1,)*.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-142">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="fb2e9-143">Se você carregar um pacote de v 2.0.0 específico SemVer nuget.org, o pacote é invisível para clientes mais antigos e disponível para os seguintes clientes NuGet:</span><span class="sxs-lookup"><span data-stu-id="fb2e9-143">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="fb2e9-144">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="fb2e9-144">NuGet 4.3.0+</span></span>
- <span data-ttu-id="fb2e9-145">Visual Studio 2017 versão 15,3 +</span><span class="sxs-lookup"><span data-stu-id="fb2e9-145">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="fb2e9-146">Visual Studio 2015 com [v3.6.0 VSIX NuGet](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="fb2e9-146">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="fb2e9-147">dotnet.exe (2.0.0+ .NET SDK)</span><span class="sxs-lookup"><span data-stu-id="fb2e9-147">dotnet.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="fb2e9-148">Clientes de terceiros:</span><span class="sxs-lookup"><span data-stu-id="fb2e9-148">Third-party clients:</span></span>

- <span data-ttu-id="fb2e9-149">Cláusula JetBrains adicional</span><span class="sxs-lookup"><span data-stu-id="fb2e9-149">JetBrains Rider</span></span>
- <span data-ttu-id="fb2e9-150">Paket versão 5.0 +</span><span class="sxs-lookup"><span data-stu-id="fb2e9-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="fb2e9-151">Curingas e intervalos de versão</span><span class="sxs-lookup"><span data-stu-id="fb2e9-151">Version ranges and wildcards</span></span>

<span data-ttu-id="fb2e9-152">Ao fazer referência a dependências do pacote, NuGet suporta usando a notação de intervalo para especificar os intervalos de versão, resumidos da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="fb2e9-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="fb2e9-153">Notation</span><span class="sxs-lookup"><span data-stu-id="fb2e9-153">Notation</span></span> | <span data-ttu-id="fb2e9-154">Regra aplicada</span><span class="sxs-lookup"><span data-stu-id="fb2e9-154">Applied rule</span></span> | <span data-ttu-id="fb2e9-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="fb2e9-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="fb2e9-156">1.0</span><span class="sxs-lookup"><span data-stu-id="fb2e9-156">1.0</span></span> | <span data-ttu-id="fb2e9-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="fb2e9-157">x ≥ 1.0</span></span> | <span data-ttu-id="fb2e9-158">Versão mínima, inclusive</span><span class="sxs-lookup"><span data-stu-id="fb2e9-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="fb2e9-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="fb2e9-159">(1.0,)</span></span> | <span data-ttu-id="fb2e9-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="fb2e9-160">x > 1.0</span></span> | <span data-ttu-id="fb2e9-161">Versão mínima, exclusivo</span><span class="sxs-lookup"><span data-stu-id="fb2e9-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="fb2e9-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="fb2e9-162">[1.0]</span></span> | <span data-ttu-id="fb2e9-163">x = = 1.0</span><span class="sxs-lookup"><span data-stu-id="fb2e9-163">x == 1.0</span></span> | <span data-ttu-id="fb2e9-164">Correspondência exata de versão</span><span class="sxs-lookup"><span data-stu-id="fb2e9-164">Exact version match</span></span> |
| <span data-ttu-id="fb2e9-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="fb2e9-165">(,1.0]</span></span> | <span data-ttu-id="fb2e9-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="fb2e9-166">x ≤ 1.0</span></span> | <span data-ttu-id="fb2e9-167">Versão máxima, inclusive</span><span class="sxs-lookup"><span data-stu-id="fb2e9-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="fb2e9-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="fb2e9-168">(,1.0)</span></span> | <span data-ttu-id="fb2e9-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="fb2e9-169">x < 1.0</span></span> | <span data-ttu-id="fb2e9-170">Versão máxima, exclusivo</span><span class="sxs-lookup"><span data-stu-id="fb2e9-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="fb2e9-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="fb2e9-171">[1.0,2.0]</span></span> | <span data-ttu-id="fb2e9-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="fb2e9-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="fb2e9-173">Intervalo exato, inclusive</span><span class="sxs-lookup"><span data-stu-id="fb2e9-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="fb2e9-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="fb2e9-174">(1.0,2.0)</span></span> | <span data-ttu-id="fb2e9-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="fb2e9-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="fb2e9-176">Intervalo exato, exclusivo</span><span class="sxs-lookup"><span data-stu-id="fb2e9-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="fb2e9-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="fb2e9-177">[1.0,2.0)</span></span> | <span data-ttu-id="fb2e9-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="fb2e9-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="fb2e9-179">Mista inclusivo mínima e exclusiva máximo da versão</span><span class="sxs-lookup"><span data-stu-id="fb2e9-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="fb2e9-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="fb2e9-180">(1.0)</span></span>    | <span data-ttu-id="fb2e9-181">inválidos</span><span class="sxs-lookup"><span data-stu-id="fb2e9-181">invalid</span></span> | <span data-ttu-id="fb2e9-182">inválidos</span><span class="sxs-lookup"><span data-stu-id="fb2e9-182">invalid</span></span> |

<span data-ttu-id="fb2e9-183">Ao usar o formato PackageReference, os NuGet também oferece suporte ao uso de uma notação de curinga, \*, para o principal, secundária, Patch e partes de sufixo de pré-lançamento do número.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="fb2e9-184">Não há suporte para caracteres curinga com o `packages.config` formato.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="fb2e9-185">As versões de pré-lançamento não são incluídas durante a resolução de intervalos de versão.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="fb2e9-186">As versões de pré-lançamento *são* incluído ao usar um caractere curinga (\*).</span><span class="sxs-lookup"><span data-stu-id="fb2e9-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="fb2e9-187">O intervalo de versão *[1.0,2.0]*, por exemplo, não inclua 2.0 beta, mas a notação de curinga _2.0-\*_ does.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-\*_ does.</span></span> <span data-ttu-id="fb2e9-188">Consulte [emitir 912](https://github.com/NuGet/Home/issues/912) para uma discussão mais detalhada em pré-lançamento curingas.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="fb2e9-189">Exemplos</span><span class="sxs-lookup"><span data-stu-id="fb2e9-189">Examples</span></span>

<span data-ttu-id="fb2e9-190">Sempre especifique uma versão ou um intervalo de versão para as dependências do pacote em arquivos de projeto, `packages.config` arquivos, e `.nuspec` arquivos.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="fb2e9-191">Sem uma versão ou um intervalo de versão, o NuGet 2.8.x e escolhe anteriormente a versão mais recente do pacote disponíveis ao resolver uma dependência, enquanto o NuGet 3. x e posterior escolhe a versão mais antiga do pacote.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="fb2e9-192">Especificando uma versão ou intervalo evita este incerteza.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="fb2e9-193">Referências em arquivos de projeto (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="fb2e9-193">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="fb2e9-194">**Referências em `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="fb2e9-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="fb2e9-195">Em `packages.config`, cada dependência é listada com um exata `version` atributo que é usado durante a restauração de pacotes.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="fb2e9-196">O `allowedVersions` atributo é usado somente durante as operações de atualização para restringir as versões aos quais o pacote pode ser atualizado.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

<span data-ttu-id="fb2e9-197">**Referências em `.nuspec` arquivos**</span><span class="sxs-lookup"><span data-stu-id="fb2e9-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="fb2e9-198">O `version` atributo em um `<dependency>` elemento descreve as versões de intervalo são aceitáveis em uma dependência.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a><span data-ttu-id="fb2e9-199">Números de versão normalizado</span><span class="sxs-lookup"><span data-stu-id="fb2e9-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="fb2e9-200">Isso é uma alteração significativa para NuGet 3.4 e versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="fb2e9-201">Ao obter pacotes de um repositório durante a instalação, reinstale ou restaurar as operações, o NuGet 3.4 + trata números de versão da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="fb2e9-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="fb2e9-202">Zeros à esquerda são removidos dos números de versão:</span><span class="sxs-lookup"><span data-stu-id="fb2e9-202">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="fb2e9-203">Um zero na quarta parte do número de versão será omitido</span><span class="sxs-lookup"><span data-stu-id="fb2e9-203">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="fb2e9-204">Essa normalização não afeta os números de versão dos pacotes em si; ele afeta somente como NuGet corresponde versões durante a resolução de dependências.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="fb2e9-205">No entanto, os repositórios de pacote do NuGet devem tratar esses valores da mesma maneira como o NuGet para evitar duplicação de versão do pacote.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="fb2e9-206">Portanto, um repositório que contém a versão *1.0* de um pacote não devem também hospedar versão *1.0.0* como um pacote diferente e separado.</span><span class="sxs-lookup"><span data-stu-id="fb2e9-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
