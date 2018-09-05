---
title: Comando de exclusão de CLI do NuGet
description: Referência do comando delete nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 11eea6e806d7bfe364587db9c7ef8374da1819f9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548504"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="ca59b-103">Excluir comando (CLI do NuGet)</span><span class="sxs-lookup"><span data-stu-id="ca59b-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="ca59b-104">**Aplica-se a:** publicação de pacote &bullet; **versões com suporte:** todos os</span><span class="sxs-lookup"><span data-stu-id="ca59b-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ca59b-105">Exclui ou retira da lista um pacote a partir de uma origem de pacote.</span><span class="sxs-lookup"><span data-stu-id="ca59b-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="ca59b-106">Para nuget.org, o comando de exclusão [retira da lista o pacote](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ca59b-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="ca59b-107">Uso</span><span class="sxs-lookup"><span data-stu-id="ca59b-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="ca59b-108">em que `<packageID>` e `<packageVersion>` identificar o pacote exato para excluir ou remover da lista.</span><span class="sxs-lookup"><span data-stu-id="ca59b-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="ca59b-109">O comportamento exato depende do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="ca59b-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="ca59b-110">Para pastas locais, por exemplo, o pacote é excluído; para nuget.org, o pacote é removido da lista.</span><span class="sxs-lookup"><span data-stu-id="ca59b-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="ca59b-111">Opções</span><span class="sxs-lookup"><span data-stu-id="ca59b-111">Options</span></span>

| <span data-ttu-id="ca59b-112">Opção</span><span class="sxs-lookup"><span data-stu-id="ca59b-112">Option</span></span> | <span data-ttu-id="ca59b-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="ca59b-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ca59b-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="ca59b-114">ApiKey</span></span> | <span data-ttu-id="ca59b-115">A chave de API para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="ca59b-115">The API key for the target repository.</span></span> <span data-ttu-id="ca59b-116">Se não estiver presente, aquele especificado no arquivo de configuração será usada.</span><span class="sxs-lookup"><span data-stu-id="ca59b-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="ca59b-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ca59b-117">ConfigFile</span></span> | <span data-ttu-id="ca59b-118">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="ca59b-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ca59b-119">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="ca59b-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ca59b-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ca59b-120">ForceEnglishOutput</span></span> | <span data-ttu-id="ca59b-121">*(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="ca59b-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ca59b-122">Ajuda</span><span class="sxs-lookup"><span data-stu-id="ca59b-122">Help</span></span> | <span data-ttu-id="ca59b-123">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="ca59b-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="ca59b-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ca59b-124">NonInteractive</span></span> | <span data-ttu-id="ca59b-125">Suprime a solicitações de entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="ca59b-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ca59b-126">Origem</span><span class="sxs-lookup"><span data-stu-id="ca59b-126">Source</span></span> | <span data-ttu-id="ca59b-127">Especifica a URL do servidor.</span><span class="sxs-lookup"><span data-stu-id="ca59b-127">Specifies the server URL.</span></span> <span data-ttu-id="ca59b-128">A URL para o nuget.org é `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="ca59b-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="ca59b-129">Para feeds privados, substitua o nome de host, por exemplo, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="ca59b-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="ca59b-130">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="ca59b-130">Verbosity</span></span> | <span data-ttu-id="ca59b-131">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="ca59b-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ca59b-132">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ca59b-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ca59b-133">Exemplos</span><span class="sxs-lookup"><span data-stu-id="ca59b-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
