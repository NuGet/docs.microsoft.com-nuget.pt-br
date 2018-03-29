---
title: Comando do NuGet CLI init | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referência para o comando de inicialização de nuget.exe
keywords: referência de init NuGet, o comando de inicialização
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 01a3553622020b5868e33ece09cd7555cb712fd3
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="init-command-nuget-cli"></a>comando init (NuGet CLI)

**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** 3.3 +

Copia todos os pacotes de uma pasta simples em uma pasta de destino usando um layout hierárquico, conforme descrito para o [adicionar comando](cli-ref-add.md). Ou seja, usando `init` é equivalente a usar o `add` comando em cada pacote na pasta.

Assim como acontece com `add`, o destino deve ser uma pasta local ou um caminho UNC; Não há suporte para os repositórios de pacote HTTP como nuget.org ou servidores privadas.

## <a name="usage"></a>Uso

```cli
nuget init <source> <destination> [options]
```

onde `<source>` é a pasta que contém pacotes e `<destination>` é a pasta local ou caminho UNC para o qual os pacotes são copiados.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Expandir | Adiciona todos os arquivos em cada pacote que é adicionado à origem do pacote; mesmo que `-Expand` com o `add` comando. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime avisos para a entrada do usuário ou confirmações. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
