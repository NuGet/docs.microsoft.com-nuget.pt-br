---
title: Referência de avisos e erros do NuGet
description: Referência completa para avisos e erros emitidos do NuGet durante várias operações do NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 25c8a22fc0bce2372c54cf29b904a8d9fbbe9ace
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843424"
---
# <a name="errors-and-warnings"></a>Erros e avisos

O NuGet 4.3.0, erros e avisos são numerados conforme descrito neste tópico em fornecem informações detalhadas para ajudá-lo a resolver os problemas envolvidos.

Os erros e avisos listados aqui estão disponíveis apenas com [baseado em PackageReference](../consume-packages/package-references-in-project-files.md) projetos e o NuGet 4.3.0. NuGet também respeita as propriedades do MSBuild para suprimir avisos ou eleve-os a erros. Para obter mais informações, consulte [como: suprimir avisos do compilador](/visualstudio/ide/how-to-suppress-compiler-warnings) na documentação do Visual Studio.

**Erros**

| Grupo | Números de erro |
| --- | --- |
| Erros de entrada inválidos | [NU1001](./errors-and-warnings/NU1001.md), [NU1002](./errors-and-warnings/NU1002.md), [NU1003](./errors-and-warnings/NU1003.md) |
| Erros de pacote e projeto ausentes | [NU1100](./errors-and-warnings/NU1100.md), [NU1101](./errors-and-warnings/NU1101.md), [NU1102](./errors-and-warnings/NU1102.md), [NU1103](./errors-and-warnings/NU1103.md), [NU1104](./errors-and-warnings/NU1104.md), [NU1105](./errors-and-warnings/NU1105.md), [NU1106](./errors-and-warnings/NU1106.md), [NU1107](./errors-and-warnings/NU1107.md) (anteriormente NU1607) [NU1108](./errors-and-warnings/NU1108.md) (anteriormente NU1606) |
| Erros de compatibilidade | [NU1201](./errors-and-warnings/NU1201.md), [NU1202](./errors-and-warnings/NU1202.md), [NU1203](./errors-and-warnings/NU1203.md), [NU1401](./errors-and-warnings/NU1401.md) |
| Erros internos do NuGet | [NU1000](./errors-and-warnings/NU1000.md) |
| Erros de pacotes assinados (criação e verificação) | [NU3000](./errors-and-warnings/NU3000.md), [NU3001](./errors-and-warnings/NU3001.md), [NU3004](./errors-and-warnings/NU3004.md), [NU3008](./errors-and-warnings/NU3008.md) |

**Avisos**

| Grupo | Números de aviso |
| --- | --- |
| Avisos de entrada inválidos | [NU1501](./errors-and-warnings/NU1501.md), [NU1502](./errors-and-warnings/NU1502.md), [NU1503](./errors-and-warnings/NU1503.md) |
| Avisos de versão do pacote inesperado | [NU1601](./errors-and-warnings/NU1601.md), [NU1602](./errors-and-warnings/NU1602.md), [NU1603](./errors-and-warnings/NU1603.md), [NU1604](./errors-and-warnings/NU1604.md), [NU1605](./errors-and-warnings/NU1605.md) |
| Avisos de conflito de resolução | [NU1608](./errors-and-warnings/NU1608.md) |
| Avisos de fallback do pacote | [NU1701](./errors-and-warnings/NU1701.md) |
| Avisos de feed | [NU1801](./errors-and-warnings/NU1801.md) |
| Avisos internos do NuGet | [NU1500](./errors-and-warnings/NU1500.md) |
| Avisos de pacotes assinados (criação e verificação) | [NU3002](./errors-and-warnings/NU3002.md), [NU3018](./errors-and-warnings/NU3018.md), [NU3028](./errors-and-warnings/NU3028.md) |
