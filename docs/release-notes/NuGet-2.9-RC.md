---
title: Notas de versão do NuGet 2,9-RC
description: Notas de versão do NuGet 2,9 RC incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b9d32f09fae7e12f81cf92b5b6e6b36c71d55f26
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780313"
---
# <a name="nuget-29-rc-release-notes"></a>Notas de versão do NuGet 2,9-RC

Notas de versão do [NuGet 2.8.7](../release-notes/nuget-2.8.7.md)  |  [Notas de versão de visualização do NuGet 3,0](../release-notes/nuget-3.0-preview.md)

O NuGet 2,9 foi lançado em 10 de setembro de 2015 como uma atualização do VSIX 2.8.7 para Visual Studio 2012 e 2013.

### <a name="updates-in-this-release"></a>Atualizações nesta versão

* Agora ignorando os pacotes de processamento se o `.nuspec` documento contido estiver malformado- [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Manipulação de multipartwebrequest corrigida de \r\n para cenários UNIX/Linux- [776](https://github.com/NuGet/Home/issues/776)
* Integração corrigida com eventos de compilação no Visual Studio 2013 Community Edition- [1180](https://github.com/NuGet/Home/issues/1180)


A lista completa de correções nesta versão pode ser encontrada no GitHub no [Marco 2.8.8](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
