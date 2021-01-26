---
title: Notas de versão do NuGet 3.4.3
description: Notas de versão do NuGet 3.4.3 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776465"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="0e1c4-103">Notas de versão do NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="0e1c4-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="0e1c4-104">Notas de versão do [NuGet 3.4.2](../release-notes/nuget-3.4.2.md)  |  [Notas de versão do NuGet 3.4.4](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="0e1c4-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="0e1c4-105">O NuGet 3.4.3 foi lançado em 22 de abril de 2016 para resolver vários problemas identificados nas versões 3,4 e subsequentes.</span><span class="sxs-lookup"><span data-stu-id="0e1c4-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="0e1c4-106">Você pode baixar o VSIX e o nuget.exe [aqui](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="0e1c4-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="0e1c4-107">Atualizações e aprimoramentos</span><span class="sxs-lookup"><span data-stu-id="0e1c4-107">Updates and Improvements</span></span>

* <span data-ttu-id="0e1c4-108">Confiabilidade aprimorada do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0e1c4-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="0e1c4-109">Corrigimos alguns problemas no NuGet que causaram falhas no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0e1c4-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="0e1c4-110">Correções</span><span class="sxs-lookup"><span data-stu-id="0e1c4-110">Fixes</span></span>

* <span data-ttu-id="0e1c4-111">Correção de alguns problemas de autorização com feeds do NuGet privados protegidos por senha.</span><span class="sxs-lookup"><span data-stu-id="0e1c4-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="0e1c4-112">Correção de um problema ao não conseguir restaurar PCL do `project.json` com tempos de execução especificados.</span><span class="sxs-lookup"><span data-stu-id="0e1c4-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="0e1c4-113">Alguns clientes estavam executando falhas intermitentes ao instalar pacotes.</span><span class="sxs-lookup"><span data-stu-id="0e1c4-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="0e1c4-114">Agora, isso foi corrigido nesta versão.</span><span class="sxs-lookup"><span data-stu-id="0e1c4-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="0e1c4-115">Correção de um problema que causou falhas de restauração em projetos C++/CLI com `project.json` .</span><span class="sxs-lookup"><span data-stu-id="0e1c4-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="0e1c4-116">Alguns pacotes (por exemplo, ModernHttpClient) onde não são descompactados corretamente quando você usa o NuGet no mono.</span><span class="sxs-lookup"><span data-stu-id="0e1c4-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="0e1c4-117">Agora, isso foi corrigido nesta versão.</span><span class="sxs-lookup"><span data-stu-id="0e1c4-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="0e1c4-118">Para obter uma lista completa de correções e aprimoramentos nesta versão, confira a lista de problemas [aqui](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="0e1c4-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>