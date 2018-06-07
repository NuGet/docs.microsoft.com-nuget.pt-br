---
title: Comando de envio por push do NuGet CLI
description: Referência para o comando de envio de nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 05cafa981ecf42829d1b3d8b8988ed51449d9d86
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817185"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="a3ed7-103">comando de envio (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a3ed7-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="a3ed7-104">**Aplica-se a:** pacote publicação &bullet; **versões com suporte:** todos; 4.1.0+ necessário para nuget.org</span><span class="sxs-lookup"><span data-stu-id="a3ed7-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="a3ed7-105">Para enviar pacotes para nuget.org, você deve usar nuget.exe v4.1.0 +, que implementa o necessária [NuGet protocolos](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="a3ed7-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="a3ed7-106">Envia um pacote para uma origem de pacote e o publica.</span><span class="sxs-lookup"><span data-stu-id="a3ed7-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="a3ed7-107">Configuração de padrão do NuGet é obtida Carregando `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac Linux), em seguida, carregar qualquer `Nuget.Config` ou `.nuget\Nuget.Config` arquivos a partir da raiz da unidade e terminando no diretório atual (consulte [Configurando Comportamento do NuGet](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="a3ed7-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="a3ed7-108">Uso</span><span class="sxs-lookup"><span data-stu-id="a3ed7-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="a3ed7-109">onde `<packagePath>` identifica o pacote para enviar por push para o servidor.</span><span class="sxs-lookup"><span data-stu-id="a3ed7-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="a3ed7-110">Opções</span><span class="sxs-lookup"><span data-stu-id="a3ed7-110">Options</span></span>

| <span data-ttu-id="a3ed7-111">Opção</span><span class="sxs-lookup"><span data-stu-id="a3ed7-111">Option</span></span> | <span data-ttu-id="a3ed7-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="a3ed7-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a3ed7-113">apiKey</span><span class="sxs-lookup"><span data-stu-id="a3ed7-113">ApiKey</span></span> | <span data-ttu-id="a3ed7-114">A chave de API para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="a3ed7-114">The API key for the target repository.</span></span> <span data-ttu-id="a3ed7-115">Se não estiver presente, o especificado no arquivo de configuração é usado.</span><span class="sxs-lookup"><span data-stu-id="a3ed7-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="a3ed7-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a3ed7-116">ConfigFile</span></span> | <span data-ttu-id="a3ed7-117">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="a3ed7-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a3ed7-118">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="a3ed7-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a3ed7-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="a3ed7-119">DisableBuffering</span></span> | <span data-ttu-id="a3ed7-120">Desabilita o buffer de envio por push para um servidor HTTP (s) para diminuir o uso de memória.</span><span class="sxs-lookup"><span data-stu-id="a3ed7-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="a3ed7-121">Cuidado: quando esta opção for usada, a autenticação integrada do Windows pode não funcionar.</span><span class="sxs-lookup"><span data-stu-id="a3ed7-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="a3ed7-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a3ed7-122">ForceEnglishOutput</span></span> | <span data-ttu-id="a3ed7-123">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="a3ed7-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a3ed7-124">Ajuda</span><span class="sxs-lookup"><span data-stu-id="a3ed7-124">Help</span></span> | <span data-ttu-id="a3ed7-125">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="a3ed7-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="a3ed7-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a3ed7-126">NonInteractive</span></span> | <span data-ttu-id="a3ed7-127">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="a3ed7-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a3ed7-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="a3ed7-128">NoSymbols</span></span> | <span data-ttu-id="a3ed7-129">*(3.5 +)*  Se existe um pacote de símbolos, ele não será enviado a um servidor de símbolos.</span><span class="sxs-lookup"><span data-stu-id="a3ed7-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="a3ed7-130">Origem</span><span class="sxs-lookup"><span data-stu-id="a3ed7-130">Source</span></span> | <span data-ttu-id="a3ed7-131">Especifica a URL do servidor.</span><span class="sxs-lookup"><span data-stu-id="a3ed7-131">Specifies the server URL.</span></span> <span data-ttu-id="a3ed7-132">NuGet identifica um UNC ou uma fonte de pasta local e simplesmente copia o arquivo em vez de enviar por push usando HTTP.</span><span class="sxs-lookup"><span data-stu-id="a3ed7-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="a3ed7-133">Além disso, a partir do NuGet 3.4.2, este parâmetro é obrigatório, a menos que o `NuGet.Config` arquivo Especifica um *DefaultPushSource* valor (consulte [NuGet Configurando comportamento](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="a3ed7-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="a3ed7-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="a3ed7-134">SymbolSource</span></span> | <span data-ttu-id="a3ed7-135">*(3.5 +)*  Especifica a URL do servidor de símbolo; nuget.smbsrc.net é usado ao enviar para nuget.org</span><span class="sxs-lookup"><span data-stu-id="a3ed7-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="a3ed7-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="a3ed7-136">SymbolApiKey</span></span> | <span data-ttu-id="a3ed7-137">*(3.5 +)*  Especifica a chave de API para a URL especificada em `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="a3ed7-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="a3ed7-138">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="a3ed7-138">Timeout</span></span> | <span data-ttu-id="a3ed7-139">Especifica o tempo limite, em segundos, para enviar por push para um servidor.</span><span class="sxs-lookup"><span data-stu-id="a3ed7-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="a3ed7-140">O padrão é 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="a3ed7-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="a3ed7-141">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="a3ed7-141">Verbosity</span></span> | <span data-ttu-id="a3ed7-142">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="a3ed7-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a3ed7-143">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a3ed7-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a3ed7-144">Exemplos</span><span class="sxs-lookup"><span data-stu-id="a3ed7-144">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
