---
title: Comando local da CLI do NuGet
description: Referência para o comando de locais do NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327803"
---
# <a name="locals-command-nuget-cli"></a>Commando locals (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** de consumo de pacote: 3.3+

Limpa ou lista os recursos do NuGet local, como a pasta *http-cache*, *global-Packages* e a pasta Temp. O `locals` comando também pode ser usado para exibir uma lista desses locais. Para obter mais informações, consulte [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Uso

```cli
nuget locals <folder> [options]
```

em `<folder>` que é um `all`de `http-cache`, `packages-cache` , *(3,5 e anterior)* `global-packages`, `temp` , *(3.4 +)* e `plugins-cache` *(4.8 +)* .

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| Clear | Limpa a pasta especificada. |
| ConfigFile | O arquivo de configuração do NuGet a ser aplicado. Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.|
| ForceEnglishOutput | *(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês. |
| Help | Exibe informações de ajuda para o comando. |
| Lista | Lista o local da pasta especificada ou os locais de todas as pastas quando usados com *todos*. |
| NonInteractive | Suprime prompts de entrada ou confirmações do usuário. |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Para obter exemplos adicionais, consulte [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).
