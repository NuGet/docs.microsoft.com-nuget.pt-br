---
title: Notas de versão do NuGet 2.8.2
description: Notas de versão do NuGet 2.8.2 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780374"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="3af40-103">Notas de versão do NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="3af40-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="3af40-104">Notas de versão do [NuGet 2.8.1](../release-notes/nuget-2.8.1.md)  |  [Notas de versão do NuGet 2.8.3](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="3af40-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="3af40-105">O NuGet 2.8.2 foi lançado em 22 de maio de 2014.</span><span class="sxs-lookup"><span data-stu-id="3af40-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="3af40-106">Essa versão inclui apenas alterações na linha de comando nuget.exe, no pacote NuGet. Server e em outros pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="3af40-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="3af40-107">A versão não incluiu uma extensão do Visual Studio atualizada ou a extensão do WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="3af40-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="3af40-108">Atualizações notáveis</span><span class="sxs-lookup"><span data-stu-id="3af40-108">Notable Updates</span></span>

<span data-ttu-id="3af40-109">As atualizações mais notáveis estavam na linha de comando nuget.exe e no pacote NuGet. Server (para feeds do NuGet auto-hospedados).</span><span class="sxs-lookup"><span data-stu-id="3af40-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="3af40-110">Importantes nuget.exe correções de bugs</span><span class="sxs-lookup"><span data-stu-id="3af40-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="3af40-111">nuget.exe Push falha e continua tentando novamente</span><span class="sxs-lookup"><span data-stu-id="3af40-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="3af40-112">nuget.exe Push não envia credenciais de autenticação básicas corretamente</span><span class="sxs-lookup"><span data-stu-id="3af40-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="3af40-113">nuget.exe Push não seguirá o redirecionamento temporário</span><span class="sxs-lookup"><span data-stu-id="3af40-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="3af40-114">Correção importante do bug do NuGet. Server</span><span class="sxs-lookup"><span data-stu-id="3af40-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="3af40-115">Valor errado de IsAbsoluteLatestVersion retornado pelo NuGet. Server</span><span class="sxs-lookup"><span data-stu-id="3af40-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="3af40-116">Pacotes atualizados</span><span class="sxs-lookup"><span data-stu-id="3af40-116">Packages Updated</span></span>

<span data-ttu-id="3af40-117">As correções de linha de comando nuget.exe e NuGet. Server são fornecidas como atualizações de pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="3af40-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="3af40-118">Havia outros pacotes atualizados com 2.8.2 também.</span><span class="sxs-lookup"><span data-stu-id="3af40-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="3af40-119">Aqui está a lista de pacotes atualizados:</span><span class="sxs-lookup"><span data-stu-id="3af40-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="3af40-120">NuGet. Core</span><span class="sxs-lookup"><span data-stu-id="3af40-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="3af40-121">NuGet. CommandLine</span><span class="sxs-lookup"><span data-stu-id="3af40-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="3af40-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="3af40-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="3af40-123">NuGet. Build</span><span class="sxs-lookup"><span data-stu-id="3af40-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="3af40-124">[NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (o pacote, não a extensão)</span><span class="sxs-lookup"><span data-stu-id="3af40-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="3af40-125">Todas as alterações</span><span class="sxs-lookup"><span data-stu-id="3af40-125">All Changes</span></span>
<span data-ttu-id="3af40-126">Foram abordados 10 problemas na versão.</span><span class="sxs-lookup"><span data-stu-id="3af40-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="3af40-127">Para obter uma lista completa dos itens de trabalho corrigidos no NuGet 2.8.2, consulte o [rastreador de problemas do NuGet para esta versão](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="3af40-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
