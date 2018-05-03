---
title: Comando do NuGet CLI setapikey
description: Referência para o comando de setapikey nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 968e22f32e51659590a6fe1e881bf5a9792a1331
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="b109d-103">comando setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b109d-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="b109d-104">**Aplica-se a:** consumo de pacote, a publicação &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="b109d-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b109d-105">Salva uma chave de API para uma URL de servidor específico em `NuGet.Config` para que ele não precisa ser inserido para os comandos subsequentes.</span><span class="sxs-lookup"><span data-stu-id="b109d-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="b109d-106">Uso</span><span class="sxs-lookup"><span data-stu-id="b109d-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="b109d-107">onde `<source>` identifica o servidor e `<key>` é a chave ou senha para salvar.</span><span class="sxs-lookup"><span data-stu-id="b109d-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="b109d-108">Se `<source>` for omitido, nuget.org é assumido.</span><span class="sxs-lookup"><span data-stu-id="b109d-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="b109d-109">Opções</span><span class="sxs-lookup"><span data-stu-id="b109d-109">Options</span></span>

| <span data-ttu-id="b109d-110">Opção</span><span class="sxs-lookup"><span data-stu-id="b109d-110">Option</span></span> | <span data-ttu-id="b109d-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="b109d-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b109d-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b109d-112">ConfigFile</span></span> | <span data-ttu-id="b109d-113">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="b109d-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b109d-114">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="b109d-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b109d-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b109d-115">ForceEnglishOutput</span></span> | <span data-ttu-id="b109d-116">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="b109d-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b109d-117">Ajuda</span><span class="sxs-lookup"><span data-stu-id="b109d-117">Help</span></span> | <span data-ttu-id="b109d-118">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="b109d-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="b109d-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b109d-119">NonInteractive</span></span> | <span data-ttu-id="b109d-120">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="b109d-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b109d-121">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="b109d-121">Verbosity</span></span> | <span data-ttu-id="b109d-122">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="b109d-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b109d-123">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b109d-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b109d-124">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b109d-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
