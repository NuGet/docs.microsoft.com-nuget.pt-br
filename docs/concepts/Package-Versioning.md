---
title: Referência da versão do pacote NuGet
description: Detalhes exatos sobre a especificação de números de versão e intervalos para outros pacotes dos quais um pacote NuGet depende e como as dependências são instaladas.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 912c0d015e2f499bc7386483bc6c35ecd765d3d4
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428831"
---
# <a name="package-versioning"></a><span data-ttu-id="a0d58-103">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="a0d58-103">Package versioning</span></span>

<span data-ttu-id="a0d58-104">Um pacote específico é sempre referenciado usando seu identificador de pacote e um número de versão exato.</span><span class="sxs-lookup"><span data-stu-id="a0d58-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="a0d58-105">Por exemplo, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) em nuget.org tem várias dezenas de pacotes específicos disponíveis, desde a versão *4.1.10311* até a versão *6.1.3* (a última versão estável) e uma variedade de versões de pré-lançamento, como *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="a0d58-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="a0d58-106">Ao criar um pacote, você atribui um número de versão específico a um sufixo de texto de pré-lançamento opcional.</span><span class="sxs-lookup"><span data-stu-id="a0d58-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="a0d58-107">Ao consumir pacotes, por outro lado, você pode especificar um número de versão exato ou um intervalo de versões aceitáveis.</span><span class="sxs-lookup"><span data-stu-id="a0d58-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="a0d58-108">Neste tópico:</span><span class="sxs-lookup"><span data-stu-id="a0d58-108">In this topic:</span></span>

