---
title: Comando Add da CLI do NuGet
description: Referência para o comando de adição NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327853"
---
# <a name="add-command-nuget-cli"></a>Commando add (NuGet CLI)

**Aplica-se a**: &bullet; **versões com suporte**para publicação de pacotes: 3.3+

Adiciona um pacote especificado a uma origem de pacote não HTTP (uma pasta ou caminho UNC) em um layout hierárquico, onde as pastas são criadas para a ID do pacote e o número de versão. Por exemplo:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Ao restaurar ou atualizar na origem do pacote, o layout hierárquico fornece um desempenho significativamente melhor.

Para expandir todos os arquivos no pacote para a origem do pacote de destino, use `-Expand` a opção. Isso normalmente resulta em subpastas adicionais que aparecem no destino, como `tools` e. `lib`

## <a name="usage"></a>Uso

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

em `<packagePath>` que é o nome do caminho para o pacote a `<sourcePath>` ser adicionado e especifica a origem do pacote baseado em pasta à qual o pacote será adicionado. Não há suporte para fontes HTTP.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| ConfigFile | O arquivo de configuração do NuGet a ser aplicado. Se não for especificado `%AppData%\NuGet\NuGet.Config` , (Windows) `~/.nuget/NuGet/NuGet.Config` ou (Mac/Linux) será usado.|
| Expand | Adiciona todos os arquivos no pacote à origem do pacote. |
| ForceEnglishOutput | *(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês. |
| Help | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime prompts de entrada ou confirmações do usuário. |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
