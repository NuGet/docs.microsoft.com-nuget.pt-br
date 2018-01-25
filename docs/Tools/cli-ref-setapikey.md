---
title: Comando do NuGet CLI setapikey | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência para o comando de setapikey nuget.exe"
keywords: "NuGet setapikey referência, o comando setapikey"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ca6caddbf1404bcaa1ca068c9556f7cf0c651947
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="cc8af-104">comando setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cc8af-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="cc8af-105">**Aplica-se a:** consumo de pacote, a publicação &bullet; **versões com suporte:** todos</span><span class="sxs-lookup"><span data-stu-id="cc8af-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="cc8af-106">Salva uma chave de API para uma URL de servidor específico em `NuGet.Config` para que ele não precisa ser inserido para os comandos subsequentes.</span><span class="sxs-lookup"><span data-stu-id="cc8af-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="cc8af-107">Uso</span><span class="sxs-lookup"><span data-stu-id="cc8af-107">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="cc8af-108">onde `<source>` identifica o servidor e `<key>` é a chave ou senha para salvar.</span><span class="sxs-lookup"><span data-stu-id="cc8af-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="cc8af-109">Se `<source>` for omitido, nuget.org é assumido.</span><span class="sxs-lookup"><span data-stu-id="cc8af-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="cc8af-110">Opções</span><span class="sxs-lookup"><span data-stu-id="cc8af-110">Options</span></span>

| <span data-ttu-id="cc8af-111">Opção</span><span class="sxs-lookup"><span data-stu-id="cc8af-111">Option</span></span> | <span data-ttu-id="cc8af-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="cc8af-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc8af-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="cc8af-113">ConfigFile</span></span> | <span data-ttu-id="cc8af-114">O arquivo de configuração do NuGet para modificar.</span><span class="sxs-lookup"><span data-stu-id="cc8af-114">The NuGet configuration file to modify.</span></span> <span data-ttu-id="cc8af-115">Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado.</span><span class="sxs-lookup"><span data-stu-id="cc8af-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="cc8af-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cc8af-116">ForceEnglishOutput</span></span> | <span data-ttu-id="cc8af-117">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="cc8af-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cc8af-118">Ajuda</span><span class="sxs-lookup"><span data-stu-id="cc8af-118">Help</span></span> | <span data-ttu-id="cc8af-119">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="cc8af-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="cc8af-120">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="cc8af-120">NonInteractive</span></span> | <span data-ttu-id="cc8af-121">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="cc8af-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="cc8af-122">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="cc8af-122">Verbosity</span></span> | <span data-ttu-id="cc8af-123">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="cc8af-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="cc8af-124">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cc8af-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cc8af-125">Exemplos</span><span class="sxs-lookup"><span data-stu-id="cc8af-125">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
