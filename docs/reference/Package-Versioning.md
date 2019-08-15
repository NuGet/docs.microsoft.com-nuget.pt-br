---
title: Referência de versão do pacote NuGet
description: Detalhes exatos sobre a especificação de números de versão e intervalos para outros pacotes sobre os quais um pacote NuGet depende e como as dependências são instaladas.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69019991"
---
# <a name="package-versioning"></a><span data-ttu-id="9be91-103">Controle de versão do pacote</span><span class="sxs-lookup"><span data-stu-id="9be91-103">Package versioning</span></span>

<span data-ttu-id="9be91-104">Um pacote específico sempre é referenciado usando seu identificador de pacote e um número de versão exato.</span><span class="sxs-lookup"><span data-stu-id="9be91-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="9be91-105">Por exemplo, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) no NuGet.org tem várias dúzias de pacotes específicos disponíveis, variando da versão *4.1.10311* para a versão *6.1.3* (a versão estável mais recente) e uma variedade de versões de pré-lançamento como *6.2.0-beta1* .</span><span class="sxs-lookup"><span data-stu-id="9be91-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="9be91-106">Ao criar um pacote, você atribui um número de versão específico com um sufixo de texto de pré-lançamento opcional.</span><span class="sxs-lookup"><span data-stu-id="9be91-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="9be91-107">Ao consumir pacotes, por outro lado, você pode especificar um número de versão exato ou um intervalo de versões aceitáveis.</span><span class="sxs-lookup"><span data-stu-id="9be91-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="9be91-108">Neste tópico:</span><span class="sxs-lookup"><span data-stu-id="9be91-108">In this topic:</span></span>

