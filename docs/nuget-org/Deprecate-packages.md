---
title: Depreciando pacotes em nuget.org
description: Descrição detalhada sobre o processo de depreciação de pacotes e como os clientes mostram essas informações
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "74096877"
---
# <a name="deprecating-packages"></a><span data-ttu-id="2f2b1-103">Depreciação de pacotes</span><span class="sxs-lookup"><span data-stu-id="2f2b1-103">Deprecating packages</span></span>

<span data-ttu-id="2f2b1-104">Você pode depreciar um pacote se você não mantiver mais um pacote ou se quiser encorajar os consumidores do seu pacote a se mudarem para outro pacote.</span><span class="sxs-lookup"><span data-stu-id="2f2b1-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="2f2b1-105">A depreciação do pacote é diferente da **deslistagem** do seu pacote, conforme explicado abaixo:</span><span class="sxs-lookup"><span data-stu-id="2f2b1-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="2f2b1-106">**A deslistagem de** um pacote impede sua descoberta porque está escondida nos resultados de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="2f2b1-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="2f2b1-107">**Depreciar** um pacote permite que os consumidores existentes do seu pacote descubram se eles o instalaram ou foram usados em seus projetos.</span><span class="sxs-lookup"><span data-stu-id="2f2b1-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="2f2b1-108">Ele também permite que eles saibam o motivo da depreciação e um pacote recomendado alternativo, conforme especificado por você (o editor do pacote).</span><span class="sxs-lookup"><span data-stu-id="2f2b1-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="2f2b1-109">Depreciar um pacote não deslista o pacote.</span><span class="sxs-lookup"><span data-stu-id="2f2b1-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="2f2b1-110">Como editor, você pode optar por deslistar, bem como depredar pacotes.</span><span class="sxs-lookup"><span data-stu-id="2f2b1-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="2f2b1-111">Fluxo de trabalho de depreciação</span><span class="sxs-lookup"><span data-stu-id="2f2b1-111">Deprecation workflow</span></span>
1. <span data-ttu-id="2f2b1-112">Para depreciar um pacote, vá para **Gerenciar pacotes** e **selecione Depreciação**:</span><span class="sxs-lookup"><span data-stu-id="2f2b1-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![Vá para depreciar a opção de pacote](media/deprecation-select-option.png)

2. <span data-ttu-id="2f2b1-114">Selecione a versão que deseja depreciar.</span><span class="sxs-lookup"><span data-stu-id="2f2b1-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="2f2b1-115">Se você quiser depreciar todas as versões, escolha Selecionar a opção **Selecionar todas as versões.**</span><span class="sxs-lookup"><span data-stu-id="2f2b1-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![Selecione versões do pacote para depreciar](media/deprecation-select-version.png)

3. <span data-ttu-id="2f2b1-117">Escolha uma razão para depreciação.</span><span class="sxs-lookup"><span data-stu-id="2f2b1-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="2f2b1-118">Se o pacote não for mais mantido, escolha a opção **Legado.**</span><span class="sxs-lookup"><span data-stu-id="2f2b1-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="2f2b1-119">Se a versão específica tiver um bug crítico, escolha a opção **tem bugs críticos.**</span><span class="sxs-lookup"><span data-stu-id="2f2b1-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="2f2b1-120">Por qualquer outra razão, selecione **Outros**.</span><span class="sxs-lookup"><span data-stu-id="2f2b1-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="2f2b1-121">Você sempre pode especificar um pacote recomendado alternativo (e uma versão) e uma mensagem personalizada para os proprietários.</span><span class="sxs-lookup"><span data-stu-id="2f2b1-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![Selecione razões para recomendação de pacote alternativo e mensagem personalizada](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="2f2b1-123">A mensagem personalizada só é mostrada em nuget.org mas não dos clientes.</span><span class="sxs-lookup"><span data-stu-id="2f2b1-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="2f2b1-124">Atualmente, clientes `dotnet.exe` como e o NuGet Package Manager não mostram a mensagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="2f2b1-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="2f2b1-125">Experiência do cliente para pacotes preteridos</span><span class="sxs-lookup"><span data-stu-id="2f2b1-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="2f2b1-126">Uma vez que um pacote tenha sido preterido, seus consumidores são notificados sobre ele das seguintes maneiras (dependendo do cliente utilizado).</span><span class="sxs-lookup"><span data-stu-id="2f2b1-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="2f2b1-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2f2b1-127">Visual Studio</span></span> 
<span data-ttu-id="2f2b1-128">*Disponível a partir do Visual Studio 2019 versão 16.3*</span><span class="sxs-lookup"><span data-stu-id="2f2b1-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="2f2b1-129">Visual Studio avisa sobre o uso de um `Installed` pacote preterido na guia. Ele mostrará um aviso para o pacote e suas informações de depreciação (incluindo a razão pela qual foi preterido e o pacote alternativo para usar em seu lugar, se presente).</span><span class="sxs-lookup"><span data-stu-id="2f2b1-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab. It will show a warning for the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![Pacotes depreciados no Visual Studio instalado guia do gerenciador de pacotes](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="2f2b1-131">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="2f2b1-131">dotnet.exe</span></span>
<span data-ttu-id="2f2b1-132">*Disponível a partir de .NET SDK 3.0*</span><span class="sxs-lookup"><span data-stu-id="2f2b1-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="2f2b1-133">Se você usar dotnet.exe, você `dotnet list package --deprecated` pode executar o comando na solução ou pasta do projeto para obter uma lista de pacotes depreciados, juntamente com as informações de depreciação:</span><span class="sxs-lookup"><span data-stu-id="2f2b1-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
