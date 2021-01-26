---
title: Versões de pré-lançamento em pacotes do NuGet
description: Diretrizes para compilar pacotes de pré-lançamento
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: ae6628efa6d97ff5ba2c4c359b9565a3214cb346
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774661"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="80854-103">Compilando pacotes de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="80854-103">Building pre-release packages</span></span>

<span data-ttu-id="80854-104">Sempre que você liberar um pacote atualizado com um novo número de versão, o NuGet considerará esse como a “última versão estável” conforme mostrado, por exemplo, na interface do usuário do Gerenciador de Pacotes no Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="80854-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![A interface do usuário do Gerenciador de Pacotes mostrando a versão estável mais recente](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="80854-106">Uma versão estável é aquela que é considerado confiável suficiente para ser usada na produção.</span><span class="sxs-lookup"><span data-stu-id="80854-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="80854-107">A versão estável mais recente também é aquela que será instalada como uma atualização de pacote ou durante a restauração do pacote (sujeito a restrições, conforme descrito em [Reinstalando e atualizando pacotes](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="80854-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="80854-108">Para dar suporte ao ciclo de vida de versão de software, o NuGet 1.6 e posterior permite a distribuição de pacotes de pré-lançamento, em que o número de versão inclui um sufixo de controle de versão semântico como `-alpha`, `-beta` ou `-rc`.</span><span class="sxs-lookup"><span data-stu-id="80854-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="80854-109">Para obter mais informações, consulte [Controle de versão de pacote](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="80854-109">For more information, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="80854-110">Você pode especificar essas versões usando uma das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="80854-110">You can specify such versions using one of the following ways:</span></span>

- <span data-ttu-id="80854-111">**Se seu projeto usa [`PackageReference`](../consume-packages/package-references-in-project-files.md)**: incluir o sufixo de versão semântica no elemento [`PackageVersion`](/dotnet/core/tools/csproj#packageversion) do arquivo `.csproj`:</span><span class="sxs-lookup"><span data-stu-id="80854-111">**If your project uses [`PackageReference`](../consume-packages/package-references-in-project-files.md)**: include the semantic version suffix in the `.csproj` file's [`PackageVersion`](/dotnet/core/tools/csproj#packageversion) element:</span></span>

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- <span data-ttu-id="80854-112">**Se seu projeto usa um arquivo [`packages.config`](../reference/packages-config.md)**: incluir o sufixo de versão semântica no elemento [`version`](../reference/nuspec.md#version) do arquivo [`.nuspec`](../reference/nuspec.md):</span><span class="sxs-lookup"><span data-stu-id="80854-112">**If your project has a [`packages.config`](../reference/packages-config.md) file**: include the semantic version suffix in the [`.nuspec`](../reference/nuspec.md) file's [`version`](../reference/nuspec.md#version) element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

<span data-ttu-id="80854-113">Quando você estiver pronto para lançar uma versão estável, basta remover o sufixo e o pacote terá precedência sobre as versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="80854-113">When you're ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="80854-114">Novamente, consulte [Controle de versão do pacote](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="80854-114">Again, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="80854-115">Instalando e atualizando pacotes de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="80854-115">Installing and updating pre-release packages</span></span>

<span data-ttu-id="80854-116">Por padrão, o NuGet não inclui as versões de pré-lançamento ao trabalhar com pacotes, mas você pode alterar esse comportamento da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="80854-116">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="80854-117">**Interface do usuário do Gerenciador de Pacotes no Visual Studio**: na interface do usuário **Gerenciar pacotes do NuGet**, marque a caixa **Incluir pré-lançamento**:</span><span class="sxs-lookup"><span data-stu-id="80854-117">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![A caixa de seleção Incluir pré-lançamento no Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="80854-119">Definir ou desmarcar esta caixa atualizará a interface do usuário do Gerenciador de Pacotes e a lista de versões disponíveis que você pode instalar.</span><span class="sxs-lookup"><span data-stu-id="80854-119">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="80854-120">**Console do Gerenciador de pacotes**: Use a `-IncludePrerelease` opção com os `Find-Package` comandos,, `Get-Package` `Install-Package` , `Sync-Package` e `Update-Package` .</span><span class="sxs-lookup"><span data-stu-id="80854-120">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="80854-121">Consulte a [Referência do PowerShell](../reference/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="80854-121">Refer to the [PowerShell Reference](../reference/powershell-reference.md).</span></span>

- <span data-ttu-id="80854-122">**CLI do NuGet**: Use a `-prerelease` opção com `install` os `update` comandos,, `delete` e `mirror` .</span><span class="sxs-lookup"><span data-stu-id="80854-122">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="80854-123">Consulte a [referência da CLI do NuGet](../reference/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="80854-123">Refer to the [NuGet CLI reference](../reference/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="80854-124">Controle de versão semântico</span><span class="sxs-lookup"><span data-stu-id="80854-124">Semantic versioning</span></span>

<span data-ttu-id="80854-125">O [Semantic Versioning or SemVer convention](https://semver.org/spec/v1.0.0.html) (Controle de versão semântico ou convenção de SemVer) descreve como utilizar as cadeias de caracteres em números de versão para expressar o significado do código subjacente.</span><span class="sxs-lookup"><span data-stu-id="80854-125">The [Semantic Versioning or SemVer convention](https://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="80854-126">Nesta convenção, cada versão tem três partes, `Major.Minor.Patch`, com o seguinte significado:</span><span class="sxs-lookup"><span data-stu-id="80854-126">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="80854-127">`Major`: alterações significativas</span><span class="sxs-lookup"><span data-stu-id="80854-127">`Major`: Breaking changes</span></span>
- <span data-ttu-id="80854-128">`Minor`: novos recursos, mas compatível com versões anteriores</span><span class="sxs-lookup"><span data-stu-id="80854-128">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="80854-129">`Patch`: somente correções de bug compatíveis com versões anteriores</span><span class="sxs-lookup"><span data-stu-id="80854-129">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="80854-130">As versões de pré-lançamento são indicadas acrescentando um hífen e uma cadeia de caracteres após o número de patch.</span><span class="sxs-lookup"><span data-stu-id="80854-130">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="80854-131">Tecnicamente, é possível usar *qualquer* cadeia de caracteres após o hífen e o NuGet tratará o pacote como a versão de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="80854-131">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="80854-132">O NuGet exibe, então, o número de versão completa na interface do usuário aplicável, deixando os consumidores para interpretar o significado por si mesmos.</span><span class="sxs-lookup"><span data-stu-id="80854-132">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="80854-133">Considerando isso, geralmente é aconselhável seguir as convenções de nomenclatura reconhecidas como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="80854-133">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="80854-134">`-alpha`: versão alfa, normalmente usado para o trabalho e experimentação em andamento</span><span class="sxs-lookup"><span data-stu-id="80854-134">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="80854-135">`-beta`: versão beta, normalmente uma completa com recursos para a próxima versão planejada, mas pode conter erros conhecidos.</span><span class="sxs-lookup"><span data-stu-id="80854-135">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="80854-136">`-rc`: versão Release candidate, normalmente uma versão que é potencialmente a final (estável), a menos que surjam bugs significativos.</span><span class="sxs-lookup"><span data-stu-id="80854-136">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="80854-137">O NuGet 4.3.0+ é compatível com o [Semantic Versioning v2.0.0](https://semver.org/spec/v2.0.0.html), que oferece compatibilidade com números com notação de ponto pré-lançamento, como no `1.0.1-build.23`.</span><span class="sxs-lookup"><span data-stu-id="80854-137">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="80854-138">A notação de ponto não e compatível com as versões do NuGet anteriores à 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="80854-138">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="80854-139">Em versões anteriores do NuGet, você poderia usar um formulário como `1.0.1-build23`, mas ela sempre foi considerada uma versão de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="80854-139">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="80854-140">Qualquer sufixo que você usar, no entanto, receberá precedência do NuGet cem ordem alfabética inversa:</span><span class="sxs-lookup"><span data-stu-id="80854-140">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta.12
1.0.1-beta.5
1.0.1-beta
1.0.1-alpha.2
1.0.1-alpha
```

<span data-ttu-id="80854-141">Conforme mostrado, a versão sem nenhum sufixo sempre terá precedência sobre as versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="80854-141">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span>

<span data-ttu-id="80854-142">Zeros à esquerda não são necessários com semver2, mas são com o esquema de versão antiga.</span><span class="sxs-lookup"><span data-stu-id="80854-142">Leading 0s are not needed with semver2, but they are with the old version schema.</span></span> <span data-ttu-id="80854-143">Se você usar sufixos numéricos com marcas de pré-lançamento que possam vir a usar números de dois dígitos (ou mais), use zeros à esquerda (como “beta.01” e “beta.05”) para garantir que sejam classificados corretamente quando os números aumentarem.</span><span class="sxs-lookup"><span data-stu-id="80854-143">If you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta.01 and beta.05 to ensure that they sort correctly when the numbers get larger.</span></span> <span data-ttu-id="80854-144">Essa recomendação só se aplica ao esquema de versão antiga.</span><span class="sxs-lookup"><span data-stu-id="80854-144">This recommendation only applies to the old version schema.</span></span>
