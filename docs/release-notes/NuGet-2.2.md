---
title: Notas de versão do NuGet 2,2
description: Notas de versão do NuGet 2,2 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780433"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="30873-103">Notas de versão do NuGet 2,2</span><span class="sxs-lookup"><span data-stu-id="30873-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="30873-104">Notas de versão do [NuGet 2,1](../release-notes/nuget-2.1.md)  |  [Notas de versão do NuGet 2.2.1](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="30873-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="30873-105">O NuGet 2,2 foi lançado em 12 de dezembro de 2012.</span><span class="sxs-lookup"><span data-stu-id="30873-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="30873-106">Início rápido do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="30873-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="30873-107">Um dos novos recursos que foi adicionado no Visual Studio 2012 foi a [caixa de diálogo início rápido](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="30873-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="30873-108">O NuGet 2,2 estende essa caixa de diálogo, permitindo que ela inicialize a caixa de diálogo do Gerenciador de pacotes com os termos de pesquisa inseridos no início rápido.</span><span class="sxs-lookup"><span data-stu-id="30873-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="30873-109">Por exemplo, inserir "jQuery" no início rápido agora inclui uma opção nos resultados para pesquisar os pacotes NuGet que correspondem a "jQuery".</span><span class="sxs-lookup"><span data-stu-id="30873-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![Início rápido do NuGet no Visual Studio](./media/quick-launch.png)

<span data-ttu-id="30873-111">A seleção dessa opção iniciará a experiência de pesquisa padrão do Gerenciador de pacotes do NuGet para o termo ' jQuery '.</span><span class="sxs-lookup"><span data-stu-id="30873-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Caixa de diálogo do Gerenciador de pacotes do NuGet preenchida previamente](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="30873-113">Especificar a pasta inteira para o conteúdo do pacote</span><span class="sxs-lookup"><span data-stu-id="30873-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="30873-114">O NuGet 2,2 agora permite que você especifique uma pasta inteira no `<file>` elemento do `.nuspec` arquivo para incluir todo o conteúdo dessa pasta.</span><span class="sxs-lookup"><span data-stu-id="30873-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="30873-115">Por exemplo, o seguinte fará com que todos os scripts na pasta de scripts do pacote sejam adicionados à pasta contents\scripts quando o pacote for instalado em um projeto.</span><span class="sxs-lookup"><span data-stu-id="30873-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="30873-116">**Atualização 6/24/16: as pastas vazias na pasta "conteúdo" são ignoradas durante a instalação do pacote.**</span><span class="sxs-lookup"><span data-stu-id="30873-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="30873-117">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="30873-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="30873-118">Falha na instalação do pacote para projetos F # ao usar o console do Gerenciador de pacotes</span><span class="sxs-lookup"><span data-stu-id="30873-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="30873-119">Ao tentar instalar um pacote NuGet em um projeto F # usando o console do Gerenciador de pacotes, um InvalidOperationException é gerado.</span><span class="sxs-lookup"><span data-stu-id="30873-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="30873-120">Estamos trabalhando ativamente com a equipe do F # para resolver o problema, mas enquanto isso, a solução alternativa é instalar pacotes NuGet em projetos F # por meio da caixa de diálogo Gerenciador de pacotes do NuGet, em vez do console.</span><span class="sxs-lookup"><span data-stu-id="30873-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="30873-121">[Mais informações estão disponíveis no CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="30873-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="30873-122">Correções de bugs</span><span class="sxs-lookup"><span data-stu-id="30873-122">Bug Fixes</span></span>
<span data-ttu-id="30873-123">O NuGet 2,2 inclui muitas correções de bugs.</span><span class="sxs-lookup"><span data-stu-id="30873-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="30873-124">Para obter uma lista completa de itens de trabalho corrigidos no NuGet 2,2, consulte o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="30873-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
