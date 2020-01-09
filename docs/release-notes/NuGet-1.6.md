---
title: Notas de versão do NuGet 1,6
description: Notas de versão do NuGet 1,6 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2878d3809b2be4fb71f4e7b1a1e08e405ead44b9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384131"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="6aa48-103">Notas de versão do NuGet 1,6</span><span class="sxs-lookup"><span data-stu-id="6aa48-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="6aa48-104">[Notas de versão do nuget 1,5](../release-notes/nuget-1.5.md) | [notas de versão do NuGet 1,7](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="6aa48-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="6aa48-105">O NuGet 1,6 foi lançado em 13 de dezembro de 2011.</span><span class="sxs-lookup"><span data-stu-id="6aa48-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="6aa48-106">Problema de instalação conhecido</span><span class="sxs-lookup"><span data-stu-id="6aa48-106">Known Installation Issue</span></span>
<span data-ttu-id="6aa48-107">Se você estiver executando o VS 2010 SP1, poderá encontrar um erro de instalação ao tentar atualizar o NuGet se tiver uma versão mais antiga instalada.</span><span class="sxs-lookup"><span data-stu-id="6aa48-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="6aa48-108">A solução alternativa é simplesmente desinstalar o NuGet e, em seguida, instalá-lo a partir da Galeria de extensões do VS.</span><span class="sxs-lookup"><span data-stu-id="6aa48-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="6aa48-109">Consulte <https://support.microsoft.com/kb/2581019> para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="6aa48-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="6aa48-110">Observação: se o Visual Studio não permitir que você desinstale a extensão (o botão desinstalar está desabilitado), provavelmente, você precisará reiniciar o Visual Studio usando "executar como administrador".</span><span class="sxs-lookup"><span data-stu-id="6aa48-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="6aa48-111">Recursos</span><span class="sxs-lookup"><span data-stu-id="6aa48-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="6aa48-112">Suporte para versão semântica e pacotes de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="6aa48-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="6aa48-113">O NuGet 1,6 apresenta suporte para o controle de versão semântico (SemVer).</span><span class="sxs-lookup"><span data-stu-id="6aa48-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="6aa48-114">Para obter mais detalhes sobre como ele usa o SemVer, leia a [documentação de controle de versão](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="6aa48-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="6aa48-115">Usando o NuGet sem fazer check-in de pacotes (restauração de pacote)</span><span class="sxs-lookup"><span data-stu-id="6aa48-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="6aa48-116">O NuGet 1,6 agora tem suporte de primeira classe para o fluxo de trabalho no qual os pacotes NuGet não são adicionados ao controle do código-fonte, mas, em vez disso, são restaurados no momento da compilação, se ausente.</span><span class="sxs-lookup"><span data-stu-id="6aa48-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="6aa48-117">Para obter mais detalhes, leia o tópico [usando o NuGet sem confirmar pacotes no controle do código-fonte](../consume-packages/packages-and-source-control.md) .</span><span class="sxs-lookup"><span data-stu-id="6aa48-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="6aa48-118">Modelos de item que instalam pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="6aa48-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="6aa48-119">Com base no trabalho para dar suporte ao pacote do NuGet pré-instalado para modelos de projeto do Visual Studio, o NuGet 1,6 também adiciona suporte para modelos de item do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6aa48-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="6aa48-120">Os modelos de item podem ter pacotes NuGet associados que são instalados quando o modelo é chamado.</span><span class="sxs-lookup"><span data-stu-id="6aa48-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="6aa48-121">Para obter mais detalhes sobre como alterar um modelo de projeto/item para instalar pacotes NuGet, leia o tópico [pacotes no Visual Studio modelos](../visual-studio-extensibility/visual-studio-templates.md) .</span><span class="sxs-lookup"><span data-stu-id="6aa48-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="6aa48-122">Suporte para desabilitar as origens do pacote</span><span class="sxs-lookup"><span data-stu-id="6aa48-122">Support for disabling package sources</span></span>
<span data-ttu-id="6aa48-123">Quando várias fontes de pacote são configuradas, o NuGet examinará cada uma para pacotes durante a instalação de um pacote e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="6aa48-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="6aa48-124">Uma origem de pacote que está inoperante por algum motivo pode retardar seriamente o NuGet.</span><span class="sxs-lookup"><span data-stu-id="6aa48-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="6aa48-125">Antes do NuGet 1,6, você pode remover a origem do pacote, mas, em seguida, você precisa se lembrar dos detalhes de quando deseja adicioná-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="6aa48-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="6aa48-126">O NuGet 1,6 permite desmarcar uma origem de pacote para desabilitá-la, mas mantê-la.</span><span class="sxs-lookup"><span data-stu-id="6aa48-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Desabilitando um pacote](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="6aa48-128">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="6aa48-128">Bug Fixes</span></span>
<span data-ttu-id="6aa48-129">O NuGet 1,6 tinha um total de 106 itens de trabalho corrigidos.</span><span class="sxs-lookup"><span data-stu-id="6aa48-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="6aa48-130">95 daqueles foram classificados como bugs e 10 desses eram recursos.</span><span class="sxs-lookup"><span data-stu-id="6aa48-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="6aa48-131">Para obter uma lista completa de itens de trabalho corrigidos no NuGet 1,6, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="6aa48-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
