---
title: Comando de Ajuda do NuGet CLI | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência para o comando de ajuda de nuget.exe"
keywords: "referência da Ajuda NuGet, o comando de ajuda"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 97f72e1be0df6e97f8b06696b2b3861800e4ea08
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="help-or--command-nuget-cli"></a>Ajuda ou? comando (NuGet CLI)

**Aplica-se a:** todos os &bullet; **versões com suporte**: todos os

Exibe geral informações de Ajuda e informações de ajuda sobre os comandos específicos.

## <a name="usage"></a>Uso

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

onde [comando] identifica um comando específico para o qual exibir a Ajuda.

> [!Warning]
> Com alguns comandos, lembre-se de especificar *ajuda* primeiro, como com `nuget help install`, pois há um pacote denominado "Ajuda" em nuget.org. Se você fornecer o comando `nuget install help`, você não poderá obter ajuda sobre o comando de instalação, mas em vez disso, instalará o pacote denominado ajuda.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| Todos | Imprimir a ajuda detalhada para todos os comandos disponíveis; ignorado se for fornecido um comando específico. |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado. |
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
