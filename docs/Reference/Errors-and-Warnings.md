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
ms.openlocfilehash: 29eb72cbb6c095cd3aeb524fd8b28416ec5dc798
ms.sourcegitcommit: 6ccb963e065680ab2e7df1d8dd5492897fd56b04
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="5d20c-104">Erros e avisos</span><span class="sxs-lookup"><span data-stu-id="5d20c-104">Errors and warnings</span></span>

<span data-ttu-id="5d20c-105">NuGet 4.3.0, erros e avisos são numerados conforme descrito neste tópico e fornecem informações detalhadas para ajudá-lo a resolver os problemas envolvidos.</span><span class="sxs-lookup"><span data-stu-id="5d20c-105">In NuGet 4.3.0, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span> 

<span data-ttu-id="5d20c-106">Os erros e avisos listados aqui estão disponíveis apenas com [com base em PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) NuGet 4.3.0 e projetos.</span><span class="sxs-lookup"><span data-stu-id="5d20c-106">The errors and warnings listed here are available only with [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) projects and NuGet 4.3.0.</span></span> <span data-ttu-id="5d20c-107">NuGet também respeita propriedades MSBuild para suprimir avisos ou elevá-las a erros.</span><span class="sxs-lookup"><span data-stu-id="5d20c-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="5d20c-108">Para obter mais informações, consulte [como: suprimir avisos do compilador](/visualstudio/ide/how-to-suppress-compiler-warnings) na documentação do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5d20c-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="5d20c-109">**Erros**</span><span class="sxs-lookup"><span data-stu-id="5d20c-109">**Errors**</span></span>

