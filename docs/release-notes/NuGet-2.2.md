---
title: Notas de versão 2.2 do NuGet
description: Notas de versão para 2.2 de NuGet, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545986"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="f875b-103">Notas de versão 2.2 do NuGet</span><span class="sxs-lookup"><span data-stu-id="f875b-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="f875b-104">[Notas de versão do NuGet 2.1](../release-notes/nuget-2.1.md) | [notas de versão do NuGet 2.2.1](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="f875b-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="f875b-105">NuGet 2.2 foi lançado em 12 de dezembro de 2012.</span><span class="sxs-lookup"><span data-stu-id="f875b-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="f875b-106">Início rápido do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f875b-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="f875b-107">Um dos novos recursos que foi adicionado no Visual Studio 2012 foi a [caixa de diálogo de início rápido](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="f875b-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="f875b-108">2.2 NuGet estende essa caixa de diálogo, permitindo que ele inicializar a caixa de diálogo do Gerenciador de pacote com os termos de pesquisa inseridos no início rápido.</span><span class="sxs-lookup"><span data-stu-id="f875b-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="f875b-109">Por exemplo, inserir 'jquery' no início rápido agora inclui uma opção nos resultados para pesquisar pacotes do NuGet 'jquery' de correspondência.</span><span class="sxs-lookup"><span data-stu-id="f875b-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![NuGet no início rápido do Visual Studio](./media/quick-launch.png)

<span data-ttu-id="f875b-111">Selecionar esta opção iniciará a standard NuGet pacote manager experiência de pesquisa para o termo 'jquery'.</span><span class="sxs-lookup"><span data-stu-id="f875b-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Caixa de diálogo de Gerenciador de pacotes NuGet previamente preenchido](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="f875b-113">Especifique a pasta inteira para o conteúdo do pacote</span><span class="sxs-lookup"><span data-stu-id="f875b-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="f875b-114">2.2 NuGet agora permite que você especifique uma pasta inteira na `<file>` elemento do `.nuspec` arquivo para incluir todo o conteúdo dessa pasta.</span><span class="sxs-lookup"><span data-stu-id="f875b-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="f875b-115">Por exemplo, a seguir fará com que todos os scripts na pasta de scripts do pacote a ser adicionado à pasta contents\scripts quando o pacote é instalado em um projeto.</span><span class="sxs-lookup"><span data-stu-id="f875b-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="f875b-116">**Atualizar 6/24/16: pastas vazias na pasta "content" são ignoradas quando a instalação do pacote.**</span><span class="sxs-lookup"><span data-stu-id="f875b-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="f875b-117">Problemas Conhecidos</span><span class="sxs-lookup"><span data-stu-id="f875b-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="f875b-118">Falha da instalação do pacote para projetos do F # ao usar o console do Gerenciador de pacotes</span><span class="sxs-lookup"><span data-stu-id="f875b-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="f875b-119">Ao tentar instalar um pacote do NuGet em um projeto do F # usando o console do Gerenciador de pacotes, será gerada uma InvalidOperationException.</span><span class="sxs-lookup"><span data-stu-id="f875b-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="f875b-120">Estamos trabalhando ativamente com a equipe do F # para resolver o problema, mas por enquanto, a solução alternativa é instalar os pacotes NuGet em projetos do F # por meio da caixa de diálogo de Gerenciador de pacote do NuGet em vez do console.</span><span class="sxs-lookup"><span data-stu-id="f875b-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="f875b-121">[Mais informações estão disponíveis no CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="f875b-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="f875b-122">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="f875b-122">Bug Fixes</span></span>
<span data-ttu-id="f875b-123">NuGet 2.2 inclui muitas correções de bugs.</span><span class="sxs-lookup"><span data-stu-id="f875b-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="f875b-124">Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.2, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="f875b-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
