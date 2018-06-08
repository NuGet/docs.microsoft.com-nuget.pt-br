---
title: Configurando feeds locais do NuGet
description: Como criar um feed local para pacotes do NuGet usando pastas em sua rede local
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/06/2017
ms.topic: conceptual
ms.openlocfilehash: 5d86657bdf26452d027593b953168e28694acf82
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818679"
---
# <a name="local-feeds"></a><span data-ttu-id="fbf6c-103">Feeds locais</span><span class="sxs-lookup"><span data-stu-id="fbf6c-103">Local feeds</span></span>

<span data-ttu-id="fbf6c-104">Feeds de pacote do NuGet locais são simplesmente estruturas de pasta hierárquicas em sua rede local (ou até mesmo seu próprio computador) em que os pacotes são colocados.</span><span class="sxs-lookup"><span data-stu-id="fbf6c-104">Local NuGet package feeds are simply hierarchical folder structures on your local network (or even just your own computer) in which you place packages.</span></span> <span data-ttu-id="fbf6c-105">Esses feeds podem ser usados como fontes de pacote com todas as outras operações do NuGet usando a CLI, a interface do usuário do Gerenciador de Pacotes e Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="fbf6c-105">These feeds can then be used as package sources with all other NuGet operations using the CLI, the Package Manager UI, and the Package Manager Console.</span></span>

<span data-ttu-id="fbf6c-106">Para habilitar a origem, adicione o nome do caminho (como `\\myserver\packages`) à lista de origens que usam a [Interface do usuário do Gerenciador de Pacotes](../tools/package-manager-ui.md#package-sources) ou o comando [`nuget sources`](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="fbf6c-106">To enable the source, add its pathname (such as `\\myserver\packages`) to the list of sources using the [Package Manager UI](../tools/package-manager-ui.md#package-sources) or the [`nuget sources`](../tools/cli-ref-sources.md) command.</span></span>

> [!Note]
> <span data-ttu-id="fbf6c-107">Estruturas de pastas hierárquicas são compatíveis com o NuGet 3.3 ou superior.</span><span class="sxs-lookup"><span data-stu-id="fbf6c-107">Hierarchical folder structures are supported in NuGet 3.3+.</span></span> <span data-ttu-id="fbf6c-108">Versões mais antigas do NuGet usam apenas uma única pasta que contém pacotes, com a qual o desempenho é muito menor que a estrutura hierárquica.</span><span class="sxs-lookup"><span data-stu-id="fbf6c-108">Older versions of NuGet use only a single folder containing packages, with which performance is much lower than the hierarchical structure.</span></span>

## <a name="initializing-and-maintaining-hierarchical-folders"></a><span data-ttu-id="fbf6c-109">Inicializando e mantendo pastas hierárquicas</span><span class="sxs-lookup"><span data-stu-id="fbf6c-109">Initializing and maintaining hierarchical folders</span></span>

<span data-ttu-id="fbf6c-110">A árvore hierárquica de pastas com controle de versão tem a seguinte estrutura geral:</span><span class="sxs-lookup"><span data-stu-id="fbf6c-110">The hierarchical versioned folder tree has the following general structure:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

<span data-ttu-id="fbf6c-111">O NuGet cria essa estrutura automaticamente quando você usa o comando [`nuget add`](../tools/cli-ref-add.md) para copiar um pacote para o feed:</span><span class="sxs-lookup"><span data-stu-id="fbf6c-111">NuGet creates this structure automatically when you use the [`nuget add`](../tools/cli-ref-add.md) command to copy a package to the feed:</span></span>

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

<span data-ttu-id="fbf6c-112">O comando `nuget add` funciona com um pacote ao mesmo tempo, o que pode ser inconveniente ao configurar um feed com vários pacotes.</span><span class="sxs-lookup"><span data-stu-id="fbf6c-112">The `nuget add` command works with one package at a time, which can be inconvenient when setting up a feed with multiple packages.</span></span>

<span data-ttu-id="fbf6c-113">Nesses casos, use o comando [`nuget init`](../tools/cli-ref-init.md) para copiar todos os pacotes em uma pasta para o feed como se você tivesse executado `nuget add` em cada um deles individualmente.</span><span class="sxs-lookup"><span data-stu-id="fbf6c-113">In such cases, use the [`nuget init`](../tools/cli-ref-init.md) command to copy all packages in a folder to the feed as if you ran `nuget add` on each one individually.</span></span> <span data-ttu-id="fbf6c-114">Por exemplo, o comando a seguir copia todos os pacotes de `c:\packages` para uma árvore hierárquica em `\\myserver\packages`:</span><span class="sxs-lookup"><span data-stu-id="fbf6c-114">For example, the following command copies all packages from `c:\packages` to a hierarchical tree on `\\myserver\packages`:</span></span>

```cli
nuget init c:\packages \\myserver\packages
```

<span data-ttu-id="fbf6c-115">Assim como acontece com o comando `add`, `init` cria uma pasta para cada identificador de pacote, cada uma delas contendo uma pasta de número de versão, na qual está o pacote apropriado.</span><span class="sxs-lookup"><span data-stu-id="fbf6c-115">As with the `add` command, `init` creates a folder for each package identifier, each of which contains a version number folder, within which is the appropriate package.</span></span>
