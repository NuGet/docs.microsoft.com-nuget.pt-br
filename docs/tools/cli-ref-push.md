---
title: Comando do CLI do NuGet push
description: Referência do comando de envio por push nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bce04864224a66019a52cdfff8355f68dc424204
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65974998"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="14208-103">envio por push de comando (CLI do NuGet)</span><span class="sxs-lookup"><span data-stu-id="14208-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="14208-104">**Aplica-se a:** publicação de pacote &bullet; **versões com suporte:** todos os; 4.1.0 + necessários para o nuget.org</span><span class="sxs-lookup"><span data-stu-id="14208-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="14208-105">Enviar pacotes para nuget.org, você deve usar nuget.exe verze 4.1.0 +, que implementa o necessária [protocolos NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="14208-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="14208-106">Envia um pacote para uma origem de pacote e os publica.</span><span class="sxs-lookup"><span data-stu-id="14208-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="14208-107">Configuração de padrão do NuGet é obtida ao carregar `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), em seguida, carregar qualquer `Nuget.Config` ou `.nuget\Nuget.Config` arquivos a partir da raiz da unidade e terminar no diretório atual (consulte [Configurando O comportamento do NuGet](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="14208-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="14208-108">Uso</span><span class="sxs-lookup"><span data-stu-id="14208-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="14208-109">onde `<packagePath>` identifica o pacote para enviar por push para o servidor.</span><span class="sxs-lookup"><span data-stu-id="14208-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="14208-110">Opções</span><span class="sxs-lookup"><span data-stu-id="14208-110">Options</span></span>

| <span data-ttu-id="14208-111">Opção</span><span class="sxs-lookup"><span data-stu-id="14208-111">Option</span></span> | <span data-ttu-id="14208-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="14208-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="14208-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="14208-113">ApiKey</span></span> | <span data-ttu-id="14208-114">A chave de API para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="14208-114">The API key for the target repository.</span></span> <span data-ttu-id="14208-115">Se não estiver presente, aquele especificado no arquivo de configuração será usada.</span><span class="sxs-lookup"><span data-stu-id="14208-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="14208-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="14208-116">ConfigFile</span></span> | <span data-ttu-id="14208-117">O arquivo de configuração do NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="14208-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="14208-118">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.</span><span class="sxs-lookup"><span data-stu-id="14208-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="14208-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="14208-119">DisableBuffering</span></span> | <span data-ttu-id="14208-120">Desabilita o armazenamento em buffer ao enviar por push a um servidor HTTP (s) para diminuir o uso de memória.</span><span class="sxs-lookup"><span data-stu-id="14208-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="14208-121">Cuidado: quando esta opção for usada, a autenticação integrada do Windows pode não funcionar.</span><span class="sxs-lookup"><span data-stu-id="14208-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="14208-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="14208-122">ForceEnglishOutput</span></span> | <span data-ttu-id="14208-123">*(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês.</span><span class="sxs-lookup"><span data-stu-id="14208-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="14208-124">Help</span><span class="sxs-lookup"><span data-stu-id="14208-124">Help</span></span> | <span data-ttu-id="14208-125">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="14208-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="14208-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="14208-126">NonInteractive</span></span> | <span data-ttu-id="14208-127">Suprime a solicitações de entrada do usuário ou confirmações.</span><span class="sxs-lookup"><span data-stu-id="14208-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="14208-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="14208-128">NoSymbols</span></span> | <span data-ttu-id="14208-129">*(3.5 ou superior)*  Se existe um pacote de símbolos, ele não será enviado a um servidor de símbolos.</span><span class="sxs-lookup"><span data-stu-id="14208-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="14208-130">Origem</span><span class="sxs-lookup"><span data-stu-id="14208-130">Source</span></span> | <span data-ttu-id="14208-131">Especifica a URL do servidor.</span><span class="sxs-lookup"><span data-stu-id="14208-131">Specifies the server URL.</span></span> <span data-ttu-id="14208-132">O NuGet identifica um UNC ou uma fonte de pasta local e simplesmente copia o arquivo em vez de enviá-la usando HTTP.</span><span class="sxs-lookup"><span data-stu-id="14208-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="14208-133">Além disso, começando com o NuGet 3.4.2, este parâmetro é obrigatório, a menos que o `NuGet.Config` arquivo Especifica um *DefaultPushSource* valor (consulte [o comportamento do NuGet configurando](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="14208-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="14208-134">SkipDuplicate</span><span class="sxs-lookup"><span data-stu-id="14208-134">SkipDuplicate</span></span> | <span data-ttu-id="14208-135">Se já existe um pacote e versão, ignorá-la e continuar com o próximo pacote no envio, se houver.</span><span class="sxs-lookup"><span data-stu-id="14208-135">If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="14208-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="14208-136">SymbolSource</span></span> | <span data-ttu-id="14208-137">*(3.5 ou superior)*  Especifica a URL do servidor de símbolo; nuget.smbsrc.net é usado ao enviar por push para nuget.org</span><span class="sxs-lookup"><span data-stu-id="14208-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="14208-138">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="14208-138">SymbolApiKey</span></span> | <span data-ttu-id="14208-139">*(3.5 ou superior)*  Especifica a chave de API para a URL especificada no `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="14208-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="14208-140">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="14208-140">Timeout</span></span> | <span data-ttu-id="14208-141">Especifica o tempo limite, em segundos, para enviar por push a um servidor.</span><span class="sxs-lookup"><span data-stu-id="14208-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="14208-142">O padrão é 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="14208-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="14208-143">Verbosity</span><span class="sxs-lookup"><span data-stu-id="14208-143">Verbosity</span></span> | <span data-ttu-id="14208-144">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*.</span><span class="sxs-lookup"><span data-stu-id="14208-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="14208-145">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="14208-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="14208-146">Exemplos</span><span class="sxs-lookup"><span data-stu-id="14208-146">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
