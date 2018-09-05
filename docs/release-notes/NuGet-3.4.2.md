---
title: Notas de versão do NuGet 3.4.2
description: Notas de versão do NuGet 3.4.2 incluindo conhecidos problemas, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549145"
---
# <a name="nuget-342-release-notes"></a>Notas de versão do NuGet 3.4.2

[Notas de versão do NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [notas de versão do NuGet 3.4.3](../release-notes/nuget-3.4.3.md)

O NuGet 3.4.2 foi lançado em 8 de abril de 2016 para abordar vários problemas que foram identificados na 3.4 e 3.4.1 de versão.

## <a name="nugetexe-342-rc-is-now-available"></a>NuGet.exe 3.4.2 RC agora está disponível

Você pode baixar o versão Release candidate do nuget.exe 3.4.2 [aqui](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Atualizações e aprimoramentos

* Aprimoramos consideravelmente o desempenho de atualizações em um cenário específico, onde as atualizações em pacotes com grafos de dependência profunda demoravam muito tempo e parou ao Visual Studio.
* restauração do NuGet sem que o tráfego de rede é 2,5 x – 3 vezes mais rápido dentro do Visual Studio.
* Além dessa alteração, corrigimos um problema em que podemos foram acessando a rede duas vezes quando buscando a atualização de contagem na interface do usuário VS. Isso foi parcialmente responsável por alguns clientes de problemas de tempo limite experientes em 3.4/3.4.1.
* Adicionado suporte para configuração de no_proxy

## <a name="fixes"></a>Correções

* Corrigido um problema no qual origem nuget.org estava ausente nas configurações de NuGet ou configuração após a atualização para 3.4.1.
* Corrigido um problema em que uma alteração de maiusculas e minúsculas para FindPackagesById no 3.4.1 rompe Artifactory.
* Corrigido um problema com o FIPS que causava falhas de restauração do NuGet com nuget.exe.
* Corrigida uma falha ao navegar por fontes com a URL do ícone inválido.
* Correção de problemas com a mesclagem de versões e as entradas de 'Todas as fontes'.

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Problemas conhecidos no 3.4.2 linha de comando do Windows x86 (RC)

Esses problemas serão corrigidos logo na próxima semana antes de que atingimos RTM.

*  Restauração do nuget em execução em uma solução falhará se o arquivo de solução é colocado em uma hierarquia de pastas menor que os arquivos de projeto.
*  A execução do comando de exclusão do nuget em um pacote usando o feed V2 falhará. Use o feed V3.


Para obter uma lista de correções e aprimoramentos nesta versão, confira a lista de problemas [aqui](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).