| <span data-ttu-id="5d20c-110">Grupo</span><span class="sxs-lookup"><span data-stu-id="5d20c-110">Group</span></span> | <span data-ttu-id="5d20c-111">Números de erro</span><span class="sxs-lookup"><span data-stu-id="5d20c-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="5d20c-112">Erros de entrada inválidos</span><span class="sxs-lookup"><span data-stu-id="5d20c-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="5d20c-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="5d20c-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="5d20c-114">Erros de pacote e projeto ausentes</span><span class="sxs-lookup"><span data-stu-id="5d20c-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="5d20c-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (anteriormente NU1607) [NU1108](#nu1108) (anteriormente NU1606)</span><span class="sxs-lookup"><span data-stu-id="5d20c-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="5d20c-116">Erros de compatibilidade</span><span class="sxs-lookup"><span data-stu-id="5d20c-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="5d20c-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="5d20c-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="5d20c-118">**Avisos**</span><span class="sxs-lookup"><span data-stu-id="5d20c-118">**Warnings**</span></span>

| <span data-ttu-id="5d20c-119">Grupo</span><span class="sxs-lookup"><span data-stu-id="5d20c-119">Group</span></span> | <span data-ttu-id="5d20c-120">Números de aviso</span><span class="sxs-lookup"><span data-stu-id="5d20c-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="5d20c-121">Avisos de entrada inválidos</span><span class="sxs-lookup"><span data-stu-id="5d20c-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="5d20c-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="5d20c-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="5d20c-123">Avisos de versão de pacote inesperado</span><span class="sxs-lookup"><span data-stu-id="5d20c-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="5d20c-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="5d20c-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="5d20c-125">Avisos de conflito de resolução</span><span class="sxs-lookup"><span data-stu-id="5d20c-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="5d20c-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="5d20c-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="5d20c-127">Avisos de fallback do pacote</span><span class="sxs-lookup"><span data-stu-id="5d20c-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="5d20c-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="5d20c-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="5d20c-129">Avisos de feeds</span><span class="sxs-lookup"><span data-stu-id="5d20c-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="5d20c-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="5d20c-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="5d20c-131">Avisos e erros internos do NuGet</span><span class="sxs-lookup"><span data-stu-id="5d20c-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="5d20c-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="5d20c-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="5d20c-133">Erros de entrada inválidos</span><span class="sxs-lookup"><span data-stu-id="5d20c-133">Invalid input errors</span></span>

<span data-ttu-id="5d20c-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="5d20c-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="5d20c-135">NU1001</span><span class="sxs-lookup"><span data-stu-id="5d20c-135">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-136">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-136">**Issue**</span></span> | <span data-ttu-id="5d20c-137">O projeto não contém um ou mais frameworks.</span><span class="sxs-lookup"><span data-stu-id="5d20c-137">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="5d20c-138">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-138">**Common causes**</span></span> | <span data-ttu-id="5d20c-139">O projeto não contém um `TargetFramework` ou `TargetFrameworks` propriedade.</span><span class="sxs-lookup"><span data-stu-id="5d20c-139">The project doesn't contain a `TargetFramework` or `TargetFrameworks` property.</span></span> |
| <span data-ttu-id="5d20c-140">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-140">**Example message**</span></span> | <span data-ttu-id="5d20c-141">*O projeto projA não especifica nenhuma estrutura de destino em c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="5d20c-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |

### <a name="nu1002"></a><span data-ttu-id="5d20c-142">NU1002</span><span class="sxs-lookup"><span data-stu-id="5d20c-142">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-143">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-143">**Issue**</span></span> | <span data-ttu-id="5d20c-144">Combinação inválida de entradas, junto com uma palavra-chave criptografada.</span><span class="sxs-lookup"><span data-stu-id="5d20c-144">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="5d20c-145">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-145">**Common causes**</span></span> | <span data-ttu-id="5d20c-146">CLEAR não pode ser combinado com outras entradas.</span><span class="sxs-lookup"><span data-stu-id="5d20c-146">CLEAR may not be combined with other inputs.</span></span> |
| <span data-ttu-id="5d20c-147">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-147">**Example message**</span></span> | <span data-ttu-id="5d20c-148">*'CLEAR' não pode ser usado em conjunto com outros valores*</span><span class="sxs-lookup"><span data-stu-id="5d20c-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |

### <a name="nu1003"></a><span data-ttu-id="5d20c-149">NU1003</span><span class="sxs-lookup"><span data-stu-id="5d20c-149">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-150">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-150">**Issue**</span></span> | <span data-ttu-id="5d20c-151">`PackageTargetFallback`e `AssetTargetFallback` fornecem um comportamento diferente para a seleção de recursos e não podem ser usados juntos.</span><span class="sxs-lookup"><span data-stu-id="5d20c-151">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="5d20c-152">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-152">**Common causes**</span></span> | <span data-ttu-id="5d20c-153">Ambos `PackageTargetFallback` e `AssetTargetFallback` existe no projeto.</span><span class="sxs-lookup"><span data-stu-id="5d20c-153">Both `PackageTargetFallback` and `AssetTargetFallback` exist in the project.</span></span> |
| <span data-ttu-id="5d20c-154">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-154">**Example message**</span></span> | <span data-ttu-id="5d20c-155">*PackageTargetFallback e AssetTargetFallback não podem ser usados juntos. Remova as referências de PackageTargetFallback(deprecated) do ambiente do projeto.*</span><span class="sxs-lookup"><span data-stu-id="5d20c-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="5d20c-156">Erros de pacote e projeto ausentes</span><span class="sxs-lookup"><span data-stu-id="5d20c-156">Missing package and project errors</span></span>

<span data-ttu-id="5d20c-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="5d20c-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="5d20c-158">NU1100</span><span class="sxs-lookup"><span data-stu-id="5d20c-158">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-159">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-159">**Issue**</span></span> | <span data-ttu-id="5d20c-160">Um grupo de dependência não ser resolvido.</span><span class="sxs-lookup"><span data-stu-id="5d20c-160">A dependency group not be resolved.</span></span> <span data-ttu-id="5d20c-161">Esse é um problema genérico para tipos que não são pacotes ou projetos.</span><span class="sxs-lookup"><span data-stu-id="5d20c-161">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="5d20c-162">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-162">**Common causes**</span></span> | <span data-ttu-id="5d20c-163">O projeto contém uma dependência em um item que não existe.</span><span class="sxs-lookup"><span data-stu-id="5d20c-163">The project contains a dependency on an item that doesn't exist.</span></span> |
| <span data-ttu-id="5d20c-164">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-164">**Example message**</span></span> | <span data-ttu-id="5d20c-165">*Não é possível resolver System.Missing para net45*</span><span class="sxs-lookup"><span data-stu-id="5d20c-165">*Unable to resolve System.Missing for net45*</span></span> |

### <a name="nu1101"></a><span data-ttu-id="5d20c-166">NU1101</span><span class="sxs-lookup"><span data-stu-id="5d20c-166">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-167">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-167">**Issue**</span></span> | <span data-ttu-id="5d20c-168">O pacote não foi encontrado em qualquer fonte.</span><span class="sxs-lookup"><span data-stu-id="5d20c-168">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="5d20c-169">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-169">**Common causes**</span></span> | <span data-ttu-id="5d20c-170">A origem do pacote correto está ausente ou o identificador de pacote está incorreto.</span><span class="sxs-lookup"><span data-stu-id="5d20c-170">The correct package source is missing or the package identifier is incorrect.</span></span> |
| <span data-ttu-id="5d20c-171">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-171">**Example message**</span></span> | <span data-ttu-id="5d20c-172">*Não é possível encontrar o pacote System.Missing. Nenhum pacote existe com essa id na fonte (s): dotnet-core, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="5d20c-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |

### <a name="nu1102"></a><span data-ttu-id="5d20c-173">NU1102</span><span class="sxs-lookup"><span data-stu-id="5d20c-173">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-174">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-174">**Issue**</span></span> | <span data-ttu-id="5d20c-175">O identificador de pacote for encontrado, mas não é possível encontrar uma versão dentro do intervalo de dependência especificada em qualquer uma das fontes.</span><span class="sxs-lookup"><span data-stu-id="5d20c-175">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> |
| <span data-ttu-id="5d20c-176">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-176">**Common causes**</span></span> | <span data-ttu-id="5d20c-177">A origem do pacote correto está ausente ou o intervalo de dependência está incorreto.</span><span class="sxs-lookup"><span data-stu-id="5d20c-177">The correct package source is missing or the dependency range is incorrect.</span></span> <span data-ttu-id="5d20c-178">O intervalo pode ser especificado por um pacote e não ao usuário.</span><span class="sxs-lookup"><span data-stu-id="5d20c-178">The range might be specified by a package and not the user.</span></span> <span data-ttu-id="5d20c-179">O usuário talvez precise alternar para uma versão disponível se esse pacote é referenciado pelo projeto diretamente.</span><span class="sxs-lookup"><span data-stu-id="5d20c-179">The user may need to switch to an available version if this package is referenced by the project directly.</span></span> |
| <span data-ttu-id="5d20c-180">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-180">**Example message**</span></span> | <span data-ttu-id="5d20c-181">*Não é possível localizar o pacote NuGet.Versioning com a versão (> = 9.0.1)<br/> -versão (ões) de 30 encontrado em nuget.org [mais próximo de versão: 4.0.0]<br/> -versão (ões) de 10 encontrado em dotnet buildtools [mais próximo de versão: 4.0.0-rc-2129]<br/> -9 encontrado versão (ões) em NuGetVolatile [mais próximo de versão: 3.0.0-beta-00032]<br/> -encontrado versões 0 no núcleo do dotnet<br/> -encontrado versões 0 no roslyn dotnet*</span><span class="sxs-lookup"><span data-stu-id="5d20c-181">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1103"></a><span data-ttu-id="5d20c-182">NU1103</span><span class="sxs-lookup"><span data-stu-id="5d20c-182">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-183">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-183">**Issue**</span></span> | <span data-ttu-id="5d20c-184">Nenhuma versão estável foram encontrado no intervalo de dependência.</span><span class="sxs-lookup"><span data-stu-id="5d20c-184">No stable versions were found in the dependency range.</span></span> <span data-ttu-id="5d20c-185">As versões de pré-lançamento foram encontradas, mas não são permitidas.</span><span class="sxs-lookup"><span data-stu-id="5d20c-185">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="5d20c-186">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-186">**Common causes**</span></span> | <span data-ttu-id="5d20c-187">O projeto especificado para o intervalo de dependência a uma versão estável.</span><span class="sxs-lookup"><span data-stu-id="5d20c-187">The project specified a stable version for the dependency range.</span></span> <span data-ttu-id="5d20c-188">Os usuários precisam alterar o intervalo de versão para incluir as versões de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="5d20c-188">Users need to change the version range to include pre-release versions.</span></span> |
| <span data-ttu-id="5d20c-189">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-189">**Example message**</span></span> | <span data-ttu-id="5d20c-190">*Não é possível localizar um pacote estável NuGet.Versioning com a versão (> = 3.0.0)<br/> -versão (ões) de 10 encontrado em dotnet buildtools [mais próximo de versão: 4.0.0-rc-2129]<br/> -versão (ões) de 9 encontrado em NuGetVolatile [mais próximo de versão: 3.0.0-beta-00032] <br/> -Encontrado versões 0 no núcleo do dotnet<br/> -encontrado versões 0 no roslyn dotnet*</span><span class="sxs-lookup"><span data-stu-id="5d20c-190">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1104"></a><span data-ttu-id="5d20c-191">NU1104</span><span class="sxs-lookup"><span data-stu-id="5d20c-191">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-192">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-192">**Issue**</span></span> | <span data-ttu-id="5d20c-193">Um ProjectReference aponta para um arquivo que não existe.</span><span class="sxs-lookup"><span data-stu-id="5d20c-193">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="5d20c-194">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-194">**Common causes**</span></span> | <span data-ttu-id="5d20c-195">O arquivo de projeto está ausente do disco ou a referência está incorreta.</span><span class="sxs-lookup"><span data-stu-id="5d20c-195">The project file is missing from disk or the reference is incorrect.</span></span> |
| <span data-ttu-id="5d20c-196">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-196">**Example message**</span></span> | <span data-ttu-id="5d20c-197">*Referência de projeto não existe 'c:\a.csproj'. Verifique se a referência de projeto é válida e se existe o arquivo de projeto.*</span><span class="sxs-lookup"><span data-stu-id="5d20c-197">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |

### <a name="nu1105"></a><span data-ttu-id="5d20c-198">NU1105</span><span class="sxs-lookup"><span data-stu-id="5d20c-198">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-199">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-199">**Issue**</span></span> | <span data-ttu-id="5d20c-200">O arquivo de projeto existe, mas nenhuma informação de restauração foi fornecida para ele.</span><span class="sxs-lookup"><span data-stu-id="5d20c-200">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="5d20c-201">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-201">**Common causes**</span></span> | <span data-ttu-id="5d20c-202">No Visual Studio, isso pode significar que o projeto está descarregado.</span><span class="sxs-lookup"><span data-stu-id="5d20c-202">In Visual Studio this could mean that the project is unloaded.</span></span> <span data-ttu-id="5d20c-203">Na linha de comando, isso pode significar que o arquivo está corrompido ou que não contenha personalizado após o destino de importações necessário para restauração ler o projeto.</span><span class="sxs-lookup"><span data-stu-id="5d20c-203">From the command line this could mean that the file is corrupt or that it doesn't contain the custom after imports target needed for restore to read the project.</span></span> |
| <span data-ttu-id="5d20c-204">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-204">**Example message**</span></span> | <span data-ttu-id="5d20c-205">*Não é possível ler as informações de projeto para 'c:\a.csproj'. O arquivo de projeto pode ser inválidos ou ausentes destinos necessários para a restauração.*</span><span class="sxs-lookup"><span data-stu-id="5d20c-205">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

### <a name="nu1106"></a><span data-ttu-id="5d20c-206">NU1106</span><span class="sxs-lookup"><span data-stu-id="5d20c-206">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-207">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-207">**Issue**</span></span> | <span data-ttu-id="5d20c-208">Restrições de dependência não podem ser resolvidas.</span><span class="sxs-lookup"><span data-stu-id="5d20c-208">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="5d20c-209">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-209">**Common causes**</span></span> | <span data-ttu-id="5d20c-210">Os pacotes contêm dependência em versões exatas de um pacote em vez de intervalos abertos.</span><span class="sxs-lookup"><span data-stu-id="5d20c-210">Packages contain dependency on exact versions of a package instead of open-ended ranges.</span></span> |
| <span data-ttu-id="5d20c-211">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-211">**Example message**</span></span> | <span data-ttu-id="5d20c-212">*Não foi possível satisfazer solicitações conflitantes para {id}: {caminho conflito} Framework: {gráfico de destino}*</span><span class="sxs-lookup"><span data-stu-id="5d20c-212">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |

<a name="nu1107"></a> 

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="5d20c-213">NU1107 (anteriormente NU1607)</span><span class="sxs-lookup"><span data-stu-id="5d20c-213">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-214">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-214">**Issue**</span></span> | <span data-ttu-id="5d20c-215">Não é possível resolver as restrições de dependência entre pacotes.</span><span class="sxs-lookup"><span data-stu-id="5d20c-215">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="5d20c-216">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-216">**Common causes**</span></span> | <span data-ttu-id="5d20c-217">Pacotes com restrições de dependência em versões exatas não permitir que outros pacotes para aumentar a versão, se necessário.</span><span class="sxs-lookup"><span data-stu-id="5d20c-217">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> |
| <span data-ttu-id="5d20c-218">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-218">**Example message**</span></span> | <span data-ttu-id="5d20c-219">*Conflito de versão detectado para NuGet.Versioning. Referenciar o pacote diretamente do projeto para resolver esse problema.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="5d20c-219">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="5d20c-220">NU1108 (anteriormente NU1606)</span><span class="sxs-lookup"><span data-stu-id="5d20c-220">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-221">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-221">**Issue**</span></span> | <span data-ttu-id="5d20c-222">Foi detectada uma dependência circular.</span><span class="sxs-lookup"><span data-stu-id="5d20c-222">A circular dependency was detected.</span></span> |
| <span data-ttu-id="5d20c-223">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-223">**Common causes**</span></span> | <span data-ttu-id="5d20c-224">Um pacote foi criado incorretamente.</span><span class="sxs-lookup"><span data-stu-id="5d20c-224">A package is authored incorrectly.</span></span> |
| <span data-ttu-id="5d20c-225">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-225">**Example message**</span></span> | <span data-ttu-id="5d20c-226">*Ciclo detectado: A -> B -> um*</span><span class="sxs-lookup"><span data-stu-id="5d20c-226">*Cycle detected: A -> B -> A*</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="5d20c-227">Erros de compatibilidade</span><span class="sxs-lookup"><span data-stu-id="5d20c-227">Compatibility errors</span></span>

<span data-ttu-id="5d20c-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="5d20c-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="5d20c-229">NU1201</span><span class="sxs-lookup"><span data-stu-id="5d20c-229">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-230">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-230">**Issue**</span></span> | <span data-ttu-id="5d20c-231">Um projeto de dependência não contém uma estrutura compatível com o projeto atual.</span><span class="sxs-lookup"><span data-stu-id="5d20c-231">A dependency project doesn't contain a framework compatible with the current project.</span></span> |
| <span data-ttu-id="5d20c-232">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-232">**Common causes**</span></span> | <span data-ttu-id="5d20c-233">Estrutura de destino do projeto é uma versão superior do projeto de consumo.</span><span class="sxs-lookup"><span data-stu-id="5d20c-233">The project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="5d20c-234">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-234">**Example message**</span></span> | <span data-ttu-id="5d20c-235">*ServerWeb do projeto não é compatível com netstandard1.3 (. Identificadores de NETStandard, versão = v 1.3). Projeto suporta ServerWeb:<br/> -netstandard1.6 (. Identificadores de NETStandard, versão = v 1.6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = v 1.0)*</span><span class="sxs-lookup"><span data-stu-id="5d20c-235">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |

### <a name="nu1202"></a><span data-ttu-id="5d20c-236">NU1202</span><span class="sxs-lookup"><span data-stu-id="5d20c-236">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-237">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-237">**Issue**</span></span> | <span data-ttu-id="5d20c-238">Um pacote de dependência não contém qualquer ativos compatíveis com o projeto.</span><span class="sxs-lookup"><span data-stu-id="5d20c-238">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="5d20c-239">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-239">**Common causes**</span></span> | <span data-ttu-id="5d20c-240">O pacote não dá suporte a estrutura de destino do projeto.</span><span class="sxs-lookup"><span data-stu-id="5d20c-240">The package doesn't support the project's target framework.</span></span> |
| <span data-ttu-id="5d20c-241">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-241">**Example message**</span></span> | <span data-ttu-id="5d20c-242">*Pacote System.ComponentModel.EventBasedAsync 4.0.11 não é compatível com netstandard1.3 (. Identificadores de NETStandard, versão = v 1.3). Pacote suporta System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, versão = v 1.0)<br/> -monotouch10 (MonoTouch, versão = v 1.0)<br/> -net45 (. NETFramework, Version = v 4.5)<br/> -netcore50 (. NETCore, Version = v 5.0)<br/> -netstandard1.0 (. Identificadores de NETStandard, versão = v 1.0)<br/> -portátil net45 + win8 + wp8 + wpa81 (. NETPortable, Version = v0.0, perfil = Profile259)<br/> -win8 (Windows, versão = v 8.0)<br/> -wp8 (WindowsPhone, versão = v 8.0)<br/> -wpa81 (WindowsPhoneApp, versão = 8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="5d20c-242">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|

### <a name="nu1203"></a><span data-ttu-id="5d20c-243">NU1203</span><span class="sxs-lookup"><span data-stu-id="5d20c-243">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-244">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-244">**Issue**</span></span> | <span data-ttu-id="5d20c-245">O pacote não oferece suporte para o projeto `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="5d20c-245">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="5d20c-246">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-246">**Common causes**</span></span> | <span data-ttu-id="5d20c-247">O pacote não dá suporte a atual `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="5d20c-247">The package doesn't support the current `RuntimeIdentifier`.</span></span> <span data-ttu-id="5d20c-248">Alterar o `RuntimeIdentifier` valores usados no projeto, se necessário.</span><span class="sxs-lookup"><span data-stu-id="5d20c-248">Change the `RuntimeIdentifier` values used in the project if needed.</span></span> |
| <span data-ttu-id="5d20c-249">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-249">**Example message**</span></span> | <span data-ttu-id="5d20c-250">*System.Example 1.0.0 fornece uma referência de tempo de compilação do assembly para o. dll em net461, mas não há nenhum tempo de execução do assembly compatível.*</span><span class="sxs-lookup"><span data-stu-id="5d20c-250">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |

### <a name="nu1401"></a><span data-ttu-id="5d20c-251">NU1401</span><span class="sxs-lookup"><span data-stu-id="5d20c-251">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-252">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-252">**Issue**</span></span> | <span data-ttu-id="5d20c-253">O pacote requer recursos ou estruturas atualmente não há suportadas à versão instalada do NuGet.</span><span class="sxs-lookup"><span data-stu-id="5d20c-253">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="5d20c-254">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-254">**Common causes**</span></span> | <span data-ttu-id="5d20c-255">Atualize o NuGet para corrigir o problema.</span><span class="sxs-lookup"><span data-stu-id="5d20c-255">Upgrade NuGet to fix the issue.</span></span> |
| <span data-ttu-id="5d20c-256">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-256">**Example message**</span></span> | <span data-ttu-id="5d20c-257">*O pacote 'NuGet.Versioning' requer o NuGet versão de cliente '5.0.0' ou superior, mas a versão atual do NuGet é '4.3.0'. Para atualizar o NuGet, acesse http://docs.nuget.org/consume/installing-nuget.*</span><span class="sxs-lookup"><span data-stu-id="5d20c-257">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'. To upgrade NuGet, please go to http://docs.nuget.org/consume/installing-nuget.*</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="5d20c-258">Avisos de entrada inválidos</span><span class="sxs-lookup"><span data-stu-id="5d20c-258">Invalid input warnings</span></span>

<span data-ttu-id="5d20c-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="5d20c-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="5d20c-260">NU1501</span><span class="sxs-lookup"><span data-stu-id="5d20c-260">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-261">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-261">**Issue**</span></span> | <span data-ttu-id="5d20c-262">A restauração do projeto está tentando operar em não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="5d20c-262">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="5d20c-263">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-263">**Common causes**</span></span> | <span data-ttu-id="5d20c-264">O projeto está ausente.</span><span class="sxs-lookup"><span data-stu-id="5d20c-264">The project is missing.</span></span> |
| <span data-ttu-id="5d20c-265">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-265">**Example message**</span></span> | <span data-ttu-id="5d20c-266">*A pasta 'c:\projects\a' não contém um projeto para restaurar.*</span><span class="sxs-lookup"><span data-stu-id="5d20c-266">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |

### <a name="nu1502"></a><span data-ttu-id="5d20c-267">NU1502</span><span class="sxs-lookup"><span data-stu-id="5d20c-267">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-268">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-268">**Issue**</span></span> | <span data-ttu-id="5d20c-269">`RuntimeSupports`contém um perfil inválido.</span><span class="sxs-lookup"><span data-stu-id="5d20c-269">`RuntimeSupports` contains an invalid profile.</span></span> |
| <span data-ttu-id="5d20c-270">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-270">**Common causes**</span></span> | <span data-ttu-id="5d20c-271">O dá suporte a perfil não foi encontrado em um `runtime.json` arquivo dos pacotes de dependência atual.</span><span class="sxs-lookup"><span data-stu-id="5d20c-271">The supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span> |
| <span data-ttu-id="5d20c-272">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-272">**Example message**</span></span> | <span data-ttu-id="5d20c-273">*Perfil de compatibilidade desconhecido: aaa*</span><span class="sxs-lookup"><span data-stu-id="5d20c-273">*Unknown Compatibility Profile: aaa*</span></span> |

### <a name="nu1503"></a><span data-ttu-id="5d20c-274">NU1503</span><span class="sxs-lookup"><span data-stu-id="5d20c-274">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-275">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-275">**Issue**</span></span> | <span data-ttu-id="5d20c-276">Um projeto de dependência não importa destinos de restauração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="5d20c-276">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="5d20c-277">Isso é semelhante a NU1105, mas aqui o projeto será ignorado e ignorado em vez fazendo com que todos os de restauração falhe.</span><span class="sxs-lookup"><span data-stu-id="5d20c-277">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="5d20c-278">Em soluções complexas geralmente há outros tipos de projetos que podem não oferecer suporte a restauração.</span><span class="sxs-lookup"><span data-stu-id="5d20c-278">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="5d20c-279">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-279">**Common causes**</span></span> | <span data-ttu-id="5d20c-280">Isso pode acontecer para projetos que não importar props/destinos comuns que importar automaticamente a restauração.</span><span class="sxs-lookup"><span data-stu-id="5d20c-280">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="5d20c-281">Se o projeto não precisa ser restaurados isso pode ser ignorado.</span><span class="sxs-lookup"><span data-stu-id="5d20c-281">If the project doesn't need to be restored this can be ignored.</span></span> |
| <span data-ttu-id="5d20c-282">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-282">**Example message**</span></span> | <span data-ttu-id="5d20c-283">*Ignorando a restauração para o projeto 'c:\a.csproj'. O arquivo de projeto pode ser inválidos ou ausentes destinos necessários para a restauração.*</span><span class="sxs-lookup"><span data-stu-id="5d20c-283">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="5d20c-284">Avisos de versão de pacote inesperado</span><span class="sxs-lookup"><span data-stu-id="5d20c-284">Unexpected package version warnings</span></span>

<span data-ttu-id="5d20c-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="5d20c-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="5d20c-286">NU1601</span><span class="sxs-lookup"><span data-stu-id="5d20c-286">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-287">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-287">**Issue**</span></span> | <span data-ttu-id="5d20c-288">Uma dependência de projeto foi aumentada para uma versão maior do que o projeto especificado.</span><span class="sxs-lookup"><span data-stu-id="5d20c-288">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="5d20c-289">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-289">**Common causes**</span></span> | <span data-ttu-id="5d20c-290">Outro pacote de dependência necessária uma versão mais recente e aumentado o pacote em.</span><span class="sxs-lookup"><span data-stu-id="5d20c-290">Another dependency package required a higher version and bumped the package up.</span></span> |
| <span data-ttu-id="5d20c-291">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-291">**Example message**</span></span> | <span data-ttu-id="5d20c-292">*Dependência especificada foi NuGet.Versioning (> = 3.5.0) mas acabou com NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="5d20c-292">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |

### <a name="nu1602"></a><span data-ttu-id="5d20c-293">NU1602</span><span class="sxs-lookup"><span data-stu-id="5d20c-293">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-294">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-294">**Issue**</span></span> | <span data-ttu-id="5d20c-295">Uma dependência de pacote não tem um limite inferior.</span><span class="sxs-lookup"><span data-stu-id="5d20c-295">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="5d20c-296">Isso não permite que a restauração localizar o *melhor correspondência*.</span><span class="sxs-lookup"><span data-stu-id="5d20c-296">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="5d20c-297">Cada restauração flutua para baixo ao tentar encontrar uma versão inferior que pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="5d20c-297">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="5d20c-298">Isso significa que a restauração fica online para verificar se todas as fontes de cada vez em vez de usar os pacotes que já existem na pasta de pacote do usuário.</span><span class="sxs-lookup"><span data-stu-id="5d20c-298">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="5d20c-299">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-299">**Common causes**</span></span> | <span data-ttu-id="5d20c-300">Isso geralmente é um erro de criação de pacote.</span><span class="sxs-lookup"><span data-stu-id="5d20c-300">This is usually a package authoring error.</span></span> |
| <span data-ttu-id="5d20c-301">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-301">**Example message**</span></span> | <span data-ttu-id="5d20c-302">*NuGet. Packaging 4.0.0 não fornece um limite inferior inclusivo de dependência NuGet.Versioning (3.5.0 >). Uma melhor correspondência aproximada de 3.6.0 foi resolvida.*</span><span class="sxs-lookup"><span data-stu-id="5d20c-302">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |

### <a name="nu1603"></a><span data-ttu-id="5d20c-303">NU1603</span><span class="sxs-lookup"><span data-stu-id="5d20c-303">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-304">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-304">**Issue**</span></span> | <span data-ttu-id="5d20c-305">Uma dependência de pacote especificado de uma versão que não pôde ser encontrada.</span><span class="sxs-lookup"><span data-stu-id="5d20c-305">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="5d20c-306">Uma versão mais recente foi usada em vez disso, o que é diferente do que o pacote foi criado.</span><span class="sxs-lookup"><span data-stu-id="5d20c-306">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="5d20c-307">Isso significa que a restauração não localizou o *melhor correspondência*.</span><span class="sxs-lookup"><span data-stu-id="5d20c-307">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="5d20c-308">Cada restauração flutua para baixo ao tentar encontrar uma versão inferior que pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="5d20c-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="5d20c-309">Isso significa que a restauração fica online para verificar se todas as fontes de cada vez em vez de usar os pacotes que já existem na pasta de pacote do usuário.</span><span class="sxs-lookup"><span data-stu-id="5d20c-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="5d20c-310">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-310">**Common causes**</span></span> | <span data-ttu-id="5d20c-311">As fontes de pacote contém a versão inferior esperado.</span><span class="sxs-lookup"><span data-stu-id="5d20c-311">The package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="5d20c-312">Se o pacote esperado não foi liberado, em seguida, isso pode ser um erro de criação de pacote.</span><span class="sxs-lookup"><span data-stu-id="5d20c-312">If the package expected has not been released then this may be a package authoring error.</span></span> |
| <span data-ttu-id="5d20c-313">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-313">**Example message**</span></span> | <span data-ttu-id="5d20c-314">NuGet. Packaging 4.0.0 depende NuGet.Versioning (> = 4.0.0) mas 4.0.0 não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="5d20c-314">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="5d20c-315">Uma melhor correspondência aproximada de 5.0.0 foi resolvida.</span><span class="sxs-lookup"><span data-stu-id="5d20c-315">An approximate best match of 5.0.0 was resolved.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="5d20c-316">NU1604</span><span class="sxs-lookup"><span data-stu-id="5d20c-316">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-317">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-317">**Issue**</span></span> | <span data-ttu-id="5d20c-318">Uma dependência de projeto não define um limite inferior.</span><span class="sxs-lookup"><span data-stu-id="5d20c-318">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="5d20c-319">Isso significa que a restauração não localizou o *melhor correspondência*.</span><span class="sxs-lookup"><span data-stu-id="5d20c-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="5d20c-320">Cada restauração flutua para baixo ao tentar encontrar uma versão inferior que pode ser usada.</span><span class="sxs-lookup"><span data-stu-id="5d20c-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="5d20c-321">Isso significa que a restauração fica online para verificar se todas as fontes de cada vez em vez de usar os pacotes que já existem na pasta de pacote do usuário.</span><span class="sxs-lookup"><span data-stu-id="5d20c-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="5d20c-322">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-322">**Common causes**</span></span> | <span data-ttu-id="5d20c-323">O projeto *PackageReference* *versão* atributo deve ser atualizado para incluir um limite inferior.</span><span class="sxs-lookup"><span data-stu-id="5d20c-323">The project's *PackageReference* *Version* attribute should be updated to include a lower bound.</span></span> |
| <span data-ttu-id="5d20c-324">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-324">**Example message**</span></span> | <span data-ttu-id="5d20c-325">*Projeto dependência NuGet.Versioning (< = 9.0.0) doe não contêm um limite inferior inclusivo. Inclua um limite inferior na versão de dependência para garantir resultados consistentes de restauração.*</span><span class="sxs-lookup"><span data-stu-id="5d20c-325">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |

### <a name="nu1605"></a><span data-ttu-id="5d20c-326">NU1605</span><span class="sxs-lookup"><span data-stu-id="5d20c-326">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-327">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-327">**Issue**</span></span> | <span data-ttu-id="5d20c-328">Um pacote de dependência especificou uma restrição de versão em uma versão superior de um pacote de restauração finalmente resolvida.</span><span class="sxs-lookup"><span data-stu-id="5d20c-328">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> |
| <span data-ttu-id="5d20c-329">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-329">**Common causes**</span></span> | <span data-ttu-id="5d20c-330">Wins mais próximos ao resolver pacotes.</span><span class="sxs-lookup"><span data-stu-id="5d20c-330">Nearest wins when resolving packages.</span></span> <span data-ttu-id="5d20c-331">Um pacote distante pode ter substituído a um pacote mais próximo no gráfico.</span><span class="sxs-lookup"><span data-stu-id="5d20c-331">A nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="5d20c-332">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-332">**Example message**</span></span> | <span data-ttu-id="5d20c-333">*Detectado o downgrade do pacote: NuGet.Versioning de 4.0.0 para 3.5.0. Referenciar o pacote diretamente do projeto para selecionar uma versão diferente.<br/>  NuGet. Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="5d20c-333">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="5d20c-334">Avisos de conflito de resolução</span><span class="sxs-lookup"><span data-stu-id="5d20c-334">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="5d20c-335">NU1608</span><span class="sxs-lookup"><span data-stu-id="5d20c-335">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-336">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-336">**Issue**</span></span> | <span data-ttu-id="5d20c-337">Um pacote de solução é maior do que permite que uma restrição de dependência.</span><span class="sxs-lookup"><span data-stu-id="5d20c-337">A resolve package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="5d20c-338">Em alguns casos, isso é intencional e o aviso pode ser suprimido.</span><span class="sxs-lookup"><span data-stu-id="5d20c-338">In some cases this is intentional and the warning can be suppressed.</span></span> |
| <span data-ttu-id="5d20c-339">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-339">**Common causes**</span></span> | <span data-ttu-id="5d20c-340">Um pacote referenciado diretamente por um projeto substituirão as restrições de dependência de outros pacotes.</span><span class="sxs-lookup"><span data-stu-id="5d20c-340">A package referenced directly by a project will override dependency constraints from other packages.</span></span>   |
| <span data-ttu-id="5d20c-341">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-341">**Example message**</span></span> | <span data-ttu-id="5d20c-342">*Versão do pacote detectado fora da restrição de dependência: x 1.0.0 requer y (= 1.0.0), mas a versão y 2.0.0 foi resolvido.*</span><span class="sxs-lookup"><span data-stu-id="5d20c-342">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="5d20c-343">Avisos de fallback do pacote</span><span class="sxs-lookup"><span data-stu-id="5d20c-343">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="5d20c-344">NU1701</span><span class="sxs-lookup"><span data-stu-id="5d20c-344">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-345">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-345">**Issue**</span></span> | <span data-ttu-id="5d20c-346">*PackageTargetFallback/AssetTargetFallback* foi usado para selecionar os ativos de um pacote.</span><span class="sxs-lookup"><span data-stu-id="5d20c-346">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span></span> <span data-ttu-id="5d20c-347">Este é um aviso para informar o usuário que os ativos podem não ser 100% compatível.</span><span class="sxs-lookup"><span data-stu-id="5d20c-347">This is a warning to let the user know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="5d20c-348">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-348">**Common causes**</span></span> | <span data-ttu-id="5d20c-349">O pacote não dá suporte a estrutura do projeto.</span><span class="sxs-lookup"><span data-stu-id="5d20c-349">The package doesn't support the project framework.</span></span> |
| <span data-ttu-id="5d20c-350">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-350">**Example message**</span></span> | <span data-ttu-id="5d20c-351">*Pacote 'NuGet.Versioning' foi restaurado usando 'portátil net45 + win8' em vez disso, a estrutura de destino do projeto 'netstandard1.5'. Esse pacote pode não ser totalmente compatível com o seu projeto.*</span><span class="sxs-lookup"><span data-stu-id="5d20c-351">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="5d20c-352">Avisos de feeds</span><span class="sxs-lookup"><span data-stu-id="5d20c-352">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="5d20c-353">NU1801</span><span class="sxs-lookup"><span data-stu-id="5d20c-353">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-354">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-354">**Issue**</span></span> | <span data-ttu-id="5d20c-355">Ocorreu um erro ao ler o feed quando `IgnoreFailedSources` está definido como true, convertendo-o para um aviso não fatal.</span><span class="sxs-lookup"><span data-stu-id="5d20c-355">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="5d20c-356">Isso pode conter qualquer mensagem e é genérico.</span><span class="sxs-lookup"><span data-stu-id="5d20c-356">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="5d20c-357">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-357">**Common causes**</span></span> | <span data-ttu-id="5d20c-358">A fonte é inválida.</span><span class="sxs-lookup"><span data-stu-id="5d20c-358">The source is invalid.</span></span> |
| <span data-ttu-id="5d20c-359">**Exemplo de mensagem**</span><span class="sxs-lookup"><span data-stu-id="5d20c-359">**Example message**</span></span> | <span data-ttu-id="5d20c-360">N/D</span><span class="sxs-lookup"><span data-stu-id="5d20c-360">n/a</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="5d20c-361">Avisos e erros internos do NuGet</span><span class="sxs-lookup"><span data-stu-id="5d20c-361">NuGet internal errors and warnings</span></span>

<span data-ttu-id="5d20c-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="5d20c-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="5d20c-363">NU1000</span><span class="sxs-lookup"><span data-stu-id="5d20c-363">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-364">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-364">**Issue**</span></span> | <span data-ttu-id="5d20c-365">Um erro interno não específico do NuGet.</span><span class="sxs-lookup"><span data-stu-id="5d20c-365">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="5d20c-366">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-366">**Common causes**</span></span> | <span data-ttu-id="5d20c-367">Verifique os logs para obter mais informações</span><span class="sxs-lookup"><span data-stu-id="5d20c-367">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="5d20c-368">NU1500</span><span class="sxs-lookup"><span data-stu-id="5d20c-368">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="5d20c-369">**Issue**</span><span class="sxs-lookup"><span data-stu-id="5d20c-369">**Issue**</span></span> | <span data-ttu-id="5d20c-370">Um aviso interno não específico do NuGet.</span><span class="sxs-lookup"><span data-stu-id="5d20c-370">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="5d20c-371">**Causas comuns**</span><span class="sxs-lookup"><span data-stu-id="5d20c-371">**Common causes**</span></span> | <span data-ttu-id="5d20c-372">Verifique os logs para obter mais informações</span><span class="sxs-lookup"><span data-stu-id="5d20c-372">Check the logs for more information</span></span> |
