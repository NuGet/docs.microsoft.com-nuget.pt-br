---
title: Notas de versão 3.1 do NuGet
description: Notas de versão do NuGet 3.1 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d14455da6f8af4db92f7105ea1b0e88eb9e71600
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820854"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="2b976-103">Notas de versão 3.1 do NuGet</span><span class="sxs-lookup"><span data-stu-id="2b976-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="2b976-104">[Notas de versão do NuGet 3.0](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 notas de versão](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="2b976-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="2b976-105">3.1 NuGet foi lançado em 27 de julho de 2015 como uma extensão de pacote para o SDK de plataforma Universal do Windows para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="2b976-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="2b976-106">Fornecemos desta versão com o SDK de plataforma do Windows para que a experiência de desenvolvimento do Windows pode aproveitar o trabalho de plataforma cruzada do NuGet ter sido iniciado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2b976-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="2b976-107">Esta versão da extensão NuGet só está disponível para o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="2b976-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="2b976-108">Recomendamos que os desenvolvedores que têm acesso a atualização da Galeria do Visual Studio para a versão mais recente está disponível, como estamos sempre publicando atualizações com novos recursos e correções de bugs.</span><span class="sxs-lookup"><span data-stu-id="2b976-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="2b976-109">Extensão do NuGet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2b976-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="2b976-110">Problemas e recursos nesta versão são marcados no GitHub, com o ["3.1 suporte transitiva UWP RTM" Marco](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) no total, é fechada 67 problemas na versão 3.1.</span><span class="sxs-lookup"><span data-stu-id="2b976-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="2b976-111">Novos recursos</span><span class="sxs-lookup"><span data-stu-id="2b976-111">New Features</span></span>

* <span data-ttu-id="2b976-112">`project.json` suporte para suporte de UWP do Windows e do ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="2b976-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="2b976-113">Instalação do pacote transitiva</span><span class="sxs-lookup"><span data-stu-id="2b976-113">Transitive package installation</span></span>

<span data-ttu-id="2b976-114">Descrição e a definição desses recursos podem ser encontrados em outro lugar na documentação.</span><span class="sxs-lookup"><span data-stu-id="2b976-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="2b976-115">Preterido</span><span class="sxs-lookup"><span data-stu-id="2b976-115">Deprecated</span></span>

<span data-ttu-id="2b976-116">Os recursos a seguir não estão mais disponíveis para o Visual Studio 2015:</span><span class="sxs-lookup"><span data-stu-id="2b976-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="2b976-117">Pacotes de nível de solução não podem mais ser instalados</span><span class="sxs-lookup"><span data-stu-id="2b976-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="2b976-118">Os recursos a seguir não estão mais disponíveis para o Visual Studio 2015 e projetos que usam o `project.json` especificação</span><span class="sxs-lookup"><span data-stu-id="2b976-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="2b976-119">`install.ps1` e `uninstall.ps1` -esses scripts serão ignorados durante a instalação do pacote, restaurar, atualizar e desinstalar</span><span class="sxs-lookup"><span data-stu-id="2b976-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="2b976-120">Transformações de configuração serão ignoradas</span><span class="sxs-lookup"><span data-stu-id="2b976-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="2b976-121">Conteúdo será executado, mas não foi copiado em um projeto.</span><span class="sxs-lookup"><span data-stu-id="2b976-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="2b976-122">A equipe está trabalhando para implementar novamente esse recurso, siga a discussão e andamento em: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="2b976-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="2b976-123">Problemas Conhecidos</span><span class="sxs-lookup"><span data-stu-id="2b976-123">Known Issues</span></span>

<span data-ttu-id="2b976-124">Houve um número de problemas conhecidos, fornecido com esta versão.</span><span class="sxs-lookup"><span data-stu-id="2b976-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="2b976-125">Instalação da versão 3.1 com o SDK do Windows 10 desatualizará qualquer versão da extensão do NuGet instalada anteriormente</span><span class="sxs-lookup"><span data-stu-id="2b976-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="2b976-126">Linha de comando do NuGet</span><span class="sxs-lookup"><span data-stu-id="2b976-126">NuGet Command-line</span></span>

<span data-ttu-id="2b976-127">O executável de linha de comando do NuGet foi atualizado e movido para um novo local de distribuição para que as versões históricas de nuget.exe podem continuar a ser disponibilizado.</span><span class="sxs-lookup"><span data-stu-id="2b976-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="2b976-128">Você pode baixar a versão 3.1 beta do nuget.exe Windows em: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="2b976-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="2b976-129">O novo local distribuível reside no host dist.nuget.org, com uma estrutura de pastas que segue este modelo:</span><span class="sxs-lookup"><span data-stu-id="2b976-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="2b976-130">Novos recursos</span><span class="sxs-lookup"><span data-stu-id="2b976-130">New Features</span></span>

* <span data-ttu-id="2b976-131">NuGet.exe pode restaurar e instalar pacotes em projetos que usam um `project.json` arquivo.</span><span class="sxs-lookup"><span data-stu-id="2b976-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="2b976-132">NuGet.exe pode se conectar e consumir o protocolo de v3 do NuGet em: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="2b976-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="2b976-133">Problemas Conhecidos</span><span class="sxs-lookup"><span data-stu-id="2b976-133">Known Issues</span></span> ##

1.    <span data-ttu-id="2b976-134">Não é possível executar o pacote em relação a um `project.json` arquivo - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="2b976-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="2b976-135">Não há suporte para Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="2b976-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="2b976-136">Não é localizado - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="2b976-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="2b976-137">Não é assinado, assim como existente http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="2b976-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
