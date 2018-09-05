---
title: Notas de versão 1.3 do NuGet
description: Notas de versão para 1.3 de NuGet, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551345"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="61eb3-103">Notas de versão 1.3 do NuGet</span><span class="sxs-lookup"><span data-stu-id="61eb3-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="61eb3-104">[Notas de versão do NuGet 1.2](../release-notes/nuget-1.2.md) | [notas de versão do NuGet 1.4](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="61eb3-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="61eb3-105">1.3 do NuGet foi lançado em 25 de abril de 2011.</span><span class="sxs-lookup"><span data-stu-id="61eb3-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="61eb3-106">Novos recursos</span><span class="sxs-lookup"><span data-stu-id="61eb3-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="61eb3-107">Criação simplificada de pacote com a integração do servidor de símbolo</span><span class="sxs-lookup"><span data-stu-id="61eb3-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="61eb3-108">A equipe do NuGet em parceria com o pessoal [SymbolSource.org](http://www.symbolsource.org/) para oferecer uma maneira muito simple de publicação de suas fontes e do PDB junto com seu pacote.</span><span class="sxs-lookup"><span data-stu-id="61eb3-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="61eb3-109">Isso permite que os consumidores do seu pacote percorrer o código-fonte para o pacote no depurador.</span><span class="sxs-lookup"><span data-stu-id="61eb3-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="61eb3-110">Para obter mais detalhes, leia [criando e publicando um pacote de símbolos](../create-packages/symbol-packages.md) a forma mais fácil para publicar pacotes do NuGet com códigos-fonte.</span><span class="sxs-lookup"><span data-stu-id="61eb3-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="61eb3-111">Você também pode assistir uma demonstração ao vivo desse recurso como parte do NuGet em profundidade falar em Mix11.</span><span class="sxs-lookup"><span data-stu-id="61eb3-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="61eb3-112">Esse recurso totalmente é demonstrado começando na marca de 20 minutos do vídeo.</span><span class="sxs-lookup"><span data-stu-id="61eb3-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="61eb3-113">`Open-PackagePage` Comando</span><span class="sxs-lookup"><span data-stu-id="61eb3-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="61eb3-114">Este comando torna fácil chegar à página do projeto para um pacote de dentro do Console do Gerenciador de pacotes.</span><span class="sxs-lookup"><span data-stu-id="61eb3-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="61eb3-115">Ele também fornece opções para abrir a URL de licença e a página de abuso de relatório para o pacote.</span><span class="sxs-lookup"><span data-stu-id="61eb3-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="61eb3-116">A sintaxe do comando é:</span><span class="sxs-lookup"><span data-stu-id="61eb3-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="61eb3-117">O `-PassThru` opção é usada para retornar o valor da URL especificada.</span><span class="sxs-lookup"><span data-stu-id="61eb3-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="61eb3-118">Exemplos:</span><span class="sxs-lookup"><span data-stu-id="61eb3-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="61eb3-119">Abre um navegador para a URL de projeto especificada no pacote Ninject.</span><span class="sxs-lookup"><span data-stu-id="61eb3-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="61eb3-120">Abre um navegador para a URL de licença especificada no pacote Ninject.</span><span class="sxs-lookup"><span data-stu-id="61eb3-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="61eb3-121">Abre um navegador para a URL de origem do pacote atual usada para relatar abuso para o pacote especificado.</span><span class="sxs-lookup"><span data-stu-id="61eb3-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="61eb3-122">Atribui a URL de licença à variável, $url, sem abrir a URL em um navegador.</span><span class="sxs-lookup"><span data-stu-id="61eb3-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="61eb3-123">Melhorias de desempenho</span><span class="sxs-lookup"><span data-stu-id="61eb3-123">Performance Improvements</span></span>

<span data-ttu-id="61eb3-124">1.3 NuGet apresenta muitos dos aprimoramentos de desempenho.</span><span class="sxs-lookup"><span data-stu-id="61eb3-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="61eb3-125">1.3 NuGet evita o download a mesma versão de um pacote várias vezes com a inclusão de um cache local por usuário.</span><span class="sxs-lookup"><span data-stu-id="61eb3-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="61eb3-126">O cache pode ser acessado e desmarcado por meio da caixa de diálogo Configurações do Gerenciador de pacotes:</span><span class="sxs-lookup"><span data-stu-id="61eb3-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Caixa de diálogo de opções de NuGet com as configurações de Cache do pacote](./media/nuget-options.png)

<span data-ttu-id="61eb3-128">Outros aprimoramentos de desempenho incluem adicionar suporte à compactação HTTP e melhorar a velocidade de instalação do pacote dentro do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="61eb3-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="61eb3-129">O Visual Studio e nuget.exe usa a mesma lista de origens de pacote</span><span class="sxs-lookup"><span data-stu-id="61eb3-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="61eb3-130">Antes do NuGet 1.3, a lista de origens de pacote usado pelo nuget.exe e o NuGet Visual Studio Add-In não foram armazenados no mesmo local.</span><span class="sxs-lookup"><span data-stu-id="61eb3-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="61eb3-131">1.3 NuGet agora usa a mesma lista em ambos os locais.</span><span class="sxs-lookup"><span data-stu-id="61eb3-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="61eb3-132">A lista é armazenada em `NuGet.Config` e armazenados na pasta AppData.</span><span class="sxs-lookup"><span data-stu-id="61eb3-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="61eb3-133">NuGet.exe ignora arquivos e pastas que começam com '.' por padrão</span><span class="sxs-lookup"><span data-stu-id="61eb3-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="61eb3-134">Para fazer com que o NuGet funciona bem com sistemas de controle do código-fonte, como o Subversion e o Mercurial, nuget.exe ignora pastas e arquivos que começam com o '.' ao criar pacotes de caracteres.</span><span class="sxs-lookup"><span data-stu-id="61eb3-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="61eb3-135">Isso pode ser substituído usando dois sinalizadores novo:</span><span class="sxs-lookup"><span data-stu-id="61eb3-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="61eb3-136">__-NoDefaultExcludes__ é usado para substituir essa configuração e incluir todos os arquivos.</span><span class="sxs-lookup"><span data-stu-id="61eb3-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="61eb3-137">__-Excluir__ é usado para adicionar outros arquivos ou pastas a serem excluídos usando um padrão.</span><span class="sxs-lookup"><span data-stu-id="61eb3-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="61eb3-138">Por exemplo, para excluir todos os arquivos com a extensão de arquivo '. bak'</span><span class="sxs-lookup"><span data-stu-id="61eb3-138">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="61eb3-139">_Observação: o padrão não é recursiva por padrão._</span><span class="sxs-lookup"><span data-stu-id="61eb3-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="61eb3-140">Suporte para projetos WiX e o .NET Micro Framework</span><span class="sxs-lookup"><span data-stu-id="61eb3-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="61eb3-141">Graças a contribuições da comunidade, o NuGet inclui suporte para tipos de projeto do WiX, bem como o .NET Micro Framework.</span><span class="sxs-lookup"><span data-stu-id="61eb3-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="61eb3-142">Correções de Bug</span><span class="sxs-lookup"><span data-stu-id="61eb3-142">Bug Fixes</span></span>

<span data-ttu-id="61eb3-143">Para obter uma lista completa de correções de bugs, exibir o [rastreador de problemas do NuGet para esta versão](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="61eb3-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="61eb3-144">Correções de bugs, vale a pena observar</span><span class="sxs-lookup"><span data-stu-id="61eb3-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="61eb3-145">Pacotes com arquivos de origem funcionam em ambos os sites e em projetos de aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="61eb3-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="61eb3-146">Para sites, os arquivos de origem são copiados para o `App_Code` pasta</span><span class="sxs-lookup"><span data-stu-id="61eb3-146">For Websites, source files are copied into the `App_Code` folder</span></span>
