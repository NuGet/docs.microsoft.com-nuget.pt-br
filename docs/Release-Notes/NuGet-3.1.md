---
title: "Notas de versão do NuGet 3.1 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0fc4d89a-ccca-4d63-85bf-461cd9ced882
description: "Notas de versão do NuGet 3.1 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão 3.1 do NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: eef2b2c1af99671c7ae3874c2c12130f104e88eb
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-31-release-notes"></a>Notas de versão 3.1 do NuGet

[Notas de versão do NuGet 3.0](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 notas de versão](../release-notes/nuget-3.1.1.md)

3.1 NuGet foi lançado em 27 de julho de 2015 como uma extensão de pacote para o SDK de plataforma Universal do Windows para Visual Studio 2015. Fornecemos desta versão com o SDK de plataforma do Windows para que a experiência de desenvolvimento do Windows pode aproveitar o trabalho de plataforma cruzada do NuGet ter sido iniciado anteriormente. Esta versão da extensão NuGet só está disponível para o Visual Studio 2015.

Recomendamos que os desenvolvedores que têm acesso a atualização da Galeria do Visual Studio para a versão mais recente está disponível, como estamos sempre publicando atualizações com novos recursos e correções de bugs.

## <a name="nuget-visual-studio-extension"></a>Extensão do NuGet Visual Studio

Problemas e recursos nesta versão são marcados no GitHub, com o ["3.1 suporte transitiva UWP RTM" Marco](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) no total, é fechada 67 problemas na versão 3.1.

### <a name="new-features"></a>Novos recursos

* `project.json`suporte para suporte de UWP do Windows e do ASP.NET 5
* Instalação do pacote transitiva

Descrição e a definição desses recursos podem ser encontrados em outro lugar na documentação.

### <a name="deprecated"></a>Preterido

Os recursos a seguir não estão mais disponíveis para o Visual Studio 2015:

* Pacotes de nível de solução não podem mais ser instalados

Os recursos a seguir não estão mais disponíveis para o Visual Studio 2015 e projetos que usam o `project.json` especificação

* `install.ps1`e `uninstall.ps1` -esses scripts serão ignorados durante a instalação do pacote, restaurar, atualizar e desinstalar
* Transformações de configuração serão ignoradas
* Conteúdo será executado, mas não foi copiado em um projeto.
    * A equipe está trabalhando para implementar novamente esse recurso, siga a discussão e andamento em: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Problemas conhecidos

Houve um número de problemas conhecidos, fornecido com esta versão.

* Instalação da versão 3.1 com o SDK do Windows 10 desatualizará qualquer versão da extensão do NuGet instalada anteriormente

## <a name="nuget-command-line"></a>Linha de comando do NuGet

O executável de linha de comando do NuGet foi atualizado e movido para um novo local de distribuição para que as versões históricas de nuget.exe podem continuar a ser disponibilizado.  Você pode baixar a versão 3.1 beta do nuget.exe para Windows no: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

O novo local distribuível reside no host dist.nuget.org, com uma estrutura de pastas que segue este modelo:

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>Novos recursos

* NuGet.exe pode restaurar e instalar pacotes em projetos que usam um `project.json` arquivo.
* NuGet.exe pode se conectar e consumir o protocolo de v3 do NuGet em: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Problemas conhecidos ##

1.    Não é possível executar o pacote em relação a um `project.json` arquivo - [928](https://github.com/NuGet/Home/issues/928)
2.    Não há suporte para Mono - [1059](https://github.com/NuGet/Home/issues/1059)
3.    Não é localizado - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    Não é assinado, assim como o http://nuget.org/nuget.exe existente - [1073](https://github.com/NuGet/Home/issues/1073)