- <span data-ttu-id="a0d58-109">[Noções básicas sobre versão](#version-basics), incluindo sufixos de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="a0d58-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="a0d58-110">Intervalos de versão</span><span class="sxs-lookup"><span data-stu-id="a0d58-110">Version ranges</span></span>](#version-ranges)
- [<span data-ttu-id="a0d58-111">Números de versão normalizados</span><span class="sxs-lookup"><span data-stu-id="a0d58-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="a0d58-112">Noções básicas sobre versão</span><span class="sxs-lookup"><span data-stu-id="a0d58-112">Version basics</span></span>

<span data-ttu-id="a0d58-113">Um número de versão específico está no formato *Principal.Secundário.Patch [-Sufixo]* , em que os componentes possuem os seguintes significados:</span><span class="sxs-lookup"><span data-stu-id="a0d58-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="a0d58-114">*Principal*: alterações recentes</span><span class="sxs-lookup"><span data-stu-id="a0d58-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="a0d58-115">*Secundário*: novos recursos, mas compatível com versões anteriores</span><span class="sxs-lookup"><span data-stu-id="a0d58-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="a0d58-116">*Patch*: somente correções de bugs compatíveis com versões anteriores</span><span class="sxs-lookup"><span data-stu-id="a0d58-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="a0d58-117">*-Sufixo* (opcional): um hífen seguido por uma cadeia de caracteres denotando uma versão de pré-lançamento (seguindo a [convenção Controle de Versão Semântico ou SemVer 1.0](https://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="a0d58-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="a0d58-118">**Exemplos:**</span><span class="sxs-lookup"><span data-stu-id="a0d58-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="a0d58-119">nuget.org rejeita qualquer upload de pacote que não tenha um número de versão exato.</span><span class="sxs-lookup"><span data-stu-id="a0d58-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="a0d58-120">A versão precisa ser especificada no `.nuspec` ou no arquivo de projeto usado para criar o pacote.</span><span class="sxs-lookup"><span data-stu-id="a0d58-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="a0d58-121">Versões de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="a0d58-121">Pre-release versions</span></span>

<span data-ttu-id="a0d58-122">Tecnicamente falando, os criadores de pacotes podem usar qualquer cadeia de caracteres como sufixo para denotar uma versão de pré-lançamento, já que o NuGet trata qualquer versão como pré-lançamento e não faz outra interpretação.</span><span class="sxs-lookup"><span data-stu-id="a0d58-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="a0d58-123">Ou seja, o NuGet exibe a cadeia de caracteres de versão completa em qualquer interface do usuário, deixando qualquer interpretação do significado do sufixo para o consumidor.</span><span class="sxs-lookup"><span data-stu-id="a0d58-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="a0d58-124">Dito isso, os desenvolvedores de pacotes geralmente seguem as convenções de nomenclatura reconhecidas:</span><span class="sxs-lookup"><span data-stu-id="a0d58-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="a0d58-125">`-alpha`: versão Alfa, normalmente usada para trabalho em andamento e experimentação.</span><span class="sxs-lookup"><span data-stu-id="a0d58-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="a0d58-126">`-beta`: versão beta, normalmente uma completa com recursos para a próxima versão planejada, mas pode conter erros conhecidos.</span><span class="sxs-lookup"><span data-stu-id="a0d58-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="a0d58-127">`-rc`: versão Release candidate, normalmente uma versão que é potencialmente a final (estável), a menos que surjam bugs significativos.</span><span class="sxs-lookup"><span data-stu-id="a0d58-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="a0d58-128">O NuGet 4.3.0+ é compatível com o [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), que oferece suporte para números com notação de ponto pré-lançamento, como no *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="a0d58-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="a0d58-129">A notação de ponto não e compatível com as versões do NuGet anteriores à 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="a0d58-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="a0d58-130">Você pode usar um formulário como *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="a0d58-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="a0d58-131">Quando as referências de pacote e várias versões de pacote diferem apenas pelo sufixo, o NuGet escolhe uma versão sem um sufixo primeiro e, em seguida, aplica a precedência às versões de pré-lançamento em ordem alfabética inversa.</span><span class="sxs-lookup"><span data-stu-id="a0d58-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="a0d58-132">Por exemplo, as seguintes versões seriam escolhidas na ordem exata mostrada:</span><span class="sxs-lookup"><span data-stu-id="a0d58-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="a0d58-133">Controle de Versão Semântico 2.0.0</span><span class="sxs-lookup"><span data-stu-id="a0d58-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="a0d58-134">Com o NuGet 4.3.0+ e o Visual Studio 2017 versão 15.3+, o NuGet oferece suporte ao [Controle de Versão Semântico 2.0.0](https://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="a0d58-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="a0d58-135">Determinadas semânticas do SemVer v2.0.0 não têm suporte em clientes mais antigos.</span><span class="sxs-lookup"><span data-stu-id="a0d58-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="a0d58-136">O NuGet considerará uma versão do pacote como SemVer v2.0.0 específica se qualquer uma das seguintes afirmações for verdadeira:</span><span class="sxs-lookup"><span data-stu-id="a0d58-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="a0d58-137">O rótulo de pré-lançamento é separado por pontos, por exemplo,*1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="a0d58-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="a0d58-138">A versão tem metadados de build, por exemplo, *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="a0d58-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="a0d58-139">Para nuget.org, um pacote será definido como um pacote SemVer v2.0.0 se qualquer uma das seguintes afirmações for verdadeira:</span><span class="sxs-lookup"><span data-stu-id="a0d58-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="a0d58-140">A versão do pacote é compatível com SemVer v2.0.0, mas não compatível com SemVer v1.0.0, conforme definido acima.</span><span class="sxs-lookup"><span data-stu-id="a0d58-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="a0d58-141">Qualquer um dos intervalos de versão de dependência do pacote tem uma versão mínima ou máxima que é compatível com SemVer v2.0.0, mas não compatível com SemVer v1.0.0, definida acima; por exemplo, *[1.0.0-alpha.1, )* .</span><span class="sxs-lookup"><span data-stu-id="a0d58-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="a0d58-142">Se você carregar um pacote específico do SemVer v2.0.0 para o nuget.org, o pacote ficará invisível para os clientes mais antigos e estará disponível apenas para os seguintes clientes do NuGet:</span><span class="sxs-lookup"><span data-stu-id="a0d58-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="a0d58-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="a0d58-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="a0d58-144">Versão do Visual Studio 2017 15.3+</span><span class="sxs-lookup"><span data-stu-id="a0d58-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="a0d58-145">Visual Studio 2015 com [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="a0d58-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="a0d58-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="a0d58-146">dotnet</span></span>
  - <span data-ttu-id="a0d58-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="a0d58-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="a0d58-148">Clientes de terceiros:</span><span class="sxs-lookup"><span data-stu-id="a0d58-148">Third-party clients:</span></span>

- <span data-ttu-id="a0d58-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="a0d58-149">JetBrains Rider</span></span>
- <span data-ttu-id="a0d58-150">Paket versão 5.0+</span><span class="sxs-lookup"><span data-stu-id="a0d58-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a><span data-ttu-id="a0d58-151">Intervalos de versão</span><span class="sxs-lookup"><span data-stu-id="a0d58-151">Version ranges</span></span>

<span data-ttu-id="a0d58-152">Ao se referir a dependências de pacote, o NuGet oferece suporte ao uso de notação de intervalo para especificar intervalos de versão, resumidos da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="a0d58-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="a0d58-153">Notation</span><span class="sxs-lookup"><span data-stu-id="a0d58-153">Notation</span></span> | <span data-ttu-id="a0d58-154">Regra aplicada</span><span class="sxs-lookup"><span data-stu-id="a0d58-154">Applied rule</span></span> | <span data-ttu-id="a0d58-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="a0d58-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="a0d58-156">1.0</span><span class="sxs-lookup"><span data-stu-id="a0d58-156">1.0</span></span> | <span data-ttu-id="a0d58-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="a0d58-157">x ≥ 1.0</span></span> | <span data-ttu-id="a0d58-158">Versão mínima, inclusiva</span><span class="sxs-lookup"><span data-stu-id="a0d58-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="a0d58-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="a0d58-159">(1.0,)</span></span> | <span data-ttu-id="a0d58-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="a0d58-160">x > 1.0</span></span> | <span data-ttu-id="a0d58-161">Versão mínima, exclusiva</span><span class="sxs-lookup"><span data-stu-id="a0d58-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="a0d58-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="a0d58-162">[1.0]</span></span> | <span data-ttu-id="a0d58-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="a0d58-163">x == 1.0</span></span> | <span data-ttu-id="a0d58-164">Correspondência exata da versão</span><span class="sxs-lookup"><span data-stu-id="a0d58-164">Exact version match</span></span> |
| <span data-ttu-id="a0d58-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="a0d58-165">(,1.0]</span></span> | <span data-ttu-id="a0d58-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="a0d58-166">x ≤ 1.0</span></span> | <span data-ttu-id="a0d58-167">Versão máxima, inclusiva</span><span class="sxs-lookup"><span data-stu-id="a0d58-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="a0d58-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="a0d58-168">(,1.0)</span></span> | <span data-ttu-id="a0d58-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="a0d58-169">x < 1.0</span></span> | <span data-ttu-id="a0d58-170">Versão máxima, exclusiva</span><span class="sxs-lookup"><span data-stu-id="a0d58-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="a0d58-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="a0d58-171">[1.0,2.0]</span></span> | <span data-ttu-id="a0d58-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="a0d58-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="a0d58-173">Intervalo exato, inclusivo</span><span class="sxs-lookup"><span data-stu-id="a0d58-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="a0d58-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="a0d58-174">(1.0,2.0)</span></span> | <span data-ttu-id="a0d58-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="a0d58-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="a0d58-176">Intervalo exato, exclusivo</span><span class="sxs-lookup"><span data-stu-id="a0d58-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="a0d58-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="a0d58-177">[1.0,2.0)</span></span> | <span data-ttu-id="a0d58-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="a0d58-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="a0d58-179">Versão mínima inclusiva e máxima exclusiva combinadas</span><span class="sxs-lookup"><span data-stu-id="a0d58-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="a0d58-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="a0d58-180">(1.0)</span></span>    | <span data-ttu-id="a0d58-181">invalid</span><span class="sxs-lookup"><span data-stu-id="a0d58-181">invalid</span></span> | <span data-ttu-id="a0d58-182">invalid</span><span class="sxs-lookup"><span data-stu-id="a0d58-182">invalid</span></span> |

<span data-ttu-id="a0d58-183">Ao usar o formato PackageReference, o NuGet também dá suporte ao uso de uma notação flutuante, \*, para as partes de sufixo principal, secundária, patch e de pré-lançamento do número.</span><span class="sxs-lookup"><span data-stu-id="a0d58-183">When using the PackageReference format, NuGet also supports using a floating notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="a0d58-184">Não há suporte para versões flutuantes com o formato `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="a0d58-184">Floating versions are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="a0d58-185">Os intervalos de versão no PackageReference incluem versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="a0d58-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="a0d58-186">Por design, versões flutuantes não resolvem as versões de pré-lançamento, a menos que sejam aceitas.</span><span class="sxs-lookup"><span data-stu-id="a0d58-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="a0d58-187">Para obter o status da solicitação de recurso relacionada, confira [Problema 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="a0d58-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="a0d58-188">Exemplos</span><span class="sxs-lookup"><span data-stu-id="a0d58-188">Examples</span></span>

<span data-ttu-id="a0d58-189">Sempre especifique uma versão ou intervalo de versão para dependências de pacote em arquivos de projeto, arquivos `packages.config` e arquivos `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="a0d58-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="a0d58-190">Sem uma versão ou intervalo de versão, o NuGet 2.8.x e versões anteriores escolhem a versão do pacote disponível mais recente ao resolver uma dependência, enquanto o NuGet 3.xe posterior escolhe a versão de pacote mais baixa.</span><span class="sxs-lookup"><span data-stu-id="a0d58-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="a0d58-191">Especificar uma versão ou um intervalo de versões evita essa incerteza.</span><span class="sxs-lookup"><span data-stu-id="a0d58-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="a0d58-192">Referências em arquivos de projeto (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="a0d58-192">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="a0d58-193">**Referências em `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="a0d58-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="a0d58-194">Em `packages.config`, toda dependência é listada com um atributo de `version` exato que é usado ao restaurar pacotes.</span><span class="sxs-lookup"><span data-stu-id="a0d58-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="a0d58-195">O atributo `allowedVersions` é usado apenas durante as operações de atualização para restringir as versões às quais o pacote pode ser atualizado.</span><span class="sxs-lookup"><span data-stu-id="a0d58-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="a0d58-196">**Referências em arquivos `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="a0d58-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="a0d58-197">O atributo `version` em um elemento `<dependency>` descreve as versões de intervalo aceitáveis ​​para uma dependência.</span><span class="sxs-lookup"><span data-stu-id="a0d58-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="a0d58-198">Números de versão normalizados</span><span class="sxs-lookup"><span data-stu-id="a0d58-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="a0d58-199">Essa é uma alteração significativa para o NuGet 3.4 e posterior.</span><span class="sxs-lookup"><span data-stu-id="a0d58-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="a0d58-200">Ao obter pacotes de um repositório durante a instalação, reinstalação ou restauração de operações, o NuGet 3.4+ trata os números de versão da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a0d58-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="a0d58-201">Zeros à esquerda são removidos dos números de versão:</span><span class="sxs-lookup"><span data-stu-id="a0d58-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="a0d58-202">um zero na quarta parte do número de versão será omitido</span><span class="sxs-lookup"><span data-stu-id="a0d58-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="a0d58-203">As operações `pack` e `restore` normalizam as versões sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="a0d58-203">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="a0d58-204">Para pacotes já compilados, essa normalização não afeta os números de versão nos próprios pacotes; ela afeta apenas como o NuGet faz a correspondência das versões ao resolver dependências.</span><span class="sxs-lookup"><span data-stu-id="a0d58-204">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="a0d58-205">No entanto, os repositórios de pacotes do NuGet devem tratar esses valores da mesma maneira que o NuGet para evitar a duplicação da versão do pacote.</span><span class="sxs-lookup"><span data-stu-id="a0d58-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="a0d58-206">Portanto, um repositório que contenha a versão *1.0* de um pacote não deve hospedar também a versão *1.0.0* como um pacote separado e diferente.</span><span class="sxs-lookup"><span data-stu-id="a0d58-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
