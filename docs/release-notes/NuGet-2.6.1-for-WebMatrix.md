---
title: NuGet 2.6.1 para notas de lançamento do WebMatrix
description: Notas de versão do NuGet 2.6.1 para WebMatrix, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550311"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="aab67-103">NuGet 2.6.1 para notas de lançamento do WebMatrix</span><span class="sxs-lookup"><span data-stu-id="aab67-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="aab67-104">[Notas de versão do NuGet 2.6](../release-notes/nuget-2.6.md) | [notas de versão do NuGet 2.7](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="aab67-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="aab67-105">A equipe do NuGet lançou uma extensão do Gerenciador de pacotes NuGet atualizado para o WebMatrix em 26 de março de 2014.</span><span class="sxs-lookup"><span data-stu-id="aab67-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="aab67-106">Essa atualização pode ser instalada do [Galeria de extensão do WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) usando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="aab67-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="aab67-107">Abre o WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="aab67-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="aab67-108">Clique no ícone de extensões na faixa de opções página inicial</span><span class="sxs-lookup"><span data-stu-id="aab67-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="aab67-109">Selecione a guia atualizações</span><span class="sxs-lookup"><span data-stu-id="aab67-109">Select the Updates tab</span></span>
1. <span data-ttu-id="aab67-110">Clique para atualizar o Gerenciador de pacotes NuGet para 2.6.1</span><span class="sxs-lookup"><span data-stu-id="aab67-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="aab67-111">Feche e reinicie o WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="aab67-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="aab67-112">Alterações importantes</span><span class="sxs-lookup"><span data-stu-id="aab67-112">Notable Changes</span></span>

<span data-ttu-id="aab67-113">Essa extensão atualização resolve dois dos usuários problemas maiores têm enfrentado consumir pacotes do NuGet do WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="aab67-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="aab67-114">O primeiro foi um erro de versão de esquema do NuGet e a segunda era um bug que leva a DLLs de zero byte no `bin` pasta.</span><span class="sxs-lookup"><span data-stu-id="aab67-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="aab67-115">Erro de versão do esquema do NuGet</span><span class="sxs-lookup"><span data-stu-id="aab67-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="aab67-116">Desde o lançamento do WebMatrix 3, novos recursos foram introduzidos no NuGet que exigem uma nova versão de esquema para os pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="aab67-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="aab67-117">Ao tentar gerenciar os pacotes do NuGet em seu site da web, esses novos pacotes podem levar a erros que você vê no WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="aab67-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Ocorreu um erro.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="aab67-121">Esta versão mais recente fornece compatibilidade com os pacotes NuGet mais recentes, impedindo que esse erro ocorra.</span><span class="sxs-lookup"><span data-stu-id="aab67-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="aab67-122">Novas versões dos pacotes incluindo Microsoft.AspNet.WebPages agora podem ser instaladas no WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="aab67-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="aab67-123">Alguns desses pacotes foram usando recursos do NuGet, como [transformações XDT config](../release-notes/nuget-2.6.md#xdt), que não era suportado no WebMatrix até agora.</span><span class="sxs-lookup"><span data-stu-id="aab67-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="aab67-124">DLLs de zero bytes na pasta de compartimentalização</span><span class="sxs-lookup"><span data-stu-id="aab67-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="aab67-125">Alguns usuários relataram que a depois de instalar o NuGet pacotes em WebMatrix que incluem as DLLs que podem ser copiadas para o compartimento que mostram as DLLs para cima no `bin` pasta arquivos de 0 byte.</span><span class="sxs-lookup"><span data-stu-id="aab67-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="aab67-126">Isso interrompe o aplicativo em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="aab67-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="aab67-127">[Esse problema](https://nuget.codeplex.com/workitem/4060) agora foi corrigido.</span><span class="sxs-lookup"><span data-stu-id="aab67-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="aab67-128">Outros aperfeiçoamentos recentes</span><span class="sxs-lookup"><span data-stu-id="aab67-128">Other Recent Improvements</span></span>

<span data-ttu-id="aab67-129">Quando o Gerenciador de pacote NuGet 2.8 foi lançado para o Visual Studio, também lançamos NuGet Package Manager 2.5.0 para o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="aab67-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="aab67-130">Enquanto isso foi mencionado o [notas de versão do NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), não mencionamos específico novos recursos que introduziu a atualização.</span><span class="sxs-lookup"><span data-stu-id="aab67-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="aab67-131">Atualizar tudo</span><span class="sxs-lookup"><span data-stu-id="aab67-131">Update All</span></span>

<span data-ttu-id="aab67-132">Agora você pode atualizar todos os pacotes do seu site em uma única etapa!</span><span class="sxs-lookup"><span data-stu-id="aab67-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="aab67-133">Quando você abre a extensão do NuGet no WebMatrix, você ver a lista de todos os pacotes na galeria, estiverem instalados e aqueles com atualizações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="aab67-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="aab67-134">Anteriormente, todos os pacotes precisaria ser atualizado individualmente, mas agora há um botão "Atualizar tudo" útil que aparece na guia atualizações.</span><span class="sxs-lookup"><span data-stu-id="aab67-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Clique em Atualizar tudo para atualizar todos os pacotes com atualizações disponíveis](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="aab67-136">Substituir arquivos existentes</span><span class="sxs-lookup"><span data-stu-id="aab67-136">Overwrite Existing Files</span></span>

<span data-ttu-id="aab67-137">Ao instalar os pacotes que contêm arquivos que já existem no seu site da web, o NuGet ignorou silenciosamente sempre apenas desses arquivos (deixando apenas os arquivos existentes).</span><span class="sxs-lookup"><span data-stu-id="aab67-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="aab67-138">Isso pode levar a impressão de que um pacote foi instalado ou atualizado corretamente quando na verdade não era.</span><span class="sxs-lookup"><span data-stu-id="aab67-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="aab67-139">Agora, o NuGet solicitará para arquivos a serem substituídos.</span><span class="sxs-lookup"><span data-stu-id="aab67-139">NuGet will now prompt for files to be overwritten.</span></span>

![Resolução de conflitos de arquivo](./media/NuGet-2.8/webmatrix-overwrite-file.png)
