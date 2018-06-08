---
title: Versões de pré-lançamento em pacotes do NuGet
description: Diretrizes para compilar pacotes de pré-lançamento
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 498509e03a794878eeeadd46d499521d19415600
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818367"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="4b8ef-103">Compilando pacotes de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="4b8ef-103">Building pre-release packages</span></span>

<span data-ttu-id="4b8ef-104">Sempre que você liberar um pacote atualizado com um novo número de versão, o NuGet considerará esse como a “última versão estável” conforme mostrado, por exemplo, na interface do usuário do Gerenciador de Pacotes no Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="4b8ef-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![A interface do usuário do Gerenciador de Pacotes mostrando a versão estável mais recente](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="4b8ef-106">Uma versão estável é aquela que é considerado confiável suficiente para ser usada na produção.</span><span class="sxs-lookup"><span data-stu-id="4b8ef-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="4b8ef-107">A versão estável mais recente também é aquela que será instalada como uma atualização de pacote ou durante a restauração do pacote (sujeito a restrições, conforme descrito em [Reinstalando e atualizando pacotes](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="4b8ef-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="4b8ef-108">Para dar suporte ao ciclo de vida de versão de software, o NuGet 1.6 e posterior permite a distribuição de pacotes de pré-lançamento, em que o número de versão inclui um sufixo de controle de versão semântico como `-alpha`, `-beta` ou `-rc`.</span><span class="sxs-lookup"><span data-stu-id="4b8ef-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="4b8ef-109">Para obter mais informações, consulte [Controle de versão de pacote](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="4b8ef-109">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="4b8ef-110">Você pode especificar essas versões de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="4b8ef-110">You can specify such versions in two ways:</span></span>

- <span data-ttu-id="4b8ef-111">Arquivo `.nuspec`: inclua o sufixo de versão semântico no elemento `version`:</span><span class="sxs-lookup"><span data-stu-id="4b8ef-111">`.nuspec` file: include the semantic version suffix in the `version` element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

- <span data-ttu-id="4b8ef-112">Atributos de assembly: ao compilar um pacote de um projeto do Visual Studio (`.csproj` ou `.vbproj`), use o `AssemblyInformationalVersionAttribute` para especificar a versão:</span><span class="sxs-lookup"><span data-stu-id="4b8ef-112">Assembly attributes: when building a package from a Visual Studio project (`.csproj` or `.vbproj`), use the `AssemblyInformationalVersionAttribute` to specify the version:</span></span>

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    <span data-ttu-id="4b8ef-113">O NuGet adota esse valor em vez daquele especificado no atributo `AssemblyVersion`, que não é compatível com o controle de versão semântico.</span><span class="sxs-lookup"><span data-stu-id="4b8ef-113">NuGet picks up this value instead of the one specified in the `AssemblyVersion` attribute, which does not support semantic versioning.</span></span>

<span data-ttu-id="4b8ef-114">Quando você estiver pronto para lançar uma versão estável, basta remover o sufixo e o pacote terá precedência sobre as versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="4b8ef-114">When you’re ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="4b8ef-115">Novamente, consulte [Controle de versão do pacote](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="4b8ef-115">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="4b8ef-116">Instalando e atualizando pacotes de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="4b8ef-116">Installing and updating pre-release packages</span></span>

<span data-ttu-id="4b8ef-117">Por padrão, o NuGet não inclui as versões de pré-lançamento ao trabalhar com pacotes, mas você pode alterar esse comportamento da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4b8ef-117">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="4b8ef-118">**Interface do usuário do Gerenciador de Pacotes no Visual Studio**: na interface do usuário **Gerenciar pacotes do NuGet**, marque a caixa **Incluir pré-lançamento**:</span><span class="sxs-lookup"><span data-stu-id="4b8ef-118">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![A caixa de seleção Incluir pré-lançamento no Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="4b8ef-120">Definir ou desmarcar esta caixa atualizará a interface do usuário do Gerenciador de Pacotes e a lista de versões disponíveis que você pode instalar.</span><span class="sxs-lookup"><span data-stu-id="4b8ef-120">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="4b8ef-121">**Console do Gerenciador de Pacotes**: use a opção `-IncludePrerelease` com os comandos `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` e `Update-Package`.</span><span class="sxs-lookup"><span data-stu-id="4b8ef-121">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="4b8ef-122">Consulte a [Referência do PowerShell](../tools/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="4b8ef-122">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="4b8ef-123">**CLI do NuGet**: use a opção `-prerelease` com os comandos `install`, `update`, `delete` e `mirror`.</span><span class="sxs-lookup"><span data-stu-id="4b8ef-123">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="4b8ef-124">Consulte a [referência da CLI do NuGet](../tools/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="4b8ef-124">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="4b8ef-125">Controle de versão semântico</span><span class="sxs-lookup"><span data-stu-id="4b8ef-125">Semantic versioning</span></span>

<span data-ttu-id="4b8ef-126">O [Controle de versão semântico ou convenção de SemVer](http://semver.org/spec/v1.0.0.html) descreve como utilizar as cadeias de caracteres em números de versão para expressar o significado do código subjacente.</span><span class="sxs-lookup"><span data-stu-id="4b8ef-126">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey they meaning of the underlying code.</span></span>

<span data-ttu-id="4b8ef-127">Nesta convenção, cada versão tem três partes, `Major.Minor.Patch`, com o seguinte significado:</span><span class="sxs-lookup"><span data-stu-id="4b8ef-127">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="4b8ef-128">`Major`: alterações significativas</span><span class="sxs-lookup"><span data-stu-id="4b8ef-128">`Major`: Breaking changes</span></span>
- <span data-ttu-id="4b8ef-129">`Minor`: novos recursos, mas compatível com versões anteriores</span><span class="sxs-lookup"><span data-stu-id="4b8ef-129">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="4b8ef-130">`Patch`: somente correções de bug compatíveis com versões anteriores</span><span class="sxs-lookup"><span data-stu-id="4b8ef-130">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="4b8ef-131">As versões de pré-lançamento são indicadas acrescentando um hífen e uma cadeia de caracteres após o número de patch.</span><span class="sxs-lookup"><span data-stu-id="4b8ef-131">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="4b8ef-132">Tecnicamente, você pode usar *qualquer* cadeia de caracteres após o hífen e o NuGet tratará o pacote como a versão de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="4b8ef-132">Technically speaking, you can use *any *string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="4b8ef-133">O NuGet exibe, então, o número de versão completa na interface do usuário aplicável, deixando os consumidores para interpretar o significado por si mesmos.</span><span class="sxs-lookup"><span data-stu-id="4b8ef-133">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="4b8ef-134">Considerando isso, geralmente é aconselhável seguir as convenções de nomenclatura reconhecidas como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="4b8ef-134">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="4b8ef-135">`-alpha`: versão alfa, normalmente usado para o trabalho e experimentação em andamento</span><span class="sxs-lookup"><span data-stu-id="4b8ef-135">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="4b8ef-136">`-beta`: versão beta, normalmente uma completa com recursos para a próxima versão planejada, mas pode conter erros conhecidos.</span><span class="sxs-lookup"><span data-stu-id="4b8ef-136">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="4b8ef-137">`-rc`: versão Release candidate, normalmente uma versão que é potencialmente a final (estável), a menos que surjam bugs significativos.</span><span class="sxs-lookup"><span data-stu-id="4b8ef-137">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="4b8ef-138">O NuGet 4.3.0+ é compatível com o [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), que oferece compatibilidade com números com notação de ponto pré-lançamento, como no `1.0.1-build.23`.</span><span class="sxs-lookup"><span data-stu-id="4b8ef-138">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="4b8ef-139">A notação de ponto não e compatível com as versões do NuGet anteriores à 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="4b8ef-139">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="4b8ef-140">Em versões anteriores do NuGet, você poderia usar um formulário como `1.0.1-build23`, mas ela sempre foi considerada uma versão de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="4b8ef-140">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="4b8ef-141">Qualquer sufixo que você usar, no entanto, receberá precedência do NuGet cem ordem alfabética inversa:</span><span class="sxs-lookup"><span data-stu-id="4b8ef-141">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

<span data-ttu-id="4b8ef-142">Conforme mostrado, a versão sem nenhum sufixo sempre terá precedência sobre as versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="4b8ef-142">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="4b8ef-143">Observe também que, se você usar sufixos numéricos com marcas de pré-lançamento que podem usar números de dois dígitos (ou mais), use zeros à esquerda como beta01 e beta05 para garantir que eles sejam classificados corretamente quando os números aumentarem.</span><span class="sxs-lookup"><span data-stu-id="4b8ef-143">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>
