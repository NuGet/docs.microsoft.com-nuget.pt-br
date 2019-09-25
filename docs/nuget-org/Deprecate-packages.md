---
title: Preterindo pacotes no nuget.org
description: Descrição detalhada sobre o processo de substituição de pacotes e como os clientes mostram essas informações
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 120b463fda856fe9dd407b6eba32d60e0918f763
ms.sourcegitcommit: 188ade66b7ac807ba1667c77cfb9325bf89a8a4a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71248893"
---
# <a name="deprecating-packages"></a><span data-ttu-id="3743d-103">Substituição de pacotes</span><span class="sxs-lookup"><span data-stu-id="3743d-103">Deprecating packages</span></span>

<span data-ttu-id="3743d-104">Você poderá substituir um pacote se não mantiver mais um pacote ou se desejar incentivar os consumidores do pacote a migrar para outro pacote.</span><span class="sxs-lookup"><span data-stu-id="3743d-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="3743d-105">A substituição do pacote é diferente de **deslistar** o pacote, conforme explicado abaixo:</span><span class="sxs-lookup"><span data-stu-id="3743d-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="3743d-106">A **deslistação** de um pacote impede sua descoberta porque está oculta nos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="3743d-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="3743d-107">A **substituição** de um pacote permite que os consumidores existentes do pacote descubram se eles o têm instalado ou usados em seus projetos.</span><span class="sxs-lookup"><span data-stu-id="3743d-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="3743d-108">Ele também permite que eles saibam o motivo da substituição e um pacote recomendado alternativo, conforme especificado por você (o fornecedor do pacote).</span><span class="sxs-lookup"><span data-stu-id="3743d-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="3743d-109">A substituição de um pacote não lista o pacote.</span><span class="sxs-lookup"><span data-stu-id="3743d-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="3743d-110">Como Publicador, você pode optar por deslistar, bem como substituir pacotes.</span><span class="sxs-lookup"><span data-stu-id="3743d-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="3743d-111">Fluxo de trabalho de substituição</span><span class="sxs-lookup"><span data-stu-id="3743d-111">Deprecation workflow</span></span>
1. <span data-ttu-id="3743d-112">Para substituir um pacote, vá para **gerenciar pacotes** e selecione **reprovação**:</span><span class="sxs-lookup"><span data-stu-id="3743d-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![Ir para a opção de pacote obsoleto](media/deprecation-select-option.png)

2. <span data-ttu-id="3743d-114">Selecione a versão que deseja substituir.</span><span class="sxs-lookup"><span data-stu-id="3743d-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="3743d-115">Se você quiser substituir toda a versão, escolha a opção **selecionar todas as versões** .</span><span class="sxs-lookup"><span data-stu-id="3743d-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![Selecionar versões de pacote para preterir](media/deprecation-select-version.png)

3. <span data-ttu-id="3743d-117">Escolha um motivo para a reprovação.</span><span class="sxs-lookup"><span data-stu-id="3743d-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="3743d-118">Se o pacote não for mais mantido, escolha a opção **herdada** .</span><span class="sxs-lookup"><span data-stu-id="3743d-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="3743d-119">Se a versão específica tiver um bug crítico, escolha a opção **tem bugs críticos** .</span><span class="sxs-lookup"><span data-stu-id="3743d-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="3743d-120">Por qualquer outro motivo, selecione **outro**.</span><span class="sxs-lookup"><span data-stu-id="3743d-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="3743d-121">Você sempre pode especificar um pacote recomendado alternativo (e versão) e uma mensagem personalizada para os proprietários.</span><span class="sxs-lookup"><span data-stu-id="3743d-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![Selecionar motivos da recomendação do pacote alternativo e da mensagem personalizada](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="3743d-123">A mensagem personalizada só é mostrada em nuget.org, mas não nos clientes.</span><span class="sxs-lookup"><span data-stu-id="3743d-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="3743d-124">Atualmente, clientes como `dotnet.exe` o e o Gerenciador de pacotes NuGet não mostram a mensagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="3743d-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="3743d-125">Experiência do cliente para pacotes preteridos</span><span class="sxs-lookup"><span data-stu-id="3743d-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="3743d-126">Depois que um pacote tiver sido preterido, seus consumidores serão notificados sobre ele das seguintes maneiras (dependendo do cliente usado).</span><span class="sxs-lookup"><span data-stu-id="3743d-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="3743d-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3743d-127">Visual Studio</span></span> 
<span data-ttu-id="3743d-128">*Disponível a partir do Visual Studio 2019 versão 16,3*</span><span class="sxs-lookup"><span data-stu-id="3743d-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="3743d-129">O Visual Studio avisa sobre o `Installed` uso de um pacote preterido na guia. Ele levará você para o pacote e suas informações de substituição (incluindo o motivo de ele ter sido preterido e o pacote alternativo a ser usado, se houver).</span><span class="sxs-lookup"><span data-stu-id="3743d-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab.It will lead you to the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![Pacotes preteridos na guia Visual Studio instalada do Gerenciador de pacotes](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="3743d-131">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="3743d-131">dotnet.exe</span></span>
<span data-ttu-id="3743d-132">*Disponível a partir do SDK do .NET 3,0*</span><span class="sxs-lookup"><span data-stu-id="3743d-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="3743d-133">Se você usar dotnet. exe, poderá executar o comando `dotnet list package --deprecated` na pasta da solução ou do projeto para obter uma lista de pacotes preteridos junto com as informações de substituição:</span><span class="sxs-lookup"><span data-stu-id="3743d-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
