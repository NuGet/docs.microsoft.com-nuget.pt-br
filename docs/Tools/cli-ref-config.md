---
title: Comando de configuração de CLI do NuGet
description: Referência para o comando de configuração de nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 414eb8386f949347772f33170de881534dc71482
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="5254a-103">comando de configuração (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5254a-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="5254a-104">**Aplica-se a:** todos os &bullet; **versões com suporte**: todos os</span><span class="sxs-lookup"><span data-stu-id="5254a-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="5254a-105">Obtém ou define os valores de configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="5254a-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="5254a-106">Para uso adicional, consulte [Configurando NuGet comportamento](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="5254a-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="5254a-107">Para obter detalhes sobre nomes de chave permitidos, consulte o [referência do arquivo de configuração NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="5254a-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="5254a-108">Uso</span><span class="sxs-lookup"><span data-stu-id="5254a-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="5254a-109">onde `<name>` e `<value>` Especifica um par chave-valor a ser definido na configuração.</span><span class="sxs-lookup"><span data-stu-id="5254a-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="5254a-110">Você pode especificar quantos pares conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="5254a-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="5254a-111">Para remover um valor, especifique o nome e o `=` sinal, mas nenhum valor.</span><span class="sxs-lookup"><span data-stu-id="5254a-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="5254a-112">Para nomes de chave permitidos, consulte o [referência do arquivo de configuração NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="5254a-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="5254a-113">No NuGet 3.4 ou posterior, `<value>` pode usar [variáveis de ambiente](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="5254a-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="5254a-114">Opções</span><span class="sxs-lookup"><span data-stu-id="5254a-114">Options</span></span>

| <span data-ttu-id="5254a-115">Opção</span><span class="sxs-lookup"><span data-stu-id="5254a-115">Option</span></span> | <span data-ttu-id="5254a-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="5254a-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5254a-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="5254a-117">AsPath</span></span> | <span data-ttu-id="5254a-118">Retorna a configuração do valor como um caminho, ignorado quando `-Set` é usado.</span><span class="sxs-lookup"><span data-stu-id="5254a-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="5254a-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5254a-119">ConfigFile</span></span> | <span data-ttu-id="5254a-120">O arquivo de configuração do NuGet para modificar.</span><span class="sxs-lookup"><span data-stu-id="5254a-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="5254a-121">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="5254a-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5254a-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5254a-122">ForceEnglishOutput</span></span> | <span data-ttu-id="5254a-123">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="5254a-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5254a-124">Ajuda</span><span class="sxs-lookup"><span data-stu-id="5254a-124">Help</span></span> | <span data-ttu-id="5254a-125">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="5254a-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="5254a-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="5254a-126">NonInteractive</span></span> | <span data-ttu-id="5254a-127">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="5254a-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5254a-128">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="5254a-128">Verbosity</span></span> | <span data-ttu-id="5254a-129">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="5254a-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5254a-130">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5254a-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="5254a-131">Exemplos</span><span class="sxs-lookup"><span data-stu-id="5254a-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
