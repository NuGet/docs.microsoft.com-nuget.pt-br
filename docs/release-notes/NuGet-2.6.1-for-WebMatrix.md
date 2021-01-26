---
title: Notas de versão do NuGet 2.6.1 para WebMatrix
description: Notas de versão do NuGet 2.6.1 para WebMatrix, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780419"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="aea6e-103">Notas de versão do NuGet 2.6.1 para WebMatrix</span><span class="sxs-lookup"><span data-stu-id="aea6e-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="aea6e-104">Notas de versão do [NuGet 2,6](../release-notes/nuget-2.6.md)  |  [Notas de versão do NuGet 2,7](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="aea6e-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="aea6e-105">A equipe do NuGet lançou uma extensão atualizada do Gerenciador de pacotes do NuGet para WebMatrix em 26 de março de 2014.</span><span class="sxs-lookup"><span data-stu-id="aea6e-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="aea6e-106">Essa atualização pode ser instalada a partir da [Galeria de extensões do WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) usando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="aea6e-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="aea6e-107">Abrir o WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="aea6e-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="aea6e-108">Clique no ícone extensões na faixa de faixas página inicial</span><span class="sxs-lookup"><span data-stu-id="aea6e-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="aea6e-109">Selecione a guia Atualizações</span><span class="sxs-lookup"><span data-stu-id="aea6e-109">Select the Updates tab</span></span>
1. <span data-ttu-id="aea6e-110">Clique para atualizar o Gerenciador de pacotes NuGet para 2.6.1</span><span class="sxs-lookup"><span data-stu-id="aea6e-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="aea6e-111">Fechar e reiniciar o WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="aea6e-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="aea6e-112">Alterações notáveis</span><span class="sxs-lookup"><span data-stu-id="aea6e-112">Notable Changes</span></span>

<span data-ttu-id="aea6e-113">Essa atualização de extensão aborda dois dos maiores problemas que os usuários enfrentam para consumir pacotes NuGet no WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="aea6e-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="aea6e-114">O primeiro era um erro de versão do esquema do NuGet e o segundo era um bug que levava a DLLs de zero byte na `bin` pasta.</span><span class="sxs-lookup"><span data-stu-id="aea6e-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="aea6e-115">Erro de versão do esquema do NuGet</span><span class="sxs-lookup"><span data-stu-id="aea6e-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="aea6e-116">Como o WebMatrix 3 foi lançado, novos recursos foram introduzidos no NuGet que exigem uma nova versão de esquema para os pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="aea6e-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="aea6e-117">Ao tentar gerenciar seus pacotes NuGet no seu site, esses novos pacotes podem levar a erros que você vê no WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="aea6e-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Ocorreu um erro.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="aea6e-121">Esta versão mais recente fornece compatibilidade com os pacotes NuGet mais recentes, impedindo que esse erro ocorra.</span><span class="sxs-lookup"><span data-stu-id="aea6e-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="aea6e-122">Novas versões de pacotes, incluindo Microsoft. AspNet. webpages, agora podem ser instaladas no WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="aea6e-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="aea6e-123">Alguns desses pacotes estavam usando recursos do NuGet, como [transformações de configuração xdt](../release-notes/nuget-2.6.md#xdt), que não tinha suporte no WebMatrix até agora.</span><span class="sxs-lookup"><span data-stu-id="aea6e-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="aea6e-124">Zero-Byte DLLs na pasta bin</span><span class="sxs-lookup"><span data-stu-id="aea6e-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="aea6e-125">Alguns usuários relataram que depois de instalar os pacotes NuGet no WebMatrix que incluem DLLs que são copiadas para o compartimento, que as DLLs aparecem na `bin` pasta como arquivos de 0 byte.</span><span class="sxs-lookup"><span data-stu-id="aea6e-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="aea6e-126">Isso interrompe o aplicativo em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="aea6e-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="aea6e-127">[Esse problema](https://nuget.codeplex.com/workitem/4060) agora foi corrigido.</span><span class="sxs-lookup"><span data-stu-id="aea6e-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="aea6e-128">Outros aprimoramentos recentes</span><span class="sxs-lookup"><span data-stu-id="aea6e-128">Other Recent Improvements</span></span>

<span data-ttu-id="aea6e-129">Quando o Gerenciador de pacotes NuGet 2,8 foi lançado para o Visual Studio, também lançamos o Gerenciador de pacotes NuGet 2.5.0 para WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="aea6e-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="aea6e-130">Embora isso tenha sido mencionado nas [notas de versão do NuGet 2,8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), não mencionamos os novos recursos específicos que a atualização introduziu.</span><span class="sxs-lookup"><span data-stu-id="aea6e-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="aea6e-131">Atualizar Tudo</span><span class="sxs-lookup"><span data-stu-id="aea6e-131">Update All</span></span>

<span data-ttu-id="aea6e-132">Agora você pode atualizar todos os pacotes de seu site em uma única etapa!</span><span class="sxs-lookup"><span data-stu-id="aea6e-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="aea6e-133">Quando você abre a extensão NuGet no WebMatrix, você vê a lista de todos os pacotes na Galeria, aqueles instalados e aqueles com atualizações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="aea6e-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="aea6e-134">Anteriormente, todo pacote teria que ser atualizado individualmente, mas agora há um botão "atualizar tudo" útil que aparece na guia Atualizações.</span><span class="sxs-lookup"><span data-stu-id="aea6e-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Clique em atualizar tudo para atualizar todos os pacotes com atualizações disponíveis](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="aea6e-136">Substituir arquivos existentes</span><span class="sxs-lookup"><span data-stu-id="aea6e-136">Overwrite Existing Files</span></span>

<span data-ttu-id="aea6e-137">Ao instalar pacotes que contêm arquivos que já existem no seu site, o NuGet sempre ignorou silenciosamente esses arquivos (deixando apenas os arquivos existentes).</span><span class="sxs-lookup"><span data-stu-id="aea6e-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="aea6e-138">Isso pode levar à impressão de que um pacote foi instalado ou atualizado corretamente quando, na verdade, não era.</span><span class="sxs-lookup"><span data-stu-id="aea6e-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="aea6e-139">Agora, o NuGet solicitará que os arquivos sejam substituídos.</span><span class="sxs-lookup"><span data-stu-id="aea6e-139">NuGet will now prompt for files to be overwritten.</span></span>

![Resolução de conflito de arquivo](./media/NuGet-2.8/webmatrix-overwrite-file.png)
