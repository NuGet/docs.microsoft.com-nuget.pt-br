---
title: Notas de versão do NuGet 3,1
description: Notas de versão do NuGet 3,1 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776534"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="436ea-103">Notas de versão do NuGet 3,1</span><span class="sxs-lookup"><span data-stu-id="436ea-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="436ea-104">Notas de versão do [NuGet 3,0](../release-notes/nuget-3.0.0.md)  |  [Notas de versão do NuGet 3.1.1](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="436ea-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="436ea-105">O NuGet 3,1 foi lançado em 27 de julho de 2015 como uma extensão agrupada para o SDK do Plataforma Universal do Windows para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="436ea-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="436ea-106">Fornecemos esta versão com o SDK da plataforma Windows para que a experiência de desenvolvimento do Windows pudesse aproveitar o trabalho de plataforma cruzada do NuGet que foi iniciado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="436ea-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="436ea-107">Esta versão de extensão NuGet só está disponível para o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="436ea-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="436ea-108">Recomendamos que esses desenvolvedores tenham acesso à atualização da galeria do Visual Studio para a versão mais recente disponível, pois estamos sempre publicando atualizações com correções de bugs e novos recursos.</span><span class="sxs-lookup"><span data-stu-id="436ea-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="436ea-109">Extensão do NuGet do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="436ea-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="436ea-110">Os problemas e os recursos desta versão são marcados no GitHub com a [etapa "suporte transitivo do UWP da 3,1 RTM"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  no total, fechamos 67 problemas na versão 3,1.</span><span class="sxs-lookup"><span data-stu-id="436ea-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="436ea-111">Novos recursos</span><span class="sxs-lookup"><span data-stu-id="436ea-111">New Features</span></span>

* <span data-ttu-id="436ea-112">`project.json` suporte para o Windows UWP e suporte a ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="436ea-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="436ea-113">Instalação de pacote transitiva</span><span class="sxs-lookup"><span data-stu-id="436ea-113">Transitive package installation</span></span>

<span data-ttu-id="436ea-114">A descrição e a definição desses recursos podem ser encontradas em outro lugar na documentação.</span><span class="sxs-lookup"><span data-stu-id="436ea-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="436ea-115">Preterido</span><span class="sxs-lookup"><span data-stu-id="436ea-115">Deprecated</span></span>

<span data-ttu-id="436ea-116">Os seguintes recursos não estão mais disponíveis para o Visual Studio 2015:</span><span class="sxs-lookup"><span data-stu-id="436ea-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="436ea-117">Pacotes de nível de solução não podem mais ser instalados</span><span class="sxs-lookup"><span data-stu-id="436ea-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="436ea-118">Os recursos a seguir não estão mais disponíveis para o Visual Studio 2015 e projetos que usam a `project.json` especificação</span><span class="sxs-lookup"><span data-stu-id="436ea-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="436ea-119">`install.ps1` e `uninstall.ps1` -esses scripts serão ignorados durante a instalação, restauração, atualização e desinstalação do pacote</span><span class="sxs-lookup"><span data-stu-id="436ea-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="436ea-120">As transformações de configuração serão ignoradas</span><span class="sxs-lookup"><span data-stu-id="436ea-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="436ea-121">O conteúdo será transportado, mas não copiado em um projeto.</span><span class="sxs-lookup"><span data-stu-id="436ea-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="436ea-122">A equipe está trabalhando para implementar esse recurso novamente, siga a discussão e o progresso em: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="436ea-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="436ea-123">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="436ea-123">Known Issues</span></span>

<span data-ttu-id="436ea-124">Houve uma série de problemas conhecidos fornecidos com esta versão.</span><span class="sxs-lookup"><span data-stu-id="436ea-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="436ea-125">A instalação da versão 3,1 com o SDK do Windows 10 fará o downgrade de qualquer versão da extensão do NuGet que foi instalada anteriormente</span><span class="sxs-lookup"><span data-stu-id="436ea-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="436ea-126">Linha de comando do NuGet</span><span class="sxs-lookup"><span data-stu-id="436ea-126">NuGet Command-line</span></span>

<span data-ttu-id="436ea-127">O executável de linha de comando do NuGet foi atualizado e movido para um novo local de distribuição para que as versões históricas do nuget.exe possam continuar a ser disponibilizadas.</span><span class="sxs-lookup"><span data-stu-id="436ea-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="436ea-128">Você pode baixar a versão beta 3,1 do nuget.exe para Windows em: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="436ea-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="436ea-129">O novo local distribuível reside no host dist.nuget.org, com uma estrutura de pastas que segue este modelo:</span><span class="sxs-lookup"><span data-stu-id="436ea-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a><span data-ttu-id="436ea-130">Novos recursos</span><span class="sxs-lookup"><span data-stu-id="436ea-130">New Features</span></span>

* <span data-ttu-id="436ea-131">nuget.exe pode restaurar e instalar pacotes em projetos que usam um `project.json` arquivo.</span><span class="sxs-lookup"><span data-stu-id="436ea-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="436ea-132">nuget.exe pode se conectar e consumir o protocolo NuGet v3 em: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="436ea-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="436ea-133">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="436ea-133">Known Issues</span></span> ##

1.    <span data-ttu-id="436ea-134">Não é possível executar o pacote em um `project.json` arquivo- [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="436ea-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="436ea-135">Não tem suporte no mono- [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="436ea-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="436ea-136">Não localizado- [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="436ea-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="436ea-137">Não é assinado, assim como o existente http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="436ea-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
