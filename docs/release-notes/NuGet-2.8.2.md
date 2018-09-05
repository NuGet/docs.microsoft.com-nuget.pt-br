---
title: Notas de versão do NuGet 2.8.2
description: Notas de versão do NuGet 2.8.2 incluindo conhecidos problemas, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551142"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="8df1e-103">Notas de versão do NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="8df1e-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="8df1e-104">[Notas de versão do NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [notas de versão do NuGet 2.8.3](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="8df1e-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="8df1e-105">O NuGet 2.8.2 foi lançado em 22 de maio de 2014.</span><span class="sxs-lookup"><span data-stu-id="8df1e-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="8df1e-106">Esta versão incluídas apenas as alterações a nuget.exe de linha de comando, o pacote do NuGet. Server e outros pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="8df1e-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="8df1e-107">A versão não incluía uma extensão atualizada do Visual Studio ou a extensão do WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="8df1e-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="8df1e-108">Atualizações importantes</span><span class="sxs-lookup"><span data-stu-id="8df1e-108">Notable Updates</span></span>

<span data-ttu-id="8df1e-109">As atualizações mais importantes ocorreram no nuget.exe de linha de comando e o pacote do NuGet. Server (para feeds de NuGet auto-hospedados).</span><span class="sxs-lookup"><span data-stu-id="8df1e-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="8df1e-110">Correções de bugs importantes nuget.exe</span><span class="sxs-lookup"><span data-stu-id="8df1e-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="8df1e-111">NuGet.exe Push falha e mantém a tentar novamente</span><span class="sxs-lookup"><span data-stu-id="8df1e-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="8df1e-112">NuGet.exe por Push não envia as credenciais de autenticação básica corretamente</span><span class="sxs-lookup"><span data-stu-id="8df1e-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="8df1e-113">NuGet.exe por Push não siga redirecionamento temporário</span><span class="sxs-lookup"><span data-stu-id="8df1e-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="8df1e-114">Correção de Bug importantes NuGet. Server</span><span class="sxs-lookup"><span data-stu-id="8df1e-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="8df1e-115">Valor incorreto de IsAbsoluteLatestVersion retornado pelo NuGet. Server</span><span class="sxs-lookup"><span data-stu-id="8df1e-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="8df1e-116">Pacotes atualizados</span><span class="sxs-lookup"><span data-stu-id="8df1e-116">Packages Updated</span></span>

<span data-ttu-id="8df1e-117">Os nuget.exe de linha de comando e as correções do NuGet. Server são fornecidas como atualizações de pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="8df1e-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="8df1e-118">Não havia outros pacotes atualizados com 2.8.2 também.</span><span class="sxs-lookup"><span data-stu-id="8df1e-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="8df1e-119">Aqui está a lista de pacotes atualizadas:</span><span class="sxs-lookup"><span data-stu-id="8df1e-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="8df1e-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="8df1e-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="8df1e-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="8df1e-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="8df1e-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="8df1e-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="8df1e-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="8df1e-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="8df1e-124">[NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (o pacote, não a extensão)</span><span class="sxs-lookup"><span data-stu-id="8df1e-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="8df1e-125">Todas as alterações</span><span class="sxs-lookup"><span data-stu-id="8df1e-125">All Changes</span></span>
<span data-ttu-id="8df1e-126">Havia 10 problemas abordados na versão.</span><span class="sxs-lookup"><span data-stu-id="8df1e-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="8df1e-127">Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.8.2, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="8df1e-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
