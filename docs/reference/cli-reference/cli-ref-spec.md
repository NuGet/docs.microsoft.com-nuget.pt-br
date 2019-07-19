---
title: Comando de especificação da CLI do NuGet
description: Referência para o comando de especificação NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327563"
---
# <a name="spec-command-nuget-cli"></a>comando spec (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** para criação de pacote: todas

Gera um `.nuspec` arquivo para um novo pacote. Se for executado na mesma pasta que um arquivo de projeto`.csproj`( `.vbproj`, `.fsproj`,) `spec` , o criará `.nuspec` um arquivo com tokens. Para obter informações adicionais, consulte [criando um pacote](../../create-packages/creating-a-package.md).

## <a name="usage"></a>Uso

```cli
nuget spec [<packageID>] [options]
```

em `<packageID>` que é um identificador de pacote opcional para salvar `.nuspec` no arquivo.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| AssemblyPath | Especifica o caminho para o assembly a ser usado para metadados. |
| Aplicação | Substitui qualquer arquivo existente `.nuspec` . |
| ForceEnglishOutput | *(3,5 +)* Força o NuGet. exe a ser executado usando uma cultura invariável baseada em inglês. |
| Help | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime prompts de entrada ou confirmações do usuário. |
| Verbosity | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhado*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
