---
title: Perguntas frequentes do NuGet
description: Perguntas e respostas comuns sobre usar o NuGet na linha de comando e no Visual Studio e trabalhar com a Galeria do NuGet.
author: shishirx34
ms.author: shishirh
ms.date: 01/15/2019
ms.topic: conceptual
ms.openlocfilehash: f15639c883241c328b5fc0a4bf5617540b52b7ee
ms.sourcegitcommit: d5a35a097e6b461ae791d9f66b3a85d5219d7305
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56145677"
---
# <a name="nuget-frequently-asked-questions"></a>Perguntas frequentes do NuGet

**O que é necessário para executar o NuGet?**

Todas as informações sobre a interface do usuário e as ferramentas de linha de comando estão disponíveis na [Guia de instalação](../install-nuget-client-tools.md).

**O NuGet é compatível com o Mono?**

A ferramenta de linha de comando, `nuget.exe`, compila e executa em Mono 3.2 e superior, e pode criar pacotes em Mono.

Embora `nuget.exe` funcione completamente no Windows, existem alguns problemas conhecidos no Linux e no OS X. Consulte [Problemas do Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) no GitHub.

Um [cliente gráfico](https://github.com/mrward/monodevelop-nuget-addin) está disponível como um suplemento para MonoDevelop.

**Como fazer para determinar o que um pacote contém e se ele é estável e útil para meu aplicativo?**

A origem primária para aprender sobre um pacote é a página de listagem em nuget.org (ou outro feed privado). Cada página do pacote em nuget.org inclui uma descrição do pacote, seu histórico de versão e as estatísticas de uso. A seção **Informações** na página do pacote também contém um link para o site da Web do projeto em que você normalmente encontrar muitos exemplos e documentação para ajudá-lo a aprender como o pacote é usado.

Para obter mais informações, consulte [Localizando e escolhendo pacotes](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>NuGet no Visual Studio

**Como é a compatibilidade do NuGet com os diferentes produtos do Visual Studio?**

- O Visual Studio no Windows é compatível com a [Interface do usuário do Gerenciador de Pacotes](../tools/package-manager-ui.md) e o [Console do Gerenciador de Pacotes](../tools/package-manager-console.md).
- O Visual Studio para Mac tem recursos internos do NuGet, conforme descrito em [Incluindo um pacote do NuGet em seu projeto](/visualstudio/mac/nuget-walkthrough).
- O Visual Studio Code (todas as plataformas) não tem nenhuma integração direta do NuGet. Usar a [CLI do NuGet](../tools/nuget-exe-cli-reference.md) ou a [CLI do dotnet](../tools/dotnet-commands.md).
- O Azure DevOps fornece [uma etapa de build para restaurar os pacotes do NuGet](/vsts/build-release/tasks/package/nuget). Você também pode [hospedar feeds privados de pacote do NuGet no Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).

**Como fazer para verificar a versão exata das ferramentas do NuGet que estão instaladas?**

No Visual Studio, use o comando **Ajuda > Sobre o Microsoft Visual Studio** e examine a versão exibida ao lado de **Gerenciador de Pacotes do NuGet**.

Como alternativa, inicie o Console do Gerenciador de Pacotes (**Ferramentas > Gerenciador de Pacotes do NuGet > Console do Gerenciador de Pacotes**) e digite `$host` para ver informações sobre o NuGet, incluindo a versão.

**Quais linguagens de programação são compatíveis com o NuGet?**

O NuGet geralmente funciona para linguagens .NET e foi projetado para trazer bibliotecas .NET em um projeto. Como também há suporte para a automação do MSBuild e do Visual Studio em alguns tipos de projeto, também há suporte para outros projetos e idiomas em diversos níveis.

A versão mais recente do NuGet é compatível com C#, Visual Basic, F#, WiX e C++.

**Quais modelos de projeto são compatíveis com o NuGet?**

O NuGet tem suporte completo para uma variedade de modelos de projeto como Windows, Web, Cloud, SharePoint, Wix e assim por diante.

**Como fazer para atualizar pacotes que fazem parte dos modelos do Visual Studio?**

Acesse a guia **Atualizações** na interface do usuário do Gerenciador de Pacotes e selecione **Atualizar tudo** [ou use o comando `Update-Package`](../tools/ps-ref-update-package.md) do Console do Gerenciador de Pacotes.

Para atualizar o próprio modelo, você precisa atualizar manualmente o repositório de modelos. Consulte o [blog de Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) sobre este assunto. Observe que isso é feito por seu próprio risco, pois atualizações manuais podem corromper o modelo se a versão mais recente de todas as dependências não forem compatível entre si.

**Posso usar o NuGet fora do Visual Studio?**

Sim, o NuGet funciona diretamente da linha de comando. Consulte o [Guia de instalação](../install-nuget-client-tools.md) e a [CLI de referência](../tools/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>Linha de comando do NuGet

**Como fazer para obter a versão mais recente da ferramenta de linha de comando do NuGet?**

Consulte o [Guia de instalação](../install-nuget-client-tools.md).

**O que é a licença para nuget.exe?**

Você pode redistribuir o nuget.exe sob os termos da licença do MIT. Você é responsável pela atualização e manutenção das cópias do nuget.exe que você escolhe redistribuir.

**É possível estender a ferramenta de linha de comando do NuGet?**

Sim, é possível adicionar comandos personalizados para `nuget.exe`, conforme descrito na [postagem de Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>Console do Gerenciador de Pacotes do NuGet (Visual Studio no Windows)

**Como fazer para obter acesso ao objeto DTE no console do Gerenciador de Pacotes?**

O objeto de nível superior no modelo de objeto de automação do Visual Studio é chamado o objeto DTE (Ambiente de Ferramentas de Desenvolvimento). O console fornece isso por meio de uma variável chamada `$DTE`. Para obter mais informações, consulte [Visão geral do modelo de automação](/visualstudio/extensibility/internals/automation-model-overview) na documentação de Extensibilidade do Visual Studio.

**Tento converter a variável $DTE para o tipo DTE2, mas eu recebo um erro: Não é possível converter o valor de "EnvDTE.DTEClass" do tipo "EnvDTE.DTEClass" para o tipo "EnvDTE80.DTE2". Qual é o problema?**

Este é um problema conhecido em como o PowerShell interage com um objeto COM. Experimente o seguinte:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` é uma função auxiliar adicionada pelo host do NuGet PowerShell.

## <a name="creating-and-publishing-packages"></a>Criar e publicar pacotes

**Como fazer para listar meu pacote em um feed?**

Consulte [Criar e publicar um pacote](../quickstart/create-and-publish-a-package.md).

**Tenho várias versões da minha biblioteca que usam versões diferentes do .NET Framework. Como fazer para compilar um único pacote compatível com isso?**

Consulte [Suporte a várias versões e perfis do .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).

**Como fazer para configurar meu próprio repositório ou feed?**

Consulte a [Visão geral de hospedagem de pacotes](../hosting-packages/overview.md).

**Como posso carregar pacotes para meu feed do NuGet em massa?**

Consulte [Publicação de pacotes do NuGet em massa](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).

## <a name="working-with-packages"></a>Trabalhando com pacotes

**Qual é a diferença entre um pacote de nível de projeto e um pacote de nível de solução?**

Um pacote de nível de solução (NuGet 3.x ou superior) é instalado apenas uma vez em uma solução e fica disponível para todos os projetos na solução. Um pacote de nível de projeto está instalado em cada projeto que o utiliza. Um pacote de nível de solução também pode instalar novos comandos que podem ser chamados de dentro do Console do Gerenciador de Pacotes.

**É possível instalar os pacotes do NuGet sem conectividade com a Internet?**

Sim, consulte a postagem no blog de Scott Hanselman [How to access NuGet when nuget.org is down (or you're on a plane) [Como acessar o NuGet quando o nuget.org estiver inativo (ou você estiver a bordo de um avião)]](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).

**Como fazer para instalar pacotes em um local diferente da pasta de pacotes padrão?**

Defina a configuração [`repositoryPath`](../reference/nuget-config-file.md#config-section) em `Nuget.Config` usando `nuget config -set repositoryPath=<path>`.

**Como evitar adicionar a pasta de pacotes do NuGet ao controle do código-fonte?**

Defina o [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) em `Nuget.Config` para `true`. Essa chave funciona no nível da solução e, portanto, precisa ser adicionada ao arquivo `$(Solutiondir)\.nuget\Nuget.Config`. Habilitando a restauração do pacote do Visual Studio cria esse arquivo automaticamente.

**Como fazer para desligar a restauração do pacote?**

Consulte [Habilitar e desabilitar a restauração de pacote](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

**Por que recebo um “Não é possível resolver o erro de dependência” ao instalar um pacote local com dependências remotas?**

Você precisa selecionar a origem **Todos** ao instalar um pacote local para o projeto. Isso agrega todos os feeds em vez de usar apenas um. O motivo pelo qual este erro ocorre é que os usuários de um repositório local geralmente desejam evitar instalar acidentalmente um pacote remoto devido a políticas corporativa.

**Tenho vários projetos na mesma pasta, como posso usar arquivos packages.config separados para cada projeto?**

Na maioria dos projetos em que projetos separados residem em pastas separadas, isso não é um problema, pois o NuGet identifica os arquivos `packages.config` em cada projeto. Com o NuGet 3.3 e superior, e com vários projetos na mesma pasta, você pode inserir o nome do projeto nos nomes de arquivo `packages.config` que usam o padrão `packages.{project-name}.config` e o NuGet usará esse arquivo.

Isso não é um problema ao usar PackageReference, pois cada arquivo de projeto contém sua própria lista de dependências.

**Não vejo o nuget.org na minha lista de repositórios, como faço para obtê-lo novamente?**

- Adicione `https://api.nuget.org/v3/index.json` à lista de fontes ou
- Exclua `%appdata%\.nuget\NuGet.Config` (Windows) ou `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) e deixe o NuGet recriá-lo.

**Quais são os termos de licença padrão se um pacote não fornecer informações de licença específicas?**

Cada pacote é regido pelos termos incluídos no pacote. Você deve examinar os termos aplicáveis antes de acessar, baixar ou adquirir os pacotes. Em nuget.org, use o link **Informações de Licença** na página do pacote.

Se um pacote não especificar os termos de licença, entre em contato com o proprietário do pacote diretamente usando o link **Contatar os proprietários** na página do pacote em nuget.org. A Microsoft não licencia nenhuma propriedade intelectual para você de provedores de pacotes de terceiros, nem é responsável pelas informações fornecidas por terceiros.

## <a name="managing-packages-on-nugetorg"></a>Gerenciando pacotes em nuget.org

**Posso editar os metadados do pacote depois que ele é carregado?**

O NuGet recomenda que todos os pacotes sejam assinados. Um princípio de design da assinatura de pacote é que o conteúdo do pacote assinado deve ser imutável, que inclui o nuspec. Editar os resultados de metadados de pacote em alterações de nuspec, invalidando assinaturas existentes. É recomendável modificar fluxos de trabalho existentes para não exigir a edição dos metadados do pacote depois que o este foi criado.

Observe que as dependências listadas para seu pacote são geradas automaticamente do próprio pacote e não podem ser editadas.

Além disso, carregar pacotes para [int.nugettest.org](https://int.nugettest.org) é uma ótima maneira de testar e validar seu pacote sem disponibilizá-lo na galeria pública.

**É possível reservar nomes para os pacotes que serão publicados no futuro?**

Sim. Você pode reservar IDs para os pacotes em [nuget.org](https://www.nuget.org/) solicitando um prefixo de ID de pacote para a sua conta. Para solicitar um prefixo da ID do pacote, siga as instruções na [documentação](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).

**Como fazer para declarar a propriedade de pacotes?**

Consulte [Gerenciando os proprietários de pacote no nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).

**Como fazer para lidar com um proprietário de pacote que está violando minha licença de software?**

Estimulamos a comunidade do NuGet para trabalhar juntos para resolver as controvérsias que podem surgir entre os proprietários do pacote e os proprietários de outro software. Criamos um [processo de solução de controvérsias](../policies/dispute-resolution.md) que deve ser seguido antes de solicitar a intervenção dos administradores do nuget.org.

**É recomendável carregar pacotes meu teste para o nuget.org?**

Para fins de teste, você pode usar [int.nugettest.org](https://int.nugettest.org) ou os servidores NuGet públicos alternativos como [myget.org](https://myget.org) ou [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Observe que os pacotes carregados para o int.nugettest.org podem não ser preservados.

**Qual é o tamanho máximo dos pacotes que posso carregar para o nuget.org?**

O nuget.org permite usar pacotes com até 250 MB, mas é recomendável manter os pacotes abaixo de 1 MB se possível e usar as dependências para unir pacotes. Como regra geral, os pacotes contêm apenas um assembly para evitar colisões.

O NuGet usa HTTP para baixar os pacotes, por isso pacotes maiores têm maior probabilidade de apresentar falha na instalação do que os menores.

É possível compartilhar as dependências entre vários pacotes, reduzindo o tamanho total do download para os consumidores de seus pacotes do NuGet.

As dependências são principalmente estáticas e nunca mudam. Ao corrigir um bug no código, as dependências não precisarão ser atualizadas. Se você agrupar dependências, pacotes cada vez maiores são distribuídos a cada vez. Dividir os pacotes do NuGet em dependências relacionadas torna os upgrades muito mais refinados para os consumidores do seu pacote.

## <a name="nugetorg-not-accessible"></a>O nuget.org não está acessível

**Por que não é possível baixar ou carregar pacotes para o nuget.org?**

Primeiro, verifique se que você está usando as versões mais recentes do NuGet. Se essa versão continuar falhando, [entre em contato com o suporte](https://www.nuget.org/policies/Contact) e forneça as informações de solução de problemas de conexão adicionais, incluindo:

- A versão do NuGet que você está usando
- As origens de pacote que você está usando
- Um log de restauração detalhado
- MTR ou um rastreamento do Fiddler (veja abaixo)
- Sua área geográfica
- Se seu computador está por trás de um proxy ou firewall?
- Se seu computador está localizado no data center dos provedores de nuvem (Azure, AWS etc.)? Se sim, forneça o nome do provedor e a região.

*Para capturar MTR:*

- Baixe o WinMTR em [http://winmtr.net/download/](http://winmtr.net/)
- Digite `api.nuget.org` como o nome do host e clique em **Iniciar**.
- Aguarde até a coluna **Sent** ser >= 100.

    ![Capturando MTR](media/mtr.png)

- Copie texto para a área de transferência.

*Para capturar o Fiddler:*

- Instale a versão mais recente do [Fiddler](http://www.telerik.com/download/fiddler).
- Inicie o Fiddler e desabilite a captura de tráfego usando o menu **Arquivo > Capturar tráfego**.
- Remova todas as sessões (selecione todos os itens na lista, pressione a tecla **Delete**).
- Configure o Fiddler para capturar o tráfego HTTPS marcando **Descriptografar tráfego HTTPS** na guia **HTTPS** do menu **Ferramentas > Opções do Fiddler...**.
- Feche o Visual Studio.
- Habilitar o menu **Arquivo > Capturar Tráfego**.
- Inicie o Visual Studio ou .exe do nuget.exe e execute as ações que não estão funcionando. O tráfego gerado por essas ações deve ser exibido no Fiddler.
- Depois das ações serem executadas, use **Arquivo > Salvar > Todas as sessões** para armazenar as sessões capturadas.

Observação: pode ser necessário definir a variável de ambiente `HTTP_PROXY` para `http://127.0.0.1:8888` para rotear o tráfego do NuGet através do Fiddler.

Se isso falhar, experimente as [dicas mencionadas nesta postagem do StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

## <a name="what-is-the-api-endpoint-for-nugetorg"></a>O que é o ponto de extremidade de API para o nuget.org?

Para usar o nuget.org como um repositório de pacotes com os clientes do NuGet, você deve usar o seguinte ponto de extremidade de API V3: 

**`https://api.nuget.org/v3/index.json`**

Os clientes mais antigos ainda podem usar o protocolo V2 para acessar o nuget.org. No entanto, observe que, para os clientes do NuGet 3.0 ou posterior, o serviço será mais lento e menos confiável usando o protocolo V2:

`https://www.nuget.org/api/v2` (PRETERIDO!!!) **Observação:** use "www." para obter a melhor confiabilidade possível.

## <a name="nugetorg-account-management"></a>gerenciamento de contas do nuget.org

### <a name="how-to-create-a-new-nugetorg-account"></a>Como criar uma conta do nuget.org?

Para criar uma conta do nuget.org, você precisa ter uma MSA (conta Microsoft pessoal) ou uma conta do AAD (Azure Active Directory). Se não tiver uma ID da Apple, [crie](https://signup.live.com) uma. Siga as etapas a seguir se você tiver uma conta MSA ou do AAD.
1. Vá para a [página de logon do nuget.org](https://www.nuget.org/users/account/LogOn).
1. Clique no botão **Entrar com a conta Microsoft**.
1. Insira os detalhes da conta MSA ou do AAD.
1. Aceite que as permissões sejam concedidas ao aplicativo *NuGet.org*.
1. Você será redirecionado para nuget.org e será solicitado que você registre um nome de usuário.
1. Especifique o nome de usuário na caixa de entrada. Observe que o nome de usuário **diferencia** maiúsculas de minúsculas e não pode ser alterado/renomeado mais tarde.
1. Clique no botão **Registrar**.

Agora você tem uma conta do nuget.org. Você pode executar o gerenciamento de conta na página de [configurações da conta](https://www.nuget.org/account).

### <a name="how-to-recover-nugetorg-password-login"></a>Como recuperar o logon com senha do nuget.org?

Observe que o [logon com senha do nuget.org foi descontinuado](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) e a única maneira de fazer logon no nuget.org é com uma MSA (conta Microsoft pessoal) ou conta do AAD (Azure Active Directory). No entanto, se você não conseguir acessar suas contas do AAD/MSA associadas, talvez será preciso usar o logon com senha para recuperar sua conta do nuget.org. Nessa situação, siga as etapas abaixo.
- **Requisito:** Você precisará ter acesso ao email que está associado com a conta para a qual você precisa recuperar a senha.
- Vá para a [página Esqueci a senha](https://www.nuget.org/account/ForgotPassword)
- Insira o endereço de **email** que está associado com a conta do nuget.org que deseja recuperar.
- Clique no botão **Enviar**.
- Você receberá um email para a conta do endereço de email especificado com um link para redefinir sua senha. Clique nesse link e defina a nova senha. Se não encontrar o email, verifique a pasta "lixo eletrônico".
- Quando terminar, você poderá fazer logon com nome de usuário/senha no NuGet.
- Para fazer logon com nome de usuário e senha, use o link **Entrar usando a conta do Nuget.org** na [página de logon do nuget.org](https://www.nuget.org/users/account/LogOn).

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>Qual conta Microsoft está vinculada à minha conta do nuget.org?

Se você tiver esquecido qual conta Microsoft está associada à conta do nuget.org, siga as etapas abaixo para obter assistência.
1. Vá para a [página de logon do nuget.org](https://www.nuget.org/users/account/LogOn) e clique no link **Precisa de ajuda para entrar?**
1. Isso mostrará a caixa de diálogo de pop-up para que você obtenha assistência. Siga as etapas nessa caixa de diálogo para entender quais são as contas Microsoft associadas à sua conta do nuget.org.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>Como alterar a conta Microsoft que eu uso para logon no nuget.org?
Se você quiser alterar a conta Microsoft para o usuário do nuget.org, siga as etapas abaixo. Digamos que sua conta Microsoft com o email `account1@outlook.com` está associada à conta do nuget.org com o nome de usuário `MyNuGetAccount`. É melhor que você altere o logon para outra conta Microsoft com o email `account2@outlook.com`
1. Entre usando a **conta Microsoft associada atualmente**, ou seja, `account1@outlook.com` na [página de logon](https://www.nuget.org/users/account/LogOn) depois de clicar em **Entrar com a conta Microsoft**.
1. Depois de conectado, vá para a página de [configurações da conta](https://www.nuget.org/account).
1. Expanda a seção **Conta de Logon**. Clique no botão **Alterar a Conta**.
1. Agora você será redirecionado à página de logon da Microsoft. Entre com a conta cuja associação você deseja alterar, ou seja, `account2@outlook.com`. **Observação**: talvez você precise clicar em **Sair e entrar com outra conta** durante o fluxo de entrada para ser capaz de fazer logon com uma conta Microsoft diferente.
1. Se você vir um erro como o abaixo, confira [A conta Microsoft está vinculada a outra conta do nuget.org](#microsoft-account-is-linked-with-another-nugetorg-account) para obter mais detalhes.
    >_Falha ao atualizar a conta Microsoft com 'account2 <account2@outlook.com>'. Isso pode acontecer se ela já está vinculada a outra conta do NuGet. Entre em contato com o suporte para obter mais informações._

1. Depois que entrar com êxito com sua segunda conta, você será redirecionado para a página de configurações da conta do nuget.org e deverá ver então a nova conta Microsoft associada à conta de logon. Prosseguindo, você deverá usar essa conta ao entrar no nuget.org.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>A conta Microsoft está vinculada a outra conta do nuget.org.

Se você tentou alterar seu logon da Microsoft e viu o erro abaixo:
> _Falha ao atualizar a conta Microsoft com 'account2 <account2@outlook.com>'. Isso pode acontecer se ela já está vinculada a outra conta do NuGet. Entre em contato com o suporte para obter mais informações._

Digamos que você está tentando alterar o logon da conta Microsoft de `account1@outlook.com` para o usuário do nuget.org com nome de usuário `MyNuGetAccount1` para outra conta Microsoft com o email `account2@outlook.com`. E você vê o erro acima.

**O que o erro acima significa?**

Significa que há outra conta de nuget.org associada com a conta Microsoft para a qual você está tentando alterá-la, ou seja, no exemplo acima, a conta Microsoft com o email `<account2@outlook.com>` está associada a outra conta do nuget.org com, digamos, o nome de usuário `MyNuGetAccount2`.

Você não pode alterar o logon associado com uma conta Microsoft que está vinculada a uma conta do nuget.org diferente.

**Eu esqueci que tinha outra conta do nuget.org, como posso descobrir qual conta do nuget.org é essa?**

Faça logon com a segunda conta Microsoft na [página de logon](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "página de logon"). Isso conectará você à conta do nuget.org atualmente associada à segunda conta Microsoft. Em seguida, você poderá exibir os pacotes carregados e executar o gerenciamento de conta nessa conta.

**Não me importo com essa segunda conta do nuget.org, quero alterar meu logon para a primeira conta do nuget.org com a segunda conta Microsoft. O que devo fazer?**

Se você não se importa com a segunda conta do nuget.org e ainda quer voltar a usar a conta Microsoft associada com o email `account2@outlook.com`. 

Você pode liberar a associação entre a conta Microsoft e a conta do nuget.org excluindo essa última.
1. Siga as etapas para [excluir usuário](#how-to-delete-my-nugetorg-account) para a segunda conta do nuget.org `MyNuGetAccount2`. 
1. Depois que essa conta for excluída, você poderá repetir as etapas para [alterar o logon da conta Microsoft](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login).

**Espere, eu me preocupo com essa segunda conta também. Eu não quero perder esta conta, apenas alterar meu logons de conta associados à primeira conta.**

Você precisará criar/usar uma terceira conta Microsoft, por exemplo, com o email `account3@outlook.com`. 
1. Primeiro você deve fazer logon com sua segunda conta Microsoft, `account2@outlook.com` em nuget.org. Siga as etapas acima para alterar os logons associados e associar a terceira conta Microsoft a essa conta do nuget.org.
1. Uma vez feito, sua segunda conta Microsoft com o email `account2@outlook.com` está livre para ser associada à primeira conta do nuget.org, `MyNuGetAccount1`. Siga as mesmas etapas acima para alterar os logons da Microsoft para a segunda conta Microsoft.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>Entrar com a conta Microsoft mostra que meu email está vinculado a outra conta Microsoft
Se você tiver tentado entrar com sua conta Microsoft, por exemplo, com o email `account1@outlook.com`, e vir um erro como o mostrado abaixo:
> _A conta com o email 'account1@outlook.com' está vinculada a outra conta Microsoft._
>
> _Se quiser atualizar a conta Microsoft vinculada, você poderá fazer isso na página de configurações de conta._

**O que o erro acima significa?**

Quando uma conta é criada em nuget.org, há um endereço de email de comunicação associado a essa conta. Esse é normalmente o mesmo que o endereço de email usado para a conta Microsoft associada. No entanto, você pode optar por especificar um endereço de email diferente para fins de comunicação. Então, tecnicamente, você poderia ter uma conta Microsoft diferente, por exemplo, com `account2@outlook.com`, que estivesse vinculada à conta do nuget.org e usasse o endereço de email de comunicação `account1@outlook.com`.

Portanto, o erro acima significa que já existe uma conta do nuget.org com o endereço de email de comunicação `account1@outlook.com`, mas está associada a outra conta Microsoft com um email **diferente de** `account1@outlook.com`.

**Como descobrir qual conta Microsoft está vinculada a esta conta do nuget.org?**

Você precisa usar o fluxo [assistência para entrada](#which-microsoft-account-is-linked-to-my-nugetorg-account) para descobrir qual conta Microsoft está vinculada à conta do nuget.org com o endereço de email `account1@outlook.com`.

**Desejo substituir essa conta com minha conta Microsoft**

Siga as etapas na seção [Não é possível usar o logon da Microsoft. Como recuperar minha conta do nuget.org?](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) para associar a conta Microsoft à conta do nuget.org existente.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Não é possível usar o logon da Microsoft. Como recuperar minha conta do nuget.org?

Se você tentou usar o recurso [assistência para entrada](#which-microsoft-account-is-linked-to-my-nugetorg-account) e não teve acesso à conta Microsoft associada à conta do nuget.org, siga as etapas abaixo para vincular uma nova conta Microsoft à conta do nuget.org.
1. **Requisito**: Você precisará de acesso a uma conta Microsoft (que não esteja associado a nenhuma conta do nuget.org existente). Se não tiver uma ID da Apple, [crie](https://signup.live.com) uma.
2. Siga os [passos para recuperar seu logon por senha](#how-to-recover-nugetorg-password-login). Se você já tem o logon por senha, ignore esta etapa.
3. [Faça logon no nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount) usando o logon por nome de usuário e senha.
4. Depois de conectado, você verá a caixa de diálogo pop-up ser exibida conforme demonstrado abaixo. Essa é a caixa de diálogo de descontinuação de senha.
5. **OBSERVAÇÃO**: Ignore as instruções para fazer logon com a conta Microsoft especificada. Agora você pode vincular sua conta do nuget.org a qualquer outro logon da Microsoft.
6. Clique no botão **Entrar com a conta da Microsoft** e faça logon com a conta Microsoft à qual você tem acesso, conforme mencionado na etapa 1.
7. Sua conta agora será vinculada à nova conta Microsoft, que poderá ser usada no futuro para fazer logon no nuget.org.

    ![Caixa de diálogo Vincular MSA](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>Como transformar a minha conta do nuget.org em uma organização?

Se você deseja transformar sua conta em uma organização e essa conta já está associada a um logon de conta Microsoft, siga as etapas descritas na documentação de [organizações no nuget.org](https://docs.microsoft.com/en-us/nuget/reference/organizations-on-nuget-org).

No entanto, se sua conta do nuget.org não está associada/vinculada a uma conta Microsoft, você pode seguir as etapas abaixo para transformar essa conta em uma organização.
1. **Requisito**: Você precisa ter uma conta individual criada primeiramente no nuget.org a ser usada como um administrador na conta da organização. Se você não tiver uma, [crie uma conta do nuget.org](#how-to-create-a-nugetorg-account)
2. Se você ainda não tiver logon por senha para sua conta do nuget.org, siga as [etapas para recuperar seu logon por senha](#how-to-recover-nugetorg-password-login). Se já tiver, ignore esta etapa.
3. [Faça logon no nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount) usando o logon por nome de usuário e senha.
4. Depois de conectado, você verá a caixa de diálogo pop-up ser exibida conforme demonstrado abaixo. Essa é a caixa de diálogo de descontinuação de senha. 
    > [!Important]
    > Ignore esta caixa de diálogo **não** clique no botão **entrar com a Microsoft**.

5. Acesse [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform). Isso permitirá que você converta a conta do nuget.org em uma organização sem vinculá-la a uma conta Microsoft.
6. Especifique o nome de usuário de administrador para sua conta do nuget.org pessoal/a conta que você criou na Etapa 1.
7. Siga as instruções para concluir a transformação dessa conta em uma organização.

    ![Caixa de diálogo Vincular MSA](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>Problemas de logon do nuget.org para contas do AAD com locatário não gerenciado?

Se você vir um erro como o abaixo durante o fluxo de logon com seu domínio da conta de email (@yourdomain.com), veja as etapas abaixo para recuperar sua conta do nuget.org.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**O que significa estado não gerenciado durante o logon? E por que isso está acontecendo agora?** 

Sua conta parece ter sido registrada anteriormente como uma conta Microsoft pessoal e isso funcionou bem, no entanto, agora parece que sua conta foi registrada como um locatário "Não gerenciado" no Azure Active Directory (o serviço de identidade que usamos para autenticar contas Microsoft). 

Isso pode ter acontecido porque você ou alguém da sua organização (com endereço de email @yourdomain.com) registrou-se com um dos serviços integrados do AAD ou [inscreveu-se por autoatendimento do Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-self-service-signup), o que cria um locatário "Não gerenciado" para o domínio da conta Microsoft usado (@yourdomain.com no seu caso). 

**O que posso fazer para recuperar minha conta?**

No momento não há uma maneira para nós (nuget.org) autenticarmos contas com essas contas de locatário "Não gerenciado" no Azure Active Directory. Estamos buscando autenticar essas contas de uma maneira melhor.

Se quiser fazer logon no nuget.org com sua conta Microsoft (@yourdomain.com), você (ou um administrador na sua empresa) precisará declarar-se proprietário do AAD fazendo uma validação de DNS para autenticar usuários com o endereço de email "@yourdomain.com". Siga as etapas para [tomada de controle do administrador de domínios](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/domains-admin-takeover) documentadas pelo Azure Active Directory. Depois que isso for feito, seu logon normal deverá começar a funcionar.

**Não quero fazer tudo isso, qual é a outra maneira de recuperar a minha conta?**

Você pode [criar](https://www.microsoft.com/en-us/account) uma conta Microsoft (com um email **não** associado com @yourdomain.com). Siga as etapas fornecidas na seção [recuperar sua conta do nuget.org](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account).

### <a name="how-do-i-change-my-nugetorg-account-username"></a>Como fazer para alterar meu nome de usuário da conta do nuget.org?

Não é possível fazer isso. Por uma questão de política, não permitimos a alteração de nomes de usuário até o momento. A única maneira de alterar seu nome de usuário é criar uma conta com o nome de usuário desejado. Recomendamos que exclua sua conta existente antes de criar uma nova, caso contrário, você não poderá reutilizar sua conta Microsoft registrada.
> [!Important]
> Excluir o usuário ainda **reservará** o `username`. Você não poderá reutilizar o mesmo nome de usuário novamente e **isso inclui a alteração do uso de maiúsculas e minúsculas**. Como um exemplo, se você tiver criado um usuário com nome de usuário `mycoolname` e desejar alterá-lo para `MyCoolName` (alterações de maiúsculas e minúsculas), isso não será possível depois de excluir o usuário.

Siga as etapas fornecidas na seção [excluir sua conta do nuget.org](#how-to-delete-my-nugetorg-account) e [registre uma nova conta](#how-to-create-a-new-nugetorg-account) com o nome de usuário correto.

### <a name="how-to-delete-my-nugetorg-account"></a>Como excluir minha conta do nuget.org?

Para excluir sua conta, recomendamos que você transfira a propriedade de todos os pacotes dos quais você é o único proprietário. Você pode ler mais sobre como fazê-lo em [gerenciamento dos proprietários de pacote](https://docs.microsoft.com/en-us/nuget/create-packages/publish-a-package#managing-package-owners-on-nugetorg). Isso também ajuda a agilizar sua solicitação.

> [!Important]
> Excluir o usuário resultará no seguinte:
>  1. Revoga as chaves de API associadas. 
>  2. Remova a conta como um proprietário de quaisquer pacotes filho.
>  3. Desassocie todas as reservas de prefixo de ID existentes anteriormente com esta conta.
>  4. Remova a conta como um membro de quaisquer organizações.
>  5. Seu nome de usuário será reservado e ninguém poderá reutilizá-lo sem nossas permissões.

Siga as etapas a seguir para continuar com a exclusão da conta.
1. [Faça logon no nuget.org](https://www.nuget.org/users/account/LogOn) com a conta que você deseja excluir.
2. Clique nesta URL: [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete) e siga as etapas para enviar a solicitação para excluir a conta.

Nosso atendimento ao cliente processará essa solicitação e executará a exclusão da conta.
