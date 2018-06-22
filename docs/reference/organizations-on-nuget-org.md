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
ms.openlocfilehash: 7f40654a08ac221c5ec3a90c86387b6760b28994
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34449572"
---
# <a name="organization-on-nugetorg"></a><span data-ttu-id="7859b-103">Organização em nuget.org</span><span class="sxs-lookup"><span data-stu-id="7859b-103">Organization on nuget.org</span></span>

<span data-ttu-id="7859b-104">Organizações permitir que as empresas e projetos de código-fonte aberto para colaborar nos pacotes usando uma identidade nuget.org único.</span><span class="sxs-lookup"><span data-stu-id="7859b-104">Organizations enable businesses and open-source projects to collaborate on packages using a single nuget.org identity.</span></span> <span data-ttu-id="7859b-105">Para um consumidor de pacote, uma conta de organização é exibida mesma que uma conta de usuário existentes em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7859b-105">For a package consumer, an organization account appears same as an existing user account on nuget.org.</span></span>

## <a name="user-accounts-vs-organization-accounts"></a><span data-ttu-id="7859b-106">Contas de usuário e contas da organização</span><span class="sxs-lookup"><span data-stu-id="7859b-106">User accounts vs. organization accounts</span></span>

<span data-ttu-id="7859b-107">Sua conta de usuário é sua identidade em nuget.org e pode ser um membro de qualquer número de organizações.</span><span class="sxs-lookup"><span data-stu-id="7859b-107">Your user account is your identity on nuget.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="7859b-108">Um pacote pode pertencer a uma conta de organização como ele pode pertencer a uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="7859b-108">A package can belong to an organization account like it can belong to a user account.</span></span> <span data-ttu-id="7859b-109">Os consumidores de pacote não percebem nenhuma diferença entre uma conta de usuário ou a conta de organização: ambos aparecem como pacote `owners`.</span><span class="sxs-lookup"><span data-stu-id="7859b-109">Package consumers don't see any difference between an user account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="7859b-110">Uma conta de organização tem uma ou mais contas de usuário como membros.</span><span class="sxs-lookup"><span data-stu-id="7859b-110">An organization account has one or more user accounts as its members.</span></span> <span data-ttu-id="7859b-111">Esses membros podem administrar um conjunto de pacotes, mantendo uma única identidade de propriedade.</span><span class="sxs-lookup"><span data-stu-id="7859b-111">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="7859b-112">Adicionando uma nova organização</span><span class="sxs-lookup"><span data-stu-id="7859b-112">Adding a new organization</span></span>

<span data-ttu-id="7859b-113">Para adicionar uma nova organização, selecione sua conta em nuget.org e selecione o **gerenciar organizações...**  comando de menu:</span><span class="sxs-lookup"><span data-stu-id="7859b-113">To add a new organization, select your account on nuget.org, then select the **Manage Organizations...** menu command:</span></span>

![Opção de menu em nuget.org para organizações Manager](media/org-manage-option.png)

<span data-ttu-id="7859b-115">Na página seguinte, selecione o **adicionar nova organização** botão:</span><span class="sxs-lookup"><span data-stu-id="7859b-115">On the next page, select the **Add new organization** button:</span></span>

![Botão para criar uma nova organização em nuget.org](media/org-add-new-option.png)

<span data-ttu-id="7859b-117">Na próxima página, forneça o endereço de email e o nome da organização.</span><span class="sxs-lookup"><span data-stu-id="7859b-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="7859b-118">Como contas da organização compartilham o mesmo namespace como contas de usuário, o nome da organização deve ser diferente de qualquer organização existente ou contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="7859b-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="7859b-119">O endereço de email também deve ser exclusivo entre todas as contas.</span><span class="sxs-lookup"><span data-stu-id="7859b-119">The email address must also be unique across all accounts.</span></span>

![Adicionar nova página de organização em nuget.org](media/org-add-new-page.png)

