---
title: Comando init da CLI do NuGet
description: Referência para o comando nuget.exe init
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f37572624cea744ce60a9a2e58ad3cbe2696cb9e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780065"
---
# <a name="init-command-nuget-cli"></a>comando init (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** para criação de pacote: 3.3 +

Copia todos os pacotes de uma pasta simples para uma pasta de destino usando um layout hierárquico, conforme descrito para o [comando Add](cli-ref-add.md). Ou seja, `init` o uso do é equivalente ao uso do `add` comando em cada pacote na pasta.

Assim como acontece com `add` o, o destino deve ser uma pasta local ou um caminho UNC; Não há suporte para repositórios de pacotes HTTP, como nuget.org ou servidores privados.

## <a name="usage"></a>Uso

```cli
nuget init <source> <destination> [options]
```

em que `<source>` é a pasta que contém pacotes e `<destination>` é a pasta local ou o nome do caminho UNC para o qual os pacotes são copiados.

## <a name="options"></a>Opções

- **`-ConfigFile`**

  O arquivo de configuração do NuGet a ser aplicado. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` ou `~/.config/NuGet/NuGet.Config` (Mac/Linux) será usado.

- **`-Expand`**

  Adiciona todos os arquivos em cada pacote que é adicionado à origem do pacote; o mesmo que `-Expand` com o `add` comando.

- **`-ForceEnglishOutput`**

  *(3,5 +)* Força o nuget.exe a ser executado usando uma cultura invariável baseada em inglês.

- **`-?|-help`**

  Exibe informações de ajuda para o comando.

- **`-NonInteractive`**

  Suprime prompts de entrada ou confirmações do usuário.

- **`-Verbosity [normal|quiet|detailed]`**

  Especifica a quantidade de detalhes exibidos na saída: `normal` (o padrão), `quiet` ou `detailed` .

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
