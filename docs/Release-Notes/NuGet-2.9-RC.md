---
title: "Notas de versão 2.9 RC NuGet | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão do NuGet 2.9 RC incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão RC do NuGet 2.9, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0e73b54ab7bbf97806269834c67ad0a159c9065b
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-29-rc-release-notes"></a>Notas de versão 2.9 RC do NuGet

[Notas de versão do NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [notas de versão de visualização do NuGet 3.0](../release-notes/nuget-3.0-preview.md)

2.9 NuGet foi lançada em 10 de setembro de 2015 como uma atualização para o 2.8.7 VSIX para o Visual Studio 2012 e 2013.

### <a name="updates-in-this-release"></a>Atualizações nesta versão

* Agora, ignorando os pacotes de processamento se seus independente `.nuspec` documento está malformado - [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Corrigido o tratamento de multipartwebrequest de \r\n para cenários de Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)
* Corrigida a integração com eventos de compilação no Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)


A lista completa de correções desta versão pode ser encontrada no GitHub no [2.8.8 marco](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
