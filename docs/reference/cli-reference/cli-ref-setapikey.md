---
title: Comando setapikey da CLI do NuGet
description: Referência para o comando setapikey do NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231221"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="02ec0-103">comando setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="02ec0-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="02ec0-104">**Aplica-se a:** consumo de pacote, publicação &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="02ec0-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="02ec0-105">Salva uma chave de API para uma determinada URL de servidor em `NuGet.Config` para que ela não precise ser inserida para comandos subsequentes.</span><span class="sxs-lookup"><span data-stu-id="02ec0-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="02ec0-106">Uso</span><span class="sxs-lookup"><span data-stu-id="02ec0-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="02ec0-107">onde `<source>` identifica o servidor e `<key>` é a chave a ser salva.</span><span class="sxs-lookup"><span data-stu-id="02ec0-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="02ec0-108">Se `<source>` for omitido, nuget.org será assumido.</span><span class="sxs-lookup"><span data-stu-id="02ec0-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="02ec0-109">A chave de API não é usada para autenticação com o feed particular.</span><span class="sxs-lookup"><span data-stu-id="02ec0-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="02ec0-110">Consulte [`nuget sources` comando](../cli-reference/cli-ref-sources.md) para gerenciar credenciais para autenticação com a origem.</span><span class="sxs-lookup"><span data-stu-id="02ec0-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="02ec0-111">As chaves de API podem ser obtidas dos servidores NuGet individuais.</span><span class="sxs-lookup"><span data-stu-id="02ec0-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="02ec0-112">Para criar e gerenciar APIKeys para nuget.org, consulte [Publish-API-Key](../../quickstart/includes/publish-api-key.md)</span><span class="sxs-lookup"><span data-stu-id="02ec0-112">To create and manage APIKeys for nuget.org refer to [publish-api-key](../../quickstart/includes/publish-api-key.md)</span></span>

## <a name="options"></a><span data-ttu-id="02ec0-113">Opções</span><span class="sxs-lookup"><span data-stu-id="02ec0-113">Options</span></span>

| <span data-ttu-id="02ec0-114">Opção</span><span class="sxs-lookup"><span data-stu-id="02ec0-114">Option</span></span> | <span data-ttu-id="02ec0-115">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="02ec0-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="02ec0-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="02ec0-116">ConfigFile</span></span> | <span data-ttu-id="02ec0-117">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="02ec0-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="02ec0-118">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="02ec0-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="02ec0-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="02ec0-119">ForceEnglishOutput</span></span> | <span data-ttu-id="02ec0-120">*(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="02ec0-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="02ec0-121">Ajuda</span><span class="sxs-lookup"><span data-stu-id="02ec0-121">Help</span></span> | <span data-ttu-id="02ec0-122">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="02ec0-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="02ec0-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="02ec0-123">NonInteractive</span></span> | <span data-ttu-id="02ec0-124">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="02ec0-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="02ec0-125">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="02ec0-125">Verbosity</span></span> | <span data-ttu-id="02ec0-126">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="02ec0-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="02ec0-127">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="02ec0-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="02ec0-128">Exemplos</span><span class="sxs-lookup"><span data-stu-id="02ec0-128">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
