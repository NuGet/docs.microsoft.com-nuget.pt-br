---
title: Notas de versão 3.3 do NuGet
description: Notas de versão do NuGet 3.3 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: adf193437de237ed32da481e627552a8dba6f656
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821558"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="e42ed-103">Notas de versão 3.3 do NuGet</span><span class="sxs-lookup"><span data-stu-id="e42ed-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="e42ed-104">[Notas de versão do NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC notas](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="e42ed-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="e42ed-105">3.3 NuGet foi liberado 30 de novembro de 2015, com um número significativo de atualizações de interface do usuário e recursos de linha de comando, bem como um conjunto de correções úteis para os clientes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="e42ed-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="e42ed-106">Novos recursos</span><span class="sxs-lookup"><span data-stu-id="e42ed-106">New Features</span></span>

* <span data-ttu-id="e42ed-107">Foram introduzidos provedores de credenciais que permitem que os clientes de linha de comando do NuGet poder funcionar perfeitamente com um feed autenticado.</span><span class="sxs-lookup"><span data-stu-id="e42ed-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="e42ed-108">[Provedor de credenciais de instruções sobre como instalar o Visual Studio Team Services ](../api/nuget-exe-credential-providers.md) e configurar o NuGet clientes para usá-lo estão disponíveis em documentos do NuGet.</span><span class="sxs-lookup"><span data-stu-id="e42ed-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="e42ed-109">Novos recursos de Interface do usuário</span><span class="sxs-lookup"><span data-stu-id="e42ed-109">New User Interface Features</span></span>

* <span data-ttu-id="e42ed-110">Guias separadas de procurar, instalar e atualizações disponíveis</span><span class="sxs-lookup"><span data-stu-id="e42ed-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="e42ed-111">Atualizações de notificação disponível que indica o número de pacotes com atualizações disponíveis</span><span class="sxs-lookup"><span data-stu-id="e42ed-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="e42ed-112">Notificações de pacote na lista de pacotes para indicar se o pacote está instalado, ou uma atualização disponível</span><span class="sxs-lookup"><span data-stu-id="e42ed-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="e42ed-113">Baixar a contagem e adicionado à lista de pacotes de autor</span><span class="sxs-lookup"><span data-stu-id="e42ed-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="e42ed-114">Maior número de versão disponíveis e o número de versão instalada atualmente na lista de pacotes</span><span class="sxs-lookup"><span data-stu-id="e42ed-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="e42ed-115">Botões de ação para permitir a rápida instalar, atualizar e desinstalar da lista de pacotes</span><span class="sxs-lookup"><span data-stu-id="e42ed-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="e42ed-116">Botões de ação mais claros no painel de detalhes do pacote</span><span class="sxs-lookup"><span data-stu-id="e42ed-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="e42ed-117">Data de atualização de pacote no painel de detalhes do pacote</span><span class="sxs-lookup"><span data-stu-id="e42ed-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="e42ed-118">Consolidar o painel no modo de exibição de solução</span><span class="sxs-lookup"><span data-stu-id="e42ed-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="e42ed-119">Grade classificável de projetos e os números de versão instalada no modo de exibição de solução</span><span class="sxs-lookup"><span data-stu-id="e42ed-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="e42ed-120">Novos recursos de linha de comando</span><span class="sxs-lookup"><span data-stu-id="e42ed-120">New Command-line Features</span></span>

<span data-ttu-id="e42ed-121">Nesta versão, apresentamos o `add` e `init` comandos para inicializar com base em pasta repositórios conforme descrito no [nuget.exe referência](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="e42ed-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="e42ed-122">Estrutura de repositórios que são construídos e mantidos com esta pasta será [fornecer benefícios significativos de desempenho](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) conforme descrito em nosso blog.</span><span class="sxs-lookup"><span data-stu-id="e42ed-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="e42ed-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="e42ed-123">ContentFiles</span></span>

<span data-ttu-id="e42ed-124">Agora há suporte para o conteúdo em `project.json` gerenciados projetos por meio do novo `contentFiles` pasta e `.nuspec` `contentFiles` notação de elemento.</span><span class="sxs-lookup"><span data-stu-id="e42ed-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="e42ed-125">Esse conteúdo pode ser especificado mais diretamente pelo autor do pacote para interações com sistemas de projeto.</span><span class="sxs-lookup"><span data-stu-id="e42ed-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="e42ed-126">Para obter mais informações sobre como configurar contentFiles em uma `.nuspec` documento pode ser encontrado na [. NuSpec referência](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="e42ed-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="e42ed-127">Gerenciamento de Cache do NuGet locais</span><span class="sxs-lookup"><span data-stu-id="e42ed-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="e42ed-128">O linha de comando do NuGet foi atualizado para incluir informações sobre como gerenciar os caches locais em uma estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e42ed-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="e42ed-129">Para obter mais informações sobre o comando locais estão disponíveis na [referência de linha de comando do NuGet](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="e42ed-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="e42ed-130">Problemas corrigidos</span><span class="sxs-lookup"><span data-stu-id="e42ed-130">Fixed Issues</span></span>

<span data-ttu-id="e42ed-131">**Problemas importantes**</span><span class="sxs-lookup"><span data-stu-id="e42ed-131">**Notable Issues**</span></span>

* <span data-ttu-id="e42ed-132">Pacotes do NuGet restaurado suporte para a restauração com um arquivo de solução Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="e42ed-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="e42ed-133">A lista completa de problemas foram resolvidos na versão 3.3 pode ser encontrada no GitHub sob o [3.3 marco](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="e42ed-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="e42ed-134">A lista de problemas corrigidos na versão de linha de comando 3.3 são registradas no [3.3 etapa de linha de comando](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="e42ed-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="e42ed-135">Problemas Conhecidos</span><span class="sxs-lookup"><span data-stu-id="e42ed-135">Known Issues</span></span>

<span data-ttu-id="e42ed-136">Continuamos a rastrear problemas em nossa lista de problemas do GitHub que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="e42ed-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>