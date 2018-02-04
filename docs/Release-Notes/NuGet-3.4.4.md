---
title: "Notas de versão do NuGet 3.4.4 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão do NuGet 3.4.4 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs."
keywords: "Notas de versão NuGet 3.4.4, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fabc10ae5c8e0bd43581f85c7763eb23e9483aaf
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-344-release-notes"></a><span data-ttu-id="008d7-104">Notas de versão do NuGet 3.4.4</span><span class="sxs-lookup"><span data-stu-id="008d7-104">NuGet 3.4.4 Release Notes</span></span>

<span data-ttu-id="008d7-105">[Notas de versão do NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [notas de versão 3.5 Beta do NuGet](../release-notes/nuget-3.5-Beta.md)</span><span class="sxs-lookup"><span data-stu-id="008d7-105">[NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md) | [NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md)</span></span>

<span data-ttu-id="008d7-106">O foco principal desta versão foram as melhorias a qualidade das 3.4.3 versão de nuget.exe com algumas correções à extensão do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="008d7-106">The primary focus of this release was improvements to the quality of 3.4.3 version of nuget.exe with a few fixes to the Visual Studio extension as well.</span></span>

<span data-ttu-id="008d7-107">Você pode baixar o VSIX e nuget.exe [aqui](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="008d7-107">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a><span data-ttu-id="008d7-108">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span><span class="sxs-lookup"><span data-stu-id="008d7-108">[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)</span></span>

[<span data-ttu-id="008d7-109">Log de alteração completa</span><span class="sxs-lookup"><span data-stu-id="008d7-109">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[<span data-ttu-id="008d7-110">Lista de problemas</span><span class="sxs-lookup"><span data-stu-id="008d7-110">List of Issues</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a><span data-ttu-id="008d7-111">Alterações</span><span class="sxs-lookup"><span data-stu-id="008d7-111">Changes</span></span>

- <span data-ttu-id="008d7-112">Aprimoramentos do pacote: Melhorias Empacotando símbolos, de remessa com `project.json` e mais [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)</span><span class="sxs-lookup"><span data-stu-id="008d7-112">Pack Improvements: Improvements to packing symbols, packing with `project.json` and more [\#606](https://github.com/NuGet/NuGet.Client/pull/606)</span></span>
- <span data-ttu-id="008d7-113">Exibir a exceção quando não houver uma falha ao localizar a projetos no comando update [\#605] (https://github.com/NuGet/NuGet.Client/pull/605</span><span class="sxs-lookup"><span data-stu-id="008d7-113">Display exception when there is a failure finding projects in update command [\#605](https://github.com/NuGet/NuGet.Client/pull/605</span></span>
- <span data-ttu-id="008d7-114">Ler o tipo de pacote de entrada `.nuspec` e `project.json` quando remessa [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)</span><span class="sxs-lookup"><span data-stu-id="008d7-114">Read package type from input `.nuspec` and `project.json` when packing [\#603](https://github.com/NuGet/NuGet.Client/pull/603)</span></span>
- <span data-ttu-id="008d7-115">Verifique NuGet.Shared não em um projeto.</span><span class="sxs-lookup"><span data-stu-id="008d7-115">Make NuGet.Shared not a project.</span></span> [<span data-ttu-id="008d7-116">\#602</span><span class="sxs-lookup"><span data-stu-id="008d7-116">\#602</span></span>](https://github.com/NuGet/NuGet.Client/pull/602)
- <span data-ttu-id="008d7-117">Use o tempo limite de envio por push o tempo de limite de resposta HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)</span><span class="sxs-lookup"><span data-stu-id="008d7-117">Use the push timeout as the HTTP response timeout [\#599](https://github.com/NuGet/NuGet.Client/pull/599)</span></span>
- <span data-ttu-id="008d7-118">Arquivos de pacote com tempos de futuros não terão seus vezes usado [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)</span><span class="sxs-lookup"><span data-stu-id="008d7-118">Package files with future times will not have their times used [\#597](https://github.com/NuGet/NuGet.Client/pull/597)</span></span>
- <span data-ttu-id="008d7-119">Atualizando `NuGet.Core.dll` versão 2.12.0 para corrigir o problema XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)</span><span class="sxs-lookup"><span data-stu-id="008d7-119">Updating `NuGet.Core.dll` version to 2.12.0 to fix XML issue [\#594](https://github.com/NuGet/NuGet.Client/pull/594)</span></span>
- <span data-ttu-id="008d7-120">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span><span class="sxs-lookup"><span data-stu-id="008d7-120">Support ./NuGet.CommandLine.XPlat -v \<verbosity\> \<mode\> [\#593](https://github.com/NuGet/NuGet.Client/pull/593)</span></span>
- <span data-ttu-id="008d7-121">Erro ao exibir restaurar sem `project.json` ou `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)</span><span class="sxs-lookup"><span data-stu-id="008d7-121">Display error restoring without `project.json` or `packages.config` [\#590](https://github.com/NuGet/NuGet.Client/pull/590)</span></span>
- <span data-ttu-id="008d7-122">Correção de versões de dependência quando diferem versões necessárias [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)</span><span class="sxs-lookup"><span data-stu-id="008d7-122">Fixing dependency versions when required versions differ [\#559](https://github.com/NuGet/NuGet.Client/pull/559)</span></span>