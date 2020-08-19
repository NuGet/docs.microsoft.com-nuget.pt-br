---
title: Comando de configuração da CLI do NuGet
description: Referência para o comando de configuração nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7d0c1c51f40cba9a5b69f209ffbd995451bfeb9f
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622870"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="5c4e0-103">comando config (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5c4e0-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="5c4e0-104">**Aplica-se a:** todas as &bullet; **versões com suporte**: todas</span><span class="sxs-lookup"><span data-stu-id="5c4e0-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="5c4e0-105">Obtém ou define os valores de configuração do NuGet.</span><span class="sxs-lookup"><span data-stu-id="5c4e0-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="5c4e0-106">Para uso adicional, consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="5c4e0-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="5c4e0-107">Para obter detalhes sobre nomes de chave permitidos, consulte a [referência do arquivo de configuração do NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="5c4e0-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="5c4e0-108">Uso</span><span class="sxs-lookup"><span data-stu-id="5c4e0-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="5c4e0-109">onde `<name>` e `<value>` especifique um par chave-valor a ser definido na configuração.</span><span class="sxs-lookup"><span data-stu-id="5c4e0-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="5c4e0-110">Você pode especificar quantos pares desejar.</span><span class="sxs-lookup"><span data-stu-id="5c4e0-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="5c4e0-111">Para remover um valor, especifique o nome e o `=` sinal, mas nenhum valor.</span><span class="sxs-lookup"><span data-stu-id="5c4e0-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="5c4e0-112">Para nomes de chave permitidos, consulte a [referência do arquivo de configuração do NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="5c4e0-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="5c4e0-113">No NuGet 3.4 +, o `<value>` pode usar [variáveis de ambiente](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="5c4e0-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="5c4e0-114">Opções</span><span class="sxs-lookup"><span data-stu-id="5c4e0-114">Options</span></span>


- **`AsPath`**

  <span data-ttu-id="5c4e0-115">Retorna o valor de configuração como um caminho, ignorado quando `-Set` é usado.</span><span class="sxs-lookup"><span data-stu-id="5c4e0-115">Returns the config value as a path, ignored when `-Set` is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="5c4e0-116">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="5c4e0-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5c4e0-117">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="5c4e0-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="5c4e0-118">*(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="5c4e0-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="5c4e0-119">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="5c4e0-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="5c4e0-120">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="5c4e0-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-Set`**

  <span data-ttu-id="5c4e0-121">Um em mais pares chave-valor a ser definido na configuração.</span><span class="sxs-lookup"><span data-stu-id="5c4e0-121">One on more key-value pairs to be set in config.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="5c4e0-122">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="5c4e0-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="5c4e0-123">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5c4e0-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="5c4e0-124">Exemplos</span><span class="sxs-lookup"><span data-stu-id="5c4e0-124">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
