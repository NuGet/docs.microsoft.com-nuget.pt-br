---
title: "Referência de avisos e erros do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência completa de avisos e erros emitidos do NuGet durante várias operações do NuGet."
keywords: "NuGet erros, avisos do NuGet, diagnóstico"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 59bbe37d1a965e5167800148603869645fc5e0b2
ms.sourcegitcommit: df21fe770900644d476d51622a999597a6f20ef8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/12/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="17a4b-104">Erros e avisos</span><span class="sxs-lookup"><span data-stu-id="17a4b-104">Errors and warnings</span></span>

<span data-ttu-id="17a4b-105">NuGet 4.3.0+, erros e avisos são numerados conforme descrito neste tópico e fornecem informações detalhadas para ajudá-lo a resolver os problemas envolvidos.</span><span class="sxs-lookup"><span data-stu-id="17a4b-105">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="17a4b-106">Os erros e avisos listados aqui estão disponíveis apenas com [com base em PackageReference](../consume-packages/package-references-in-project-files.md) 4.3.0+ NuGet e projetos.</span><span class="sxs-lookup"><span data-stu-id="17a4b-106">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="17a4b-107">NuGet também respeita propriedades MSBuild para suprimir avisos ou elevá-las a erros.</span><span class="sxs-lookup"><span data-stu-id="17a4b-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="17a4b-108">Para obter mais informações, consulte [como: suprimir avisos do compilador](/visualstudio/ide/how-to-suppress-compiler-warnings) na documentação do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17a4b-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="17a4b-109">**Erros**</span><span class="sxs-lookup"><span data-stu-id="17a4b-109">**Errors**</span></span>

