---
title: Notas de versão do NuGet 3.0 RC
description: Notas de versão do NuGet 3.0 RC incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551713"
---
# <a name="nuget-30-rc-release-notes"></a>Notas de versão do NuGet 3.0 RC

[Notas de versão do NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md) | [notas de versão do NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md)

RC do NuGet 3.0 foi lançado em 29 de abril de 2015 com o lançamento do Visual Studio 2015 RC. Esta versão tem uma série de correções de bugs importantes, melhorias de desempenho e as atualizações para dar suporte a novas estruturas.  Ele só está disponível para o Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>Sobre o desempenho

Estabilidade e desempenho de consultas do NuGet continuam sendo um assunto que estamos nos concentrando no.  Com esta versão, você deve iniciar ver as operações de pesquisa muito rápida no site de UI NuGet e.  Estamos monitorando o serviço e como usar o serviço para que possamos continuar a ajustar essas operações.

## <a name="significant-issues-resolved"></a>Problemas significativos resolvidos

Para se estabilizar os clientes do NuGet, resolvemos muitos problemas como parte desta versão.  Aqui é apenas uma lista breve de alguns dos problemas mais importantes que são resolvidos:

* Como parte da renomeação do framework K para ASP.NET 5, monikers de estrutura foram atualizados para lidar com o dnx e dnxcore [link](https://github.com/NuGet/Home/issues/215)
* Adicionada a documentação de ajuda de links na IU do Visual Studio [link](https://github.com/NuGet/Home/issues/232)
* Melhor tratamento de referências complexas em `.nuspec` com referências de estrutura delimitada por vírgulas de [link](https://github.com/NuGet/Home/issues/276)
* Corrigido o suporte para culturas japonês [link](https://github.com/NuGet/Home/issues/253)
* O cliente atualizado para permitir que os projetos ASP.NET 5 usar os novos pontos de extremidade v3 [link](https://github.com/NuGet/Home/issues/219)
* Atualizado para melhor identificador de pasta de pacotes com controle do código-fonte [link](https://github.com/NuGet/Home/issues/56)
* Corrigido o suporte para pacotes satélite [link](https://github.com/NuGet/Home/issues/17)
* Corrigido o suporte para arquivos de conteúdo específicos de estrutura [link](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>Revisão de presença do GitHub

Fizemos algumas alterações em nossos [fonte de repositórios de código no GitHub](http://github.com/nuget/home).  Se você tiver problemas com o cliente do NuGet Visual Studio, os comandos do Powershell ou da linha de comando executável faça esses problemas e monitorar seu progresso em nossa [lista de problemas do repositório GitHub Home](http://github.com/nuget/home/issues).  Estamos acompanhando problemas para a Galeria em nossa [repositório GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Fique ligado

Por favor, fique atento [nosso blog](http://blog.nuget.org) para obter mais progresso e anúncios para NuGet 3.0!