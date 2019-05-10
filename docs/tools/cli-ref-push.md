---
title: Comando do CLI do NuGet push
description: Referência do comando de envio por push nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4a9460944e2c232e2a72195434a491d26eee3559
ms.sourcegitcommit: 3fc93f7a64be040699fe12125977dd25a7948470
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64877951"
---
# <a name="push-command-nuget-cli"></a>envio por push de comando (CLI do NuGet)

**Aplica-se a:** publicação de pacote &bullet; **versões com suporte:** todos os; 4.1.0 + necessários para o nuget.org

> [!Important]
> Enviar pacotes para nuget.org, você deve usar nuget.exe verze 4.1.0 +, que implementa o necessária [protocolos NuGet](../api/nuget-protocols.md).

Envia um pacote para uma origem de pacote e os publica.

Configuração de padrão do NuGet é obtida ao carregar `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), em seguida, carregar qualquer `Nuget.Config` ou `.nuget\Nuget.Config` arquivos a partir da raiz da unidade e terminar no diretório atual (consulte [Configurando O comportamento do NuGet](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Uso

```cli
nuget push <packagePath> [options]
```

onde `<packagePath>` identifica o pacote para enviar por push para o servidor.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ApiKey | A chave de API para o repositório de destino. Se não estiver presente, aquele especificado no arquivo de configuração será usada. |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| DisableBuffering | Desabilita o armazenamento em buffer ao enviar por push a um servidor HTTP (s) para diminuir o uso de memória. Cuidado: quando esta opção for usada, a autenticação integrada do Windows pode não funcionar. |
| ForceEnglishOutput | *(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Help | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime a solicitações de entrada do usuário ou confirmações. |
| NoSymbols | *(3.5 ou superior)*  Se existe um pacote de símbolos, ele não será enviado a um servidor de símbolos. |
| Origem | Especifica a URL do servidor. O NuGet identifica um UNC ou uma fonte de pasta local e simplesmente copia o arquivo em vez de enviá-la usando HTTP.  Além disso, começando com o NuGet 3.4.2, este parâmetro é obrigatório, a menos que o `NuGet.Config` arquivo Especifica um *DefaultPushSource* valor (consulte [o comportamento do NuGet configurando](../consume-packages/configuring-nuget-behavior.md)). |
| SymbolSource | *(3.5 ou superior)*  Especifica a URL do servidor de símbolo; nuget.smbsrc.net é usado ao enviar por push para nuget.org |
| SymbolApiKey | *(3.5 ou superior)*  Especifica a chave de API para a URL especificada no `-SymbolSource`. |
| Tempo limite | Especifica o tempo limite, em segundos, para enviar por push a um servidor. O padrão é 300 segundos (5 minutos). |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/
```
