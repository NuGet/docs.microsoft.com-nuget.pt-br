---
title: Comando de configuração de CLI do NuGet
description: Referência para o comando de configuração de nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 9deab9fcca740ea99da61b7d54700a29c1813e88
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818159"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="718bc-103">comando de configuração (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="718bc-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="718bc-104">**Aplica-se a:** todos os &bullet; **versões com suporte**: todos os</span><span class="sxs-lookup"><span data-stu-id="718bc-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="718bc-105">Obtém ou define os valores de configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="718bc-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="718bc-106">Para uso adicional, consulte [Configurando NuGet comportamento](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="718bc-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="718bc-107">Para obter detalhes sobre nomes de chave permitidos, consulte o [referência do arquivo de configuração NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="718bc-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="718bc-108">Uso</span><span class="sxs-lookup"><span data-stu-id="718bc-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="718bc-109">onde `<name>` e `<value>` Especifica um par chave-valor a ser definido na configuração.</span><span class="sxs-lookup"><span data-stu-id="718bc-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="718bc-110">Você pode especificar quantos pares conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="718bc-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="718bc-111">Para remover um valor, especifique o nome e o `=` sinal, mas nenhum valor.</span><span class="sxs-lookup"><span data-stu-id="718bc-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="718bc-112">Para nomes de chave permitidos, consulte o [referência do arquivo de configuração NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="718bc-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="718bc-113">No NuGet 3.4 ou posterior, `<value>` pode usar [variáveis de ambiente](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="718bc-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="718bc-114">Opções</span><span class="sxs-lookup"><span data-stu-id="718bc-114">Options</span></span>

| <span data-ttu-id="718bc-115">Opção</span><span class="sxs-lookup"><span data-stu-id="718bc-115">Option</span></span> | <span data-ttu-id="718bc-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="718bc-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="718bc-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="718bc-117">AsPath</span></span> | <span data-ttu-id="718bc-118">Retorna a configuração do valor como um caminho, ignorado quando `-Set` é usado.</span><span class="sxs-lookup"><span data-stu-id="718bc-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="718bc-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="718bc-119">ConfigFile</span></span> | <span data-ttu-id="718bc-120">O arquivo de configuração do NuGet para modificar.</span><span class="sxs-lookup"><span data-stu-id="718bc-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="718bc-121">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="718bc-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="718bc-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="718bc-122">ForceEnglishOutput</span></span> | <span data-ttu-id="718bc-123">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="718bc-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="718bc-124">Ajuda</span><span class="sxs-lookup"><span data-stu-id="718bc-124">Help</span></span> | <span data-ttu-id="718bc-125">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="718bc-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="718bc-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="718bc-126">NonInteractive</span></span> | <span data-ttu-id="718bc-127">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="718bc-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="718bc-128">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="718bc-128">Verbosity</span></span> | <span data-ttu-id="718bc-129">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="718bc-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="718bc-130">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="718bc-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="718bc-131">Exemplos</span><span class="sxs-lookup"><span data-stu-id="718bc-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
