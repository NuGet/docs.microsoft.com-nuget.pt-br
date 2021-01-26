---
title: Notas de versão do NuGet 2.8.6
description: Notas de versão do NuGet 2.8.6 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776707"
---
# <a name="nuget-286-release-notes"></a>Notas de versão do NuGet 2.8.6

Notas de versão do [NuGet 2.8.5](../release-notes/nuget-2.8.5.md)  |  [Notas de versão do NuGet 2.8.7](../release-notes/nuget-2.8.7.md)

O NuGet 2.8.6 foi lançado em 20 de julho de 2015 como uma pequena atualização para nosso VSIX 2.8.5 com algumas correções e aprimoramentos direcionados para oferecer suporte a pacotes que podem ser fornecidos com suporte para o modelo de desenvolvimento UWP do Windows 10.

Esta versão da extensão do Gerenciador de pacotes NuGet fornece suporte somente para Visual Studio 2013.

Nesta versão, a caixa de diálogo Gerenciador de pacotes NuGet tinha suporte adicionado para:

* Introduziu o moniker da estrutura de destino UAP para dar suporte ao desenvolvimento de aplicativos do Windows 10.
* Pontos de extremidade da versão 3 do protocolo NuGet
* Suporte para [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) atributo protocolVersion em fontes de repositório. O valor padrão é "2"
* Voltando ao repositório remoto se uma versão de pacote necessária não estiver disponível no cache local