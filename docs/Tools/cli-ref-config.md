---
title: "Comando de configuração de CLI do NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência para o comando de configuração de nuget.exe"
keywords: "referência de configuração NuGet, o comando de configuração"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 31abc5c1ade0aff9a2f23ec89ec7082acedb3653
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="50e04-104">comando de configuração (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="50e04-104">config command (NuGet CLI)</span></span>

<span data-ttu-id="50e04-105">**Aplica-se a:** todos os &bullet; **versões com suporte**: todos os</span><span class="sxs-lookup"><span data-stu-id="50e04-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="50e04-106">Obtém ou define os valores de configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="50e04-106">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="50e04-107">Para uso adicional, consulte [Configurando NuGet comportamento](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="50e04-107">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="50e04-108">Para obter detalhes sobre nomes de chave permitidos, consulte o [referência do arquivo de configuração NuGet](../Schema/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="50e04-108">For details on allowable key names, refer to the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="50e04-109">Uso</span><span class="sxs-lookup"><span data-stu-id="50e04-109">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="50e04-110">onde `<name>` e `<value>` Especifica um par chave-valor a ser definido na configuração.</span><span class="sxs-lookup"><span data-stu-id="50e04-110">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="50e04-111">Você pode especificar quantos pares conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="50e04-111">You can specify as many pairs as desired.</span></span> <span data-ttu-id="50e04-112">Para remover um valor, especifique o nome e o `=` sinal, mas nenhum valor.</span><span class="sxs-lookup"><span data-stu-id="50e04-112">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="50e04-113">Para nomes de chave permitidos, consulte o [referência do arquivo de configuração NuGet](../Schema/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="50e04-113">For allowable key names, see the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

<span data-ttu-id="50e04-114">No NuGet 3.4 ou posterior, `<value>` pode usar [variáveis de ambiente](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="50e04-114">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="50e04-115">Opções</span><span class="sxs-lookup"><span data-stu-id="50e04-115">Options</span></span>

| <span data-ttu-id="50e04-116">Opção</span><span class="sxs-lookup"><span data-stu-id="50e04-116">Option</span></span> | <span data-ttu-id="50e04-117">Descrição</span><span class="sxs-lookup"><span data-stu-id="50e04-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="50e04-118">AsPath</span><span class="sxs-lookup"><span data-stu-id="50e04-118">AsPath</span></span> | <span data-ttu-id="50e04-119">Retorna a configuração do valor como um caminho, ignorado quando `-Set` é usado.</span><span class="sxs-lookup"><span data-stu-id="50e04-119">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="50e04-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="50e04-120">ConfigFile</span></span> | <span data-ttu-id="50e04-121">O arquivo de configuração do NuGet para modificar.</span><span class="sxs-lookup"><span data-stu-id="50e04-121">The NuGet configuration file to modify.</span></span> <span data-ttu-id="50e04-122">Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado.</span><span class="sxs-lookup"><span data-stu-id="50e04-122">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="50e04-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="50e04-123">ForceEnglishOutput</span></span> | <span data-ttu-id="50e04-124">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="50e04-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="50e04-125">Ajuda</span><span class="sxs-lookup"><span data-stu-id="50e04-125">Help</span></span> | <span data-ttu-id="50e04-126">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="50e04-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="50e04-127">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="50e04-127">NonInteractive</span></span> | <span data-ttu-id="50e04-128">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="50e04-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="50e04-129">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="50e04-129">Verbosity</span></span> | <span data-ttu-id="50e04-130">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="50e04-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="50e04-131">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="50e04-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="50e04-132">Exemplos</span><span class="sxs-lookup"><span data-stu-id="50e04-132">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
