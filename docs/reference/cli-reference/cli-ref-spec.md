---
title: Comando de especificação da CLI do NuGet
description: Referência para o comando nuget.exe spec
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17603fa30a75c7906f867c96c5d77f31732eaa59
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622558"
---
# <a name="spec-command-nuget-cli"></a>comando spec (NuGet CLI)

**Aplica-se a:** &bullet; **versões com suporte** para criação de pacote: todas

Gera um `.nuspec` arquivo para um novo pacote. Se for executado na mesma pasta que um arquivo de projeto ( `.csproj` , `.vbproj` , `.fsproj` ), `spec` o criará um arquivo com tokens `.nuspec` . Para obter informações adicionais, consulte [criando um pacote](../../create-packages/creating-a-package.md).

## <a name="usage"></a>Uso

```cli
nuget spec [<packageID>] [options]
```

em que `<packageID>` é um identificador de pacote opcional para salvar no `.nuspec` arquivo.

## <a name="options"></a>Opções

- **`-AssemblyPath`**

  Especifica o caminho para o assembly a ser usado para metadados.

- **`-Force`**

  Substitui qualquer `.nuspec` arquivo existente.


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
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
