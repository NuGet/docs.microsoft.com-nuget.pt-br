---
title: "Notas de versão do NuGet 2.8.2 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: bb547f5d-3c0e-4721-b2c7-3fc7e09c34de
description: "Notas de versão do NuGet 2.8.2 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs."
keywords: "Notas de versão NuGet 2.8.2, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 221b8970663ca80a986fc3ee542b99971c5e2018
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="9c7fd-104">Notas de versão do NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="9c7fd-104">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="9c7fd-105">[Notas de versão do NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 notas de versão](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="9c7fd-105">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="9c7fd-106">NuGet 2.8.2 foi lançado em 22 de maio de 2014.</span><span class="sxs-lookup"><span data-stu-id="9c7fd-106">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="9c7fd-107">Esta versão incluído somente as alterações para o nuget.exe de linha de comando, o pacote de NuGet.Server e outros pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="9c7fd-107">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="9c7fd-108">A versão não incluiu uma extensão atualizada do Visual Studio ou a extensão do WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="9c7fd-108">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="9c7fd-109">Atualizações importantes</span><span class="sxs-lookup"><span data-stu-id="9c7fd-109">Notable Updates</span></span>

<span data-ttu-id="9c7fd-110">As atualizações mais importantes foram no nuget.exe de linha de comando e o pacote de NuGet.Server (para feeds do NuGet auto-hospedado).</span><span class="sxs-lookup"><span data-stu-id="9c7fd-110">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="9c7fd-111">Correções de bugs importantes nuget.exe</span><span class="sxs-lookup"><span data-stu-id="9c7fd-111">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="9c7fd-112">NuGet.exe Push falha e mantém a tentar novamente</span><span class="sxs-lookup"><span data-stu-id="9c7fd-112">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="9c7fd-113">NuGet.exe por Push não envia credenciais de autenticação básica corretamente</span><span class="sxs-lookup"><span data-stu-id="9c7fd-113">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="9c7fd-114">Envio de NuGet.exe não siga redirecionamento temporário</span><span class="sxs-lookup"><span data-stu-id="9c7fd-114">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="9c7fd-115">Correção de Bug NuGet.Server importantes</span><span class="sxs-lookup"><span data-stu-id="9c7fd-115">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="9c7fd-116">Valor incorreto de IsAbsoluteLatestVersion retornado por NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="9c7fd-116">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="9c7fd-117">Pacotes atualizados</span><span class="sxs-lookup"><span data-stu-id="9c7fd-117">Packages Updated</span></span>

<span data-ttu-id="9c7fd-118">O nuget.exe de linha de comando e NuGet.Server correções são entregues como atualizações de pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="9c7fd-118">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="9c7fd-119">Não havia outros pacotes atualizados com 2.8.2 também.</span><span class="sxs-lookup"><span data-stu-id="9c7fd-119">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="9c7fd-120">Aqui está a lista de pacotes atualizados:</span><span class="sxs-lookup"><span data-stu-id="9c7fd-120">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="9c7fd-121">Core</span><span class="sxs-lookup"><span data-stu-id="9c7fd-121">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="9c7fd-122">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="9c7fd-122">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="9c7fd-123">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="9c7fd-123">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="9c7fd-124">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="9c7fd-124">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="9c7fd-125">[NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (o pacote, não a extensão)</span><span class="sxs-lookup"><span data-stu-id="9c7fd-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="9c7fd-126">Todas as alterações</span><span class="sxs-lookup"><span data-stu-id="9c7fd-126">All Changes</span></span>
<span data-ttu-id="9c7fd-127">Não havia 10 problemas abordados na versão.</span><span class="sxs-lookup"><span data-stu-id="9c7fd-127">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="9c7fd-128">Para obter uma lista completa do trabalho de itens corrigidos no NuGet 2.8.2,. exibir o [NuGet Issue Tracker para esta versão](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="9c7fd-128">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
