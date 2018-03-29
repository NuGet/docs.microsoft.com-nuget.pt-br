---
title: Notas de versão do NuGet 3.0 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Notas de versão do NuGet 3.0.0 incluindo problemas conhecidos, correções de bug, recursos adicionados e DCRs.
keywords: Notas de versão NuGet 3.0.0, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: fc669e4a8440c295f08eef461186eef5f505df42
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-30-release-notes"></a>Notas de versão 3.0 do NuGet

[Notas de versão do NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [notas de versão 3.1 do NuGet](../release-notes/nuget-3.1.md)

NuGet 3.0 foi lançado em 20 de julho de 2015 como uma extensão do pacote para o Visual Studio 2015. É enviado para oferecer esta versão com o Visual Studio para que a experiência completa de NuGet 3.0 atualizada está disponível para novos usuários do Visual Studio. Esta versão da extensão NuGet só está disponível para o Visual Studio 2015.

Recomendamos que os desenvolvedores que têm acesso a atualização da Galeria do Visual Studio para a versão mais recente está disponível, como estamos publicando uma atualização logo após o lançamento do Visual Studio 2015 que contém suporte para o desenvolvimento do Windows 10.

No total, é fechada 240 problemas na versão 3.0, e você pode examinar o [lista completa dos problemas no GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Problemas Conhecidos

Houve um número de problemas conhecidos, fornecido com esta versão e todos esses itens corrigidos na nossa versão 3.1 agendado para coincidir com a versão do Windows 10 em 29 de julho.  É possível atualizar a extensão do Visual Studio da Galeria em ou após essa data para corrigir esses problemas conhecidos.

*  Conversão não for fornecida para o rótulo "Não mostrar esta mensagem novamente" na janela de visualização e o rótulo "Autores" na janela de descrição do pacote.
*  Quando você trabalhar em um projeto usando o TFS controle de origem, o NuGet não é possível apresentar o Gerenciador de pacotes interface do usuário se o arquivo NuGet. config está marcado como somente leitura.
   * **Solução alternativa** Check-out do arquivo do TFS.
*  Texto em amarelos "reinicialização barra" na janela do Powershell do NuGet não é visível quando você usa o tema escuro do Visual Studio.
   * **Solução alternativa** usar o tema claro do Visual Studio.


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
* [Corrigido o link 'Saiba mais sobre as opções' para evitar falhas no Windows 10](https://github.com/NuGet/Home/issues/822)
* [Lembre-se a configuração da caixa de seleção de pré-lançamento](https://github.com/NuGet/Home/issues/732)
* [Obter melhor desempenho armazenando em cache os resultados em projetos em uma solução](https://github.com/NuGet/Home/issues/721)
* [Vários pacotes podem ser obtidos em paralelo](https://github.com/NuGet/Home/issues/713)
* [Removeu o pacote de instalação-força o comando](https://github.com/NuGet/Home/issues/697)

Fique atento [nosso blog](http://blog.nuget.org) para mais de progresso e anúncios como preparamos oferecer suporte para o desenvolvimento do Windows 10.