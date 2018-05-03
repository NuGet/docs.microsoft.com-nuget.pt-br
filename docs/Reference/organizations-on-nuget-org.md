---
title: Organizações em nuget.org
description: As organizações em nuget.org ajuda você a gerenciar pacotes publicados por grupo ou em uma equipe, o ambiente da empresa.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 0e836f5f39620f0b83212c9510735481119ddda2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="organization-on-nugetorg"></a>Organização em nuget.org

Organizações permitir que as empresas e projetos de código-fonte aberto para colaborar nos pacotes usando uma identidade nuget.org único. Para um consumidor de pacote, uma conta de organização é exibida mesma que uma conta de usuário existentes em nuget.org.

## <a name="user-accounts-vs-organization-accounts"></a>Contas de usuário e contas da organização

Sua conta de usuário é sua identidade em nuget.org e pode ser um membro de qualquer número de organizações. Um pacote pode pertencer a uma conta de organização como ele pode pertencer a uma conta de usuário. Os consumidores de pacote não percebem nenhuma diferença entre uma conta de usuário ou a conta de organização: ambos aparecem como pacote `owners`.

Uma conta de organização tem uma ou mais contas de usuário como membros. Esses membros podem administrar um conjunto de pacotes, mantendo uma única identidade de propriedade.

## <a name="adding-a-new-organization"></a>Adicionando uma nova organização

Para adicionar uma nova organização, selecione sua conta em nuget.org e selecione o **gerenciar organizações...**  comando de menu:

![Opção de menu em nuget.org para organizações Manager](media/org-manage-option.png)

Na página seguinte, selecione o **adicionar nova organização** botão:

![Botão para criar uma nova organização em nuget.org](media/org-add-new-option.png)

Na próxima página, forneça o endereço de email e o nome da organização. Como contas da organização compartilham o mesmo namespace como contas de usuário, o nome da organização deve ser diferente de qualquer organização existente ou contas de usuário. O endereço de email também deve ser exclusivo entre todas as contas.

![Adicionar nova página de organização em nuget.org](media/org-add-new-page.png)

Depois de criar a conta de organização, você é o administrador e pode enviar pacotes para a organização e adicionar membros da organização.

### <a name="transform-existing-account-to-an-organization"></a>Transformar a conta existente para uma organização

> [!Warning]
> Conversão de conta é irreversível: não é possível transformar uma organização para uma conta de usuário.

Se você estiver gerenciando pacotes em equipe usando uma conta de usuário único e gostaria de converter essa conta em uma organização, use o **transformar sua conta para uma organização** opção o **gerenciar organizações** página:

![Opção em nuget.org para transformar uma conta existente para uma organização](media/org-transform-option.png)

Na próxima página, especifique outra conta de usuário para atribuir como o administrador da organização, em seguida, selecione **transformação**.

![Inserir informações para transformar uma conta de usuário de uma organização](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Gerenciar os membros da organização

Como administrador da organização, você pode adicionar membros, fornecendo a nuget.org cada membro *nome de conta de usuário*; endereços de email não podem ser usados. Você, em seguida, marque cada membro como um parceiro ou com as seguintes permissões:

| Permissão | Colaborador | Administrador |
| --- | --- | --- |
| Gerenciar pacotes da organização<br/>(Enviar novos pacotes, atualizar ou remover da lista de pacotes existentes) | Sim | Sim |
| Metadados de organização de alteração<br/>(endereço de email, as configurações de notificação) | Não | Sim |
| Gerenciar membros da organização | Não | Sim |
| Solicitar ou agir sobre solicitações de co-ownership de pacotes de organização | Não | Sim |

## <a name="managing-packages"></a>Gerenciando pacotes

Você pode exibir todos os pacotes em sua conta e todas as organizações dos quais você é um membro no [gerenciar pacotes](https://www.nuget.org/account/Packages) página. Para exibir os pacotes específicos para sua conta ou qualquer organização específica, use o filtro de contas na parte superior direita da página.

![Gerenciando pacotes com o filtro de conta](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Transferência de pacotes para uma organização
Se você deseja transferir alguns de seus pacotes para uma organização criada recentemente, você pode fazer isso solicitando a conta de organização para coproprietário o pacote e, em seguida, remover você mesmo como o proprietário. Se você for um administrador da organização, não há nenhuma confirmação precisam aceitar a propriedade. No entanto, se você for um colaborador, adicionando a organização como um proprietário requer um dos administradores para aceitar a propriedade.

## <a name="publishing-packages"></a>Publicando pacotes

Publicar pacotes de uma organização que você publicar pacotes em uma conta de usuário: Carregando diretamente o pacote em nuget.org ou enviando o pacote por meio de `nuget push` ou `dotnet nuget push` comandos CLI.

### <a name="uploading-packages"></a>Carregando pacotes

Quando você carrega diretamente um novo pacote no [nuget.org carregamento](https://www.nuget.org/packages/manage/upload) página, você atribui o proprietário do pacote para uma conta de usuário ou a organização:

![Carregar pacote com a opção de conta](media/org-upload-option.png)

### <a name="using-api-keys"></a>Usando chaves de API

Para enviar um pacote por meio de `nuget push` ou `dotnet nuget push` comandos CLI, você deve obter uma chave de API necessária por esses comandos. Para obter detalhes, consulte [publica um pacote](https://docs.microsoft.com/en-us/nuget/quickstart/create-and-publish-a-package-using-visual-studio#publish-the-package).

Ao criar uma nova chave de API, selecione a organização apropriada no **proprietário do pacote** lista suspensa. Qualquer chave de API que você cria é aplicável somente para a organização escolhida:

![Chave de API com a opção de conta](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Remoção de uma organização

Como um usuário, você pode remover seu nome de uma organização selecionando o `X` mostrado pela associação de sua organização:

![Removendo uma conta de usuário de uma organização](media/org-remove-self-option.png)

Os administradores podem remover qualquer membro da organização, incluindo outros administradores. Se você for o único administrador para uma organização, você não pode remover você mesmo, a menos que você adicionar outro membro como um administrador.

### <a name="deleting-an-organization-account"></a>Excluir uma conta de organização

Este recurso estará disponível em breve.
