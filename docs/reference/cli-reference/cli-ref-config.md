---
title: Comando de configuração da CLI do NuGet
description: Referência para o comando de configuração NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433313"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="01dc4-103">comando config (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="01dc4-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="01dc4-104">**Aplica-se a:** todas &bullet; as **versões com suporte**: todas</span><span class="sxs-lookup"><span data-stu-id="01dc4-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="01dc4-105">Obtém ou define os valores de configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="01dc4-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="01dc4-106">Para uso adicional, consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="01dc4-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="01dc4-107">Para obter detalhes sobre nomes de chave permitidos, consulte a [referência do arquivo de configuração do NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="01dc4-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="01dc4-108">Uso</span><span class="sxs-lookup"><span data-stu-id="01dc4-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="01dc4-109">onde `<name>` e`<value>` especifique um par chave-valor a ser definido na configuração.</span><span class="sxs-lookup"><span data-stu-id="01dc4-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="01dc4-110">Você pode especificar quantos pares desejar.</span><span class="sxs-lookup"><span data-stu-id="01dc4-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="01dc4-111">Para remover um valor, especifique o nome e o `=` sinal, mas nenhum valor.</span><span class="sxs-lookup"><span data-stu-id="01dc4-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="01dc4-112">Para nomes de chave permitidos, consulte a [referência do arquivo de configuração do NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="01dc4-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="01dc4-113">No NuGet 3.4 +, `<value>` o pode usar [variáveis de ambiente](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="01dc4-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="01dc4-114">Opções</span><span class="sxs-lookup"><span data-stu-id="01dc4-114">Options</span></span>

| <span data-ttu-id="01dc4-115">Opção</span><span class="sxs-lookup"><span data-stu-id="01dc4-115">Option</span></span> | <span data-ttu-id="01dc4-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="01dc4-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="01dc4-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="01dc4-117">AsPath</span></span> | <span data-ttu-id="01dc4-118">Retorna o valor de configuração como um caminho, ignorado `-Set` quando é usado.</span><span class="sxs-lookup"><span data-stu-id="01dc4-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="01dc4-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="01dc4-119">ConfigFile</span></span> | <span data-ttu-id="01dc4-120">O arquivo de configuração do NuGet a ser modificado.</span><span class="sxs-lookup"><span data-stu-id="01dc4-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="01dc4-121">Se não for especificado, o arquivo padrão será usado`%AppData%\NuGet\NuGet.Config` -(Windows) `~/.config/NuGet/NuGet.Config` ou (Mac/Linux) `~/.nuget/NuGet/NuGet.Config` ou (varia de acordo com a distribuição do sistema operacional).</span><span class="sxs-lookup"><span data-stu-id="01dc4-121">If not specified, the default file is used -`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.config/NuGet/NuGet.Config`  (Mac/Linux) or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution).</span></span>|
| <span data-ttu-id="01dc4-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="01dc4-122">ForceEnglishOutput</span></span> | <span data-ttu-id="01dc4-123">*(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="01dc4-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="01dc4-124">Help</span><span class="sxs-lookup"><span data-stu-id="01dc4-124">Help</span></span> | <span data-ttu-id="01dc4-125">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="01dc4-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="01dc4-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="01dc4-126">NonInteractive</span></span> | <span data-ttu-id="01dc4-127">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="01dc4-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="01dc4-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="01dc4-128">Verbosity</span></span> | <span data-ttu-id="01dc4-129">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="01dc4-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="01dc4-130">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="01dc4-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="01dc4-131">Exemplos</span><span class="sxs-lookup"><span data-stu-id="01dc4-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
