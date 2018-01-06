---
title: "Referência de erros e avisos a restauração do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b76b8a00-7155-4163-b533-894086d2ef78
description: "Referência completa para avisos e erros emitidos durante a restauração do pacote do NuGet"
keywords: "NuGet erros, avisos do NuGet, diagnóstico"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53fccbb86f2920d870b5383070d043e25045a626
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="15536-104">Erros e avisos</span><span class="sxs-lookup"><span data-stu-id="15536-104">Errors and warnings</span></span>

<span data-ttu-id="15536-105">NuGet 4.3.0, erros e avisos são numerados conforme descrito neste tópico e fornecem informações detalhadas para ajudá-lo a resolver os problemas envolvidos.</span><span class="sxs-lookup"><span data-stu-id="15536-105">In NuGet 4.3.0, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span> 

<span data-ttu-id="15536-106">Os erros e avisos listados aqui estão disponíveis apenas com [com base em PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) NuGet 4.3.0 e projetos.</span><span class="sxs-lookup"><span data-stu-id="15536-106">The errors and warnings listed here are available only with [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) projects and NuGet 4.3.0.</span></span> <span data-ttu-id="15536-107">NuGet também respeita propriedades MSBuild para suprimir avisos ou elevá-las a erros.</span><span class="sxs-lookup"><span data-stu-id="15536-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="15536-108">Para obter mais informações, consulte [como: suprimir avisos do compilador](/visualstudio/ide/how-to-suppress-compiler-warnings) na documentação do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15536-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="15536-109">**Erros**</span><span class="sxs-lookup"><span data-stu-id="15536-109">**Errors**</span></span>

