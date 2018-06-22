---
title: Notas de versão do NuGet 3.4.2
description: Notas de versão do NuGet 3.4.2 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 88d29a84e280433663ab6c1c04ae16e1329420f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819660"
---
# <a name="nuget-342-release-notes"></a>Notas de versão do NuGet 3.4.2

[Notas de versão do NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [notas de versão do NuGet 3.4.3](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 foi lançado em 8 de abril de 2016 para abordar vários problemas que foram identificados no 3.4 e 3.4.1 de versão.

## <a name="nugetexe-342-rc-is-now-available"></a>NuGet.exe 3.4.2 RC agora está disponível

Você pode baixar a versão release candidate do nuget.exe 3.4.2 [aqui](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Atualizações e aprimoramentos

* Aprimoramos significativamente o desempenho de atualizações em um cenário específico, onde as atualizações em pacotes com gráficos de dependência profunda levaram muito tempo e suspenso Visual Studio.
* restauração do NuGet sem o tráfego de rede é 2,5 x – 3 vezes mais rápido do Visual Studio.
* Além dessa alteração, corrigimos um problema em que podemos foram atingir a rede duas vezes quando buscar a atualização de contagem na IU do VS. Isso foi parcialmente responsável por alguns clientes de problemas de tempo limite experiência em 3.4/3.4.1.
* Adicionado suporte para configuração de no_proxy

## <a name="fixes"></a>Correções

* Corrigido um problema em que nuget.org fonte estava ausente nas configurações do NuGet ou de configuração após a atualização para 3.4.1.
* Corrigido um problema em que uma alteração de maiusculas e minúsculas para FindPackagesById no 3.4.1 quebras Artifactory.
* Corrigido um problema com o FIPS que causou a falhas de restauração do NuGet com nuget.exe.
* Corrigido uma falha durante a navegação de fontes com a URL do ícone inválido.
* Correção de problemas com a mesclagem de versões e as entradas de 'Todas as fontes'.

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Problemas conhecidos no 3.4.2 linha de comando do Windows x86 (RC)

Esses problemas serão corrigidos antecipado próxima semana antes de que atingiremos RTM.

*  Restauração do nuget em execução em uma solução falhará se o arquivo de solução é colocado em uma hierarquia de pasta menor que os arquivos de projeto.
*  Executar o comando de exclusão do nuget em um pacote usando o feed V2 falhará. Use o feed V3.


Para obter uma lista de correções e aperfeiçoamentos desta versão, confira a lista de problemas [aqui](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).