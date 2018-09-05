---
title: Notas de versão 3.3 do NuGet
description: Notas de versão do NuGet 3.3, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546641"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="7fcd0-103">Notas de versão 3.3 do NuGet</span><span class="sxs-lookup"><span data-stu-id="7fcd0-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="7fcd0-104">[Notas de versão do NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [notas de versão do RC 3.4 do NuGet](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="7fcd0-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="7fcd0-105">O NuGet 3.3 foi lançado o dia 30 de novembro de 2015, com um número significativo de atualizações de interface do usuário e recursos de linha de comando, bem como uma coleção de correções úteis para os clientes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="7fcd0-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="7fcd0-106">Novos recursos</span><span class="sxs-lookup"><span data-stu-id="7fcd0-106">New Features</span></span>

* <span data-ttu-id="7fcd0-107">Foram introduzidos os provedores de credenciais que permitem que os clientes de linha de comando do NuGet ser capaz de trabalhar perfeitamente com um feed autenticado.</span><span class="sxs-lookup"><span data-stu-id="7fcd0-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="7fcd0-108">[Provedor de credenciais de instruções sobre como instalar o Visual Studio Team Services ](../api/nuget-exe-credential-providers.md) e configurar o NuGet para usá-lo, os clientes estão disponíveis no NuGet Docs.</span><span class="sxs-lookup"><span data-stu-id="7fcd0-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="7fcd0-109">Novos recursos de Interface do usuário</span><span class="sxs-lookup"><span data-stu-id="7fcd0-109">New User Interface Features</span></span>

* <span data-ttu-id="7fcd0-110">Guias separadas de procurar, instalado e as atualizações disponíveis</span><span class="sxs-lookup"><span data-stu-id="7fcd0-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="7fcd0-111">Atualizações disponível selo que indica o número de pacotes com atualizações disponíveis</span><span class="sxs-lookup"><span data-stu-id="7fcd0-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="7fcd0-112">Notificações de pacote na lista de pacotes para indicar se o pacote está instalado ou tem uma atualização disponível</span><span class="sxs-lookup"><span data-stu-id="7fcd0-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="7fcd0-113">Baixe a contagem e autor adicionado à lista de pacotes</span><span class="sxs-lookup"><span data-stu-id="7fcd0-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="7fcd0-114">Maior número de versão disponíveis e o número de versão instalada atualmente na lista de pacotes</span><span class="sxs-lookup"><span data-stu-id="7fcd0-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="7fcd0-115">Botões de ação para permitir a instalação rápida, atualizar e desinstalar da lista de pacotes</span><span class="sxs-lookup"><span data-stu-id="7fcd0-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="7fcd0-116">Botões de ação mais claros sobre o painel de detalhes do pacote</span><span class="sxs-lookup"><span data-stu-id="7fcd0-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="7fcd0-117">Data de atualização de pacote no painel de detalhes do pacote</span><span class="sxs-lookup"><span data-stu-id="7fcd0-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="7fcd0-118">Consolidar o painel no modo de exibição de solução</span><span class="sxs-lookup"><span data-stu-id="7fcd0-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="7fcd0-119">Grade classificável de projetos e os números da versão instalada no modo de exibição de solução</span><span class="sxs-lookup"><span data-stu-id="7fcd0-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="7fcd0-120">Novos recursos de linha de comando</span><span class="sxs-lookup"><span data-stu-id="7fcd0-120">New Command-line Features</span></span>

<span data-ttu-id="7fcd0-121">Nesta versão, apresentamos os `add` e `init` comandos para inicializar repositórios baseados em pastas, conforme descrito a [nuget.exe referência](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="7fcd0-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="7fcd0-122">Estrutura de repositórios que são construídos e mantidos com nessa pasta serão [fornecer benefícios significativos de desempenho](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) conforme descrito em nosso blog.</span><span class="sxs-lookup"><span data-stu-id="7fcd0-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="7fcd0-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="7fcd0-123">ContentFiles</span></span>

<span data-ttu-id="7fcd0-124">Agora há suporte para o conteúdo no `project.json` projetos por meio do novo gerenciados `contentFiles` pasta e `.nuspec` `contentFiles` notação do elemento.</span><span class="sxs-lookup"><span data-stu-id="7fcd0-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="7fcd0-125">Esse conteúdo pode ser especificado mais diretamente pelo autor do pacote para interações com os sistemas de projeto.</span><span class="sxs-lookup"><span data-stu-id="7fcd0-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="7fcd0-126">Para obter mais informações sobre como configurar contentFiles em uma `.nuspec` documento pode ser encontrado na [. NuSpec referência](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="7fcd0-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="7fcd0-127">Gerenciamento de Cache do NuGet Locals</span><span class="sxs-lookup"><span data-stu-id="7fcd0-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="7fcd0-128">O linha de comando do NuGet foi atualizado para incluir informações sobre como gerenciar os caches locais em uma estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7fcd0-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="7fcd0-129">Para obter mais informações sobre o comando locals estão disponíveis na [referência de linha de comando do NuGet](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="7fcd0-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="7fcd0-130">Problemas corrigidos</span><span class="sxs-lookup"><span data-stu-id="7fcd0-130">Fixed Issues</span></span>

<span data-ttu-id="7fcd0-131">**Problemas importantes**</span><span class="sxs-lookup"><span data-stu-id="7fcd0-131">**Notable Issues**</span></span>

* <span data-ttu-id="7fcd0-132">Suporte restaurado de linha de comando do NuGet para a restauração de pacotes com um arquivo de solução no Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="7fcd0-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="7fcd0-133">A lista completa de problemas que foram abordados na versão 3.3 pode ser encontrada no GitHub sob o [etapa 3.3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="7fcd0-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="7fcd0-134">A lista de problemas corrigidos na versão de linha de comando 3.3 são registradas na [3.3 marco de linha de comando](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="7fcd0-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="7fcd0-135">Problemas Conhecidos</span><span class="sxs-lookup"><span data-stu-id="7fcd0-135">Known Issues</span></span>

<span data-ttu-id="7fcd0-136">Continuamos a acompanhar os problemas em nossa lista de problemas do GitHub que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="7fcd0-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>