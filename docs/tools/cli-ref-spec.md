---
title: Comando spec da CLI do NuGet
description: Referência do comando spec nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68b165751ab6794d2a01d7e466619b1ce4d7ed72
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546443"
---
# <a name="spec-command-nuget-cli"></a>comando spec (CLI do NuGet)

**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** todos os

Gera um `.nuspec` arquivo para um novo pacote. Se executado na mesma pasta como um arquivo de projeto (`.csproj`, `.vbproj`, `.fsproj`), `spec` cria com um token `.nuspec` arquivo. Para obter mais informações, consulte [criando um pacote](../create-packages/creating-a-package.md).

## <a name="usage"></a>Uso

```cli
nuget spec [<packageID>] [options]
```

em que `<packageID>` é um identificador de pacote opcional para salvar no `.nuspec` arquivo.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| AssemblyPath | Especifica o caminho para o assembly a ser usado para metadados. |
| Force | Substitui todos os existentes `.nuspec` arquivo. |
| ForceEnglishOutput | *(3.5 ou superior)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime a solicitações de entrada do usuário ou confirmações. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
