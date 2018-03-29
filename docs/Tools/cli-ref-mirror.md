---
title: Comando de espelho do NuGet CLI | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referência para o comando de espelho nuget.exe
keywords: referência de espelho do NuGet, comando de espelho
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 512bd72d568cda81eb7c6a1555c36ead66b5c438
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="bcf15-104">comando de espelho (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="bcf15-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="bcf15-105">**Aplica-se a:** pacote publicação &bullet; **versões com suporte:** preterido no 3.2 +</span><span class="sxs-lookup"><span data-stu-id="bcf15-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="bcf15-106">Reflete um pacote e suas dependências de repositórios de origem especificado para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="bcf15-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="bcf15-107">Para habilitar esse comando para versões do NuGet antes 3.2, vá para [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), selecione a versão estável mais recente, baixe `NuGet.ServerExtensions.dll` e `Nuget-Signed.exe` para seu disco local e renomear `Nuget-Signed.exe` para `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="bcf15-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="bcf15-108">Uso</span><span class="sxs-lookup"><span data-stu-id="bcf15-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="bcf15-109">onde `<packageID>` é o pacote para o espelho, ou `<configFilePath>` identifica o `packages.config` arquivo que lista os pacotes para espelhar.</span><span class="sxs-lookup"><span data-stu-id="bcf15-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="bcf15-110">O `<listUrlTarget>` Especifica o repositório de origem e `<publishUrlTarget>` Especifica o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="bcf15-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="bcf15-111">Se o repositório de destino estiver em `https://machine/repo` que está executando o [NuGet.Server](../hosting-packages/nuget-server.md), as urls de lista e enviar por push será `https://machine/repo/nuget` e `https://machine/repo/api/v2/package`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="bcf15-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="bcf15-112">Opções</span><span class="sxs-lookup"><span data-stu-id="bcf15-112">Options</span></span>

| <span data-ttu-id="bcf15-113">Opção</span><span class="sxs-lookup"><span data-stu-id="bcf15-113">Option</span></span> | <span data-ttu-id="bcf15-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="bcf15-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bcf15-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="bcf15-115">ApiKey</span></span> | <span data-ttu-id="bcf15-116">A chave de API para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="bcf15-116">The API key for the target repository.</span></span> <span data-ttu-id="bcf15-117">Se não estiverem presentes, o especificado no arquivo de configuração é usado (`%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Linux/Mac)).</span><span class="sxs-lookup"><span data-stu-id="bcf15-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="bcf15-118">Ajuda</span><span class="sxs-lookup"><span data-stu-id="bcf15-118">Help</span></span> | <span data-ttu-id="bcf15-119">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="bcf15-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="bcf15-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="bcf15-120">NoCache</span></span> | <span data-ttu-id="bcf15-121">Impede que o NuGet usando pacotes armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="bcf15-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="bcf15-122">Consulte [Gerenciando os pacotes globais e as pastas do cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="bcf15-122">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="bcf15-123">NOOP</span><span class="sxs-lookup"><span data-stu-id="bcf15-123">Noop</span></span> | <span data-ttu-id="bcf15-124">Registra o que deve ser feito, mas não executa as ações; assume o sucesso para operações de envio por push.</span><span class="sxs-lookup"><span data-stu-id="bcf15-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="bcf15-125">Versão de pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="bcf15-125">PreRelease</span></span> | <span data-ttu-id="bcf15-126">Inclui pacotes pré-lançados na operação de espelhamento.</span><span class="sxs-lookup"><span data-stu-id="bcf15-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="bcf15-127">Origem</span><span class="sxs-lookup"><span data-stu-id="bcf15-127">Source</span></span> | <span data-ttu-id="bcf15-128">Uma lista de fontes de pacote para espelhar.</span><span class="sxs-lookup"><span data-stu-id="bcf15-128">A list of package sources to mirror.</span></span> <span data-ttu-id="bcf15-129">Se nenhuma fonte for especificada, aqueles definidos no arquivo de configuração (consulte ApiKey acima) são usados, padronizando para nuget.org se nenhum for especificado.</span><span class="sxs-lookup"><span data-stu-id="bcf15-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="bcf15-130">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="bcf15-130">Timeout</span></span> | <span data-ttu-id="bcf15-131">Especifica o tempo limite, em segundos, para enviar por push para um servidor.</span><span class="sxs-lookup"><span data-stu-id="bcf15-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="bcf15-132">O padrão é 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="bcf15-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="bcf15-133">Versão</span><span class="sxs-lookup"><span data-stu-id="bcf15-133">Version</span></span> | <span data-ttu-id="bcf15-134">A versão do pacote para instalação.</span><span class="sxs-lookup"><span data-stu-id="bcf15-134">The version of the package to install.</span></span> <span data-ttu-id="bcf15-135">Se não for especificado, a versão mais recente é espelhada.</span><span class="sxs-lookup"><span data-stu-id="bcf15-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="bcf15-136">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="bcf15-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="bcf15-137">Exemplos</span><span class="sxs-lookup"><span data-stu-id="bcf15-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
