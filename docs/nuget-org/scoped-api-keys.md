---
title: Chaves de API no escopo
description: Assuma o controle das chaves de API que você usa para efetuar push de pacotes
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: 12d12d5294a474c4d3e4f5d3cad468bb515d21d5
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426941"
---
# <a name="scoped-api-keys"></a>Chaves de API no escopo

Para tornar o NuGet um ambiente mais seguro para a distribuição de pacote, você pode assumir o controle das chaves de API adicionando escopos.

A capacidade de fornecer o escopo para as chaves de API dará a você um melhor controle sobre suas APIs. Você pode:

- Criar várias chaves de API no escopo que podem ser usadas para diferentes pacotes com períodos de expiração variados.
- Obter chaves de API com segurança.
- Editar as chaves de API existentes para alterar a aplicabilidade do pacote.
- Atualizar ou excluir as chaves de API existentes sem dificultar as operações que usam outras chaves.

## <a name="why-do-we-support-scoped-api-keys"></a>Por que damos suporte a chaves de API no escopo?

Damos suporte a escopos para chaves de API a fim de permitir que você tenha permissões mais refinadas. Anteriormente, o NuGet oferecia uma única chave de API para uma conta, e essa abordagem apresentava várias desvantagens:

- **Uma chave de API para controlar todos os pacotes**. Com uma única chave de API que é usada para gerenciar todos os pacotes, fica difícil compartilhar a chave com segurança quando vários desenvolvedores estão envolvidos com diferentes pacotes e quando eles compartilham uma conta de editor.
- **Todas as permissões ou nenhuma**. Qualquer pessoa com acesso à chave de API tem todas as permissões (publicar, efetuar push e remover da lista) nos pacotes. Em geral, isso não é desejável em ambiente com várias equipes.
- **Ponto único de falha**. Uma única chave de API também significa um ponto único de falha. Se a chave for comprometida, todos os pacotes associados à conta poderão ficar comprometidos. A atualização da chave de API é a única maneira de "conter o vazamento" e evitar uma interrupção no fluxo de trabalho da CI/CD. Além disso, pode haver casos em que você deseje revogar o acesso à chave de API para um indivíduo (por exemplo, quando um funcionário sai da organização). Atualmente, não existe uma forma perfeita para lidar com isso.

Com as chaves de API no escopo, tentamos resolver esses problemas e, ao mesmo tempo, garantir que nenhum dos fluxos de trabalho existentes sejam interrompidos.

## <a name="acquire-an-api-key"></a>Adquirir uma chave de API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a>Criar chaves de API no escopo

Você pode criar várias chaves de API com base em seus requisitos. Uma chave de API pode se aplicar a um ou mais pacotes, ter escopos variados que concedem privilégios específicos e ter uma data de expiração associada a ela.

No exemplo a seguir, você tem uma chave de API chamada `Contoso service CI` que pode ser usada para efetuar push de pacotes para pacotes `Contoso.Service` específicos e é válida por 365 dias. Esse é um cenário típico, em que diferentes equipes da mesma organização trabalham em pacotes diferentes e os membros da equipe recebem a chave que concede privilégios apenas ao pacote no qual estão trabalhando. A expiração serve como um mecanismo para prevenir chaves obsoletas ou esquecidas.

![Criar chaves de API](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a>Usar padrões glob

Se estiver trabalhando em vários pacotes e tiver uma lista grande de pacotes para gerenciar, opte por usar padrões de recurso de curinga para selecionar vários pacotes juntos. Por exemplo, caso deseje conceder escopos específicos a uma chave para todos os pacotes cuja ID comece com `Fabrikam.Service`, faça isso especificando `fabrikam.service.*` na caixa de texto **Padrão glob**.

![Criar chaves de API](media/scoped-api-keys-glob-pattern.png)

O uso de padrões glob para determinar as permissões da chave de API também se aplica a novos pacotes que correspondem ao padrão glob. Por exemplo, se você tentar efetuar push de um novo pacote chamado `Fabrikam.Service.Framework`, poderá fazer isso com a chave criada anteriormente, pois o pacote corresponde ao padrão glob `fabrikam.service.*`.

## <a name="obtain-api-keys-securely"></a>Obter chaves de API com segurança

Por segurança, uma chave recém-criada nunca é mostrada na tela e só fica disponível por meio do botão **Copiar**. Da mesma forma, a chave não é acessível depois que a página é atualizada.

![Criar chaves de API](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a>Editar as chaves de API existentes

Além disso, o ideal é atualizar as permissões de chave e os escopos sem alterar a própria chave. Caso você tenha uma chave com escopos específicos para um único pacote, poderá optar por aplicar os mesmos escopos a um ou muitos outros pacotes.

![Criar chaves de API](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a>Atualizar ou excluir as chaves de API existentes

O proprietário da conta pode optar por atualizar a chave, caso em que a permissão (nos pacotes), o escopo e a expiração permanecem os mesmos, mas uma nova chave é emitida, tornando a chave antiga inutilizável. Isso é útil no gerenciamento de chaves obsoletas ou quando há potencial de um vazamento da chave de API.

![Criar chaves de API](media/scoped-api-keys-refresh.png)

Você também poderá optar por excluir essas chaves se elas não forem mais necessárias. A exclusão de uma chave remove a chave e a torna inutilizável.

## <a name="faqs"></a>Perguntas frequentes

### <a name="what-happens-to-my-old-legacy-api-key"></a>O que acontecerá com minha chave de API antiga (herdada)?

Sua chave de API antiga (herdada) continuará funcionando e poderá funcionar pelo tempo que você desejar. No entanto, essas chaves serão desativadas se não forem usadas por mais de 365 dias para efetuar push de um pacote. Para obter mais detalhes, confira a postagem no blog [Alterações nas chaves de API com data de expiração](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html). Não será mais possível atualizar essa chave. Você precisará excluir a chave herdada e criar outra chave no escopo.

> [!NOTE]
> Essa chave tem todas as permissões em todos os pacotes e nunca expira. Considere excluir essa chave e criar outras chaves com permissões no escopo e expiração definida.

### <a name="how-many-api-keys-can-i-create"></a>Quantas chaves de API podem ser criadas?

Não há nenhum limite no número de chaves de API que podem ser criadas. No entanto, recomendamos limitar esse número a uma contagem gerenciável, para não acabar tendo muitas chaves obsoletas sem nenhum conhecimento de quem está usando as chaves e do local em que estão sendo usadas.

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a>Posso excluir minha chave de API herdada ou descontinuar seu uso agora?

Sim. Você pode – e provavelmente deve – excluir sua chave de API herdada.

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a>Posso recuperar minha chave de API excluída por engano?

Nº Depois que a chave for excluída, você só poderá criar outras chaves. Não há nenhuma recuperação possível para chaves excluídas acidentalmente.

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a>A chave de API antiga continua funcionando após a atualização da chave de API?

Nº Depois que você atualiza uma chave, é gerada uma nova chave que tem o mesmo escopo, a mesma permissão e a mesma expiração da antiga. A chave antiga deixa de existir.

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a>Posso conceder mais permissões a uma chave de API existente?

Não é possível modificar o escopo, mas é possível editar a lista de pacotes a qual ele é aplicável.

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a>Como saber se uma de minhas chaves expirou ou se está prestes a expirar?

Se qualquer chave expirar, nós o informaremos por meio de uma mensagem de aviso na parte superior da página. Também enviamos um email de aviso ao titular da conta dez dias antes da expiração da chave, de modo que você possa tomar providências antecipadamente.