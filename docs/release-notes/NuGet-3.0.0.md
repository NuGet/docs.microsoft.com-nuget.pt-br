---
title: Notas de versão do NuGet 3,0
description: Notas de versão do NuGet 3.0.0 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776554"
---
# <a name="nuget-30-release-notes"></a>Notas de versão do NuGet 3,0

Notas de versão do [NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)  |  [Notas de versão do NuGet 3,1](../release-notes/nuget-3.1.md)

O NuGet 3,0 foi lançado em 20 de julho de 2015 como uma extensão de pacote para o Visual Studio 2015. Enviamos por push essa versão com o Visual Studio para que a experiência completa do NuGet 3,0 esteja disponível para novos usuários do Visual Studio. Esta versão de extensão NuGet só está disponível para o Visual Studio 2015.

Recomendamos que esses desenvolvedores tenham acesso à atualização da galeria do Visual Studio para a versão mais recente disponível, pois publicaremos uma atualização logo após o lançamento do Visual Studio 2015 que contém suporte para o desenvolvimento do Windows 10.

No total, fechamos 240 problemas na versão 3,0, e você pode examinar a [lista completa de problemas no GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Problemas conhecidos

Houve uma série de problemas conhecidos fornecidos com esta versão, e todos esses itens são corrigidos em nossa versão 3,1 agendada para coincidir com o lançamento do Windows 10 em julho de 29.  Você pode atualizar sua extensão do Visual Studio a partir da galeria ou após essa data para corrigir esses problemas conhecidos.

*  A tradução não é fornecida para o rótulo "não mostrar isso novamente" na janela de visualização e no rótulo "autores" na janela descrição do pacote.
*  Quando você trabalha em um projeto usando o controle do código-fonte do TFS, o NuGet não pode apresentar a interface do usuário do Gerenciador de pacotes se o arquivo de Nuget.Config está marcado como somente leitura.
   * **Solução alternativa** Confira o arquivo do TFS.
*  O texto na "barra de reinício" amarela na janela do PowerShell do NuGet não é visível quando você usa o tema escuro do Visual Studio.
   * **Solução alternativa** Use o tema do Visual Studio Light.


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
* [Correção do link "Saiba mais sobre as opções" para evitar falhas no Windows 10](https://github.com/NuGet/Home/issues/822)
* [Lembrar configuração da caixa de seleção de pré-lançamento](https://github.com/NuGet/Home/issues/732)
* [Melhor desempenho de coleta armazenando em cache os resultados entre projetos em uma solução](https://github.com/NuGet/Home/issues/721)
* [Vários pacotes podem ser coletados em paralelo](https://github.com/NuGet/Home/issues/713)
* [Removida a instalação do comando Package-Force](https://github.com/NuGet/Home/issues/697)

Fique atento ao [nosso blog](http://blog.nuget.org) para obter mais progresso e anúncios, pois estamos prontos para fornecer suporte para o desenvolvimento do Windows 10.