---
title: Referência de erros e avisos do NuGet
description: Referência completa para avisos e erros emitidos do NuGet durante várias operações do NuGet.
author: JonDouglas
ms.author: jodou
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 196b0650866902d753b261dc1bd196ea6601b9df
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775425"
---
# <a name="errors-and-warnings"></a>Erros e avisos

No NuGet 4.3.0 +, erros e avisos são numerados conforme descrito neste tópico e fornecem informações detalhadas para ajudá-lo a resolver os problemas envolvidos.

Os erros e avisos listados aqui estão disponíveis somente com projetos [baseados em PackageReference](../consume-packages/package-references-in-project-files.md) e NuGet 4.3.0 +. O NuGet também respeita as propriedades do MSBuild para suprimir avisos ou promovê-los para erros. Para obter mais informações, consulte [como: suprimir avisos do compilador](/visualstudio/ide/how-to-suppress-compiler-warnings) na documentação do Visual Studio.

## <a name="errors"></a>Errors

| Grupo | Números de erro |
| --- | --- |
| Erros de entrada inválidos | [NU1001](./errors-and-warnings/NU1001.md), [NU1002](./errors-and-warnings/NU1002.md), [NU1003](./errors-and-warnings/NU1003.md) |
| Erros de pacote e projeto ausentes | [NU1100](./errors-and-warnings/NU1100.md), [NU1101](./errors-and-warnings/NU1101.md), [NU1102](./errors-and-warnings/NU1102.md), [NU1103](./errors-and-warnings/NU1103.md), [NU1104](./errors-and-warnings/NU1104.md), [NU1105](./errors-and-warnings/NU1105.md), [NU1106](./errors-and-warnings/NU1106.md), [NU1107](./errors-and-warnings/NU1107.md), [NU1108](./errors-and-warnings/NU1108.md) |
| Erros de compatibilidade | [NU1201](./errors-and-warnings/NU1201.md), [NU1202](./errors-and-warnings/NU1202.md), [NU1203](./errors-and-warnings/NU1203.md), [NU1401](./errors-and-warnings/NU1401.md) |
| Erros internos do NuGet | [NU1000](./errors-and-warnings/NU1000.md) |
| Erros de pacotes assinados (criação e verificação) | [NU3001](./errors-and-warnings/NU3001.md), [NU3004](./errors-and-warnings/NU3004.md), [NU3005](./errors-and-warnings/NU3005.md), [NU3008](./errors-and-warnings/NU3008.md), [NU3034](./errors-and-warnings/NU3034.md)|
| Erros de pacote | [NU5000](./errors-and-warnings/NU5000.md), [NU5001](./errors-and-warnings/NU5001.md), [NU5002](./errors-and-warnings/NU5002.md), [NU5003](./errors-and-warnings/NU5003.md), [NU5004](./errors-and-warnings/NU5004.md), [NU5005](./errors-and-warnings/NU5005.md), [NU5007](./errors-and-warnings/NU5007.md), [NU5008](./errors-and-warnings/NU5008.md), [NU5009](./errors-and-warnings/NU5009.md), [NU5010](./errors-and-warnings/NU5010.md), [NU5011](./errors-and-warnings/NU5011.md), [NU5012](./errors-and-warnings/NU5012.md), [NU5013](./errors-and-warnings/NU5013.md), [NU5014](./errors-and-warnings/NU5014.md), [NU5015](./errors-and-warnings/NU5015.md), [NU5016](./errors-and-warnings/NU5016.md), [NU5017](./errors-and-warnings/NU5017.md), [NU5018](./errors-and-warnings/NU5018.md), [NU5019](./errors-and-warnings/NU5019.md), [NU5020](./errors-and-warnings/NU5020.md), [NU5021](./errors-and-warnings/NU5021.md), [NU5022](./errors-and-warnings/NU5022.md), [NU5023](./errors-and-warnings/NU5023.md), [NU5024](./errors-and-warnings/NU5024.md), [NU5025](./errors-and-warnings/NU5025.md), [NU5026](./errors-and-warnings/NU5026.md), [NU5027](./errors-and-warnings/NU5027.md), [NU5028](./errors-and-warnings/NU5028.md), [NU5029](./errors-and-warnings/NU5029.md), [NU5036](./errors-and-warnings/NU5036.md)
| Erros de pacote de licença específica | [NU5030](./errors-and-warnings/NU5030.md), [NU5031](./errors-and-warnings/NU5031.md), [NU5032](./errors-and-warnings/NU5032.md), [NU5033](./errors-and-warnings/NU5033.md), [NU5034](./errors-and-warnings/NU5034.md), [NU5035](./errors-and-warnings/NU5035.md)

## <a name="warnings"></a>Warnings