<span data-ttu-id="7859b-121">Depois de criar a conta de organização, você é o administrador e pode enviar pacotes para a organização e adicionar membros da organização.</span><span class="sxs-lookup"><span data-stu-id="7859b-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="7859b-122">Transformar a conta existente para uma organização</span><span class="sxs-lookup"><span data-stu-id="7859b-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="7859b-123">Conversão de conta é irreversível: não é possível transformar uma organização para uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="7859b-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="7859b-124">Se você estiver gerenciando pacotes em equipe usando uma conta de usuário único e gostaria de converter essa conta em uma organização, use o **transformar sua conta para uma organização** opção o **gerenciar organizações** página:</span><span class="sxs-lookup"><span data-stu-id="7859b-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Opção em nuget.org para transformar uma conta existente para uma organização](media/org-transform-option.png)

<span data-ttu-id="7859b-126">Na próxima página, especifique outra conta de usuário para atribuir como o administrador da organização, em seguida, selecione **transformação**.</span><span class="sxs-lookup"><span data-stu-id="7859b-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Inserir informações para transformar uma conta de usuário de uma organização](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="7859b-128">Gerenciar os membros da organização</span><span class="sxs-lookup"><span data-stu-id="7859b-128">Managing organization members</span></span>

<span data-ttu-id="7859b-129">Como administrador da organização, você pode adicionar membros, fornecendo a nuget.org cada membro *nome de conta de usuário*; endereços de email não podem ser usados.</span><span class="sxs-lookup"><span data-stu-id="7859b-129">As the organization administrator, you can add members by providing each member's nuget.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="7859b-130">Você, em seguida, marque cada membro como um parceiro ou com as seguintes permissões:</span><span class="sxs-lookup"><span data-stu-id="7859b-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="7859b-131">Permissão</span><span class="sxs-lookup"><span data-stu-id="7859b-131">Permission</span></span> | <span data-ttu-id="7859b-132">Colaborador</span><span class="sxs-lookup"><span data-stu-id="7859b-132">Collaborator</span></span> | <span data-ttu-id="7859b-133">Administrador</span><span class="sxs-lookup"><span data-stu-id="7859b-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7859b-134">Gerenciar pacotes da organização</span><span class="sxs-lookup"><span data-stu-id="7859b-134">Manage the organization's packages</span></span><br/><span data-ttu-id="7859b-135">(Enviar novos pacotes, atualizar ou remover da lista de pacotes existentes)</span><span class="sxs-lookup"><span data-stu-id="7859b-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="7859b-136">Sim</span><span class="sxs-lookup"><span data-stu-id="7859b-136">Yes</span></span> | <span data-ttu-id="7859b-137">Sim</span><span class="sxs-lookup"><span data-stu-id="7859b-137">Yes</span></span> |
| <span data-ttu-id="7859b-138">Metadados de organização de alteração</span><span class="sxs-lookup"><span data-stu-id="7859b-138">Change organization metadata</span></span><br/><span data-ttu-id="7859b-139">(endereço de email, as configurações de notificação)</span><span class="sxs-lookup"><span data-stu-id="7859b-139">(email address, notification settings)</span></span> | <span data-ttu-id="7859b-140">Não</span><span class="sxs-lookup"><span data-stu-id="7859b-140">No</span></span> | <span data-ttu-id="7859b-141">Sim</span><span class="sxs-lookup"><span data-stu-id="7859b-141">Yes</span></span> |
| <span data-ttu-id="7859b-142">Gerenciar membros da organização</span><span class="sxs-lookup"><span data-stu-id="7859b-142">Manage organization members</span></span> | <span data-ttu-id="7859b-143">Não</span><span class="sxs-lookup"><span data-stu-id="7859b-143">No</span></span> | <span data-ttu-id="7859b-144">Sim</span><span class="sxs-lookup"><span data-stu-id="7859b-144">Yes</span></span> |
| <span data-ttu-id="7859b-145">Solicitar ou agir sobre solicitações de co-ownership de pacotes de organização</span><span class="sxs-lookup"><span data-stu-id="7859b-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="7859b-146">Não</span><span class="sxs-lookup"><span data-stu-id="7859b-146">No</span></span> | <span data-ttu-id="7859b-147">Sim</span><span class="sxs-lookup"><span data-stu-id="7859b-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="7859b-148">Gerenciando pacotes</span><span class="sxs-lookup"><span data-stu-id="7859b-148">Managing packages</span></span>

