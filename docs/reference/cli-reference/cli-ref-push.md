---
title: Comando Push da CLI do NuGet
description: Referência para o comando nuget.exe push
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d53a2e7f41219e68e59b195d1d5a9d1f62ad7c63
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622838"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="a2d19-103">comando push (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a2d19-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="a2d19-104">**Aplica-se a:** &bullet; **versões com suporte** para publicação de pacotes: tudo; 4.1.0 + obrigatório para NuGet.org</span><span class="sxs-lookup"><span data-stu-id="a2d19-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="a2d19-105">Para enviar pacotes por push para o nuget.org, você deve usar nuget.exe v 4.1.0 +, que implementa os [protocolos do NuGet](../../api/nuget-protocols.md)necessários.</span><span class="sxs-lookup"><span data-stu-id="a2d19-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="a2d19-106">Envia por push um pacote para uma origem de pacote e o publica.</span><span class="sxs-lookup"><span data-stu-id="a2d19-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="a2d19-107">A configuração padrão do NuGet é obtida carregando `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) e, em seguida, carregando qualquer `Nuget.Config` `.nuget\Nuget.Config` arquivo ou iniciando da raiz da unidade e terminando no diretório atual (consulte [configurações comuns do NuGet](../../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="a2d19-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="a2d19-108">Uso</span><span class="sxs-lookup"><span data-stu-id="a2d19-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="a2d19-109">onde `<packagePath>` o identifica o pacote a ser enviado por push para o servidor.</span><span class="sxs-lookup"><span data-stu-id="a2d19-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="a2d19-110">Opções</span><span class="sxs-lookup"><span data-stu-id="a2d19-110">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="a2d19-111">A chave de API para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="a2d19-111">The API key for the target repository.</span></span> <span data-ttu-id="a2d19-112">Se não estiver presente, o especificado no arquivo de configuração será usado.</span><span class="sxs-lookup"><span data-stu-id="a2d19-112">If not present,  the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="a2d19-113">O arquivo de configuração do NuGet a ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="a2d19-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a2d19-114">Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.</span><span class="sxs-lookup"><span data-stu-id="a2d19-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DisableBuffering`**

  <span data-ttu-id="a2d19-115">Desabilita o armazenamento em buffer ao enviar por push para um servidor HTTP (s) para diminuir os usos de memória.</span><span class="sxs-lookup"><span data-stu-id="a2d19-115">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="a2d19-116">Cuidado: quando essa opção é usada, a autenticação integrada do Windows pode não funcionar.</span><span class="sxs-lookup"><span data-stu-id="a2d19-116">Caution: when this option is used, integrated Windows authentication might not work.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="a2d19-117">*(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.</span><span class="sxs-lookup"><span data-stu-id="a2d19-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a2d19-118">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="a2d19-118">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a2d19-119">Suprime prompts de entrada ou confirmações do usuário.</span><span class="sxs-lookup"><span data-stu-id="a2d19-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoServiceEndpoint`**

  <span data-ttu-id="a2d19-120">Não acrescenta `api/v2/packages` à URL de origem.</span><span class="sxs-lookup"><span data-stu-id="a2d19-120">Does not append `api/v2/packages` to the source URL.</span></span>

- **`-NoSymbols`**

  <span data-ttu-id="a2d19-121">*(3,5 +)* Se existir um pacote de símbolos, ele não será enviado por push para um servidor de símbolos.</span><span class="sxs-lookup"><span data-stu-id="a2d19-121">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="a2d19-122">Especifica a URL do servidor.</span><span class="sxs-lookup"><span data-stu-id="a2d19-122">Specifies the server URL.</span></span> <span data-ttu-id="a2d19-123">O NuGet identifica uma origem UNC ou de pasta local e simplesmente copia o arquivo em vez de enviá-lo por push usando HTTP.</span><span class="sxs-lookup"><span data-stu-id="a2d19-123">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="a2d19-124">Além disso, começando com o NuGet 3.4.2, esse é um parâmetro obrigatório, a menos que o `NuGet.Config` arquivo especifique um valor *defaultpushe* (consulte [Configurando o comportamento do NuGet](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="a2d19-124">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span>

- **`-SkipDuplicate`**

  <span data-ttu-id="a2d19-125">*(5.1 +)* Se já existir um pacote e uma versão, pule-o e continue com o próximo pacote no envio por push, se houver.</span><span class="sxs-lookup"><span data-stu-id="a2d19-125">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span>

- **`-SymbolSource`**

  <span data-ttu-id="a2d19-126">*(3,5 +)* Especifica a URL do servidor de símbolos; nuget.smbsrc.net é usado ao enviar para nuget.org</span><span class="sxs-lookup"><span data-stu-id="a2d19-126">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span>

- **`-SymbolApiKey`**

  <span data-ttu-id="a2d19-127">*(3,5 +)* Especifica a chave de API para a URL especificada em `-SymbolSource` .</span><span class="sxs-lookup"><span data-stu-id="a2d19-127">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span>

- **`-Timeout`**

  <span data-ttu-id="a2d19-128">Especifica o tempo limite, em segundos, para envio por push para um servidor.</span><span class="sxs-lookup"><span data-stu-id="a2d19-128">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="a2d19-129"> O padrão é 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="a2d19-129">The default is 300 seconds (5 minutes).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a2d19-130">Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .</span><span class="sxs-lookup"><span data-stu-id="a2d19-130">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


<span data-ttu-id="a2d19-131">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a2d19-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a2d19-132">Exemplos</span><span class="sxs-lookup"><span data-stu-id="a2d19-132">Examples</span></span>

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
