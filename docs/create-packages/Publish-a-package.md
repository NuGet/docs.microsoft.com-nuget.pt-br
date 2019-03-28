---
title: Como publicar um pacote do NuGet
description: Instruções detalhadas sobre como publicar um pacote do NuGet no nuget.org ou feeds privados e como gerenciar a propriedade de pacote no nuget.org.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 6d183100a8319b517347567f34d276e94eb4e15d
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432537"
---
# <a name="publishing-packages"></a><span data-ttu-id="59cde-103">Publicando pacotes</span><span class="sxs-lookup"><span data-stu-id="59cde-103">Publishing packages</span></span>

<span data-ttu-id="59cde-104">Após você ter criado um pacote e ter seu arquivo `.nupkg`, é um processo simples disponibilizá-lo para outros desenvolvedores, públicos ou privados:</span><span class="sxs-lookup"><span data-stu-id="59cde-104">Once you have created a package and have your `.nupkg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="59cde-105">Pacotes públicos são disponibilizados para todos os desenvolvedores globalmente por meio do [nuget.org](https://www.nuget.org/packages/manage/upload), conforme descrito neste artigo (requer NuGet 4.1.0 ou posterior).</span><span class="sxs-lookup"><span data-stu-id="59cde-105">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="59cde-106">Os pacotes privados estão disponíveis apenas para uma equipe ou uma organização hospedando-os em um compartilhamento de arquivo, em um servidor NuGet privado, no [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) ou em um repositório de terceiros, como myget, ProGet, Nexus Repository e Artifactory.</span><span class="sxs-lookup"><span data-stu-id="59cde-106">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="59cde-107">Para ver detalhes adicionais, consulte [Visão geral de hospedagem de pacotes](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="59cde-107">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="59cde-108">Este artigo aborda a publicação no nuget.org. Para saber sobre a publicação no Azure Artifacts, confira [Gerenciamento de pacotes](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="59cde-108">This article covers publishing to nuget.org; for publishing to Azure Artifacts, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="59cde-109">Publicar no nuget.org</span><span class="sxs-lookup"><span data-stu-id="59cde-109">Publish to nuget.org</span></span>

<span data-ttu-id="59cde-110">No nuget.org, entre com uma conta da Microsoft. Será solicitado que você registre essa conta em nuget.org. Você também pode entrar com uma conta de nuget.org criada com versões mais antigas do portal.</span><span class="sxs-lookup"><span data-stu-id="59cde-110">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![Localização de entrada do NuGet](media/publish_NuGetSignIn.png)

<span data-ttu-id="59cde-112">Em seguida, você poderá carregar o pacote por meio do portal da Web nuget.org, enviar por push ao nuget.org usando a linha de comando (exige `nuget.exe` 4.1.0 ou posterior) ou publicar como parte de um processo de CI/CD por meio do Azure DevOps Services, conforme descrito nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="59cde-112">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Azure DevOps Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="59cde-113">Portal da Web: use a guia Carregar Pacote no nuget.org</span><span class="sxs-lookup"><span data-stu-id="59cde-113">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="59cde-114">Selecione **Upload** no menu superior de nuget.org e navegue até a localização do pacote.</span><span class="sxs-lookup"><span data-stu-id="59cde-114">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![Carregue um pacote em nuget.org](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="59cde-116">nuget.org informa se o nome do pacote está disponível.</span><span class="sxs-lookup"><span data-stu-id="59cde-116">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="59cde-117">Se não estiver, altere o identificador de pacote no seu projeto, recompile e tente carregar novamente.</span><span class="sxs-lookup"><span data-stu-id="59cde-117">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="59cde-118">Se o nome do pacote estiver disponível, nuget.org abrirá uma seção **Verify** (Verificar) em que é possível examinar os metadados do manifesto do pacote.</span><span class="sxs-lookup"><span data-stu-id="59cde-118">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="59cde-119">Para alterar os metadados, edite seu projeto (arquivo de projeto ou arquivo `.nuspec`), recompile, recrie o pacote e carregue-o novamente.</span><span class="sxs-lookup"><span data-stu-id="59cde-119">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="59cde-120">Em **Import Documentation** (Importar Documentação), você pode colar Markdown, apontar para seus documentos com uma URL ou carregar um arquivo de documentação.</span><span class="sxs-lookup"><span data-stu-id="59cde-120">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="59cde-121">Quando todas as informações estiverem prontas, selecione o botão **Submit** (Enviar)</span><span class="sxs-lookup"><span data-stu-id="59cde-121">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="59cde-122">Linha de comando</span><span class="sxs-lookup"><span data-stu-id="59cde-122">Command line</span></span>

<span data-ttu-id="59cde-123">Para efetuar push em pacotes para o nuget.org, você precisa usar o [nuget.exe v4.1.0 ou superior](https://www.nuget.org/downloads), que implementa os [protocolos NuGet](../api/nuget-protocols.md) necessários.</span><span class="sxs-lookup"><span data-stu-id="59cde-123">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="59cde-124">Também é preciso ter uma chave de API, que é criada em nuget.org.</span><span class="sxs-lookup"><span data-stu-id="59cde-124">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="59cde-125">Criar chaves de API</span><span class="sxs-lookup"><span data-stu-id="59cde-125">Create API keys</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="59cde-126">Publicar com dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="59cde-126">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="59cde-127">Publicar com nuget push</span><span class="sxs-lookup"><span data-stu-id="59cde-127">Publish with nuget push</span></span>

1. <span data-ttu-id="59cde-128">Em um prompt de comando, execute o seguinte comando, substituindo `<your_API_key>` pela chave obtida em nuget.org:</span><span class="sxs-lookup"><span data-stu-id="59cde-128">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="59cde-129">Esse comando armazena a chave de API em sua configuração do NuGet para que você não precise repetir essa etapa novamente no mesmo computador.</span><span class="sxs-lookup"><span data-stu-id="59cde-129">This command stores your API key in your NuGet configuration so that you need repeat this step again on the same computer.</span></span>

1. <span data-ttu-id="59cde-130">Efetue push do pacote para a Galeria do NuGet usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="59cde-130">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a><span data-ttu-id="59cde-131">Publicar pacotes assinados</span><span class="sxs-lookup"><span data-stu-id="59cde-131">Publish signed packages</span></span>

<span data-ttu-id="59cde-132">Para enviar pacotes assinados, primeiro você deve [registrar o certificado](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) usado para assinar os pacotes.</span><span class="sxs-lookup"><span data-stu-id="59cde-132">To submit signed packages, you must first [register the certificate](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) used for signing the packages.</span></span> 

> [!Warning]
> <span data-ttu-id="59cde-133">O nuget.org rejeita os pacotes que não atendem aos [requisitos de pacotes assinados](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="59cde-133">nuget.org rejects packages that don't satisfy the [signed package requirements](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span></span>

### <a name="package-validation-and-indexing"></a><span data-ttu-id="59cde-134">Validação e indexação de pacote</span><span class="sxs-lookup"><span data-stu-id="59cde-134">Package validation and indexing</span></span>

<span data-ttu-id="59cde-135">Os pacotes enviados por push para nuget.org passam por várias validações, como verificações de vírus.</span><span class="sxs-lookup"><span data-stu-id="59cde-135">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="59cde-136">(Todos os pacotes em nuget.org são examinados periodicamente).</span><span class="sxs-lookup"><span data-stu-id="59cde-136">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="59cde-137">Quando o pacote tiver passado todas as verificações de validação, pode levar algum tempo para que ele seja indexado e exibido nos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="59cde-137">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="59cde-138">Após a conclusão da indexação, você receberá um email confirmando que o pacote foi publicado com êxito.</span><span class="sxs-lookup"><span data-stu-id="59cde-138">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="59cde-139">Se a verificação de validação do pacote falhar, a página de detalhes do pacote será atualizada para exibir o erro associado e você também receberá uma notificação por email.</span><span class="sxs-lookup"><span data-stu-id="59cde-139">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="59cde-140">A validação e indexação do pacote geralmente leva menos de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="59cde-140">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="59cde-141">Se a publicação do pacote estiver demorando mais do que o esperado, visite [status.nuget.org](https://status.nuget.org/) para verificar se o nuget.org está passando por alguma interrupção.</span><span class="sxs-lookup"><span data-stu-id="59cde-141">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="59cde-142">Se todos os sistemas estiverem operacionais e o pacote não tiver sido publicado com êxito dentro de uma hora, faça logon no nuget.org e entre em contato conosco usando o link Entre em contato com o suporte na página do pacote.</span><span class="sxs-lookup"><span data-stu-id="59cde-142">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="59cde-143">Para ver o status de um pacote, selecione **Manage packages** (Gerenciar pacotes) em seu nome de conta em nuget.org. Quando a validação estiver concluída, você receberá um email de confirmação.</span><span class="sxs-lookup"><span data-stu-id="59cde-143">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="59cde-144">Observe que pode levar algum tempo para o pacote ser indexado e aparecer nos resultados da pesquisa em que outras pessoas podem encontrá-lo e, durante esse período, você verá a seguinte mensagem na página do seu pacote:</span><span class="sxs-lookup"><span data-stu-id="59cde-144">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![Mensagem que indica que um pacote ainda não está publicado](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a><span data-ttu-id="59cde-146">Azure DevOps Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="59cde-146">Azure DevOps Services (CI/CD)</span></span>

<span data-ttu-id="59cde-147">Se você enviar pacotes por push ao nuget.org usando os Azure DevOps Services como parte do processo de integração/implantação contínua, será necessário usar o `nuget.exe` 4.1 ou superior nas tarefas do NuGet.</span><span class="sxs-lookup"><span data-stu-id="59cde-147">If you push packages to nuget.org using Azure DevOps Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="59cde-148">Veja mais detalhes em [Usando o NuGet mais recente no seu build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog do Microsoft DevOps).</span><span class="sxs-lookup"><span data-stu-id="59cde-148">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="59cde-149">Gerenciando os proprietários de pacote no nuget.org</span><span class="sxs-lookup"><span data-stu-id="59cde-149">Managing package owners on nuget.org</span></span>

<span data-ttu-id="59cde-150">Embora cada arquivo `.nuspec` do pacote do NuGet defina os autores do pacote, a galeria do nuget.org não usa metadados para definir a propriedade.</span><span class="sxs-lookup"><span data-stu-id="59cde-150">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="59cde-151">Em vez disso, o nuget.org atribui a propriedade inicial à pessoa que publica o pacote.</span><span class="sxs-lookup"><span data-stu-id="59cde-151">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="59cde-152">Este é o usuário conectado que carregou o pacote por meio da interface do usuário do nuget.org ou os usuários cuja chave de API foi usada com `nuget SetApiKey` ou `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="59cde-152">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="59cde-153">Todos os proprietários de pacote têm permissões totais para o pacote, incluindo adicionar e remover outros proprietários e publicar atualizações.</span><span class="sxs-lookup"><span data-stu-id="59cde-153">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="59cde-154">Para alterar a propriedade de um pacote, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="59cde-154">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="59cde-155">Entre em nuget.org com a conta que é o proprietário atual do pacote.</span><span class="sxs-lookup"><span data-stu-id="59cde-155">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="59cde-156">Selecione o nome da conta, selecione **Manage packages** (Gerenciar pacotes) e expanda **Published Packages** (Pacotes publicados).</span><span class="sxs-lookup"><span data-stu-id="59cde-156">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="59cde-157">Selecione o pacote que você deseja gerenciar e, no lado direito, selecione **Manage owners** (Gerenciar proprietários).</span><span class="sxs-lookup"><span data-stu-id="59cde-157">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="59cde-158">Daqui, você tem várias opções:</span><span class="sxs-lookup"><span data-stu-id="59cde-158">From here you have several options:</span></span>

