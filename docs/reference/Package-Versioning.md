---
title: Referência de versão do pacote do NuGet
description: Obter detalhes exatos sobre como especificar números de versão e intervalos para outros pacotes mediante o qual depende de um pacote do NuGet e como as dependências são instaladas.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6407cd2ea5e5e7a9c9e2be679764a8a0d5dd9260
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852462"
---
# <a name="package-versioning"></a><span data-ttu-id="703e4-103">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="703e4-103">Package versioning</span></span>

<span data-ttu-id="703e4-104">Um pacote específico é sempre chamado usando seu identificador de pacote e um número de versão exato.</span><span class="sxs-lookup"><span data-stu-id="703e4-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="703e4-105">Por exemplo, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) em nuget.org tem vários pacotes específicos doze disponíveis, variando desde a versão *4.1.10311* para a versão *6.1.3* (o estável mais recente versão) e, como uma variedade de versões de pré-lançamento *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="703e4-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="703e4-106">Ao criar um pacote, você pode atribuir um número de versão específico com um sufixo de pré-lançamento um texto opcional.</span><span class="sxs-lookup"><span data-stu-id="703e4-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="703e4-107">Ao consumir pacotes, por outro lado, você pode especificar um número de versão exato ou um intervalo de versões aceitáveis.</span><span class="sxs-lookup"><span data-stu-id="703e4-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="703e4-108">Neste tópico:</span><span class="sxs-lookup"><span data-stu-id="703e4-108">In this topic:</span></span>

