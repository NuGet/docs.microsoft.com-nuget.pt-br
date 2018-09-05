---
title: Notas de versão do NuGet 3.0 RC2
description: Notas de versão do NuGet 3.0 RC2 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 863e48e632387b768a43530b987683605baf6db7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545815"
---
# <a name="nuget-30-rc2-release-notes"></a>Notas de versão do NuGet 3.0 RC2

[Notas de versão do NuGet 3.0 RC](../release-notes/nuget-3.0-RC.md) | [notas de versão do NuGet 3.0](../release-notes/nuget-3.0.0.md)

RC2 do NuGet 3.0 foi lançado em 3 de junho de 2015 como um lançamento disponível do que a Galeria de extensões do Visual Studio 2015 e [Codeplex](https://nuget.codeplex.com/releases/view/615507). Esta versão tem várias correções de bugs importantes e melhorias de desempenho que acreditamos que eram importantes liberar antes do lançamento do Visual Studio 2015 concluído. Esta versão da extensão NuGet só está disponível para o Visual Studio 2015.

No total, e, fechamos 158 problemas nesta versão, você pode examinar os [uma lista completa dos problemas no GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

## <a name="summary-of-top-issues-resolved"></a>Resumo dos principais problemas resolvidos

* [Atualização frequente de rede chama quando a janela do Gerenciador de pacotes é atualizada](https://github.com/NuGet/Home/issues/515)
* [Atraso de rolagem quando a alteração para instalado o modo de exibição no Gerenciador de pacotes](https://github.com/NuGet/Home/issues/519)
* [Chamadas de rede devem ser executadas em um thread em segundo plano](https://github.com/NuGet/Home/issues/516)
* [Adicionada a caixa de seleção 'Não Mostrar janela de visualização'](https://github.com/NuGet/Home/issues/566)
* [Processo adicionado limitação para reduzir o uso do processador](https://github.com/NuGet/Home/issues/356)
* Referência da biblioteca de classes portátil manipulação melhorada
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Serviço de preenchimento automático foi diferencia maiusculas de minúsculas](https://github.com/NuGet/Home/issues/198)
* [Atualização reintroduzir credenciais de autenticação básica](https://github.com/NuGet/Home/issues/456)
* [Log de erros aprimorado](https://github.com/NuGet/Home/issues/407)
* [Mensagens de erro do powershell aprimorado ao chamar o pacote de atualização](https://github.com/NuGet/Home/issues/5)

Baixe este [atualizar para a extensão do NuGet](https://nuget.codeplex.com/releases/view/615507) do Codeplex e, por favor, fique atento [nosso blog](http://blog.nuget.org) para obter mais progresso e anúncios para NuGet 3.0!