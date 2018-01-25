---
title: "Notas de versão do NuGet 3.0 RC2 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Notas de versão do NuGet 3.0 RC2 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão NuGet 3.0 RC2, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67299408170ae3c3676c2866bec2945b41ad4184
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-30-rc2-release-notes"></a>Notas de versão do NuGet 3.0 RC2

[Notas de versão do NuGet 3.0 RC](../release-notes/nuget-3.0-RC.md) | [notas de versão do NuGet 3.0](../release-notes/nuget-3.0.0.md)

Lançada em 3 de junho de 2015 RC2 do NuGet 3.0 como versão disponível da Galeria de extensões do Visual Studio 2015 e [Codeplex](https://nuget.codeplex.com/releases/view/615507). Esta versão tem um número de correções de bugs importantes e melhorias de desempenho que constatamos foram importantes liberar antes do lançamento do Visual Studio 2015 concluído. Esta versão da extensão NuGet só está disponível para o Visual Studio 2015.

No total, é fechada 158 problemas nesta versão, e você pode examinar o [lista completa dos problemas no GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

## <a name="summary-of-top-issues-resolved"></a>Resumo dos principais problemas resolvidos

* [Atualização da rede frequentes chama quando a janela do Gerenciador de pacote é atualizada](https://github.com/NuGet/Home/issues/515)
* [Atrasado rolagem quando alterar para instalado exibição no Gerenciador de pacotes](https://github.com/NuGet/Home/issues/519)
* [Chamadas de rede devem ser executadas em um thread em segundo plano](https://github.com/NuGet/Home/issues/516)
* [Adicionar caixa de seleção 'Não mostrar a janela de visualização'](https://github.com/NuGet/Home/issues/566)
* [Limitação para reduzir a utilização do processador do processo de inclusão](https://github.com/NuGet/Home/issues/356)
* Melhor tratamento de referência de biblioteca de classes portátil
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Serviço de preenchimento automático foi diferencia maiusculas de minúsculas](https://github.com/NuGet/Home/issues/198)
* [Atualização reintroduzir credenciais de autenticação básica](https://github.com/NuGet/Home/issues/456)
* [Log de erros aprimorado](https://github.com/NuGet/Home/issues/407)
* [Mensagens de erro do powershell aprimorado ao chamar o pacote de atualização](https://github.com/NuGet/Home/issues/5)

Baixe este [atualizar para a extensão do NuGet](https://nuget.codeplex.com/releases/view/615507) do Codeplex e fique atento [nosso blog](http://blog.nuget.org) para mais de progresso e avisos do NuGet 3.0!