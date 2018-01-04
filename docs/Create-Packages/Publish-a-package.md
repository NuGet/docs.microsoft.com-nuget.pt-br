---
title: Como publicar um pacote do NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/5/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2342aabd-983e-4db1-9230-57c84fa36969
description: "Instruções detalhadas sobre como publicar um pacote do NuGet no nuget.org ou feeds privados e como gerenciar a propriedade de pacote no nuget.org."
keywords: "publicação de pacotes do NuGet, publicar pacote do NuGet, propriedade de pacote do NuGet, publicar no nuget.org, feeds do NuGet privados"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: fab25931165afb65aa3fd09c5bc37492ce814a49
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="publishing-packages"></a><span data-ttu-id="f6df2-104">Publicando pacotes</span><span class="sxs-lookup"><span data-stu-id="f6df2-104">Publishing packages</span></span>

<span data-ttu-id="f6df2-105">Após você ter [criado um pacote](../create-packages/creating-a-package.md) com `nuget pack`, é um processo simples disponibilizá-lo para outros desenvolvedores, públicos ou privados:</span><span class="sxs-lookup"><span data-stu-id="f6df2-105">Once you have [created a package](../create-packages/creating-a-package.md) with `nuget pack`, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="f6df2-106">Pacotes públicos são disponibilizados para todos os desenvolvedores globalmente por meio do [nuget.org](https://www.nuget.org/packages/manage/upload), conforme descrito neste tópico.</span><span class="sxs-lookup"><span data-stu-id="f6df2-106">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this topic.</span></span>
- <span data-ttu-id="f6df2-107">Pacotes privados estão disponíveis apenas para uma equipe ou organização e eles são hospedados em um compartilhamento de arquivos, um servidor NuGet privado, no [Gerenciamento de Pacotes do Visual Studio Team Services](https://www.visualstudio.com/docs/package/nuget/publish) ou em um repositório de terceiros, como myget, ProGet, Nexus Repository e Artifactory.</span><span class="sxs-lookup"><span data-stu-id="f6df2-107">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="f6df2-108">Para ver detalhes adicionais, consulte [Visão geral de hospedagem de pacotes](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="f6df2-108">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="f6df2-109">Este tópico abrange a publicação para o nuget.org; para publicar no Visual Studio Team Services, consulte [Gerenciamento de pacotes](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="f6df2-109">This topic covers publishing to nuget.org; for publishing to Visual Studio Team Services, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="f6df2-110">Publicar no nuget.org</span><span class="sxs-lookup"><span data-stu-id="f6df2-110">Publish to nuget.org</span></span>

<span data-ttu-id="f6df2-111">Para nuget.org, primeiro é necessário [registrar-se em uma conta gratuita](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) ou entrar, se já estiver registrado:</span><span class="sxs-lookup"><span data-stu-id="f6df2-111">For nuget.org, you must first [register for a free account](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) or sign in if already registered:</span></span>

![Registro do NuGet e local de entrada](media/publish_NuGetSignIn.png)

<span data-ttu-id="f6df2-113">Em seguida, você pode carregar o pacote por meio do portal da Web nuget.org, efetuar push para nuget.org da linha de comando ou publicar como parte de um processo de CI/CD por meio do Visual Studio Team Services, conforme descrito nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="f6df2-113">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line, or publish as part of a CI/CD process through Visual Studio Team Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="f6df2-114">Portal da Web: use a guia Carregar Pacote no nuget.org:</span><span class="sxs-lookup"><span data-stu-id="f6df2-114">Web portal: use the Upload Package tab on nuget.org:</span></span>

![Carregar um pacote com o Gerenciador de Pacotes do NuGet](media/publish_UploadYourPackage.PNG)

### <a name="command-line"></a><span data-ttu-id="f6df2-116">Linha de comando:</span><span class="sxs-lookup"><span data-stu-id="f6df2-116">Command line:</span></span>
> [!Important]
> <span data-ttu-id="f6df2-117">Para efetuar push em pacotes para o nuget.org, você precisa usar o [nuget.exe v4.1.0 ou superior](https://www.nuget.org/downloads), que implementa os [protocolos NuGet](../api/nuget-protocols.md) necessários.</span><span class="sxs-lookup"><span data-stu-id="f6df2-117">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="f6df2-118">Clique no seu nome de usuário para navegar para suas configurações de conta.</span><span class="sxs-lookup"><span data-stu-id="f6df2-118">Click on your user name to navigate to your account settings.</span></span>
2. <span data-ttu-id="f6df2-119">Na **Chave de API**, clique em **copiar para a área de transferência** para recuperar a chave de acesso que você precisará na CLI:</span><span class="sxs-lookup"><span data-stu-id="f6df2-119">Under **API Key**, click **copy to clipboard** to retrieve the access key you'll need in the CLI:</span></span>

    ![Copiando uma chave de API das configurações de conta](media/publish_APIKey.png)

3. <span data-ttu-id="f6df2-121">No prompt de comando, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="f6df2-121">At a command prompt, run the following command:</span></span>

    ```
    nuget setApiKey Your-API-Key
    ```

    <span data-ttu-id="f6df2-122">Isso armazena a chave de API no computador para que você não precise executar essa etapa novamente no mesmo computador.</span><span class="sxs-lookup"><span data-stu-id="f6df2-122">This stores your API key on the machine so that you need not do this step again on the same machine.</span></span>

4. <span data-ttu-id="f6df2-123">Efetuar push no pacote para a Galeria do NuGet usando o comando:</span><span class="sxs-lookup"><span data-stu-id="f6df2-123">Push your package to NuGet Gallery using the command:</span></span>

    ```
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

5. <span data-ttu-id="f6df2-124">Antes de se tornar público, todos os pacotes carregados para o nuget.org são examinados em busca de vírus e rejeitados caso algum vírus seja encontrado.</span><span class="sxs-lookup"><span data-stu-id="f6df2-124">Before being made public, all packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="f6df2-125">Todos os pacotes listados em nuget.org também são examinados periodicamente.</span><span class="sxs-lookup"><span data-stu-id="f6df2-125">All packages listed on nuget.org are also scanned periodically.</span></span>

6. <span data-ttu-id="f6df2-126">Em sua conta no nuget.org, clique em **Gerenciar meus pacotes** para ver aquele que você acabou de publicar; você também receberá um email de confirmação.</span><span class="sxs-lookup"><span data-stu-id="f6df2-126">In your account on nuget.org, click **Manage my packages** to see the one that you just published; you'll also receive a confirmation email.</span></span> <span data-ttu-id="f6df2-127">Observe que pode levar algum tempo para o pacote ser indexado e aparecer nos resultados da pesquisa em que outras pessoas podem encontrá-lo e, durante esse período, você verá a seguinte mensagem na página do seu pacote:</span><span class="sxs-lookup"><span data-stu-id="f6df2-127">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you'll see the following message on your package page:</span></span>

    ![Mensagem que indica que um pacote ainda não está indexado](media/publish_NotYetIndexed.png)

### <a name="package-validation-and-indexing"></a><span data-ttu-id="f6df2-129">Validação e indexação de pacote</span><span class="sxs-lookup"><span data-stu-id="f6df2-129">Package Validation and Indexing</span></span>

<span data-ttu-id="f6df2-130">Pacotes enviados por push para NuGet.org passam por várias validações.</span><span class="sxs-lookup"><span data-stu-id="f6df2-130">Packages pushed to NuGet.org undergo several validations.</span></span> <span data-ttu-id="f6df2-131">Quando o pacote tiver passado todas as verificações de validação, pode levar algum tempo para que ele seja indexado e exibido nos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f6df2-131">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="f6df2-132">Depois que a indexação estiver concluída, você receberá um email confirmando que o pacote foi publicado com êxito.</span><span class="sxs-lookup"><span data-stu-id="f6df2-132">Once indexing is complete, you'll receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="f6df2-133">Se a verificação de validação do pacote falhar, a página de detalhes do pacote será atualizada para exibir o erro associado e você também receberá um email notificando-o.</span><span class="sxs-lookup"><span data-stu-id="f6df2-133">If the package fails a validation check, the package details page will update to display the associated error and you'll also receive an email notifying you about it.</span></span>

<span data-ttu-id="f6df2-134">A validação e indexação do pacote geralmente leva menos de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="f6df2-134">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="f6df2-135">Se a publicação do pacote estiver demorando mais do que o esperado, visite [status.nuget.org](https://status.nuget.org/) para verificar se o NuGet.org está passando por alguma interrupção.</span><span class="sxs-lookup"><span data-stu-id="f6df2-135">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="f6df2-136">Se todos os sistemas estiverem operacionais e o pacote não tiver sido publicado com êxito dentro de uma hora, faça logon no NuGet.org e entre em contato conosco usando o link Entre em contato com o suporte na página do pacote.</span><span class="sxs-lookup"><span data-stu-id="f6df2-136">If all systems are operational and the package hasn't been successfully published within an hour, please login to NuGet.org and contact us using the Contact Support link on the package page.</span></span>

### <a name="visual-studio-team-services-cicd"></a><span data-ttu-id="f6df2-137">Visual Studio Team Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="f6df2-137">Visual Studio Team Services (CI/CD)</span></span>

<span data-ttu-id="f6df2-138">Se você efetuar push em pacotes para o nuget.org usando o Visual Studio Team Services como parte do processo de Integração/Implantação Contínua, será preciso usar o nuget.exe 4.1 ou superior nas tarefas NuGet.</span><span class="sxs-lookup"><span data-stu-id="f6df2-138">If you push packages to nuget.org using Visual Studio Team Services as part of your Continuous Integration/Deployment process, you must use nuget.exe 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="f6df2-139">Veja mais detalhes em [Usando o NuGet mais recente no seu build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog do Microsoft DevOps).</span><span class="sxs-lookup"><span data-stu-id="f6df2-139">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="f6df2-140">Gerenciando os proprietários de pacote no nuget.org</span><span class="sxs-lookup"><span data-stu-id="f6df2-140">Managing package owners on nuget.org</span></span>

<span data-ttu-id="f6df2-141">Embora cada arquivo `.nuspec` do pacote do NuGet defina os autores do pacote, a galeria do nuget.org não usa metadados para definir a propriedade.</span><span class="sxs-lookup"><span data-stu-id="f6df2-141">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="f6df2-142">Em vez disso, o nuget.org atribui a propriedade inicial à pessoa que publica o pacote.</span><span class="sxs-lookup"><span data-stu-id="f6df2-142">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="f6df2-143">Este é o usuário conectado que carregou o pacote por meio da interface do usuário do nuget.org ou os usuários cuja chave de API foi usada com `nuget SetApiKey` ou `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="f6df2-143">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="f6df2-144">Todos os proprietários de pacote têm permissões totais para o pacote, incluindo adicionar e remover outros proprietários e publicar atualizações.</span><span class="sxs-lookup"><span data-stu-id="f6df2-144">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="f6df2-145">Para alterar a propriedade de um pacote, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f6df2-145">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="f6df2-146">Entre em nuget.org com a conta que é o proprietário atual do pacote.</span><span class="sxs-lookup"><span data-stu-id="f6df2-146">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="f6df2-147">Clique no seu nome de usuário e, em **Gerenciar meus pacotes**, escolha o pacote que você deseja gerenciar.</span><span class="sxs-lookup"><span data-stu-id="f6df2-147">Click on your username, then on **Manage my packages**, then on the package you want to manage.</span></span>
1. <span data-ttu-id="f6df2-148">Clique no link **Gerenciar proprietários** no lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="f6df2-148">Click the **Manage owners** link on the left side.</span></span>

<span data-ttu-id="f6df2-149">Daqui, você tem várias opções:</span><span class="sxs-lookup"><span data-stu-id="f6df2-149">From here you have several options:</span></span>

1. <span data-ttu-id="f6df2-150">Para adicionar um proprietário, digite o nome de conta do NuGet e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f6df2-150">To add an owner, enter their NuGet account name and click **Add**.</span></span> <span data-ttu-id="f6df2-151">Isso envia um email ao novo coproprietário com um link de confirmação.</span><span class="sxs-lookup"><span data-stu-id="f6df2-151">This sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="f6df2-152">Depois de confirmado, essa pessoa tem permissões completas para adicionar e remover os proprietários.</span><span class="sxs-lookup"><span data-stu-id="f6df2-152">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="f6df2-153">(Até que seja confirmado, a página **Gerenciar proprietários** indica “aprovação pendente” para essa pessoa).</span><span class="sxs-lookup"><span data-stu-id="f6df2-153">(Until confirmed, the **Manage owners** page indicates "pending approval" for that person).</span></span>
1. <span data-ttu-id="f6df2-154">Para remover um proprietário, selecione o nome dele em **Gerenciar proprietários** e clique em **Remover**.</span><span class="sxs-lookup"><span data-stu-id="f6df2-154">To remove an owner, select their name on the **Manage owners** and click **Remove**.</span></span>
1. <span data-ttu-id="f6df2-155">Para transferir a propriedade (como quando a propriedade muda ou um pacote foi publicado na conta errada), basta adicionar o novo proprietário e, depois da propriedade ser confirmada, será possível remover você da lista.</span><span class="sxs-lookup"><span data-stu-id="f6df2-155">To transfer ownership (as when ownership changes or a package was published under the wrong account), simply add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="f6df2-156">Para atribuir a propriedade a uma empresa ou grupo, crie uma conta do nuget.org usando um alias de email que é encaminhado para os membros da equipe apropriada.</span><span class="sxs-lookup"><span data-stu-id="f6df2-156">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="f6df2-157">Por exemplo, vários pacotes do Microsoft ASP.NET são propriedades conjuntas de contas da [microsoft](http://nuget.org/profiles/microsoft) e [aspnet](http://nuget.org/profiles/aspnet), que simplesmente esses aliases.</span><span class="sxs-lookup"><span data-stu-id="f6df2-157">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="f6df2-158">Recuperar a propriedade do pacote</span><span class="sxs-lookup"><span data-stu-id="f6df2-158">Recovering package ownership</span></span>

<span data-ttu-id="f6df2-159">Ocasionalmente, um pacote pode não ter um proprietário ativo.</span><span class="sxs-lookup"><span data-stu-id="f6df2-159">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="f6df2-160">Por exemplo, o proprietário original deixou a empresa que produz o pacote, as credenciais do nuget.org foram perdidas ou erros anteriores na galeria deixaram pacote sem proprietário.</span><span class="sxs-lookup"><span data-stu-id="f6df2-160">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="f6df2-161">Se você é o proprietário legítimo de um pacote e precisa recuperar a propriedade, use o [formulário de contato](https://www.nuget.org/policies/Contact) em nuget.org para explicar a situação para a equipe do NuGet.</span><span class="sxs-lookup"><span data-stu-id="f6df2-161">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="f6df2-162">Em seguida, seguimos um processo para confirmar a sua propriedade do pacote, incluindo tentando localizar o proprietário existente por meio da URL do projeto do pacote, Twitter, email ou outros meios.</span><span class="sxs-lookup"><span data-stu-id="f6df2-162">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="f6df2-163">Porém, se tudo o mais falhar, nós podemos lhe enviar um novo convite para se tornar um proprietário.</span><span class="sxs-lookup"><span data-stu-id="f6df2-163">But if all else fails, we can send you a new invite to become an owner.</span></span>
