---
title: CLI do NuGet adicionar comando
description: Referência para o nuget.exe adicionar comando
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545828"
---
# <a name="add-command-nuget-cli"></a>Commando add (NuGet CLI)

**Aplica-se ao**: a publicação do pacote &bullet; **versões com suporte**: 3.3 ou superior

Adiciona um pacote especificado para uma origem de pacote não HTTP (uma pasta ou caminho UNC) em um layout hierárquico, no qual as pastas são criadas para o número de ID e a versão do pacote. Por exemplo:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Ao restaurar ou atualizar em relação a origem do pacote, o layout hierárquico fornece um desempenho significativamente melhor.

Para expandir todos os arquivos no pacote para a origem do pacote de destino, use o `-Expand` alternar. Isso normalmente resulta em subpastas adicionais que aparecem no destino, como `tools` e `lib`.

## <a name="usage"></a>Uso

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

em que `<packagePath>` é o nome do caminho para o pacote para adicionar, e `<sourcePath>` Especifica a origem de pacote com base em pasta à qual o pacote será adicionado. Não há suporte para fontes de HTTP.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| Expand | Adiciona todos os arquivos no pacote de origem do pacote. |
| ForceEnglishOutput | *(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Help | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime a solicitações de entrada do usuário ou confirmações. |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
