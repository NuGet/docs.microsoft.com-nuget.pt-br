---
title: Versões de pré-lançamento em pacotes do NuGet
description: Diretrizes para compilar pacotes de pré-lançamento
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 696f51905198defdbfd475ba7d010ac3e27ac557
ms.sourcegitcommit: 3fc93f7a64be040699fe12125977dd25a7948470
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64877938"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="9ff85-103">Compilando pacotes de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="9ff85-103">Building pre-release packages</span></span>

<span data-ttu-id="9ff85-104">Sempre que você liberar um pacote atualizado com um novo número de versão, o NuGet considerará esse como a “última versão estável” conforme mostrado, por exemplo, na interface do usuário do Gerenciador de Pacotes no Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="9ff85-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![A interface do usuário do Gerenciador de Pacotes mostrando a versão estável mais recente](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="9ff85-106">Uma versão estável é aquela que é considerado confiável suficiente para ser usada na produção.</span><span class="sxs-lookup"><span data-stu-id="9ff85-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="9ff85-107">A versão estável mais recente também é aquela que será instalada como uma atualização de pacote ou durante a restauração do pacote (sujeito a restrições, conforme descrito em [Reinstalando e atualizando pacotes](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="9ff85-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="9ff85-108">Para dar suporte ao ciclo de vida de versão de software, o NuGet 1.6 e posterior permite a distribuição de pacotes de pré-lançamento, em que o número de versão inclui um sufixo de controle de versão semântico como `-alpha`, `-beta` ou `-rc`.</span><span class="sxs-lookup"><span data-stu-id="9ff85-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="9ff85-109">Para obter mais informações, consulte [Controle de versão de pacote](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="9ff85-109">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="9ff85-110">Você pode especificar essas versões de três maneiras:</span><span class="sxs-lookup"><span data-stu-id="9ff85-110">You can specify such versions in three ways:</span></span>

- <span data-ttu-id="9ff85-111">Arquivo `.nuspec`: inclua o sufixo de versão semântico no elemento `version`:</span><span class="sxs-lookup"><span data-stu-id="9ff85-111">`.nuspec` file: include the semantic version suffix in the `version` element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

- <span data-ttu-id="9ff85-112">Arquivo `.csproj`: inclua o sufixo de versão semântico no elemento `PackageVersion`:</span><span class="sxs-lookup"><span data-stu-id="9ff85-112">`.csproj` file: include the semantic version suffix in the `PackageVersion` element:</span></span>

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- <span data-ttu-id="9ff85-113">Atributos de assembly: especifique a versão usando `AssemblyInformationalVersionAttribute`:</span><span class="sxs-lookup"><span data-stu-id="9ff85-113">Assembly attributes: specify the version using `AssemblyInformationalVersionAttribute`:</span></span>

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    <span data-ttu-id="9ff85-114">O NuGet adota esse valor em vez daquele especificado no atributo `AssemblyVersion`, que não é compatível com o controle de versão semântico.</span><span class="sxs-lookup"><span data-stu-id="9ff85-114">NuGet picks up this value instead of the one specified in the `AssemblyVersion` attribute, which does not support semantic versioning.</span></span>

<span data-ttu-id="9ff85-115">Quando você estiver pronto para lançar uma versão estável, basta remover o sufixo e o pacote terá precedência sobre as versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="9ff85-115">When you’re ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="9ff85-116">Novamente, consulte [Controle de versão do pacote](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="9ff85-116">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="9ff85-117">Instalando e atualizando pacotes de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="9ff85-117">Installing and updating pre-release packages</span></span>

<span data-ttu-id="9ff85-118">Por padrão, o NuGet não inclui as versões de pré-lançamento ao trabalhar com pacotes, mas você pode alterar esse comportamento da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9ff85-118">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="9ff85-119">**Interface do Usuário do Gerenciador de Pacotes no Visual Studio**: na Interface do Usuário **Gerenciar pacotes NuGet**, marque a caixa de seleção **Incluir pré-lançamento**:</span><span class="sxs-lookup"><span data-stu-id="9ff85-119">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![A caixa de seleção Incluir pré-lançamento no Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="9ff85-121">Definir ou desmarcar esta caixa atualizará a interface do usuário do Gerenciador de Pacotes e a lista de versões disponíveis que você pode instalar.</span><span class="sxs-lookup"><span data-stu-id="9ff85-121">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="9ff85-122">**Console do Gerenciador de Pacotes**: Use a opção `-IncludePrerelease` com os comandos `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` e `Update-Package`.</span><span class="sxs-lookup"><span data-stu-id="9ff85-122">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="9ff85-123">Consulte a [Referência do PowerShell](../tools/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="9ff85-123">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="9ff85-124">**CLI do NuGet**: Use a opção `-prerelease` com os comandos `install`, `update`, `delete` e `mirror`.</span><span class="sxs-lookup"><span data-stu-id="9ff85-124">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="9ff85-125">Consulte a [referência da CLI do NuGet](../tools/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="9ff85-125">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="9ff85-126">Controle de versão semântico</span><span class="sxs-lookup"><span data-stu-id="9ff85-126">Semantic versioning</span></span>

<span data-ttu-id="9ff85-127">O [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) (Controle de versão semântico ou convenção de SemVer) descreve como utilizar as cadeias de caracteres em números de versão para expressar o significado do código subjacente.</span><span class="sxs-lookup"><span data-stu-id="9ff85-127">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="9ff85-128">Nesta convenção, cada versão tem três partes, `Major.Minor.Patch`, com o seguinte significado:</span><span class="sxs-lookup"><span data-stu-id="9ff85-128">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="9ff85-129">`Major`: Alterações da falha</span><span class="sxs-lookup"><span data-stu-id="9ff85-129">`Major`: Breaking changes</span></span>
- <span data-ttu-id="9ff85-130">`Minor`: Novos recursos, mas compatível com versões anteriores</span><span class="sxs-lookup"><span data-stu-id="9ff85-130">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="9ff85-131">`Patch`: Somente correções de bug compatíveis com versões anteriores</span><span class="sxs-lookup"><span data-stu-id="9ff85-131">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="9ff85-132">As versões de pré-lançamento são indicadas acrescentando um hífen e uma cadeia de caracteres após o número de patch.</span><span class="sxs-lookup"><span data-stu-id="9ff85-132">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="9ff85-133">Tecnicamente, é possível usar *qualquer* cadeia de caracteres após o hífen e o NuGet tratará o pacote como a versão de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="9ff85-133">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="9ff85-134">O NuGet exibe, então, o número de versão completa na interface do usuário aplicável, deixando os consumidores para interpretar o significado por si mesmos.</span><span class="sxs-lookup"><span data-stu-id="9ff85-134">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="9ff85-135">Considerando isso, geralmente é aconselhável seguir as convenções de nomenclatura reconhecidas como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="9ff85-135">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="9ff85-136">`-alpha`: Versão alfa, normalmente usada para o trabalho e experimentação em andamento</span><span class="sxs-lookup"><span data-stu-id="9ff85-136">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="9ff85-137">`-beta`: Versão beta, normalmente uma completa com recursos para a próxima versão planejada, mas pode conter erros conhecidos.</span><span class="sxs-lookup"><span data-stu-id="9ff85-137">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="9ff85-138">`-rc`: Versão Release Candidate, normalmente uma versão que é potencialmente a final (estável), a menos que surjam bugs significativos.</span><span class="sxs-lookup"><span data-stu-id="9ff85-138">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="9ff85-139">O NuGet 4.3.0+ é compatível com o [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), que oferece compatibilidade com números com notação de ponto pré-lançamento, como no `1.0.1-build.23`.</span><span class="sxs-lookup"><span data-stu-id="9ff85-139">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="9ff85-140">A notação de ponto não e compatível com as versões do NuGet anteriores à 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="9ff85-140">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="9ff85-141">Em versões anteriores do NuGet, você poderia usar um formulário como `1.0.1-build23`, mas ela sempre foi considerada uma versão de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="9ff85-141">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="9ff85-142">Qualquer sufixo que você usar, no entanto, receberá precedência do NuGet cem ordem alfabética inversa:</span><span class="sxs-lookup"><span data-stu-id="9ff85-142">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

<span data-ttu-id="9ff85-143">Conforme mostrado, a versão sem nenhum sufixo sempre terá precedência sobre as versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="9ff85-143">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="9ff85-144">Observe também que, se você usar sufixos numéricos com marcas de pré-lançamento que podem usar números de dois dígitos (ou mais), use zeros à esquerda como beta01 e beta05 para garantir que eles sejam classificados corretamente quando os números aumentarem.</span><span class="sxs-lookup"><span data-stu-id="9ff85-144">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>
