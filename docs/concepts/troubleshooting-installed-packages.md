---
title: Solucionando problemas de pacotes instalados
description: Como descobrir qual origem do pacote foi usada para pacotes individuais
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387540"
---
# <a name="troubleshooting-installed-packages"></a><span data-ttu-id="93fc9-103">Solucionando problemas de pacotes instalados</span><span class="sxs-lookup"><span data-stu-id="93fc9-103">Troubleshooting Installed Packages</span></span>

<span data-ttu-id="93fc9-104">Às vezes, talvez você queira validar de qual fonte um pacote específico foi instalado.</span><span class="sxs-lookup"><span data-stu-id="93fc9-104">Sometimes you might want to validate which source a specific package was installed from.</span></span> <span data-ttu-id="93fc9-105">Aqui estão algumas maneiras que você pode verificar.</span><span class="sxs-lookup"><span data-stu-id="93fc9-105">Here are some ways you can check.</span></span>

> [!Note]
> <span data-ttu-id="93fc9-106">Algumas fontes de pacote dão suporte a um conceito conhecido como origens de upstream.</span><span class="sxs-lookup"><span data-stu-id="93fc9-106">Some package sources support a concept known as upstream sources.</span></span> <span data-ttu-id="93fc9-107">Por exemplo, [Azure Artifacts as fontes upstream](/azure/devops/artifacts/concepts/upstream-sources).</span><span class="sxs-lookup"><span data-stu-id="93fc9-107">For example, [Azure Artifacts upstream sources](/azure/devops/artifacts/concepts/upstream-sources).</span></span> <span data-ttu-id="93fc9-108">Os clientes NuGet não sabem se um pacote veio de uma origem de upstream.</span><span class="sxs-lookup"><span data-stu-id="93fc9-108">NuGet clients do not know whether a package came from an upstream source.</span></span> <span data-ttu-id="93fc9-109">Portanto, qualquer log da origem do pacote listará a origem configurada, não a origem de upstream.</span><span class="sxs-lookup"><span data-stu-id="93fc9-109">Therefore, any logging of the package source will list the configured source, not the upstream source.</span></span>

## <a name="nupkgmetadata-file-in-global-packages-folder"></a><span data-ttu-id="93fc9-110">`.nupkg.metadata` arquivo na pasta de pacotes globais</span><span class="sxs-lookup"><span data-stu-id="93fc9-110">`.nupkg.metadata` file in global packages folder</span></span>

<span data-ttu-id="93fc9-111">Quando um pacote é extraído para a pasta *global-Packages* , um arquivo `.nupkg.metadata` é gravado.</span><span class="sxs-lookup"><span data-stu-id="93fc9-111">When a package is extracted into the *global-packages* folder, a file `.nupkg.metadata` is written.</span></span> <span data-ttu-id="93fc9-112">A partir do NuGet 5.9.0, o NuGet adicionará a origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="93fc9-112">Starting from NuGet 5.9.0, NuGet will add the package source.</span></span> <span data-ttu-id="93fc9-113">Veja abaixo para mapear as versões do NuGet para as versões do Visual Studio ou SDK do .NET.</span><span class="sxs-lookup"><span data-stu-id="93fc9-113">See below to map NuGet versions to Visual Studio or .NET SDK versions.</span></span> <span data-ttu-id="93fc9-114">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="93fc9-114">For example:</span></span>

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> <span data-ttu-id="93fc9-115">Se a pasta *global-Packages* tiver pacotes extraídos antes da atualização para uma versão mais recente das ferramentas com NuGet 5.9.0, o arquivo será a `.nupkg.metadata` versão 1 e não conterá a origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="93fc9-115">If your *global-packages* folder has packages extracted before you upgraded to a newer version of tools that has NuGet 5.9.0, the `.nupkg.metadata` file will be version 1 and will not contain the package source.</span></span> <span data-ttu-id="93fc9-116">Você pode [limpar a pasta *global-Packages*](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) para garantir que todos os pacotes conterão a origem do pacote.</span><span class="sxs-lookup"><span data-stu-id="93fc9-116">You can [clear your *global-packages* folder](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) to ensure all packages will contain the package source.</span></span>

