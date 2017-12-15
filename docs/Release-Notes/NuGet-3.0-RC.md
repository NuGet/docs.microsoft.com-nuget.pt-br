---
title: "Notas de versão do NuGet 3.0 RC | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: cd0c102f-bc33-4aa2-a921-61fa21d42b28
description: "Notas de versão do NuGet 3.0 RC, incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão RC do NuGet 3.0, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5d0eeae479617bc30901b599251628f72950cc67
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-rc-release-notes"></a>Notas de versão do NuGet 3.0 RC

[Notas de versão do NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md) | [notas de versão do NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md)

Com o lançamento do Visual Studio 2015 RC, NuGet 3.0 RC foi lançado em 29 de abril de 2015. Esta versão tem um número de correções de bugs importantes, melhorias de desempenho e atualizações para dar suporte as novas estruturas.  Só está disponível para Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>Enfoque no desempenho

Estabilidade e desempenho de consultas do NuGet continuam a ser um assunto foco.  Com esta versão, você começará a ver as operações de pesquisa muito rápida do NuGet UI e do site.  Estamos monitorando o serviço e como usar o serviço para que possamos continuar a ajustar essas operações.

## <a name="significant-issues-resolved"></a>Problemas significativos resolvidos

Para estabilizar os clientes do NuGet, solucionado muitos problemas como parte desta versão.  Aqui está a apenas uma lista breve de alguns dos problemas mais importantes resolvidos:

* Como parte da renomeação do framework K para ASP.NET 5, identificadores de framework foram atualizados para tratar dnx e dnxcore [link](https://github.com/NuGet/Home/issues/215)
* Adicionada a documentação de ajuda de links na interface do usuário do Visual Studio [link](https://github.com/NuGet/Home/issues/232)
* Melhor tratamento de referências complexas em `.nuspec` com referências de framework delimitada por vírgulas [link](https://github.com/NuGet/Home/issues/276)
* Corrigido o suporte para japonês culturas [link](https://github.com/NuGet/Home/issues/253)
* O cliente atualizado para permitir que os projetos ASP.NET 5 usar os novos pontos de extremidade v3 [link](https://github.com/NuGet/Home/issues/219)
* Pasta de pacotes de identificador atualizado para melhor com controle de origem [link](https://github.com/NuGet/Home/issues/56)
* Corrigido o suporte para pacotes de satélite [link](https://github.com/NuGet/Home/issues/17)
* Corrigido o suporte para os arquivos de conteúdo específica da estrutura [link](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>Revisão de presença do GitHub

Fizemos algumas alterações para nosso [da fonte de repositórios de código no GitHub](http://github.com/nuget/home).  Se você tiver problemas com o cliente do NuGet Visual Studio, os comandos do Powershell ou a linha de comando executável faça esses problemas e monitorar seu progresso em nosso [lista de problemas do repositório GitHub Home](http://github.com/nuget/home/issues).  Estamos acompanhando problemas para a galeria no nosso [repositório GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Fique atento

Fique atento [nosso blog](http://blog.nuget.org) para mais de progresso e avisos do NuGet 3.0!