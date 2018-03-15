---
title: Comando de envio por push do NuGet CLI | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência para o comando de envio de nuget.exe"
keywords: "referência de push NuGet, o comando de envio"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 095e81406df3db5fbfc6c5202362894b2c6d7cf8
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2018
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="de22a-104">comando de envio (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="de22a-104">push command (NuGet CLI)</span></span>

<span data-ttu-id="de22a-105">**Aplica-se a:** pacote publicação &bullet; **versões com suporte:** todos; 4.1.0+ necessário para nuget.org</span><span class="sxs-lookup"><span data-stu-id="de22a-105">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="de22a-106">Para enviar pacotes para nuget.org, você deve usar nuget.exe v4.1.0 +, que implementa o necessária [NuGet protocolos](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="de22a-106">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="de22a-107">Envia um pacote para uma origem de pacote e o publica.</span><span class="sxs-lookup"><span data-stu-id="de22a-107">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="de22a-108">Configuração de padrão do NuGet é obtida Carregando `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac Linux), em seguida, carregar qualquer `Nuget.Config` ou `.nuget\Nuget.Config` arquivos a partir da raiz da unidade e terminando no diretório atual (consulte [Configurando Comportamento do NuGet](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="de22a-108">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="de22a-109">Uso</span><span class="sxs-lookup"><span data-stu-id="de22a-109">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="de22a-110">onde `<packagePath>` identifica o pacote para enviar por push para o servidor.</span><span class="sxs-lookup"><span data-stu-id="de22a-110">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="de22a-111">Opções</span><span class="sxs-lookup"><span data-stu-id="de22a-111">Options</span></span>

| <span data-ttu-id="de22a-112">Opção</span><span class="sxs-lookup"><span data-stu-id="de22a-112">Option</span></span> | <span data-ttu-id="de22a-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="de22a-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de22a-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="de22a-114">ApiKey</span></span> | <span data-ttu-id="de22a-115">A chave de API para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="de22a-115">The API key for the target repository.</span></span> <span data-ttu-id="de22a-116">Se não estiver presente, o especificado no arquivo de configuração é usado.</span><span class="sxs-lookup"><span data-stu-id="de22a-116">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="de22a-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="de22a-117">ConfigFile</span></span> | <span data-ttu-id="de22a-118">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="de22a-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="de22a-119">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="de22a-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="de22a-120">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="de22a-120">DisableBuffering</span></span> | <span data-ttu-id="de22a-121">Desabilita o buffer de envio por push para um servidor HTTP (s) para diminuir o uso de memória.</span><span class="sxs-lookup"><span data-stu-id="de22a-121">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="de22a-122">Cuidado: quando esta opção for usada, a autenticação integrada do Windows pode não funcionar.</span><span class="sxs-lookup"><span data-stu-id="de22a-122">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="de22a-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="de22a-123">ForceEnglishOutput</span></span> | <span data-ttu-id="de22a-124">*(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="de22a-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="de22a-125">Ajuda</span><span class="sxs-lookup"><span data-stu-id="de22a-125">Help</span></span> | <span data-ttu-id="de22a-126">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="de22a-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="de22a-127">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="de22a-127">NonInteractive</span></span> | <span data-ttu-id="de22a-128">Suprime avisos para a entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="de22a-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="de22a-129">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="de22a-129">NoSymbols</span></span> | <span data-ttu-id="de22a-130">*(3.5 +)*  Se existe um pacote de símbolos, ele não será enviado a um servidor de símbolos.</span><span class="sxs-lookup"><span data-stu-id="de22a-130">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="de22a-131">Origem</span><span class="sxs-lookup"><span data-stu-id="de22a-131">Source</span></span> | <span data-ttu-id="de22a-132">Especifica a URL do servidor.</span><span class="sxs-lookup"><span data-stu-id="de22a-132">Specifies the server URL.</span></span> <span data-ttu-id="de22a-133">NuGet identifica um UNC ou uma fonte de pasta local e simplesmente copia o arquivo em vez de enviar por push usando HTTP.</span><span class="sxs-lookup"><span data-stu-id="de22a-133">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="de22a-134">Além disso, a partir do NuGet 3.4.2, este parâmetro é obrigatório, a menos que o `NuGet.Config` arquivo Especifica um *DefaultPushSource* valor (consulte [NuGet Configurando comportamento](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="de22a-134">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="de22a-135">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="de22a-135">SymbolSource</span></span> | <span data-ttu-id="de22a-136">*(3.5 +)*  Especifica a URL do servidor de símbolo; nuget.smbsrc.net é usado ao enviar para nuget.org</span><span class="sxs-lookup"><span data-stu-id="de22a-136">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="de22a-137">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="de22a-137">SymbolApiKey</span></span> | <span data-ttu-id="de22a-138">*(3.5 +)*  Especifica a chave de API para a URL especificada em `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="de22a-138">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="de22a-139">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="de22a-139">Timeout</span></span> | <span data-ttu-id="de22a-140">Especifica o tempo limite, em segundos, para enviar por push para um servidor.</span><span class="sxs-lookup"><span data-stu-id="de22a-140">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="de22a-141">O padrão é 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="de22a-141">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="de22a-142">Detalhamento</span><span class="sxs-lookup"><span data-stu-id="de22a-142">Verbosity</span></span> | <span data-ttu-id="de22a-143">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="de22a-143">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="de22a-144">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="de22a-144">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="de22a-145">Exemplos</span><span class="sxs-lookup"><span data-stu-id="de22a-145">Examples</span></span>

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
