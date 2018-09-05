---
title: Comando do CLI do NuGet setapikey
description: Referência do comando de setapikey nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549214"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="8f14c-103">setapikey comando (CLI do NuGet)</span><span class="sxs-lookup"><span data-stu-id="8f14c-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="8f14c-104">**Aplica-se a:** consumo de pacote, publicando &bullet; **versões com suporte:** todos os</span><span class="sxs-lookup"><span data-stu-id="8f14c-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8f14c-105">Salva uma chave de API para uma URL de servidor específico em `NuGet.Config` para que ele não precisa ser inserido para comandos subsequentes.</span><span class="sxs-lookup"><span data-stu-id="8f14c-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="8f14c-106">Uso</span><span class="sxs-lookup"><span data-stu-id="8f14c-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="8f14c-107">em que `<source>` identifica o servidor e `<key>` é a chave ou senha para salvar.</span><span class="sxs-lookup"><span data-stu-id="8f14c-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="8f14c-108">Se `<source>` for omitido, o nuget.org é assumido.</span><span class="sxs-lookup"><span data-stu-id="8f14c-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="8f14c-109">Opções</span><span class="sxs-lookup"><span data-stu-id="8f14c-109">Options</span></span>

| <span data-ttu-id="8f14c-110">Opção</span><span class="sxs-lookup"><span data-stu-id="8f14c-110">Option</span></span> | <span data-ttu-id="8f14c-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="8f14c-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8f14c-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8f14c-112">ConfigFile</span></span> | <span data-ttu-id="8f14c-113">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="8f14c-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8f14c-114">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="8f14c-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8f14c-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8f14c-115">ForceEnglishOutput</span></span> | <span data-ttu-id="8f14c-116">*(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="8f14c-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8f14c-117">Ajuda</span><span class="sxs-lookup"><span data-stu-id="8f14c-117">Help</span></span> | <span data-ttu-id="8f14c-118">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="8f14c-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="8f14c-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8f14c-119">NonInteractive</span></span> | <span data-ttu-id="8f14c-120">Suprime a solicitações de entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="8f14c-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8f14c-121">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="8f14c-121">Verbosity</span></span> | <span data-ttu-id="8f14c-122">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="8f14c-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8f14c-123">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8f14c-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8f14c-124">Exemplos</span><span class="sxs-lookup"><span data-stu-id="8f14c-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
