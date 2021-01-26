---
title: Notas de versão do NuGet 3,0 RC2
description: Notas de versão do NuGet 3,0 RC2, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780273"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="917f2-103">Notas de versão do NuGet 3,0 RC2</span><span class="sxs-lookup"><span data-stu-id="917f2-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="917f2-104">Notas de versão do [NuGet 3,0 RC](../release-notes/nuget-3.0-RC.md)  |  [Notas de versão do NuGet 3,0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="917f2-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="917f2-105">O NuGet 3,0 RC2 foi lançado em 3 de junho de 2015 como uma versão provisória disponível na Galeria de extensões do Visual Studio 2015 e no [codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="917f2-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="917f2-106">Esta versão tem uma série de correções de bugs importantes e melhorias de desempenho que achamos importantes para serem lançadas antes da versão concluída do Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="917f2-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="917f2-107">Esta versão de extensão NuGet só está disponível para o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="917f2-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="917f2-108">No total, fechamos 158 problemas nesta versão, e você pode examinar a [lista completa de problemas no GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="917f2-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="917f2-109">Resumo dos principais problemas resolvidos</span><span class="sxs-lookup"><span data-stu-id="917f2-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="917f2-110">Chamadas frequentes de atualização de rede quando a janela do Gerenciador de pacotes é atualizada</span><span class="sxs-lookup"><span data-stu-id="917f2-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="917f2-111">Rolagem atrasada ao mudar para a exibição instalada no Gerenciador de pacotes</span><span class="sxs-lookup"><span data-stu-id="917f2-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="917f2-112">Chamadas de rede devem ser executadas em um thread em segundo plano</span><span class="sxs-lookup"><span data-stu-id="917f2-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="917f2-113">Caixa de seleção ' não mostrar janela de visualização ' adicionada</span><span class="sxs-lookup"><span data-stu-id="917f2-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="917f2-114">Limitação de processo adicionada para reduzir o uso do processador</span><span class="sxs-lookup"><span data-stu-id="917f2-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="917f2-115">Manipulação de referência de biblioteca de classe portátil aprimorada</span><span class="sxs-lookup"><span data-stu-id="917f2-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="917f2-116">O serviço de conclusão total diferencia maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="917f2-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="917f2-117">Atualizar para reintroduzir as credenciais básicas de autenticação</span><span class="sxs-lookup"><span data-stu-id="917f2-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="917f2-118">Aprimorado o relatório de erros</span><span class="sxs-lookup"><span data-stu-id="917f2-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="917f2-119">Mensagens de erro do PowerShell aprimoradas ao chamar Update-Package</span><span class="sxs-lookup"><span data-stu-id="917f2-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="917f2-120">Baixe essa [atualização para a extensão do NuGet](https://nuget.codeplex.com/releases/view/615507) do CodePlex e fique atento ao [nosso blog](http://blog.nuget.org) para obter mais progresso e anúncios para o NuGet 3,0!</span><span class="sxs-lookup"><span data-stu-id="917f2-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>