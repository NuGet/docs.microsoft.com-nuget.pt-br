---
title: Notas de versão do NuGet 3.4.4
description: Notas de versão do NuGet 3.4.4 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780223"
---
# <a name="nuget-344-release-notes"></a>Notas de versão do NuGet 3.4.4

Notas de versão do [NuGet 3.4.3](../release-notes/nuget-3.4.3.md)  |  [Notas de versão do NuGet 3,5-Beta](../release-notes/nuget-3.5-Beta.md)

O foco principal dessa versão foi aprimoramentos para a qualidade da versão 3.4.3 do nuget.exe com algumas correções para a extensão do Visual Studio também.

Você pode baixar o VSIX e o nuget.exe [aqui](https://dist.nuget.org/index.html).

## <a name="344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Changelog completo](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Lista de problemas](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Alterações

- Aprimoramentos de pacote: aprimoramentos para empacotar símbolos, empacotamento com `project.json` e mais [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606)
- Exibir exceção quando houver uma falha ao encontrar projetos no comando de atualização [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605
- Ler o tipo de pacote da entrada `.nuspec` e `project.json` ao empacotar [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)
- Tornar NuGet. Shared não é um projeto. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Use o tempo limite de push como o tempo limite de resposta HTTP [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599)
- Os arquivos de pacote com tempos futuros não terão seus horários usados [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)
- Atualizando `NuGet.Core.dll` a versão para 2.12.0 para corrigir o problema de XML [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)
- Support./NuGet.CommandLine.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)
- Exibir erro ao restaurar sem `project.json` ou `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590)
- Corrigindo as versões de dependência quando as versões necessárias forem diferentes [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)