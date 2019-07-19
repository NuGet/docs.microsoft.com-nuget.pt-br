---
title: Comando init da CLI do NuGet
description: Referência para o comando init NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327773"
---
# <a name="init-command-nuget-cli"></a>comando init (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** para criação de pacote: 3.3+

Copia todos os pacotes de uma pasta simples para uma pasta de destino usando um layout hierárquico, conforme descrito para o [comando Add](cli-ref-add.md). Ou seja, o `init` uso do é equivalente ao `add` uso do comando em cada pacote na pasta.

Assim como `add`acontece com o, o destino deve ser uma pasta local ou um caminho UNC; Não há suporte para repositórios de pacotes HTTP, como nuget.org ou servidores privados.

## <a name="usage"></a>Uso

```cli
nuget init <source> <destination> [options]
```

em `<source>` que é a pasta que contém `<destination>` pacotes e é a pasta local ou o nome do caminho UNC para o qual os pacotes são copiados.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet a ser aplicado. Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.|
| ForceEnglishOutput | *(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês. |
| Expandir | Adiciona todos os arquivos em cada pacote que é adicionado à origem do pacote; o mesmo `-Expand` que com `add` o comando. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime prompts de entrada ou confirmações do usuário. |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
