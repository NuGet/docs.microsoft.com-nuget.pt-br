---
title: Como publicar um pacote do NuGet
description: Instruções detalhadas sobre como publicar um pacote do NuGet no nuget.org ou feeds privados e como gerenciar a propriedade de pacote no nuget.org.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 02c6c8f3018bfd063c2d16a10381f88b54cac840
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429020"
---
# <a name="publishing-packages"></a>Publicando pacotes

Após você ter criado um pacote e ter seu arquivo `.nupkg`, é um processo simples disponibilizá-lo para outros desenvolvedores, públicos ou privados:

- Pacotes públicos são disponibilizados para todos os desenvolvedores globalmente por meio do [nuget.org](https://www.nuget.org/packages/manage/upload), conforme descrito neste artigo (requer NuGet 4.1.0 ou posterior).
- Os pacotes privados estão disponíveis apenas para uma equipe ou uma organização hospedando-os em um compartilhamento de arquivo, em um servidor NuGet privado, no [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) ou em um repositório de terceiros, como myget, ProGet, Nexus Repository e Artifactory. Para ver detalhes adicionais, consulte [Visão geral de hospedagem de pacotes](../hosting-packages/overview.md).

Este artigo aborda a publicação no nuget.org. Para saber sobre a publicação no Azure Artifacts, confira [Gerenciamento de pacotes](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Publicar no nuget.org

Para nuget.org, você deve fazer login com uma conta da Microsoft, com a qual você será solicitado a registrar a conta com nuget.org. Você também pode fazer login com uma conta nuget.org criada usando versões mais antigas do portal.

![Localização de entrada do NuGet](media/publish_NuGetSignIn.png)

Em seguida, você poderá carregar o pacote por meio do portal da Web nuget.org, enviar por push ao nuget.org usando a linha de comando (exige `nuget.exe` 4.1.0 ou posterior) ou publicar como parte de um processo de CI/CD por meio do Azure DevOps Services, conforme descrito nas seções a seguir.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Portal da Web: use a guia Carregar Pacote no nuget.org

1. Selecione **Upload** no menu superior de nuget.org e navegue até a localização do pacote.

    ![Carregue um pacote em nuget.org](media/publish_UploadYourPackage.PNG)

1. nuget.org informa se o nome do pacote está disponível. Se não estiver, altere o identificador de pacote no seu projeto, recompile e tente carregar novamente.

1. Se o nome do pacote estiver disponível, nuget.org abrirá uma seção **Verify** (Verificar) em que é possível examinar os metadados do manifesto do pacote. Para alterar os metadados, edite seu projeto (arquivo de projeto ou arquivo `.nuspec`), recompile, recrie o pacote e carregue-o novamente.

1. Em **Import Documentation** (Importar Documentação), você pode colar Markdown, apontar para seus documentos com uma URL ou carregar um arquivo de documentação.

1. Quando todas as informações estiverem prontas, selecione o botão **Submit** (Enviar)

### <a name="command-line"></a>Linha de comando

Para efetuar push em pacotes para o nuget.org, você precisa usar o [nuget.exe v4.1.0 ou superior](https://www.nuget.org/downloads), que implementa os [protocolos NuGet](../api/nuget-protocols.md) necessários. Também é preciso ter uma chave de API, que é criada em nuget.org.

#### <a name="create-api-keys"></a>Criar chaves de API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>Publicar com dotnet nuget push

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>Publicar com nuget push

1. Em um prompt de comando, execute o seguinte comando, substituindo `<your_API_key>` pela chave obtida em nuget.org:

    ```cli
    nuget setApiKey <your_API_key>
    ```

    Este comando armazena sua chave de API na configuração NuGet para que você não precise repetir esse passo novamente no mesmo computador.

    > [!NOTE]
    > A chave API não é usada para autenticar com o feed privado. Consulte o [ `nuget sources` comando](../reference/cli-reference/cli-ref-sources.md) para gerenciar credenciais para autenticação com a fonte.
    > As chaves de API podem ser obtidas dos servidores NuGet individuais. Para criar e manange APIKeys para nuget.org consulte [publish-api-key](../quickstart/includes/publish-api-key.md)

1. Efetue push do pacote para a Galeria do NuGet usando o seguinte comando:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>Publicar pacotes assinados

Para enviar pacotes assinados, primeiro você deve [registrar o certificado](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) usado para assinar os pacotes. 

> [!Warning]
> O nuget.org rejeita os pacotes que não atendem aos [requisitos de pacotes assinados](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).

### <a name="package-validation-and-indexing"></a>Validação e indexação de pacote

Os pacotes enviados por push para nuget.org passam por várias validações, como verificações de vírus. (Todos os pacotes em nuget.org são examinados periodicamente).

Quando o pacote tiver passado todas as verificações de validação, pode levar algum tempo para que ele seja indexado e exibido nos resultados da pesquisa. Após a conclusão da indexação, você receberá um email confirmando que o pacote foi publicado com êxito. Se a verificação de validação do pacote falhar, a página de detalhes do pacote será atualizada para exibir o erro associado e você também receberá uma notificação por email.

A validação e indexação do pacote geralmente leva menos de 15 minutos. Se a publicação do pacote estiver demorando mais do que o esperado, visite [status.nuget.org](https://status.nuget.org/) para verificar se nuget.org está sofrendo interrupções. Se todos os sistemas estiverem operacionais e o pacote não tiver sido publicado com êxito dentro de uma hora, faça logon no nuget.org e entre em contato conosco usando o link Entre em contato com o suporte na página do pacote.

Para ver o status de um pacote, **selecione Gerenciar pacotes** com o nome da sua conta em nuget.org. Você recebe um e-mail de confirmação quando a validação estiver concluída.

Observe que pode levar algum tempo para o pacote ser indexado e aparecer nos resultados da pesquisa em que outras pessoas podem encontrá-lo e, durante esse período, você verá a seguinte mensagem na página do seu pacote:

![Mensagem que indica que um pacote ainda não está publicado](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a>Azure DevOps Services (CI/CD)

Se você enviar pacotes por push ao nuget.org usando os Azure DevOps Services como parte do processo de integração/implantação contínua, será necessário usar o `nuget.exe` 4.1 ou superior nas tarefas do NuGet. Veja mais detalhes em [Usando o NuGet mais recente no seu build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog do Microsoft DevOps).

## <a name="managing-package-owners-on-nugetorg"></a>Gerenciando os proprietários de pacote no nuget.org

Embora cada arquivo `.nuspec` do pacote do NuGet defina os autores do pacote, a galeria do nuget.org não usa metadados para definir a propriedade. Em vez disso, o nuget.org atribui a propriedade inicial à pessoa que publica o pacote. Este é o usuário conectado que carregou o pacote por meio da interface do usuário do nuget.org ou os usuários cuja chave de API foi usada com `nuget SetApiKey` ou `nuget push`.

Todos os proprietários de pacote têm permissões totais para o pacote, incluindo adicionar e remover outros proprietários e publicar atualizações.

Para alterar a propriedade de um pacote, faça o seguinte:

1. Entre em nuget.org com a conta que é o proprietário atual do pacote.
1. Selecione o nome da conta, selecione **Manage packages** (Gerenciar pacotes) e expanda **Published Packages** (Pacotes publicados).
1. Selecione o pacote que você deseja gerenciar e, no lado direito, selecione **Manage owners** (Gerenciar proprietários).

Daqui, você tem várias opções:

1. Remova qualquer proprietário listado em **Current Owners** (Proprietários atuais).
1. Adicione um proprietário em **Add Owner** (Adicionar proprietário) inserindo o nome de usuário dele, uma mensagem e selecionando **Add** (Adicionar). Essa ação envia um email ao novo coproprietário com um link de confirmação. Depois de confirmado, essa pessoa tem permissões completas para adicionar e remover os proprietários. (Até a confirmação, a página **Current Owners** (Proprietários atuais) indica “aprovação pendente” para essa pessoa).
1. Para transferir a propriedade (como quando a propriedade muda ou um pacote foi publicado na conta errada), adicione o novo proprietário e, depois da propriedade ser confirmada, será possível remover você da lista.

Para atribuir a propriedade a uma empresa ou grupo, crie uma conta do nuget.org usando um alias de email que é encaminhado para os membros da equipe apropriada. Por exemplo, vários pacotes do Microsoft ASP.NET são propriedades conjuntas de contas da [microsoft](https://nuget.org/profiles/microsoft) e [aspnet](https://nuget.org/profiles/aspnet), que simplesmente esses aliases.

### <a name="recovering-package-ownership"></a>Recuperar a propriedade do pacote

Ocasionalmente, um pacote pode não ter um proprietário ativo. Por exemplo, o proprietário original deixou a empresa que produz o pacote, as credenciais do nuget.org foram perdidas ou erros anteriores na galeria deixaram pacote sem proprietário.

Se você é o proprietário legítimo de um pacote e precisa recuperar a propriedade, use o [formulário de contato](https://www.nuget.org/policies/Contact) em nuget.org para explicar a situação para a equipe do NuGet. Em seguida, seguimos um processo para confirmar a sua propriedade do pacote, incluindo tentando localizar o proprietário existente por meio da URL do projeto do pacote, Twitter, email ou outros meios. Porém, se tudo o mais falhar, nós podemos lhe enviar um novo convite para se tornar um proprietário.
