---
title: Comando setapikey da CLI do NuGet
description: Referência para o comando nuget.exe setapikey
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b84d4257c580f6e734c26ebfc589be27bea10c82
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622805"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="37617-103">comando setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="37617-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="37617-104">**Aplica-se a:** consumo de pacote, &bullet; **versões com suporte para publicação:** todos</span><span class="sxs-lookup"><span data-stu-id="37617-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="37617-105">Salva uma chave de API para uma determinada URL de servidor no `NuGet.Config` para que ela não precise ser inserida para comandos subsequentes.</span><span class="sxs-lookup"><span data-stu-id="37617-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="37617-106">Uso</span><span class="sxs-lookup"><span data-stu-id="37617-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="37617-107">onde o `<source>` identifica o servidor e `<key>` é a chave a ser salva.</span><span class="sxs-lookup"><span data-stu-id="37617-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="37617-108">Se `<source>` for omitido, NuGet.org será assumido.</span><span class="sxs-lookup"><span data-stu-id="37617-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="37617-109">A chave de API não é usada para autenticação com o feed particular.</span><span class="sxs-lookup"><span data-stu-id="37617-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="37617-110">Consulte o [ `nuget sources` comando](../cli-reference/cli-ref-sources.md) para gerenciar as credenciais de autenticação com a origem.</span><span class="sxs-lookup"><span data-stu-id="37617-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="37617-111">As chaves de API podem ser obtidas dos servidores NuGet individuais.</span><span class="sxs-lookup"><span data-stu-id="37617-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="37617-112">Para criar e gerenciar APIKeys para nuget.org, consulte [adquirir-a-API-Key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span><span class="sxs-lookup"><span data-stu-id="37617-112">To create and manage APIKeys for nuget.org refer to [acquire-an-api-key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span></span>

## <a name="options"></a><span data-ttu-id="37617-113">Opções</span><span class="sxs-lookup"><span data-stu-id="37617-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="37617-114">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="37617-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="37617-115">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="37617-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="37617-116">*(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="37617-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="37617-117">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="37617-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="37617-118">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="37617-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="37617-119">URL do servidor em que a chave de API é válida.</span><span class="sxs-lookup"><span data-stu-id="37617-119">Server URL where the API key is valid.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="37617-120">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="37617-120">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="37617-121">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="37617-121">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="37617-122">Exemplos</span><span class="sxs-lookup"><span data-stu-id="37617-122">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
