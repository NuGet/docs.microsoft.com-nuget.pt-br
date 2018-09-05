---
title: Comando de inicialização da CLI do NuGet
description: Referência para o comando de inicialização nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551404"
---
# <a name="init-command-nuget-cli"></a>comando de inicialização (CLI do NuGet)

**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** 3.3 ou superior

Copia todos os pacotes de uma pasta de simples para uma pasta de destino usando um layout hierárquico, conforme descrito para o [adicionar comando](cli-ref-add.md). Ou seja, usando `init` é equivalente a usar o `add` comando em cada pacote na pasta.

Assim como acontece com `add`, o destino deve ser uma pasta local ou um caminho UNC; Não há suporte para repositórios de pacote HTTP como o nuget.org ou servidores privados.

## <a name="usage"></a>Uso

```cli
nuget init <source> <destination> [options]
```

em que `<source>` é a pasta que contém pacotes e `<destination>` é a pasta local ou o nome do caminho UNC para o qual os pacotes são copiados.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| ForceEnglishOutput | *(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Expandir | Adiciona todos os arquivos em cada pacote que é adicionado à origem do pacote; mesmo que `-Expand` com o `add` comando. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime a solicitações de entrada do usuário ou confirmações. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
