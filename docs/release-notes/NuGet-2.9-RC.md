---
title: Notas de versão 2.9 RC do NuGet
description: Notas de versão do NuGet 2.9 RC incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 17c1c3a0c91928602aa47b5ba599faeac0424a4a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548318"
---
# <a name="nuget-29-rc-release-notes"></a>Notas de versão 2.9 RC do NuGet

[Notas de versão do NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [notas de versão do NuGet 3.0 versão prévia](../release-notes/nuget-3.0-preview.md)

NuGet 2.9 foi lançada em 10 de setembro de 2015 como uma atualização para o 2.8.7 VSIX para Visual Studio 2012 e 2013.

### <a name="updates-in-this-release"></a>Atualizações nesta versão

* Agora, ignorando o processamento de pacotes se seus independente `.nuspec` documento está malformado - [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Corrigido o tratamento de multipartwebrequest de \r\n para cenários de Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)
* Corrigida a integração com eventos de build no Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)


A lista completa de correções nesta versão pode ser encontrada no GitHub no [2.8.8 marco](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
