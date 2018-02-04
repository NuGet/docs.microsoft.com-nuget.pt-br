---
title: Comando spec NuGet CLI | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referência para o comando spec nuget.exe"
keywords: "referência de especificação do NuGet, especificações de comando"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc7e772e737a0f74929d13e2b126f7796b6d0dc7
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="spec-command-nuget-cli"></a>comando spec (NuGet CLI)

**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** todos

Gera um `.nuspec` arquivo para um novo pacote. Se executar na mesma pasta como um arquivo de projeto (`.csproj`, `.vbproj`, `.fsproj`), `spec` cria um editáveis `.nuspec` arquivo. Para obter mais informações, consulte [criando um pacote](../create-packages/creating-a-package.md).

## <a name="usage"></a>Uso

```cli
nuget spec [<packageID>] [options]
```

onde `<packageID>` é um identificador de pacote opcional para salvar no `.nuspec` arquivo.

## <a name="options"></a>Opções

| Opção | Descrição |
| --- | --- |
| AssemblyPath | Especifica o caminho para o assembly a ser usado para metadados. |
| Force | Substitui qualquer existente `.nuspec` arquivo. |
| ForceEnglishOutput | *(3.5 +)*  Força nuget.exe para ser executado usando uma cultura invariável, com base em inglês. |
| Ajuda | Exibe informações de ajuda para o comando. |
| NonInteractive | Suprime avisos para a entrada do usuário ou confirmações. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
