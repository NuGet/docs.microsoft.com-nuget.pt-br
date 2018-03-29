---
title: Comando do NuGet CLI locais | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referência para o comando de locais de nuget.exe
keywords: referência de locais do NuGet, comando locais
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0122c79e55b12838bd123cf91bfcbc5dbbd2a65c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="locals-command-nuget-cli"></a>comando de locais (NuGet CLI)

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
