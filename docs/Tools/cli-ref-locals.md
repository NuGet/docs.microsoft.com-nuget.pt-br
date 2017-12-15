---
title: Comando do NuGet CLI locais | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 7f672c7c-74c9-4296-bc27-4d47882b541c
description: "Referência para o comando de locais de nuget.exe"
keywords: "referência de locais do NuGet, comando locais"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8cc06eedc20507e2bdd210e40c471ff551b89563
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
## <a name="locals-command-nuget-cli"></a>comando de locais (NuGet CLI)

**Aplica-se a:** pacote consumo &bullet; **versões com suporte:** 3.3 +

Limpa ou lista os recursos locais do NuGet, como o cache de solicitação de http, cache de pacotes e a pasta pacotes global de todo o computador. O `locals` comando também pode ser usado para exibir uma lista desses locais. Para obter mais informações, consulte [gerenciamento do Cache do NuGet](../consume-packages/managing-the-nuget-cache.md).

## <a name="usage"></a>Uso

```
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
| Não interativo | Suprime avisos para a entrada do usuário ou confirmações. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```
nuget locals all -list
nuget locals http-cache -clear
```
