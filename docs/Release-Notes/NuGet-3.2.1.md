---
title: "Notas de versão do NuGet 3.2.1 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão do NuGet 3.2.1 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs."
keywords: "Notas de versão NuGet 3.2.1, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7c9c2457c33eb3630f632c98bf0cf96703c3a548
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="7f4b3-104">Notas de versão do NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="7f4b3-104">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="7f4b3-105">[Notas de versão do NuGet 3.2](../release-notes/nuget-3.2.md) | [notas de versão do NuGet 3.3](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="7f4b3-105">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="7f4b3-106">3.2.1 o NuGet para a linha de comando foi lançado em 12 de outubro de 2015 com algumas otimizações e correções para a versão 3.2 e está disponível em [dist.nuget.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="7f4b3-106">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="7f4b3-107">Melhorias</span><span class="sxs-lookup"><span data-stu-id="7f4b3-107">Improvements</span></span>

* <span data-ttu-id="7f4b3-108">Agora, o NuGet usa o arquivo de configuração com o uso de maiusculas original `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="7f4b3-108">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="7f4b3-109">Isso é importante em sistemas operacionais de maiusculas e minúsculas [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="7f4b3-109">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="7f4b3-110">Restauração do NuGet agora irá ignorar projetos dnx (`*.xproj`) que deve ser processado com `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="7f4b3-110">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="7f4b3-111">Otimização de uso da rede quando estiver trabalhando com `index.json` e dados de registro do pacote [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="7f4b3-111">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="7f4b3-112">Download de recurso aprimorado tratamento para ser mais robustos com serviços v2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="7f4b3-112">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="7f4b3-113">Correções</span><span class="sxs-lookup"><span data-stu-id="7f4b3-113">Fixes</span></span>

* <span data-ttu-id="7f4b3-114">NuGet corretamente atualiza `.csproj` / `.vcxproj` referências [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="7f4b3-114">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="7f4b3-115">Impedindo que uma pasta. NuGet local sejam criadas quando um SpecialFolders.UserProfile não é possível localizar [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="7f4b3-115">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="7f4b3-116">Melhor tratamento de pacotes no cache local está corrompida durante o download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="7f4b3-116">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="7f4b3-117">Uma lista completa dos problemas abordados para a extensão de linha de comando e o Visual Studio pode ser encontrada no NuGet GitHub [3.2.1 marco](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="7f4b3-117">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="7f4b3-118">Problemas Conhecidos</span><span class="sxs-lookup"><span data-stu-id="7f4b3-118">Known Issues</span></span>

<span data-ttu-id="7f4b3-119">Continuamos a rastrear problemas em nossa lista de problemas do GitHub que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="7f4b3-119">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>