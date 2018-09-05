---
title: Notas de versão 3.0 do NuGet
description: Notas de versão do NuGet 3.0.0 incluindo conhecidos problemas, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551857"
---
# <a name="nuget-30-release-notes"></a>Notas de versão 3.0 do NuGet

[Notas de versão do NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [notas de versão do NuGet 3.1](../release-notes/nuget-3.1.md)

NuGet 3.0 foi lançado em 20 de julho de 2015 como uma extensão do pacote para o Visual Studio 2015. Incentivamos para fornecer essa versão com o Visual Studio para que a experiência completa de NuGet 3.0 atualizada estaria disponível para novos usuários do Visual Studio. Esta versão da extensão NuGet só está disponível para o Visual Studio 2015.

Recomendamos que os desenvolvedores que têm acesso a atualização da Galeria do Visual Studio para a versão mais recente que está disponível, como estamos publicando uma atualização logo após o lançamento do Visual Studio 2015 que contém suporte para o desenvolvimento do Windows 10.

No total, e, fechamos 240 problemas na versão 3.0, você pode examinar os [uma lista completa dos problemas no GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Problemas Conhecidos

Houve um número de problemas conhecidos entregues com esta versão, e todos esses itens são fixos em nossa versão 3.1 programada para coincidir com o lançamento do Windows 10 em 29 de julho.  É possível atualizar sua extensão do Visual Studio da Galeria em ou após essa data, para corrigir esses problemas conhecidos.

*  Conversão não for fornecida para o rótulo "Não mostrar isto novamente" na janela de visualização e o rótulo "Autores" na janela de descrição do pacote.
*  Quando você trabalhar em um projeto usando o TFS controle de origem, o NuGet não é possível apresentar o Gerenciador de pacotes interface do usuário se o arquivo NuGet. config está marcado como somente leitura.
   * **Solução alternativa** Check-out do arquivo do TFS.
*  Texto no amarelo "reinicialização bar" na janela do Powershell do NuGet não é visível quando você usa o tema escuro do Visual Studio.
   * **Solução alternativa** usar o tema claro do Visual Studio.


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
* [Corrigido o link 'Saiba mais sobre as opções' para evitar o travamento no Windows 10](https://github.com/NuGet/Home/issues/822)
* [Lembre-se a configuração da caixa de seleção de pré-lançamento](https://github.com/NuGet/Home/issues/732)
* [Desempenho aprimorado de coleta armazenando em cache os resultados em projetos em uma solução](https://github.com/NuGet/Home/issues/721)
* [Vários pacotes podem ser obtidos em paralelo](https://github.com/NuGet/Home/issues/713)
* [Removeu o pacote de instalação-forçar o comando](https://github.com/NuGet/Home/issues/697)

Por favor, fique atento [nosso blog](http://blog.nuget.org) para obter mais progresso e comunicados quando estivermos prontos para oferecer suporte para o desenvolvimento do Windows 10.