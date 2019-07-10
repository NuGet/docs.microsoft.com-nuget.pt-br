---
title: Contas individuais
description: São necessárias contas individuais no NuGet.org para publicar pacotes
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427131"
---
# <a name="individual-accounts"></a><span data-ttu-id="abe9c-103">Contas individuais</span><span class="sxs-lookup"><span data-stu-id="abe9c-103">Individual accounts</span></span>

<span data-ttu-id="abe9c-104">É necessário criar uma conta individual para publicar e gerenciar pacotes no NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="abe9c-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="abe9c-105">Contas individuais vs. contas da organização</span><span class="sxs-lookup"><span data-stu-id="abe9c-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="abe9c-106">Sua conta (de usuário) individual é a sua identidade no NuGet.org e pode ser membro de qualquer número de organizações.</span><span class="sxs-lookup"><span data-stu-id="abe9c-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="abe9c-107">Um pacote pode pertencer a uma conta da organização da mesma forma que pode pertencer a uma conta individual.</span><span class="sxs-lookup"><span data-stu-id="abe9c-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="abe9c-108">Os consumidores do pacote não veem nenhuma diferença entre uma conta individual ou a conta da organização: ambas são exibidas como o pacote `owners`.</span><span class="sxs-lookup"><span data-stu-id="abe9c-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="abe9c-109">Uma conta da organização tem uma ou mais contas individuais como seus membros.</span><span class="sxs-lookup"><span data-stu-id="abe9c-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="abe9c-110">Esses membros podem gerenciar um conjunto de pacotes, mantendo uma única identidade para a propriedade.</span><span class="sxs-lookup"><span data-stu-id="abe9c-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="abe9c-111">Adicionar uma nova conta individual</span><span class="sxs-lookup"><span data-stu-id="abe9c-111">Add a new individual account</span></span>

<span data-ttu-id="abe9c-112">Para criar uma conta do NuGet.org, você precisa ter uma MSA (conta Microsoft pessoal) ou uma conta do AAD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="abe9c-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="abe9c-113">Se não tiver uma ID da Apple, [crie](https://signup.live.com) uma.</span><span class="sxs-lookup"><span data-stu-id="abe9c-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="abe9c-114">Siga as etapas a seguir caso você tenha uma conta MSA ou do AAD.</span><span class="sxs-lookup"><span data-stu-id="abe9c-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="abe9c-115">Acesse a [página de logon do NuGet.org](https://www.nuget.org/users/account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="abe9c-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="abe9c-116">Clique no botão **Entrar com a conta Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="abe9c-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="abe9c-117">Insira os detalhes de sua conta Microsoft ou sua conta do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="abe9c-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="abe9c-118">Clique em **Sim** para aceitar as permissões a serem concedidas ao aplicativo do *NuGet.org*.</span><span class="sxs-lookup"><span data-stu-id="abe9c-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Como conceder permissões ao NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="abe9c-120">Você será redirecionado para *nuget.org* e deverá registrar um nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="abe9c-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="abe9c-121">Especifique o nome de usuário na caixa de entrada.</span><span class="sxs-lookup"><span data-stu-id="abe9c-121">Specify the username in the input box.</span></span> <span data-ttu-id="abe9c-122">Observe que o nome de usuário **diferencia** maiúsculas de minúsculas e não pode ser alterado ou renomeado mais tarde.</span><span class="sxs-lookup"><span data-stu-id="abe9c-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Especificar um nome de usuário no NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="abe9c-124">Clique no botão **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="abe9c-124">Click the **Register** button.</span></span>

<span data-ttu-id="abe9c-125">Agora você tem uma conta do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="abe9c-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="abe9c-126">Realize o gerenciamento de contas na página de [configurações da conta](https://www.nuget.org/account).</span><span class="sxs-lookup"><span data-stu-id="abe9c-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>
