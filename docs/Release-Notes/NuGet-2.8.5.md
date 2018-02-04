---
title: "Notas de versão do NuGet 2.8.5 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão do NuGet 2.8.5 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs."
keywords: "Notas de versão NuGet 2.8.5, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ace56284e56f24394d49c0598ec3604b62caaf67
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
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