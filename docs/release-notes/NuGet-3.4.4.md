---
title: Notas de versão do NuGet 3.4.4
description: Notas de versão do NuGet 3.4.4 incluindo conhecidos problemas, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547467"
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="5632c-103">Notas de versão do NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="5632c-103">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="5632c-104">[Notas de versão do NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [notas de versão 3.5 Beta do NuGet](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="5632c-104">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="5632c-105">O principal foco desta versão foram as melhorias para a qualidade do 3.4.3 versão do nuget.exe com algumas correções à extensão do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5632c-105">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="5632c-106">Você pode baixar o VSIX e nuget.exe [aqui](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="5632c-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="5632c-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="5632c-107">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="5632c-108">Log de alterações completo</span><span class="sxs-lookup"><span data-stu-id="5632c-108">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="5632c-109">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="5632c-109">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="5632c-110">Alterações</span><span class="sxs-lookup"><span data-stu-id="5632c-110">Changes</span></span>

- <span data-ttu-id="5632c-111">Aprimoramentos do pacote: Melhorias para empacotamento de símbolos, com o empacotamento `project.json` mais [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="5632c-111">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="5632c-112">Exibir a exceção quando não há uma falha ao localizar os projetos no comando de atualização [\#605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="5632c-112">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="5632c-113">Ler o tipo de pacote de entrada `.nuspec` e `project.json` quando o empacotamento [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="5632c-113">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="5632c-114">Verifique NuGet.Shared não em um projeto.</span><span class="sxs-lookup"><span data-stu-id="5632c-114">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="5632c-115">\#602</span><span class="sxs-lookup"><span data-stu-id="5632c-115">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="5632c-116">Use o tempo limite de envio por push o tempo de limite de resposta HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="5632c-116">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="5632c-117">Arquivos de pacote com tempos de futuros não terão suas horas de usado [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="5632c-117">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="5632c-118">Atualizando `NuGet.Core.dll` versão para 2.12.0 para corrigir o problema XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="5632c-118">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="5632c-119">Dar suporte a v -./NuGet.CommandLine.XPlat \<detalhamento\> \<modo\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="5632c-119">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="5632c-120">Erro de exibição restaurando sem `project.json` ou `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="5632c-120">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="5632c-121">Correção de versões de dependência quando as versões necessárias diferem [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="5632c-121">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>