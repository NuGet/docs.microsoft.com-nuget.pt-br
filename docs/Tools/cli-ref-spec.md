---
title: Comando spec NuGet CLI | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: "Referência para o comando spec nuget.exe"
keywords: "referência de especificação do NuGet, especificações de comando"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a>comando spec (NuGet CLI)

**Aplica-se a:** criação do pacote &bullet; **versões com suporte:** todos

Gera um `.nuspec` arquivo para um novo pacote. Se executar na mesma pasta como um arquivo de projeto (`.csproj`, `.vbproj`, `.fsproj`), `spec` cria um editáveis `.nuspec` arquivo. Para obter mais informações, consulte [criando um pacote](../create-packages/creating-a-package.md).

## <a name="usage"></a>Uso

```
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
| Não interativo | Suprime avisos para a entrada do usuário ou confirmações. |
| Detalhamento | Especifica a quantidade de detalhes exibidos na saída: *normal*, *silencioso*, *detalhadas (2.5 +)*. |

Consulte também [variáveis de ambiente](cli-ref-environment-variables.md)

## <a name="examples"></a>Exemplos

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
