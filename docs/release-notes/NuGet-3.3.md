---
title: Notas de versão do NuGet 3,3
description: Notas de versão do NuGet 3,3 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa8290c80cc500b59d1779bf76662c07382fd277
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813774"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="0fe1f-103">Notas de versão do NuGet 3,3</span><span class="sxs-lookup"><span data-stu-id="0fe1f-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="0fe1f-104">[Notas de versão do NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3,4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="0fe1f-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="0fe1f-105">O NuGet 3,3 foi lançado em 30 de novembro de 2015 com um número significativo de atualizações de interface do usuário e recursos de linha de comando, bem como uma coleção de correções úteis para os clientes NuGet.</span><span class="sxs-lookup"><span data-stu-id="0fe1f-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="0fe1f-106">Novos recursos</span><span class="sxs-lookup"><span data-stu-id="0fe1f-106">New Features</span></span>

* <span data-ttu-id="0fe1f-107">Provedores de credenciais foram introduzidos para permitir que os clientes de linha de comando do NuGet possam trabalhar sem problemas com um feed autenticado.</span><span class="sxs-lookup"><span data-stu-id="0fe1f-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="0fe1f-108">[Instruções sobre como instalar o provedor de credenciais Visual Studio Team Services](../reference/extensibility/nuget-exe-credential-providers.md) e configurar os clientes do NuGet para usá-lo estão disponíveis em documentos do NuGet.</span><span class="sxs-lookup"><span data-stu-id="0fe1f-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../reference/extensibility/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="0fe1f-109">Novos recursos da interface do usuário</span><span class="sxs-lookup"><span data-stu-id="0fe1f-109">New User Interface Features</span></span>

* <span data-ttu-id="0fe1f-110">Guias de procurar, instalar e atualizar disponíveis separados</span><span class="sxs-lookup"><span data-stu-id="0fe1f-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="0fe1f-111">Notificação de atualizações disponíveis indicando o número de pacotes com atualizações disponíveis</span><span class="sxs-lookup"><span data-stu-id="0fe1f-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="0fe1f-112">Notificações de pacote na lista de pacotes para indicar se o pacote está instalado ou se tem uma atualização disponível</span><span class="sxs-lookup"><span data-stu-id="0fe1f-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="0fe1f-113">Baixar a contagem e o autor adicionados à lista de pacotes</span><span class="sxs-lookup"><span data-stu-id="0fe1f-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="0fe1f-114">Número de versão mais alto disponível e número de versão atualmente instalado na lista de pacotes</span><span class="sxs-lookup"><span data-stu-id="0fe1f-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="0fe1f-115">Botões de ação para permitir instalação, atualização e desinstalação rápida na lista de pacotes</span><span class="sxs-lookup"><span data-stu-id="0fe1f-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="0fe1f-116">Botões de ação mais claros no painel de detalhes do pacote</span><span class="sxs-lookup"><span data-stu-id="0fe1f-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="0fe1f-117">Data de atualização do pacote no painel de detalhes do pacote</span><span class="sxs-lookup"><span data-stu-id="0fe1f-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="0fe1f-118">Painel consolidar no modo de exibição de solução</span><span class="sxs-lookup"><span data-stu-id="0fe1f-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="0fe1f-119">Grade classificável de projetos e números de versão instalados no modo de exibição de solução</span><span class="sxs-lookup"><span data-stu-id="0fe1f-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="0fe1f-120">Novos recursos de linha de comando</span><span class="sxs-lookup"><span data-stu-id="0fe1f-120">New Command-line Features</span></span>

<span data-ttu-id="0fe1f-121">Nesta versão, apresentamos os comandos `add` e `init` para inicializar repositórios baseados em pasta, conforme descrito na [referência do NuGet. exe](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="0fe1f-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="0fe1f-122">Os repositórios construídos e mantidos com essa estrutura de pastas fornecerão [benefícios de desempenho significativos](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) , conforme descrito em nosso blog.</span><span class="sxs-lookup"><span data-stu-id="0fe1f-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="0fe1f-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="0fe1f-123">ContentFiles</span></span>

<span data-ttu-id="0fe1f-124">Agora há suporte para conteúdo em `project.json` projetos gerenciados por meio da nova pasta `contentFiles` e `.nuspec` notação de elemento `contentFiles`.</span><span class="sxs-lookup"><span data-stu-id="0fe1f-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="0fe1f-125">Esse conteúdo pode ser especificado mais diretamente pelo autor do pacote para interações com sistemas de projeto.</span><span class="sxs-lookup"><span data-stu-id="0fe1f-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="0fe1f-126">Mais informações sobre como configurar o contentFiles em um documento `.nuspec` podem ser encontradas na [referência de. nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="0fe1f-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="0fe1f-127">Gerenciamento de cache local do NuGet</span><span class="sxs-lookup"><span data-stu-id="0fe1f-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="0fe1f-128">A linha de comando do NuGet foi atualizada para incluir informações sobre como gerenciar os caches locais em uma estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0fe1f-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="0fe1f-129">Mais informações sobre o comando locals estão disponíveis na [referência de linha de comando do NuGet](../reference/cli-reference/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="0fe1f-129">More information about the locals command is available in the [NuGet command-line reference](../reference/cli-reference/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="0fe1f-130">Problemas corrigidos</span><span class="sxs-lookup"><span data-stu-id="0fe1f-130">Fixed Issues</span></span>

<span data-ttu-id="0fe1f-131">**Problemas notáveis**</span><span class="sxs-lookup"><span data-stu-id="0fe1f-131">**Notable Issues**</span></span>

* <span data-ttu-id="0fe1f-132">Suporte de linha de comando do NuGet restaurado para restaurar pacotes com um arquivo de solução no mono- [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="0fe1f-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="0fe1f-133">A lista completa de problemas que foram resolvidos na versão 3,3 pode ser encontrada no GitHub na [etapa 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="0fe1f-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="0fe1f-134">A lista de problemas corrigidos na versão de linha de comando 3,3 é registrada na [etapa de linha de comando 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="0fe1f-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="0fe1f-135">Problemas Conhecidos</span><span class="sxs-lookup"><span data-stu-id="0fe1f-135">Known Issues</span></span>

<span data-ttu-id="0fe1f-136">Continuamos a acompanhar problemas em nossa lista de problemas do GitHub, que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="0fe1f-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>