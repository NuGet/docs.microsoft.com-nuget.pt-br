---
title: "Notas de versão do NuGet 2.2 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 25389d8c-e7db-4920-ab5e-cff20cebee7e
description: "Notas de versão do NuGet 2.2 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão 2.2 do NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1f6080e01777431c4dfb2278db167bd3bc9a67ea
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="2c72d-104">Notas de versão 2.2 do NuGet</span><span class="sxs-lookup"><span data-stu-id="2c72d-104">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="2c72d-105">[Notas de versão do NuGet 2.1](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 notas de versão](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="2c72d-105">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="2c72d-106">NuGet 2.2 foi lançado em 12 de dezembro de 2012.</span><span class="sxs-lookup"><span data-stu-id="2c72d-106">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="2c72d-107">Início rápido do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2c72d-107">Visual Studio Quick Launch</span></span>
<span data-ttu-id="2c72d-108">Um dos novos recursos que foi adicionado no Visual Studio 2012 foi o [caixa de diálogo de início rápido](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="2c72d-108">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="2c72d-109">2.2 NuGet estende essa caixa de diálogo que lhe permite inicializar a caixa de diálogo de Gerenciador de pacote com os termos de pesquisa inseridos no início rápido.</span><span class="sxs-lookup"><span data-stu-id="2c72d-109">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="2c72d-110">Por exemplo, inserir 'jquery' no início rápido agora inclui uma opção nos resultados para pesquisar pacotes do NuGet correspondência 'jquery'.</span><span class="sxs-lookup"><span data-stu-id="2c72d-110">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![NuGet em início rápido do Visual Studio](./media/quick-launch.png)

<span data-ttu-id="2c72d-112">Esta opção iniciará a padrão NuGet pacote manager experiência de pesquisa para o termo 'jquery'.</span><span class="sxs-lookup"><span data-stu-id="2c72d-112">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Caixa de diálogo preenchido previamente o NuGet Package Manager](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="2c72d-114">Especifique a pasta inteira para o conteúdo do pacote</span><span class="sxs-lookup"><span data-stu-id="2c72d-114">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="2c72d-115">2.2 NuGet agora permite que você especifique uma pasta inteira no `<file>` elemento o `.nuspec` arquivo para incluir todo o conteúdo dessa pasta.</span><span class="sxs-lookup"><span data-stu-id="2c72d-115">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="2c72d-116">Por exemplo, a seguir fará com que todos os scripts na pasta de scripts do pacote a ser adicionado à pasta contents\scripts quando o pacote for instalado em um projeto.</span><span class="sxs-lookup"><span data-stu-id="2c72d-116">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="2c72d-117">**Atualizar 24/6/16: pastas vazias na pasta "conteúdo" serão ignoradas durante a instalação do pacote.**</span><span class="sxs-lookup"><span data-stu-id="2c72d-117">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="2c72d-118">Problemas Conhecidos</span><span class="sxs-lookup"><span data-stu-id="2c72d-118">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="2c72d-119">Falha da instalação do pacote para projetos F # ao usar o console do Gerenciador de pacote</span><span class="sxs-lookup"><span data-stu-id="2c72d-119">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="2c72d-120">Ao tentar instalar um pacote do NuGet para um projeto do F # usando o console do Gerenciador de pacote, um InvalidOperationException é gerado.</span><span class="sxs-lookup"><span data-stu-id="2c72d-120">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="2c72d-121">Estamos trabalhando ativamente com a equipe do F # para resolver o problema, mas por enquanto, a solução alternativa é instalar os pacotes do NuGet em F # projetos por meio da caixa de diálogo de Gerenciador de pacote do NuGet em vez do console.</span><span class="sxs-lookup"><span data-stu-id="2c72d-121">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="2c72d-122">[Mais informações estão disponíveis no CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="2c72d-122">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="2c72d-123">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="2c72d-123">Bug Fixes</span></span>
<span data-ttu-id="2c72d-124">NuGet 2.2 inclui muitas correções de bugs.</span><span class="sxs-lookup"><span data-stu-id="2c72d-124">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="2c72d-125">Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.2, por favor, exibição de [NuGet Issue Tracker para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="2c72d-125">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
