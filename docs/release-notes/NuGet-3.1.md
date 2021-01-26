---
title: Notas de versão do NuGet 3,1
description: Notas de versão do NuGet 3,1 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776534"
---
# <a name="nuget-31-release-notes"></a>Notas de versão do NuGet 3,1

Notas de versão do [NuGet 3,0](../release-notes/nuget-3.0.0.md)  |  [Notas de versão do NuGet 3.1.1](../release-notes/nuget-3.1.1.md)

O NuGet 3,1 foi lançado em 27 de julho de 2015 como uma extensão agrupada para o SDK do Plataforma Universal do Windows para Visual Studio 2015. Fornecemos esta versão com o SDK da plataforma Windows para que a experiência de desenvolvimento do Windows pudesse aproveitar o trabalho de plataforma cruzada do NuGet que foi iniciado anteriormente. Esta versão de extensão NuGet só está disponível para o Visual Studio 2015.

Recomendamos que esses desenvolvedores tenham acesso à atualização da galeria do Visual Studio para a versão mais recente disponível, pois estamos sempre publicando atualizações com correções de bugs e novos recursos.

## <a name="nuget-visual-studio-extension"></a>Extensão do NuGet do Visual Studio

Os problemas e os recursos desta versão são marcados no GitHub com a [etapa "suporte transitivo do UWP da 3,1 RTM"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  no total, fechamos 67 problemas na versão 3,1.

### <a name="new-features"></a>Novos recursos

* `project.json` suporte para o Windows UWP e suporte a ASP.NET 5
* Instalação de pacote transitiva

A descrição e a definição desses recursos podem ser encontradas em outro lugar na documentação.

### <a name="deprecated"></a>Preterido

Os seguintes recursos não estão mais disponíveis para o Visual Studio 2015:

* Pacotes de nível de solução não podem mais ser instalados

Os recursos a seguir não estão mais disponíveis para o Visual Studio 2015 e projetos que usam a `project.json` especificação

* `install.ps1` e `uninstall.ps1` -esses scripts serão ignorados durante a instalação, restauração, atualização e desinstalação do pacote
* As transformações de configuração serão ignoradas
* O conteúdo será transportado, mas não copiado em um projeto.
    * A equipe está trabalhando para implementar esse recurso novamente, siga a discussão e o progresso em: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Problemas conhecidos

Houve uma série de problemas conhecidos fornecidos com esta versão.

* A instalação da versão 3,1 com o SDK do Windows 10 fará o downgrade de qualquer versão da extensão do NuGet que foi instalada anteriormente

## <a name="nuget-command-line"></a>Linha de comando do NuGet

O executável de linha de comando do NuGet foi atualizado e movido para um novo local de distribuição para que as versões históricas do nuget.exe possam continuar a ser disponibilizadas.  Você pode baixar a versão beta 3,1 do nuget.exe para Windows em: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

O novo local distribuível reside no host dist.nuget.org, com uma estrutura de pastas que segue este modelo:

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a>Novos recursos

* nuget.exe pode restaurar e instalar pacotes em projetos que usam um `project.json` arquivo.
* nuget.exe pode se conectar e consumir o protocolo NuGet v3 em: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Problemas conhecidos ##

1.    Não é possível executar o pacote em um `project.json` arquivo- [928](https://github.com/NuGet/Home/issues/928)
2.    Não tem suporte no mono- [1059](https://github.com/NuGet/Home/issues/1059)
3.    Não localizado- [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)
4.    Não é assinado, assim como o existente http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)
