---
title: Notas de versão 3.0 do NuGet
description: Notas de versão do NuGet 3.0.0 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 26236c2db0e1a6be9c660905db567d9ebbbbe377
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820284"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="b4117-103">Notas de versão 3.0 do NuGet</span><span class="sxs-lookup"><span data-stu-id="b4117-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="b4117-104">[Notas de versão do NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [notas de versão 3.1 do NuGet](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="b4117-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="b4117-105">NuGet 3.0 foi lançado em 20 de julho de 2015 como uma extensão do pacote para o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="b4117-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="b4117-106">É enviado para oferecer esta versão com o Visual Studio para que a experiência completa de NuGet 3.0 atualizada está disponível para novos usuários do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b4117-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="b4117-107">Esta versão da extensão NuGet só está disponível para o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="b4117-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="b4117-108">Recomendamos que os desenvolvedores que têm acesso a atualização da Galeria do Visual Studio para a versão mais recente está disponível, como estamos publicando uma atualização logo após o lançamento do Visual Studio 2015 que contém suporte para o desenvolvimento do Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b4117-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="b4117-109">No total, é fechada 240 problemas na versão 3.0, e você pode examinar o [lista completa dos problemas no GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="b4117-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="b4117-110">Problemas Conhecidos</span><span class="sxs-lookup"><span data-stu-id="b4117-110">Known Issues</span></span>

<span data-ttu-id="b4117-111">Houve um número de problemas conhecidos, fornecido com esta versão e todos esses itens corrigidos na nossa versão 3.1 agendado para coincidir com a versão do Windows 10 em 29 de julho.</span><span class="sxs-lookup"><span data-stu-id="b4117-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="b4117-112">É possível atualizar a extensão do Visual Studio da Galeria em ou após essa data para corrigir esses problemas conhecidos.</span><span class="sxs-lookup"><span data-stu-id="b4117-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="b4117-113">Conversão não for fornecida para o rótulo "Não mostrar esta mensagem novamente" na janela de visualização e o rótulo "Autores" na janela de descrição do pacote.</span><span class="sxs-lookup"><span data-stu-id="b4117-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="b4117-114">Quando você trabalhar em um projeto usando o TFS controle de origem, o NuGet não é possível apresentar o Gerenciador de pacotes interface do usuário se o arquivo NuGet. config está marcado como somente leitura.</span><span class="sxs-lookup"><span data-stu-id="b4117-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="b4117-115">**Solução alternativa** Check-out do arquivo do TFS.</span><span class="sxs-lookup"><span data-stu-id="b4117-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="b4117-116">Texto em amarelos "reinicialização barra" na janela do Powershell do NuGet não é visível quando você usa o tema escuro do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b4117-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="b4117-117">**Solução alternativa** usar o tema claro do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b4117-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="b4117-118">Resumo dos principais problemas resolvidos</span><span class="sxs-lookup"><span data-stu-id="b4117-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="b4117-119">Atualização da rede frequentes chama quando a janela do Gerenciador de pacote é atualizada</span><span class="sxs-lookup"><span data-stu-id="b4117-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="b4117-120">Atrasado rolagem quando alterar para instalado exibição no Gerenciador de pacotes</span><span class="sxs-lookup"><span data-stu-id="b4117-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="b4117-121">Chamadas de rede devem ser executadas em um thread em segundo plano</span><span class="sxs-lookup"><span data-stu-id="b4117-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="b4117-122">Adicionar caixa de seleção 'Não mostrar a janela de visualização'</span><span class="sxs-lookup"><span data-stu-id="b4117-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="b4117-123">Limitação para reduzir a utilização do processador do processo de inclusão</span><span class="sxs-lookup"><span data-stu-id="b4117-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="b4117-124">Melhor tratamento de referência de biblioteca de classes portátil</span><span class="sxs-lookup"><span data-stu-id="b4117-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="b4117-125">Serviço de preenchimento automático foi diferencia maiusculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="b4117-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="b4117-126">Atualização reintroduzir credenciais de autenticação básica</span><span class="sxs-lookup"><span data-stu-id="b4117-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="b4117-127">Log de erros aprimorado</span><span class="sxs-lookup"><span data-stu-id="b4117-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="b4117-128">Mensagens de erro do powershell aprimorado ao chamar o pacote de atualização</span><span class="sxs-lookup"><span data-stu-id="b4117-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="b4117-129">Corrigido o link 'Saiba mais sobre as opções' para evitar falhas no Windows 10</span><span class="sxs-lookup"><span data-stu-id="b4117-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="b4117-130">Lembre-se a configuração da caixa de seleção de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="b4117-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="b4117-131">Obter melhor desempenho armazenando em cache os resultados em projetos em uma solução</span><span class="sxs-lookup"><span data-stu-id="b4117-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="b4117-132">Vários pacotes podem ser obtidos em paralelo</span><span class="sxs-lookup"><span data-stu-id="b4117-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="b4117-133">Removeu o pacote de instalação-força o comando</span><span class="sxs-lookup"><span data-stu-id="b4117-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="b4117-134">Fique atento [nosso blog](http://blog.nuget.org) para mais de progresso e anúncios como preparamos oferecer suporte para o desenvolvimento do Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b4117-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>