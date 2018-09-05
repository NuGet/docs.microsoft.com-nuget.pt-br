---
title: Comando de espelho da CLI do NuGet
description: Referência do comando de espelho nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550200"
---
# <a name="mirror-command-nuget-cli"></a>Commando mirror (NuGet CLI)

**Aplica-se a:** publicação de pacote &bullet; **versões com suporte:** preterido no 3.2 e superior

Espelha um pacote e suas dependências de repositórios de origem especificado para o repositório de destino.

> [!NOTE]
> Para habilitar esse comando para versões do NuGet antes 3.2, acesse [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), selecione a versão estável mais recente, baixe `NuGet.ServerExtensions.dll` e `Nuget-Signed.exe` em seu disco local e renomeação `Nuget-Signed.exe` para `nuget.exe`.

## <a name="usage"></a>Uso

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

em que `<packageID>` é o pacote para espelhar, ou `<configFilePath>` identifica o `packages.config` arquivo que lista os pacotes para espelhar.

O `<listUrlTarget>` Especifica o repositório de origem, e `<publishUrlTarget>` Especifica o repositório de destino.

Se o repositório de destino estiver no `https://machine/repo` que está executando o [NuGet. Server](../hosting-packages/nuget-server.md), as urls de lista e push serão `https://machine/repo/nuget` e `https://machine/repo/api/v2/package`, respectivamente.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ApiKey | A chave de API para o repositório de destino. Se não estiver presente, o especificado no arquivo de configuração será usada (`%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| Ajuda | Exibe informações de ajuda para o comando. |
| NoCache | Impede que o NuGet usando pacotes armazenados em cache. Ver [gerenciar as pastas de cache e de pacotes globais](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NOOP | Registra o que seria feito, mas não executa as ações; pressupõe sucesso para operações de envio por push. |
| Versão de pré-lançamento | Inclui pacotes pré-lançados na operação de espelhamento. |
| Origem | Uma lista de origens de pacote para espelhar. Se nenhuma fonte forem especificado, aqueles definidos no arquivo de configuração (consulte ApiKey acima) são usados, padronizando para nuget.org, se nenhum for especificado. |
| Tempo limite | Especifica o tempo limite, em segundos, para enviar por push a um servidor. O padrão é 300 segundos (5 minutos). |
| Versão | A versão do pacote a instalar. Se não for especificado, a versão mais recente é espelhada. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