| <span data-ttu-id="15536-110">Grupo</span><span class="sxs-lookup"><span data-stu-id="15536-110">Group</span></span> | <span data-ttu-id="15536-111">Números de erro</span><span class="sxs-lookup"><span data-stu-id="15536-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="15536-112">Erros de entrada inválidos</span><span class="sxs-lookup"><span data-stu-id="15536-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="15536-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="15536-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="15536-114">Erros de pacote e projeto ausentes</span><span class="sxs-lookup"><span data-stu-id="15536-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="15536-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (anteriormente NU1607) [NU1108](#nu1107) (anteriormente NU1606)</span><span class="sxs-lookup"><span data-stu-id="15536-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1107) (previously NU1606)</span></span> |
| [<span data-ttu-id="15536-116">Erros de compatibilidade</span><span class="sxs-lookup"><span data-stu-id="15536-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="15536-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="15536-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="15536-118">**Avisos**</span><span class="sxs-lookup"><span data-stu-id="15536-118">**Warnings**</span></span>

| <span data-ttu-id="15536-119">Grupo</span><span class="sxs-lookup"><span data-stu-id="15536-119">Group</span></span> | <span data-ttu-id="15536-120">Números de aviso</span><span class="sxs-lookup"><span data-stu-id="15536-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="15536-121">Avisos de entrada inválidos</span><span class="sxs-lookup"><span data-stu-id="15536-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="15536-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="15536-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="15536-123">Avisos de versão de pacote inesperado</span><span class="sxs-lookup"><span data-stu-id="15536-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="15536-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="15536-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="15536-125">Avisos de conflito de resolução</span><span class="sxs-lookup"><span data-stu-id="15536-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="15536-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="15536-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="15536-127">Avisos de fallback do pacote</span><span class="sxs-lookup"><span data-stu-id="15536-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="15536-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="15536-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="15536-129">Avisos de feeds</span><span class="sxs-lookup"><span data-stu-id="15536-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="15536-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="15536-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="15536-131">Avisos e erros internos do NuGet</span><span class="sxs-lookup"><span data-stu-id="15536-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="15536-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="15536-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="15536-133">Erros de entrada inválidos</span><span class="sxs-lookup"><span data-stu-id="15536-133">Invalid input errors</span></span>

<span data-ttu-id="15536-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="15536-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="15536-135">NU1001</span><span class="sxs-lookup"><span data-stu-id="15536-135">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-136">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-136">**Issue**</span></span> | <span data-ttu-id="15536-137">O projeto não contém um ou mais frameworks.</span><span class="sxs-lookup"><span data-stu-id="15536-137">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="15536-138">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-138">**Common causes**</span></span> | <span data-ttu-id="15536-139">O projeto não contém um `TargetFramework` ou `TargetFrameworks` propriedade.</span><span class="sxs-lookup"><span data-stu-id="15536-139">The project doesn't contain a `TargetFramework` or `TargetFrameworks` property.</span></span> |
| <span data-ttu-id="15536-140">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-140">**Example message**</span></span> | <span data-ttu-id="15536-141">*O projeto projA não especifica nenhuma estrutura de destino em c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="15536-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |

### <a name="nu1002"></a><span data-ttu-id="15536-142">NU1002</span><span class="sxs-lookup"><span data-stu-id="15536-142">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-143">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-143">**Issue**</span></span> | <span data-ttu-id="15536-144">Combinação inválida de entradas, junto com uma palavra-chave criptografada.</span><span class="sxs-lookup"><span data-stu-id="15536-144">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="15536-145">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-145">**Common causes**</span></span> | <span data-ttu-id="15536-146">CLEAR não pode ser combinado com outras entradas.</span><span class="sxs-lookup"><span data-stu-id="15536-146">CLEAR may not be combined with other inputs.</span></span> |
| <span data-ttu-id="15536-147">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-147">**Example message**</span></span> | <span data-ttu-id="15536-148">*'CLEAR' não pode ser usado em conjunto com outros valores*</span><span class="sxs-lookup"><span data-stu-id="15536-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |

### <a name="nu1003"></a><span data-ttu-id="15536-149">NU1003</span><span class="sxs-lookup"><span data-stu-id="15536-149">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-150">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-150">**Issue**</span></span> | <span data-ttu-id="15536-151">`PackageTargetFallback`e `AssetTargetFallback` fornecem um comportamento diferente para a seleção de recursos e não podem ser usados juntos.</span><span class="sxs-lookup"><span data-stu-id="15536-151">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="15536-152">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-152">**Common causes**</span></span> | <span data-ttu-id="15536-153">Ambos `PackageTargetFallback` e `AssetTargetFallback` existe no projeto.</span><span class="sxs-lookup"><span data-stu-id="15536-153">Both `PackageTargetFallback` and `AssetTargetFallback` exist in the project.</span></span> |
| <span data-ttu-id="15536-154">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-154">**Example message**</span></span> | <span data-ttu-id="15536-155">*PackageTargetFallback e AssetTargetFallback não podem ser usados juntos. Remova as referências de PackageTargetFallback(deprecated) do ambiente do projeto.*</span><span class="sxs-lookup"><span data-stu-id="15536-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="15536-156">Erros de pacote e projeto ausentes</span><span class="sxs-lookup"><span data-stu-id="15536-156">Missing package and project errors</span></span>

<span data-ttu-id="15536-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104 ](#nu1104)  |  [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="15536-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="15536-158">NU1100</span><span class="sxs-lookup"><span data-stu-id="15536-158">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-159">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-159">**Issue**</span></span> | <span data-ttu-id="15536-160">Um grupo de dependência não ser resolvido.</span><span class="sxs-lookup"><span data-stu-id="15536-160">A dependency group not be resolved.</span></span> <span data-ttu-id="15536-161">Esse é um problema genérico para tipos que não são pacotes ou projetos.</span><span class="sxs-lookup"><span data-stu-id="15536-161">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="15536-162">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-162">**Common causes**</span></span> | <span data-ttu-id="15536-163">O projeto contém uma dependência em um item que não existe.</span><span class="sxs-lookup"><span data-stu-id="15536-163">The project contains a dependency on an item that doesn't exist.</span></span> |
| <span data-ttu-id="15536-164">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-164">**Example message**</span></span> | <span data-ttu-id="15536-165">*Não é possível resolver System.Missing para net45*</span><span class="sxs-lookup"><span data-stu-id="15536-165">*Unable to resolve System.Missing for net45*</span></span> |

### <a name="nu1101"></a><span data-ttu-id="15536-166">NU1101</span><span class="sxs-lookup"><span data-stu-id="15536-166">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-167">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-167">**Issue**</span></span> | <span data-ttu-id="15536-168">O pacote não foi encontrado em qualquer fonte.</span><span class="sxs-lookup"><span data-stu-id="15536-168">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="15536-169">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-169">**Common causes**</span></span> | <span data-ttu-id="15536-170">A origem do pacote correto está ausente ou o identificador de pacote está incorreto.</span><span class="sxs-lookup"><span data-stu-id="15536-170">The correct package source is missing or the package identifier is incorrect.</span></span> |
| <span data-ttu-id="15536-171">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-171">**Example message**</span></span> | <span data-ttu-id="15536-172">*Não é possível encontrar o pacote System.Missing. Nenhum pacote existe com essa id na fonte (s): dotnet-core, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="15536-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |

### <a name="nu1102"></a><span data-ttu-id="15536-173">NU1102</span><span class="sxs-lookup"><span data-stu-id="15536-173">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-174">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-174">**Issue**</span></span> | <span data-ttu-id="15536-175">O identificador de pacote for encontrado, mas não é possível encontrar uma versão dentro do intervalo de dependência especificada em qualquer uma das fontes.</span><span class="sxs-lookup"><span data-stu-id="15536-175">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> |
| <span data-ttu-id="15536-176">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-176">**Common causes**</span></span> | <span data-ttu-id="15536-177">A origem do pacote correto está ausente ou o intervalo de dependência está incorreto.</span><span class="sxs-lookup"><span data-stu-id="15536-177">The correct package source is missing or the dependency range is incorrect.</span></span> <span data-ttu-id="15536-178">O intervalo pode ser especificado por um pacote e não ao usuário.</span><span class="sxs-lookup"><span data-stu-id="15536-178">The range might be specified by a package and not the user.</span></span> <span data-ttu-id="15536-179">O usuário talvez precise alternar para uma versão disponível se esse pacote é referenciado pelo projeto diretamente.</span><span class="sxs-lookup"><span data-stu-id="15536-179">The user may need to switch to an available version if this package is referenced by the project directly.</span></span> |
| <span data-ttu-id="15536-180">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-180">**Example message**</span></span> | <span data-ttu-id="15536-181">*Não é possível localizar o pacote NuGet.Versioning com a versão (> = 9.0.1)<br/> -versão (ões) de 30 encontrado em nuget.org [mais próximo de versão: 4.0.0]<br/> -versão (ões) de 10 encontrado em dotnet buildtools [mais próximo de versão: 4.0.0-rc-2129]<br/> -9 encontrado versão (ões) em NuGetVolatile [mais próximo de versão: 3.0.0-beta-00032]<br/> -encontrado versões 0 no núcleo do dotnet<br/> -encontrado versões 0 no roslyn dotnet*</span><span class="sxs-lookup"><span data-stu-id="15536-181">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1103"></a><span data-ttu-id="15536-182">NU1103</span><span class="sxs-lookup"><span data-stu-id="15536-182">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-183">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-183">**Issue**</span></span> | <span data-ttu-id="15536-184">Nenhuma versão estável foram encontrado no intervalo de dependência.</span><span class="sxs-lookup"><span data-stu-id="15536-184">No stable versions were found in the dependency range.</span></span> <span data-ttu-id="15536-185">As versões de pré-lançamento foram encontradas, mas não são permitidas.</span><span class="sxs-lookup"><span data-stu-id="15536-185">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="15536-186">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-186">**Common causes**</span></span> | <span data-ttu-id="15536-187">O projeto especificado para o intervalo de dependência a uma versão estável.</span><span class="sxs-lookup"><span data-stu-id="15536-187">The project specified a stable version for the dependency range.</span></span> <span data-ttu-id="15536-188">Os usuários precisam alterar o intervalo de versão para incluir as versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="15536-188">Users need to change the version range to include pre-release versions.</span></span> |
| <span data-ttu-id="15536-189">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-189">**Example message**</span></span> | <span data-ttu-id="15536-190">*Não é possível localizar um pacote estável NuGet.Versioning com a versão (> = 3.0.0)<br/> -versão (ões) de 10 encontrado em dotnet buildtools [mais próximo de versão: 4.0.0-rc-2129]<br/> -versão (ões) de 9 encontrado em NuGetVolatile [mais próximo de versão: 3.0.0-beta-00032] <br/> -Encontrado versões 0 no núcleo do dotnet<br/> -encontrado versões 0 no roslyn dotnet*</span><span class="sxs-lookup"><span data-stu-id="15536-190">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1104"></a><span data-ttu-id="15536-191">NU1104</span><span class="sxs-lookup"><span data-stu-id="15536-191">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-192">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-192">**Issue**</span></span> | <span data-ttu-id="15536-193">Um ProjectReference aponta para um arquivo que não existe.</span><span class="sxs-lookup"><span data-stu-id="15536-193">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="15536-194">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-194">**Common causes**</span></span> | <span data-ttu-id="15536-195">O arquivo de projeto está ausente do disco ou a referência está incorreta.</span><span class="sxs-lookup"><span data-stu-id="15536-195">The project file is missing from disk or the reference is incorrect.</span></span> |
| <span data-ttu-id="15536-196">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-196">**Example message**</span></span> | <span data-ttu-id="15536-197">*Referência de projeto não existe 'c:\a.csproj'. Verifique se a referência de projeto é válida e se existe o arquivo de projeto.*</span><span class="sxs-lookup"><span data-stu-id="15536-197">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |

### <a name="nu1105"></a><span data-ttu-id="15536-198">NU1105</span><span class="sxs-lookup"><span data-stu-id="15536-198">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-199">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-199">**Issue**</span></span> | <span data-ttu-id="15536-200">O arquivo de projeto existe, mas nenhuma informação de restauração foi fornecida para ele.</span><span class="sxs-lookup"><span data-stu-id="15536-200">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="15536-201">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-201">**Common causes**</span></span> | <span data-ttu-id="15536-202">No Visual Studio, isso pode significar que o projeto está descarregado.</span><span class="sxs-lookup"><span data-stu-id="15536-202">In Visual Studio this could mean that the project is unloaded.</span></span> <span data-ttu-id="15536-203">Na linha de comando, isso pode significar que o arquivo está corrompido ou que não contenha personalizado após o destino de importações necessário para restauração ler o projeto.</span><span class="sxs-lookup"><span data-stu-id="15536-203">From the command line this could mean that the file is corrupt or that it doesn't contain the custom after imports target needed for restore to read the project.</span></span> |
| <span data-ttu-id="15536-204">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-204">**Example message**</span></span> | <span data-ttu-id="15536-205">*Não é possível ler as informações de projeto para 'c:\a.csproj'. O arquivo de projeto pode ser inválidos ou ausentes destinos necessários para a restauração.*</span><span class="sxs-lookup"><span data-stu-id="15536-205">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

### <a name="nu1106"></a><span data-ttu-id="15536-206">NU1106</span><span class="sxs-lookup"><span data-stu-id="15536-206">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-207">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-207">**Issue**</span></span> | <span data-ttu-id="15536-208">Restrições de dependência não podem ser resolvidas.</span><span class="sxs-lookup"><span data-stu-id="15536-208">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="15536-209">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-209">**Common causes**</span></span> | <span data-ttu-id="15536-210">Os pacotes contêm dependência em versões exatas de um pacote em vez de intervalos abertos.</span><span class="sxs-lookup"><span data-stu-id="15536-210">Packages contain dependency on exact versions of a package instead of open-ended ranges.</span></span> |
| <span data-ttu-id="15536-211">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-211">**Example message**</span></span> | <span data-ttu-id="15536-212">*Não foi possível satisfazer solicitações conflitantes para {id}: {caminho conflito} Framework: {gráfico de destino}*</span><span class="sxs-lookup"><span data-stu-id="15536-212">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |

<span data-ttu-id="15536-213">< a name = "NU1107 ></a></span><span class="sxs-lookup"><span data-stu-id="15536-213"><a name="NU1107></a></span></span>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="15536-214">NU1107 (anteriormente NU1607)</span><span class="sxs-lookup"><span data-stu-id="15536-214">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-215">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-215">**Issue**</span></span> | <span data-ttu-id="15536-216">Não é possível resolver as restrições de dependência entre pacotes.</span><span class="sxs-lookup"><span data-stu-id="15536-216">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="15536-217">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-217">**Common causes**</span></span> | <span data-ttu-id="15536-218">Pacotes com restrições de dependência em versões exatas não permitir que outros pacotes para aumentar a versão, se necessário.</span><span class="sxs-lookup"><span data-stu-id="15536-218">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> |
| <span data-ttu-id="15536-219">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-219">**Example message**</span></span> | <span data-ttu-id="15536-220">*Conflito de versão detectado para NuGet.Versioning. Referenciar o pacote diretamente do projeto para resolver esse problema.<br/>  NuGet. Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="15536-220">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |

<span data-ttu-id="15536-221">< a name = "NU1108 ></a></span><span class="sxs-lookup"><span data-stu-id="15536-221"><a name="NU1108></a></span></span>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="15536-222">NU1108 (anteriormente NU1606)</span><span class="sxs-lookup"><span data-stu-id="15536-222">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-223">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-223">**Issue**</span></span> | <span data-ttu-id="15536-224">Foi detectada uma dependência circular.</span><span class="sxs-lookup"><span data-stu-id="15536-224">A circular dependency was detected.</span></span> |
| <span data-ttu-id="15536-225">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-225">**Common causes**</span></span> | <span data-ttu-id="15536-226">Um pacote foi criado incorretamente.</span><span class="sxs-lookup"><span data-stu-id="15536-226">A package is authored incorrectly.</span></span> |
| <span data-ttu-id="15536-227">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-227">**Example message**</span></span> | <span data-ttu-id="15536-228">*Ciclo detectado: A -> B -> um*</span><span class="sxs-lookup"><span data-stu-id="15536-228">*Cycle detected: A -> B -> A*</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="15536-229">Erros de compatibilidade</span><span class="sxs-lookup"><span data-stu-id="15536-229">Compatibility errors</span></span>

<span data-ttu-id="15536-230">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="15536-230">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="15536-231">NU1201</span><span class="sxs-lookup"><span data-stu-id="15536-231">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-232">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-232">**Issue**</span></span> | <span data-ttu-id="15536-233">Um projeto de dependência não contém uma estrutura compatível com o projeto atual.</span><span class="sxs-lookup"><span data-stu-id="15536-233">A dependency project doesn't contain a framework compatible with the current project.</span></span> |
| <span data-ttu-id="15536-234">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-234">**Common causes**</span></span> | <span data-ttu-id="15536-235">Estrutura de destino do projeto é uma versão superior do projeto de consumo.</span><span class="sxs-lookup"><span data-stu-id="15536-235">The project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="15536-236">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-236">**Example message**</span></span> | <span data-ttu-id="15536-237">*ServerWeb do projeto não é compatível com netstandard1.3 (. Identificadores de NETStandard, versão = v 1.3). Projeto suporta ServerWeb:<br/> -netstandard1.6 (. Identificadores de NETStandard, versão = v 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = v 1.0)*</span><span class="sxs-lookup"><span data-stu-id="15536-237">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |

### <a name="nu1202"></a><span data-ttu-id="15536-238">NU1202</span><span class="sxs-lookup"><span data-stu-id="15536-238">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-239">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-239">**Issue**</span></span> | <span data-ttu-id="15536-240">Um pacote de dependência não contém qualquer ativos compatíveis com o projeto.</span><span class="sxs-lookup"><span data-stu-id="15536-240">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="15536-241">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-241">**Common causes**</span></span> | <span data-ttu-id="15536-242">O pacote não dá suporte a estrutura de destino do projeto.</span><span class="sxs-lookup"><span data-stu-id="15536-242">The package doesn't support the project's target framework.</span></span> |
| <span data-ttu-id="15536-243">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-243">**Example message**</span></span> | <span data-ttu-id="15536-244">*Pacote System.ComponentModel.EventBasedAsync 4.0.11 não é compatível com netstandard1.3 (. Identificadores de NETStandard, versão = v 1.3). Pacote suporta System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, versão = v 1.0)<br/> -monotouch10 (MonoTouch, versão = v 1.0)<br/> -net45 (. NETFramework, Version = v 4.5)<br/> -netcore50 (. NETCore, Version = v 5.0)<br/> -netstandard1.0 (. Identificadores de NETStandard, versão = v 1.0)<br/> -portátil net45 + win8 + wp8 + wpa81 (. NETPortable, Version = v0.0, perfil = Profile259)<br/> -win8 (Windows, versão = v 8.0)<br/> -wp8 (WindowsPhone, versão = v 8.0)<br/> -wpa81 (WindowsPhoneApp, versão = 8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="15536-244">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|

### <a name="nu1203"></a><span data-ttu-id="15536-245">NU1203</span><span class="sxs-lookup"><span data-stu-id="15536-245">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-246">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-246">**Issue**</span></span> | <span data-ttu-id="15536-247">O pacote não oferece suporte para o projeto `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="15536-247">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="15536-248">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-248">**Common causes**</span></span> | <span data-ttu-id="15536-249">O pacote não dá suporte a atual `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="15536-249">The package doesn't support the current `RuntimeIdentifier`.</span></span> <span data-ttu-id="15536-250">Alterar o `RuntimeIdentifier` valores usados no projeto, se necessário.</span><span class="sxs-lookup"><span data-stu-id="15536-250">Change the `RuntimeIdentifier` values used in the project if needed.</span></span> |
| <span data-ttu-id="15536-251">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-251">**Example message**</span></span> | <span data-ttu-id="15536-252">*System.Example 1.0.0 fornece uma referência de tempo de compilação do assembly para o. dll em net461, mas não há nenhum tempo de execução do assembly compatível.*</span><span class="sxs-lookup"><span data-stu-id="15536-252">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |

### <a name="nu1401"></a><span data-ttu-id="15536-253">NU1401</span><span class="sxs-lookup"><span data-stu-id="15536-253">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-254">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-254">**Issue**</span></span> | <span data-ttu-id="15536-255">O pacote requer recursos ou estruturas atualmente não há suportadas à versão instalada do NuGet.</span><span class="sxs-lookup"><span data-stu-id="15536-255">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="15536-256">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-256">**Common causes**</span></span> | <span data-ttu-id="15536-257">Atualize o NuGet para corrigir o problema.</span><span class="sxs-lookup"><span data-stu-id="15536-257">Upgrade NuGet to fix the issue.</span></span> |
| <span data-ttu-id="15536-258">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-258">**Example message**</span></span> | <span data-ttu-id="15536-259">*O pacote 'NuGet.Versioning' requer o NuGet versão de cliente '5.0.0' ou superior, mas a versão atual do NuGet é '4.3.0'. Para atualizar o NuGet, acesse http://docs.nuget.org/consume/installing-nuget.*</span><span class="sxs-lookup"><span data-stu-id="15536-259">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'. To upgrade NuGet, please go to http://docs.nuget.org/consume/installing-nuget.*</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="15536-260">Avisos de entrada inválidos</span><span class="sxs-lookup"><span data-stu-id="15536-260">Invalid input warnings</span></span>

<span data-ttu-id="15536-261">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="15536-261">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="15536-262">NU1501</span><span class="sxs-lookup"><span data-stu-id="15536-262">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-263">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-263">**Issue**</span></span> | <span data-ttu-id="15536-264">A restauração do projeto está tentando operar em não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="15536-264">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="15536-265">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-265">**Common causes**</span></span> | <span data-ttu-id="15536-266">O projeto está ausente.</span><span class="sxs-lookup"><span data-stu-id="15536-266">The project is missing.</span></span> |
| <span data-ttu-id="15536-267">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-267">**Example message**</span></span> | <span data-ttu-id="15536-268">*A pasta 'c:\projects\a' não contém um projeto para restaurar.*</span><span class="sxs-lookup"><span data-stu-id="15536-268">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |

### <a name="nu1502"></a><span data-ttu-id="15536-269">NU1502</span><span class="sxs-lookup"><span data-stu-id="15536-269">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-270">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-270">**Issue**</span></span> | <span data-ttu-id="15536-271">`RuntimeSupports`contém um perfil inválido.</span><span class="sxs-lookup"><span data-stu-id="15536-271">`RuntimeSupports` contains an invalid profile.</span></span> |
| <span data-ttu-id="15536-272">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-272">**Common causes**</span></span> | <span data-ttu-id="15536-273">O dá suporte a perfil não foi encontrado em um `runtime.json` arquivo dos pacotes de dependência atual.</span><span class="sxs-lookup"><span data-stu-id="15536-273">The supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span> |
| <span data-ttu-id="15536-274">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-274">**Example message**</span></span> | <span data-ttu-id="15536-275">*Perfil de compatibilidade desconhecido: aaa*</span><span class="sxs-lookup"><span data-stu-id="15536-275">*Unknown Compatibility Profile: aaa*</span></span> |

### <a name="nu1503"></a><span data-ttu-id="15536-276">NU1503</span><span class="sxs-lookup"><span data-stu-id="15536-276">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-277">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-277">**Issue**</span></span> | <span data-ttu-id="15536-278">Um projeto de dependência não importa destinos de restauração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="15536-278">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="15536-279">Isso é semelhante a NU1105, mas aqui o projeto será ignorado e ignorado em vez fazendo com que todos os de restauração falhe.</span><span class="sxs-lookup"><span data-stu-id="15536-279">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="15536-280">Em soluções complexas geralmente há outros tipos de projetos que podem não oferecer suporte a restauração.</span><span class="sxs-lookup"><span data-stu-id="15536-280">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="15536-281">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-281">**Common causes**</span></span> | <span data-ttu-id="15536-282">Isso pode acontecer para projetos que não importar props/destinos comuns que importar automaticamente a restauração.</span><span class="sxs-lookup"><span data-stu-id="15536-282">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="15536-283">Se o projeto não precisa ser restaurados isso pode ser ignorado.</span><span class="sxs-lookup"><span data-stu-id="15536-283">If the project doesn't need to be restored this can be ignored.</span></span> |
| <span data-ttu-id="15536-284">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-284">**Example message**</span></span> | <span data-ttu-id="15536-285">*Ignorando a restauração para o projeto 'c:\a.csproj'. O arquivo de projeto pode ser inválidos ou ausentes destinos necessários para a restauração.*</span><span class="sxs-lookup"><span data-stu-id="15536-285">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="15536-286">Avisos de versão de pacote inesperado</span><span class="sxs-lookup"><span data-stu-id="15536-286">Unexpected package version warnings</span></span>

<span data-ttu-id="15536-287">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="15536-287">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="15536-288">NU1601</span><span class="sxs-lookup"><span data-stu-id="15536-288">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-289">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-289">**Issue**</span></span> | <span data-ttu-id="15536-290">Uma dependência de projeto foi aumentada para uma versão maior do que o projeto especificado.</span><span class="sxs-lookup"><span data-stu-id="15536-290">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="15536-291">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-291">**Common causes**</span></span> | <span data-ttu-id="15536-292">Outro pacote de dependência necessária uma versão mais recente e aumentado o pacote em.</span><span class="sxs-lookup"><span data-stu-id="15536-292">Another dependency package required a higher version and bumped the package up.</span></span> |
| <span data-ttu-id="15536-293">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-293">**Example message**</span></span> | <span data-ttu-id="15536-294">*Dependência especificada foi NuGet.Versioning (> = 3.5.0) mas acabou com NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="15536-294">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |

### <a name="nu1602"></a><span data-ttu-id="15536-295">NU1602</span><span class="sxs-lookup"><span data-stu-id="15536-295">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-296">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-296">**Issue**</span></span> | <span data-ttu-id="15536-297">Uma dependência de pacote não tem um limite inferior.</span><span class="sxs-lookup"><span data-stu-id="15536-297">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="15536-298">Isso não permite que a restauração localizar o *melhor correspondência*.</span><span class="sxs-lookup"><span data-stu-id="15536-298">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="15536-299">Cada restauração flutua para baixo ao tentar encontrar uma versão inferior que pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="15536-299">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="15536-300">Isso significa que a restauração fica online para verificar se todas as fontes de cada vez em vez de usar os pacotes que já existem na pasta de pacote do usuário.</span><span class="sxs-lookup"><span data-stu-id="15536-300">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="15536-301">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-301">**Common causes**</span></span> | <span data-ttu-id="15536-302">Isso geralmente é um erro de criação de pacote.</span><span class="sxs-lookup"><span data-stu-id="15536-302">This is usually a package authoring error.</span></span> |
| <span data-ttu-id="15536-303">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-303">**Example message**</span></span> | <span data-ttu-id="15536-304">*NuGet. Packaging 4.0.0 não fornece um limite inferior inclusivo de dependência NuGet.Versioning (3.5.0 >). Uma melhor correspondência aproximada de 3.6.0 foi resolvida.*</span><span class="sxs-lookup"><span data-stu-id="15536-304">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |

### <a name="nu1603"></a><span data-ttu-id="15536-305">NU1603</span><span class="sxs-lookup"><span data-stu-id="15536-305">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-306">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-306">**Issue**</span></span> | <span data-ttu-id="15536-307">Uma dependência de pacote especificado de uma versão que não pôde ser encontrada.</span><span class="sxs-lookup"><span data-stu-id="15536-307">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="15536-308">Uma versão mais recente foi usada em vez disso, o que é diferente do que o pacote foi criado.</span><span class="sxs-lookup"><span data-stu-id="15536-308">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="15536-309">Isso significa que a restauração não localizou o *melhor correspondência*.</span><span class="sxs-lookup"><span data-stu-id="15536-309">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="15536-310">Cada restauração flutua para baixo ao tentar encontrar uma versão inferior que pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="15536-310">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="15536-311">Isso significa que a restauração fica online para verificar se todas as fontes de cada vez em vez de usar os pacotes que já existem na pasta de pacote do usuário.</span><span class="sxs-lookup"><span data-stu-id="15536-311">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="15536-312">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-312">**Common causes**</span></span> | <span data-ttu-id="15536-313">As fontes de pacote contém a versão inferior esperado.</span><span class="sxs-lookup"><span data-stu-id="15536-313">The package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="15536-314">Se o pacote esperado não foi liberado, em seguida, isso pode ser um erro de criação de pacote.</span><span class="sxs-lookup"><span data-stu-id="15536-314">If the package expected has not been released then this may be a package authoring error.</span></span> |
| <span data-ttu-id="15536-315">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-315">**Example message**</span></span> | <span data-ttu-id="15536-316">NuGet. Packaging 4.0.0 depende NuGet.Versioning (> = 4.0.0) mas 4.0.0 não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="15536-316">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="15536-317">Uma melhor correspondência aproximada de 5.0.0 foi resolvida.</span><span class="sxs-lookup"><span data-stu-id="15536-317">An approximate best match of 5.0.0 was resolved.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="15536-318">NU1604</span><span class="sxs-lookup"><span data-stu-id="15536-318">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-319">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-319">**Issue**</span></span> | <span data-ttu-id="15536-320">Uma dependência de projeto não define um limite inferior.</span><span class="sxs-lookup"><span data-stu-id="15536-320">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="15536-321">Isso significa que a restauração não localizou o *melhor correspondência*.</span><span class="sxs-lookup"><span data-stu-id="15536-321">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="15536-322">Cada restauração flutua para baixo ao tentar encontrar uma versão inferior que pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="15536-322">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="15536-323">Isso significa que a restauração fica online para verificar se todas as fontes de cada vez em vez de usar os pacotes que já existem na pasta de pacote do usuário.</span><span class="sxs-lookup"><span data-stu-id="15536-323">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="15536-324">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-324">**Common causes**</span></span> | <span data-ttu-id="15536-325">O projeto *PackageReference* *versão* atributo deve ser atualizado para incluir um limite inferior.</span><span class="sxs-lookup"><span data-stu-id="15536-325">The project's *PackageReference* *Version* attribute should be updated to include a lower bound.</span></span> |
| <span data-ttu-id="15536-326">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-326">**Example message**</span></span> | <span data-ttu-id="15536-327">*Projeto dependência NuGet.Versioning (< = 9.0.0) doe não contêm um limite inferior inclusivo. Inclua um limite inferior na versão de dependência para garantir resultados consistentes de restauração.*</span><span class="sxs-lookup"><span data-stu-id="15536-327">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |

### <a name="nu1605"></a><span data-ttu-id="15536-328">NU1605</span><span class="sxs-lookup"><span data-stu-id="15536-328">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-329">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-329">**Issue**</span></span> | <span data-ttu-id="15536-330">Um pacote de dependência especificou uma restrição de versão em uma versão superior de um pacote de restauração finalmente resolvida.</span><span class="sxs-lookup"><span data-stu-id="15536-330">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> |
| <span data-ttu-id="15536-331">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-331">**Common causes**</span></span> | <span data-ttu-id="15536-332">Wins mais próximos ao resolver pacotes.</span><span class="sxs-lookup"><span data-stu-id="15536-332">Nearest wins when resolving packages.</span></span> <span data-ttu-id="15536-333">Um pacote distante pode ter substituído a um pacote mais próximo no gráfico.</span><span class="sxs-lookup"><span data-stu-id="15536-333">A nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="15536-334">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-334">**Example message**</span></span> | <span data-ttu-id="15536-335">*Detectado o downgrade do pacote: NuGet.Versioning de 4.0.0 para 3.5.0. Referenciar o pacote diretamente do projeto para selecionar uma versão diferente.<br/>  NuGet. Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="15536-335">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="15536-336">Avisos de conflito de resolução</span><span class="sxs-lookup"><span data-stu-id="15536-336">Resolver conflict warnings</span></span>

[<span data-ttu-id="15536-337">NU1608</span><span class="sxs-lookup"><span data-stu-id="15536-337">NU1608</span></span>](#nu1608)

### <a name="nu1608"></a><span data-ttu-id="15536-338">NU1608</span><span class="sxs-lookup"><span data-stu-id="15536-338">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-339">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-339">**Issue**</span></span> | <span data-ttu-id="15536-340">Um pacote de solução é maior do que permite que uma restrição de dependência.</span><span class="sxs-lookup"><span data-stu-id="15536-340">A resolve package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="15536-341">Em alguns casos, isso é intencional e o aviso pode ser suprimido.</span><span class="sxs-lookup"><span data-stu-id="15536-341">In some cases this is intentional and the warning can be suppressed.</span></span> |
| <span data-ttu-id="15536-342">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-342">**Common causes**</span></span> | <span data-ttu-id="15536-343">Um pacote referenciado diretamente por um projeto substituirão as restrições de dependência de outros pacotes.</span><span class="sxs-lookup"><span data-stu-id="15536-343">A package referenced directly by a project will override dependency constraints from other packages.</span></span>   |
| <span data-ttu-id="15536-344">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-344">**Example message**</span></span> | <span data-ttu-id="15536-345">*Versão do pacote detectado fora da restrição de dependência: x 1.0.0 requer y (= 1.0.0), mas a versão y 2.0.0 foi resolvido.*</span><span class="sxs-lookup"><span data-stu-id="15536-345">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="15536-346">Avisos de fallback do pacote</span><span class="sxs-lookup"><span data-stu-id="15536-346">Package fallback warnings</span></span>

[<span data-ttu-id="15536-347">NU1701</span><span class="sxs-lookup"><span data-stu-id="15536-347">NU1701</span></span>](#nu1701)

### <a name="nu1701"></a><span data-ttu-id="15536-348">NU1701</span><span class="sxs-lookup"><span data-stu-id="15536-348">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-349">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-349">**Issue**</span></span> | <span data-ttu-id="15536-350">*PackageTargetFallback/AssetTargetFallback* foi usado para selecionar os ativos de um pacote.</span><span class="sxs-lookup"><span data-stu-id="15536-350">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span></span> <span data-ttu-id="15536-351">Este é um aviso para informar o usuário que os ativos podem não ser 100% compatível.</span><span class="sxs-lookup"><span data-stu-id="15536-351">This is a warning to let the user know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="15536-352">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-352">**Common causes**</span></span> | <span data-ttu-id="15536-353">O pacote não dá suporte a estrutura do projeto.</span><span class="sxs-lookup"><span data-stu-id="15536-353">The package doesn't support the project framework.</span></span> |
| <span data-ttu-id="15536-354">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-354">**Example message**</span></span> | <span data-ttu-id="15536-355">*Pacote 'NuGet.Versioning' foi restaurado usando 'portátil net45 + win8' em vez disso, a estrutura de destino do projeto 'netstandard1.5'. Esse pacote pode não ser totalmente compatível com o seu projeto.*</span><span class="sxs-lookup"><span data-stu-id="15536-355">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="15536-356">Avisos de feeds</span><span class="sxs-lookup"><span data-stu-id="15536-356">Feed warnings</span></span>

[<span data-ttu-id="15536-357">NU1801</span><span class="sxs-lookup"><span data-stu-id="15536-357">NU1801</span></span>](#nu1801)

### <a name="nu1801"></a><span data-ttu-id="15536-358">NU1801</span><span class="sxs-lookup"><span data-stu-id="15536-358">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-359">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-359">**Issue**</span></span> | <span data-ttu-id="15536-360">Ocorreu um erro ao ler o feed quando `IgnoreFailedSources` está definido como true, convertendo-o para um aviso não fatal.</span><span class="sxs-lookup"><span data-stu-id="15536-360">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="15536-361">Isso pode conter qualquer mensagem e é genérico.</span><span class="sxs-lookup"><span data-stu-id="15536-361">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="15536-362">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-362">**Common causes**</span></span> | <span data-ttu-id="15536-363">A fonte é inválida.</span><span class="sxs-lookup"><span data-stu-id="15536-363">The source is invalid.</span></span> |
| <span data-ttu-id="15536-364">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="15536-364">**Example message**</span></span> | <span data-ttu-id="15536-365">N/D</span><span class="sxs-lookup"><span data-stu-id="15536-365">n/a</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="15536-366">Avisos e erros internos do NuGet</span><span class="sxs-lookup"><span data-stu-id="15536-366">NuGet internal errors and warnings</span></span>

<span data-ttu-id="15536-367">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="15536-367">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="15536-368">NU1000</span><span class="sxs-lookup"><span data-stu-id="15536-368">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-369">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-369">**Issue**</span></span> | <span data-ttu-id="15536-370">Um erro interno não específico do NuGet.</span><span class="sxs-lookup"><span data-stu-id="15536-370">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="15536-371">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-371">**Common causes**</span></span> | <span data-ttu-id="15536-372">Verifique os logs para obter mais informações</span><span class="sxs-lookup"><span data-stu-id="15536-372">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="15536-373">NU1500</span><span class="sxs-lookup"><span data-stu-id="15536-373">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="15536-374">**Problema**</span><span class="sxs-lookup"><span data-stu-id="15536-374">**Issue**</span></span> | <span data-ttu-id="15536-375">Um aviso interno não específico do NuGet.</span><span class="sxs-lookup"><span data-stu-id="15536-375">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="15536-376">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="15536-376">**Common causes**</span></span> | <span data-ttu-id="15536-377">Verifique os logs para obter mais informações</span><span class="sxs-lookup"><span data-stu-id="15536-377">Check the logs for more information</span></span> |
