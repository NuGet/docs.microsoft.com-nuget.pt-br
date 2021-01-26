---
title: Notas de versão do NuGet 3.4.3
description: Notas de versão do NuGet 3.4.3 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776465"
---
# <a name="nuget-343-release-notes"></a>Notas de versão do NuGet 3.4.3

Notas de versão do [NuGet 3.4.2](../release-notes/nuget-3.4.2.md)  |  [Notas de versão do NuGet 3.4.4](../release-notes/nuget-3.4.4.md)

O NuGet 3.4.3 foi lançado em 22 de abril de 2016 para resolver vários problemas identificados nas versões 3,4 e subsequentes.

Você pode baixar o VSIX e o nuget.exe [aqui](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Atualizações e aprimoramentos

* Confiabilidade aprimorada do Visual Studio. Corrigimos alguns problemas no NuGet que causaram falhas no Visual Studio.

## <a name="fixes"></a>Correções

* Correção de alguns problemas de autorização com feeds do NuGet privados protegidos por senha.
* Correção de um problema ao não conseguir restaurar PCL do `project.json` com tempos de execução especificados.
* Alguns clientes estavam executando falhas intermitentes ao instalar pacotes. Agora, isso foi corrigido nesta versão.
* Correção de um problema que causou falhas de restauração em projetos C++/CLI com `project.json` .
* Alguns pacotes (por exemplo, ModernHttpClient) onde não são descompactados corretamente quando você usa o NuGet no mono. Agora, isso foi corrigido nesta versão.

Para obter uma lista completa de correções e aprimoramentos nesta versão, confira a lista de problemas [aqui](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).