---
title: Notas de versão do NuGet 2.8.5
description: Notas de versão do NuGet 2.8.5 incluindo conhecidos problemas, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548619"
---
# <a name="nuget-285-release-notes"></a>Notas de versão do NuGet 2.8.5

[Notas de versão do NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [notas de versão do NuGet 2.8.6](../release-notes/nuget-2.8.6.md)

O NuGet 2.8.5 foi lançado em 30 de março de 2015. Ele é uma pequena atualização para nossos 2.8.3 VSIX com alguns destino correções.

Nesta versão, a caixa de diálogo Gerenciador de pacotes do NuGet foi adicionado suporte às [Monikers da estrutura de destino DNX](https://github.com/aspnet/dnx).  Esses novos monikers de estrutura com suporte incluem:

* **core50** – um moniker de estrutura (TFM) é compatível com o Core CLR de destino 'base'.
* **dnx452** – aplicativos específicos com base em DNX um TFM, usando o 4.5.2 completo versão do framework
* **dnx46** – aplicativos específicos com base em DNX um TFM, usando a versão 4.6 completa do framework
* **dnxcore50** – aplicativos específicos com base em DNX um TFM, usando a versão 5.0 do núcleo do framework

Um bug foi corrigido que impedia pacotes seja instalado em projetos FSharp corretamente:

https://nuget.codeplex.com/workitem/4400