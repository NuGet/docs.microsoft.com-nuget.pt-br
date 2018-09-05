---
title: Notas de versão 1.6 do NuGet
description: Notas da versão 1.6 do NuGet incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549006"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="81ccc-103">Notas de versão 1.6 do NuGet</span><span class="sxs-lookup"><span data-stu-id="81ccc-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="81ccc-104">[Notas de versão do NuGet 1.5](../release-notes/nuget-1.5.md) | [notas de versão do NuGet 1.7](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="81ccc-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="81ccc-105">O NuGet 1.6 foi lançada em 13 de dezembro de 2011.</span><span class="sxs-lookup"><span data-stu-id="81ccc-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="81ccc-106">Problema de instalação conhecidos</span><span class="sxs-lookup"><span data-stu-id="81ccc-106">Known Installation Issue</span></span>
<span data-ttu-id="81ccc-107">Se você estiver executando o VS 2010 SP1, você pode executar em um erro de instalação quando tentar atualizar o NuGet se você tiver uma versão mais antiga instalada.</span><span class="sxs-lookup"><span data-stu-id="81ccc-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="81ccc-108">A solução alternativa é simplesmente desinstalar o NuGet e, em seguida, instalá-lo da Galeria de extensão do VS.</span><span class="sxs-lookup"><span data-stu-id="81ccc-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="81ccc-109">Veja [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="81ccc-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="81ccc-110">Observação: Se o Visual Studio não permitirão que você desinstale a extensão (o botão Desinstalar está desabilitado), em seguida, é provável que você precisa reiniciar o Visual Studio usando "Executar como administrador".</span><span class="sxs-lookup"><span data-stu-id="81ccc-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="81ccc-111">Recursos</span><span class="sxs-lookup"><span data-stu-id="81ccc-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="81ccc-112">Suporte para controle de versão semântico e pacotes de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="81ccc-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="81ccc-113">O NuGet 1.6 apresenta suporte para controle de versão semântico (SemVer).</span><span class="sxs-lookup"><span data-stu-id="81ccc-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="81ccc-114">Para obter mais detalhes sobre como ele usa o SemVer, leia as [documentação do controle de versão](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="81ccc-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="81ccc-115">Usando o NuGet sem fazer check-In de pacotes (restauração de pacote)</span><span class="sxs-lookup"><span data-stu-id="81ccc-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="81ccc-116">O NuGet 1.6 agora tem suporte de primeira classe para o fluxo de trabalho no qual NuGet pacotes não são adicionados ao controle de origem, mas em vez disso, são restaurados no momento da compilação se estiverem ausentes.</span><span class="sxs-lookup"><span data-stu-id="81ccc-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="81ccc-117">Para obter mais detalhes, leia as [usando o NuGet sem confirmar pacotes no controle do código-fonte](../consume-packages/packages-and-source-control.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="81ccc-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="81ccc-118">Modelos de item que instalar os pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="81ccc-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="81ccc-119">Criando o trabalho para dar suporte ao pacote do NuGet pré-instalado para modelos de projeto do Visual Studio, 1.6 do NuGet também adiciona suporte para modelos de item do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="81ccc-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="81ccc-120">Modelos de item podem ter associadas a pacotes do NuGet que são instalados quando o modelo no invocado.</span><span class="sxs-lookup"><span data-stu-id="81ccc-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="81ccc-121">Para obter mais detalhes sobre como alterar um modelo de projeto/item para instalar pacotes do NuGet, leia as [pacotes em modelos do Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="81ccc-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="81ccc-122">Suporte para desabilitar origens de pacote</span><span class="sxs-lookup"><span data-stu-id="81ccc-122">Support for disabling package sources</span></span>
<span data-ttu-id="81ccc-123">Quando várias origens de pacote são configuradas, NuGet examinará cada um para pacotes durante a instalação de um pacote e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="81ccc-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="81ccc-124">Uma origem de pacote que está inativo por algum motivo gravemente lenta NuGet.</span><span class="sxs-lookup"><span data-stu-id="81ccc-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="81ccc-125">Antes do NuGet 1.6, você pode remover a origem do pacote, mas, em seguida, você precisa se lembrar os detalhes para quando você quiser adicioná-lo de volta.</span><span class="sxs-lookup"><span data-stu-id="81ccc-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="81ccc-126">O NuGet 1.6 permite desmarcando uma origem de pacote para desabilitá-lo, mas mantê-lo.</span><span class="sxs-lookup"><span data-stu-id="81ccc-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Desabilitando um pacote](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="81ccc-128">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="81ccc-128">Bug Fixes</span></span>
<span data-ttu-id="81ccc-129">O NuGet 1.6 tinha um total de 106 fixos de itens de trabalho.</span><span class="sxs-lookup"><span data-stu-id="81ccc-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="81ccc-130">95 deles foram classificados como bugs e foram de 10 desses recursos.</span><span class="sxs-lookup"><span data-stu-id="81ccc-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="81ccc-131">Para obter uma lista completa de trabalho itens corrigidos no NuGet 1.6, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="81ccc-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
