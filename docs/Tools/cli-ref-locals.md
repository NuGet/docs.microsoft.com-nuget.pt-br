---
title: Comando do NuGet CLI locais | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência para o comando de locais de nuget.exe"
keywords: "referência de locais do NuGet, comando locais"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="locals-command-nuget-cli"></a>comando de locais (NuGet CLI)

**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** 3.3 +

Limpa ou lista os recursos locais do NuGet, como o cache de solicitação de http, cache de pacotes e a pasta pacotes global de todo o computador. O `locals` comando também pode ser usado para exibir uma lista desses locais. Para obter mais informações, consulte [gerenciamento do Cache do NuGet](../consume-packages/managing-the-nuget-cache.md).

## <a name="usage"></a>Uso

```cli
nuget locals <cache> [options]
```

onde `<cache>` é um dos `all`, `http-cache`, `packages-cache`, `global-packages`, e `temp` *(3.4 ou posterior)*.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| Clear | Limpa o cache especificado. |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, *%AppData%\NuGet\NuGet.Config* é usado. |
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| Lista | Lista o local do cache especificado ou os locais de todos os caches quando usado com *todos os*. |
| NonInteractive | Suprime avisos para a entrada do usuário ou confirmações. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget locals all -list
nuget locals http-cache -clear
```
