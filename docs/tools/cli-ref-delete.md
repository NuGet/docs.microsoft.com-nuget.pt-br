---
title: Comando de exclusão de CLI do NuGet
description: Referência do comando delete nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3ea2dc3e87d0a626704fe5623d39eaf5bd3f3446
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426117"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="19bd8-103">Excluir comando (CLI do NuGet)</span><span class="sxs-lookup"><span data-stu-id="19bd8-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="19bd8-104">**Aplica-se a:** publicação de pacote &bullet; **versões com suporte:** todos os</span><span class="sxs-lookup"><span data-stu-id="19bd8-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="19bd8-105">Exclui ou retira da lista um pacote a partir de uma origem de pacote.</span><span class="sxs-lookup"><span data-stu-id="19bd8-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="19bd8-106">Para nuget.org, o comando de exclusão [retira da lista o pacote](../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="19bd8-106">For nuget.org, the delete command [unlists the package](../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="19bd8-107">Uso</span><span class="sxs-lookup"><span data-stu-id="19bd8-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="19bd8-108">em que `<packageID>` e `<packageVersion>` identificar o pacote exato para excluir ou remover da lista.</span><span class="sxs-lookup"><span data-stu-id="19bd8-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="19bd8-109">O comportamento exato depende do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="19bd8-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="19bd8-110">Para pastas locais, por exemplo, o pacote é excluído; para nuget.org, o pacote é removido da lista.</span><span class="sxs-lookup"><span data-stu-id="19bd8-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="19bd8-111">Opções</span><span class="sxs-lookup"><span data-stu-id="19bd8-111">Options</span></span>

| <span data-ttu-id="19bd8-112">Opção</span><span class="sxs-lookup"><span data-stu-id="19bd8-112">Option</span></span> | <span data-ttu-id="19bd8-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="19bd8-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="19bd8-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="19bd8-114">ApiKey</span></span> | <span data-ttu-id="19bd8-115">A chave de API para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="19bd8-115">The API key for the target repository.</span></span> <span data-ttu-id="19bd8-116">Se não estiver presente, aquele especificado no arquivo de configuração será usada.</span><span class="sxs-lookup"><span data-stu-id="19bd8-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="19bd8-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="19bd8-117">ConfigFile</span></span> | <span data-ttu-id="19bd8-118">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="19bd8-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="19bd8-119">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="19bd8-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="19bd8-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="19bd8-120">ForceEnglishOutput</span></span> | <span data-ttu-id="19bd8-121">*(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="19bd8-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="19bd8-122">Help</span><span class="sxs-lookup"><span data-stu-id="19bd8-122">Help</span></span> | <span data-ttu-id="19bd8-123">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="19bd8-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="19bd8-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="19bd8-124">NonInteractive</span></span> | <span data-ttu-id="19bd8-125">Suprime a solicitações de entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="19bd8-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="19bd8-126">Source</span><span class="sxs-lookup"><span data-stu-id="19bd8-126">Source</span></span> | <span data-ttu-id="19bd8-127">Especifica a URL do servidor.</span><span class="sxs-lookup"><span data-stu-id="19bd8-127">Specifies the server URL.</span></span> <span data-ttu-id="19bd8-128">A URL para o nuget.org é `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="19bd8-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="19bd8-129">Para feeds privados, substitua o nome de host, por exemplo, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="19bd8-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="19bd8-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="19bd8-130">Verbosity</span></span> | <span data-ttu-id="19bd8-131">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="19bd8-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="19bd8-132">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="19bd8-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="19bd8-133">Exemplos</span><span class="sxs-lookup"><span data-stu-id="19bd8-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
