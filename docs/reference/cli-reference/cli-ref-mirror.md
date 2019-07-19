---
title: Comando de espelhamento da CLI do NuGet
description: Referência para o comando de espelho NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327663"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="854a7-103">Commando mirror (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="854a7-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="854a7-104">**Aplica-se a:** &bullet; **versões com suporte** para publicação de pacotes: preterida em 3.2 +</span><span class="sxs-lookup"><span data-stu-id="854a7-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="854a7-105">Espelha um pacote e suas dependências dos repositórios de origem especificados para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="854a7-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="854a7-106">Para habilitar esse comando para versões do NuGet anteriores a 3,2, [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)vá para, selecione a versão estável mais `NuGet.ServerExtensions.dll` recente `Nuget-Signed.exe` , baixe e para o disco `Nuget-Signed.exe` local `nuget.exe` e renomeie para.</span><span class="sxs-lookup"><span data-stu-id="854a7-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="854a7-107">Uso</span><span class="sxs-lookup"><span data-stu-id="854a7-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="854a7-108">em `<packageID>` que é o pacote a ser espelhado ou `packages.config` `<configFilePath>` identifica o arquivo que lista os pacotes a serem espelhados.</span><span class="sxs-lookup"><span data-stu-id="854a7-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="854a7-109">O `<listUrlTarget>` especifica o repositório de origem e `<publishUrlTarget>` especifica o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="854a7-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="854a7-110">Se o seu repositório de destino `https://machine/repo` estiver no que está executando o [NuGet. Server](../../hosting-packages/nuget-server.md), a lista e as `https://machine/repo/nuget` URLs `https://machine/repo/api/v2/package`de push serão e, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="854a7-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="854a7-111">Opções</span><span class="sxs-lookup"><span data-stu-id="854a7-111">Options</span></span>

| <span data-ttu-id="854a7-112">Opção</span><span class="sxs-lookup"><span data-stu-id="854a7-112">Option</span></span> | <span data-ttu-id="854a7-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="854a7-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="854a7-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="854a7-114">ApiKey</span></span> | <span data-ttu-id="854a7-115">A chave de API para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="854a7-115">The API key for the target repository.</span></span> <span data-ttu-id="854a7-116">Se não estiver presente, o especificado no arquivo de configuração será usado (`%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="854a7-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="854a7-117">Ajuda</span><span class="sxs-lookup"><span data-stu-id="854a7-117">Help</span></span> | <span data-ttu-id="854a7-118">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="854a7-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="854a7-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="854a7-119">NoCache</span></span> | <span data-ttu-id="854a7-120">Impede que o NuGet use pacotes armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="854a7-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="854a7-121">Consulte [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="854a7-121">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="854a7-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="854a7-122">Noop</span></span> | <span data-ttu-id="854a7-123">Registra o que seria feito, mas não executa as ações; pressupõe êxito para operações de envio por push.</span><span class="sxs-lookup"><span data-stu-id="854a7-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="854a7-124">Pré-lançamento</span><span class="sxs-lookup"><span data-stu-id="854a7-124">PreRelease</span></span> | <span data-ttu-id="854a7-125">Inclui pacotes de pré-lançamento na operação de espelhamento.</span><span class="sxs-lookup"><span data-stu-id="854a7-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="854a7-126">Origem</span><span class="sxs-lookup"><span data-stu-id="854a7-126">Source</span></span> | <span data-ttu-id="854a7-127">Uma lista de origens do pacote a ser espelhada.</span><span class="sxs-lookup"><span data-stu-id="854a7-127">A list of package sources to mirror.</span></span> <span data-ttu-id="854a7-128">Se nenhuma fonte for especificada, as definidas no arquivo de configuração (consulte ApiKey acima) serão usadas, padronizando para nuget.org se nenhuma for especificada.</span><span class="sxs-lookup"><span data-stu-id="854a7-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="854a7-129">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="854a7-129">Timeout</span></span> | <span data-ttu-id="854a7-130">Especifica o tempo limite, em segundos, para envio por push para um servidor.</span><span class="sxs-lookup"><span data-stu-id="854a7-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="854a7-131">O padrão é 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="854a7-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="854a7-132">Versão</span><span class="sxs-lookup"><span data-stu-id="854a7-132">Version</span></span> | <span data-ttu-id="854a7-133">A versão do pacote a ser instalado.</span><span class="sxs-lookup"><span data-stu-id="854a7-133">The version of the package to install.</span></span> <span data-ttu-id="854a7-134">Se não for especificado, a versão mais recente será espelhada.</span><span class="sxs-lookup"><span data-stu-id="854a7-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="854a7-135">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="854a7-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="854a7-136">Exemplos</span><span class="sxs-lookup"><span data-stu-id="854a7-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