- <span data-ttu-id="9be91-109">[Noções básicas de versão](#version-basics) , incluindo sufixos de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="9be91-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="9be91-110">Intervalos de versão e curingas</span><span class="sxs-lookup"><span data-stu-id="9be91-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="9be91-111">Números de versão normalizados</span><span class="sxs-lookup"><span data-stu-id="9be91-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="9be91-112">Noções básicas da versão</span><span class="sxs-lookup"><span data-stu-id="9be91-112">Version basics</span></span>

<span data-ttu-id="9be91-113">Um número de versão específico está no formato *Major. Minor. patch [-suffix]* , em que os componentes têm os seguintes significados:</span><span class="sxs-lookup"><span data-stu-id="9be91-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="9be91-114">*Principal*: Alterações da falha</span><span class="sxs-lookup"><span data-stu-id="9be91-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="9be91-115">*Secundária*: Novos recursos, mas compatível com versões anteriores</span><span class="sxs-lookup"><span data-stu-id="9be91-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="9be91-116">*Patch*: Somente correções de bug compatíveis com versões anteriores</span><span class="sxs-lookup"><span data-stu-id="9be91-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="9be91-117">*-Sufixo* (opcional): um hífen seguido por uma cadeia de caracteres que denota uma versão de pré-lançamento (seguindo a [Convenção de controle de versão semântico ou SemVer 1,0](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="9be91-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="9be91-118">**Disso**</span><span class="sxs-lookup"><span data-stu-id="9be91-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="9be91-119">nuget.org rejeita qualquer upload de pacote que não tem um número de versão exato.</span><span class="sxs-lookup"><span data-stu-id="9be91-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="9be91-120">A versão deve ser especificada no arquivo `.nuspec` de projeto ou usado para criar o pacote.</span><span class="sxs-lookup"><span data-stu-id="9be91-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="9be91-121">Versões de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="9be91-121">Pre-release versions</span></span>

<span data-ttu-id="9be91-122">Tecnicamente, os criadores de pacote podem usar qualquer cadeia de caracteres como um sufixo para denotar uma versão de pré-lançamento, pois o NuGet trata dessa versão como pré-lançamento e não faz outra interpretação.</span><span class="sxs-lookup"><span data-stu-id="9be91-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="9be91-123">Ou seja, o NuGet exibe a cadeia de caracteres da versão completa em qualquer interface do usuário envolvida, deixando qualquer interpretação do significado do sufixo para o consumidor.</span><span class="sxs-lookup"><span data-stu-id="9be91-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="9be91-124">Dito isso, os desenvolvedores de pacotes geralmente seguem as convenções de nomenclatura reconhecidas:</span><span class="sxs-lookup"><span data-stu-id="9be91-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="9be91-125">`-alpha`: Versão Alfa, normalmente usada para trabalho em andamento e experimentação.</span><span class="sxs-lookup"><span data-stu-id="9be91-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="9be91-126">`-beta`: Versão beta, normalmente uma completa com recursos para a próxima versão planejada, mas pode conter erros conhecidos.</span><span class="sxs-lookup"><span data-stu-id="9be91-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="9be91-127">`-rc`: Versão Release Candidate, normalmente uma versão que é potencialmente a final (estável), a menos que surjam bugs significativos.</span><span class="sxs-lookup"><span data-stu-id="9be91-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="9be91-128">O NuGet 4.3.0 + dá suporte a [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), que dá suporte a números de pré-lançamento com notação de ponto, como em *1.0.1-Build. 23*.</span><span class="sxs-lookup"><span data-stu-id="9be91-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="9be91-129">A notação de ponto não e compatível com as versões do NuGet anteriores à 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="9be91-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="9be91-130">Você pode usar um formulário como o *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="9be91-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="9be91-131">Ao resolver referências de pacote e várias versões de pacote diferem somente por sufixo, o NuGet escolhe uma versão sem um sufixo primeiro e aplica precedência às versões de pré-lançamento em ordem alfabética inversa.</span><span class="sxs-lookup"><span data-stu-id="9be91-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="9be91-132">Por exemplo, as seguintes versões seriam escolhidas na ordem exata mostrada:</span><span class="sxs-lookup"><span data-stu-id="9be91-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="9be91-133">2\.0.0 de controle de versão semântico</span><span class="sxs-lookup"><span data-stu-id="9be91-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="9be91-134">Com o NuGet 4.3.0 + e o Visual Studio 2017 versão 15.3 +, o NuGet dá suporte à [2.0.0 semântica de controle de versão](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="9be91-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="9be91-135">Não há suporte para determinadas semânticas de SemVer v 2.0.0 em clientes mais antigos.</span><span class="sxs-lookup"><span data-stu-id="9be91-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="9be91-136">O NuGet considera uma versão de pacote como SemVer v 2.0.0 específica se qualquer uma das seguintes instruções for verdadeira:</span><span class="sxs-lookup"><span data-stu-id="9be91-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="9be91-137">O rótulo de pré-lançamento é separado por ponto, por exemplo, *1.0.0-Alpha. 1*</span><span class="sxs-lookup"><span data-stu-id="9be91-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="9be91-138">A versão tem metadados de compilação, por exemplo, *1.0.0 + githash*</span><span class="sxs-lookup"><span data-stu-id="9be91-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="9be91-139">Para nuget.org, um pacote é definido como um pacote SemVer v 2.0.0 se uma das seguintes instruções for verdadeira:</span><span class="sxs-lookup"><span data-stu-id="9be91-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="9be91-140">A versão do pacote é em conformidade com o SemVer v 2.0.0, mas não com o SemVer v 1.0.0 em conformidade, conforme definido acima.</span><span class="sxs-lookup"><span data-stu-id="9be91-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="9be91-141">Qualquer um dos intervalos de versão de dependência do pacote tem uma versão mínima ou máxima que está em conformidade com o SemVer v 2.0.0, mas não com o SemVer v 1.0.0 em conformidade, definido acima; por exemplo, *[1.0.0-Alpha. 1,)* .</span><span class="sxs-lookup"><span data-stu-id="9be91-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="9be91-142">Se você carregar um pacote específico do SemVer v 2.0.0 no nuget.org, o pacote será invisível para clientes mais antigos e estará disponível apenas para os seguintes clientes do NuGet:</span><span class="sxs-lookup"><span data-stu-id="9be91-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="9be91-143">NuGet 4.3.0 +</span><span class="sxs-lookup"><span data-stu-id="9be91-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="9be91-144">Visual Studio 2017 versão 15.3 +</span><span class="sxs-lookup"><span data-stu-id="9be91-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="9be91-145">Visual Studio 2015 com [NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="9be91-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="9be91-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="9be91-146">dotnet</span></span>
  - <span data-ttu-id="9be91-147">dotnetcore. exe (SDK do .NET 2.0.0 +)</span><span class="sxs-lookup"><span data-stu-id="9be91-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="9be91-148">Clientes de terceiros:</span><span class="sxs-lookup"><span data-stu-id="9be91-148">Third-party clients:</span></span>

- <span data-ttu-id="9be91-149">Cláusula JetBrains</span><span class="sxs-lookup"><span data-stu-id="9be91-149">JetBrains Rider</span></span>
- <span data-ttu-id="9be91-150">Paket versão 5.0 +</span><span class="sxs-lookup"><span data-stu-id="9be91-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="9be91-151">Intervalos de versão e curingas</span><span class="sxs-lookup"><span data-stu-id="9be91-151">Version ranges and wildcards</span></span>

<span data-ttu-id="9be91-152">Ao fazer referência a dependências de pacote, o NuGet dá suporte ao uso de notação de intervalo para especificar intervalos de versão, resumido da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9be91-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="9be91-153">Notation</span><span class="sxs-lookup"><span data-stu-id="9be91-153">Notation</span></span> | <span data-ttu-id="9be91-154">Regra aplicada</span><span class="sxs-lookup"><span data-stu-id="9be91-154">Applied rule</span></span> | <span data-ttu-id="9be91-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="9be91-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="9be91-156">1.0</span><span class="sxs-lookup"><span data-stu-id="9be91-156">1.0</span></span> | <span data-ttu-id="9be91-157">x ≥ 1,0</span><span class="sxs-lookup"><span data-stu-id="9be91-157">x ≥ 1.0</span></span> | <span data-ttu-id="9be91-158">Versão mínima, inclusiva</span><span class="sxs-lookup"><span data-stu-id="9be91-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="9be91-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="9be91-159">(1.0,)</span></span> | <span data-ttu-id="9be91-160">x > 1,0</span><span class="sxs-lookup"><span data-stu-id="9be91-160">x > 1.0</span></span> | <span data-ttu-id="9be91-161">Versão mínima, exclusiva</span><span class="sxs-lookup"><span data-stu-id="9be91-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="9be91-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="9be91-162">[1.0]</span></span> | <span data-ttu-id="9be91-163">x = = 1,0</span><span class="sxs-lookup"><span data-stu-id="9be91-163">x == 1.0</span></span> | <span data-ttu-id="9be91-164">Correspondência de versão exata</span><span class="sxs-lookup"><span data-stu-id="9be91-164">Exact version match</span></span> |
| <span data-ttu-id="9be91-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="9be91-165">(,1.0]</span></span> | <span data-ttu-id="9be91-166">x ≤ 1,0</span><span class="sxs-lookup"><span data-stu-id="9be91-166">x ≤ 1.0</span></span> | <span data-ttu-id="9be91-167">Versão máxima, inclusiva</span><span class="sxs-lookup"><span data-stu-id="9be91-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="9be91-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="9be91-168">(,1.0)</span></span> | <span data-ttu-id="9be91-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="9be91-169">x < 1.0</span></span> | <span data-ttu-id="9be91-170">Versão máxima, exclusiva</span><span class="sxs-lookup"><span data-stu-id="9be91-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="9be91-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="9be91-171">[1.0,2.0]</span></span> | <span data-ttu-id="9be91-172">1,0 ≤ x ≤ 2,0</span><span class="sxs-lookup"><span data-stu-id="9be91-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="9be91-173">Intervalo exato, inclusivo</span><span class="sxs-lookup"><span data-stu-id="9be91-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="9be91-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="9be91-174">(1.0,2.0)</span></span> | <span data-ttu-id="9be91-175">1,0 < x < 2,0</span><span class="sxs-lookup"><span data-stu-id="9be91-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="9be91-176">Intervalo exato, exclusivo</span><span class="sxs-lookup"><span data-stu-id="9be91-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="9be91-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="9be91-177">[1.0,2.0)</span></span> | <span data-ttu-id="9be91-178">1,0 ≤ x < 2,0</span><span class="sxs-lookup"><span data-stu-id="9be91-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="9be91-179">Versão mínima inclusiva e exclusiva misturada</span><span class="sxs-lookup"><span data-stu-id="9be91-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="9be91-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="9be91-180">(1.0)</span></span>    | <span data-ttu-id="9be91-181">inválidos</span><span class="sxs-lookup"><span data-stu-id="9be91-181">invalid</span></span> | <span data-ttu-id="9be91-182">inválidos</span><span class="sxs-lookup"><span data-stu-id="9be91-182">invalid</span></span> |

<span data-ttu-id="9be91-183">Ao usar o formato PackageReference, o NuGet também dá suporte ao uso de \*uma notação curinga, para as partes de sufixo principal, secundária, patch e de pré-lançamento do número.</span><span class="sxs-lookup"><span data-stu-id="9be91-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="9be91-184">Não há suporte para caracteres curinga com `packages.config` o formato.</span><span class="sxs-lookup"><span data-stu-id="9be91-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="9be91-185">Os intervalos de versão no PackageReference incluem versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="9be91-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="9be91-186">Por design, as versões flutuantes não resolvem versões de pré-lançamento, a menos que tenham optado por.</span><span class="sxs-lookup"><span data-stu-id="9be91-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="9be91-187">Para obter o status da solicitação de recurso relacionada, consulte o [problema 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="9be91-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="9be91-188">Exemplos</span><span class="sxs-lookup"><span data-stu-id="9be91-188">Examples</span></span>

<span data-ttu-id="9be91-189">Sempre especifique uma versão ou intervalo de versão para dependências de pacote em `packages.config` arquivos de projeto `.nuspec` , arquivos e arquivos.</span><span class="sxs-lookup"><span data-stu-id="9be91-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="9be91-190">Sem uma versão ou intervalo de versão, o NuGet 2.8. x e anterior escolhe a versão de pacote mais recente disponível ao resolver uma dependência, enquanto o NuGet 3. x e posterior escolhe a versão de pacote mais baixa.</span><span class="sxs-lookup"><span data-stu-id="9be91-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="9be91-191">A especificação de uma versão ou intervalo de versão evita essa incerteza.</span><span class="sxs-lookup"><span data-stu-id="9be91-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="9be91-192">Referências em arquivos de projeto (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="9be91-192">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="9be91-193">**Referências em `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="9be91-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="9be91-194">No `packages.config`, cada dependência é listada com um `version` atributo exato que é usado durante a restauração de pacotes.</span><span class="sxs-lookup"><span data-stu-id="9be91-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="9be91-195">O `allowedVersions` atributo é usado somente durante operações de atualização para restringir as versões para as quais o pacote pode ser atualizado.</span><span class="sxs-lookup"><span data-stu-id="9be91-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="9be91-196">**Referências em `.nuspec` arquivos**</span><span class="sxs-lookup"><span data-stu-id="9be91-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="9be91-197">O `version` atributo em um `<dependency>` elemento descreve as versões de intervalo aceitáveis para uma dependência.</span><span class="sxs-lookup"><span data-stu-id="9be91-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="9be91-198">Números de versão normalizados</span><span class="sxs-lookup"><span data-stu-id="9be91-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="9be91-199">Essa é uma alteração significativa para o NuGet 3,4 e posterior.</span><span class="sxs-lookup"><span data-stu-id="9be91-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="9be91-200">Ao obter pacotes de um repositório durante as operações de instalação, reinstalação ou restauração, o NuGet 3.4 + trata os números de versão da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9be91-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="9be91-201">Os zeros à esquerda são removidos dos números de versão:</span><span class="sxs-lookup"><span data-stu-id="9be91-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="9be91-202">Um zero na quarta parte do número de versão será omitido</span><span class="sxs-lookup"><span data-stu-id="9be91-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="9be91-203">`pack`e `restore` as operações normalizam versões sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="9be91-203">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="9be91-204">Para pacotes já compilados, essa normalização não afeta os números de versão nos próprios pacotes; Ele afeta apenas o modo como o NuGet corresponde às versões ao resolver as dependências.</span><span class="sxs-lookup"><span data-stu-id="9be91-204">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="9be91-205">No entanto, os repositórios do pacote NuGet devem tratar esses valores da mesma forma que o NuGet para impedir a duplicação da versão do pacote.</span><span class="sxs-lookup"><span data-stu-id="9be91-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="9be91-206">Portanto, um repositório que contém a versão *1,0* de um pacote também não deve hospedar a versão *1.0.0* como um pacote separado e diferente.</span><span class="sxs-lookup"><span data-stu-id="9be91-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
