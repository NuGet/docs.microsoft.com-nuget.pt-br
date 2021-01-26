---
title: Comando de espelhamento da CLI do NuGet
description: Referência para o comando nuget.exe Mirror
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6ecd5c11383f78fdaeb01090366a8ffe294b4f8b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779170"
---
# <a name="mirror-command-nuget-cli"></a>comando Mirror (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** para publicação de pacotes: preterida em 3.2 +

Espelha um pacote e suas dependências dos repositórios de origem especificados para o repositório de destino.

> [!NOTE]
> NuGet.ServerExtensions.dll e NuGet-Signed.exe que anteriormente tinham suporte para esse comando no NuGet 2. x (renomeando NuGet-Signed.exe para nuget.exe) não estão mais disponíveis para download. Para usar um comando semelhante a este, tente [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).

## <a name="usage"></a>Uso

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

em que `<packageID>` é o pacote a ser espelhado ou `<configFilePath>` identifica o `packages.config` arquivo que lista os pacotes a serem espelhados.

O `<listUrlTarget>` especifica o repositório de origem e `<publishUrlTarget>` especifica o repositório de destino.

Se o seu repositório de destino estiver no `https://machine/repo` que está executando o [NuGet. Server](../../hosting-packages/nuget-server.md), a lista e as URLs de push serão `https://machine/repo/nuget` e `https://machine/repo/api/v2/package` , respectivamente.

## <a name="options"></a>Opções

- **`-ApiKey`**

  A chave de API para o repositório de destino. Se não estiver presente, o especificado no arquivo de configuração será usado ( `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).

- **`-Help`**

  Exibe informações de ajuda para o comando.

- **`-NoCache`**

  Impede que o NuGet use pacotes armazenados em cache. Consulte [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-Noop`**

  Registra o que seria feito, mas não executa as ações; pressupõe êxito para operações de envio por push.

- **`-PreRelease`**

  Inclui pacotes de pré-lançamento na operação de espelhamento.

- **`-Source`**

  Uma lista de origens do pacote a ser espelhada. Se nenhuma fonte for especificada, as definidas no arquivo de configuração (consulte ApiKey acima) serão usadas, padronizando para nuget.org se nenhuma for especificada.

- **`-Timeout`**

  Especifica o tempo limite, em segundos, para envio por push para um servidor.  O padrão é 300 segundos (5 minutos).

- **`-Version`**

  A versão do pacote a ser instalado. Se não for especificado, a versão mais recente será espelhada.

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
