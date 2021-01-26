---
title: Notas de versão do NuGet 1,7
description: Notas de versão do NuGet 1,7 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777070"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="920e6-103">Notas de versão do NuGet 1,7</span><span class="sxs-lookup"><span data-stu-id="920e6-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="920e6-104">Notas de versão do [NuGet 1,6](../release-notes/nuget-1.6.md)  |  [Notas de versão do NuGet 1,8](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="920e6-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="920e6-105">O NuGet 1,7 foi lançado em 4 de abril de 2012.</span><span class="sxs-lookup"><span data-stu-id="920e6-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="920e6-106">Problema de instalação conhecido</span><span class="sxs-lookup"><span data-stu-id="920e6-106">Known Installation Issue</span></span>
<span data-ttu-id="920e6-107">Se você estiver executando o VS 2010 SP1, poderá encontrar um erro de instalação ao tentar atualizar o NuGet se tiver uma versão mais antiga instalada.</span><span class="sxs-lookup"><span data-stu-id="920e6-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="920e6-108">A solução alternativa é simplesmente desinstalar o NuGet e, em seguida, instalá-lo a partir da Galeria de extensões do VS.</span><span class="sxs-lookup"><span data-stu-id="920e6-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="920e6-109">Consulte <https://support.microsoft.com/kb/2581019> para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="920e6-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="920e6-110">Observação: se o Visual Studio não permitir que você desinstale a extensão (o botão desinstalar está desabilitado), provavelmente, você precisará reiniciar o Visual Studio usando "executar como administrador".</span><span class="sxs-lookup"><span data-stu-id="920e6-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="920e6-111">Recursos</span><span class="sxs-lookup"><span data-stu-id="920e6-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="920e6-112">Suporte ao abrir o arquivo de readme.txt após a instalação</span><span class="sxs-lookup"><span data-stu-id="920e6-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="920e6-113">Novo no 1,7, se o pacote incluir um `readme.txt` arquivo na raiz do pacote, o NuGet abrirá automaticamente esse arquivo depois de concluir a instalação do pacote.</span><span class="sxs-lookup"><span data-stu-id="920e6-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="920e6-114">Mostrar pacotes de pré-lançamento na caixa de diálogo gerenciar pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="920e6-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="920e6-115">A caixa de diálogo gerenciar pacotes NuGet agora inclui uma lista suspensa que fornece a opção para mostrar pacotes de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="920e6-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Mostrando pacotes de pré-lançamento](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="920e6-117">Mostrar botão de restauração de pacote quando arquivos de pacote estiverem ausentes</span><span class="sxs-lookup"><span data-stu-id="920e6-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="920e6-118">Quando você abre o console do Gerenciador de pacotes ou a caixa de diálogo pacotes NuGet do Gerenciador, o NuGet verificará se a solução atual habilitou o modo de restauração do pacote e se algum arquivo de pacote está ausente da `packages` pasta.</span><span class="sxs-lookup"><span data-stu-id="920e6-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="920e6-119">Se essas duas condições forem atendidas, o NuGet irá notificá-lo e mostrará um botão de restauração conveniente.</span><span class="sxs-lookup"><span data-stu-id="920e6-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="920e6-120">Clicar neste botão irá disparar o NuGet para restaurar todos os pacotes ausentes.</span><span class="sxs-lookup"><span data-stu-id="920e6-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Botão de restauração do pacote na caixa de diálogo](./media/packagerestore-dialog.png)

![Botão de restauração do pacote no console](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="920e6-123">Adicionar arquivo de packages.config no nível da solução</span><span class="sxs-lookup"><span data-stu-id="920e6-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="920e6-124">Nas versões anteriores do NuGet, cada projeto tem um `packages.config` arquivo que controla quais pacotes NuGet estão instalados nesse projeto.</span><span class="sxs-lookup"><span data-stu-id="920e6-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="920e6-125">No entanto, não havia nenhum arquivo semelhante no nível da solução para controlar os pacotes no nível da solução.</span><span class="sxs-lookup"><span data-stu-id="920e6-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="920e6-126">Como resultado, não havia como restaurar pacotes de nível de solução.</span><span class="sxs-lookup"><span data-stu-id="920e6-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="920e6-127">Esse recurso agora está implementado no NuGet 1,7.</span><span class="sxs-lookup"><span data-stu-id="920e6-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="920e6-128">O arquivo de nível de solução `packages.config` é colocado sob a `.nuget` pasta na raiz da solução e armazenará apenas pacotes no nível da solução.</span><span class="sxs-lookup"><span data-stu-id="920e6-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="920e6-129">Remover New-Package comando</span><span class="sxs-lookup"><span data-stu-id="920e6-129">Remove New-Package command</span></span>
<span data-ttu-id="920e6-130">Devido ao baixo uso, o comando New-Package foi removido.</span><span class="sxs-lookup"><span data-stu-id="920e6-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="920e6-131">Os desenvolvedores são recomendados a usar nuget.exe ou o Gerenciador de pacotes do NuGet útil para criar pacotes.</span><span class="sxs-lookup"><span data-stu-id="920e6-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="920e6-132">Correções de bugs</span><span class="sxs-lookup"><span data-stu-id="920e6-132">Bug Fixes</span></span>
<span data-ttu-id="920e6-133">O NuGet 1,7 corrigiu muitos bugs em relação ao fluxo de trabalho de restauração de pacote e aos cenários de controle de rede/origem.</span><span class="sxs-lookup"><span data-stu-id="920e6-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="920e6-134">Para obter uma lista completa de itens de trabalho corrigidos no NuGet 1,7, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="920e6-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