<span data-ttu-id="7859b-149">Você pode exibir todos os pacotes em sua conta e todas as organizações dos quais você é um membro no [gerenciar pacotes](https://www.nuget.org/account/Packages) página.</span><span class="sxs-lookup"><span data-stu-id="7859b-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="7859b-150">Para exibir os pacotes específicos para sua conta ou qualquer organização específica, use o filtro de contas na parte superior direita da página.</span><span class="sxs-lookup"><span data-stu-id="7859b-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Gerenciando pacotes com o filtro de conta](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="7859b-152">Transferência de pacotes para uma organização</span><span class="sxs-lookup"><span data-stu-id="7859b-152">Transferring packages to an organization</span></span>
<span data-ttu-id="7859b-153">Se você deseja transferir alguns de seus pacotes para uma organização criada recentemente, você pode fazer isso solicitando a conta de organização para coproprietário o pacote e, em seguida, remover você mesmo como o proprietário.</span><span class="sxs-lookup"><span data-stu-id="7859b-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="7859b-154">Se você for um administrador da organização, não há nenhuma confirmação precisam aceitar a propriedade.</span><span class="sxs-lookup"><span data-stu-id="7859b-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="7859b-155">No entanto, se você for um colaborador, adicionando a organização como um proprietário requer um dos administradores para aceitar a propriedade.</span><span class="sxs-lookup"><span data-stu-id="7859b-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="7859b-156">Publicando pacotes</span><span class="sxs-lookup"><span data-stu-id="7859b-156">Publishing packages</span></span>

<span data-ttu-id="7859b-157">Publicar pacotes de uma organização que você publicar pacotes em uma conta de usuário: Carregando diretamente o pacote em nuget.org ou enviando o pacote por meio de `nuget push` ou `dotnet nuget push` comandos CLI.</span><span class="sxs-lookup"><span data-stu-id="7859b-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to nuget.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="7859b-158">Carregando pacotes</span><span class="sxs-lookup"><span data-stu-id="7859b-158">Uploading packages</span></span>

<span data-ttu-id="7859b-159">Quando você carrega diretamente um novo pacote no [nuget.org carregamento](https://www.nuget.org/packages/manage/upload) página, você atribui o proprietário do pacote para uma conta de usuário ou a organização:</span><span class="sxs-lookup"><span data-stu-id="7859b-159">When you directly upload a new package on the [nuget.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Carregar pacote com a opção de conta](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="7859b-161">Usando chaves de API</span><span class="sxs-lookup"><span data-stu-id="7859b-161">Using API keys</span></span>

<span data-ttu-id="7859b-162">Para enviar um pacote por meio de `nuget push` ou `dotnet nuget push` comandos CLI, você deve obter uma chave de API necessária por esses comandos.</span><span class="sxs-lookup"><span data-stu-id="7859b-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="7859b-163">Para obter detalhes, consulte [publica um pacote](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="7859b-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="7859b-164">Ao criar uma nova chave de API, selecione a organização apropriada no **proprietário do pacote** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="7859b-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="7859b-165">Qualquer chave de API que você cria é aplicável somente para a organização escolhida:</span><span class="sxs-lookup"><span data-stu-id="7859b-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Chave de API com a opção de conta](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="7859b-167">Remoção de uma organização</span><span class="sxs-lookup"><span data-stu-id="7859b-167">Removing an organization</span></span>

<span data-ttu-id="7859b-168">Como um usuário, você pode remover seu nome de uma organização selecionando o `X` mostrado pela associação de sua organização:</span><span class="sxs-lookup"><span data-stu-id="7859b-168">As a user, you can remove yourself from an organization by selecting the `X` button shown by your organization membership:</span></span>

![Removendo uma conta de usuário de uma organização](media/org-remove-self-option.png)

<span data-ttu-id="7859b-170">Os administradores podem remover qualquer membro da organização, incluindo outros administradores.</span><span class="sxs-lookup"><span data-stu-id="7859b-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="7859b-171">Se você for o único administrador para uma organização, você não pode remover você mesmo, a menos que você adicionar outro membro como um administrador.</span><span class="sxs-lookup"><span data-stu-id="7859b-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="7859b-172">Excluir uma conta de organização</span><span class="sxs-lookup"><span data-stu-id="7859b-172">Deleting an organization account</span></span>

<span data-ttu-id="7859b-173">Este recurso estará disponível em breve.</span><span class="sxs-lookup"><span data-stu-id="7859b-173">This feature is coming soon.</span></span>
