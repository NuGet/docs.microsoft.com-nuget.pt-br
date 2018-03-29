---
title: Comando do NuGet CLI delete | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referência para o comando de exclusão de nuget.exe
keywords: NuGet excluir referência, excluir o comando de pacote
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9445042c46ef41721def1fbbb8dcebf4afc14d1b
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="2e8e6-104">Excluir um comando NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2e8e6-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="2e8e6-105">**Aplica-se a:** pacote publicação &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="2e8e6-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="2e8e6-106">Exclui ou unlists um pacote de uma origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="2e8e6-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="2e8e6-107">Para nuget.org, o comando Excluir [unlists o pacote](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="2e8e6-107">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="2e8e6-108">Uso</span><span class="sxs-lookup"><span data-stu-id="2e8e6-108">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="2e8e6-109">onde `<packageID>` e `<packageVersion>` identificar o pacote exato para excluir ou remover da lista.</span><span class="sxs-lookup"><span data-stu-id="2e8e6-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="2e8e6-110">O comportamento exato depende da fonte.</span><span class="sxs-lookup"><span data-stu-id="2e8e6-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="2e8e6-111">Para pastas locais, por exemplo, o pacote foi excluído; para o pacote do nuget.org está na lista.</span><span class="sxs-lookup"><span data-stu-id="2e8e6-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="2e8e6-112">Opções</span><span class="sxs-lookup"><span data-stu-id="2e8e6-112">Options</span></span>

| <span data-ttu-id="2e8e6-113">Opção</span><span class="sxs-lookup"><span data-stu-id="2e8e6-113">Option</span></span> | <span data-ttu-id="2e8e6-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="2e8e6-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2e8e6-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="2e8e6-115">ApiKey</span></span> | <span data-ttu-id="2e8e6-116">A chave de API para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="2e8e6-116">The API key for the target repository.</span></span> <span data-ttu-id="2e8e6-117">Se não estiver presente, o especificado no arquivo de configuração é usado.</span><span class="sxs-lookup"><span data-stu-id="2e8e6-117">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="2e8e6-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2e8e6-118">ConfigFile</span></span> | <span data-ttu-id="2e8e6-119">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="2e8e6-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2e8e6-120">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="2e8e6-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2e8e6-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2e8e6-121">ForceEnglishOutput</span></span> | <span data-ttu-id="2e8e6-122">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="2e8e6-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2e8e6-123">Ajuda</span><span class="sxs-lookup"><span data-stu-id="2e8e6-123">Help</span></span> | <span data-ttu-id="2e8e6-124">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="2e8e6-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="2e8e6-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2e8e6-125">NonInteractive</span></span> | <span data-ttu-id="2e8e6-126">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="2e8e6-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2e8e6-127">Origem</span><span class="sxs-lookup"><span data-stu-id="2e8e6-127">Source</span></span> | <span data-ttu-id="2e8e6-128">Especifica a URL do servidor.</span><span class="sxs-lookup"><span data-stu-id="2e8e6-128">Specifies the server URL.</span></span> <span data-ttu-id="2e8e6-129">A URL para nuget.org é `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="2e8e6-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="2e8e6-130">Para feeds privados, substitua o nome de host, por exemplo, *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="2e8e6-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="2e8e6-131">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="2e8e6-131">Verbosity</span></span> | <span data-ttu-id="2e8e6-132">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="2e8e6-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2e8e6-133">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2e8e6-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2e8e6-134">Exemplos</span><span class="sxs-lookup"><span data-stu-id="2e8e6-134">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
