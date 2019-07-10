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
# <a name="your-organization-on-nugetorg"></a><span data-ttu-id="87cd4-103">Sua organização no NuGet.org</span><span class="sxs-lookup"><span data-stu-id="87cd4-103">Your organization on NuGet.org</span></span>

<span data-ttu-id="87cd4-104">As organizações permitem que empresas e projetos de open-source colaborem em pacotes usando uma única identidade do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="87cd4-104">Organizations enable businesses and open-source projects to collaborate on packages using a single NuGet.org identity.</span></span> <span data-ttu-id="87cd4-105">Para um consumidor do pacote, uma conta da organização é exibida da mesma forma que uma conta de usuário existente no NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="87cd4-105">For a package consumer, an organization account appears same as an existing user account on NuGet.org.</span></span>

## <a name="organization-accounts-vs-individual-accounts"></a><span data-ttu-id="87cd4-106">Contas da organização vs. contas individuais</span><span class="sxs-lookup"><span data-stu-id="87cd4-106">Organization accounts vs. individual accounts</span></span>

<span data-ttu-id="87cd4-107">Uma conta da organização tem uma ou mais contas (de usuário) individuais como seus membros.</span><span class="sxs-lookup"><span data-stu-id="87cd4-107">An organization account has one or more individual (user) accounts as its members.</span></span> <span data-ttu-id="87cd4-108">Esses membros podem gerenciar um conjunto de pacotes, mantendo uma única identidade para a propriedade.</span><span class="sxs-lookup"><span data-stu-id="87cd4-108">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

<span data-ttu-id="87cd4-109">Sua conta individual é a sua identidade no NuGet.org e pode ser membro de qualquer número de organizações.</span><span class="sxs-lookup"><span data-stu-id="87cd4-109">Your individual account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="87cd4-110">Um pacote pode pertencer a uma conta da organização da mesma forma que pode pertencer a uma conta individual.</span><span class="sxs-lookup"><span data-stu-id="87cd4-110">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="87cd4-111">Os consumidores do pacote não veem nenhuma diferença entre uma conta individual ou a conta da organização: ambas são exibidas como o pacote `owners`.</span><span class="sxs-lookup"><span data-stu-id="87cd4-111">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="87cd4-112">Como adicionar uma nova organização</span><span class="sxs-lookup"><span data-stu-id="87cd4-112">Adding a new organization</span></span>

<span data-ttu-id="87cd4-113">Para adicionar uma nova organização, selecione sua conta no NuGet.org e, em seguida, selecione o comando de menu **Gerenciar Organizações...** :</span><span class="sxs-lookup"><span data-stu-id="87cd4-113">To add a new organization, select your account on NuGet.org, then select the **Manage Organizations...** menu command:</span></span>

![Opção de menu Gerenciar Organizações no NuGet.org](media/org-manage-option.png)

<span data-ttu-id="87cd4-115">Na próxima página, selecione o botão **Adicionar nova organização**:</span><span class="sxs-lookup"><span data-stu-id="87cd4-115">On the next page, select the **Add new organization** button:</span></span>

![Botão para criar uma organização no NuGet.org](media/org-add-new-option.png)

<span data-ttu-id="87cd4-117">Na próxima página, forneça o nome da organização e o endereço de email.</span><span class="sxs-lookup"><span data-stu-id="87cd4-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="87cd4-118">Como as contas da organização compartilham o mesmo namespace das contas de usuário, o nome da organização precisa ser diferente de qualquer conta de usuário ou da organização existente.</span><span class="sxs-lookup"><span data-stu-id="87cd4-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="87cd4-119">O endereço de email também precisa ser exclusivo em todas as contas.</span><span class="sxs-lookup"><span data-stu-id="87cd4-119">The email address must also be unique across all accounts.</span></span>

![Página Adicionar nova organização no NuGet.org](media/org-add-new-page.png)

<span data-ttu-id="87cd4-121">Após a criação da conta da organização, você será o administrador e poderá enviar pacotes para a organização e adicionar membros da organização.</span><span class="sxs-lookup"><span data-stu-id="87cd4-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="87cd4-122">Transformar a conta existente em uma organização</span><span class="sxs-lookup"><span data-stu-id="87cd4-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="87cd4-123">A conversão de conta é irreversível: não é possível transformar uma organização novamente em uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="87cd4-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="87cd4-124">Caso você esteja gerenciando pacotes como uma equipe usando uma única conta de usuário e deseje converter essa conta em uma organização, use a opção **Transformar sua conta em uma organização** na página **Gerenciar Organizações**:</span><span class="sxs-lookup"><span data-stu-id="87cd4-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Opção no NuGet.org para transformar uma conta existente em uma organização](media/org-transform-option.png)

