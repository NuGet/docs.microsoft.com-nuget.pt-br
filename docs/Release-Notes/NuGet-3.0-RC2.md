---
title: "Notas de versão do NuGet 3.0 RC2 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 20f9b360-2d78-4676-a803-e86996eb2f10
description: "Notas de versão do NuGet 3.0 RC2 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão NuGet 3.0 RC2, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2a708babf200a650a0faffc704235d3c142f510f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="a3157-104">Notas de versão do NuGet 3.0 RC2</span><span class="sxs-lookup"><span data-stu-id="a3157-104">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="a3157-105">[Notas de versão do NuGet 3.0 RC](../release-notes/nuget-3.0-RC.md) | [notas de versão do NuGet 3.0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="a3157-105">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="a3157-106">Lançada em 3 de junho de 2015 RC2 do NuGet 3.0 como versão disponível da Galeria de extensões do Visual Studio 2015 e [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="a3157-106">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="a3157-107">Esta versão tem um número de correções de bugs importantes e melhorias de desempenho que constatamos foram importantes liberar antes do lançamento do Visual Studio 2015 concluído.</span><span class="sxs-lookup"><span data-stu-id="a3157-107">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="a3157-108">Esta versão da extensão NuGet só está disponível para o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="a3157-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="a3157-109">No total, é fechada 158 problemas nesta versão, e você pode examinar o [lista completa dos problemas no GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="a3157-109">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="a3157-110">Resumo dos principais problemas resolvidos</span><span class="sxs-lookup"><span data-stu-id="a3157-110">Summary of top issues resolved</span></span>

* [<span data-ttu-id="a3157-111">Atualização da rede frequentes chama quando a janela do Gerenciador de pacote é atualizada</span><span class="sxs-lookup"><span data-stu-id="a3157-111">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="a3157-112">Atrasado rolagem quando alterar para instalado exibição no Gerenciador de pacotes</span><span class="sxs-lookup"><span data-stu-id="a3157-112">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="a3157-113">Chamadas de rede devem ser executadas em um thread em segundo plano</span><span class="sxs-lookup"><span data-stu-id="a3157-113">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="a3157-114">Adicionar caixa de seleção 'Não mostrar a janela de visualização'</span><span class="sxs-lookup"><span data-stu-id="a3157-114">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="a3157-115">Limitação para reduzir a utilização do processador do processo de inclusão</span><span class="sxs-lookup"><span data-stu-id="a3157-115">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="a3157-116">Melhor tratamento de referência de biblioteca de classes portátil</span><span class="sxs-lookup"><span data-stu-id="a3157-116">Improved portable-class-library reference handling</span></span>
    * [<span data-ttu-id="a3157-117">https://GitHub.com/NuGet/home/issues/562</span><span class="sxs-lookup"><span data-stu-id="a3157-117">https://github.com/NuGet/Home/issues/562</span></span>](https://github.com/NuGet/Home/issues/562)
    * [<span data-ttu-id="a3157-118">https://GitHub.com/NuGet/home/issues/454</span><span class="sxs-lookup"><span data-stu-id="a3157-118">https://github.com/NuGet/Home/issues/454</span></span>](https://github.com/NuGet/Home/issues/454)
    * [<span data-ttu-id="a3157-119">https://GitHub.com/NuGet/home/issues/440</span><span class="sxs-lookup"><span data-stu-id="a3157-119">https://github.com/NuGet/Home/issues/440</span></span>](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="a3157-120">Serviço de preenchimento automático foi diferencia maiusculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="a3157-120">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="a3157-121">Atualização reintroduzir credenciais de autenticação básica</span><span class="sxs-lookup"><span data-stu-id="a3157-121">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="a3157-122">Log de erros aprimorado</span><span class="sxs-lookup"><span data-stu-id="a3157-122">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="a3157-123">Mensagens de erro do powershell aprimorado ao chamar o pacote de atualização</span><span class="sxs-lookup"><span data-stu-id="a3157-123">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="a3157-124">Baixe este [atualizar para a extensão do NuGet](https://nuget.codeplex.com/releases/view/615507) do Codeplex e fique atento [nosso blog](http://blog.nuget.org) para mais de progresso e avisos do NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="a3157-124">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>