---
title: "Notas de versão 2.9 RC NuGet | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 04d76a22-63b0-41d1-9c27-799f4b35058f
description: "Notas de versão do NuGet 2.9 RC incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão RC do NuGet 2.9, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 64b4cd17394ddb902c7101b9117039f381dc8488
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-29-rc-release-notes"></a>Notas de versão 2.9 RC do NuGet

[Notas de versão do NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [notas de versão de visualização do NuGet 3.0](../release-notes/nuget-3.0-preview.md)

2.9 NuGet foi lançada em 10 de setembro de 2015 como uma atualização para o 2.8.7 VSIX para o Visual Studio 2012 e 2013.

### <a name="updates-in-this-release"></a>Atualizações nesta versão

* Agora, ignorando os pacotes de processamento se seus independente `.nuspec` documento está malformado - [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Corrigido o tratamento de multipartwebrequest de \r\n para cenários de Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)
* Corrigida a integração com eventos de compilação no Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)


A lista completa de correções desta versão pode ser encontrada no GitHub no [2.8.8 marco](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
