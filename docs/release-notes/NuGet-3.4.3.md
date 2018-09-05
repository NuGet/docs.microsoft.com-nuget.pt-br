---
title: Notas de versão do NuGet 3.4.3
description: Notas de versão do NuGet 3.4.3 incluindo conhecidos problemas, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549159"
---
# <a name="nuget-343-release-notes"></a>Notas de versão do NuGet 3.4.3

[Notas de versão do NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [notas de versão do NuGet 3.4.4](../release-notes/nuget-3.4.4.md)

O NuGet 3.4.3 foi lançado em 22 de abril de 2016 para abordar vários problemas que foram identificados nas versões 3.4 e posteriores.

Você pode baixar o VSIX e nuget.exe [aqui](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Atualizações e aprimoramentos

* Confiabilidade aprimorada do Visual Studio. Corrigimos alguns problemas no NuGet que causou a falha no Visual Studio.

## <a name="fixes"></a>Correções

* Correção de alguns problemas de autorização com o nuget privado protegido por senha feeds.
* Corrigido um problema em torno de não ser capaz de restaurar o PCL do `project.json` com tempos de execução especificados.
* Alguns clientes estavam sendo executados em falhas intermitentes durante a instalação de pacotes. Agora, esse problema foi corrigido nesta versão.
* Corrigido um problema que causava falhas de restauração no C + + c++ CLI projetos com `project.json`.
* Alguns pacotes (por exemplo ModernHttpClient) onde não sendo descompactou corretamente quando você usa o nuget em mono. Agora, esse problema foi corrigido nesta versão.

Para obter uma lista de correções e aprimoramentos nesta versão, confira a lista de problemas [aqui](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).