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
# <a name="troubleshooting-installed-packages"></a>Solucionando problemas de pacotes instalados

Às vezes, talvez você queira validar de qual fonte um pacote específico foi instalado. Aqui estão algumas maneiras que você pode verificar.

> [!Note]
> Algumas fontes de pacote dão suporte a um conceito conhecido como origens de upstream. Por exemplo, [Azure Artifacts as fontes upstream](/azure/devops/artifacts/concepts/upstream-sources). Os clientes NuGet não sabem se um pacote veio de uma origem de upstream. Portanto, qualquer log da origem do pacote listará a origem configurada, não a origem de upstream.

## <a name="nupkgmetadata-file-in-global-packages-folder"></a>`.nupkg.metadata` arquivo na pasta de pacotes globais

Quando um pacote é extraído para a pasta *global-Packages* , um arquivo `.nupkg.metadata` é gravado. A partir do NuGet 5.9.0, o NuGet adicionará a origem do pacote. Veja abaixo para mapear as versões do NuGet para as versões do Visual Studio ou SDK do .NET. Por exemplo:

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> Se a pasta *global-Packages* tiver pacotes extraídos antes da atualização para uma versão mais recente das ferramentas com NuGet 5.9.0, o arquivo será a `.nupkg.metadata` versão 1 e não conterá a origem do pacote. Você pode [limpar a pasta *global-Packages*](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) para garantir que todos os pacotes conterão a origem do pacote.

> [!Tip]
> O NuGet grava o `.nupkg.metadata` arquivo somente na pasta *global-Packages* . Projetos `packages.config` que usam usar uma pasta de pacotes de solução, que não cria um `.nupkg.metadata` arquivo.

## <a name="installed-package-log-message"></a>Mensagem de log do pacote instalado

A partir do NuGet 5.9.0, o NuGet gera a origem do pacote na mensagem de restauração informando que um pacote foi instalado. Por exemplo:

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> Essa mensagem é saída no detalhamento normal/informativo. O Visual Studio e a `dotnet` CLI assumem como padrão o mínimo de verbosidade, portanto, essa mensagem não será visível por padrão. O `msbuild` e as `nuget` ferramentas da CLI assumem como padrão o detalhamento normal, portanto, essa mensagem ficará visível por padrão.

## <a name="http-log-message"></a>Mensagem de log HTTP

Quando um pacote não está disponível localmente, na pasta *global-Packages* , em uma pasta de fallback ou em uma fonte de arquivo local, o NuGet o baixará de qualquer origem de pacote configurada sobre http. As solicitações e respostas HTTP são registradas no nível de verbosidade normal e você deve ver apenas uma única solicitação e resposta por versão do pacote. Por exemplo:

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

Se os arquivos foram baixados recentemente, eles podem ser recuperados do *cache http* do NuGet

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

O formato da URL pode ser diferente para diferentes implementações do servidor HTTP do NuGet e se ele está implementando o protocolo HTTP do NuGet v2 ou v3.

Se o `nuget.config` tiver várias fontes http definidas, você verá várias solicitações para cada arquivo de pacote `index.json` , uma para cada fonte. Mas haverá apenas um único `nupkg` download para cada versão do pacote.

## <a name="package-signature-log-message"></a>Mensagem de log de assinatura do pacote

Se o pacote que está sendo baixado for assinado, o NuGet validará a assinatura e registrará a seguinte mensagem em detalhes detalhados:

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

Esta mensagem será relatada se o pacote foi baixado de uma origem de pacote HTTP ou copiado de uma origem de pacote local. Ele não será apresentado se o pacote já estiver disponível na pasta *global-Packages* ou em uma pasta de fallback.

> [!Important]
> Devido à [remoção da confiança do](https://github.com/dotnet/announcements/issues/180) NUGET da AC da VeriSign, você desabilitou a verificação de pacote assinado em determinadas plataformas, em determinadas versões do NuGet e do SDK do .net. Portanto, os mesmos pacotes podem ter `PackageSignatureVerificationLog` logs, ou esses logs podem estar ausentes, dependendo de qual plataforma você está executando a restauração e qual versão do .net ou NuGet você está usando.

## <a name="nuget-version-map"></a>Mapa de versão do NuGet

As seguintes versões do NuGet têm alterações importantes em relação ao log de origem do pacote:

|Versão do NuGet|Versão do Visual Studio|Versão do SDK do .NET|
|---|---|---|
|5.9.0 NuGet|Visual Studio 2019 16.9.0|SDK DO .NET 5 5.0.200|
