---
title: Comando Adicionar do NuGet CLI
description: Comando de adicionar a referência para o nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4a4201a321ffe0f7fb61f4e98012a1a2d7d8fda4
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="add-command-nuget-cli"></a>Commando add (NuGet CLI)

**Aplica-se a**: a publicação do pacote &bullet; **versões com suporte**: 3.3 +

Adiciona um pacote especificado para uma origem de pacote não HTTP (uma pasta ou caminho UNC) em um layout hierárquico, no qual as pastas são criadas para o número de ID e a versão do pacote. Por exemplo:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Ao restaurar ou atualizar em relação a origem do pacote, o layout hierárquico fornece um desempenho significativamente melhor.

Para expandir todos os arquivos no pacote de origem do pacote de destino, use o `-Expand` alternar. Isso normalmente resulta em subpastas adicionais que aparecem no destino, como `tools` e `lib`.

## <a name="usage"></a>Uso

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

onde `<packagePath>` é o nome do caminho para o pacote a ser adicionado e `<sourcePath>` Especifica a origem de pacote com base em pasta à qual o pacote será adicionado. Não há suporte para fontes HTTP.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet para aplicar. Se não for especificado, `%AppData%\NuGet\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) é usado.|
| Expandir | Adiciona todos os arquivos no pacote de origem do pacote. |
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime avisos para a entrada do usuário ou confirmações. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```