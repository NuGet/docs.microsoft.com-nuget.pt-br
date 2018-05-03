---
title: Notas de versão do NuGet 2.8.5
description: Notas de versão do NuGet 2.8.5 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-285-release-notes"></a>Notas de versão do NuGet 2.8.5

[Notas de versão do NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [notas de versão do NuGet 2.8.6](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 foi lançado em 30 de março de 2015. É uma pequena atualização para nosso 2.8.3 VSIX com alguns direcionados correções.

Nesta versão, a caixa de diálogo Gerenciador de pacotes do NuGet foi adicionado suporte às [Monikers de Framework de destino do DNX](https://github.com/aspnet/dnx).  Esses novos identificadores de framework com suporte incluem:

* **core50** - um moniker do framework (TFM) que é compatível com o CLR principal 'base' de destino.
* **dnx452** - TFM A aplicativos específicos com base em DNX usando o 4.5.2 completo versão do framework
* **dnx46** - TFM A aplicativos específicos com base em DNX usando a versão 4.6 completo do framework
* **dnxcore50** - TFM A aplicativos específicos com base em DNX usando a versão 5.0 do núcleo do framework

Um bug foi corrigido que pacotes impedido de instalar nos projetos FSharp corretamente:

https://nuget.codeplex.com/workitem/4400