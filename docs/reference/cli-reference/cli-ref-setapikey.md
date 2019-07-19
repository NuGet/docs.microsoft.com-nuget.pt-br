---
title: Comando setapikey da CLI do NuGet
description: Referência para o comando setapikey do NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327603"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="b9f0e-103">comando setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b9f0e-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="b9f0e-104">**Aplica-se a:** consumo de &bullet; pacote, **versões com suporte para publicação:** todos</span><span class="sxs-lookup"><span data-stu-id="b9f0e-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b9f0e-105">Salva uma chave de API para uma determinada URL de `NuGet.Config` servidor no para que ela não precise ser inserida para comandos subsequentes.</span><span class="sxs-lookup"><span data-stu-id="b9f0e-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="b9f0e-106">Uso</span><span class="sxs-lookup"><span data-stu-id="b9f0e-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="b9f0e-107">onde `<source>` o identifica o servidor `<key>` e é a chave ou a senha a ser salva.</span><span class="sxs-lookup"><span data-stu-id="b9f0e-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="b9f0e-108">Se `<source>` for omitido, NuGet.org será assumido.</span><span class="sxs-lookup"><span data-stu-id="b9f0e-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="b9f0e-109">Opções</span><span class="sxs-lookup"><span data-stu-id="b9f0e-109">Options</span></span>

| <span data-ttu-id="b9f0e-110">Opção</span><span class="sxs-lookup"><span data-stu-id="b9f0e-110">Option</span></span> | <span data-ttu-id="b9f0e-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="b9f0e-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b9f0e-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b9f0e-112">ConfigFile</span></span> | <span data-ttu-id="b9f0e-113">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="b9f0e-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b9f0e-114">Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="b9f0e-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b9f0e-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b9f0e-115">ForceEnglishOutput</span></span> | <span data-ttu-id="b9f0e-116">*(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="b9f0e-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b9f0e-117">Help</span><span class="sxs-lookup"><span data-stu-id="b9f0e-117">Help</span></span> | <span data-ttu-id="b9f0e-118">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="b9f0e-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="b9f0e-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b9f0e-119">NonInteractive</span></span> | <span data-ttu-id="b9f0e-120">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="b9f0e-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b9f0e-121">Verbosity</span><span class="sxs-lookup"><span data-stu-id="b9f0e-121">Verbosity</span></span> | <span data-ttu-id="b9f0e-122">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="b9f0e-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b9f0e-123">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b9f0e-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b9f0e-124">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b9f0e-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
