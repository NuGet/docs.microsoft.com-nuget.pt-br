---
title: Comando do CLI do NuGet locals
description: Referência do comando locals nuget.exe
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ea216c4651ba9619bc3b6a7ab52546fd299b0bb6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545022"
---
# <a name="locals-command-nuget-cli"></a>Commando locals (NuGet CLI)

**Aplica-se a:** consumo do pacote &bullet; **versões com suporte:** 3.3 ou superior

Limpa ou lista os recursos locais do NuGet, como o *http-cache*, *global-packages* pasta e a pasta temp. O `locals` comando também pode ser usado para exibir uma lista desses locais. Para obter mais informações, consulte [gerenciar as pastas de cache e de pacotes globais](../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Uso

```cli
nuget locals <folder> [options]
```

em que `<folder>` é uma das `all`, `http-cache`, `packages-cache` *(3.5 e anterior)*, `global-packages`, `temp` *(3.4 ou superior)*, e `plugins-cache` *(4.8 +)*.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| Clear | Limpa a pasta especificada. |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| ForceEnglishOutput | *(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| Lista | Lista o local da pasta especificada ou os locais de todas as pastas quando usado com *todos os*. |
| NonInteractive | Suprime a solicitações de entrada do usuário ou confirmações. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Para obter exemplos adicionais, consulte [gerenciar as pastas de cache e de pacotes globais](../consume-packages/managing-the-global-packages-and-cache-folders.md).
