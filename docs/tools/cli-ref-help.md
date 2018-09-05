---
title: Comando de Ajuda da CLI do NuGet
description: Referência do comando de ajuda nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546557"
---
# <a name="help-or--command-nuget-cli"></a>help or ? Commando (NuGet CLI)

**Aplica-se a:** todos os &bullet; **versões com suporte**: todos

Geral de exibe informações de Ajuda e informações de ajuda sobre comandos específicos.

## <a name="usage"></a>Uso

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

onde [comando] identifica um comando específico para o qual exibir a Ajuda.

> [!Warning]
> Com alguns comandos, lembre-se de especificar *ajudar* primeiro, como com `nuget help install`, pois há um pacote denominado "help" em nuget.org. Se você der o comando `nuget install help`, você não obter ajuda sobre o comando de instalação, mas em vez disso, instalará o pacote denominado ajuda.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| Todos | Imprimir a ajuda detalhada para todos os comandos disponíveis; ignorado se recebe um comando específico. |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| ForceEnglishOutput | *(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando de Ajuda. |
| Markdown | Imprimir no formato markdown quando usado com a ajuda detalhada `-All`. Caso contrário é ignorado. |
| NonInteractive | Suprime a solicitações de entrada do usuário ou confirmações. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
