---
title: Comando de configuração de CLI do NuGet
description: Referência do comando de configuração nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0497c7b99a2de6bee37d6d0ead8b055578e60b7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426072"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="c563c-103">configuração de comando (CLI do NuGet)</span><span class="sxs-lookup"><span data-stu-id="c563c-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="c563c-104">**Aplica-se a:** todos os &bullet; **versões com suporte**: todos</span><span class="sxs-lookup"><span data-stu-id="c563c-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="c563c-105">Obtém ou define os valores de configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="c563c-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="c563c-106">Para uso adicional, consulte [configurações de NuGet comuns](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="c563c-106">For additional usage, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="c563c-107">Para obter detalhes sobre nomes de chave permitidos, consulte o [referência de arquivo de configuração do NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="c563c-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="c563c-108">Uso</span><span class="sxs-lookup"><span data-stu-id="c563c-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="c563c-109">em que `<name>` e `<value>` especificar um par chave-valor a ser definido na configuração.</span><span class="sxs-lookup"><span data-stu-id="c563c-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="c563c-110">Você pode especificar quantos pares conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="c563c-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="c563c-111">Para remover um valor, especifique o nome e o `=` , mas nenhum valor de entrada.</span><span class="sxs-lookup"><span data-stu-id="c563c-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="c563c-112">Para nomes de chave permitidos, consulte o [referência de arquivo de configuração do NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="c563c-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="c563c-113">No NuGet 3.4 ou superior `<value>` pode usar [variáveis de ambiente](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="c563c-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="c563c-114">Opções</span><span class="sxs-lookup"><span data-stu-id="c563c-114">Options</span></span>

| <span data-ttu-id="c563c-115">Opção</span><span class="sxs-lookup"><span data-stu-id="c563c-115">Option</span></span> | <span data-ttu-id="c563c-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="c563c-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c563c-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="c563c-117">AsPath</span></span> | <span data-ttu-id="c563c-118">Retorna a configuração de valor como um caminho, ignorados quando `-Set` é usado.</span><span class="sxs-lookup"><span data-stu-id="c563c-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="c563c-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c563c-119">ConfigFile</span></span> | <span data-ttu-id="c563c-120">O arquivo de configuração do NuGet para modificar.</span><span class="sxs-lookup"><span data-stu-id="c563c-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="c563c-121">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="c563c-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="c563c-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c563c-122">ForceEnglishOutput</span></span> | <span data-ttu-id="c563c-123">*(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="c563c-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c563c-124">Help</span><span class="sxs-lookup"><span data-stu-id="c563c-124">Help</span></span> | <span data-ttu-id="c563c-125">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="c563c-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="c563c-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="c563c-126">NonInteractive</span></span> | <span data-ttu-id="c563c-127">Suprime a solicitações de entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="c563c-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c563c-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="c563c-128">Verbosity</span></span> | <span data-ttu-id="c563c-129">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="c563c-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="c563c-130">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c563c-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="c563c-131">Exemplos</span><span class="sxs-lookup"><span data-stu-id="c563c-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
