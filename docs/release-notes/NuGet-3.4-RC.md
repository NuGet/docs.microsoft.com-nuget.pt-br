---
title: Notas de versão do RC 3.4 do NuGet
description: Notas de versão do NuGet 3.4 RC incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546748"
---
# <a name="nuget-34-rc-release-notes"></a>Notas de versão do RC 3.4 do NuGet

[Notas de versão do NuGet 3.3](../release-notes/nuget-3.3.md) | [notas de versão do NuGet 3.4](../release-notes/nuget-3.4.md)

RC do NuGet 3.4 foi lançado 3 de março de 2016, juntamente com o Visual Studio 2015 atualização 2 RC e foi criado com alguns princípios em mente:

* Suporte de plataforma cruzada
* Melhorias de desempenho
* Pequenos aperfeiçoamentos de interface do usuário

Os seguintes recursos estão disponíveis neste RC, com mais planejado para a versão final 3.4.

## <a name="new-features"></a>Novos recursos

* Os clientes do NuGet agora dão suporte a codificação de conteúdo gzip de repositórios
* Suporte para PDBs de pacotes em projetos xproj
* Suporte para iOS e ações de build do Android no elemento contentFiles
* Suporte para o netstandard e netstandardapp monikers de estrutura

## <a name="new-user-interface-features"></a>Novos recursos de Interface do usuário

* Melhorias de desempenho significativas, especialmente nas guias instalado, as atualizações e consolidar
* Instalado e guias de atualizações agora estão classificadas em ordem alfabética
* Adicionado um botão de atualização que permite que uma pesquisa a ser atualizado

## <a name="updates-and-improvements"></a>Atualizações e aprimoramentos

* Pacotes referenciados no `project.json` que têm um flutuante versão não será atualizada em cada compilação. Em vez disso, eles serão atualizados somente quando forçado a restaurar, limpar, recompilar ou modificar `project.json`.
* origens de repositório de NuGet.org não são forçadas em uma configuração de projeto quando você usa a interface do usuário de configuração do NuGet.
* Não há mais o NuGet restaura pacotes em projetos compartilhados nem grava um arquivo de bloqueio.
* Nós aprimoramos falha de rede e tente novamente o tratamento para servidores inacessíveis ou lento para responder.
* Comportamentos de teclado e mouse estão aprimorados na UI do Gerenciador de pacotes do Visual Studio.
* Agora, damos suporte a versão mais recente `project.json` esquema em DNX.

## <a name="known-issues"></a>Problemas Conhecidos

Continuamos a acompanhar os problemas em nossa lista de problemas do GitHub que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)