- <span data-ttu-id="703e4-109">[Noções básicas de versão](#version-basics) incluindo sufixos de versão de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="703e4-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="703e4-110">Curingas e intervalos de versão</span><span class="sxs-lookup"><span data-stu-id="703e4-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="703e4-111">Números de versão normalizado</span><span class="sxs-lookup"><span data-stu-id="703e4-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="703e4-112">Noções básicas de versão</span><span class="sxs-lookup"><span data-stu-id="703e4-112">Version basics</span></span>

<span data-ttu-id="703e4-113">Um número de versão específico está no formato *Major [-sufixo]*, onde os componentes têm os seguintes significados:</span><span class="sxs-lookup"><span data-stu-id="703e4-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="703e4-114">*Principais*: Alterações da falha</span><span class="sxs-lookup"><span data-stu-id="703e4-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="703e4-115">*Pequenas*: Novos recursos, mas compatível com versões anteriores</span><span class="sxs-lookup"><span data-stu-id="703e4-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="703e4-116">*Patch*: Somente correções de bug compatíveis com versões anteriores</span><span class="sxs-lookup"><span data-stu-id="703e4-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="703e4-117">*-Sufixo* (opcional): um hífen seguido por uma cadeia de caracteres que indica uma versão de pré-lançamento (seguir as [convenção de SemVer 1.0 ou de controle de versão semântico](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="703e4-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="703e4-118">**Exemplos:**</span><span class="sxs-lookup"><span data-stu-id="703e4-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="703e4-119">NuGet.org rejeita qualquer upload do pacote que não tem um número de versão exato.</span><span class="sxs-lookup"><span data-stu-id="703e4-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="703e4-120">A versão deve ser especificada no `.nuspec` ou arquivo de projeto usado para criar o pacote.</span><span class="sxs-lookup"><span data-stu-id="703e4-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="703e4-121">As versões de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="703e4-121">Pre-release versions</span></span>

<span data-ttu-id="703e4-122">Tecnicamente falando, criadores de pacote podem usar qualquer cadeia de caracteres como um sufixo a para denotar uma versão de pré-lançamento, como o NuGet trata qualquer versão tal como versões de pré-lançamento e não faz com que nenhuma outra interpretação.</span><span class="sxs-lookup"><span data-stu-id="703e4-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="703e4-123">Ou seja, exibe o NuGet a versão completa da cadeia de caracteres em qualquer interface do usuário estiver envolvido, deixando qualquer interpretação do significado do sufixo para o consumidor.</span><span class="sxs-lookup"><span data-stu-id="703e4-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="703e4-124">Dito isso, os desenvolvedores de pacote geralmente seguem as convenções de nomenclatura reconhecidas:</span><span class="sxs-lookup"><span data-stu-id="703e4-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="703e4-125">`-alpha`: Versão alfa, normalmente usado para em andamento e experimentação.</span><span class="sxs-lookup"><span data-stu-id="703e4-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="703e4-126">`-beta`: Versão beta, normalmente uma completa com recursos para a próxima versão planejada, mas pode conter erros conhecidos.</span><span class="sxs-lookup"><span data-stu-id="703e4-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="703e4-127">`-rc`: Versão Release Candidate, normalmente uma versão que é potencialmente a final (estável), a menos que surjam bugs significativos.</span><span class="sxs-lookup"><span data-stu-id="703e4-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="703e4-128">Dá suporte a NuGet 4.3.0 [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), que oferece suporte a números de versão de pré-lançamento com a notação de ponto, como em *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="703e4-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="703e4-129">A notação de ponto não e compatível com as versões do NuGet anteriores à 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="703e4-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="703e4-130">Você pode usar um formulário como *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="703e4-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="703e4-131">Para resolver referências de pacote e várias versões de pacote diferem apenas pelo sufixo, NuGet escolhe uma versão sem um sufixo pela primeira vez, em seguida, aplica-se a precedência para versões de pré-lançamento em ordem alfabética inversa.</span><span class="sxs-lookup"><span data-stu-id="703e4-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="703e4-132">Por exemplo, as versões a seguir serão escolhidas na ordem exata mostrada:</span><span class="sxs-lookup"><span data-stu-id="703e4-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="703e4-133">Controle de versão semântico 2.0.0</span><span class="sxs-lookup"><span data-stu-id="703e4-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="703e4-134">Com o NuGet 4.3.0 e Visual Studio 2017 versão 15.3 ou superior, o NuGet dá suporte a [controle de versão semântico 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="703e4-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="703e4-135">Não há suporte para determinadas semântica de SemVer v2.0.0 em clientes mais antigos.</span><span class="sxs-lookup"><span data-stu-id="703e4-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="703e4-136">O NuGet considerará uma versão do pacote de SemVer v2.0.0 específico se qualquer uma das instruções a seguir for verdadeira:</span><span class="sxs-lookup"><span data-stu-id="703e4-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="703e4-137">O rótulo de pré-lançamento é separado por ponto, por exemplo, *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="703e4-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="703e4-138">A versão tem metadados de compilação, por exemplo, *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="703e4-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="703e4-139">Para nuget.org, um pacote é definido como um pacote de v2.0.0 SemVer se qualquer uma das instruções a seguir for verdadeira:</span><span class="sxs-lookup"><span data-stu-id="703e4-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="703e4-140">A versão do pacote é SemVer v2.0.0 em conformidade, mas não SemVer v1.0.0 em conformidade, conforme definido acima.</span><span class="sxs-lookup"><span data-stu-id="703e4-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="703e4-141">Qualquer um dos intervalos de versão de dependência do pacote tem uma versão mínima ou máxima é SemVer v2.0.0 em conformidade, mas não SemVer v1.0.0 em conformidade, definido acima; Por exemplo, *[1.0.0-alpha.1,)*.</span><span class="sxs-lookup"><span data-stu-id="703e4-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="703e4-142">Se você carregar um pacote do SemVer v2.0.0 específicas para o nuget.org, o pacote é invisível para os clientes mais antigos e está disponível para os seguintes clientes NuGet:</span><span class="sxs-lookup"><span data-stu-id="703e4-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="703e4-143">O NuGet 4.3.0</span><span class="sxs-lookup"><span data-stu-id="703e4-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="703e4-144">Visual Studio 2017 versão 15.3 ou superior</span><span class="sxs-lookup"><span data-stu-id="703e4-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="703e4-145">Visual Studio 2015 com [v3.6.0 VSIX NuGet](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="703e4-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="703e4-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="703e4-146">dotnet</span></span>
  - <span data-ttu-id="703e4-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="703e4-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="703e4-148">Clientes de terceiros:</span><span class="sxs-lookup"><span data-stu-id="703e4-148">Third-party clients:</span></span>

- <span data-ttu-id="703e4-149">Rider da JetBrains</span><span class="sxs-lookup"><span data-stu-id="703e4-149">JetBrains Rider</span></span>
- <span data-ttu-id="703e4-150">Paket versão 5.0 ou superior</span><span class="sxs-lookup"><span data-stu-id="703e4-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="703e4-151">Curingas e intervalos de versão</span><span class="sxs-lookup"><span data-stu-id="703e4-151">Version ranges and wildcards</span></span>

<span data-ttu-id="703e4-152">Ao fazer referência às dependências do pacote, o NuGet dá suporte a usando a notação de intervalo para especificar os intervalos de versão, resumidos da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="703e4-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="703e4-153">Notation</span><span class="sxs-lookup"><span data-stu-id="703e4-153">Notation</span></span> | <span data-ttu-id="703e4-154">Regra aplicada</span><span class="sxs-lookup"><span data-stu-id="703e4-154">Applied rule</span></span> | <span data-ttu-id="703e4-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="703e4-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="703e4-156">1.0</span><span class="sxs-lookup"><span data-stu-id="703e4-156">1.0</span></span> | <span data-ttu-id="703e4-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="703e4-157">x ≥ 1.0</span></span> | <span data-ttu-id="703e4-158">Versão mínima, inclusive</span><span class="sxs-lookup"><span data-stu-id="703e4-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="703e4-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="703e4-159">(1.0,)</span></span> | <span data-ttu-id="703e4-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="703e4-160">x > 1.0</span></span> | <span data-ttu-id="703e4-161">Versão mínima, exclusivo</span><span class="sxs-lookup"><span data-stu-id="703e4-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="703e4-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="703e4-162">[1.0]</span></span> | <span data-ttu-id="703e4-163">x = = 1.0</span><span class="sxs-lookup"><span data-stu-id="703e4-163">x == 1.0</span></span> | <span data-ttu-id="703e4-164">Correspondência exata de versão</span><span class="sxs-lookup"><span data-stu-id="703e4-164">Exact version match</span></span> |
| <span data-ttu-id="703e4-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="703e4-165">(,1.0]</span></span> | <span data-ttu-id="703e4-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="703e4-166">x ≤ 1.0</span></span> | <span data-ttu-id="703e4-167">Versão máxima, inclusive</span><span class="sxs-lookup"><span data-stu-id="703e4-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="703e4-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="703e4-168">(,1.0)</span></span> | <span data-ttu-id="703e4-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="703e4-169">x < 1.0</span></span> | <span data-ttu-id="703e4-170">Versão máxima, exclusivo</span><span class="sxs-lookup"><span data-stu-id="703e4-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="703e4-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="703e4-171">[1.0,2.0]</span></span> | <span data-ttu-id="703e4-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="703e4-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="703e4-173">Intervalo exato, inclusive</span><span class="sxs-lookup"><span data-stu-id="703e4-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="703e4-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="703e4-174">(1.0,2.0)</span></span> | <span data-ttu-id="703e4-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="703e4-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="703e4-176">Intervalo exato, exclusivo</span><span class="sxs-lookup"><span data-stu-id="703e4-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="703e4-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="703e4-177">[1.0,2.0)</span></span> | <span data-ttu-id="703e4-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="703e4-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="703e4-179">Misto inclusivo mínimo e exclusivo versão máxima do</span><span class="sxs-lookup"><span data-stu-id="703e4-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="703e4-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="703e4-180">(1.0)</span></span>    | <span data-ttu-id="703e4-181">inválidos</span><span class="sxs-lookup"><span data-stu-id="703e4-181">invalid</span></span> | <span data-ttu-id="703e4-182">inválidos</span><span class="sxs-lookup"><span data-stu-id="703e4-182">invalid</span></span> |

<span data-ttu-id="703e4-183">Ao usar o formato PackageReference, o NuGet também suporta o uso de uma notação de curinga, \*, para Major, Minor, Patch e partes de sufixo de pré-lançamento do número.</span><span class="sxs-lookup"><span data-stu-id="703e4-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="703e4-184">Não há suporte para caracteres curinga com o `packages.config` formato.</span><span class="sxs-lookup"><span data-stu-id="703e4-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="703e4-185">As versões de pré-lançamento não são incluídas durante a resolução de intervalos de versão.</span><span class="sxs-lookup"><span data-stu-id="703e4-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="703e4-186">Versões de pré-lançamento *estão* incluídos ao usar um caractere curinga (\*).</span><span class="sxs-lookup"><span data-stu-id="703e4-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="703e4-187">O intervalo de versão *[1.0,2.0]*, por exemplo, não incluem 2.0 beta, mas a notação de curinga _2.0-\*_ faz.</span><span class="sxs-lookup"><span data-stu-id="703e4-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-\*_ does.</span></span> <span data-ttu-id="703e4-188">Ver [emitir 912](https://github.com/NuGet/Home/issues/912) para uma discussão mais detalhada sobre curingas de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="703e4-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="703e4-189">Exemplos</span><span class="sxs-lookup"><span data-stu-id="703e4-189">Examples</span></span>

<span data-ttu-id="703e4-190">Sempre especifique uma versão ou intervalo de versão para dependências do pacote em arquivos de projeto `packages.config` arquivos, e `.nuspec` arquivos.</span><span class="sxs-lookup"><span data-stu-id="703e4-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="703e4-191">Sem uma versão ou intervalo de versão, o NuGet 2.8.x e escolhe anteriormente a versão mais recente do pacote disponíveis ao resolver uma dependência, enquanto o NuGet 3.x e posterior, escolhe a versão mais antiga do pacote.</span><span class="sxs-lookup"><span data-stu-id="703e4-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="703e4-192">Especificando uma versão ou intervalo evita essa incerteza.</span><span class="sxs-lookup"><span data-stu-id="703e4-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="703e4-193">Referências em arquivos de projeto (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="703e4-193">References in project files (PackageReference)</span></span>

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
```

<span data-ttu-id="703e4-194">**Referências no `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="703e4-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="703e4-195">Na `packages.config`, cada dependência é listada com um exata `version` atributo que é usado ao restaurar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="703e4-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="703e4-196">O `allowedVersions` atributo é usado somente durante as operações de atualização para restringir as versões aos quais o pacote pode ser atualizado.</span><span class="sxs-lookup"><span data-stu-id="703e4-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="703e4-197">**Referências no `.nuspec` arquivos**</span><span class="sxs-lookup"><span data-stu-id="703e4-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="703e4-198">O `version` de atributo em um `<dependency>` elemento descreve as versões de intervalo são aceitáveis para uma dependência.</span><span class="sxs-lookup"><span data-stu-id="703e4-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="703e4-199">Números de versão normalizado</span><span class="sxs-lookup"><span data-stu-id="703e4-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="703e4-200">Isso é uma alteração significativa para o NuGet 3.4 e posterior.</span><span class="sxs-lookup"><span data-stu-id="703e4-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="703e4-201">Ao obter pacotes de um repositório durante a instalação, reinstalar ou restaurar as operações, o NuGet 3.4 ou superior trata números de versão da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="703e4-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="703e4-202">Zeros à esquerda são removidos de números de versão:</span><span class="sxs-lookup"><span data-stu-id="703e4-202">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="703e4-203">Um zero na quarta parte do número de versão será omitido</span><span class="sxs-lookup"><span data-stu-id="703e4-203">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="703e4-204">Essa normalização não afeta os números de versão dos pacotes em si; ela afeta como o NuGet corresponde apenas versões ao resolver as dependências.</span><span class="sxs-lookup"><span data-stu-id="703e4-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="703e4-205">No entanto, os repositórios de pacote do NuGet devem tratar esses valores da mesma maneira como o NuGet para evitar a duplicação de versão do pacote.</span><span class="sxs-lookup"><span data-stu-id="703e4-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="703e4-206">Portanto, um repositório que contém a versão *1.0* de um pacote não devem também hospedar versão *1.0.0* como um pacote separado e diferente.</span><span class="sxs-lookup"><span data-stu-id="703e4-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
