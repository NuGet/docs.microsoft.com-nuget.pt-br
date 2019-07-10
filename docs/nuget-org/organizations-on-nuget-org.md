---
title: Sua organização no NuGet.org
description: As organizações no NuGet.org ajudam você a gerenciar os pacotes publicados por grupo ou no ambiente da empresa de uma equipe.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427071"
---
# <a name="your-organization-on-nugetorg"></a>Sua organização no NuGet.org

As organizações permitem que empresas e projetos de open-source colaborem em pacotes usando uma única identidade do NuGet.org. Para um consumidor do pacote, uma conta da organização é exibida da mesma forma que uma conta de usuário existente no NuGet.org.

## <a name="organization-accounts-vs-individual-accounts"></a>Contas da organização vs. contas individuais

Uma conta da organização tem uma ou mais contas (de usuário) individuais como seus membros. Esses membros podem gerenciar um conjunto de pacotes, mantendo uma única identidade para a propriedade.

Sua conta individual é a sua identidade no NuGet.org e pode ser membro de qualquer número de organizações. Um pacote pode pertencer a uma conta da organização da mesma forma que pode pertencer a uma conta individual. Os consumidores do pacote não veem nenhuma diferença entre uma conta individual ou a conta da organização: ambas são exibidas como o pacote `owners`.

## <a name="adding-a-new-organization"></a>Como adicionar uma nova organização

Para adicionar uma nova organização, selecione sua conta no NuGet.org e, em seguida, selecione o comando de menu **Gerenciar Organizações...** :

![Opção de menu Gerenciar Organizações no NuGet.org](media/org-manage-option.png)

Na próxima página, selecione o botão **Adicionar nova organização**:

![Botão para criar uma organização no NuGet.org](media/org-add-new-option.png)

Na próxima página, forneça o nome da organização e o endereço de email. Como as contas da organização compartilham o mesmo namespace das contas de usuário, o nome da organização precisa ser diferente de qualquer conta de usuário ou da organização existente. O endereço de email também precisa ser exclusivo em todas as contas.

![Página Adicionar nova organização no NuGet.org](media/org-add-new-page.png)

Após a criação da conta da organização, você será o administrador e poderá enviar pacotes para a organização e adicionar membros da organização.

### <a name="transform-existing-account-to-an-organization"></a>Transformar a conta existente em uma organização

> [!Warning]
> A conversão de conta é irreversível: não é possível transformar uma organização novamente em uma conta de usuário.

Caso você esteja gerenciando pacotes como uma equipe usando uma única conta de usuário e deseje converter essa conta em uma organização, use a opção **Transformar sua conta em uma organização** na página **Gerenciar Organizações**:

![Opção no NuGet.org para transformar uma conta existente em uma organização](media/org-transform-option.png)

Na próxima página, especifique outra conta de usuário para atribuir como o administrador da organização e, em seguida, selecione **Transformar**.

![Como inserir informações para transformar uma conta de usuário em uma organização](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Como gerenciar os membros da organização

Como o administrador da organização, você poderá adicionar membros fornecendo o *nome da conta de usuário* do NuGet.org de cada membro; endereços de email não podem ser usados. Em seguida, você marcará cada membro como colaborador ou administrador com as seguintes permissões:

| Permissão | Colaborador | Administrador |
| --- | --- | --- |
| Gerenciar os pacotes da organização<br/>(enviar novos pacotes, atualizar pacotes existentes ou removê-los da lista) | Sim | Sim |
| Alterar os metadados da organização<br/>(endereço de email, configurações de notificação) | Não | Sim |
| Gerenciar os membros da organização | Não | Sim |
| Solicitar ou tomar decisões em solicitações de copropriedade para os pacotes da organização | Não | Sim |

## <a name="managing-packages"></a>Como gerenciar pacotes

Você pode ver todos os pacotes em sua conta e todas as organizações das quais você é membro na página [Gerenciar Pacotes](https://www.nuget.org/account/Packages). Para exibir os pacotes específicos à sua conta ou a qualquer organização específica, use o filtro de contas no canto superior direito da página.

![Como gerenciar pacotes com o filtro de conta](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Como transferir pacotes para uma organização
Caso você deseje transferir alguns de seus pacotes para uma organização recém-criada, faça isso solicitando à conta da organização que seja um coproprietário do pacote e, em seguida, removendo a si mesmo como o proprietário. Se você for um administrador da organização, nenhuma confirmação será necessária para aceitar a propriedade. No entanto, se você for um colaborador, a adição da organização como um proprietário exigirá que um dos administradores aceite a propriedade.

## <a name="publishing-packages"></a>Publicando pacotes

Você publica pacotes para uma organização da mesma forma como publica pacotes para uma conta de usuário: carregando o pacote diretamente no NuGet.org ou efetuando push do pacote por meio dos comandos `nuget push` ou `dotnet nuget push` da CLI.

### <a name="uploading-packages"></a>Como carregar pacotes

Ao carregar um novo pacote diretamente na página [Upload do NuGet.org](https://www.nuget.org/packages/manage/upload), você atribui o proprietário do pacote a uma conta de usuário ou da organização:

![Carregar um pacote com a opção de conta](media/org-upload-option.png)

### <a name="using-api-keys"></a>Como usar chaves de API

Para efetuar push de um pacote por meio dos comandos `nuget push` ou `dotnet nuget push` da CLI, você precisará obter uma chave de API necessária para esses comandos. Para obter detalhes, confira [Publicar um pacote](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Ao criar uma chave de API, selecione a organização apropriada na lista suspensa **Proprietário do Pacote**. Qualquer chave de API criada é aplicável somente à organização escolhida:

![Chave de API com a opção de conta](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Como remover uma organização

Como usuário, você pode remover a si mesmo de uma organização selecionando o botão **X** mostrado pela associação de sua organização:

![Como remover uma conta de usuário de uma organização](media/org-remove-self-option.png)

Os administradores podem remover qualquer membro da organização, incluindo outros administradores. Se você for o único administrador de uma organização, não poderá remover a si mesmo, a menos que adicione outro membro como administrador.

### <a name="deleting-an-organization-account"></a>Como excluir uma conta da organização

Exclua uma conta da organização clicando no botão **Excluir** mostrado na página de sua organização.

![Como excluir uma organização](media/org-delete-option.png)

Para excluir a organização, você precisará confirmar isso clicando no botão de confirmação **Excluir organização**.
