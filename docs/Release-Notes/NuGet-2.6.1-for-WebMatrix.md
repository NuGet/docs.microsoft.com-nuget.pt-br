---
title: NuGet 2.6.1 para notas de versão do WebMatrix
description: Notas de versão do NuGet 2.6.1 para o WebMatrix, incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3d767788d348553cbb5cb82c6f70aac1894628c3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="8c515-103">NuGet 2.6.1 para notas de versão do WebMatrix</span><span class="sxs-lookup"><span data-stu-id="8c515-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="8c515-104">[Notas de versão do NuGet 2.6](../release-notes/nuget-2.6.md) | [notas de versão do NuGet 2.7](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="8c515-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="8c515-105">A equipe do NuGet lançou uma extensão NuGet Package Manager atualizado para o WebMatrix em 26 de março de 2014.</span><span class="sxs-lookup"><span data-stu-id="8c515-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="8c515-106">Essa atualização pode ser instalada do [Galeria de extensões do WebMatrix](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) usando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8c515-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="8c515-107">Abrir o WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="8c515-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="8c515-108">Clique no ícone de extensões na faixa de opções página inicial</span><span class="sxs-lookup"><span data-stu-id="8c515-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="8c515-109">Selecione a guia atualizações</span><span class="sxs-lookup"><span data-stu-id="8c515-109">Select the Updates tab</span></span>
1. <span data-ttu-id="8c515-110">Clique para atualizar o NuGet Package Manager 2.6.1</span><span class="sxs-lookup"><span data-stu-id="8c515-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="8c515-111">Feche e reinicie o WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="8c515-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="8c515-112">Alterações importantes</span><span class="sxs-lookup"><span data-stu-id="8c515-112">Notable Changes</span></span>

<span data-ttu-id="8c515-113">Esta extensão atualização resolve dois dos maiores usuários problemas ter enfrentado consumo pacotes do NuGet do WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="8c515-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="8c515-114">O primeiro um erro de versão de esquema do NuGet e o segundo era um bug que levam a DLLs de zero bytes no `bin` pasta.</span><span class="sxs-lookup"><span data-stu-id="8c515-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="8c515-115">Erro de versão do esquema do NuGet</span><span class="sxs-lookup"><span data-stu-id="8c515-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="8c515-116">Desde o lançamento do WebMatrix 3, novos recursos foram introduzidos NuGet que exigem uma nova versão de esquema para os pacotes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="8c515-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="8c515-117">Ao tentar gerenciar seus pacotes do NuGet em seu site da web, esses novos pacotes podem levar a erros que você vê no WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="8c515-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Ocorreu um erro.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="8c515-121">Esta última versão fornece compatibilidade com os pacotes do NuGet mais recentes, impedindo que esse erro ocorra.</span><span class="sxs-lookup"><span data-stu-id="8c515-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="8c515-122">Novas versões de pacotes, inclusive Microsoft.AspNet.WebPages agora podem ser instaladas no WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="8c515-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="8c515-123">Alguns desses pacotes foram usando recursos do NuGet como [XDT config transforma](../release-notes/nuget-2.6.md#xdt), que não era suportado no WebMatrix até agora.</span><span class="sxs-lookup"><span data-stu-id="8c515-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="8c515-124">DLLs de zero bytes na pasta de compartimento</span><span class="sxs-lookup"><span data-stu-id="8c515-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="8c515-125">Alguns usuários relatou que depois de instalar o NuGet empacota no WebMatrix que incluem DLLs que podem ser copiadas para guardar, que mostram as DLLs no `bin` pasta arquivos de 0 byte.</span><span class="sxs-lookup"><span data-stu-id="8c515-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="8c515-126">Isso interrompe o aplicativo em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="8c515-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="8c515-127">[Esse problema](https://nuget.codeplex.com/workitem/4060) agora foram corrigidos.</span><span class="sxs-lookup"><span data-stu-id="8c515-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="8c515-128">Outros aperfeiçoamentos recentes</span><span class="sxs-lookup"><span data-stu-id="8c515-128">Other Recent Improvements</span></span>

<span data-ttu-id="8c515-129">Quando foi lançado 2.8 de Gerenciador de pacote do NuGet para Visual Studio, também lançamos NuGet Package Manager 2.5.0 para o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="8c515-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="8c515-130">Enquanto isso foi mencionado o [notas de versão do NuGet 2.8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), não mencionamos específico novos recursos que introduziu a atualização.</span><span class="sxs-lookup"><span data-stu-id="8c515-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="8c515-131">Atualizar tudo</span><span class="sxs-lookup"><span data-stu-id="8c515-131">Update All</span></span>

<span data-ttu-id="8c515-132">Agora você pode atualizar todos os pacotes do seu site em uma única etapa!</span><span class="sxs-lookup"><span data-stu-id="8c515-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="8c515-133">Quando você abre a extensão do NuGet no WebMatrix, você ver a lista de todos os pacotes em Galeria, estiverem instalados e as atualizações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="8c515-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="8c515-134">Anteriormente, cada pacote precisa ser atualizado individualmente, mas agora há um botão "Atualizar tudo" útil que aparece na guia atualizações.</span><span class="sxs-lookup"><span data-stu-id="8c515-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Clique em Atualizar tudo para atualizar todos os pacotes com atualizações disponíveis](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="8c515-136">Substituir arquivos existentes</span><span class="sxs-lookup"><span data-stu-id="8c515-136">Overwrite Existing Files</span></span>

<span data-ttu-id="8c515-137">Ao instalar os pacotes que contêm arquivos que já existem no seu site da web, NuGet sempre apenas silenciosamente ignorado esses arquivos (abandonando os arquivos existentes).</span><span class="sxs-lookup"><span data-stu-id="8c515-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="8c515-138">Isso poderia gerar a impressão de que um pacote foi instalado ou atualizado corretamente quando na verdade não era.</span><span class="sxs-lookup"><span data-stu-id="8c515-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="8c515-139">NuGet agora solicita arquivos a serem substituídos.</span><span class="sxs-lookup"><span data-stu-id="8c515-139">NuGet will now prompt for files to be overwritten.</span></span>

![Resolução de conflitos de arquivo](./media/NuGet-2.8/webmatrix-overwrite-file.png)