| <span data-ttu-id="17a4b-110">Grupo</span><span class="sxs-lookup"><span data-stu-id="17a4b-110">Group</span></span> | <span data-ttu-id="17a4b-111">Números de erro</span><span class="sxs-lookup"><span data-stu-id="17a4b-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="17a4b-112">Erros de entrada inválidos</span><span class="sxs-lookup"><span data-stu-id="17a4b-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="17a4b-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="17a4b-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="17a4b-114">Erros de pacote e projeto ausentes</span><span class="sxs-lookup"><span data-stu-id="17a4b-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="17a4b-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (anteriormente NU1607) [NU1108](#nu1108) (anteriormente NU1606)</span><span class="sxs-lookup"><span data-stu-id="17a4b-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="17a4b-116">Erros de compatibilidade</span><span class="sxs-lookup"><span data-stu-id="17a4b-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="17a4b-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="17a4b-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="17a4b-118">**Avisos**</span><span class="sxs-lookup"><span data-stu-id="17a4b-118">**Warnings**</span></span>

| <span data-ttu-id="17a4b-119">Grupo</span><span class="sxs-lookup"><span data-stu-id="17a4b-119">Group</span></span> | <span data-ttu-id="17a4b-120">Números de aviso</span><span class="sxs-lookup"><span data-stu-id="17a4b-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="17a4b-121">Avisos de entrada inválidos</span><span class="sxs-lookup"><span data-stu-id="17a4b-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="17a4b-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="17a4b-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="17a4b-123">Avisos de versão de pacote inesperado</span><span class="sxs-lookup"><span data-stu-id="17a4b-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="17a4b-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="17a4b-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="17a4b-125">Avisos de conflito de resolução</span><span class="sxs-lookup"><span data-stu-id="17a4b-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="17a4b-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="17a4b-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="17a4b-127">Avisos de fallback do pacote</span><span class="sxs-lookup"><span data-stu-id="17a4b-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="17a4b-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="17a4b-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="17a4b-129">Avisos de feeds</span><span class="sxs-lookup"><span data-stu-id="17a4b-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="17a4b-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="17a4b-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="17a4b-131">Avisos e erros internos do NuGet</span><span class="sxs-lookup"><span data-stu-id="17a4b-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="17a4b-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="17a4b-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="17a4b-133">Pacotes assinados (criação e verificação)</span><span class="sxs-lookup"><span data-stu-id="17a4b-133">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="17a4b-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="17a4b-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="17a4b-135">Erros de entrada inválidos</span><span class="sxs-lookup"><span data-stu-id="17a4b-135">Invalid input errors</span></span>

<span data-ttu-id="17a4b-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="17a4b-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="17a4b-137">NU1001</span><span class="sxs-lookup"><span data-stu-id="17a4b-137">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-138">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-138">**Issue**</span></span> | <span data-ttu-id="17a4b-139">O projeto não contém um ou mais frameworks.</span><span class="sxs-lookup"><span data-stu-id="17a4b-139">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="17a4b-140">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-140">**Example message**</span></span> | <span data-ttu-id="17a4b-141">*O projeto projA não especifica nenhuma estrutura de destino em c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="17a4b-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="17a4b-142">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-142">**Solution**</span></span> | <span data-ttu-id="17a4b-143">Adicionar um `TargetFramework` ou `TargetFrameworks` propriedade para o arquivo de projeto especificado.</span><span class="sxs-lookup"><span data-stu-id="17a4b-143">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="17a4b-144">NU1002</span><span class="sxs-lookup"><span data-stu-id="17a4b-144">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-145">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-145">**Issue**</span></span> | <span data-ttu-id="17a4b-146">Combinação inválida de entradas, junto com uma palavra-chave criptografada.</span><span class="sxs-lookup"><span data-stu-id="17a4b-146">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="17a4b-147">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-147">**Example message**</span></span> | <span data-ttu-id="17a4b-148">*'CLEAR' não pode ser usado em conjunto com outros valores*</span><span class="sxs-lookup"><span data-stu-id="17a4b-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="17a4b-149">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-149">**Solution**</span></span> | <span data-ttu-id="17a4b-150">Use limpar por si só e omitir todas as outras entradas.</span><span class="sxs-lookup"><span data-stu-id="17a4b-150">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="17a4b-151">NU1003</span><span class="sxs-lookup"><span data-stu-id="17a4b-151">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-152">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-152">**Issue**</span></span> | <span data-ttu-id="17a4b-153">`PackageTargetFallback` e `AssetTargetFallback` fornecem um comportamento diferente para a seleção de recursos e não podem ser usados juntos.</span><span class="sxs-lookup"><span data-stu-id="17a4b-153">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="17a4b-154">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-154">**Example message**</span></span> | <span data-ttu-id="17a4b-155">*PackageTargetFallback e AssetTargetFallback não podem ser usados juntos. Remova as referências de PackageTargetFallback(deprecated) do ambiente do projeto.*</span><span class="sxs-lookup"><span data-stu-id="17a4b-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="17a4b-156">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-156">**Solution**</span></span> | <span data-ttu-id="17a4b-157">Remover preterido `PackageTargetFallback` elemento do projeto.</span><span class="sxs-lookup"><span data-stu-id="17a4b-157">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="17a4b-158">Erros de pacote e projeto ausentes</span><span class="sxs-lookup"><span data-stu-id="17a4b-158">Missing package and project errors</span></span>

<span data-ttu-id="17a4b-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="17a4b-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="17a4b-160">NU1100</span><span class="sxs-lookup"><span data-stu-id="17a4b-160">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-161">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-161">**Issue**</span></span> | <span data-ttu-id="17a4b-162">Um grupo de dependência não ser resolvido.</span><span class="sxs-lookup"><span data-stu-id="17a4b-162">A dependency group not be resolved.</span></span> <span data-ttu-id="17a4b-163">Esse é um problema genérico para tipos que não são pacotes ou projetos.</span><span class="sxs-lookup"><span data-stu-id="17a4b-163">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="17a4b-164">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-164">**Example message**</span></span> | <span data-ttu-id="17a4b-165">*Não é possível resolver System.Missing para net45*</span><span class="sxs-lookup"><span data-stu-id="17a4b-165">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="17a4b-166">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-166">**Solution**</span></span> | <span data-ttu-id="17a4b-167">Abra o arquivo de projeto e examine a lista de suas dependências.</span><span class="sxs-lookup"><span data-stu-id="17a4b-167">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="17a4b-168">Verifique se cada dependência existe nas fontes de pacote que você está usando, e o pacote dá suporte à estrutura de destino do projeto.</span><span class="sxs-lookup"><span data-stu-id="17a4b-168">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="17a4b-169">NU1101</span><span class="sxs-lookup"><span data-stu-id="17a4b-169">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-170">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-170">**Issue**</span></span> | <span data-ttu-id="17a4b-171">O pacote não foi encontrado em qualquer fonte.</span><span class="sxs-lookup"><span data-stu-id="17a4b-171">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="17a4b-172">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-172">**Example message**</span></span> | <span data-ttu-id="17a4b-173">*Não é possível encontrar o pacote System.Missing. Nenhum pacote existe com essa id na fonte (s): dotnet-core, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="17a4b-173">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="17a4b-174">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-174">**Solution**</span></span> | <span data-ttu-id="17a4b-175">Examine as dependências do projeto no Visual Studio para certificar-se de que você está usando o número de versão e de identificador de pacote correto.</span><span class="sxs-lookup"><span data-stu-id="17a4b-175">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="17a4b-176">Também verifique se o [configuração NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifica as origens do pacote seu pretende usar.</span><span class="sxs-lookup"><span data-stu-id="17a4b-176">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="17a4b-177">Se você usar pacotes que tenham [o controle de versão semântico 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), certifique-se de que você está usando o [V3 feed](https://api.nuget.org/v3/index.json) no [configuração NuGet](../consume-packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="17a4b-177">If you use packages that have [Semantic Versioning 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), please make sure that you are using the [V3 feed](https://api.nuget.org/v3/index.json) in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="17a4b-178">NU1102</span><span class="sxs-lookup"><span data-stu-id="17a4b-178">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-179">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-179">**Issue**</span></span> | <span data-ttu-id="17a4b-180">O identificador de pacote for encontrado, mas não é possível encontrar uma versão dentro do intervalo de dependência especificada em qualquer uma das fontes.</span><span class="sxs-lookup"><span data-stu-id="17a4b-180">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="17a4b-181">O intervalo pode ser especificado por um pacote e não ao usuário.</span><span class="sxs-lookup"><span data-stu-id="17a4b-181">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="17a4b-182">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-182">**Example message**</span></span> | <span data-ttu-id="17a4b-183">*Não é possível localizar o pacote NuGet.Versioning com a versão (> = 9.0.1)<br/> -versão (ões) de 30 encontrado em nuget.org [mais próximo de versão: 4.0.0]<br/> -versão (ões) de 10 encontrado em dotnet buildtools [mais próximo de versão: 4.0.0-rc-2129]<br/> -9 encontrado versão (ões) em NuGetVolatile [mais próximo de versão: 3.0.0-beta-00032]<br/> -encontrado versões 0 no núcleo do dotnet<br/> -encontrado versões 0 no roslyn dotnet*</span><span class="sxs-lookup"><span data-stu-id="17a4b-183">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="17a4b-184">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-184">**Solution**</span></span> | <span data-ttu-id="17a4b-185">Edite o arquivo de projeto ou `packages.config` para corrigir a versão do pacote.</span><span class="sxs-lookup"><span data-stu-id="17a4b-185">Edit the project file or `packages.config` to correct the package version.</span></span> <span data-ttu-id="17a4b-186">Também verifique se o [configuração NuGet](../consume-packages/Configuring-NuGet-Behavior.md) identifica as origens do pacote seu pretende usar.</span><span class="sxs-lookup"><span data-stu-id="17a4b-186">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="17a4b-187">Talvez seja necessário alterar a versão de requeted se esse pacote é referenciado pelo projeto diretamente.</span><span class="sxs-lookup"><span data-stu-id="17a4b-187">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="17a4b-188">NU1103</span><span class="sxs-lookup"><span data-stu-id="17a4b-188">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-189">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-189">**Issue**</span></span> | <span data-ttu-id="17a4b-190">O projeto especificado para o intervalo de dependência a uma versão estável, mas nenhuma versão estável foram encontrado nesse intervalo.</span><span class="sxs-lookup"><span data-stu-id="17a4b-190">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="17a4b-191">As versões de pré-lançamento foram encontradas, mas não são permitidas.</span><span class="sxs-lookup"><span data-stu-id="17a4b-191">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="17a4b-192">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-192">**Example message**</span></span> | <span data-ttu-id="17a4b-193">*Não é possível localizar um pacote estável NuGet.Versioning com a versão (> = 3.0.0)<br/> -versão (ões) de 10 encontrado em dotnet buildtools [mais próximo de versão: 4.0.0-rc-2129]<br/> -versão (ões) de 9 encontrado em NuGetVolatile [mais próximo de versão: 3.0.0-beta-00032] <br/> -Encontrado versões 0 no núcleo do dotnet<br/> -encontrado versões 0 no roslyn dotnet*</span><span class="sxs-lookup"><span data-stu-id="17a4b-193">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="17a4b-194">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-194">**Solution**</span></span> |  <span data-ttu-id="17a4b-195">Editar o intervalo de versão no arquivo de projeto ou `packages.config` para incluir as versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="17a4b-195">Edit the version range in the project file or `packages.config` to include pre-release versions.</span></span> <span data-ttu-id="17a4b-196">Consulte [controle de versão do pacote](../reference/Package-Versioning.md).</span><span class="sxs-lookup"><span data-stu-id="17a4b-196">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="17a4b-197">NU1104</span><span class="sxs-lookup"><span data-stu-id="17a4b-197">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-198">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-198">**Issue**</span></span> | <span data-ttu-id="17a4b-199">Um ProjectReference aponta para um arquivo que não existe.</span><span class="sxs-lookup"><span data-stu-id="17a4b-199">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="17a4b-200">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-200">**Example message**</span></span> | <span data-ttu-id="17a4b-201">*Referência de projeto não existe 'c:\a.csproj'. Verifique se a referência de projeto é válida e se existe o arquivo de projeto.*</span><span class="sxs-lookup"><span data-stu-id="17a4b-201">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="17a4b-202">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-202">**Solution**</span></span> | <span data-ttu-id="17a4b-203">Edite o arquivo de projeto para corrigir o caminho para o projeto referenciado ou para remover a referência ao mesmo tempo, se ele não for mais necessário.</span><span class="sxs-lookup"><span data-stu-id="17a4b-203">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="17a4b-204">NU1105</span><span class="sxs-lookup"><span data-stu-id="17a4b-204">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-205">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-205">**Issue**</span></span> | <span data-ttu-id="17a4b-206">O arquivo de projeto existe, mas nenhuma informação de restauração foi fornecida para ele.</span><span class="sxs-lookup"><span data-stu-id="17a4b-206">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="17a4b-207">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-207">**Example message**</span></span> | <span data-ttu-id="17a4b-208">*Não é possível ler as informações de projeto para 'c:\a.csproj'. O arquivo de projeto pode ser inválidos ou ausentes destinos necessários para a restauração.*</span><span class="sxs-lookup"><span data-stu-id="17a4b-208">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="17a4b-209">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-209">**Solution**</span></span> | <span data-ttu-id="17a4b-210">No Visual Studio, o erro pode significar que o projeto é descarregado, em cujo caso recarregar o projeto.</span><span class="sxs-lookup"><span data-stu-id="17a4b-210">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="17a4b-211">Na linha de comando, isso pode significar que o arquivo está corrompido ou que não contenha personalizado "após imports" necessário para restauração ler o projeto de destino.</span><span class="sxs-lookup"><span data-stu-id="17a4b-211">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="17a4b-212">Verifique se o arquivo de projeto é válido e contém um destino de "depois imports".</span><span class="sxs-lookup"><span data-stu-id="17a4b-212">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="17a4b-213">NU1106</span><span class="sxs-lookup"><span data-stu-id="17a4b-213">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-214">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-214">**Issue**</span></span> | <span data-ttu-id="17a4b-215">Restrições de dependência não podem ser resolvidas.</span><span class="sxs-lookup"><span data-stu-id="17a4b-215">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="17a4b-216">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-216">**Example message**</span></span> | <span data-ttu-id="17a4b-217">*Não foi possível satisfazer solicitações conflitantes para {id}: {caminho conflito} Framework: {gráfico de destino}*</span><span class="sxs-lookup"><span data-stu-id="17a4b-217">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> 
| <span data-ttu-id="17a4b-218">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-218">**Solution**</span></span> | <span data-ttu-id="17a4b-219">Edite o arquivo de projeto ou `packages.config` para especificar intervalos mais abertos para a dependência em vez de uma versão exata.</span><span class="sxs-lookup"><span data-stu-id="17a4b-219">Edit the project file or `packages.config` to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="17a4b-220">NU1107 (anteriormente NU1607)</span><span class="sxs-lookup"><span data-stu-id="17a4b-220">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-221">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-221">**Issue**</span></span> | <span data-ttu-id="17a4b-222">Não é possível resolver as restrições de dependência entre pacotes.</span><span class="sxs-lookup"><span data-stu-id="17a4b-222">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="17a4b-223">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-223">**Example message**</span></span> | <span data-ttu-id="17a4b-224">*Conflito de versão detectado para NuGet.Versioning. Referenciar o pacote diretamente do projeto para resolver esse problema.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="17a4b-224">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="17a4b-225">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-225">**Solution**</span></span> | <span data-ttu-id="17a4b-226">Pacotes com restrições de dependência em versões exatas não permitir que outros pacotes para aumentar a versão, se necessário.</span><span class="sxs-lookup"><span data-stu-id="17a4b-226">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="17a4b-227">Adicione uma referência ao projeto diretamente (no arquivo de projeto ou `packages.config`) com a versão exata necessária.</span><span class="sxs-lookup"><span data-stu-id="17a4b-227">Add a reference to the project directly (in the project file or `packages.config`) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="17a4b-228">NU1108 (anteriormente NU1606)</span><span class="sxs-lookup"><span data-stu-id="17a4b-228">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-229">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-229">**Issue**</span></span> | <span data-ttu-id="17a4b-230">Foi detectada uma dependência circular.</span><span class="sxs-lookup"><span data-stu-id="17a4b-230">A circular dependency was detected.</span></span> |
| <span data-ttu-id="17a4b-231">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-231">**Example message**</span></span> | <span data-ttu-id="17a4b-232">*Ciclo detectado: A -> B -> um*</span><span class="sxs-lookup"><span data-stu-id="17a4b-232">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="17a4b-233">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-233">**Solution**</span></span> | <span data-ttu-id="17a4b-234">O pacote foi criado incorretamente. entre em contato com o proprietário do pacote para corrigir o erro.</span><span class="sxs-lookup"><span data-stu-id="17a4b-234">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="17a4b-235">Erros de compatibilidade</span><span class="sxs-lookup"><span data-stu-id="17a4b-235">Compatibility errors</span></span>

<span data-ttu-id="17a4b-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="17a4b-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="17a4b-237">NU1201</span><span class="sxs-lookup"><span data-stu-id="17a4b-237">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-238">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-238">**Issue**</span></span> | <span data-ttu-id="17a4b-239">Um projeto de dependência não contém uma estrutura compatível com o projeto atual.</span><span class="sxs-lookup"><span data-stu-id="17a4b-239">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="17a4b-240">Normalmente, a estrutura de destino do projeto é uma versão superior do projeto de consumo.</span><span class="sxs-lookup"><span data-stu-id="17a4b-240">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="17a4b-241">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-241">**Example message**</span></span> | <span data-ttu-id="17a4b-242">*ServerWeb do projeto não é compatível com netstandard1.3 (. Identificadores de NETStandard, versão = v 1.3). Projeto suporta ServerWeb:<br/> -netstandard1.6 (. Identificadores de NETStandard, versão = v 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = v 1.0)*</span><span class="sxs-lookup"><span data-stu-id="17a4b-242">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="17a4b-243">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-243">**Solution**</span></span> | <span data-ttu-id="17a4b-244">Altere a estrutura de destino do projeto para uma versão igual ou menor que o projeto de consumo.</span><span class="sxs-lookup"><span data-stu-id="17a4b-244">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="17a4b-245">NU1202</span><span class="sxs-lookup"><span data-stu-id="17a4b-245">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-246">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-246">**Issue**</span></span> | <span data-ttu-id="17a4b-247">Um pacote de dependência não contém qualquer ativos compatíveis com o projeto.</span><span class="sxs-lookup"><span data-stu-id="17a4b-247">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="17a4b-248">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-248">**Example message**</span></span> | <span data-ttu-id="17a4b-249">*Pacote System.ComponentModel.EventBasedAsync 4.0.11 não é compatível com netstandard1.3 (. Identificadores de NETStandard, versão = v 1.3). Pacote suporta System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, versão = v 1.0)<br/> -monotouch10 (MonoTouch, versão = v 1.0)<br/> -net45 (. NETFramework, Version = v 4.5)<br/> -netcore50 (. NETCore, Version = v 5.0)<br/> -netstandard1.0 (. Identificadores de NETStandard, versão = v 1.0)<br/> -portátil net45 + win8 + wp8 + wpa81 (. NETPortable, Version = v0.0, perfil = Profile259)<br/> -win8 (Windows, versão = v 8.0)<br/> -wp8 (WindowsPhone, versão = v 8.0)<br/> -wpa81 (WindowsPhoneApp, versão = 8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="17a4b-249">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="17a4b-250">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-250">**Solution**</span></span> | <span data-ttu-id="17a4b-251">Altere a estrutura de destino do projeto para um com suporte no pacote.</span><span class="sxs-lookup"><span data-stu-id="17a4b-251">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="17a4b-252">NU1203</span><span class="sxs-lookup"><span data-stu-id="17a4b-252">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-253">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-253">**Issue**</span></span> | <span data-ttu-id="17a4b-254">O pacote não oferece suporte para o projeto `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="17a4b-254">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="17a4b-255">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-255">**Example message**</span></span> | <span data-ttu-id="17a4b-256">*System.Example 1.0.0 fornece uma referência de tempo de compilação do assembly para o. dll em net461, mas não há nenhum tempo de execução do assembly compatível.*</span><span class="sxs-lookup"><span data-stu-id="17a4b-256">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="17a4b-257">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-257">**Solution**</span></span> | <span data-ttu-id="17a4b-258">Alterar o `RuntimeIdentifier` valores usados no projeto, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="17a4b-258">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="17a4b-259">NU1401</span><span class="sxs-lookup"><span data-stu-id="17a4b-259">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-260">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-260">**Issue**</span></span> | <span data-ttu-id="17a4b-261">O pacote requer recursos ou estruturas atualmente não há suportadas à versão instalada do NuGet.</span><span class="sxs-lookup"><span data-stu-id="17a4b-261">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="17a4b-262">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-262">**Example message**</span></span> | <span data-ttu-id="17a4b-263">*O pacote 'NuGet.Versioning' requer o NuGet versão de cliente '5.0.0' ou superior, mas a versão atual do NuGet é '4.3.0'.*</span><span class="sxs-lookup"><span data-stu-id="17a4b-263">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="17a4b-264">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-264">**Solution**</span></span> | <span data-ttu-id="17a4b-265">Instale uma versão mais recente do NuGet.</span><span class="sxs-lookup"><span data-stu-id="17a4b-265">Install a newer version of NuGet.</span></span> <span data-ttu-id="17a4b-266">Consulte [ferramentas de cliente de instalar o NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="17a4b-266">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="17a4b-267">Avisos de entrada inválidos</span><span class="sxs-lookup"><span data-stu-id="17a4b-267">Invalid input warnings</span></span>

<span data-ttu-id="17a4b-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="17a4b-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="17a4b-269">NU1501</span><span class="sxs-lookup"><span data-stu-id="17a4b-269">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-270">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-270">**Issue**</span></span> | <span data-ttu-id="17a4b-271">A restauração do projeto está tentando operar em não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="17a4b-271">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="17a4b-272">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-272">**Example message**</span></span> | <span data-ttu-id="17a4b-273">*A pasta 'c:\projects\a' não contém um projeto para restaurar.*</span><span class="sxs-lookup"><span data-stu-id="17a4b-273">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="17a4b-274">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-274">**Solution**</span></span> | <span data-ttu-id="17a4b-275">Execute a restauração do nuget em uma pasta que contém um projeto.</span><span class="sxs-lookup"><span data-stu-id="17a4b-275">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="17a4b-276">NU1502</span><span class="sxs-lookup"><span data-stu-id="17a4b-276">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-277">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-277">**Issue**</span></span> | <span data-ttu-id="17a4b-278">`RuntimeSupports` contém um perfil inválido.</span><span class="sxs-lookup"><span data-stu-id="17a4b-278">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="17a4b-279">Normalmente, o oferece suporte a perfil não foi encontrado em um `runtime.json` arquivo dos pacotes de dependência atual.</span><span class="sxs-lookup"><span data-stu-id="17a4b-279">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="17a4b-280">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-280">**Example message**</span></span> | <span data-ttu-id="17a4b-281">*Perfil de compatibilidade desconhecido: aaa*</span><span class="sxs-lookup"><span data-stu-id="17a4b-281">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="17a4b-282">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-282">**Solution**</span></span> | <span data-ttu-id="17a4b-283">Verifique o `RuntimeSupports` valor em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="17a4b-283">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="17a4b-284">NU1503</span><span class="sxs-lookup"><span data-stu-id="17a4b-284">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-285">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-285">**Issue**</span></span> | <span data-ttu-id="17a4b-286">Um projeto de dependência não importa destinos de restauração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="17a4b-286">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="17a4b-287">Isso é semelhante a NU1105, mas aqui o projeto será ignorado e ignorado em vez fazendo com que todos os de restauração falhe.</span><span class="sxs-lookup"><span data-stu-id="17a4b-287">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="17a4b-288">Em soluções complexas geralmente há outros tipos de projetos que podem não oferecer suporte a restauração.</span><span class="sxs-lookup"><span data-stu-id="17a4b-288">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="17a4b-289">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-289">**Example message**</span></span> | <span data-ttu-id="17a4b-290">*Ignorando a restauração para o projeto 'c:\a.csproj'. O arquivo de projeto pode ser inválidos ou ausentes destinos necessários para a restauração.*</span><span class="sxs-lookup"><span data-stu-id="17a4b-290">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="17a4b-291">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-291">**Solution**</span></span> | <span data-ttu-id="17a4b-292">Isso pode acontecer para projetos que não importar props/destinos comuns que importar automaticamente a restauração.</span><span class="sxs-lookup"><span data-stu-id="17a4b-292">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="17a4b-293">Se o projeto não precisa ser restaurados isso pode ser ignorado.</span><span class="sxs-lookup"><span data-stu-id="17a4b-293">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="17a4b-294">Caso contrário, edite o projeto afetado para adicionar destinos de restauração.</span><span class="sxs-lookup"><span data-stu-id="17a4b-294">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="17a4b-295">Avisos de versão de pacote inesperado</span><span class="sxs-lookup"><span data-stu-id="17a4b-295">Unexpected package version warnings</span></span>

<span data-ttu-id="17a4b-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="17a4b-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="17a4b-297">NU1601</span><span class="sxs-lookup"><span data-stu-id="17a4b-297">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-298">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-298">**Issue**</span></span> | <span data-ttu-id="17a4b-299">Uma dependência de projeto foi aumentada para uma versão maior do que o projeto especificado.</span><span class="sxs-lookup"><span data-stu-id="17a4b-299">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="17a4b-300">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-300">**Example message**</span></span> | <span data-ttu-id="17a4b-301">*Dependência especificada foi NuGet.Versioning (> = 3.5.0) mas acabou com NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="17a4b-301">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="17a4b-302">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-302">**Solution**</span></span> | <span data-ttu-id="17a4b-303">Atualize a dependência no projeto para uma versão apropriada.</span><span class="sxs-lookup"><span data-stu-id="17a4b-303">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="17a4b-304">NU1602</span><span class="sxs-lookup"><span data-stu-id="17a4b-304">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-305">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-305">**Issue**</span></span> | <span data-ttu-id="17a4b-306">Uma dependência de pacote não tem um limite inferior.</span><span class="sxs-lookup"><span data-stu-id="17a4b-306">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="17a4b-307">Isso não permite que a restauração localizar o *melhor correspondência*.</span><span class="sxs-lookup"><span data-stu-id="17a4b-307">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="17a4b-308">Cada restauração flutua para baixo ao tentar encontrar uma versão inferior que pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="17a4b-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="17a4b-309">Isso significa que a restauração fica online para verificar se todas as fontes de cada vez em vez de usar os pacotes que já existem na pasta de pacote do usuário.</span><span class="sxs-lookup"><span data-stu-id="17a4b-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="17a4b-310">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-310">**Example message**</span></span> | <span data-ttu-id="17a4b-311">*NuGet. Packaging 4.0.0 não fornece um limite inferior inclusivo de dependência NuGet.Versioning (3.5.0 >). Uma melhor correspondência aproximada de 3.6.0 foi resolvida.*</span><span class="sxs-lookup"><span data-stu-id="17a4b-311">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="17a4b-312">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-312">**Solution**</span></span> | <span data-ttu-id="17a4b-313">Isso geralmente é um erro de criação de pacote.</span><span class="sxs-lookup"><span data-stu-id="17a4b-313">This is usually a package authoring error.</span></span> <span data-ttu-id="17a4b-314">Entre em contato com o autor do pacote para resolver o problema.</span><span class="sxs-lookup"><span data-stu-id="17a4b-314">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="17a4b-315">NU1603</span><span class="sxs-lookup"><span data-stu-id="17a4b-315">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-316">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-316">**Issue**</span></span> | <span data-ttu-id="17a4b-317">Uma dependência de pacote especificado de uma versão que não pôde ser encontrada.</span><span class="sxs-lookup"><span data-stu-id="17a4b-317">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="17a4b-318">Normalmente, as origens do pacote contém a versão inferior esperado.</span><span class="sxs-lookup"><span data-stu-id="17a4b-318">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="17a4b-319">Uma versão mais recente foi usada em vez disso, o que é diferente do que o pacote foi criado.</span><span class="sxs-lookup"><span data-stu-id="17a4b-319">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="17a4b-320">Isso significa que a restauração não localizou o *melhor correspondência*.</span><span class="sxs-lookup"><span data-stu-id="17a4b-320">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="17a4b-321">Cada restauração flutua para baixo ao tentar encontrar uma versão inferior que pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="17a4b-321">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="17a4b-322">Isso significa que a restauração fica online para verificar se todas as fontes de cada vez em vez de usar os pacotes que já existem na pasta de pacote do usuário.</span><span class="sxs-lookup"><span data-stu-id="17a4b-322">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="17a4b-323">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-323">**Example message**</span></span> | <span data-ttu-id="17a4b-324">NuGet. Packaging 4.0.0 depende NuGet.Versioning (> = 4.0.0) mas 4.0.0 não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="17a4b-324">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="17a4b-325">Uma melhor correspondência aproximada de 5.0.0 foi resolvida.</span><span class="sxs-lookup"><span data-stu-id="17a4b-325">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="17a4b-326">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-326">**Solution**</span></span> | <span data-ttu-id="17a4b-327">Se o pacote esperado não foi liberado, em seguida, isso pode ser um erro de criação de pacote.</span><span class="sxs-lookup"><span data-stu-id="17a4b-327">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="17a4b-328">Entre em contato com o autor do pacote para resolver o problema.</span><span class="sxs-lookup"><span data-stu-id="17a4b-328">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="17a4b-329">Se o pacote foi liberado, verifique se ela está disponível nas fontes de pacote que você está usando.</span><span class="sxs-lookup"><span data-stu-id="17a4b-329">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="17a4b-330">Se usar uma fonte particular, você precisará atualizar o pacote em que o feed.</span><span class="sxs-lookup"><span data-stu-id="17a4b-330">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="17a4b-331">NU1604</span><span class="sxs-lookup"><span data-stu-id="17a4b-331">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-332">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-332">**Issue**</span></span> | <span data-ttu-id="17a4b-333">Uma dependência de projeto não define um limite inferior.</span><span class="sxs-lookup"><span data-stu-id="17a4b-333">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="17a4b-334">Isso significa que a restauração não localizou o *melhor correspondência*.</span><span class="sxs-lookup"><span data-stu-id="17a4b-334">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="17a4b-335">Cada restauração flutua para baixo ao tentar encontrar uma versão inferior que pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="17a4b-335">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="17a4b-336">Isso significa que a restauração fica online para verificar se todas as fontes de cada vez em vez de usar os pacotes que já existem na pasta de pacote do usuário.</span><span class="sxs-lookup"><span data-stu-id="17a4b-336">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="17a4b-337">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-337">**Example message**</span></span> | <span data-ttu-id="17a4b-338">*Projeto dependência NuGet.Versioning (< = 9.0.0) doe não contêm um limite inferior inclusivo. Inclua um limite inferior na versão de dependência para garantir resultados consistentes de restauração.*</span><span class="sxs-lookup"><span data-stu-id="17a4b-338">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="17a4b-339">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-339">**Solution**</span></span> | <span data-ttu-id="17a4b-340">Atualize o projeto `PackageReference` `Version` atributo para incluir um limite inferior.</span><span class="sxs-lookup"><span data-stu-id="17a4b-340">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="17a4b-341">NU1605</span><span class="sxs-lookup"><span data-stu-id="17a4b-341">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-342">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-342">**Issue**</span></span> | <span data-ttu-id="17a4b-343">Um pacote de dependência especificou uma restrição de versão em uma versão superior de um pacote de restauração finalmente resolvida.</span><span class="sxs-lookup"><span data-stu-id="17a4b-343">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="17a4b-344">Ou seja, devido a "mais próximo de wins" regra durante a resolução de pacotes, um pacote mais próximo no gráfico pode ter substituído um pacote distante.</span><span class="sxs-lookup"><span data-stu-id="17a4b-344">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="17a4b-345">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-345">**Example message**</span></span> | <span data-ttu-id="17a4b-346">*Detectado o downgrade do pacote: NuGet.Versioning de 4.0.0 para 3.5.0. Referenciar o pacote diretamente do projeto para selecionar uma versão diferente.<br/>  NuGet. Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="17a4b-346">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="17a4b-347">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-347">**Solution**</span></span> | <span data-ttu-id="17a4b-348">Adicione uma referência direta ao projeto para a versão posterior do pacote que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="17a4b-348">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="17a4b-349">Avisos de conflito de resolução</span><span class="sxs-lookup"><span data-stu-id="17a4b-349">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="17a4b-350">NU1608</span><span class="sxs-lookup"><span data-stu-id="17a4b-350">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-351">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-351">**Issue**</span></span> | <span data-ttu-id="17a4b-352">Um pacote resolvido é maior do que permite que uma restrição de dependência.</span><span class="sxs-lookup"><span data-stu-id="17a4b-352">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="17a4b-353">Isso significa que um pacote referenciado diretamente por um projeto substitui as restrições de dependência de outros pacotes.</span><span class="sxs-lookup"><span data-stu-id="17a4b-353">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="17a4b-354">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-354">**Example message**</span></span> | <span data-ttu-id="17a4b-355">*Versão do pacote detectado fora da restrição de dependência: x 1.0.0 requer y (= 1.0.0), mas a versão y 2.0.0 foi resolvido.*</span><span class="sxs-lookup"><span data-stu-id="17a4b-355">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="17a4b-356">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-356">**Solution**</span></span> | <span data-ttu-id="17a4b-357">Em alguns casos, isso é intencional e o aviso pode ser suprimido.</span><span class="sxs-lookup"><span data-stu-id="17a4b-357">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="17a4b-358">Caso contrário, altere a referência do projeto para o pacote para ampliar suas restrições de versão.</span><span class="sxs-lookup"><span data-stu-id="17a4b-358">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="17a4b-359">Avisos de fallback do pacote</span><span class="sxs-lookup"><span data-stu-id="17a4b-359">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="17a4b-360">NU1701</span><span class="sxs-lookup"><span data-stu-id="17a4b-360">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-361">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-361">**Issue**</span></span> | <span data-ttu-id="17a4b-362">`PackageTargetFallback` / `AssetTargetFallback` foi usado para selecionar os ativos de um pacote.</span><span class="sxs-lookup"><span data-stu-id="17a4b-362">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="17a4b-363">O aviso de permitir que os usuários saibam que os ativos podem não ser 100% compatível.</span><span class="sxs-lookup"><span data-stu-id="17a4b-363">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="17a4b-364">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-364">**Example message**</span></span> | <span data-ttu-id="17a4b-365">*Pacote 'NuGet.Versioning' foi restaurado usando 'portátil net45 + win8' em vez disso, a estrutura de destino do projeto 'netstandard1.5'. Esse pacote pode não ser totalmente compatível com o seu projeto.*</span><span class="sxs-lookup"><span data-stu-id="17a4b-365">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="17a4b-366">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-366">**Solution**</span></span> | <span data-ttu-id="17a4b-367">Altere a estrutura de destino do projeto para um com suporte no pacote.</span><span class="sxs-lookup"><span data-stu-id="17a4b-367">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="17a4b-368">Avisos de feeds</span><span class="sxs-lookup"><span data-stu-id="17a4b-368">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="17a4b-369">NU1801</span><span class="sxs-lookup"><span data-stu-id="17a4b-369">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-370">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-370">**Issue**</span></span> | <span data-ttu-id="17a4b-371">Ocorreu um erro ao ler o feed quando `IgnoreFailedSources` está definido como true, convertendo-o para um aviso não fatal.</span><span class="sxs-lookup"><span data-stu-id="17a4b-371">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="17a4b-372">Isso pode conter qualquer mensagem e é genérico.</span><span class="sxs-lookup"><span data-stu-id="17a4b-372">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="17a4b-373">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-373">**Example message**</span></span> | <span data-ttu-id="17a4b-374">N/D</span><span class="sxs-lookup"><span data-stu-id="17a4b-374">n/a</span></span> |
| <span data-ttu-id="17a4b-375">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-375">**Solution**</span></span> | <span data-ttu-id="17a4b-376">Edite sua configuração para especificar fontes válidos.</span><span class="sxs-lookup"><span data-stu-id="17a4b-376">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="17a4b-377">Avisos e erros internos do NuGet</span><span class="sxs-lookup"><span data-stu-id="17a4b-377">NuGet internal errors and warnings</span></span>

<span data-ttu-id="17a4b-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="17a4b-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="17a4b-379">NU1000</span><span class="sxs-lookup"><span data-stu-id="17a4b-379">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-380">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-380">**Issue**</span></span> | <span data-ttu-id="17a4b-381">Um erro interno não específico do NuGet.</span><span class="sxs-lookup"><span data-stu-id="17a4b-381">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="17a4b-382">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-382">**Solution**</span></span> | <span data-ttu-id="17a4b-383">Verifique os logs para obter mais informações</span><span class="sxs-lookup"><span data-stu-id="17a4b-383">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="17a4b-384">NU1500</span><span class="sxs-lookup"><span data-stu-id="17a4b-384">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-385">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-385">**Issue**</span></span> | <span data-ttu-id="17a4b-386">Um aviso interno não específico do NuGet.</span><span class="sxs-lookup"><span data-stu-id="17a4b-386">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="17a4b-387">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-387">**Solution**</span></span> | <span data-ttu-id="17a4b-388">Verifique os logs para obter mais informações</span><span class="sxs-lookup"><span data-stu-id="17a4b-388">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="17a4b-389">Pacotes assinados (criação e verificação)</span><span class="sxs-lookup"><span data-stu-id="17a4b-389">Signed packages (creation and verification)</span></span>

<span data-ttu-id="17a4b-390">*NuGet 4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="17a4b-390">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="17a4b-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="17a4b-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="17a4b-392">NU3000</span><span class="sxs-lookup"><span data-stu-id="17a4b-392">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-393">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-393">**Issue**</span></span> | <span data-ttu-id="17a4b-394">Um erro não específico relacionado à assinatura do pacote e assinado verificação do pacote.</span><span class="sxs-lookup"><span data-stu-id="17a4b-394">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="17a4b-395">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-395">**Solution**</span></span> | <span data-ttu-id="17a4b-396">Verifique os logs para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="17a4b-396">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="17a4b-397">NU3001</span><span class="sxs-lookup"><span data-stu-id="17a4b-397">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-398">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-398">**Issue**</span></span> | <span data-ttu-id="17a4b-399">Argumentos inválidos para o o [sign comando](../tools/cli-ref-sign.md) ou [Verifique se o comando](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="17a4b-399">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="17a4b-400">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-400">**Solution**</span></span> | <span data-ttu-id="17a4b-401">Verifique e corrija os argumentos fornecidos.</span><span class="sxs-lookup"><span data-stu-id="17a4b-401">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="17a4b-402">NU3002</span><span class="sxs-lookup"><span data-stu-id="17a4b-402">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-403">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-403">**Issue**</span></span> | <span data-ttu-id="17a4b-404">O `-Timestamper` opção não foi especificada com o [comando de entrada do nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="17a4b-404">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="17a4b-405">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-405">**Example message**</span></span> | <span data-ttu-id="17a4b-406">*O '-Timestamper' opção não foi fornecida. O pacote assinado não poderá ser a marca.*</span><span class="sxs-lookup"><span data-stu-id="17a4b-406">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="17a4b-407">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-407">**Solution**</span></span> | <span data-ttu-id="17a4b-408">Especifique o `-Timestamper` com a opção `nuget sign`.</span><span class="sxs-lookup"><span data-stu-id="17a4b-408">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="17a4b-409">NU3004</span><span class="sxs-lookup"><span data-stu-id="17a4b-409">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-410">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-410">**Issue**</span></span> | <span data-ttu-id="17a4b-411">Um pacote não assinado foi fornecido para o [nuget Verifique se o comando](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="17a4b-411">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="17a4b-412">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-412">**Solution**</span></span> | <span data-ttu-id="17a4b-413">Executar `nuget verify` com um pacote assinado.</span><span class="sxs-lookup"><span data-stu-id="17a4b-413">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="17a4b-414">Consulte [assinar um pacote](../create-packages/Sign-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="17a4b-414">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="17a4b-415">NU3008</span><span class="sxs-lookup"><span data-stu-id="17a4b-415">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-416">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-416">**Issue**</span></span> | <span data-ttu-id="17a4b-417">Falha na verificação de integridade do pacote, que significa que um pacote assinado foi violado desde que está sendo assinado.</span><span class="sxs-lookup"><span data-stu-id="17a4b-417">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="17a4b-418">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-418">**Solution**</span></span> | <span data-ttu-id="17a4b-419">Examine o computador com um software antivírus.</span><span class="sxs-lookup"><span data-stu-id="17a4b-419">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="17a4b-420">Remova o pacote do computador, reinstale-o e tente a operação novamente.</span><span class="sxs-lookup"><span data-stu-id="17a4b-420">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="17a4b-421">Se o problema persistir, contate o proprietário da origem do pacote e o pacote.</span><span class="sxs-lookup"><span data-stu-id="17a4b-421">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="17a4b-422">NU3018</span><span class="sxs-lookup"><span data-stu-id="17a4b-422">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-423">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-423">**Issue**</span></span> | <span data-ttu-id="17a4b-424">Falha na criação da cadeia de certificados para a assinatura principal.</span><span class="sxs-lookup"><span data-stu-id="17a4b-424">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="17a4b-425">O certificado de autenticação primário é confiável, revogado, ou informações de revogação do certificado não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="17a4b-425">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="17a4b-426">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-426">**Example message**</span></span> | <span data-ttu-id="17a4b-427">*Aviso: NU3018: A função de revogação não pôde verificar a revogação do certificado.*</span><span class="sxs-lookup"><span data-stu-id="17a4b-427">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="17a4b-428">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-428">**Solution**</span></span> | <span data-ttu-id="17a4b-429">Use um certificado válido e não confiáveis.</span><span class="sxs-lookup"><span data-stu-id="17a4b-429">Use a trusted and valid certificate.</span></span> <span data-ttu-id="17a4b-430">Verifique a conectividade com a internet.</span><span class="sxs-lookup"><span data-stu-id="17a4b-430">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="17a4b-431">NU3028</span><span class="sxs-lookup"><span data-stu-id="17a4b-431">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="17a4b-432">**Issue**</span><span class="sxs-lookup"><span data-stu-id="17a4b-432">**Issue**</span></span> | <span data-ttu-id="17a4b-433">Falha na criação da cadeia de certificados para a assinatura de carimbo de hora.</span><span class="sxs-lookup"><span data-stu-id="17a4b-433">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="17a4b-434">O certificado de assinatura de carimbo de hora é confiável, revogado, ou informações de revogação do certificado não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="17a4b-434">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="17a4b-435">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="17a4b-435">**Example message**</span></span> | <span data-ttu-id="17a4b-436">*Aviso: NU3028: A função de revogação não pôde verificar a revogação do certificado.*</span><span class="sxs-lookup"><span data-stu-id="17a4b-436">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="17a4b-437">**Solução**</span><span class="sxs-lookup"><span data-stu-id="17a4b-437">**Solution**</span></span> | <span data-ttu-id="17a4b-438">Use um certificado válido e não confiáveis.</span><span class="sxs-lookup"><span data-stu-id="17a4b-438">Use a trusted and valid certificate.</span></span> <span data-ttu-id="17a4b-439">Verifique a conectividade com a internet.</span><span class="sxs-lookup"><span data-stu-id="17a4b-439">Check internet connectivity.</span></span> |