<span data-ttu-id="87cd4-126">Na próxima página, especifique outra conta de usuário para atribuir como o administrador da organização e, em seguida, selecione **Transformar**.</span><span class="sxs-lookup"><span data-stu-id="87cd4-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Como inserir informações para transformar uma conta de usuário em uma organização](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="87cd4-128">Como gerenciar os membros da organização</span><span class="sxs-lookup"><span data-stu-id="87cd4-128">Managing organization members</span></span>

<span data-ttu-id="87cd4-129">Como o administrador da organização, você poderá adicionar membros fornecendo o *nome da conta de usuário* do NuGet.org de cada membro; endereços de email não podem ser usados.</span><span class="sxs-lookup"><span data-stu-id="87cd4-129">As the organization administrator, you can add members by providing each member's NuGet.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="87cd4-130">Em seguida, você marcará cada membro como colaborador ou administrador com as seguintes permissões:</span><span class="sxs-lookup"><span data-stu-id="87cd4-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="87cd4-131">Permissão</span><span class="sxs-lookup"><span data-stu-id="87cd4-131">Permission</span></span> | <span data-ttu-id="87cd4-132">Colaborador</span><span class="sxs-lookup"><span data-stu-id="87cd4-132">Collaborator</span></span> | <span data-ttu-id="87cd4-133">Administrador</span><span class="sxs-lookup"><span data-stu-id="87cd4-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="87cd4-134">Gerenciar os pacotes da organização</span><span class="sxs-lookup"><span data-stu-id="87cd4-134">Manage the organization's packages</span></span><br/><span data-ttu-id="87cd4-135">(enviar novos pacotes, atualizar pacotes existentes ou removê-los da lista)</span><span class="sxs-lookup"><span data-stu-id="87cd4-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="87cd4-136">Sim</span><span class="sxs-lookup"><span data-stu-id="87cd4-136">Yes</span></span> | <span data-ttu-id="87cd4-137">Sim</span><span class="sxs-lookup"><span data-stu-id="87cd4-137">Yes</span></span> |
| <span data-ttu-id="87cd4-138">Alterar os metadados da organização</span><span class="sxs-lookup"><span data-stu-id="87cd4-138">Change organization metadata</span></span><br/><span data-ttu-id="87cd4-139">(endereço de email, configurações de notificação)</span><span class="sxs-lookup"><span data-stu-id="87cd4-139">(email address, notification settings)</span></span> | <span data-ttu-id="87cd4-140">Não</span><span class="sxs-lookup"><span data-stu-id="87cd4-140">No</span></span> | <span data-ttu-id="87cd4-141">Sim</span><span class="sxs-lookup"><span data-stu-id="87cd4-141">Yes</span></span> |
| <span data-ttu-id="87cd4-142">Gerenciar os membros da organização</span><span class="sxs-lookup"><span data-stu-id="87cd4-142">Manage organization members</span></span> | <span data-ttu-id="87cd4-143">Não</span><span class="sxs-lookup"><span data-stu-id="87cd4-143">No</span></span> | <span data-ttu-id="87cd4-144">Sim</span><span class="sxs-lookup"><span data-stu-id="87cd4-144">Yes</span></span> |
| <span data-ttu-id="87cd4-145">Solicitar ou tomar decisões em solicitações de copropriedade para os pacotes da organização</span><span class="sxs-lookup"><span data-stu-id="87cd4-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="87cd4-146">Não</span><span class="sxs-lookup"><span data-stu-id="87cd4-146">No</span></span> | <span data-ttu-id="87cd4-147">Sim</span><span class="sxs-lookup"><span data-stu-id="87cd4-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="87cd4-148">Como gerenciar pacotes</span><span class="sxs-lookup"><span data-stu-id="87cd4-148">Managing packages</span></span>

