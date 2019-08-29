---
title: Contas individuais – NuGet.org
description: São necessárias contas individuais no NuGet.org para publicar pacotes
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 63c6b5eb5ad635e436b4d53a5f833af35f72d76f
ms.sourcegitcommit: 7c9f157ba02d9be543de34ab06813ab1ec10192a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69999973"
---
# <a name="individual-accounts-on-nugetorg"></a><span data-ttu-id="ea352-103">Contas individuais no NuGet.org</span><span class="sxs-lookup"><span data-stu-id="ea352-103">Individual accounts on NuGet.org</span></span>

<span data-ttu-id="ea352-104">É necessário criar uma conta individual para publicar e gerenciar pacotes no NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="ea352-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="ea352-105">Contas individuais vs. contas da organização</span><span class="sxs-lookup"><span data-stu-id="ea352-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="ea352-106">Sua conta (de usuário) individual é a sua identidade no NuGet.org e pode ser membro de qualquer número de organizações.</span><span class="sxs-lookup"><span data-stu-id="ea352-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="ea352-107">Um pacote pode pertencer a uma conta da organização da mesma forma que pode pertencer a uma conta individual.</span><span class="sxs-lookup"><span data-stu-id="ea352-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="ea352-108">Os consumidores do pacote não veem nenhuma diferença entre uma conta individual ou a conta da organização: ambas são exibidas como o pacote `owners`.</span><span class="sxs-lookup"><span data-stu-id="ea352-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="ea352-109">Uma conta da organização tem uma ou mais contas individuais como seus membros.</span><span class="sxs-lookup"><span data-stu-id="ea352-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="ea352-110">Esses membros podem gerenciar um conjunto de pacotes, mantendo uma única identidade para a propriedade.</span><span class="sxs-lookup"><span data-stu-id="ea352-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="ea352-111">Adicionar uma nova conta individual</span><span class="sxs-lookup"><span data-stu-id="ea352-111">Add a new individual account</span></span>

<span data-ttu-id="ea352-112">Para criar uma conta do NuGet.org, você precisa ter uma MSA (conta Microsoft pessoal) ou uma conta do AAD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ea352-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="ea352-113">Se não tiver uma ID da Apple, [crie](https://signup.live.com) uma.</span><span class="sxs-lookup"><span data-stu-id="ea352-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="ea352-114">Siga as etapas a seguir caso você tenha uma conta MSA ou do AAD.</span><span class="sxs-lookup"><span data-stu-id="ea352-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="ea352-115">Acesse a [página de logon do NuGet.org](https://www.nuget.org/users/account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="ea352-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="ea352-116">Clique no botão **Entrar com a conta Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="ea352-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="ea352-117">Insira os detalhes de sua conta Microsoft ou sua conta do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ea352-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="ea352-118">Clique em **Sim** para aceitar as permissões a serem concedidas ao aplicativo do *NuGet.org*.</span><span class="sxs-lookup"><span data-stu-id="ea352-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Como conceder permissões ao NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="ea352-120">Você será redirecionado para *nuget.org* e deverá registrar um nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="ea352-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="ea352-121">Especifique o nome de usuário na caixa de entrada.</span><span class="sxs-lookup"><span data-stu-id="ea352-121">Specify the username in the input box.</span></span> <span data-ttu-id="ea352-122">Observe que o nome de usuário **diferencia** maiúsculas de minúsculas e não pode ser alterado ou renomeado mais tarde.</span><span class="sxs-lookup"><span data-stu-id="ea352-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Especificar um nome de usuário no NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="ea352-124">Clique no botão **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="ea352-124">Click the **Register** button.</span></span>

<span data-ttu-id="ea352-125">Agora você tem uma conta do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="ea352-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="ea352-126">Realize o gerenciamento de contas na página de [configurações da conta](https://www.nuget.org/account).</span><span class="sxs-lookup"><span data-stu-id="ea352-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>

## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="ea352-127">Habilitar a autenticação de dois fatores (2FA)</span><span class="sxs-lookup"><span data-stu-id="ea352-127">Enable two-factor authentication (2FA)</span></span>

<span data-ttu-id="ea352-128">Para proteger melhor sua conta, habilite a autenticação de dois fatores (recomendada).</span><span class="sxs-lookup"><span data-stu-id="ea352-128">To better protect your account, enable two-factor authentication (recommended).</span></span>

1. <span data-ttu-id="ea352-129">Depois de entrar em sua conta, abra seu perfil e escolha **Habilitar** em **Conta de logon**.</span><span class="sxs-lookup"><span data-stu-id="ea352-129">When logged into your account, open your profile and choose **Enable** under **Login Account**.</span></span>

   ![Habilitar 2FA](media/nuget-org-register-2fa.png)

   <span data-ttu-id="ea352-131">Você verá uma mensagem informando que, na próxima vez que entrar em *nuget.org*, serão solicitadas credenciais adicionais.</span><span class="sxs-lookup"><span data-stu-id="ea352-131">You will see a message that tells you that the next time you sign in to *nuget.org*, you will be asked for additional credentials.</span></span>

2. <span data-ttu-id="ea352-132">Para concluir a autenticação neste momento, saia e entre novamente.</span><span class="sxs-lookup"><span data-stu-id="ea352-132">To complete the authentication at this time, sign out and then sign in again.</span></span>

3. <span data-ttu-id="ea352-133">Ao entrar, escolha se deseja receber uma mensagem de texto ou email como uma segunda forma de autenticação.</span><span class="sxs-lookup"><span data-stu-id="ea352-133">When you sign in, choose either text or e-mail as a second form of authentication.</span></span>

   <span data-ttu-id="ea352-134">Verifique o número de telefone ou email já associados à sua conta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ea352-134">Verify the phone number or e-mail that is already associated with your Microsoft account.</span></span> <span data-ttu-id="ea352-135">Talvez seja necessário inserir um novo número de telefone ou email para sua conta.</span><span class="sxs-lookup"><span data-stu-id="ea352-135">You may need to enter a new phone number or e-mail for your account.</span></span> <span data-ttu-id="ea352-136">Nesse caso, insira as informações necessárias como instruído e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="ea352-136">If so, enter the required information as instructed, and click **Next**.</span></span>

   ![Habilitar 2FA](media/nuget-org-sign-in-2fa.png)

4. <span data-ttu-id="ea352-138">Verifique seu dispositivo ou conta de email e insira o código que você acabou de receber.</span><span class="sxs-lookup"><span data-stu-id="ea352-138">Check your device or e-mail account, and enter the code that you were just sent.</span></span>

   ![Habilitar 2FA](media/nuget-org-enter-code-2fa.png)

5. <span data-ttu-id="ea352-140">Siga as instruções adicionais para concluir a autenticação de dois fatores.</span><span class="sxs-lookup"><span data-stu-id="ea352-140">Follow any additional instructions to complete Two-factor authentication.</span></span>

## <a name="delete-a-nugetorg-account"></a><span data-ttu-id="ea352-141">Excluir uma conta do NuGet.org</span><span class="sxs-lookup"><span data-stu-id="ea352-141">Delete a NuGet.org account</span></span>

<span data-ttu-id="ea352-142">Para obter ajuda com tarefas adicionais relacionadas a contas, por exemplo, excluir uma conta do NuGet.org, confira [Gerenciamento de conta do NuGet.org](nuget-org-faq.md#nugetorg-account-management).</span><span class="sxs-lookup"><span data-stu-id="ea352-142">For help with additional account-related tasks, such as deleting a NuGet.org account, see [NuGet.org account management](nuget-org-faq.md#nugetorg-account-management).</span></span>