> [!Tip]
> <span data-ttu-id="93fc9-117">O NuGet grava o `.nupkg.metadata` arquivo somente na pasta *global-Packages* .</span><span class="sxs-lookup"><span data-stu-id="93fc9-117">NuGet writes the `.nupkg.metadata` file to the *global-packages* folder only.</span></span> <span data-ttu-id="93fc9-118">Projetos `packages.config` que usam usar uma pasta de pacotes de solução, que não cria um `.nupkg.metadata` arquivo.</span><span class="sxs-lookup"><span data-stu-id="93fc9-118">Projects using `packages.config` use a solution packages folder, which does not create a `.nupkg.metadata` file.</span></span>

## <a name="installed-package-log-message"></a><span data-ttu-id="93fc9-119">Mensagem de log do pacote instalado</span><span class="sxs-lookup"><span data-stu-id="93fc9-119">Installed package log message</span></span>

<span data-ttu-id="93fc9-120">A partir do NuGet 5.9.0, o NuGet gera a origem do pacote na mensagem de restauração informando que um pacote foi instalado.</span><span class="sxs-lookup"><span data-stu-id="93fc9-120">Starting from NuGet 5.9.0, NuGet outputs the package source in the restore message informing that a package was installed.</span></span> <span data-ttu-id="93fc9-121">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="93fc9-121">For example:</span></span>

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> <span data-ttu-id="93fc9-122">Essa mensagem é saída no detalhamento normal/informativo.</span><span class="sxs-lookup"><span data-stu-id="93fc9-122">This message is output at normal/informational verbosity.</span></span> <span data-ttu-id="93fc9-123">O Visual Studio e a `dotnet` CLI assumem como padrão o mínimo de verbosidade, portanto, essa mensagem não será visível por padrão.</span><span class="sxs-lookup"><span data-stu-id="93fc9-123">Visual Studio and the `dotnet` CLI default to minimal verbosity, so this message will not be visible by default.</span></span> <span data-ttu-id="93fc9-124">O `msbuild` e as `nuget` ferramentas da CLI assumem como padrão o detalhamento normal, portanto, essa mensagem ficará visível por padrão.</span><span class="sxs-lookup"><span data-stu-id="93fc9-124">The `msbuild` and `nuget` CLI tools default to normal verbosity, so this message will be visible by default.</span></span>

## <a name="http-log-message"></a><span data-ttu-id="93fc9-125">Mensagem de log HTTP</span><span class="sxs-lookup"><span data-stu-id="93fc9-125">HTTP log message</span></span>

<span data-ttu-id="93fc9-126">Quando um pacote não está disponível localmente, na pasta *global-Packages* , em uma pasta de fallback ou em uma fonte de arquivo local, o NuGet o baixará de qualquer origem de pacote configurada sobre http.</span><span class="sxs-lookup"><span data-stu-id="93fc9-126">When a package is not available locally, either in the *global-packages* folder, a fallback folder, or a local file source, NuGet will download it from any configured package source over HTTP.</span></span> <span data-ttu-id="93fc9-127">As solicitações e respostas HTTP são registradas no nível de verbosidade normal e você deve ver apenas uma única solicitação e resposta por versão do pacote.</span><span class="sxs-lookup"><span data-stu-id="93fc9-127">HTTP requests and responses are logged at the normal verbosity level, and you should see only a single request and response per package version.</span></span> <span data-ttu-id="93fc9-128">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="93fc9-128">For example:</span></span>

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

<span data-ttu-id="93fc9-129">Se os arquivos foram baixados recentemente, eles podem ser recuperados do *cache http* do NuGet</span><span class="sxs-lookup"><span data-stu-id="93fc9-129">If the files were recently downloaded, they might be retrieved from NuGet's *http-cache*</span></span>

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

<span data-ttu-id="93fc9-130">O formato da URL pode ser diferente para diferentes implementações do servidor HTTP do NuGet e se ele está implementando o protocolo HTTP do NuGet v2 ou v3.</span><span class="sxs-lookup"><span data-stu-id="93fc9-130">The URL format may be different for different NuGet HTTP server implementations, and whether it's implementing NuGet V2 or V3 HTTP protocol.</span></span>

