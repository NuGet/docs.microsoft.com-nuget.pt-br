---
title: Notas de versão do NuGet 3.2.1
description: Notas de versão do NuGet 3.2.1, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776525"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="6a06b-103">Notas de versão do NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="6a06b-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="6a06b-104">Notas de versão do [NuGet 3,2](../release-notes/nuget-3.2.md)  |  [Notas de versão do NuGet 3,3](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="6a06b-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="6a06b-105">O NuGet 3.2.1 para a linha de comando foi lançado em 12 de outubro de 2015 com algumas otimizações e correções para a versão 3,2 e está disponível em [dist.NuGet.org](http://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="6a06b-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="6a06b-106">Aprimoramentos</span><span class="sxs-lookup"><span data-stu-id="6a06b-106">Improvements</span></span>

* <span data-ttu-id="6a06b-107">O NuGet agora usa o arquivo de configuração com a capitalização original de `NuGet.Config` .</span><span class="sxs-lookup"><span data-stu-id="6a06b-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="6a06b-108">Isso é importante em sistemas operacionais com distinção de maiúsculas e minúsculas [1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="6a06b-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="6a06b-109">A restauração do NuGet agora irá ignorar projetos DNX ( `*.xproj` ) que devem ser processados com `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="6a06b-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="6a06b-110">Utilização de rede otimizada ao trabalhar com `index.json` e empacotar dados de registro [1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="6a06b-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="6a06b-111">Tratamento aprimorado de download de recursos para ser mais robusto com os serviços v2 [1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="6a06b-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="6a06b-112">Correções</span><span class="sxs-lookup"><span data-stu-id="6a06b-112">Fixes</span></span>

* <span data-ttu-id="6a06b-113">A atualização do NuGet atualiza corretamente as `.csproj` / `.vcxproj` referências [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="6a06b-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="6a06b-114">Agora, impedir que uma pasta local. NuGet seja criada quando um SpecialFolders. UserProfile não puder ser localizado [1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="6a06b-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="6a06b-115">Tratamento aprimorado de pacotes no cache local que estão corrompidos durante o download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="6a06b-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="6a06b-116">Uma lista completa de problemas abordados para a extensão de linha de comando e do Visual Studio pode ser encontrada no [Marco](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed) do GitHub do NuGet 3.2.1</span><span class="sxs-lookup"><span data-stu-id="6a06b-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="6a06b-117">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="6a06b-117">Known Issues</span></span>

<span data-ttu-id="6a06b-118">Continuamos a acompanhar problemas em nossa lista de problemas do GitHub, que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="6a06b-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>