---
title: Notas de versão do NuGet 2.8.5
description: Notas de versão do NuGet 2.8.5 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780354"
---
# <a name="nuget-285-release-notes"></a>Notas de versão do NuGet 2.8.5

Notas de versão do [NuGet 2.8.3](../release-notes/nuget-2.8.3.md)  |  [Notas de versão do NuGet 2.8.6](../release-notes/nuget-2.8.6.md)

O NuGet 2.8.5 foi lançado em 30 de março de 2015. É uma pequena atualização para nosso VSIX 2.8.3 com algumas correções direcionadas.

Nesta versão, a caixa de diálogo suporte para Gerenciador de pacotes NuGet foi adicionada para [monikers da estrutura de destino do DNX](https://github.com/aspnet/dnx).  Esses novos monikers de estrutura com suporte incluem:

* **core50** -um "base" moniker da estrutura de destino (TFM) que é compatível com o CLR principal.
* **dnx452** -um TFM específico para aplicativos baseados em DNX usando a versão 4.5.2 completa da estrutura
* **dnx46** -um TFM específico para aplicativos baseados em DNX usando a versão 4,6 completa da estrutura
* **dnxcore50** -um TFM específico para aplicativos baseados em DNX usando a versão Core 5,0 da estrutura

Foi corrigido um bug que impedia a instalação correta de pacotes em projetos FSharp:

https://nuget.codeplex.com/workitem/4400