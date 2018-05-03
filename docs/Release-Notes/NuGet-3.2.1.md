---
title: Notas de versão do NuGet 3.2.1
description: Notas de versão do NuGet 3.2.1 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 039fabaaacfdffd76fa88ff8183548e97cd4719b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="17230-103">Notas de versão do NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="17230-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="17230-104">[Notas de versão do NuGet 3.2](../release-notes/nuget-3.2.md) | [notas de versão do NuGet 3.3](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="17230-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="17230-105">3.2.1 o NuGet para a linha de comando foi lançado em 12 de outubro de 2015 com algumas otimizações e correções para a versão 3.2 e está disponível em [dist.nuget.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="17230-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="17230-106">Melhorias</span><span class="sxs-lookup"><span data-stu-id="17230-106">Improvements</span></span>

* <span data-ttu-id="17230-107">Agora, o NuGet usa o arquivo de configuração com o uso de maiusculas original `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="17230-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="17230-108">Isso é importante em sistemas operacionais de maiusculas e minúsculas [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="17230-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="17230-109">Restauração do NuGet agora irá ignorar projetos dnx (`*.xproj`) que deve ser processado com `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="17230-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="17230-110">Otimização de uso da rede quando estiver trabalhando com `index.json` e dados de registro do pacote [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="17230-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="17230-111">Download de recurso aprimorado tratamento para ser mais robustos com serviços v2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="17230-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="17230-112">Correções</span><span class="sxs-lookup"><span data-stu-id="17230-112">Fixes</span></span>

* <span data-ttu-id="17230-113">NuGet corretamente atualiza `.csproj` / `.vcxproj` referências [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="17230-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="17230-114">Impedindo que uma pasta. NuGet local sejam criadas quando um SpecialFolders.UserProfile não é possível localizar [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="17230-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="17230-115">Melhor tratamento de pacotes no cache local está corrompida durante o download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="17230-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="17230-116">Uma lista completa dos problemas abordados para a extensão de linha de comando e o Visual Studio pode ser encontrada no NuGet GitHub [3.2.1 marco](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="17230-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="17230-117">Problemas Conhecidos</span><span class="sxs-lookup"><span data-stu-id="17230-117">Known Issues</span></span>

<span data-ttu-id="17230-118">Continuamos a rastrear problemas em nossa lista de problemas do GitHub que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="17230-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>