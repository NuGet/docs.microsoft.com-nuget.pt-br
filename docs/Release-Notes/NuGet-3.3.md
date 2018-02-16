---
title: "Notas de versão do NuGet 3.3 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão do NuGet 3.3 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão 3.3 do NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4d077fb53abd8033aad6da01ad090297109aa68c
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="19cbf-104">Notas de versão 3.3 do NuGet</span><span class="sxs-lookup"><span data-stu-id="19cbf-104">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="19cbf-105">[Notas de versão do NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC notas](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="19cbf-105">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="19cbf-106">3.3 NuGet foi liberado 30 de novembro de 2015, com um número significativo de atualizações de interface do usuário e recursos de linha de comando, bem como um conjunto de correções úteis para os clientes do NuGet.</span><span class="sxs-lookup"><span data-stu-id="19cbf-106">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="19cbf-107">Novos recursos</span><span class="sxs-lookup"><span data-stu-id="19cbf-107">New Features</span></span>

* <span data-ttu-id="19cbf-108">Foram introduzidos provedores de credenciais que permitem que os clientes de linha de comando do NuGet poder funcionar perfeitamente com um feed autenticado.</span><span class="sxs-lookup"><span data-stu-id="19cbf-108">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="19cbf-109">[Provedor de credenciais de instruções sobre como instalar o Visual Studio Team Services ](../api/nuget-exe-credential-providers.md) e configurar o NuGet clientes para usá-lo estão disponíveis em documentos do NuGet.</span><span class="sxs-lookup"><span data-stu-id="19cbf-109">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="19cbf-110">Novos recursos de Interface do usuário</span><span class="sxs-lookup"><span data-stu-id="19cbf-110">New User Interface Features</span></span>

* <span data-ttu-id="19cbf-111">Guias separadas de procurar, instalar e atualizações disponíveis</span><span class="sxs-lookup"><span data-stu-id="19cbf-111">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="19cbf-112">Atualizações de notificação disponível que indica o número de pacotes com atualizações disponíveis</span><span class="sxs-lookup"><span data-stu-id="19cbf-112">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="19cbf-113">Notificações de pacote na lista de pacotes para indicar se o pacote está instalado, ou uma atualização disponível</span><span class="sxs-lookup"><span data-stu-id="19cbf-113">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="19cbf-114">Baixar a contagem e adicionado à lista de pacotes de autor</span><span class="sxs-lookup"><span data-stu-id="19cbf-114">Download count and author added to the package list</span></span>
* <span data-ttu-id="19cbf-115">Maior número de versão disponíveis e o número de versão instalada atualmente na lista de pacotes</span><span class="sxs-lookup"><span data-stu-id="19cbf-115">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="19cbf-116">Botões de ação para permitir a rápida instalar, atualizar e desinstalar da lista de pacotes</span><span class="sxs-lookup"><span data-stu-id="19cbf-116">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="19cbf-117">Botões de ação mais claros no painel de detalhes do pacote</span><span class="sxs-lookup"><span data-stu-id="19cbf-117">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="19cbf-118">Data de atualização de pacote no painel de detalhes do pacote</span><span class="sxs-lookup"><span data-stu-id="19cbf-118">Package update date on the package detail panel</span></span>
* <span data-ttu-id="19cbf-119">Consolidar o painel no modo de exibição de solução</span><span class="sxs-lookup"><span data-stu-id="19cbf-119">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="19cbf-120">Grade classificável de projetos e os números de versão instalada no modo de exibição de solução</span><span class="sxs-lookup"><span data-stu-id="19cbf-120">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="19cbf-121">Novos recursos de linha de comando</span><span class="sxs-lookup"><span data-stu-id="19cbf-121">New Command-line Features</span></span>

<span data-ttu-id="19cbf-122">Nesta versão, apresentamos o `add` e `init` comandos para inicializar com base em pasta repositórios conforme descrito no [nuget.exe referência](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="19cbf-122">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="19cbf-123">Estrutura de repositórios que são construídos e mantidos com esta pasta será [fornecer benefícios significativos de desempenho](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) conforme descrito em nosso blog.</span><span class="sxs-lookup"><span data-stu-id="19cbf-123">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="19cbf-124">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="19cbf-124">ContentFiles</span></span>

<span data-ttu-id="19cbf-125">Agora há suporte para o conteúdo em `project.json` gerenciados projetos por meio do novo `contentFiles` pasta e `.nuspec` `contentFiles` notação de elemento.</span><span class="sxs-lookup"><span data-stu-id="19cbf-125">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="19cbf-126">Esse conteúdo pode ser especificado mais diretamente pelo autor do pacote para interações com sistemas de projeto.</span><span class="sxs-lookup"><span data-stu-id="19cbf-126">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="19cbf-127">Para obter mais informações sobre como configurar contentFiles em uma `.nuspec` documento pode ser encontrado na [. NuSpec referência](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="19cbf-127">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="19cbf-128">Gerenciamento de Cache do NuGet locais</span><span class="sxs-lookup"><span data-stu-id="19cbf-128">NuGet Locals Cache Management</span></span>

<span data-ttu-id="19cbf-129">O linha de comando do NuGet foi atualizado para incluir informações sobre como gerenciar os caches locais em uma estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="19cbf-129">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="19cbf-130">Para obter mais informações sobre o comando locais estão disponíveis na [referência de linha de comando do NuGet](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="19cbf-130">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="19cbf-131">Problemas corrigidos</span><span class="sxs-lookup"><span data-stu-id="19cbf-131">Fixed Issues</span></span>

<span data-ttu-id="19cbf-132">**Problemas importantes**</span><span class="sxs-lookup"><span data-stu-id="19cbf-132">**Notable Issues**</span></span>

* <span data-ttu-id="19cbf-133">Pacotes do NuGet restaurado suporte para a restauração com um arquivo de solução Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="19cbf-133">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="19cbf-134">A lista completa de problemas foram resolvidos na versão 3.3 pode ser encontrada no GitHub sob o [3.3 marco](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="19cbf-134">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="19cbf-135">A lista de problemas corrigidos na versão de linha de comando 3.3 são registradas no [3.3 etapa de linha de comando](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="19cbf-135">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="19cbf-136">Problemas Conhecidos</span><span class="sxs-lookup"><span data-stu-id="19cbf-136">Known Issues</span></span>

<span data-ttu-id="19cbf-137">Continuamos a rastrear problemas em nossa lista de problemas do GitHub que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="19cbf-137">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>