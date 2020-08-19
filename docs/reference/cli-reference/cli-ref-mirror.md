---
title: Comando de espelhamento da CLI do NuGet
description: Referência para o comando nuget.exe Mirror
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a7247aeb21418e78dbfe9be15c2e7cd152aa3f4a
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622961"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="6ec8e-103">comando Mirror (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6ec8e-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="6ec8e-104">**Aplica-se a:** &bullet; **versões com suporte** para publicação de pacotes: preterida em 3.2 +</span><span class="sxs-lookup"><span data-stu-id="6ec8e-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="6ec8e-105">Espelha um pacote e suas dependências dos repositórios de origem especificados para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="6ec8e-106">NuGet.ServerExtensions.dll e NuGet-Signed.exe que anteriormente tinham suporte para esse comando no NuGet 2. x (renomeando NuGet-Signed.exe para nuget.exe) não estão mais disponíveis para download.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="6ec8e-107">Para usar um comando semelhante a este, tente [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span><span class="sxs-lookup"><span data-stu-id="6ec8e-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="6ec8e-108">Uso</span><span class="sxs-lookup"><span data-stu-id="6ec8e-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="6ec8e-109">em que `<packageID>` é o pacote a ser espelhado ou `<configFilePath>` identifica o `packages.config` arquivo que lista os pacotes a serem espelhados.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="6ec8e-110">O `<listUrlTarget>` especifica o repositório de origem e `<publishUrlTarget>` especifica o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="6ec8e-111">Se o seu repositório de destino estiver no `https://machine/repo` que está executando o [NuGet. Server](../../hosting-packages/nuget-server.md), a lista e as URLs de push serão `https://machine/repo/nuget` e `https://machine/repo/api/v2/package` , respectivamente.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="6ec8e-112">Opções</span><span class="sxs-lookup"><span data-stu-id="6ec8e-112">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="6ec8e-113">A chave de API para o repositório de destino.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-113">The API key for the target repository.</span></span> <span data-ttu-id="6ec8e-114">Se não estiver presente, o especificado no arquivo de configuração será usado ( `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="6ec8e-114">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span>

- **`-Help`**

  <span data-ttu-id="6ec8e-115">Exibe informações de ajuda para o comando.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-115">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="6ec8e-116">Impede que o NuGet use pacotes armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-116">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="6ec8e-117">Consulte [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="6ec8e-117">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-Noop`**

  <span data-ttu-id="6ec8e-118">Registra o que seria feito, mas não executa as ações; pressupõe êxito para operações de envio por push.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-118">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="6ec8e-119">Inclui pacotes de pré-lançamento na operação de espelhamento.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-119">Includes prerelease packages in the mirroring operation.</span></span>

- **`-Source`**

  <span data-ttu-id="6ec8e-120">Uma lista de origens do pacote a ser espelhada.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-120">A list of package sources to mirror.</span></span> <span data-ttu-id="6ec8e-121">Se nenhuma fonte for especificada, as definidas no arquivo de configuração (consulte ApiKey acima) serão usadas, padronizando para nuget.org se nenhuma for especificada.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-121">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span>

- **`-Timeout`**

  <span data-ttu-id="6ec8e-122">Especifica o tempo limite, em segundos, para envio por push para um servidor.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-122">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="6ec8e-123"> O padrão é 300 segundos (5 minutos).</span><span class="sxs-lookup"><span data-stu-id="6ec8e-123">The default is 300 seconds (5 minutes).</span></span>

- **`-Version`**

  <span data-ttu-id="6ec8e-124">A versão do pacote a ser instalado.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-124">The version of the package to install.</span></span> <span data-ttu-id="6ec8e-125">Se não for especificado, a versão mais recente será espelhada.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-125">If not specified, the latest version is mirrored.</span></span>

<span data-ttu-id="6ec8e-126">Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6ec8e-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6ec8e-127">Exemplos</span><span class="sxs-lookup"><span data-stu-id="6ec8e-127">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
