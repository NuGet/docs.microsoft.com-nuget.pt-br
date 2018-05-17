---
title: Comando de espelho do NuGet CLI
description: Referência para o comando de espelho nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5ba13196d385abf42a5af2faa3fe6f0e80fb59d8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="mirror-command-nuget-cli"></a>Commando mirror (NuGet CLI)

**Aplica-se a:** pacote publicação &bullet; **versões com suporte:** preterido no 3.2 +

Reflete um pacote e suas dependências de repositórios de origem especificado para o repositório de destino.

> [!NOTE]
> Para habilitar esse comando para versões do NuGet antes 3.2, vá para [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), selecione a versão estável mais recente, baixe `NuGet.ServerExtensions.dll` e `Nuget-Signed.exe` para seu disco local e renomear `Nuget-Signed.exe` para `nuget.exe`.

## <a name="usage"></a>Uso

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

onde `<packageID>` é o pacote para o espelho, ou `<configFilePath>` identifica o `packages.config` arquivo que lista os pacotes para espelhar.

O `<listUrlTarget>` Especifica o repositório de origem e `<publishUrlTarget>` Especifica o repositório de destino.

Se o repositório de destino estiver em `https://machine/repo` que está executando o [NuGet.Server](../hosting-packages/nuget-server.md), as urls de lista e enviar por push será `https://machine/repo/nuget` e `https://machine/repo/api/v2/package`, respectivamente.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| apiKey | A chave de API para o repositório de destino. Se não estiverem presentes, o especificado no arquivo de configuração é usado (`%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Linux/Mac)). |
| Ajuda | Exibe informações de ajuda para o comando. |
| NoCache | Impede que o NuGet usando pacotes armazenados em cache. Consulte [Gerenciando os pacotes globais e as pastas do cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NOOP | Registra o que deve ser feito, mas não executa as ações; assume o sucesso para operações de envio por push. |
| Versão de pré-lançamento | Inclui pacotes pré-lançados na operação de espelhamento. |
| Origem | Uma lista de fontes de pacote para espelhar. Se nenhuma fonte for especificada, aqueles definidos no arquivo de configuração (consulte ApiKey acima) são usados, padronizando para nuget.org se nenhum for especificado. |
| Tempo limite | Especifica o tempo limite, em segundos, para enviar por push para um servidor. O padrão é 300 segundos (5 minutos). |
| Versão | A versão do pacote para instalação. Se não for especificado, a versão mais recente é espelhada. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```