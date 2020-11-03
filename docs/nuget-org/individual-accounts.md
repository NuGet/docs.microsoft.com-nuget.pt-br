---
title: Contas individuais – NuGet.org
description: São necessárias contas individuais no NuGet.org para publicar pacotes
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 7951b3db0cdcaee0a1eb955a5bf6fedce24c79c9
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237608"
---
# <a name="individual-accounts-on-nugetorg"></a>Contas individuais no NuGet.org

É necessário criar uma conta individual para publicar e gerenciar pacotes no NuGet.org.

## <a name="individual-accounts-vs-organization-accounts"></a>Contas individuais vs. contas da organização

Sua conta (de usuário) individual é a sua identidade no NuGet.org e pode ser membro de qualquer número de organizações. Um pacote pode pertencer a uma conta da organização da mesma forma que pode pertencer a uma conta individual. Os consumidores do pacote não veem nenhuma diferença entre uma conta individual ou a conta da organização: ambas são exibidas como o pacote `owners`.

Uma conta da organização tem uma ou mais contas individuais como seus membros. Esses membros podem gerenciar um conjunto de pacotes, mantendo uma única identidade para a propriedade.

## <a name="add-a-new-individual-account"></a>Adicionar uma nova conta individual

Para criar uma conta do NuGet.org, você precisa ter uma MSA (conta Microsoft pessoal) ou uma conta do AAD (Azure Active Directory). Se não tiver uma ID da Apple, [crie](https://signup.live.com) uma. Siga as etapas a seguir caso você tenha uma conta MSA ou do AAD.

1. Vá para a [página de logon do NuGet.org](https://www.nuget.org/users/account/LogOn).

1. Clique no botão **Entrar com a conta Microsoft** .

1. Insira os detalhes de sua conta Microsoft ou sua conta do Azure Active Directory.

1. Clique em **Sim** para aceitar as permissões a serem concedidas ao aplicativo do *NuGet.org* .

   ![Como conceder permissões ao NuGet.org](media/nuget-org-permissions.png)

1. Você será redirecionado para *NuGet.org* e solicitado a registrar um nome de usuário.

1. Especifique o nome de usuário na caixa de entrada. Observe que o nome de usuário **diferencia** maiúsculas de minúsculas e não pode ser alterado ou renomeado mais tarde.

   ![Especificar um nome de usuário no NuGet.org](media/nuget-org-register.png) 

1. Clique no botão **registrar** .

Agora você tem uma conta do NuGet.org. Realize o gerenciamento de contas na página de [configurações da conta](https://www.nuget.org/account).

## <a name="enable-two-factor-authentication-2fa"></a>Habilitar a autenticação de dois fatores (2FA)

A autenticação de dois fatores, ou 2FA, é uma camada extra de segurança usada ao fazer logon em sites ou aplicativos. Com o 2FA, você precisa fazer logon com sua conta da Microsoft (MSA) e fornecer outra forma de autenticação que só você conhece ou tem acesso ao. Para proteger melhor sua conta, habilite a autenticação de dois fatores (recomendada).

1. Depois de entrar em sua conta, abra seu perfil e escolha **Habilitar** em **Conta de logon** .

   ![Habilitar 2FA](media/nuget-org-register-2fa.png)

   Você verá uma mensagem informando que, na próxima vez que entrar em *nuget.org* , serão solicitadas credenciais adicionais.

2. Para concluir a autenticação neste momento, saia e entre novamente.

3. Ao entrar, escolha se deseja receber uma mensagem de texto ou email como uma segunda forma de autenticação.

   Verifique o número de telefone ou email já associados à sua conta Microsoft. Talvez seja necessário inserir um novo número de telefone ou email para sua conta. Nesse caso, insira as informações necessárias como instruído e clique em **Avançar** .

   ![Habilitar 2FA](media/nuget-org-sign-in-2fa.png)

4. Verifique seu dispositivo ou conta de email e insira o código que você acabou de receber.

   ![Habilitar 2FA](media/nuget-org-enter-code-2fa.png)

5. Siga as instruções adicionais para concluir a autenticação de dois fatores.

> [!Tip]
> Habilitar o 2FA para sua conta do NuGet.org não afeta as configurações de autenticação para outras contas ou serviços que podem estar vinculados ao conta Microsoft usado para fazer logon no NuGet.org.

## <a name="delete-a-nugetorg-account"></a>Excluir uma conta do NuGet.org

Para obter ajuda com tarefas adicionais relacionadas a contas, por exemplo, excluir uma conta do NuGet.org, confira [Gerenciamento de conta do NuGet.org](nuget-org-faq.md#nugetorg-account-management).
