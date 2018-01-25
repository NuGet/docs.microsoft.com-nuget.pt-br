---
title: Comando do NuGet CLI delete | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência para o comando de exclusão de nuget.exe"
keywords: "NuGet excluir referência, excluir o comando de pacote"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3890e33ab0fc425e1c2ee39631ade57ea9b92bc9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="b26b7-104">Excluir um comando NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b26b7-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="b26b7-105">**Aplica-se a:** pacote publicação &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="b26b7-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b26b7-106">Exclui ou unlists um pacote de uma origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="b26b7-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="b26b7-107">Para nuget.org, o comando Excluir [unlists o pacote](../policies/Deleting-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="b26b7-107">For nuget.org, the delete command [unlists the package](../policies/Deleting-Packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="b26b7-108">Uso</span><span class="sxs-lookup"><span data-stu-id="b26b7-108">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="b26b7-109">onde `<packageID>` e `<packageVersion>` identificar o pacote exato para excluir ou remover da lista.</span><span class="sxs-lookup"><span data-stu-id="b26b7-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="b26b7-110">O comportamento exato depende da fonte.</span><span class="sxs-lookup"><span data-stu-id="b26b7-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="b26b7-111">Para pastas locais, por exemplo, o pacote foi excluído; para o pacote do nuget.org está na lista.</span><span class="sxs-lookup"><span data-stu-id="b26b7-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="b26b7-112">Opções</span><span class="sxs-lookup"><span data-stu-id="b26b7-112">Options</span></span>

| <span data-ttu-id="b26b7-113">Opção</span><span class="sxs-lookup"><span data-stu-id="b26b7-113">Option</span></span> | <span data-ttu-id="b26b7-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="b26b7-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b26b7-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="b26b7-115">ApiKey</span></span> | <span data-ttu-id="b26b7-116">A chave de API para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="b26b7-116">The API key for the target repository.</span></span> <span data-ttu-id="b26b7-117">Se não estiverem presentes, especificada na *%AppData%\NuGet\NuGet.Config* é usado.</span><span class="sxs-lookup"><span data-stu-id="b26b7-117">If not present, the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="b26b7-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b26b7-118">ConfigFile</span></span> | <span data-ttu-id="b26b7-119">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="b26b7-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b26b7-120">Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado.</span><span class="sxs-lookup"><span data-stu-id="b26b7-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="b26b7-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b26b7-121">ForceEnglishOutput</span></span> | <span data-ttu-id="b26b7-122">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="b26b7-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b26b7-123">Ajuda</span><span class="sxs-lookup"><span data-stu-id="b26b7-123">Help</span></span> | <span data-ttu-id="b26b7-124">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="b26b7-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="b26b7-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b26b7-125">NonInteractive</span></span> | <span data-ttu-id="b26b7-126">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="b26b7-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b26b7-127">Origem</span><span class="sxs-lookup"><span data-stu-id="b26b7-127">Source</span></span> | <span data-ttu-id="b26b7-128">Especifica a URL do servidor.</span><span class="sxs-lookup"><span data-stu-id="b26b7-128">Specifies the server URL.</span></span> <span data-ttu-id="b26b7-129">A URL para nuget.org é `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="b26b7-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="b26b7-130">Para feeds privados, substitua o nome de host, por exemplo, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="b26b7-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="b26b7-131">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="b26b7-131">Verbosity</span></span> | <span data-ttu-id="b26b7-132">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="b26b7-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b26b7-133">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b26b7-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b26b7-134">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b26b7-134">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
