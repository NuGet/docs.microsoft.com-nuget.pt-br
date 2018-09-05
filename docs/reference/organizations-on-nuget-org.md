---
title: Organizações em nuget.org
description: As organizações em nuget.org ajuda você a gerenciar os pacotes publicados por grupo ou em uma equipe, o ambiente da empresa.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: ea1ca607f169cd31c0a1b59d575d1a743763420c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551222"
---
# <a name="organization-on-nugetorg"></a>Organização em nuget.org

As organizações permitem que as empresas e projetos de código-fonte aberto para colaborar em pacotes usando uma identidade única nuget.org. Para um consumidor do pacote, uma conta de organização é exibida mesma que uma conta de usuário em nuget.org.

## <a name="user-accounts-vs-organization-accounts"></a>Contas de usuário versus contas da organização

Sua conta de usuário é a sua identidade em nuget.org e pode ser um membro de qualquer número de organizações. Um pacote pode pertencer a uma conta de organização como ele pode pertencer a uma conta de usuário. Os consumidores de pacote não verá nenhuma diferença entre uma conta de usuário ou a conta de organização: ambos aparecer como pacote `owners`.

Uma conta de organização tem uma ou mais contas de usuário como seus membros. Esses membros podem gerenciar um conjunto de pacotes, mantendo uma única identidade para a propriedade.

## <a name="adding-a-new-organization"></a>Adicionando uma nova organização

Para adicionar uma nova organização, selecione sua conta em nuget.org e, em seguida, selecione o **organizações gerenciar...**  comando de menu:

![Opção de menu em nuget.org para organizações de Gerenciador](media/org-manage-option.png)

Na próxima página, selecione a **adicionar nova organização** botão:

![Botão para criar uma nova organização em nuget.org](media/org-add-new-option.png)

Na próxima página, forneça o endereço de nome e email da organização. Como contas da organização compartilham o mesmo namespace que as contas de usuário, o nome da organização deve ser diferente de qualquer organização existente ou contas de usuário. O endereço de email também deve ser exclusivo em todas as contas.

![Adicionar nova página de organização no nuget.org](media/org-add-new-page.png)

Depois de criar a conta de organização, você é o administrador e pode enviar pacotes para a organização e adicione os membros da organização.

### <a name="transform-existing-account-to-an-organization"></a>Transformar a conta existente para uma organização

> [!Warning]
> Conversão de conta é irreversível: não é possível transformar uma organização para uma conta de usuário.

Se você estiver gerenciando pacotes como uma equipe usando uma conta de usuário único e gostaria de converter essa conta em uma organização, use o **transformar sua conta para uma organização** opção o **organizações gerenciar** página:

![Opção em nuget.org para transformar uma conta existente para uma organização](media/org-transform-option.png)

Na próxima página, especifique a conta de usuário diferente para atribuir como o administrador da organização e, em seguida, selecione **transformar**.

![Inserir informações para transformar uma conta de usuário para uma organização](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Gerenciar os membros da organização

Como o administrador da organização, você pode adicionar membros, fornecendo a nuget.org do cada membro *nome da conta de usuário*; endereços de email não podem ser usados. Você, em seguida, marque cada membro como um colaborador ou administrador com as seguintes permissões:

| Permissão | Colaborador | Administrador |
| --- | --- | --- |
| Gerenciar pacotes da organização<br/>(Enviar novos pacotes, atualizar ou remover da lista de pacotes existentes) | Sim | Sim |
| Metadados de organização de alteração<br/>(endereço de email, as configurações de notificação) | Não | Sim |
| Gerenciar os membros da organização | Não | Sim |
| Solicitar ou agir em solicitações de co-ownership para pacotes de organização | Não | Sim |

## <a name="managing-packages"></a>Gerenciamento de pacotes

Você pode exibir todos os pacotes em sua conta e todas as organizações das quais você é um membro na [gerenciar pacotes](https://www.nuget.org/account/Packages) página. Para exibir os pacotes específicos para sua conta ou qualquer organização específica, use o filtro de contas no canto superior direito da página.

![Gerenciando pacotes com o filtro de conta](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Transferência de pacotes para uma organização
Se você deseja transferir alguns dos seus pacotes para uma organização recém-criado, você pode fazer isso solicitando a conta de organização para o pacote de um coproprietário e, em seguida, removendo-se como o proprietário. Se você for um administrador da organização, não há nenhuma confirmação necessária para aceitar a propriedade. No entanto, se você for um colaborador, adicionando a organização como um proprietário requer um dos administradores para aceitar a propriedade.

## <a name="publishing-packages"></a>Publicando pacotes

Publicar pacotes para uma organização, como publicar pacotes para uma conta de usuário: Carregando diretamente o pacote no nuget.org ou por push o pacote por meio de `nuget push` ou `dotnet nuget push` comandos da CLI.

### <a name="uploading-packages"></a>Carregando pacotes

Quando você carrega diretamente um novo pacote na [nuget.org Upload](https://www.nuget.org/packages/manage/upload) página, você atribuir o proprietário do pacote a uma conta de usuário ou da organização:

![Carregar pacote com a opção de conta](media/org-upload-option.png)

### <a name="using-api-keys"></a>Usando chaves de API

Para enviar por push a um pacote por meio de `nuget push` ou `dotnet nuget push` comandos da CLI, você deve obter uma chave de API necessária para esses comandos. Para obter detalhes, consulte [publicar um pacote](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Ao criar uma nova chave de API, selecione a organização apropriada na **proprietário do pacote** lista suspensa. Qualquer chave de API que você cria é aplicável somente para a organização escolhida:

![Chave de API com a opção de conta](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Remoção de uma organização

Como um usuário, você pode remover de uma organização, selecionando o `X` botão mostrado pela associação de sua organização:

![Removendo uma conta de usuário de uma organização](media/org-remove-self-option.png)

Os administradores podem remover qualquer membro da organização, incluindo outros administradores. Se você for o único administrador para uma organização, é possível remover você mesmo, a menos que você adiciona outro membro como um administrador.

### <a name="deleting-an-organization-account"></a>Excluir uma conta de organização

Esse recurso estará disponível em breve.