<span data-ttu-id="87cd4-149">Você pode ver todos os pacotes em sua conta e todas as organizações das quais você é membro na página [Gerenciar Pacotes](https://www.nuget.org/account/Packages).</span><span class="sxs-lookup"><span data-stu-id="87cd4-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="87cd4-150">Para exibir os pacotes específicos à sua conta ou a qualquer organização específica, use o filtro de contas no canto superior direito da página.</span><span class="sxs-lookup"><span data-stu-id="87cd4-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Como gerenciar pacotes com o filtro de conta](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="87cd4-152">Como transferir pacotes para uma organização</span><span class="sxs-lookup"><span data-stu-id="87cd4-152">Transferring packages to an organization</span></span>
<span data-ttu-id="87cd4-153">Caso você deseje transferir alguns de seus pacotes para uma organização recém-criada, faça isso solicitando à conta da organização que seja um coproprietário do pacote e, em seguida, removendo a si mesmo como o proprietário.</span><span class="sxs-lookup"><span data-stu-id="87cd4-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="87cd4-154">Se você for um administrador da organização, nenhuma confirmação será necessária para aceitar a propriedade.</span><span class="sxs-lookup"><span data-stu-id="87cd4-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="87cd4-155">No entanto, se você for um colaborador, a adição da organização como um proprietário exigirá que um dos administradores aceite a propriedade.</span><span class="sxs-lookup"><span data-stu-id="87cd4-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="87cd4-156">Publicando pacotes</span><span class="sxs-lookup"><span data-stu-id="87cd4-156">Publishing packages</span></span>

<span data-ttu-id="87cd4-157">Você publica pacotes para uma organização da mesma forma como publica pacotes para uma conta de usuário: carregando o pacote diretamente no NuGet.org ou efetuando push do pacote por meio dos comandos `nuget push` ou `dotnet nuget push` da CLI.</span><span class="sxs-lookup"><span data-stu-id="87cd4-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to NuGet.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="87cd4-158">Como carregar pacotes</span><span class="sxs-lookup"><span data-stu-id="87cd4-158">Uploading packages</span></span>

<span data-ttu-id="87cd4-159">Ao carregar um novo pacote diretamente na página [Upload do NuGet.org](https://www.nuget.org/packages/manage/upload), você atribui o proprietário do pacote a uma conta de usuário ou da organização:</span><span class="sxs-lookup"><span data-stu-id="87cd4-159">When you directly upload a new package on the [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Carregar um pacote com a opção de conta](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="87cd4-161">Como usar chaves de API</span><span class="sxs-lookup"><span data-stu-id="87cd4-161">Using API keys</span></span>

<span data-ttu-id="87cd4-162">Para efetuar push de um pacote por meio dos comandos `nuget push` ou `dotnet nuget push` da CLI, você precisará obter uma chave de API necessária para esses comandos.</span><span class="sxs-lookup"><span data-stu-id="87cd4-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="87cd4-163">Para obter detalhes, confira [Publicar um pacote](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="87cd4-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="87cd4-164">Ao criar uma chave de API, selecione a organização apropriada na lista suspensa **Proprietário do Pacote**.</span><span class="sxs-lookup"><span data-stu-id="87cd4-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="87cd4-165">Qualquer chave de API criada é aplicável somente à organização escolhida:</span><span class="sxs-lookup"><span data-stu-id="87cd4-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Chave de API com a opção de conta](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="87cd4-167">Como remover uma organização</span><span class="sxs-lookup"><span data-stu-id="87cd4-167">Removing an organization</span></span>

<span data-ttu-id="87cd4-168">Como usuário, você pode remover a si mesmo de uma organização selecionando o botão **X** mostrado pela associação de sua organização:</span><span class="sxs-lookup"><span data-stu-id="87cd4-168">As a user, you can remove yourself from an organization by selecting the **X** button shown by your organization membership:</span></span>

![Como remover uma conta de usuário de uma organização](media/org-remove-self-option.png)

<span data-ttu-id="87cd4-170">Os administradores podem remover qualquer membro da organização, incluindo outros administradores.</span><span class="sxs-lookup"><span data-stu-id="87cd4-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="87cd4-171">Se você for o único administrador de uma organização, não poderá remover a si mesmo, a menos que adicione outro membro como administrador.</span><span class="sxs-lookup"><span data-stu-id="87cd4-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="87cd4-172">Como excluir uma conta da organização</span><span class="sxs-lookup"><span data-stu-id="87cd4-172">Deleting an organization account</span></span>

<span data-ttu-id="87cd4-173">Exclua uma conta da organização clicando no botão **Excluir** mostrado na página de sua organização.</span><span class="sxs-lookup"><span data-stu-id="87cd4-173">You can delete an organization account by clicking the **Delete** button shown in your organization page.</span></span>

![Como excluir uma organização](media/org-delete-option.png)

<span data-ttu-id="87cd4-175">Para excluir a organização, você precisará confirmar isso clicando no botão de confirmação **Excluir organização**.</span><span class="sxs-lookup"><span data-stu-id="87cd4-175">To delete the organizaiton, you must confirm it by clicking the **Delete organization** confirmation button.</span></span>
