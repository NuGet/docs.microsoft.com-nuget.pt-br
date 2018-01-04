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
# <a name="publishing-packages"></a>Publicando pacotes

Após você ter [criado um pacote](../create-packages/creating-a-package.md) com `nuget pack`, é um processo simples disponibilizá-lo para outros desenvolvedores, públicos ou privados:

- Pacotes públicos são disponibilizados para todos os desenvolvedores globalmente por meio do [nuget.org](https://www.nuget.org/packages/manage/upload), conforme descrito neste tópico.
- Pacotes privados estão disponíveis apenas para uma equipe ou organização e eles são hospedados em um compartilhamento de arquivos, um servidor NuGet privado, no [Gerenciamento de Pacotes do Visual Studio Team Services](https://www.visualstudio.com/docs/package/nuget/publish) ou em um repositório de terceiros, como myget, ProGet, Nexus Repository e Artifactory. Para ver detalhes adicionais, consulte [Visão geral de hospedagem de pacotes](../hosting-packages/overview.md).

Este tópico abrange a publicação para o nuget.org; para publicar no Visual Studio Team Services, consulte [Gerenciamento de pacotes](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Publicar no nuget.org

Para nuget.org, primeiro é necessário [registrar-se em uma conta gratuita](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) ou entrar, se já estiver registrado:

![Registro do NuGet e local de entrada](media/publish_NuGetSignIn.png)

Em seguida, você pode carregar o pacote por meio do portal da Web nuget.org, efetuar push para nuget.org da linha de comando ou publicar como parte de um processo de CI/CD por meio do Visual Studio Team Services, conforme descrito nas seções a seguir.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Portal da Web: use a guia Carregar Pacote no nuget.org:

![Carregar um pacote com o Gerenciador de Pacotes do NuGet](media/publish_UploadYourPackage.PNG)

### <a name="command-line"></a>Linha de comando:
> [!Important]
> Para efetuar push em pacotes para o nuget.org, você precisa usar o [nuget.exe v4.1.0 ou superior](https://www.nuget.org/downloads), que implementa os [protocolos NuGet](../api/nuget-protocols.md) necessários.

1. Clique no seu nome de usuário para navegar para suas configurações de conta.
2. Na **Chave de API**, clique em **copiar para a área de transferência** para recuperar a chave de acesso que você precisará na CLI:

    ![Copiando uma chave de API das configurações de conta](media/publish_APIKey.png)

3. No prompt de comando, execute o seguinte comando:

    ```
    nuget setApiKey Your-API-Key
    ```

    Isso armazena a chave de API no computador para que você não precise executar essa etapa novamente no mesmo computador.

4. Efetuar push no pacote para a Galeria do NuGet usando o comando:

    ```
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

5. Antes de se tornar público, todos os pacotes carregados para o nuget.org são examinados em busca de vírus e rejeitados caso algum vírus seja encontrado. Todos os pacotes listados em nuget.org também são examinados periodicamente.

6. Em sua conta no nuget.org, clique em **Gerenciar meus pacotes** para ver aquele que você acabou de publicar; você também receberá um email de confirmação. Observe que pode levar algum tempo para o pacote ser indexado e aparecer nos resultados da pesquisa em que outras pessoas podem encontrá-lo e, durante esse período, você verá a seguinte mensagem na página do seu pacote:

    ![Mensagem que indica que um pacote ainda não está indexado](media/publish_NotYetIndexed.png)

### <a name="package-validation-and-indexing"></a>Validação e indexação de pacote

Pacotes enviados por push para NuGet.org passam por várias validações. Quando o pacote tiver passado todas as verificações de validação, pode levar algum tempo para que ele seja indexado e exibido nos resultados da pesquisa. Depois que a indexação estiver concluída, você receberá um email confirmando que o pacote foi publicado com êxito. Se a verificação de validação do pacote falhar, a página de detalhes do pacote será atualizada para exibir o erro associado e você também receberá um email notificando-o.

A validação e indexação do pacote geralmente leva menos de 15 minutos. Se a publicação do pacote estiver demorando mais do que o esperado, visite [status.nuget.org](https://status.nuget.org/) para verificar se o NuGet.org está passando por alguma interrupção. Se todos os sistemas estiverem operacionais e o pacote não tiver sido publicado com êxito dentro de uma hora, faça logon no NuGet.org e entre em contato conosco usando o link Entre em contato com o suporte na página do pacote.

### <a name="visual-studio-team-services-cicd"></a>Visual Studio Team Services (CI/CD)

Se você efetuar push em pacotes para o nuget.org usando o Visual Studio Team Services como parte do processo de Integração/Implantação Contínua, será preciso usar o nuget.exe 4.1 ou superior nas tarefas NuGet. Veja mais detalhes em [Usando o NuGet mais recente no seu build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog do Microsoft DevOps).

## <a name="managing-package-owners-on-nugetorg"></a>Gerenciando os proprietários de pacote no nuget.org

Embora cada arquivo `.nuspec` do pacote do NuGet defina os autores do pacote, a galeria do nuget.org não usa metadados para definir a propriedade. Em vez disso, o nuget.org atribui a propriedade inicial à pessoa que publica o pacote. Este é o usuário conectado que carregou o pacote por meio da interface do usuário do nuget.org ou os usuários cuja chave de API foi usada com `nuget SetApiKey` ou `nuget push`.

Todos os proprietários de pacote têm permissões totais para o pacote, incluindo adicionar e remover outros proprietários e publicar atualizações.

Para alterar a propriedade de um pacote, faça o seguinte:

1. Entre em nuget.org com a conta que é o proprietário atual do pacote.
1. Clique no seu nome de usuário e, em **Gerenciar meus pacotes**, escolha o pacote que você deseja gerenciar.
1. Clique no link **Gerenciar proprietários** no lado esquerdo.

Daqui, você tem várias opções:

1. Para adicionar um proprietário, digite o nome de conta do NuGet e clique em **Adicionar**. Isso envia um email ao novo coproprietário com um link de confirmação. Depois de confirmado, essa pessoa tem permissões completas para adicionar e remover os proprietários. (Até que seja confirmado, a página **Gerenciar proprietários** indica “aprovação pendente” para essa pessoa).
1. Para remover um proprietário, selecione o nome dele em **Gerenciar proprietários** e clique em **Remover**.
1. Para transferir a propriedade (como quando a propriedade muda ou um pacote foi publicado na conta errada), basta adicionar o novo proprietário e, depois da propriedade ser confirmada, será possível remover você da lista.

Para atribuir a propriedade a uma empresa ou grupo, crie uma conta do nuget.org usando um alias de email que é encaminhado para os membros da equipe apropriada. Por exemplo, vários pacotes do Microsoft ASP.NET são propriedades conjuntas de contas da [microsoft](http://nuget.org/profiles/microsoft) e [aspnet](http://nuget.org/profiles/aspnet), que simplesmente esses aliases.

### <a name="recovering-package-ownership"></a>Recuperar a propriedade do pacote

Ocasionalmente, um pacote pode não ter um proprietário ativo. Por exemplo, o proprietário original deixou a empresa que produz o pacote, as credenciais do nuget.org foram perdidas ou erros anteriores na galeria deixaram pacote sem proprietário.

Se você é o proprietário legítimo de um pacote e precisa recuperar a propriedade, use o [formulário de contato](https://www.nuget.org/policies/Contact) em nuget.org para explicar a situação para a equipe do NuGet. Em seguida, seguimos um processo para confirmar a sua propriedade do pacote, incluindo tentando localizar o proprietário existente por meio da URL do projeto do pacote, Twitter, email ou outros meios. Porém, se tudo o mais falhar, nós podemos lhe enviar um novo convite para se tornar um proprietário.
