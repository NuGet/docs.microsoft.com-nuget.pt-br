---
title: Comando spec NuGet CLI
description: Referência para o comando spec nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17d3c5fc083f52fd9ab4a854ad358995bc55293b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817080"
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
