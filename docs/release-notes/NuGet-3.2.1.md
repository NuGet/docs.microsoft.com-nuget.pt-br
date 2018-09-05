---
title: Notas de versão do NuGet 3.2.1
description: Notas de versão do NuGet 3.2.1 incluindo conhecidos problemas, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548184"
---
# <a name="nuget-321-release-notes"></a>Notas de versão do NuGet 3.2.1

[Notas de versão do NuGet 3.2](../release-notes/nuget-3.2.md) | [notas de versão do NuGet 3.3](../release-notes/nuget-3.3.md)

O NuGet 3.2.1 para a linha de comando foi lançado em 12 de outubro de 2015 com algumas otimizações e correções para a versão 3.2 e está disponível no [dist.nuget.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Melhorias

* Agora, o NuGet usa o arquivo de configuração com a capitalização original da `NuGet.Config`.  Isso é importante em sistemas operacionais de diferencia maiusculas de minúsculas [1427](https://github.com/NuGet/Home/issues/1427)
* Restauração do NuGet agora irá ignorar os projetos dnx (`*.xproj`) que devem ser processadas com `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Com otimização de utilização da rede ao trabalhar com `index.json` e dados de registro do pacote [1426](https://github.com/NuGet/Home/issues/1426)
* Download de um recurso aprimorado de tratamento para ser mais robusta com os serviços de v2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Correções

* Atualização do NuGet atualiza corretamente `.csproj` / `.vcxproj` referências [1483](https://github.com/NuGet/Home/issues/1483)
* Impedindo que uma pasta local .nuget sejam criadas quando um SpecialFolders.UserProfile não é possível localizar [1531](https://github.com/NuGet/Home/issues/1531)
* Manipulação de pacotes no cache local que estão corrompidos durante o download melhorada [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Uma lista completa dos problemas abordados para a extensão de linha de comando e o Visual Studio pode ser encontrada no NuGet GitHub [3.2.1 marco](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>Problemas Conhecidos

Continuamos a acompanhar os problemas em nossa lista de problemas do GitHub que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)