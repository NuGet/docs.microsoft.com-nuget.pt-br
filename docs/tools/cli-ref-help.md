---
title: Comando de Ajuda do NuGet CLI
description: Referência para o comando de ajuda de nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d7112209a0a2a267343c3458ebacaf6b744786a9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818250"
---
# <a name="help-or--command-nuget-cli"></a>help or ? Commando (NuGet CLI)

**Aplica-se a:** todos os &bullet; **versões com suporte**: todos os

Exibe geral informações de Ajuda e informações de ajuda sobre os comandos específicos.

## <a name="usage"></a>Uso

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

onde [comando] identifica um comando específico para o qual exibir a Ajuda.

> [!Warning]
> Com alguns comandos, lembre-se de especificar *ajuda* primeiro, como com `nuget help install`, pois há um pacote denominado "Ajuda" em nuget.org. Se você fornecer o comando `nuget install help`, você não obter ajuda sobre o comando de instalação, mas em vez disso, instalará o pacote denominado ajuda.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| Todos | Imprimir a ajuda detalhada para todos os comandos disponíveis; ignorado se for fornecido um comando específico. |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando Ajuda. |
| Markdown | Imprimir a ajuda detalhada no formato de redução quando usado com `-All`. Caso contrário é ignorado. |
| NonInteractive | Suprime avisos para a entrada do usuário ou confirmações. |
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
