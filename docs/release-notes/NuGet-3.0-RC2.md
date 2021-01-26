---
title: Notas de versão do NuGet 3,0 RC2
description: Notas de versão do NuGet 3,0 RC2, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780273"
---
# <a name="nuget-30-rc2-release-notes"></a>Notas de versão do NuGet 3,0 RC2

Notas de versão do [NuGet 3,0 RC](../release-notes/nuget-3.0-RC.md)  |  [Notas de versão do NuGet 3,0](../release-notes/nuget-3.0.0.md)

O NuGet 3,0 RC2 foi lançado em 3 de junho de 2015 como uma versão provisória disponível na Galeria de extensões do Visual Studio 2015 e no [codeplex](https://nuget.codeplex.com/releases/view/615507). Esta versão tem uma série de correções de bugs importantes e melhorias de desempenho que achamos importantes para serem lançadas antes da versão concluída do Visual Studio 2015. Esta versão de extensão NuGet só está disponível para o Visual Studio 2015.

No total, fechamos 158 problemas nesta versão, e você pode examinar a [lista completa de problemas no GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

## <a name="summary-of-top-issues-resolved"></a>Resumo dos principais problemas resolvidos

* [Chamadas frequentes de atualização de rede quando a janela do Gerenciador de pacotes é atualizada](https://github.com/NuGet/Home/issues/515)
* [Rolagem atrasada ao mudar para a exibição instalada no Gerenciador de pacotes](https://github.com/NuGet/Home/issues/519)
* [Chamadas de rede devem ser executadas em um thread em segundo plano](https://github.com/NuGet/Home/issues/516)
* [Caixa de seleção ' não mostrar janela de visualização ' adicionada](https://github.com/NuGet/Home/issues/566)
* [Limitação de processo adicionada para reduzir o uso do processador](https://github.com/NuGet/Home/issues/356)
* Manipulação de referência de biblioteca de classe portátil aprimorada
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [O serviço de conclusão total diferencia maiúsculas de minúsculas](https://github.com/NuGet/Home/issues/198)
* [Atualizar para reintroduzir as credenciais básicas de autenticação](https://github.com/NuGet/Home/issues/456)
* [Aprimorado o relatório de erros](https://github.com/NuGet/Home/issues/407)
* [Mensagens de erro do PowerShell aprimoradas ao chamar Update-Package](https://github.com/NuGet/Home/issues/5)

Baixe essa [atualização para a extensão do NuGet](https://nuget.codeplex.com/releases/view/615507) do CodePlex e fique atento ao [nosso blog](http://blog.nuget.org) para obter mais progresso e anúncios para o NuGet 3,0!