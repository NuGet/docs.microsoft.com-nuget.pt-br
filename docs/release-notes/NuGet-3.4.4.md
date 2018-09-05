---
title: Notas de versão do NuGet 3.4.4
description: Notas de versão do NuGet 3.4.4 incluindo conhecidos problemas, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547467"
---
# <a name="nuget-344-release-notes"></a>Notas de versão do NuGet 3.4.4

[Notas de versão do NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [notas de versão 3.5 Beta do NuGet](../release-notes/nuget-3.5-Beta.md)

O principal foco desta versão foram as melhorias para a qualidade do 3.4.3 versão do nuget.exe com algumas correções à extensão do Visual Studio.

Você pode baixar o VSIX e nuget.exe [aqui](https://dist.nuget.org/index.html).

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-rtm](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Log de alterações completo](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Lista de problemas](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Alterações

- Aprimoramentos do pacote: Melhorias para empacotamento de símbolos, com o empacotamento `project.json` mais [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- Exibir a exceção quando não há uma falha ao localizar os projetos no comando de atualização [\#605] (https://github.com/NuGet/NuGet.Client/pull/605
- Ler o tipo de pacote de entrada `.nuspec` e `project.json` quando o empacotamento [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- Verifique NuGet.Shared não em um projeto. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Use o tempo limite de envio por push o tempo de limite de resposta HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- Arquivos de pacote com tempos de futuros não terão suas horas de usado [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- Atualizando `NuGet.Core.dll` versão para 2.12.0 para corrigir o problema XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- Dar suporte a v -./NuGet.CommandLine.XPlat \<detalhamento\> \<modo\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- Erro de exibição restaurando sem `project.json` ou `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- Correção de versões de dependência quando as versões necessárias diferem [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)