---
title: Notas de versão do NuGet 3.4.3
description: Notas de versão do NuGet 3.4.3 incluindo conhecidos problemas, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549159"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="2ddda-103">Notas de versão do NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="2ddda-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="2ddda-104">[Notas de versão do NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [notas de versão do NuGet 3.4.4](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="2ddda-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="2ddda-105">O NuGet 3.4.3 foi lançado em 22 de abril de 2016 para abordar vários problemas que foram identificados nas versões 3.4 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="2ddda-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="2ddda-106">Você pode baixar o VSIX e nuget.exe [aqui](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="2ddda-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="2ddda-107">Atualizações e aprimoramentos</span><span class="sxs-lookup"><span data-stu-id="2ddda-107">Updates and Improvements</span></span>

* <span data-ttu-id="2ddda-108">Confiabilidade aprimorada do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2ddda-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="2ddda-109">Corrigimos alguns problemas no NuGet que causou a falha no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2ddda-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="2ddda-110">Correções</span><span class="sxs-lookup"><span data-stu-id="2ddda-110">Fixes</span></span>

* <span data-ttu-id="2ddda-111">Correção de alguns problemas de autorização com o nuget privado protegido por senha feeds.</span><span class="sxs-lookup"><span data-stu-id="2ddda-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="2ddda-112">Corrigido um problema em torno de não ser capaz de restaurar o PCL do `project.json` com tempos de execução especificados.</span><span class="sxs-lookup"><span data-stu-id="2ddda-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="2ddda-113">Alguns clientes estavam sendo executados em falhas intermitentes durante a instalação de pacotes.</span><span class="sxs-lookup"><span data-stu-id="2ddda-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="2ddda-114">Agora, esse problema foi corrigido nesta versão.</span><span class="sxs-lookup"><span data-stu-id="2ddda-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="2ddda-115">Corrigido um problema que causava falhas de restauração no C + + c++ CLI projetos com `project.json`.</span><span class="sxs-lookup"><span data-stu-id="2ddda-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="2ddda-116">Alguns pacotes (por exemplo ModernHttpClient) onde não sendo descompactou corretamente quando você usa o nuget em mono.</span><span class="sxs-lookup"><span data-stu-id="2ddda-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="2ddda-117">Agora, esse problema foi corrigido nesta versão.</span><span class="sxs-lookup"><span data-stu-id="2ddda-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="2ddda-118">Para obter uma lista de correções e aprimoramentos nesta versão, confira a lista de problemas [aqui](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="2ddda-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>