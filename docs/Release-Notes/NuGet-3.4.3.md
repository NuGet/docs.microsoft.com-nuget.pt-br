---
title: "Notas de versão do NuGet 3.4.3 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão para NuGet 3.4.3, incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs."
keywords: "Notas de versão NuGet 3.4.3, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 68aab607659d15f96aefeab7bb90afc787710824
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="66fe8-104">Notas de versão do NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="66fe8-104">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="66fe8-105">[Notas de versão do NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [notas de versão do NuGet 3.4.4](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="66fe8-105">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="66fe8-106">NuGet 3.4.3 foi lançado em 22 de abril de 2016 para abordar vários problemas que foram identificados nas versões 3.4 e subsequentes.</span><span class="sxs-lookup"><span data-stu-id="66fe8-106">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="66fe8-107">Você pode baixar o VSIX e nuget.exe [aqui](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="66fe8-107">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="66fe8-108">Atualizações e aprimoramentos</span><span class="sxs-lookup"><span data-stu-id="66fe8-108">Updates and Improvements</span></span>

* <span data-ttu-id="66fe8-109">Maior confiabilidade do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66fe8-109">Improved Visual Studio reliability.</span></span> <span data-ttu-id="66fe8-110">Corrigimos alguns problemas no NuGet que causou a falha no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66fe8-110">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="66fe8-111">Correções</span><span class="sxs-lookup"><span data-stu-id="66fe8-111">Fixes</span></span>

* <span data-ttu-id="66fe8-112">Corrigidos alguns problemas de autorização com o nuget privada protegida por senha feeds.</span><span class="sxs-lookup"><span data-stu-id="66fe8-112">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="66fe8-113">Corrigido um problema se não é possível restaurar PCL de `project.json` com tempos de execução especificados.</span><span class="sxs-lookup"><span data-stu-id="66fe8-113">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="66fe8-114">Alguns clientes estavam em execução em falhas intermitentes durante a instalação de pacotes.</span><span class="sxs-lookup"><span data-stu-id="66fe8-114">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="66fe8-115">Agora, esse problema foi corrigido nesta versão.</span><span class="sxs-lookup"><span data-stu-id="66fe8-115">This has now been fixed in this release.</span></span>
* <span data-ttu-id="66fe8-116">Corrigido um problema que causou a falhas de restauração no C + + CLI projetos com `project.json`.</span><span class="sxs-lookup"><span data-stu-id="66fe8-116">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="66fe8-117">Alguns pacotes (por exemplo ModernHttpClient) onde não descompactou corretamente quando você usa o nuget em mono.</span><span class="sxs-lookup"><span data-stu-id="66fe8-117">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="66fe8-118">Agora, esse problema foi corrigido nesta versão.</span><span class="sxs-lookup"><span data-stu-id="66fe8-118">This has now been fixed in this release.</span></span>

<span data-ttu-id="66fe8-119">Para obter uma lista de correções e aperfeiçoamentos desta versão, confira a lista de problemas [aqui](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="66fe8-119">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>