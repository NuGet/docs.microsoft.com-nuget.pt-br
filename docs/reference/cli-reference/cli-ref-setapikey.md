---
title: Comando setapikey da CLI do NuGet
description: Referência para o comando setapikey do NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383963"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="8e305-103">comando setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8e305-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="8e305-104">**Aplica-se a:** consumo de pacote, publicação &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="8e305-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8e305-105">Salva uma chave de API para uma determinada URL de servidor em `NuGet.Config` para que ela não precise ser inserida para comandos subsequentes.</span><span class="sxs-lookup"><span data-stu-id="8e305-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="8e305-106">Medição de</span><span class="sxs-lookup"><span data-stu-id="8e305-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="8e305-107">onde `<source>` identifica o servidor e `<key>` é a chave ou a senha a ser salva.</span><span class="sxs-lookup"><span data-stu-id="8e305-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="8e305-108">Se `<source>` for omitido, nuget.org será assumido.</span><span class="sxs-lookup"><span data-stu-id="8e305-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

> [!NOTE]
> <span data-ttu-id="8e305-109">A chave de API não é usada para autenticação com o feed particular.</span><span class="sxs-lookup"><span data-stu-id="8e305-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="8e305-110">Consulte [`nuget sources` comando](../cli-reference/cli-ref-sources.md) para gerenciar credenciais para autenticação com a origem.</span><span class="sxs-lookup"><span data-stu-id="8e305-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>

## <a name="options"></a><span data-ttu-id="8e305-111">Opções</span><span class="sxs-lookup"><span data-stu-id="8e305-111">Options</span></span>

| <span data-ttu-id="8e305-112">Opção</span><span class="sxs-lookup"><span data-stu-id="8e305-112">Option</span></span> | <span data-ttu-id="8e305-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="8e305-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8e305-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8e305-114">ConfigFile</span></span> | <span data-ttu-id="8e305-115">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="8e305-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8e305-116">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="8e305-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8e305-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8e305-117">ForceEnglishOutput</span></span> | <span data-ttu-id="8e305-118">*(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="8e305-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8e305-119">Ajuda</span><span class="sxs-lookup"><span data-stu-id="8e305-119">Help</span></span> | <span data-ttu-id="8e305-120">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="8e305-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="8e305-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8e305-121">NonInteractive</span></span> | <span data-ttu-id="8e305-122">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="8e305-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8e305-123">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="8e305-123">Verbosity</span></span> | <span data-ttu-id="8e305-124">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="8e305-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8e305-125">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8e305-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8e305-126">Exemplos</span><span class="sxs-lookup"><span data-stu-id="8e305-126">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
