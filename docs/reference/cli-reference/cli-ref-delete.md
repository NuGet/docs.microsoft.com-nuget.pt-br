---
title: Comando de exclusão da CLI do NuGet
description: Referência para o comando de exclusão NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327833"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="87476-103">comando Delete (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="87476-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="87476-104">**Aplica-se a:** &bullet; **versões com suporte** para publicação de pacotes: todas</span><span class="sxs-lookup"><span data-stu-id="87476-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="87476-105">Exclui ou deslista um pacote de uma origem de pacote.</span><span class="sxs-lookup"><span data-stu-id="87476-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="87476-106">Para nuget.org, o comando delete [deslista o pacote](../../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="87476-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="87476-107">Uso</span><span class="sxs-lookup"><span data-stu-id="87476-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="87476-108">onde `<packageID>` e`<packageVersion>` identificar o pacote exato a ser excluído ou deslistado.</span><span class="sxs-lookup"><span data-stu-id="87476-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="87476-109">O comportamento exato depende da origem.</span><span class="sxs-lookup"><span data-stu-id="87476-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="87476-110">Para pastas locais, por exemplo, o pacote é excluído; para nuget.org, o pacote é não listado.</span><span class="sxs-lookup"><span data-stu-id="87476-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="87476-111">Opções</span><span class="sxs-lookup"><span data-stu-id="87476-111">Options</span></span>

| <span data-ttu-id="87476-112">Opção</span><span class="sxs-lookup"><span data-stu-id="87476-112">Option</span></span> | <span data-ttu-id="87476-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="87476-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="87476-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="87476-114">ApiKey</span></span> | <span data-ttu-id="87476-115">A chave de API para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="87476-115">The API key for the target repository.</span></span> <span data-ttu-id="87476-116">Se não estiver presente, o especificado no arquivo de configuração será usado.</span><span class="sxs-lookup"><span data-stu-id="87476-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="87476-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="87476-117">ConfigFile</span></span> | <span data-ttu-id="87476-118">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="87476-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="87476-119">Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="87476-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="87476-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="87476-120">ForceEnglishOutput</span></span> | <span data-ttu-id="87476-121">*(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="87476-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="87476-122">Help</span><span class="sxs-lookup"><span data-stu-id="87476-122">Help</span></span> | <span data-ttu-id="87476-123">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="87476-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="87476-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="87476-124">NonInteractive</span></span> | <span data-ttu-id="87476-125">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="87476-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="87476-126">Source</span><span class="sxs-lookup"><span data-stu-id="87476-126">Source</span></span> | <span data-ttu-id="87476-127">Especifica a URL do servidor.</span><span class="sxs-lookup"><span data-stu-id="87476-127">Specifies the server URL.</span></span> <span data-ttu-id="87476-128">A URL para nuget.org é `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="87476-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="87476-129">Para feeds particulares, substitua o nome do host, por exemplo, *% hostname%/API/v3*.</span><span class="sxs-lookup"><span data-stu-id="87476-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="87476-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="87476-130">Verbosity</span></span> | <span data-ttu-id="87476-131">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="87476-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="87476-132">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="87476-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="87476-133">Exemplos</span><span class="sxs-lookup"><span data-stu-id="87476-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
