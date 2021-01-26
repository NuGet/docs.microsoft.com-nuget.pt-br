---
title: Notas de versão do NuGet 3.4.4
description: Notas de versão do NuGet 3.4.4 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780223"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="63c2f-103">Notas de versão do NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="63c2f-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="63c2f-104">Notas de versão do [NuGet 3.4.3](../release-notes/nuget-3.4.3.md)  |  [Notas de versão do NuGet 3,5-Beta](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="63c2f-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="63c2f-105">O foco principal dessa versão foi aprimoramentos para a qualidade da versão 3.4.3 do nuget.exe com algumas correções para a extensão do Visual Studio também.</span><span class="sxs-lookup"><span data-stu-id="63c2f-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="63c2f-106">Você pode baixar o VSIX e o nuget.exe [aqui](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="63c2f-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtm-2016-05-19"></a><span data-ttu-id="63c2f-107">[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="63c2f-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="63c2f-108">Changelog completo</span><span class="sxs-lookup"><span data-stu-id="63c2f-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="63c2f-109">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="63c2f-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="63c2f-110">Alterações</span><span class="sxs-lookup"><span data-stu-id="63c2f-110">Changes</span></span>

- <span data-ttu-id="63c2f-111">Aprimoramentos de pacote: aprimoramentos para empacotar símbolos, empacotamento com `project.json` e mais [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="63c2f-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="63c2f-112">Exibir exceção quando houver uma falha ao encontrar projetos no comando de atualização [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="63c2f-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="63c2f-113">Ler o tipo de pacote da entrada `.nuspec` e `project.json` ao empacotar [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="63c2f-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="63c2f-114">Tornar NuGet. Shared não é um projeto.</span><span class="sxs-lookup"><span data-stu-id="63c2f-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="63c2f-115">\#602</span><span class="sxs-lookup"><span data-stu-id="63c2f-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="63c2f-116">Use o tempo limite de push como o tempo limite de resposta HTTP [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="63c2f-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="63c2f-117">Os arquivos de pacote com tempos futuros não terão seus horários usados [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="63c2f-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="63c2f-118">Atualizando `NuGet.Core.dll` a versão para 2.12.0 para corrigir o problema de XML [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="63c2f-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="63c2f-119">Support./NuGet.CommandLine.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="63c2f-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="63c2f-120">Exibir erro ao restaurar sem `project.json` ou `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="63c2f-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="63c2f-121">Corrigindo as versões de dependência quando as versões necessárias forem diferentes [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="63c2f-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>