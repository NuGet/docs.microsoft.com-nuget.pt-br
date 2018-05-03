---
title: Notas de versão 1.7 do NuGet
description: Notas de versão do NuGet 1.7 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 81db81642ac21b7dd41f5940dfba919d0871ec01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="1c762-103">Notas de versão 1.7 do NuGet</span><span class="sxs-lookup"><span data-stu-id="1c762-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="1c762-104">[Notas de versão do NuGet 1.6](../release-notes/nuget-1.6.md) | [notas de versão 1.8 do NuGet](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="1c762-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="1c762-105">1.7 NuGet foi lançado em 4 de abril de 2012.</span><span class="sxs-lookup"><span data-stu-id="1c762-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="1c762-106">Problema de instalação conhecidos</span><span class="sxs-lookup"><span data-stu-id="1c762-106">Known Installation Issue</span></span>
<span data-ttu-id="1c762-107">Se você estiver executando o VS 2010 SP1, você pode executar em um erro de instalação durante a tentativa de atualizar o NuGet se você tiver uma versão mais antiga.</span><span class="sxs-lookup"><span data-stu-id="1c762-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="1c762-108">A solução alternativa é simplesmente desinstalar NuGet e, em seguida, instalá-lo a partir da Galeria de extensão do VS.</span><span class="sxs-lookup"><span data-stu-id="1c762-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="1c762-109">Veja [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="1c762-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="1c762-110">Observação: Se o Visual Studio não permitirão que você desinstalar a extensão (o botão de desinstalação estiver desabilitado), em seguida, provavelmente você precisa reiniciar o Visual Studio usando "Executar como administrador".</span><span class="sxs-lookup"><span data-stu-id="1c762-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="1c762-111">Recursos</span><span class="sxs-lookup"><span data-stu-id="1c762-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="1c762-112">Suporte para abertura de arquivo Leiame. txt após a instalação</span><span class="sxs-lookup"><span data-stu-id="1c762-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="1c762-113">Novo no 1.7, se o pacote inclui um `readme.txt` arquivo na raiz do pacote, o NuGet abrirá automaticamente esse arquivo depois que ele terminou de instalar o pacote.</span><span class="sxs-lookup"><span data-stu-id="1c762-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="1c762-114">Mostrar pacotes de pré-lançamento na caixa de diálogo Gerenciar NuGet pacotes</span><span class="sxs-lookup"><span data-stu-id="1c762-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="1c762-115">A caixa de diálogo Gerenciar pacotes NuGet agora inclui uma lista suspensa que fornece a opção para mostrar os pacotes de pré-lançamento.</span><span class="sxs-lookup"><span data-stu-id="1c762-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Mostrando os pacotes de pré-lançamento](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="1c762-117">Mostrar botão de restauração de pacotes quando os arquivos de pacote estão ausentes</span><span class="sxs-lookup"><span data-stu-id="1c762-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="1c762-118">Quando você abrir o console do Gerenciador de pacotes ou pacotes do NuGet do Gerenciador de caixa de diálogo, o NuGet irá verificar se a solução atual tiver habilitado o modo de restauração de pacote e se os arquivos de pacote estão ausentes do `packages` pasta.</span><span class="sxs-lookup"><span data-stu-id="1c762-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="1c762-119">Se estas duas condições forem atendidas, o NuGet será notificado e mostrará um botão Restaurar conveniente.</span><span class="sxs-lookup"><span data-stu-id="1c762-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="1c762-120">Este botão irá disparar o NuGet para restaurar todos os pacotes ausentes.</span><span class="sxs-lookup"><span data-stu-id="1c762-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![Botão de restauração do pacote na caixa de diálogo](./media/packagerestore-dialog.png)

![Botão de restauração do pacote no console](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="1c762-123">Adicionar arquivo Packages. config de nível de solução</span><span class="sxs-lookup"><span data-stu-id="1c762-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="1c762-124">Nas versões anteriores do NuGet, cada projeto tem um `packages.config` arquivo que mantém o controle de quais pacotes NuGet estão instalados no projeto.</span><span class="sxs-lookup"><span data-stu-id="1c762-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="1c762-125">No entanto, não houve nenhum arquivo semelhante no nível da solução para controlar os pacotes de solução de nível.</span><span class="sxs-lookup"><span data-stu-id="1c762-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="1c762-126">Como resultado, não havia uma maneira de restaurar os pacotes de solução de nível.</span><span class="sxs-lookup"><span data-stu-id="1c762-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="1c762-127">Agora, esse recurso é implementado no NuGet 1.7.</span><span class="sxs-lookup"><span data-stu-id="1c762-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="1c762-128">Nível da solução `packages.config` arquivo está sob o `.nuget` pasta sob a solução raiz e armazena os pacotes somente de solução de nível.</span><span class="sxs-lookup"><span data-stu-id="1c762-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="1c762-129">Remova o comando New-Package</span><span class="sxs-lookup"><span data-stu-id="1c762-129">Remove New-Package command</span></span>
<span data-ttu-id="1c762-130">Devido ao uso de baixo, o comando New-Package foi removido.</span><span class="sxs-lookup"><span data-stu-id="1c762-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="1c762-131">Os desenvolvedores são recomendados para usar o nuget.exe ou o Explorador de pacotes do NuGet útil para criar pacotes.</span><span class="sxs-lookup"><span data-stu-id="1c762-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="1c762-132">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="1c762-132">Bug Fixes</span></span>
<span data-ttu-id="1c762-133">1.7 NuGet corrigiu vários bugs em torno de fluxo de trabalho de restauração de pacotes e cenários de controle de origem da rede /.</span><span class="sxs-lookup"><span data-stu-id="1c762-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="1c762-134">Para obter uma lista completa de trabalho itens corrigidos no NuGet 1.7. exibir o [NuGet Issue Tracker para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="1c762-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