<span data-ttu-id="93fc9-131">Se o `nuget.config` tiver várias fontes http definidas, você verá várias solicitações para cada arquivo de pacote `index.json` , uma para cada fonte.</span><span class="sxs-lookup"><span data-stu-id="93fc9-131">If your `nuget.config` has multiple HTTP sources defined, you will see multiple requests to each package's `index.json` file, one for each source.</span></span> <span data-ttu-id="93fc9-132">Mas haverá apenas um único `nupkg` download para cada versão do pacote.</span><span class="sxs-lookup"><span data-stu-id="93fc9-132">But there will be only a single `nupkg` download for each version of the package.</span></span>

## <a name="package-signature-log-message"></a><span data-ttu-id="93fc9-133">Mensagem de log de assinatura do pacote</span><span class="sxs-lookup"><span data-stu-id="93fc9-133">Package signature log message</span></span>

<span data-ttu-id="93fc9-134">Se o pacote que está sendo baixado for assinado, o NuGet validará a assinatura e registrará a seguinte mensagem em detalhes detalhados:</span><span class="sxs-lookup"><span data-stu-id="93fc9-134">If the package being downloaded is signed, NuGet will validate the signature and will log the following message at detailed verbosity:</span></span>

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

<span data-ttu-id="93fc9-135">Esta mensagem será relatada se o pacote foi baixado de uma origem de pacote HTTP ou copiado de uma origem de pacote local.</span><span class="sxs-lookup"><span data-stu-id="93fc9-135">This message will be reported whether the package was downloaded from an HTTP package source, or copied from a local package source.</span></span> <span data-ttu-id="93fc9-136">Ele não será apresentado se o pacote já estiver disponível na pasta *global-Packages* ou em uma pasta de fallback.</span><span class="sxs-lookup"><span data-stu-id="93fc9-136">It will not be output if the package is already available in the *global-packages* folder or a fallback folder.</span></span>

> [!Important]
> <span data-ttu-id="93fc9-137">Devido à [remoção da confiança do](https://github.com/dotnet/announcements/issues/180) NUGET da AC da VeriSign, você desabilitou a verificação de pacote assinado em determinadas plataformas, em determinadas versões do NuGet e do SDK do .net.</span><span class="sxs-lookup"><span data-stu-id="93fc9-137">Due to [removal of trust of VeriSign CA](https://github.com/dotnet/announcements/issues/180) NuGet has disabled signed package verification on certain platforms, in certain versions of NuGet and the .NET SDK.</span></span> <span data-ttu-id="93fc9-138">Portanto, os mesmos pacotes podem ter `PackageSignatureVerificationLog` logs, ou esses logs podem estar ausentes, dependendo de qual plataforma você está executando a restauração e qual versão do .net ou NuGet você está usando.</span><span class="sxs-lookup"><span data-stu-id="93fc9-138">Therefore, the same packages may have `PackageSignatureVerificationLog` logs, or those logs may be missing, depending on what platform you're running restore on, and which version of .NET or NuGet you're using.</span></span>

## <a name="nuget-version-map"></a><span data-ttu-id="93fc9-139">Mapa de versão do NuGet</span><span class="sxs-lookup"><span data-stu-id="93fc9-139">NuGet Version Map</span></span>

<span data-ttu-id="93fc9-140">As seguintes versões do NuGet têm alterações importantes em relação ao log de origem do pacote:</span><span class="sxs-lookup"><span data-stu-id="93fc9-140">The following versions of NuGet have important changes regarding package source logging:</span></span>

|<span data-ttu-id="93fc9-141">Versão do NuGet</span><span class="sxs-lookup"><span data-stu-id="93fc9-141">NuGet Version</span></span>|<span data-ttu-id="93fc9-142">Versão do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="93fc9-142">Visual Studio Version</span></span>|<span data-ttu-id="93fc9-143">Versão do SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="93fc9-143">.NET SDK Version</span></span>|
|---|---|---|
|<span data-ttu-id="93fc9-144">5.9.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="93fc9-144">NuGet 5.9.0</span></span>|<span data-ttu-id="93fc9-145">Visual Studio 2019 16.9.0</span><span class="sxs-lookup"><span data-stu-id="93fc9-145">Visual Studio 2019 16.9.0</span></span>|<span data-ttu-id="93fc9-146">SDK DO .NET 5 5.0.200</span><span class="sxs-lookup"><span data-stu-id="93fc9-146">.NET 5 SDK 5.0.200</span></span>|
