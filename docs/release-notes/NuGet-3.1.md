---
title: Notas de versão 3.1 do NuGet
description: Notas de versão do NuGet 3.1, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545341"
---
# <a name="nuget-31-release-notes"></a>Notas de versão 3.1 do NuGet

[Notas de versão do NuGet 3.0](../release-notes/nuget-3.0.0.md) | [notas de versão do NuGet 3.1.1](../release-notes/nuget-3.1.1.md)

O NuGet 3.1 foi lançado em 27 de julho de 2015 como uma extensão agrupada para o SDK da plataforma Windows Universal para Visual Studio 2015. Enviamos essa versão com o SDK da plataforma Windows para que a experiência de desenvolvimento do Windows pode aproveitar o trabalho de plataforma cruzada do NuGet que tivesse sido iniciado. Esta versão da extensão NuGet só está disponível para o Visual Studio 2015.

Recomendamos que os desenvolvedores que têm acesso a atualização da Galeria do Visual Studio para a versão mais recente que está disponível, como estamos sempre publicando atualizações com novos recursos e correções de bugs.

## <a name="nuget-visual-studio-extension"></a>Extensão do NuGet Visual Studio

Problemas e recursos nesta versão são marcados no GitHub com o [Marco "3.1 suporte transitiva RTM UWP"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) no total, fechamos 67 problemas na versão 3.1.

### <a name="new-features"></a>Novos recursos

* `project.json` suporte para suporte de UWP do Windows e do ASP.NET 5
* Instalação de pacote transitivo

Descrição e a definição desses recursos podem ser encontradas em outro lugar na documentação.

### <a name="deprecated"></a>Preterido

Os seguintes recursos não estão mais disponíveis para o Visual Studio 2015:

* Pacotes de nível de solução não podem mais ser instalados

Os seguintes recursos não estão mais disponíveis para o Visual Studio 2015 e projetos que usam o `project.json` especificação

* `install.ps1` e `uninstall.ps1` -esses scripts serão ignorados durante a instalação do pacote, restaurar, atualizar e desinstalar
* Transformações de configuração serão ignoradas
* Conteúdo será executado, mas não copiado para um projeto.
    * A equipe está trabalhando para implementar novamente esse recurso, acompanhe a discussão e andamento em: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Problemas Conhecidos

Houve um número de problemas conhecidos entregues com esta versão.

* Instalação da versão 3.1 com o SDK do Windows 10 desatualizará qualquer versão da extensão NuGet instalada anteriormente

## <a name="nuget-command-line"></a>Linha de comando do NuGet

O executável de linha de comando do NuGet foi atualizado e movido para um novo local pode ser distribuído para que as versões históricas de nuget.exe podem continuar a serem disponibilizados.  Você pode baixar a versão 3.1 beta do nuget.exe para Windows em: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

O novo local distribuível reside no host dist.nuget.org, com uma estrutura de pastas que segue este modelo:

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>Novos recursos

* NuGet.exe pode restaurar e instalar os pacotes em projetos que usam um `project.json` arquivo.
* NuGet.exe pode se conectar e consumir o protocolo v3 de NuGet em: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Problemas Conhecidos ##

1.    Não é possível executar o pacote em relação a um `project.json` arquivo - [928](https://github.com/NuGet/Home/issues/928)
2.    Não é compatível com Mono - [1059](https://github.com/NuGet/Home/issues/1059)
3.    Não é localizado - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    Não é assinado, assim como o existente http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)
