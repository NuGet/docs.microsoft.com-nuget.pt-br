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
# <a name="mirror-command-nuget-cli"></a>Commando mirror (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** para publicação de pacotes: preterida em 3.2 +

Espelha um pacote e suas dependências dos repositórios de origem especificados para o repositório de destino.

> [!NOTE]
> Para habilitar esse comando para versões do NuGet anteriores a 3,2, [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)vá para, selecione a versão estável mais `NuGet.ServerExtensions.dll` recente `Nuget-Signed.exe` , baixe e para o disco `Nuget-Signed.exe` local `nuget.exe` e renomeie para.

## <a name="usage"></a>Uso

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

em `<packageID>` que é o pacote a ser espelhado ou `packages.config` `<configFilePath>` identifica o arquivo que lista os pacotes a serem espelhados.

O `<listUrlTarget>` especifica o repositório de origem e `<publishUrlTarget>` especifica o repositório de destino.

Se o seu repositório de destino `https://machine/repo` estiver no que está executando o [NuGet. Server](../../hosting-packages/nuget-server.md), a lista e as `https://machine/repo/nuget` URLs `https://machine/repo/api/v2/package`de push serão e, respectivamente.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ApiKey | A chave de API para o repositório de destino. Se não estiver presente, o especificado no arquivo de configuração será usado (`%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| Ajuda | Exibe informações de ajuda para o comando. |
| NoCache | Impede que o NuGet use pacotes armazenados em cache. Consulte [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NOOP | Registra o que seria feito, mas não executa as ações; pressupõe êxito para operações de envio por push. |
| Pré-lançamento | Inclui pacotes de pré-lançamento na operação de espelhamento. |
| Origem | Uma lista de origens do pacote a ser espelhada. Se nenhuma fonte for especificada, as definidas no arquivo de configuração (consulte ApiKey acima) serão usadas, padronizando para nuget.org se nenhuma for especificada. |
| Tempo limite | Especifica o tempo limite, em segundos, para envio por push para um servidor. O padrão é 300 segundos (5 minutos). |
| Versão | A versão do pacote a ser instalado. Se não for especificado, a versão mais recente será espelhada. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```