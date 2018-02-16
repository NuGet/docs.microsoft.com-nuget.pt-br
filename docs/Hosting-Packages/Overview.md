---
title: "Visão geral da hospedagem de seus próprios Feeds de NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Uma visão geral de aberturas para hospedar seus próprios feeds de pacote do NuGet ou galerias localmente ou remotamente."
keywords: Feed de NuGet, Galeria NuGet, feed de pacote de personalizado, NuGet.Server
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 738190e20603046d075faa3f50402601890583c1
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2018
---
# <a name="hosting-your-own-nuget-feeds"></a><span data-ttu-id="13fdb-104">Hospedando seus próprios feeds do NuGet</span><span class="sxs-lookup"><span data-stu-id="13fdb-104">Hosting your own NuGet feeds</span></span>

<span data-ttu-id="13fdb-105">Em vez de disponibilizar os pacotes publicamente, pode ser útil liberar pacotes apenas para um público limitado, como sua organização ou grupo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="13fdb-105">Instead of making packages publicly available, you might want to release packages to only a limited audience, such as your organization or workgroup.</span></span> <span data-ttu-id="13fdb-106">Além disso, algumas empresas podem querer restringir quais bibliotecas de terceiros seus desenvolvedores podem usar, portanto, direcionando os desenvolvedores para obterem pacotes de uma origem limitado em vez do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="13fdb-106">In addition, some companies may want to restrict which third-party libraries their developers may use, and thus direct those developers to draw from a limited package source rather than nuget.org.</span></span>

<span data-ttu-id="13fdb-107">Para todas as finalidades, o NuGet é compatível com a configuração de origens de pacotes privadas das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="13fdb-107">For all such purposes, NuGet supports setting up private package sources in the following ways:</span></span>

- <span data-ttu-id="13fdb-108">Feed local: pacotes são simplesmente colocados em um compartilhamento de arquivos de rede adequado, visto que o ideal seria usar `nuget init` e `nuget add` para criar uma estrutura hierárquica de pastas (NuGet 3.3 ou superior).</span><span class="sxs-lookup"><span data-stu-id="13fdb-108">Local feed: Packages are simply placed on a suitable network file share, ideally using `nuget init` and `nuget add` to create a hierarchical folder structure (NuGet 3.3+).</span></span> <span data-ttu-id="13fdb-109">Para obter detalhes, consulte [Feeds Local](../hosting-packages/local-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="13fdb-109">For details, see [Local Feeds](../hosting-packages/local-feeds.md).</span></span>
- <span data-ttu-id="13fdb-110">NuGet.Server: os pacotes são disponibilizados por meio de um servidor HTTP local.</span><span class="sxs-lookup"><span data-stu-id="13fdb-110">NuGet.Server: Packages are made available through a local HTTP server.</span></span> <span data-ttu-id="13fdb-111">Para ver mais detalhes, consulte [NuGet.Server](../hosting-packages/nuget-server.md).</span><span class="sxs-lookup"><span data-stu-id="13fdb-111">For details, see [NuGet.Server](../hosting-packages/nuget-server.md).</span></span>
- <span data-ttu-id="13fdb-112">Galeria do NuGet: os pacotes são hospedados em um servidor de Internet usando o [Projeto da Galeria do NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span><span class="sxs-lookup"><span data-stu-id="13fdb-112">NuGet Gallery: Packages are hosted on an Internet server using the [NuGet Gallery Project](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span></span> <span data-ttu-id="13fdb-113">A Galeria do NuGet fornece gerenciamento de usuários e recursos como uma interface do usuário extensiva da Web que permite pesquisar e explorar pacotes de dentro do navegador, semelhante ao nuget.org.</span><span class="sxs-lookup"><span data-stu-id="13fdb-113">NuGet Gallery provides user management and features such as an extensive web UI that allows searching and exploring packages from within the browser, similar to nuget.org.</span></span>

<span data-ttu-id="13fdb-114">Também há vários outros produtos de hospedagem de NuGet compatíveis com feeds privados remotos, incluindo:</span><span class="sxs-lookup"><span data-stu-id="13fdb-114">There are also several other NuGet hosting products that support remote private feeds, including the following:</span></span>

- <span data-ttu-id="13fdb-115">[Gerenciamento de Pacotes do Visual Studio Team Services](https://www.visualstudio.com/docs/package/nuget/publish), que também está disponível no Team Foundation Server 2017 e posterior.</span><span class="sxs-lookup"><span data-stu-id="13fdb-115">[Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), which is also available on Team Foundation Server 2017 and later.</span></span>
- [<span data-ttu-id="13fdb-116">MyGet</span><span class="sxs-lookup"><span data-stu-id="13fdb-116">MyGet</span></span>](http://myget.org)
- <span data-ttu-id="13fdb-117">[ProGet](http://inedo.com/proget) da Inedo</span><span class="sxs-lookup"><span data-stu-id="13fdb-117">[ProGet](http://inedo.com/proget) from Inedo</span></span>
- <span data-ttu-id="13fdb-118">[NuGet Server](http://nugetserver.net/), um projeto da comunidade do Inedo</span><span class="sxs-lookup"><span data-stu-id="13fdb-118">[NuGet Server](http://nugetserver.net/), a community project from Inedo</span></span>
- <span data-ttu-id="13fdb-119">[NuGet Server (Software Livre)](http://nuget-server.net), uma implementação de software livre semelhante ao NuGet Server da Inedo</span><span class="sxs-lookup"><span data-stu-id="13fdb-119">[NuGet Server (Open Source)](http://nuget-server.net), an open-source implementation similar to Inedo's NuGet Server</span></span>
- <span data-ttu-id="13fdb-120">[Artifactory](https://www.jfrog.com/artifactory/) da JFrog.</span><span class="sxs-lookup"><span data-stu-id="13fdb-120">[Artifactory](https://www.jfrog.com/artifactory/) from JFrog.</span></span>
- <span data-ttu-id="13fdb-121">[Nexus](http://www.sonatype.org/nexus/) da Sonatype.</span><span class="sxs-lookup"><span data-stu-id="13fdb-121">[Nexus](http://www.sonatype.org/nexus/) from Sonatype.</span></span>
- <span data-ttu-id="13fdb-122">[TeamCity](https://www.jetbrains.com/teamcity/) da JetBrains.</span><span class="sxs-lookup"><span data-stu-id="13fdb-122">[TeamCity](https://www.jetbrains.com/teamcity/) from JetBrains.</span></span>

<span data-ttu-id="13fdb-123">Independentemente de como os pacotes são hospedados, acesse-os adicionando-os à lista de origens disponíveis em `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="13fdb-123">Regardless of how packages are hosted, you access them by adding them to the list of available sources in `NuGet.Config`.</span></span> <span data-ttu-id="13fdb-124">Isso pode ser feito no Visual Studio, conforme descrito em [Origens de Pacote](../tools/package-manager-ui.md#package-sources) ou na linha de comando usando [`nuget sources`](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="13fdb-124">This can be done in Visual Studio as described in [Package Sources](../tools/package-manager-ui.md#package-sources), or from the command line using [`nuget sources`](../tools/cli-ref-sources.md).</span></span> <span data-ttu-id="13fdb-125">O caminho para uma origem pode ser um nome de caminho de pasta local, um nome de rede ou uma URL.</span><span class="sxs-lookup"><span data-stu-id="13fdb-125">The path to a source can be a local folder pathname, a network name, or a URL.</span></span>