1. <span data-ttu-id="59cde-159">Remova qualquer proprietário listado em **Current Owners** (Proprietários atuais).</span><span class="sxs-lookup"><span data-stu-id="59cde-159">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="59cde-160">Adicione um proprietário em **Add Owner** (Adicionar proprietário) inserindo o nome de usuário dele, uma mensagem e selecionando **Add** (Adicionar).</span><span class="sxs-lookup"><span data-stu-id="59cde-160">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="59cde-161">Essa ação envia um email ao novo coproprietário com um link de confirmação.</span><span class="sxs-lookup"><span data-stu-id="59cde-161">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="59cde-162">Depois de confirmado, essa pessoa tem permissões completas para adicionar e remover os proprietários.</span><span class="sxs-lookup"><span data-stu-id="59cde-162">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="59cde-163">(Até a confirmação, a página **Current Owners** (Proprietários atuais) indica “aprovação pendente” para essa pessoa).</span><span class="sxs-lookup"><span data-stu-id="59cde-163">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="59cde-164">Para transferir a propriedade (como quando a propriedade muda ou um pacote foi publicado na conta errada), adicione o novo proprietário e, depois da propriedade ser confirmada, será possível remover você da lista.</span><span class="sxs-lookup"><span data-stu-id="59cde-164">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="59cde-165">Para atribuir a propriedade a uma empresa ou grupo, crie uma conta do nuget.org usando um alias de email que é encaminhado para os membros da equipe apropriada.</span><span class="sxs-lookup"><span data-stu-id="59cde-165">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="59cde-166">Por exemplo, vários pacotes do Microsoft ASP.NET são propriedades conjuntas de contas da [microsoft](http://nuget.org/profiles/microsoft) e [aspnet](http://nuget.org/profiles/aspnet), que simplesmente esses aliases.</span><span class="sxs-lookup"><span data-stu-id="59cde-166">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="59cde-167">Recuperar a propriedade do pacote</span><span class="sxs-lookup"><span data-stu-id="59cde-167">Recovering package ownership</span></span>

<span data-ttu-id="59cde-168">Ocasionalmente, um pacote pode não ter um proprietário ativo.</span><span class="sxs-lookup"><span data-stu-id="59cde-168">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="59cde-169">Por exemplo, o proprietário original deixou a empresa que produz o pacote, as credenciais do nuget.org foram perdidas ou erros anteriores na galeria deixaram pacote sem proprietário.</span><span class="sxs-lookup"><span data-stu-id="59cde-169">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="59cde-170">Se você é o proprietário legítimo de um pacote e precisa recuperar a propriedade, use o [formulário de contato](https://www.nuget.org/policies/Contact) em nuget.org para explicar a situação para a equipe do NuGet.</span><span class="sxs-lookup"><span data-stu-id="59cde-170">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="59cde-171">Em seguida, seguimos um processo para confirmar a sua propriedade do pacote, incluindo tentando localizar o proprietário existente por meio da URL do projeto do pacote, Twitter, email ou outros meios.</span><span class="sxs-lookup"><span data-stu-id="59cde-171">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="59cde-172">Porém, se tudo o mais falhar, nós podemos lhe enviar um novo convite para se tornar um proprietário.</span><span class="sxs-lookup"><span data-stu-id="59cde-172">But if all else fails, we can send you a new invite to become an owner.</span></span>
