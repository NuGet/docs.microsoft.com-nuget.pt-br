---
title: Referência da versão do pacote NuGet
description: Detalhes exatos sobre a especificação de números de versão e intervalos para outros pacotes dos quais um pacote NuGet depende e como as dependências são instaladas.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 4cb12f439d796d583f52d657225c39418d5a4836
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237355"
---
# <a name="package-versioning"></a><span data-ttu-id="0e76b-103">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="0e76b-103">Package versioning</span></span>

<span data-ttu-id="0e76b-104">Um pacote específico é sempre referenciado usando seu identificador de pacote e um número de versão exato.</span><span class="sxs-lookup"><span data-stu-id="0e76b-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="0e76b-105">Por exemplo, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) em nuget.org tem várias dezenas de pacotes específicos disponíveis, desde a versão *4.1.10311* até a versão *6.1.3* (a última versão estável) e uma variedade de versões de pré-lançamento, como *6.2.0-beta1* .</span><span class="sxs-lookup"><span data-stu-id="0e76b-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1* .</span></span>

<span data-ttu-id="0e76b-106">Ao criar um pacote, você atribui um número de versão específico a um sufixo de texto de pré-lançamento opcional.</span><span class="sxs-lookup"><span data-stu-id="0e76b-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="0e76b-107">Ao consumir pacotes, por outro lado, você pode especificar um número de versão exato ou um intervalo de versões aceitáveis.</span><span class="sxs-lookup"><span data-stu-id="0e76b-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="0e76b-108">Neste tópico:</span><span class="sxs-lookup"><span data-stu-id="0e76b-108">In this topic:</span></span>

