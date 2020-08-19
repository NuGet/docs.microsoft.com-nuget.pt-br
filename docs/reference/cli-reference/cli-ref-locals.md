---
title: Comando local da CLI do NuGet
description: Referência para o comando nuget.exe locais
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: cdc2b760021ffc4a9e02edacb45beac01cc99bf1
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623052"
---
# <a name="locals-command-nuget-cli"></a>comando locals (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** de consumo de pacote: 3.3 +

Limpa ou lista os recursos do NuGet local, como a pasta *http-cache*, *global-Packages* e a pasta Temp. O `locals` comando também pode ser usado para exibir uma lista desses locais. Para obter mais informações, consulte [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Uso

```cli
nuget locals <folder> [options]
```

em que `<folder>` é um de `all` , `http-cache` , `packages-cache` *(3,5 e anterior)*, `global-packages` , `temp` *(3.4 +)* e `plugins-cache` *(4.8 +)*.

## <a name="options"></a>Opções

- **`-Clear`**

  Limpa a pasta especificada.

- **`-ConfigFile`**

  O arquivo de configuração do NuGet a ser aplicado. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.

- **`-ForceEnglishOutput`**

  *(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.

- **`-?|-help`**

  Exibe informações de ajuda para o comando.

- **`-List`**

  Lista o local da pasta especificada ou os locais de todas as pastas quando usados com *todos*.

- **`-NonInteractive`**

  Suprime prompts de entrada ou confirmações do usuário.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Para obter exemplos adicionais, consulte [Gerenciando os pacotes globais e as pastas de cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md).
