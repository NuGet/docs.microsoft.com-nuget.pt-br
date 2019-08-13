---
title: Comando de espelhamento da CLI do NuGet
description: Referência para o comando de espelho NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 81866172bfbf55c42ee96c213c0117f1f986235c
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959720"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="6b8cf-103">Commando mirror (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6b8cf-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="6b8cf-104">**Aplica-se a:** &bullet; **versões com suporte** para publicação de pacotes: preterida em 3.2 +</span><span class="sxs-lookup"><span data-stu-id="6b8cf-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="6b8cf-105">Espelha um pacote e suas dependências dos repositórios de origem especificados para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="6b8cf-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="6b8cf-106">NuGet. ServerExtensions. dll e NuGet-Signed. exe que anteriormente tinham suporte para esse comando no NuGet 2. x (renomeando NuGet-Signed. exe para NuGet. exe) não estão mais disponíveis para download.</span><span class="sxs-lookup"><span data-stu-id="6b8cf-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="6b8cf-107">Para usar um comando semelhante a este, tente [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span><span class="sxs-lookup"><span data-stu-id="6b8cf-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="6b8cf-108">Uso</span><span class="sxs-lookup"><span data-stu-id="6b8cf-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="6b8cf-109">em `<packageID>` que é o pacote a ser espelhado ou `packages.config` `<configFilePath>` identifica o arquivo que lista os pacotes a serem espelhados.</span><span class="sxs-lookup"><span data-stu-id="6b8cf-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="6b8cf-110">O `<listUrlTarget>` especifica o repositório de origem e `<publishUrlTarget>` especifica o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="6b8cf-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="6b8cf-111">Se o seu repositório de destino `https://machine/repo` estiver no que está executando o [NuGet. Server](../../hosting-packages/nuget-server.md), a lista e as `https://machine/repo/nuget` URLs `https://machine/repo/api/v2/package`de push serão e, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="6b8cf-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="6b8cf-112">Opções</span><span class="sxs-lookup"><span data-stu-id="6b8cf-112">Options</span></span>

| <span data-ttu-id="6b8cf-113">Opção</span><span class="sxs-lookup"><span data-stu-id="6b8cf-113">Option</span></span> | <span data-ttu-id="6b8cf-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="6b8cf-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6b8cf-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="6b8cf-115">ApiKey</span></span> | <span data-ttu-id="6b8cf-116">A chave de API para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="6b8cf-116">The API key for the target repository.</span></span> <span data-ttu-id="6b8cf-117">Se não estiver presente, o especificado no arquivo de configuração será usado (`%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="6b8cf-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="6b8cf-118">Ajuda</span><span class="sxs-lookup"><span data-stu-id="6b8cf-118">Help</span></span> | <span data-ttu-id="6b8cf-119">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="6b8cf-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="6b8cf-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="6b8cf-120">NoCache</span></span> | <span data-ttu-id="6b8cf-121">Impede que o NuGet use pacotes armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="6b8cf-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="6b8cf-122">Consulte [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="6b8cf-122">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="6b8cf-123">NOOP</span><span class="sxs-lookup"><span data-stu-id="6b8cf-123">Noop</span></span> | <span data-ttu-id="6b8cf-124">Registra o que seria feito, mas não executa as ações; pressupõe êxito para operações de envio por push.</span><span class="sxs-lookup"><span data-stu-id="6b8cf-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="6b8cf-125">Pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="6b8cf-125">PreRelease</span></span> | <span data-ttu-id="6b8cf-126">Inclui pacotes de pré-lançamento na operação de espelhamento.</span><span class="sxs-lookup"><span data-stu-id="6b8cf-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="6b8cf-127">Origem</span><span class="sxs-lookup"><span data-stu-id="6b8cf-127">Source</span></span> | <span data-ttu-id="6b8cf-128">Uma lista de origens do pacote a ser espelhada.</span><span class="sxs-lookup"><span data-stu-id="6b8cf-128">A list of package sources to mirror.</span></span> <span data-ttu-id="6b8cf-129">Se nenhuma fonte for especificada, as definidas no arquivo de configuração (consulte ApiKey acima) serão usadas, padronizando para nuget.org se nenhuma for especificada.</span><span class="sxs-lookup"><span data-stu-id="6b8cf-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="6b8cf-130">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="6b8cf-130">Timeout</span></span> | <span data-ttu-id="6b8cf-131">Especifica o tempo limite, em segundos, para envio por push para um servidor.</span><span class="sxs-lookup"><span data-stu-id="6b8cf-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="6b8cf-132">O padrão é 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="6b8cf-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="6b8cf-133">Versão</span><span class="sxs-lookup"><span data-stu-id="6b8cf-133">Version</span></span> | <span data-ttu-id="6b8cf-134">A versão do pacote a ser instalado.</span><span class="sxs-lookup"><span data-stu-id="6b8cf-134">The version of the package to install.</span></span> <span data-ttu-id="6b8cf-135">Se não for especificado, a versão mais recente será espelhada.</span><span class="sxs-lookup"><span data-stu-id="6b8cf-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="6b8cf-136">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6b8cf-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6b8cf-137">Exemplos</span><span class="sxs-lookup"><span data-stu-id="6b8cf-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
