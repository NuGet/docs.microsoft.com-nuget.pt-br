---
title: Comando de ajuda da CLI do NuGet
description: Referência para o comando de ajuda do nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 12776b7c16aeef223a0b682ee2468edec8ea3295
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623104"
---
# <a name="help-or--command-nuget-cli"></a>help or ? comando (NuGet CLI)

**Aplica-se a:** todas as &bullet; **versões com suporte**: todas

Exibe informações gerais de ajuda e informações de ajuda sobre comandos específicos.

## <a name="usage"></a>Uso

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

em que [Command] identifica um comando específico para o qual exibir a ajuda.

> [!Warning]
> Com alguns comandos, lembre-se de especificar a *ajuda* primeiro, como com `nuget help install` o, porque há um pacote chamado "help" em NuGet.org. Se você fornecer o comando `nuget install help` , não obterá ajuda sobre o comando de instalação, mas, em vez disso, instalará o pacote chamado help.

## <a name="options"></a>Opções

- **`-All`**

  Imprimir ajuda detalhada para todos os comandos disponíveis; ignorado se um comando específico for fornecido.

- **`-ConfigFile`**

  O arquivo de configuração do NuGet a ser aplicado. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.

- **`-ForceEnglishOutput`**

  *(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.

- **`-?|-help`**

  Exibe informações de ajuda para o comando.

- **`-Markdown`**

  Imprima a ajuda detalhada em formato de redução quando usado com `-All` . Caso contrário ignorado.

- **`-NonInteractive`**

  Suprime prompts de entrada ou confirmações do usuário.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
