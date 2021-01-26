---
title: Notas de versão do NuGet 3,0 RC
description: Notas de versão do NuGet 3,0 RC incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776571"
---
# <a name="nuget-30-rc-release-notes"></a>Notas de versão do NuGet 3,0 RC

Notas de versão do [NuGet 3,0 beta](../release-notes/nuget-3.0-beta.md)  |  [Notas de versão do NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)

O NuGet 3,0 RC foi lançado em 29 de abril de 2015 com a versão do Visual Studio 2015 RC. Esta versão tem várias correções de bugs importantes, melhorias de desempenho e atualizações para dar suporte às novas estruturas.  Ele só está disponível para o Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>Foco contínuo no desempenho

A estabilidade e o desempenho das consultas do NuGet continuam a ser um tópico dinâmico no qual estamos nos concentrando.  Com esta versão, você deve começar a ver operações de pesquisa muito rápidas na interface do usuário e no site do NuGet.  Estamos monitorando o serviço e como você pode usar o serviço para que possamos continuar a ajustar essas operações.

## <a name="significant-issues-resolved"></a>Problemas significativos resolvidos

Para estabilizar os clientes do NuGet, resolvemos muitos problemas como parte desta versão.  Aqui está apenas uma breve lista de alguns dos problemas mais importantes resolvidos:

* Como parte da renomeação da estrutura K para ASP.NET 5, os monikers da estrutura foram atualizados para manipular o [link](https://github.com/NuGet/Home/issues/215) DNX e dnxcore
* Documentação de ajuda adicionada de links no [link](https://github.com/NuGet/Home/issues/232) da interface do usuário do Visual Studio
* Melhor manipulação de referências complexas no `.nuspec` com [link](https://github.com/NuGet/Home/issues/276) de referências de estrutura delimitada por vírgulas
* Corrigido o suporte para o [link](https://github.com/NuGet/Home/issues/253) de culturas japonesas
* Cliente atualizado para permitir que projetos ASP.NET 5 usem o [link](https://github.com/NuGet/Home/issues/219) de novos pontos de extremidade v3
* Atualizado para melhor manipular a pasta de pacotes com o [link](https://github.com/NuGet/Home/issues/56) de controle do código-fonte
* [Link](https://github.com/NuGet/Home/issues/17) de suporte fixo para pacotes satélite
* [Link](https://github.com/NuGet/Home/issues/18) de suporte corrigido para arquivos de conteúdo específicos da estrutura

## <a name="github-presence-overhaul"></a>Revisão de presença do GitHub

Fizemos algumas alterações em nossos [repositórios de código-fonte no GitHub](http://github.com/nuget/home).  Se você tiver problemas com o cliente NuGet do Visual Studio, os comandos do PowerShell ou o executável de linha de comando, poderá registrar esses problemas e monitorar seu progresso em nossa [lista de problemas do repositório inicial do GitHub](http://github.com/nuget/home/issues).  Estamos acompanhando problemas para a galeria em nosso [repositório NuGetGallery do GitHub](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Fique atento

Fique atento ao [nosso blog](http://blog.nuget.org) para obter mais progresso e anúncios para o NuGet 3,0!