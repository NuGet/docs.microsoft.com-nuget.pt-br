---
title: Notas de versão do NuGet 2.8.6
description: Notas de versão do NuGet 2.8.6 incluindo conhecidos problemas, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546485"
---
# <a name="nuget-286-release-notes"></a>Notas de versão do NuGet 2.8.6

[Notas de versão do NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [notas de versão do NuGet 2.8.7](../release-notes/nuget-2.8.7.md)

O NuGet 2.8.6 foi lançado 20 de julho de 2015 como uma pequena atualização para o nosso 2.8.5 direcionado de VSIX com algumas correções e aprimoramentos para oferecer suporte a pacotes que podem ser entregues com suporte para o modelo de desenvolvimento de UWP do Windows 10.

Esta versão do que a extensão de Gerenciador de pacotes do NuGet fornece suporte para Visual Studio 2013.

Nesta versão, a caixa de diálogo Gerenciador de pacotes NuGet tinha suporte adicionado para:

* Introduziu o Moniker do Framework de destino UAP para dar suporte ao desenvolvimento de aplicativo do Windows 10.
* Pontos de extremidade do NuGet protocol versão 3
* Suporte para [NuGet. config](../consume-packages/configuring-nuget-behavior.md) atributo protocolVersion em fontes de repositório. Valor padrão é "2"
* Voltando para o repositório remoto se uma versão do pacote necessário não está disponível no cache local