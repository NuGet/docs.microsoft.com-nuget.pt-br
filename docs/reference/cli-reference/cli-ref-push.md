---
title: Comando Push da CLI do NuGet
description: Referência para o comando de push NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327623"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="043e2-103">comando push (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="043e2-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="043e2-104">**Aplica-se a:** &bullet; **versões com suporte** para publicação de pacotes: tudo; 4.1.0 + obrigatório para NuGet.org</span><span class="sxs-lookup"><span data-stu-id="043e2-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="043e2-105">Para enviar pacotes por push para o nuget.org, você deve usar NuGet. exe v 4.1.0 +, que implementa os [protocolos NuGet](../../api/nuget-protocols.md)necessários.</span><span class="sxs-lookup"><span data-stu-id="043e2-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="043e2-106">Envia por push um pacote para uma origem de pacote e o publica.</span><span class="sxs-lookup"><span data-stu-id="043e2-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="043e2-107">A configuração padrão do NuGet é obtida carregando `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), carregando os `Nuget.Config` arquivos ou `.nuget\Nuget.Config` iniciando na raiz da unidade e terminando no diretório atual (consulte [NuGet comum configurações](../../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="043e2-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="043e2-108">Uso</span><span class="sxs-lookup"><span data-stu-id="043e2-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="043e2-109">onde `<packagePath>` o identifica o pacote a ser enviado por push para o servidor.</span><span class="sxs-lookup"><span data-stu-id="043e2-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="043e2-110">Opções</span><span class="sxs-lookup"><span data-stu-id="043e2-110">Options</span></span>

| <span data-ttu-id="043e2-111">Opção</span><span class="sxs-lookup"><span data-stu-id="043e2-111">Option</span></span> | <span data-ttu-id="043e2-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="043e2-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="043e2-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="043e2-113">ApiKey</span></span> | <span data-ttu-id="043e2-114">A chave de API para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="043e2-114">The API key for the target repository.</span></span> <span data-ttu-id="043e2-115">Se não estiver presente, o especificado no arquivo de configuração será usado.</span><span class="sxs-lookup"><span data-stu-id="043e2-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="043e2-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="043e2-116">ConfigFile</span></span> | <span data-ttu-id="043e2-117">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="043e2-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="043e2-118">Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="043e2-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="043e2-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="043e2-119">DisableBuffering</span></span> | <span data-ttu-id="043e2-120">Desabilita o armazenamento em buffer ao enviar por push para um servidor HTTP (s) para diminuir os usos de memória.</span><span class="sxs-lookup"><span data-stu-id="043e2-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="043e2-121">Cuidado: quando essa opção é usada, a autenticação integrada do Windows pode não funcionar.</span><span class="sxs-lookup"><span data-stu-id="043e2-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="043e2-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="043e2-122">ForceEnglishOutput</span></span> | <span data-ttu-id="043e2-123">*(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="043e2-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="043e2-124">Help</span><span class="sxs-lookup"><span data-stu-id="043e2-124">Help</span></span> | <span data-ttu-id="043e2-125">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="043e2-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="043e2-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="043e2-126">NonInteractive</span></span> | <span data-ttu-id="043e2-127">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="043e2-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="043e2-128">Nosymbols</span><span class="sxs-lookup"><span data-stu-id="043e2-128">NoSymbols</span></span> | <span data-ttu-id="043e2-129">*(3,5 +)* Se existir um pacote de símbolos, ele não será enviado por push para um servidor de símbolos.</span><span class="sxs-lookup"><span data-stu-id="043e2-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="043e2-130">Origem</span><span class="sxs-lookup"><span data-stu-id="043e2-130">Source</span></span> | <span data-ttu-id="043e2-131">Especifica a URL do servidor.</span><span class="sxs-lookup"><span data-stu-id="043e2-131">Specifies the server URL.</span></span> <span data-ttu-id="043e2-132">O NuGet identifica uma origem UNC ou de pasta local e simplesmente copia o arquivo em vez de enviá-lo por push usando HTTP.</span><span class="sxs-lookup"><span data-stu-id="043e2-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="043e2-133">Além disso, começando com o NuGet 3.4.2, esse é um parâmetro obrigatório `NuGet.Config` , a menos que o arquivo especifique um valor defaultpushe (consulte Configurando o [comportamento do NuGet](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="043e2-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="043e2-134">SkipDuplicate</span><span class="sxs-lookup"><span data-stu-id="043e2-134">SkipDuplicate</span></span> | <span data-ttu-id="043e2-135">*(5.1 +)* Se já existir um pacote e uma versão, pule-o e continue com o próximo pacote no envio por push, se houver.</span><span class="sxs-lookup"><span data-stu-id="043e2-135">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="043e2-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="043e2-136">SymbolSource</span></span> | <span data-ttu-id="043e2-137">*(3,5 +)* Especifica a URL do servidor de símbolos; nuget.smbsrc.net é usado ao enviar para nuget.org</span><span class="sxs-lookup"><span data-stu-id="043e2-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="043e2-138">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="043e2-138">SymbolApiKey</span></span> | <span data-ttu-id="043e2-139">*(3,5 +)* Especifica a chave de API para a URL especificada `-SymbolSource`em.</span><span class="sxs-lookup"><span data-stu-id="043e2-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="043e2-140">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="043e2-140">Timeout</span></span> | <span data-ttu-id="043e2-141">Especifica o tempo limite, em segundos, para envio por push para um servidor.</span><span class="sxs-lookup"><span data-stu-id="043e2-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="043e2-142">O padrão é 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="043e2-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="043e2-143">Verbosity</span><span class="sxs-lookup"><span data-stu-id="043e2-143">Verbosity</span></span> | <span data-ttu-id="043e2-144">Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*.</span><span class="sxs-lookup"><span data-stu-id="043e2-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="043e2-145">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="043e2-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="043e2-146">Exemplos</span><span class="sxs-lookup"><span data-stu-id="043e2-146">Examples</span></span>

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
