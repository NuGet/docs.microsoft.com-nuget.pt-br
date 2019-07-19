---
title: Comando de configuração da CLI do NuGet
description: Referência para o comando de configuração NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 51c4c9937483e7f8a57356515c06a60c0f9e6f62
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327843"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="16460-103">comando config (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="16460-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="16460-104">**Aplica-se a:** todas &bullet; as **versões com suporte**: todas</span><span class="sxs-lookup"><span data-stu-id="16460-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="16460-105">Obtém ou define os valores de configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="16460-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="16460-106">Para uso adicional, consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="16460-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="16460-107">Para obter detalhes sobre nomes de chave permitidos, consulte a [referência do arquivo de configuração do NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="16460-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="16460-108">Uso</span><span class="sxs-lookup"><span data-stu-id="16460-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="16460-109">onde `<name>` e`<value>` especifique um par chave-valor a ser definido na configuração.</span><span class="sxs-lookup"><span data-stu-id="16460-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="16460-110">Você pode especificar quantos pares desejar.</span><span class="sxs-lookup"><span data-stu-id="16460-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="16460-111">Para remover um valor, especifique o nome e o `=` sinal, mas nenhum valor.</span><span class="sxs-lookup"><span data-stu-id="16460-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="16460-112">Para nomes de chave permitidos, consulte a [referência do arquivo de configuração do NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="16460-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="16460-113">No NuGet 3.4 +, `<value>` o pode usar [variáveis de ambiente](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="16460-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="16460-114">Opções</span><span class="sxs-lookup"><span data-stu-id="16460-114">Options</span></span>

| <span data-ttu-id="16460-115">Opção</span><span class="sxs-lookup"><span data-stu-id="16460-115">Option</span></span> | <span data-ttu-id="16460-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="16460-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="16460-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="16460-117">AsPath</span></span> | <span data-ttu-id="16460-118">Retorna o valor de configuração como um caminho, ignorado `-Set` quando é usado.</span><span class="sxs-lookup"><span data-stu-id="16460-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="16460-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="16460-119">ConfigFile</span></span> | <span data-ttu-id="16460-120">O arquivo de configuração do NuGet a ser modificado.</span><span class="sxs-lookup"><span data-stu-id="16460-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="16460-121">Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="16460-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="16460-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="16460-122">ForceEnglishOutput</span></span> | <span data-ttu-id="16460-123">*(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="16460-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="16460-124">Help</span><span class="sxs-lookup"><span data-stu-id="16460-124">Help</span></span> | <span data-ttu-id="16460-125">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="16460-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="16460-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="16460-126">NonInteractive</span></span> | <span data-ttu-id="16460-127">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="16460-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="16460-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="16460-128">Verbosity</span></span> | <span data-ttu-id="16460-129">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="16460-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="16460-130">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="16460-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="16460-131">Exemplos</span><span class="sxs-lookup"><span data-stu-id="16460-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
