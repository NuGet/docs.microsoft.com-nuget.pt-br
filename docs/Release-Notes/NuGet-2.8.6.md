---
title: "Notas de versão do NuGet 2.8.6 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 920c551c-18a7-40f4-a32b-ce84de6ea766
description: "Notas de versão do NuGet 2.8.6 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs."
keywords: "Notas de versão NuGet 2.8.6, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4dfd0a76967280cc6a16b37fe2b2a3362231fce5
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-286-release-notes"></a>Notas de versão do NuGet 2.8.6

[Notas de versão do NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [notas de versão do NuGet 2.8.7](../release-notes/nuget-2.8.7.md)

NuGet 2.8.6 foi liberado 20 de julho de 2015 como uma pequena atualização para o nosso 2.8.5 direcionado de VSIX com algumas correções e aprimoramentos para oferecer suporte a pacotes que podem ser entregues com suporte para o modelo de desenvolvimento de UWP do Windows 10.

Esta versão da extensão de Gerenciador de pacote do NuGet fornece suporte para Visual Studio 2013.

Nesta versão, a caixa de diálogo Gerenciador de pacotes do NuGet tinha suporte adicionado para:

* Introduziu o Moniker do Framework de destino UAP para dar suporte a desenvolvimento de aplicativos do Windows 10.
* Pontos de extremidade do NuGet protocol versão 3
* Suporte para [config](../consume-packages/configuring-nuget-behavior.md) atributo protocolVersion em fontes de repositório. O valor padrão é "2"
* Voltando para o repositório remoto se uma versão de pacote necessária não está disponível no cache local