---
title: Notas de versão do NuGet 3,4-RC
description: Notas de versão do NuGet 3,4 RC incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780243"
---
# <a name="nuget-34-rc-release-notes"></a>Notas de versão do NuGet 3,4-RC

Notas de versão do [NuGet 3,3](../release-notes/nuget-3.3.md)  |  [Notas de versão do NuGet 3,4](../release-notes/nuget-3.4.md)

O NuGet 3,4-RC foi lançado em 3 de março de 2016 juntamente com o Visual Studio 2015 atualização 2 RC e foi criado com algumas filosofias nas mentes:

* Suporte de plataforma cruzada
* Melhorias de desempenho
* Melhorias secundárias da interface do usuário

Os recursos a seguir estão disponíveis neste RC, com mais planejamento para a versão final de 3,4.

## <a name="new-features"></a>Novos recursos

* Os clientes NuGet agora dão suporte à codificação de conteúdo gzip de repositórios
* Suporte para PDBs de pacotes em projetos xproj
* Suporte para ações de compilação do iOS e Android no elemento contentFiles
* Suporte para os monikers do netstandard e do netstandardapp Framework

## <a name="new-user-interface-features"></a>Novos recursos da interface do usuário

* Melhorias significativas de desempenho, especialmente nas guias instalado, atualizações e consolidar
* As guias instaladas e atualizadas agora são classificadas alfabeticamente
* Adicionado um botão Atualizar que permite que uma pesquisa seja atualizada

## <a name="updates-and-improvements"></a>Atualizações e aprimoramentos

* Os pacotes referenciados no `project.json` que têm uma versão flutuante não serão atualizados em cada compilação. Em vez disso, eles serão atualizados somente quando forçados a restaurar, limpar, recompilar ou modificar `project.json` .
* as fontes de repositório nuget.org não são mais forçadas para uma configuração de projeto quando você usa a interface do usuário de configuração do NuGet.
* O NuGet não restaura mais os pacotes em projetos compartilhados nem grava um arquivo de bloqueio.
* Melhoramos a falha de rede e a manipulação de tentativas para servidores inacessíveis ou lentos para responder.
* Os comportamentos de teclado e mouse são aprimorados na interface do usuário do Gerenciador de pacotes do Visual Studio.
* Agora, damos suporte ao `project.json` esquema mais recente em DNX.

## <a name="known-issues"></a>Problemas conhecidos

Continuamos a acompanhar problemas em nossa lista de problemas do GitHub, que pode ser encontrada em: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)