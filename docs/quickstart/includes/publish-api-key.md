---
ms.openlocfilehash: 20851cd71cc5eb6735fe5e0cd8b0f314f9100be4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "68419905"
---
1. [Entre em sua conta do nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) ou crie uma conta, se você não tiver uma.

   Para saber mais sobre como criar sua conta, confira [Contas individuais](../../nuget-org/individual-accounts.md).

1. Selecione seu nome de usuário (no canto superior direito) e selecione **Chaves de API**.

1. Selecione **Criar**, forneça um nome para sua chave, selecione **Selecionar Escopos > Push**. Digite * para **Padrão Glob** e selecione **Criar**. (Veja mais sobre escopos abaixo).

1. Após a criação da chave, selecione **Copiar** para recuperar a chave de acesso que você precisa na CLI:

    ![Copiando a chave de API para a área de transferência](../media/QS_Create-02-APIKey.png)

1. **Importante**: salve sua chave em um local seguro, pois não será possível copiar a chave novamente no futuro. Se você retornar à página da chave de API, será necessário gerar novamente a chave para copiá-la. Também é possível remover a chave de API, se você não quiser mais efetuar push de pacotes por meio da CLI.

Os escopos permitem criar chaves de API separadas para finalidades diferentes. Cada chave tem seu período de expiração e pode ter o escopo definido para pacotes específicos (ou padrões glob). Cada chave também pode ter o escopo definido para operações específicas: push de novos pacotes e atualizações, push somente de atualizações ou remoção de lista. Por meio de escopo, é possível criar chaves de API para diferentes pessoas que gerenciam os pacotes para a sua organização, de modo que elas tenham somente as permissões necessárias. Para saber mais, confira [Chaves de API com escopo](../../nuget-org/scoped-api-keys.md).