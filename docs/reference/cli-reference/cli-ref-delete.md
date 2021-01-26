---
title: Comando de exclusão da CLI do NuGet
description: Referência para o comando nuget.exe Delete
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 96c75366ae69b34f5cd1f55feb53087b5d0ea324
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775952"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="0a5a5-103">comando Delete (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="0a5a5-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="0a5a5-104">**Aplica-se a:** &bullet; **versões com suporte** para publicação de pacotes: todas</span><span class="sxs-lookup"><span data-stu-id="0a5a5-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="0a5a5-105">Exclui ou deslista um pacote de uma origem de pacote.</span><span class="sxs-lookup"><span data-stu-id="0a5a5-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="0a5a5-106">Para nuget.org, o comando delete [deslista o pacote](../../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="0a5a5-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="0a5a5-107">Uso</span><span class="sxs-lookup"><span data-stu-id="0a5a5-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="0a5a5-108">onde `<packageID>` e `<packageVersion>` identificar o pacote exato a ser excluído ou deslistado.</span><span class="sxs-lookup"><span data-stu-id="0a5a5-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="0a5a5-109">O comportamento exato depende da origem.</span><span class="sxs-lookup"><span data-stu-id="0a5a5-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="0a5a5-110">Para pastas locais, por exemplo, o pacote é excluído; para nuget.org, o pacote é não listado.</span><span class="sxs-lookup"><span data-stu-id="0a5a5-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="0a5a5-111">Opções</span><span class="sxs-lookup"><span data-stu-id="0a5a5-111">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="0a5a5-112">A chave de API para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="0a5a5-112">The API key for the target repository.</span></span> <span data-ttu-id="0a5a5-113">Se não estiver presente, o especificado no arquivo de configuração será usado.</span><span class="sxs-lookup"><span data-stu-id="0a5a5-113">If not present, the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="0a5a5-114">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="0a5a5-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="0a5a5-115">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="0a5a5-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="0a5a5-116">*(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="0a5a5-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="0a5a5-117">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="0a5a5-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="0a5a5-118">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="0a5a5-118">Suppresses prompts for user input or confirmations.</span></span>

 - **`-np|-NoPrompt`**

   <span data-ttu-id="0a5a5-119">Não avisar ao excluir.</span><span class="sxs-lookup"><span data-stu-id="0a5a5-119">Do not prompt when deleting.</span></span>

 - <span data-ttu-id="0a5a5-120">**`-NoServiceEndpoint`** Não acrescenta "API/v2/packages" à URL de origem.</span><span class="sxs-lookup"><span data-stu-id="0a5a5-120">**`-NoServiceEndpoint`** Does not append "api/v2/packages" to the source URL.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="0a5a5-121">Especifica a URL do servidor.</span><span class="sxs-lookup"><span data-stu-id="0a5a5-121">Specifies the server URL.</span></span> <span data-ttu-id="0a5a5-122">A URL para nuget.org é `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="0a5a5-122">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="0a5a5-123">Para feeds particulares, substitua o nome do host, por exemplo, *% hostname%/API/v3*.</span><span class="sxs-lookup"><span data-stu-id="0a5a5-123">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="0a5a5-124">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="0a5a5-124">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="0a5a5-125">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0a5a5-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0a5a5-126">Exemplos</span><span class="sxs-lookup"><span data-stu-id="0a5a5-126">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
