---
title: Notas de versão do NuGet 3.4.2
description: Notas de versão do NuGet 3.4.2 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780256"
---
# <a name="nuget-342-release-notes"></a>Notas de versão do NuGet 3.4.2

Notas de versão do [NuGet 3.4.1](../release-notes/nuget-3.4.1.md)  |  [Notas de versão do NuGet 3.4.3](../release-notes/nuget-3.4.3.md)

O NuGet 3.4.2 foi lançado em 8 de abril de 2016 para resolver vários problemas identificados na versão 3,4 e 3.4.1.

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe o 3.4.2 RC já está disponível

Você pode baixar a versão Release Candidate do nuget.exe 3.4.2 [aqui](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Atualizações e aprimoramentos

* Melhoramos significativamente o desempenho das atualizações em um cenário específico, em que as atualizações em pacotes com grafos de dependência profunda levaram muito tempo e travaram o Visual Studio.
* a restauração do NuGet sem tráfego de rede é 2,5 x a 3 vezes mais rápido no Visual Studio.
* Além dessa alteração, corrigimos um problema em que estávamos atingindo a rede duas vezes ao buscar a contagem de atualizações na interface do usuário do VS. Isso foi parcialmente responsável por alguns problemas de tempo limite que os clientes experimentaram em 3.4/3.4.1.
* Adicionado suporte para no_proxy configuração

## <a name="fixes"></a>Correções

* Corrigido um problema em que a origem do nuget.org estava ausente nas configurações do NuGet ou na configuração após a atualização para o 3.4.1.
* Corrigido um problema em que uma alteração de maiúsculas e minúsculas em FindPackagesById no artefato de quebras de 3.4.1.
* Correção de um problema com o FIPS que causou falhas com a restauração do NuGet com nuget.exe.
* Correção de uma falha ao procurar fontes com URL de ícone inválido.
* Correção de problemas com as versões e entradas de mesclagem de ' todas as fontes '.

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Problemas conhecidos no 3.4.2 Windows x86 CommandLine (RC)

Esses problemas serão corrigidos no início da próxima semana antes de atingirmos o RTM.

*  A execução da restauração do NuGet em uma solução falhará se o arquivo da solução for colocado em uma hierarquia de pastas inferior aos arquivos do projeto.
*  A execução do comando de exclusão do NuGet em um pacote usando o feed v2 falhará. Em vez disso, use o feed v3.


Para obter uma lista completa de correções e aprimoramentos nesta versão, confira a lista de problemas [aqui](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).