---
title: "Notas de versão do NuGet 1.6 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão do NuGet 1.6 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão 1.6 do NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 114b03cede24dee520ace1d8aa920a648ad16af1
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="ef6d8-104">Notas de versão 1.6 do NuGet</span><span class="sxs-lookup"><span data-stu-id="ef6d8-104">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="ef6d8-105">[Notas de versão do NuGet 1.5](../release-notes/nuget-1.5.md) | [notas de versão 1.7 do NuGet](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="ef6d8-105">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="ef6d8-106">1.6 NuGet foi lançado em 13 de dezembro de 2011.</span><span class="sxs-lookup"><span data-stu-id="ef6d8-106">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="ef6d8-107">Problema de instalação conhecidos</span><span class="sxs-lookup"><span data-stu-id="ef6d8-107">Known Installation Issue</span></span>
<span data-ttu-id="ef6d8-108">Se você estiver executando o VS 2010 SP1, você pode executar em um erro de instalação durante a tentativa de atualizar o NuGet se você tiver uma versão mais antiga.</span><span class="sxs-lookup"><span data-stu-id="ef6d8-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="ef6d8-109">A solução alternativa é simplesmente desinstalar NuGet e, em seguida, instalá-lo a partir da Galeria de extensão do VS.</span><span class="sxs-lookup"><span data-stu-id="ef6d8-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="ef6d8-110">Consulte [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="ef6d8-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="ef6d8-111">Observação: Se o Visual Studio não permitirão que você desinstalar a extensão (o botão de desinstalação estiver desabilitado), em seguida, provavelmente você precisa reiniciar o Visual Studio usando "Executar como administrador".</span><span class="sxs-lookup"><span data-stu-id="ef6d8-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="ef6d8-112">Recursos</span><span class="sxs-lookup"><span data-stu-id="ef6d8-112">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="ef6d8-113">Suporte para controle de versão semântico e pacotes de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="ef6d8-113">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="ef6d8-114">NuGet 1.6 apresenta suporte para controle de versão semântico (SemVer).</span><span class="sxs-lookup"><span data-stu-id="ef6d8-114">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="ef6d8-115">Para obter mais detalhes sobre como ele usa SemVer, leia o [documentação de controle de versão](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ef6d8-115">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="ef6d8-116">Usando o NuGet sem a verificação em pacotes (restauração do pacote)</span><span class="sxs-lookup"><span data-stu-id="ef6d8-116">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="ef6d8-117">1.6 NuGet agora tem suporte de primeira classe do fluxo de trabalho no qual NuGet pacotes não são adicionados ao controle de origem, mas em vez disso, são restaurados em tempo de compilação se ausente.</span><span class="sxs-lookup"><span data-stu-id="ef6d8-117">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="ef6d8-118">Para obter mais detalhes, leia o [usando o NuGet sem confirmar pacotes ao controle de origem](../consume-packages/packages-and-source-control.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="ef6d8-118">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="ef6d8-119">Modelos de item que instalam os pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="ef6d8-119">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="ef6d8-120">Aproveitando o trabalho para dar suporte ao pacote de NuGet pré-instalados para modelos de projeto do Visual Studio, o NuGet 1.6 também adiciona suporte para modelos de item do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ef6d8-120">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="ef6d8-121">Modelos de item podem ter associados a pacotes do NuGet que são instalados quando o modelo na chamada.</span><span class="sxs-lookup"><span data-stu-id="ef6d8-121">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="ef6d8-122">Para obter mais detalhes sobre como alterar um modelo de item do projeto para instalar os pacotes NuGet, leia o [pacotes em modelos do Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="ef6d8-122">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="ef6d8-123">Suporte para desabilitar origens do pacote</span><span class="sxs-lookup"><span data-stu-id="ef6d8-123">Support for disabling package sources</span></span>
<span data-ttu-id="ef6d8-124">Quando várias fontes de pacote são configurados, NuGet aparecerá em cada uma para os pacotes durante a instalação de um pacote e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="ef6d8-124">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="ef6d8-125">Uma origem do pacote que está inativo por algum motivo severos lenta NuGet.</span><span class="sxs-lookup"><span data-stu-id="ef6d8-125">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="ef6d8-126">Antes de 1.6 NuGet, você pode remover a origem do pacote, mas, em seguida, você precisa se lembrar os detalhes para quando quiser adicioná-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="ef6d8-126">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="ef6d8-127">1.6 NuGet permite desmarcar uma origem do pacote para desabilitá-lo, mas mantê-lo.</span><span class="sxs-lookup"><span data-stu-id="ef6d8-127">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Desabilitando um pacote](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="ef6d8-129">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="ef6d8-129">Bug Fixes</span></span>
<span data-ttu-id="ef6d8-130">1.6 NuGet tinha um total de 106 fixos de itens de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ef6d8-130">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="ef6d8-131">95 deles foram classificados como bugs e 10 deles foram recursos.</span><span class="sxs-lookup"><span data-stu-id="ef6d8-131">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="ef6d8-132">Para obter uma lista completa de trabalho itens corrigidos no NuGet 1.6, por favor, exibição de [NuGet Issue Tracker para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="ef6d8-132">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
