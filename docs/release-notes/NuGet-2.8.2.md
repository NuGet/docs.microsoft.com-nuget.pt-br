---
title: Notas de versão do NuGet 2.8.2
description: Notas de versão do NuGet 2.8.2 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a004c250d60a4ed1ca8dede1e83b2a68e10299bf
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821324"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="44ae9-103">Notas de versão do NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="44ae9-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="44ae9-104">[Notas de versão do NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 notas de versão](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="44ae9-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="44ae9-105">NuGet 2.8.2 foi lançado em 22 de maio de 2014.</span><span class="sxs-lookup"><span data-stu-id="44ae9-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="44ae9-106">Esta versão incluído somente as alterações para o nuget.exe de linha de comando, o pacote de NuGet.Server e outros pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="44ae9-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="44ae9-107">A versão não incluiu uma extensão atualizada do Visual Studio ou a extensão do WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="44ae9-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="44ae9-108">Atualizações importantes</span><span class="sxs-lookup"><span data-stu-id="44ae9-108">Notable Updates</span></span>

<span data-ttu-id="44ae9-109">As atualizações mais importantes foram no nuget.exe de linha de comando e o pacote de NuGet.Server (para feeds do NuGet auto-hospedado).</span><span class="sxs-lookup"><span data-stu-id="44ae9-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="44ae9-110">Correções de bugs importantes nuget.exe</span><span class="sxs-lookup"><span data-stu-id="44ae9-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="44ae9-111">NuGet.exe Push falha e mantém a tentar novamente</span><span class="sxs-lookup"><span data-stu-id="44ae9-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="44ae9-112">NuGet.exe por Push não envia credenciais de autenticação básica corretamente</span><span class="sxs-lookup"><span data-stu-id="44ae9-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="44ae9-113">Envio de NuGet.exe não siga redirecionamento temporário</span><span class="sxs-lookup"><span data-stu-id="44ae9-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="44ae9-114">Correção de Bug NuGet.Server importantes</span><span class="sxs-lookup"><span data-stu-id="44ae9-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="44ae9-115">Valor incorreto de IsAbsoluteLatestVersion retornado por NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="44ae9-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="44ae9-116">Pacotes atualizados</span><span class="sxs-lookup"><span data-stu-id="44ae9-116">Packages Updated</span></span>

<span data-ttu-id="44ae9-117">O nuget.exe de linha de comando e NuGet.Server correções são entregues como atualizações de pacote do NuGet.</span><span class="sxs-lookup"><span data-stu-id="44ae9-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="44ae9-118">Não havia outros pacotes atualizados com 2.8.2 também.</span><span class="sxs-lookup"><span data-stu-id="44ae9-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="44ae9-119">Aqui está a lista de pacotes atualizados:</span><span class="sxs-lookup"><span data-stu-id="44ae9-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="44ae9-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="44ae9-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="44ae9-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="44ae9-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="44ae9-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="44ae9-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="44ae9-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="44ae9-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="44ae9-124">[NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (o pacote, não a extensão)</span><span class="sxs-lookup"><span data-stu-id="44ae9-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="44ae9-125">Todas as alterações</span><span class="sxs-lookup"><span data-stu-id="44ae9-125">All Changes</span></span>
<span data-ttu-id="44ae9-126">Não havia 10 problemas abordados na versão.</span><span class="sxs-lookup"><span data-stu-id="44ae9-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="44ae9-127">Para obter uma lista completa do trabalho de itens corrigidos no NuGet 2.8.2,. exibir o [NuGet Issue Tracker para esta versão](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="44ae9-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