- <span data-ttu-id="0e76b-109">[Noções básicas sobre versão](#version-basics), incluindo sufixos de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="0e76b-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="0e76b-110">Intervalos de versão</span><span class="sxs-lookup"><span data-stu-id="0e76b-110">Version ranges</span></span>](#version-ranges)
- [<span data-ttu-id="0e76b-111">Números de versão normalizados</span><span class="sxs-lookup"><span data-stu-id="0e76b-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="0e76b-112">Noções básicas sobre versão</span><span class="sxs-lookup"><span data-stu-id="0e76b-112">Version basics</span></span>

<span data-ttu-id="0e76b-113">Um número de versão específico está no formato *Principal.Secundário.Patch [-Sufixo]* , em que os componentes possuem os seguintes significados:</span><span class="sxs-lookup"><span data-stu-id="0e76b-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]* , where the components have the following meanings:</span></span>

- <span data-ttu-id="0e76b-114">*Principal* : alterações recentes</span><span class="sxs-lookup"><span data-stu-id="0e76b-114">*Major* : Breaking changes</span></span>
- <span data-ttu-id="0e76b-115">*Secundário* : novos recursos, mas compatível com versões anteriores</span><span class="sxs-lookup"><span data-stu-id="0e76b-115">*Minor* : New features, but backwards compatible</span></span>
- <span data-ttu-id="0e76b-116">*Patch* : somente correções de bugs compatíveis com versões anteriores</span><span class="sxs-lookup"><span data-stu-id="0e76b-116">*Patch* : Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="0e76b-117">*-Sufixo* (opcional): um hífen seguido por uma cadeia de caracteres denotando uma versão de pré-lançamento (seguindo a [convenção Controle de Versão Semântico ou SemVer 1.0](https://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="0e76b-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="0e76b-118">**Exemplos:**</span><span class="sxs-lookup"><span data-stu-id="0e76b-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="0e76b-119">nuget.org rejeita qualquer upload de pacote que não tenha um número de versão exato.</span><span class="sxs-lookup"><span data-stu-id="0e76b-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="0e76b-120">A versão precisa ser especificada no `.nuspec` ou no arquivo de projeto usado para criar o pacote.</span><span class="sxs-lookup"><span data-stu-id="0e76b-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="0e76b-121">Versões de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="0e76b-121">Pre-release versions</span></span>

<span data-ttu-id="0e76b-122">Tecnicamente falando, os criadores de pacotes podem usar qualquer cadeia de caracteres como sufixo para denotar uma versão de pré-lançamento, já que o NuGet trata qualquer versão como pré-lançamento e não faz outra interpretação.</span><span class="sxs-lookup"><span data-stu-id="0e76b-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="0e76b-123">Ou seja, o NuGet exibe a cadeia de caracteres de versão completa em qualquer interface do usuário, deixando qualquer interpretação do significado do sufixo para o consumidor.</span><span class="sxs-lookup"><span data-stu-id="0e76b-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="0e76b-124">Dito isso, os desenvolvedores de pacotes geralmente seguem as convenções de nomenclatura reconhecidas:</span><span class="sxs-lookup"><span data-stu-id="0e76b-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="0e76b-125">`-alpha`: Versão Alfa, normalmente usada para trabalho em andamento e experimentação.</span><span class="sxs-lookup"><span data-stu-id="0e76b-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="0e76b-126">`-beta`: versão beta, normalmente uma completa com recursos para a próxima versão planejada, mas pode conter erros conhecidos.</span><span class="sxs-lookup"><span data-stu-id="0e76b-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="0e76b-127">`-rc`: versão Release candidate, normalmente uma versão que é potencialmente a final (estável), a menos que surjam bugs significativos.</span><span class="sxs-lookup"><span data-stu-id="0e76b-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="0e76b-128">O NuGet 4.3.0+ é compatível com o [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), que oferece suporte para números com notação de ponto pré-lançamento, como no *1.0.1-build.23* .</span><span class="sxs-lookup"><span data-stu-id="0e76b-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23* .</span></span> <span data-ttu-id="0e76b-129">A notação de ponto não e compatível com as versões do NuGet anteriores à 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="0e76b-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="0e76b-130">Você pode usar um formulário como *1.0.1-build23* .</span><span class="sxs-lookup"><span data-stu-id="0e76b-130">You can use a form like *1.0.1-build23* .</span></span>

<span data-ttu-id="0e76b-131">Quando as referências de pacote e várias versões de pacote diferem apenas pelo sufixo, o NuGet escolhe uma versão sem um sufixo primeiro e, em seguida, aplica a precedência às versões de pré-lançamento em ordem alfabética inversa.</span><span class="sxs-lookup"><span data-stu-id="0e76b-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="0e76b-132">Por exemplo, as seguintes versões seriam escolhidas na ordem exata mostrada:</span><span class="sxs-lookup"><span data-stu-id="0e76b-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="0e76b-133">Controle de Versão Semântico 2.0.0</span><span class="sxs-lookup"><span data-stu-id="0e76b-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="0e76b-134">Com o NuGet 4.3.0+ e o Visual Studio 2017 versão 15.3+, o NuGet oferece suporte ao [Controle de Versão Semântico 2.0.0](https://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="0e76b-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="0e76b-135">Determinadas semânticas do SemVer v2.0.0 não têm suporte em clientes mais antigos.</span><span class="sxs-lookup"><span data-stu-id="0e76b-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="0e76b-136">O NuGet considerará uma versão do pacote como SemVer v2.0.0 específica se qualquer uma das seguintes afirmações for verdadeira:</span><span class="sxs-lookup"><span data-stu-id="0e76b-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="0e76b-137">O rótulo de pré-lançamento é separado por pontos, por exemplo, *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="0e76b-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="0e76b-138">A versão tem metadados de build, por exemplo, *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="0e76b-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="0e76b-139">Para nuget.org, um pacote será definido como um pacote SemVer v2.0.0 se qualquer uma das seguintes afirmações for verdadeira:</span><span class="sxs-lookup"><span data-stu-id="0e76b-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="0e76b-140">A versão do pacote é compatível com SemVer v2.0.0, mas não compatível com SemVer v1.0.0, conforme definido acima.</span><span class="sxs-lookup"><span data-stu-id="0e76b-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="0e76b-141">Qualquer um dos intervalos de versão de dependência do pacote tem uma versão mínima ou máxima que é compatível com SemVer v2.0.0, mas não compatível com SemVer v1.0.0, definida acima; por exemplo, *[1.0.0-alpha.1, )* .</span><span class="sxs-lookup"><span data-stu-id="0e76b-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )* .</span></span>

<span data-ttu-id="0e76b-142">Se você carregar um pacote específico do SemVer v2.0.0 para o nuget.org, o pacote ficará invisível para os clientes mais antigos e estará disponível apenas para os seguintes clientes do NuGet:</span><span class="sxs-lookup"><span data-stu-id="0e76b-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="0e76b-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="0e76b-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="0e76b-144">Versão do Visual Studio 2017 15.3+</span><span class="sxs-lookup"><span data-stu-id="0e76b-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="0e76b-145">Visual Studio 2015 com [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="0e76b-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="0e76b-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="0e76b-146">dotnet</span></span>
  - <span data-ttu-id="0e76b-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="0e76b-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="0e76b-148">Clientes de terceiros:</span><span class="sxs-lookup"><span data-stu-id="0e76b-148">Third-party clients:</span></span>

- <span data-ttu-id="0e76b-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="0e76b-149">JetBrains Rider</span></span>
- <span data-ttu-id="0e76b-150">Paket versão 5.0+</span><span class="sxs-lookup"><span data-stu-id="0e76b-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a><span data-ttu-id="0e76b-151">Intervalos de versão</span><span class="sxs-lookup"><span data-stu-id="0e76b-151">Version ranges</span></span>

<span data-ttu-id="0e76b-152">Ao se referir a dependências de pacote, o NuGet oferece suporte ao uso de notação de intervalo para especificar intervalos de versão, resumidos da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="0e76b-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="0e76b-153">Notation</span><span class="sxs-lookup"><span data-stu-id="0e76b-153">Notation</span></span> | <span data-ttu-id="0e76b-154">Regra aplicada</span><span class="sxs-lookup"><span data-stu-id="0e76b-154">Applied rule</span></span> | <span data-ttu-id="0e76b-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="0e76b-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="0e76b-156">1.0</span><span class="sxs-lookup"><span data-stu-id="0e76b-156">1.0</span></span> | <span data-ttu-id="0e76b-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="0e76b-157">x ≥ 1.0</span></span> | <span data-ttu-id="0e76b-158">Versão mínima, inclusiva</span><span class="sxs-lookup"><span data-stu-id="0e76b-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="0e76b-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="0e76b-159">(1.0,)</span></span> | <span data-ttu-id="0e76b-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="0e76b-160">x > 1.0</span></span> | <span data-ttu-id="0e76b-161">Versão mínima, exclusiva</span><span class="sxs-lookup"><span data-stu-id="0e76b-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="0e76b-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="0e76b-162">[1.0]</span></span> | <span data-ttu-id="0e76b-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="0e76b-163">x == 1.0</span></span> | <span data-ttu-id="0e76b-164">Correspondência exata da versão</span><span class="sxs-lookup"><span data-stu-id="0e76b-164">Exact version match</span></span> |
| <span data-ttu-id="0e76b-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="0e76b-165">(,1.0]</span></span> | <span data-ttu-id="0e76b-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="0e76b-166">x ≤ 1.0</span></span> | <span data-ttu-id="0e76b-167">Versão máxima, inclusiva</span><span class="sxs-lookup"><span data-stu-id="0e76b-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="0e76b-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="0e76b-168">(,1.0)</span></span> | <span data-ttu-id="0e76b-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="0e76b-169">x < 1.0</span></span> | <span data-ttu-id="0e76b-170">Versão máxima, exclusiva</span><span class="sxs-lookup"><span data-stu-id="0e76b-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="0e76b-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="0e76b-171">[1.0,2.0]</span></span> | <span data-ttu-id="0e76b-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="0e76b-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="0e76b-173">Intervalo exato, inclusivo</span><span class="sxs-lookup"><span data-stu-id="0e76b-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="0e76b-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="0e76b-174">(1.0,2.0)</span></span> | <span data-ttu-id="0e76b-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="0e76b-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="0e76b-176">Intervalo exato, exclusivo</span><span class="sxs-lookup"><span data-stu-id="0e76b-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="0e76b-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="0e76b-177">[1.0,2.0)</span></span> | <span data-ttu-id="0e76b-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="0e76b-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="0e76b-179">Versão mínima inclusiva e máxima exclusiva combinadas</span><span class="sxs-lookup"><span data-stu-id="0e76b-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="0e76b-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="0e76b-180">(1.0)</span></span>    | <span data-ttu-id="0e76b-181">inválido</span><span class="sxs-lookup"><span data-stu-id="0e76b-181">invalid</span></span> | <span data-ttu-id="0e76b-182">inválido</span><span class="sxs-lookup"><span data-stu-id="0e76b-182">invalid</span></span> |

<span data-ttu-id="0e76b-183">Ao usar o formato PackageReference, o NuGet também dá suporte ao uso de uma notação flutuante, \* para as partes de sufixo principal, secundária, patch e de pré-lançamento do número.</span><span class="sxs-lookup"><span data-stu-id="0e76b-183">When using the PackageReference format, NuGet also supports using a floating notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="0e76b-184">Não há suporte para versões flutuantes com o `packages.config` formato.</span><span class="sxs-lookup"><span data-stu-id="0e76b-184">Floating versions are not supported with the `packages.config` format.</span></span> <span data-ttu-id="0e76b-185">Quando uma versão flutuante é especificada, a regra é resolver para a versão existente mais alta que corresponde à descrição da versão.</span><span class="sxs-lookup"><span data-stu-id="0e76b-185">When a floating version is specified, the rule is to resolve to the highest existent version that matches the version description.</span></span> <span data-ttu-id="0e76b-186">Os exemplos de versões flutuantes e as resoluções estão abaixo.</span><span class="sxs-lookup"><span data-stu-id="0e76b-186">Examples of floating versions and the resolutions are below.</span></span>

> [!Note]
> <span data-ttu-id="0e76b-187">Os intervalos de versão no PackageReference incluem versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="0e76b-187">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="0e76b-188">Por design, versões flutuantes não resolvem as versões de pré-lançamento, a menos que sejam aceitas.</span><span class="sxs-lookup"><span data-stu-id="0e76b-188">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="0e76b-189">Para obter o status da solicitação de recurso relacionada, confira [Problema 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="0e76b-189">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="0e76b-190">Exemplos</span><span class="sxs-lookup"><span data-stu-id="0e76b-190">Examples</span></span>

<span data-ttu-id="0e76b-191">Sempre especifique uma versão ou intervalo de versão para dependências de pacote em arquivos de projeto, arquivos `packages.config` e arquivos `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="0e76b-191">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="0e76b-192">Sem uma versão ou intervalo de versão, o NuGet 2.8.x e versões anteriores escolhem a versão do pacote disponível mais recente ao resolver uma dependência, enquanto o NuGet 3.xe posterior escolhe a versão de pacote mais baixa.</span><span class="sxs-lookup"><span data-stu-id="0e76b-192">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="0e76b-193">Especificar uma versão ou um intervalo de versões evita essa incerteza.</span><span class="sxs-lookup"><span data-stu-id="0e76b-193">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="0e76b-194">Referências em arquivos de projeto (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="0e76b-194">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version.
     Will resolve to the highest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. 
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. 
     Will resolve to the smallest acceptable stable version.
     -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher.
     Will resolve to the smallest acceptable stable version. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

#### <a name="floating-version-resolutions"></a><span data-ttu-id="0e76b-195">Resoluções de versão flutuante</span><span class="sxs-lookup"><span data-stu-id="0e76b-195">Floating version resolutions</span></span> 

| <span data-ttu-id="0e76b-196">Versão</span><span class="sxs-lookup"><span data-stu-id="0e76b-196">Version</span></span> | <span data-ttu-id="0e76b-197">Versões presentes no servidor</span><span class="sxs-lookup"><span data-stu-id="0e76b-197">Versions present on server</span></span> | <span data-ttu-id="0e76b-198">Resolução</span><span class="sxs-lookup"><span data-stu-id="0e76b-198">Resolution</span></span> | <span data-ttu-id="0e76b-199">Motivo</span><span class="sxs-lookup"><span data-stu-id="0e76b-199">Reason</span></span> | <span data-ttu-id="0e76b-200">Observações</span><span class="sxs-lookup"><span data-stu-id="0e76b-200">Notes</span></span> |
|----------|--------------|-------------|-------------|-------------|
| * | <span data-ttu-id="0e76b-201">1.1.0</span><span class="sxs-lookup"><span data-stu-id="0e76b-201">1.1.0</span></span> <br> <span data-ttu-id="0e76b-202">1.1.1</span><span class="sxs-lookup"><span data-stu-id="0e76b-202">1.1.1</span></span> <br> <span data-ttu-id="0e76b-203">1.2.0</span><span class="sxs-lookup"><span data-stu-id="0e76b-203">1.2.0</span></span> <br> <span data-ttu-id="0e76b-204">1.3.0-Alpha</span><span class="sxs-lookup"><span data-stu-id="0e76b-204">1.3.0-alpha</span></span>  | <span data-ttu-id="0e76b-205">1.2.0</span><span class="sxs-lookup"><span data-stu-id="0e76b-205">1.2.0</span></span> | <span data-ttu-id="0e76b-206">A versão estável mais alta.</span><span class="sxs-lookup"><span data-stu-id="0e76b-206">The highest stable version.</span></span> |
| <span data-ttu-id="0e76b-207">1,1. \*</span><span class="sxs-lookup"><span data-stu-id="0e76b-207">1.1.\*</span></span> | <span data-ttu-id="0e76b-208">1.1.0</span><span class="sxs-lookup"><span data-stu-id="0e76b-208">1.1.0</span></span> <br> <span data-ttu-id="0e76b-209">1.1.1</span><span class="sxs-lookup"><span data-stu-id="0e76b-209">1.1.1</span></span> <br> <span data-ttu-id="0e76b-210">1.1.2-alfa</span><span class="sxs-lookup"><span data-stu-id="0e76b-210">1.1.2-alpha</span></span> <br> <span data-ttu-id="0e76b-211">1.2.0-Alpha</span><span class="sxs-lookup"><span data-stu-id="0e76b-211">1.2.0-alpha</span></span> | <span data-ttu-id="0e76b-212">1.1.1</span><span class="sxs-lookup"><span data-stu-id="0e76b-212">1.1.1</span></span> | <span data-ttu-id="0e76b-213">A versão estável mais alta que respeita o padrão especificado.</span><span class="sxs-lookup"><span data-stu-id="0e76b-213">The highest stable version that respects the specified pattern.</span></span>|
| <span data-ttu-id="0e76b-214">\* - \*</span><span class="sxs-lookup"><span data-stu-id="0e76b-214">\* - \*</span></span> | <span data-ttu-id="0e76b-215">1.1.0</span><span class="sxs-lookup"><span data-stu-id="0e76b-215">1.1.0</span></span> <br> <span data-ttu-id="0e76b-216">1.1.1</span><span class="sxs-lookup"><span data-stu-id="0e76b-216">1.1.1</span></span> <br> <span data-ttu-id="0e76b-217">1.1.2-alfa</span><span class="sxs-lookup"><span data-stu-id="0e76b-217">1.1.2-alpha</span></span> <br> <span data-ttu-id="0e76b-218">1.3.0-beta</span><span class="sxs-lookup"><span data-stu-id="0e76b-218">1.3.0-beta</span></span>  | <span data-ttu-id="0e76b-219">1.3.0-beta</span><span class="sxs-lookup"><span data-stu-id="0e76b-219">1.3.0-beta</span></span> | <span data-ttu-id="0e76b-220">A versão mais alta, incluindo as versões não estáveis.</span><span class="sxs-lookup"><span data-stu-id="0e76b-220">The highest version including the not stable versions.</span></span> | <span data-ttu-id="0e76b-221">Disponível no Visual Studio versão 16,6, NuGet versão 5,6, SDK do .NET Core versão 3.1.300</span><span class="sxs-lookup"><span data-stu-id="0e76b-221">Available in Visual Studio version 16.6, NuGet version 5.6, .NET Core SDK version 3.1.300</span></span> |
| <span data-ttu-id="0e76b-222">1,1. *-*</span><span class="sxs-lookup"><span data-stu-id="0e76b-222">1.1.\* - \*</span></span> | <span data-ttu-id="0e76b-223">1.1.0</span><span class="sxs-lookup"><span data-stu-id="0e76b-223">1.1.0</span></span> <br> <span data-ttu-id="0e76b-224">1.1.1</span><span class="sxs-lookup"><span data-stu-id="0e76b-224">1.1.1</span></span> <br> <span data-ttu-id="0e76b-225">1.1.2-alfa</span><span class="sxs-lookup"><span data-stu-id="0e76b-225">1.1.2-alpha</span></span> <br> <span data-ttu-id="0e76b-226">1.1.2-beta</span><span class="sxs-lookup"><span data-stu-id="0e76b-226">1.1.2-beta</span></span> <br> <span data-ttu-id="0e76b-227">1.3.0-beta</span><span class="sxs-lookup"><span data-stu-id="0e76b-227">1.3.0-beta</span></span>  | <span data-ttu-id="0e76b-228">1.1.2-beta</span><span class="sxs-lookup"><span data-stu-id="0e76b-228">1.1.2-beta</span></span> | <span data-ttu-id="0e76b-229">A versão mais alta que respeita o padrão e inclui as versões não estáveis.</span><span class="sxs-lookup"><span data-stu-id="0e76b-229">The highest version respecting the pattern and including the not stable versions.</span></span> | <span data-ttu-id="0e76b-230">Disponível no Visual Studio versão 16,6, NuGet versão 5,6, SDK do .NET Core versão 3.1.300</span><span class="sxs-lookup"><span data-stu-id="0e76b-230">Available in Visual Studio version 16.6, NuGet version 5.6, .NET Core SDK version 3.1.300</span></span> |

<span data-ttu-id="0e76b-231">**Referências em `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="0e76b-231">**References in `packages.config`:**</span></span>

<span data-ttu-id="0e76b-232">Em `packages.config`, toda dependência é listada com um atributo de `version` exato que é usado ao restaurar pacotes.</span><span class="sxs-lookup"><span data-stu-id="0e76b-232">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="0e76b-233">O atributo `allowedVersions` é usado apenas durante as operações de atualização para restringir as versões às quais o pacote pode ser atualizado.</span><span class="sxs-lookup"><span data-stu-id="0e76b-233">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="0e76b-234">**Referências em arquivos `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="0e76b-234">**References in `.nuspec` files**</span></span>

<span data-ttu-id="0e76b-235">O atributo `version` em um elemento `<dependency>` descreve as versões de intervalo aceitáveis ​​para uma dependência.</span><span class="sxs-lookup"><span data-stu-id="0e76b-235">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="0e76b-236">Números de versão normalizados</span><span class="sxs-lookup"><span data-stu-id="0e76b-236">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="0e76b-237">Essa é uma alteração significativa para o NuGet 3.4 e posterior.</span><span class="sxs-lookup"><span data-stu-id="0e76b-237">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="0e76b-238">Ao obter pacotes de um repositório durante a instalação, reinstalação ou restauração de operações, o NuGet 3.4+ trata os números de versão da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0e76b-238">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="0e76b-239">Zeros à esquerda são removidos dos números de versão:</span><span class="sxs-lookup"><span data-stu-id="0e76b-239">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="0e76b-240">um zero na quarta parte do número de versão será omitido</span><span class="sxs-lookup"><span data-stu-id="0e76b-240">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1
        
- <span data-ttu-id="0e76b-241">SemVer os metadados de compilação 2.0.0 são removidos</span><span class="sxs-lookup"><span data-stu-id="0e76b-241">SemVer 2.0.0 build metadata is removed</span></span>

        1.0.7+r3456 is treated as 1.0.7

<span data-ttu-id="0e76b-242">As operações `pack` e `restore` normalizam as versões sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="0e76b-242">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="0e76b-243">Para pacotes já compilados, essa normalização não afeta os números de versão nos próprios pacotes; ela afeta apenas como o NuGet faz a correspondência das versões ao resolver dependências.</span><span class="sxs-lookup"><span data-stu-id="0e76b-243">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="0e76b-244">No entanto, os repositórios de pacotes do NuGet devem tratar esses valores da mesma maneira que o NuGet para evitar a duplicação da versão do pacote.</span><span class="sxs-lookup"><span data-stu-id="0e76b-244">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="0e76b-245">Portanto, um repositório que contenha a versão *1.0* de um pacote não deve hospedar também a versão *1.0.0* como um pacote separado e diferente.</span><span class="sxs-lookup"><span data-stu-id="0e76b-245">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