| Grupo | Números de aviso |
| --- | --- |
| Avisos de entrada inválidos | [NU1501](./errors-and-warnings/NU1501.md), [NU1502](./errors-and-warnings/NU1502.md), [NU1503](./errors-and-warnings/NU1503.md) |
| Avisos de versão de pacote inesperados | [NU1601](./errors-and-warnings/NU1601.md), [NU1602](./errors-and-warnings/NU1602.md), [NU1603](./errors-and-warnings/NU1603.md), [NU1604](./errors-and-warnings/NU1604.md), [NU1605](./errors-and-warnings/NU1605.md), [NU1606](./errors-and-warnings/NU1108.md), [NU1607](./errors-and-warnings/NU1107.md) |
| Avisos de conflito de resolvedor | [NU1608](./errors-and-warnings/NU1608.md) |
| Avisos de fallback de pacote | [NU1701](./errors-and-warnings/NU1701.md) |
| Avisos de feed | [NU1801](./errors-and-warnings/NU1801.md) |
| Avisos internos do NuGet | [NU1500](./errors-and-warnings/NU1500.md) |
| Avisos de pacotes assinados (criação e verificação) | [NU3000](./errors-and-warnings/NU3000.md), [NU3002](./errors-and-warnings/NU3002.md), [NU3003](./errors-and-warnings/NU3003.md), [NU3006](./errors-and-warnings/NU3006.md), [NU3007](./errors-and-warnings/NU3007.md), [NU3009](./errors-and-warnings/NU3009.md), [NU3010](./errors-and-warnings/NU3010.md), [NU3011](./errors-and-warnings/NU3011.md), [NU3012](./errors-and-warnings/NU3012.md), [NU3013](./errors-and-warnings/NU3013.md), [NU3014](./errors-and-warnings/NU3014.md), [NU3015](./errors-and-warnings/NU3015.md), [NU3016](./errors-and-warnings/NU3016.md), [NU3017](./errors-and-warnings/NU3017.md), [NU3018](./errors-and-warnings/NU3018.md), [NU3019](./errors-and-warnings/NU3019.md), [NU3020](./errors-and-warnings/NU3020.md), [NU3021](./errors-and-warnings/NU3021.md), [NU3022](./errors-and-warnings/NU3022.md), [NU3023,](./errors-and-warnings/NU3023.md) [NU3024, NU3025](./errors-and-warnings/NU3024.md), [NU3026](./errors-and-warnings/NU3026.md), [NU3027, NU3028](./errors-and-warnings/NU3027.md) [, NU3029](./errors-and-warnings/NU3028.md) [, NU3030](./errors-and-warnings/NU3029.md), [NU3031](./errors-and-warnings/NU3031.md), [NU3032](./errors-and-warnings/NU3032.md), [NU3033](./errors-and-warnings/NU3033.md), [NU3035](./errors-and-warnings/NU3035.md), [NU3036](./errors-and-warnings/NU3036.md), [NU3037](./errors-and-warnings/NU3037.md), [NU3038](./errors-and-warnings/NU3038.md), [NU3040](./errors-and-warnings/NU3040.md) [](./errors-and-warnings/NU3025.md) [](./errors-and-warnings/NU3030.md) |
| Avisos de pacote | [NU5100](./errors-and-warnings/NU5100.md), [NU5101](./errors-and-warnings/NU5101.md), [NU5102](./errors-and-warnings/NU5102.md), [NU5103](./errors-and-warnings/NU5103.md), [NU5104](./errors-and-warnings/NU5104.md), [NU5105](./errors-and-warnings/NU5105.md), [NU5106](./errors-and-warnings/NU5106.md), [NU5107](./errors-and-warnings/NU5107.md), [NU5108](./errors-and-warnings/NU5108.md), [NU5109](./errors-and-warnings/NU5109.md), [NU5110](./errors-and-warnings/NU5110.md), [NU5111](./errors-and-warnings/NU5111.md), [NU5112](./errors-and-warnings/NU5112.md), [NU5114](./errors-and-warnings/NU5114.md), [NU5115](./errors-and-warnings/NU5115.md), [NU5116](./errors-and-warnings/NU5116.md), [NU5117](./errors-and-warnings/NU5117.md), [NU5118](./errors-and-warnings/NU5118.md), [NU5119](./errors-and-warnings/NU5119.md), [NU5120](./errors-and-warnings/NU5120.md), [NU5121](./errors-and-warnings/NU5121.md), [NU5122](./errors-and-warnings/NU5122.md), [NU5123](./errors-and-warnings/NU5123.md), [NU5127](./errors-and-warnings/NU5127.md), [NU5128](./errors-and-warnings/NU5128.md), [NU5129](./errors-and-warnings/NU5129.md), [NU5130](./errors-and-warnings/NU5130.md), [NU5131](./errors-and-warnings/NU5131.md), [NU5500](./errors-and-warnings/NU5500.md)
| Avisos de pacote específico da licença | [NU5124](./errors-and-warnings/NU5124.md), [NU5125](./errors-and-warnings/NU5125.md)
| Ícone de avisos de pacote específico | [NU5046](./errors-and-warnings/NU5046.md), [NU5047](./errors-and-warnings/NU5047.md), [NU5048](./errors-and-warnings/NU5048.md)
