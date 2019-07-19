---
title: Comando de ajuda da CLI do NuGet
description: Referência para o comando de ajuda do NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327793"
---
# <a name="help-or--command-nuget-cli"></a>help or ? Commando (NuGet CLI)

**Aplica-se a:** todas &bullet; as **versões com suporte**: todas

Exibe informações gerais de ajuda e informações de ajuda sobre comandos específicos.

## <a name="usage"></a>Uso

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

em que [Command] identifica um comando específico para o qual exibir a ajuda.

> [!Warning]
> Com alguns comandos, lembre-se de especificar a *ajuda* primeiro, `nuget help install`como com o, porque há um pacote chamado "Help" em NuGet.org. Se você fornecer o comando `nuget install help`, não obterá ajuda sobre o comando de instalação, mas, em vez disso, instalará o pacote chamado help.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| Todos | Imprimir ajuda detalhada para todos os comandos disponíveis; ignorado se um comando específico for fornecido. |
| ConfigFile | O arquivo de configuração do NuGet a ser aplicado. Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.|
| ForceEnglishOutput | *(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês. |
| Ajuda | Exibe informações de ajuda para o próprio comando de ajuda. |
| Markdown | Imprima a ajuda detalhada em formato de redução quando `-All`usado com. Caso contrário ignorado. |
| NonInteractive | Suprime prompts de entrada ou confirmações do usuário. |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
