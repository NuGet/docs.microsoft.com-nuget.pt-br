---
title: Comando do NuGet CLI delete | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: c213a07a-711d-47e0-9ee6-1d582e6cdb69
description: "Referência para o comando de exclusão de nuget.exe"
keywords: "NuGet excluir referência, excluir o comando de pacote"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 92af9dc356f3932347864976496e0ba1216496c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="16ec6-104">Excluir um comando NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="16ec6-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="16ec6-105">**Aplica-se a:** pacote publicação &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="16ec6-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="16ec6-106">Exclui ou unlists um pacote de uma origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="16ec6-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="16ec6-107">Para nuget.org, o comando Excluir [unlists o pacote](../policies/Deleting-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="16ec6-107">For nuget.org, the delete command [unlists the package](../policies/Deleting-Packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="16ec6-108">Uso</span><span class="sxs-lookup"><span data-stu-id="16ec6-108">Usage</span></span>

```
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="16ec6-109">onde `<packageID>` e `<packageVersion>` identificar o pacote exato para excluir ou remover da lista.</span><span class="sxs-lookup"><span data-stu-id="16ec6-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="16ec6-110">O comportamento exato depende da fonte.</span><span class="sxs-lookup"><span data-stu-id="16ec6-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="16ec6-111">Para pastas locais, por exemplo, o pacote foi excluído; para o pacote do nuget.org está na lista.</span><span class="sxs-lookup"><span data-stu-id="16ec6-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="16ec6-112">Opções</span><span class="sxs-lookup"><span data-stu-id="16ec6-112">Options</span></span>

| <span data-ttu-id="16ec6-113">Opção</span><span class="sxs-lookup"><span data-stu-id="16ec6-113">Option</span></span> | <span data-ttu-id="16ec6-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="16ec6-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="16ec6-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="16ec6-115">ApiKey</span></span> | <span data-ttu-id="16ec6-116">A chave de API para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="16ec6-116">The API key for the target repository.</span></span> <span data-ttu-id="16ec6-117">Se não estiverem presentes, especificada na *%AppData%\NuGet\NuGet.Config* é usado.</span><span class="sxs-lookup"><span data-stu-id="16ec6-117">If not present, the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="16ec6-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="16ec6-118">ConfigFile</span></span> | <span data-ttu-id="16ec6-119">*(2.5 +)*  NuGet o arquivo de configuração para aplicar.</span><span class="sxs-lookup"><span data-stu-id="16ec6-119">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="16ec6-120">Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado.</span><span class="sxs-lookup"><span data-stu-id="16ec6-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="16ec6-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="16ec6-121">ForceEnglishOutput</span></span> | <span data-ttu-id="16ec6-122">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="16ec6-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="16ec6-123">Ajuda</span><span class="sxs-lookup"><span data-stu-id="16ec6-123">Help</span></span> | <span data-ttu-id="16ec6-124">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="16ec6-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="16ec6-125">Não interativo</span><span class="sxs-lookup"><span data-stu-id="16ec6-125">NonInteractive</span></span> | <span data-ttu-id="16ec6-126">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="16ec6-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="16ec6-127">Origem</span><span class="sxs-lookup"><span data-stu-id="16ec6-127">Source</span></span> | <span data-ttu-id="16ec6-128">Especifica a URL do servidor.</span><span class="sxs-lookup"><span data-stu-id="16ec6-128">Specifies the server URL.</span></span> <span data-ttu-id="16ec6-129">A URL para nuget.org é `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="16ec6-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="16ec6-130">Para feeds privados, substitua o nome de host, por exemplo, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="16ec6-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="16ec6-131">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="16ec6-131">Verbosity</span></span> | <span data-ttu-id="16ec6-132">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="16ec6-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="16ec6-133">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="16ec6-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="16ec6-134">Exemplos</span><span class="sxs-lookup"><span data-stu-id="16ec6-134">Examples</span></span>

```
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
