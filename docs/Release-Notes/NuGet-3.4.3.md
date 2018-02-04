---
title: "Notas de versão do NuGet 3.4.3 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão para NuGet 3.4.3, incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs."
keywords: "Notas de versão NuGet 3.4.3, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 68aab607659d15f96aefeab7bb90afc787710824
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-343-release-notes"></a>Notas de versão do NuGet 3.4.3

[Notas de versão do NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [notas de versão do NuGet 3.4.4](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 foi lançado em 22 de abril de 2016 para abordar vários problemas que foram identificados nas versões 3.4 e subsequentes.

Você pode baixar o VSIX e nuget.exe [aqui](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Atualizações e aprimoramentos

* Maior confiabilidade do Visual Studio. Corrigimos alguns problemas no NuGet que causou a falha no Visual Studio.

## <a name="fixes"></a>Correções

* Corrigidos alguns problemas de autorização com o nuget privada protegida por senha feeds.
* Corrigido um problema se não é possível restaurar PCL de `project.json` com tempos de execução especificados.
* Alguns clientes estavam em execução em falhas intermitentes durante a instalação de pacotes. Agora, esse problema foi corrigido nesta versão.
* Corrigido um problema que causou a falhas de restauração no C + + CLI projetos com `project.json`.
* Alguns pacotes (por exemplo ModernHttpClient) onde não descompactou corretamente quando você usa o nuget em mono. Agora, esse problema foi corrigido nesta versão.

Para obter uma lista de correções e aperfeiçoamentos desta versão, confira a lista de problemas [aqui](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).