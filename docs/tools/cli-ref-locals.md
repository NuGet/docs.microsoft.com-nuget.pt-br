---
title: Comando de locais de CLI do NuGet
description: Referência para o comando de locais de nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 90e8c85e7a3e0e9520933e2ddd6dd84447475f2b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818195"
---
# <a name="locals-command-nuget-cli"></a>Commando locals (NuGet CLI)

**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** 3.3 +

Desmarca ou lista os recursos locais do NuGet como o *cache http*, *global pacotes* pasta e a pasta temporária. O `locals` comando também pode ser usado para exibir uma lista desses locais. Para obter mais informações, consulte [Gerenciando os pacotes globais e as pastas do cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Uso

```cli
nuget locals <folder> [options]
```

onde `<folder>` é um dos `all`, `http-cache`, `packages-cache` *(3.5 e anteriores)*, `global-packages`, e `temp` *(3.4 ou posterior)*.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| Clear | Limpa a pasta especificada. |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| Lista | Lista o local da pasta especificada, ou os locais de todas as pastas quando usado com *todos os*. |
| NonInteractive | Suprime avisos para a entrada do usuário ou confirmações. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Para obter exemplos adicionais, consulte [Gerenciando os pacotes globais e as pastas do cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).
