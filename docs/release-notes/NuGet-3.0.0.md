---
title: Notas de versão do NuGet 3,0
description: Notas de versão do NuGet 3.0.0 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776554"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="f1b54-103">Notas de versão do NuGet 3,0</span><span class="sxs-lookup"><span data-stu-id="f1b54-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="f1b54-104">Notas de versão do [NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)  |  [Notas de versão do NuGet 3,1](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="f1b54-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="f1b54-105">O NuGet 3,0 foi lançado em 20 de julho de 2015 como uma extensão de pacote para o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="f1b54-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="f1b54-106">Enviamos por push essa versão com o Visual Studio para que a experiência completa do NuGet 3,0 esteja disponível para novos usuários do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1b54-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="f1b54-107">Esta versão de extensão NuGet só está disponível para o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="f1b54-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="f1b54-108">Recomendamos que esses desenvolvedores tenham acesso à atualização da galeria do Visual Studio para a versão mais recente disponível, pois publicaremos uma atualização logo após o lançamento do Visual Studio 2015 que contém suporte para o desenvolvimento do Windows 10.</span><span class="sxs-lookup"><span data-stu-id="f1b54-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="f1b54-109">No total, fechamos 240 problemas na versão 3,0, e você pode examinar a [lista completa de problemas no GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="f1b54-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="f1b54-110">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="f1b54-110">Known Issues</span></span>

<span data-ttu-id="f1b54-111">Houve uma série de problemas conhecidos fornecidos com esta versão, e todos esses itens são corrigidos em nossa versão 3,1 agendada para coincidir com o lançamento do Windows 10 em julho de 29.</span><span class="sxs-lookup"><span data-stu-id="f1b54-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="f1b54-112">Você pode atualizar sua extensão do Visual Studio a partir da galeria ou após essa data para corrigir esses problemas conhecidos.</span><span class="sxs-lookup"><span data-stu-id="f1b54-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="f1b54-113">A tradução não é fornecida para o rótulo "não mostrar isso novamente" na janela de visualização e no rótulo "autores" na janela descrição do pacote.</span><span class="sxs-lookup"><span data-stu-id="f1b54-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="f1b54-114">Quando você trabalha em um projeto usando o controle do código-fonte do TFS, o NuGet não pode apresentar a interface do usuário do Gerenciador de pacotes se o arquivo de Nuget.Config está marcado como somente leitura.</span><span class="sxs-lookup"><span data-stu-id="f1b54-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="f1b54-115">**Solução alternativa** Confira o arquivo do TFS.</span><span class="sxs-lookup"><span data-stu-id="f1b54-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="f1b54-116">O texto na "barra de reinício" amarela na janela do PowerShell do NuGet não é visível quando você usa o tema escuro do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1b54-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="f1b54-117">**Solução alternativa** Use o tema do Visual Studio Light.</span><span class="sxs-lookup"><span data-stu-id="f1b54-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="f1b54-118">Resumo dos principais problemas resolvidos</span><span class="sxs-lookup"><span data-stu-id="f1b54-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="f1b54-119">Chamadas frequentes de atualização de rede quando a janela do Gerenciador de pacotes é atualizada</span><span class="sxs-lookup"><span data-stu-id="f1b54-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="f1b54-120">Rolagem atrasada ao mudar para a exibição instalada no Gerenciador de pacotes</span><span class="sxs-lookup"><span data-stu-id="f1b54-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="f1b54-121">Chamadas de rede devem ser executadas em um thread em segundo plano</span><span class="sxs-lookup"><span data-stu-id="f1b54-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="f1b54-122">Caixa de seleção ' não mostrar janela de visualização ' adicionada</span><span class="sxs-lookup"><span data-stu-id="f1b54-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="f1b54-123">Limitação de processo adicionada para reduzir o uso do processador</span><span class="sxs-lookup"><span data-stu-id="f1b54-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="f1b54-124">Manipulação de referência de biblioteca de classe portátil aprimorada</span><span class="sxs-lookup"><span data-stu-id="f1b54-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="f1b54-125">O serviço de conclusão total diferencia maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="f1b54-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="f1b54-126">Atualizar para reintroduzir as credenciais básicas de autenticação</span><span class="sxs-lookup"><span data-stu-id="f1b54-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="f1b54-127">Aprimorado o relatório de erros</span><span class="sxs-lookup"><span data-stu-id="f1b54-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="f1b54-128">Mensagens de erro do PowerShell aprimoradas ao chamar Update-Package</span><span class="sxs-lookup"><span data-stu-id="f1b54-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="f1b54-129">Correção do link "Saiba mais sobre as opções" para evitar falhas no Windows 10</span><span class="sxs-lookup"><span data-stu-id="f1b54-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="f1b54-130">Lembrar configuração da caixa de seleção de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="f1b54-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="f1b54-131">Melhor desempenho de coleta armazenando em cache os resultados entre projetos em uma solução</span><span class="sxs-lookup"><span data-stu-id="f1b54-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="f1b54-132">Vários pacotes podem ser coletados em paralelo</span><span class="sxs-lookup"><span data-stu-id="f1b54-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="f1b54-133">Removida a instalação do comando Package-Force</span><span class="sxs-lookup"><span data-stu-id="f1b54-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="f1b54-134">Fique atento ao [nosso blog](http://blog.nuget.org) para obter mais progresso e anúncios, pois estamos prontos para fornecer suporte para o desenvolvimento do Windows 10.</span><span class="sxs-lookup"><span data-stu-id="f1b54-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>