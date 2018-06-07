---
title: Comando de exclusão de CLI do NuGet
description: Referência para o comando de exclusão de nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0f33dd5475521da47972a6f032ac6ea86d98c83
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817172"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="28346-103">Excluir um comando NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="28346-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="28346-104">**Aplica-se a:** pacote publicação &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="28346-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="28346-105">Exclui ou unlists um pacote de uma origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="28346-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="28346-106">Para nuget.org, o comando Excluir [unlists o pacote](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="28346-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="28346-107">Uso</span><span class="sxs-lookup"><span data-stu-id="28346-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="28346-108">onde `<packageID>` e `<packageVersion>` identificar o pacote exato para excluir ou remover da lista.</span><span class="sxs-lookup"><span data-stu-id="28346-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="28346-109">O comportamento exato depende da fonte.</span><span class="sxs-lookup"><span data-stu-id="28346-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="28346-110">Para pastas locais, por exemplo, o pacote foi excluído; para o pacote do nuget.org está na lista.</span><span class="sxs-lookup"><span data-stu-id="28346-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="28346-111">Opções</span><span class="sxs-lookup"><span data-stu-id="28346-111">Options</span></span>

| <span data-ttu-id="28346-112">Opção</span><span class="sxs-lookup"><span data-stu-id="28346-112">Option</span></span> | <span data-ttu-id="28346-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="28346-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="28346-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="28346-114">ApiKey</span></span> | <span data-ttu-id="28346-115">A chave de API para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="28346-115">The API key for the target repository.</span></span> <span data-ttu-id="28346-116">Se não estiver presente, o especificado no arquivo de configuração é usado.</span><span class="sxs-lookup"><span data-stu-id="28346-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="28346-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="28346-117">ConfigFile</span></span> | <span data-ttu-id="28346-118">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="28346-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="28346-119">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="28346-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="28346-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="28346-120">ForceEnglishOutput</span></span> | <span data-ttu-id="28346-121">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="28346-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="28346-122">Ajuda</span><span class="sxs-lookup"><span data-stu-id="28346-122">Help</span></span> | <span data-ttu-id="28346-123">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="28346-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="28346-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="28346-124">NonInteractive</span></span> | <span data-ttu-id="28346-125">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="28346-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="28346-126">Origem</span><span class="sxs-lookup"><span data-stu-id="28346-126">Source</span></span> | <span data-ttu-id="28346-127">Especifica a URL do servidor.</span><span class="sxs-lookup"><span data-stu-id="28346-127">Specifies the server URL.</span></span> <span data-ttu-id="28346-128">A URL para nuget.org é `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="28346-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="28346-129">Para feeds privados, substitua o nome de host, por exemplo, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="28346-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="28346-130">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="28346-130">Verbosity</span></span> | <span data-ttu-id="28346-131">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="28346-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="28346-132">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="28346-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="28346-133">Exemplos</span><span class="sxs-lookup"><span data-stu-id="28346-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
