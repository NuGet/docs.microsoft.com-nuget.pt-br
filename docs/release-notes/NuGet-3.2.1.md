---
title: Notas de versão do NuGet 3.2.1
description: Notas de versão do NuGet 3.2.1 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 039fabaaacfdffd76fa88ff8183548e97cd4719b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820138"
---
# <a name="nuget-321-release-notes"></a>Notas de versão do NuGet 3.2.1

[Notas de versão do NuGet 3.2](../release-notes/nuget-3.2.md) | [notas de versão do NuGet 3.3](../release-notes/nuget-3.3.md)

3.2.1 o NuGet para a linha de comando foi lançado em 12 de outubro de 2015 com algumas otimizações e correções para a versão 3.2 e está disponível em [dist.nuget.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Melhorias

* Agora, o NuGet usa o arquivo de configuração com o uso de maiusculas original `NuGet.Config`.  Isso é importante em sistemas operacionais de maiusculas e minúsculas [1427](https://github.com/NuGet/Home/issues/1427)
* Restauração do NuGet agora irá ignorar projetos dnx (`*.xproj`) que deve ser processado com `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Otimização de uso da rede quando estiver trabalhando com `index.json` e dados de registro do pacote [1426](https://github.com/NuGet/Home/issues/1426)
* Download de recurso aprimorado tratamento para ser mais robustos com serviços v2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Correções

* NuGet corretamente atualiza `.csproj` / `.vcxproj` referências [1483](https://github.com/NuGet/Home/issues/1483)
* Impedindo que uma pasta. NuGet local sejam criadas quando um SpecialFolders.UserProfile não é possível localizar [1531](https://github.com/NuGet/Home/issues/1531)
* Melhor tratamento de pacotes no cache local está corrompida durante o download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Uma lista completa dos problemas abordados para a extensão de linha de comando e o Visual Studio pode ser encontrada no NuGet GitHub [3.2.1 marco](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>Problemas Conhecidos

Continuamos a rastrear problemas em nossa lista de problemas do GitHub que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)