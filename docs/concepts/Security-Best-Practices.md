---
title: Práticas recomendadas para uma cadeia de fornecimento de software seguro
description: Práticas recomendadas para proteger sua cadeia de fornecimento de software usando o NuGet & GitHub.
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: e0f235d99e41e23a4551fbf7577f6c42e3381f5b
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859220"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a>Práticas recomendadas para uma cadeia de fornecimento de software seguro

O código-fonte aberto está em todos os lugares. Ele está em muitas bases de código e projetos de comunidade proprietários. Para organizações e indivíduos, a pergunta hoje não é se você está ou não está usando código-fonte aberto, mas que código de código-fonte aberto você está usando e quanto.

Se você não estiver ciente do que está em sua cadeia de fornecimento de software, uma vulnerabilidade de upstream em uma de suas dependências pode ser fatal, tornando você e seus clientes vulneráveis a um possível comprometimento. Neste documento, vamos nos aprofundar no que o termo "cadeia de fornecimento de software" significa, por que isso é importante e como você pode ajudar a proteger a cadeia de suprimentos do seu projeto com as práticas recomendadas.

![O estado do Octoverse 2020 – código-fonte aberto](media/opensource-percent.png)

## <a name="dependencies"></a>Dependências 

O termo cadeia de fornecimento de software é usado para fazer referência a tudo o que entra em seu software e de onde ele vem. São as dependências e propriedades de suas dependências das quais sua cadeia de suprimentos de software depende. Uma dependência é o que seu software precisa para ser executado. Pode ser código, binários ou outros componentes e de onde eles vêm, como um repositório ou Gerenciador de pacotes.

Ele inclui quem escreveu o código, quando ele foi contribuído, como ele foi revisado quanto a problemas de segurança, vulnerabilidades conhecidas, versões com suporte, informações de licença e praticamente qualquer coisa que o atinge em qualquer ponto do processo.

Sua cadeia de suprimentos também abrange outras partes da pilha além de um único aplicativo, como seus scripts de compilação e empacotamento ou o software que executa a infraestrutura em que seu aplicativo depende.

## <a name="vulnerabilities"></a>Vulnerabilidades

Hoje, as dependências de software são generalizadas. É muito comum que seus projetos usem centenas de dependências de software livre para a funcionalidade que você não precisa escrever por conta própria. Isso pode significar que a maior parte do seu aplicativo consiste em código que você não autorizou. 

![O estado do Octoverse 2020-Dependencies](media/dependencies.png)

As possíveis vulnerabilidades em suas dependências de terceiros ou de software livre, são presumivelmente dependências que você não pode controlar tão rigidamente quanto o código que você escreve, o que pode criar possíveis riscos de segurança em sua cadeia de suprimentos.

Se uma dessas dependências tiver uma vulnerabilidade, as chances você também terá uma vulnerabilidade. Isso pode ser assustador, pois uma de suas dependências pode ser alterada sem que você mesmo saiba. Mesmo que uma vulnerabilidade exista em uma dependência hoje, mas não possa ser explorada, ela poderá ser explorada no futuro. 

Ser capaz de aproveitar o trabalho de milhares de desenvolvedores de software livre e autores de biblioteca significa que milhares de estranhos podem contribuir com eficiência diretamente para seu código de produção. Seu produto, por meio de sua cadeia de suprimentos de software, é afetado por vulnerabilidades sem patches, erros inofensivos ou até mesmo ataques mal-intencionados contra dependências.

## <a name="supply-chain-compromises"></a>Comprometimentos da cadeia de fornecedores

A definição tradicional de uma cadeia de suprimentos vem da fabricação; é a cadeia de processos necessária para fazer e fornecer algo. Ele inclui planejamento, fornecimento de materiais, fabricação e varejo. Uma cadeia de fornecimento de software é semelhante, exceto em vez de materiais, é o código. Em vez de produção, é desenvolvimento. Em vez de aprofundar-se, o código é originado de fornecedores, de software livre ou comercial e, em geral, o código-fonte aberto vem de repositórios. Adicionar código de um repositório significa que seu produto assume uma dependência desse código.

Um exemplo de um ataque de cadeia de fornecedores de software ocorre quando um código mal-intencionado é adicionado intencionalmente a uma dependência, usando a cadeia de suprimentos dessa dependência para distribuir o código para suas vítimas. Os ataques de cadeia de fornecedores são reais. Há muitos métodos para atacar uma cadeia de fornecimento, desde a inserção direta de código mal-intencionado como um novo colaborador, a obtenção da conta de um colaborador sem que outras pessoas percebam ou até mesmo comprometem uma chave de assinatura para distribuir software que não é oficialmente parte da dependência.

Um ataque de cadeia de fornecimento de software é, em si, raramente o objetivo final, em vez disso, é o início de uma oportunidade para um invasor inserir malware ou fornecer um backdoor para acesso futuro.

![O estado do ciclo de vida da vulnerabilidade do Octoverse 2020](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a>Software sem patch

O uso de software livre hoje é significativo e não é esperado para reduzir a qualquer momento em breve. Considerando que não vamos parar de usar o software livre, a ameaça à segurança da cadeia de fornecedores é o software sem patches. Sabendo disso, como você pode resolver o risco de que uma dependência de seu projeto tenha uma vulnerabilidade?

- **Sabendo o que está em seu ambiente.** Isso exige a descoberta de suas dependências e quaisquer dependências transitivas para entender os riscos dessas dependências, como vulnerabilidades ou restrições de licenciamento.
- **Gerencie suas dependências.** Quando uma nova vulnerabilidade de segurança for descoberta, você deverá determinar se está afetada e, nesse caso, atualizar para a versão mais recente e o patch de segurança disponível. Isso é especialmente importante para revisar as alterações que introduzem novas dependências ou regularmente auditam dependências mais antigas.
- **Monitore sua cadeia de suprimentos.** Isso é auditar os controles que você tem em vigor para gerenciar suas dependências. Isso ajudará você a impor condições mais restritivas a serem atendidas para suas dependências.

![O estado das Octoverse 2020-conselhos](media/advisories.png)

Abordaremos várias ferramentas e técnicas fornecidas pelo NuGet e pelo GitHub, que você pode usar hoje para resolver riscos em potencial dentro de seu projeto. 

## <a name="knowing-what-is-in-your-environment"></a>Sabendo o que está em seu ambiente

### <a name="nuget-dependency-graph"></a>Grafo de dependência do NuGet

**📦 Consumidor do pacote**

Você pode exibir suas dependências do NuGet em seu projeto olhando diretamente no respectivo arquivo de projeto.

Normalmente, isso é encontrado em um dos dois locais:

-   [`packages.config`](../reference/packages-config.md) – Localizado na raiz do projeto.
-   [`<PackageReference>`](../consume-packages/package-references-in-project-files.md) – Localizado no arquivo de projeto. 

Dependendo do método usado para gerenciar suas dependências do NuGet, você também pode usar o Visual Studio para exibir suas dependências diretamente no [Gerenciador de soluções](/visualstudio/ide/solutions-and-projects-in-visual-studio#solution-explorer) ou no [Gerenciador de pacotes NuGet](../consume-packages/install-use-packages-visual-studio.md).

Para ambientes da CLI, você pode usar o [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) comando para listar as dependências do seu projeto ou da solução. 

Para obter mais informações sobre como gerenciar dependências do NuGet, [consulte a documentação a seguir](../consume-packages/overview-and-workflow.md).

### <a name="github-dependency-graph"></a>Grafo de dependência do GitHub 

**📦 Consumidor do pacote | 📦🖊 Autor do pacote**

Você pode usar o grafo de dependência do GitHub para ver os pacotes dos quais seu projeto depende e os repositórios que dependem dele. Isso pode ajudá-lo a ver as vulnerabilidades detectadas em suas dependências.

Para obter mais informações sobre dependências do repositório GitHub, [consulte a documentação a seguir](https://github.co/dependency-graph).

### <a name="dependency-versions"></a>Versões de dependência

**📦 Consumidor do pacote | 📦🖊 Autor do pacote**

Para garantir uma cadeia segura de dependências, você desejará garantir que todas as suas dependências & ferramentas sejam atualizadas regularmente para a versão estável mais recente, pois elas geralmente incluirão a funcionalidade e os patches de segurança mais recentes para vulnerabilidades conhecidas. Suas dependências podem incluir o código no qual você depende, os binários consumidos, as ferramentas usadas e outros componentes. Isso pode incluir:

-   [Visual Studio](https://visualstudio.microsoft.com/downloads/)
-   [SDK do .NET & tempo de execução](https://dotnet.microsoft.com/download)
-   [NuGet](https://www.nuget.org/downloads)
-   [Pacotes NuGet](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a>Gerenciar suas dependências

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a>Dependências preteridas e vulneráveis do NuGet

**📦 Consumidor do pacote | 📦🖊 Autor do pacote**

Você pode usar a [CLI do dotnet](/dotnet/core/tools/dotnet-list-package) para listar quaisquer dependências preteridas ou obsoletas conhecidas que você pode ter dentro de seu projeto ou solução. Você pode usar o comando `dotnet list package --deprecated` ou `dotnet list package --vulnerable` para fornecer uma lista de todas as preterições ou vulnerabilidades conhecidas.

### <a name="github-vulnerable-dependencies"></a>Dependências vulneráveis do GitHub

**📦 Consumidor do pacote | 📦🖊 Autor do pacote**

Se o seu projeto estiver hospedado no GitHub, você poderá aproveitar a [segurança do GitHub](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) para localizar vulnerabilidades de segurança e erros em seu projeto e o Dependabot os corrigirá abrindo uma solicitação de pull em sua base de código. 

A captura de dependências vulneráveis antes que elas sejam introduzidas é uma meta do movimento ["deslocar para a esquerda"](https://en.wikipedia.org/wiki/Shift-left_testing) . Ser capaz de ter informações sobre suas dependências, como sua licença, dependências transitivas e a idade das dependências, ajuda você a fazer exatamente isso.

Para obter mais informações sobre alertas do Dependabot & atualizações de segurança, [consulte a documentação a seguir](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies).

### <a name="nuget-feeds"></a>Feeds do NuGet

**📦 Consumidor do pacote**

Ao usar vários feeds públicos de origem do NuGet & privado, um pacote pode ser baixado de qualquer um dos feeds. Para garantir que sua compilação seja previsível e protegida contra ataques conhecidos, como [confusão de dependência](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610), saber de quais feeds (s) os seus pacotes são provenientes de uma prática recomendada. Você pode usar um único feed ou feed particular com recursos de upstream para proteção.

Para obter mais informações para proteger seus feeds de pacote, consulte [três maneiras de mitigar riscos ao usar feeds de pacotes privados](https://azure.microsoft.com/en-us/resources/3-ways-to-mitigate-risk-using-private-package-feeds/).

### <a name="client-trust-policies"></a>Políticas de confiança do cliente

**📦 Consumidor do pacote**

Há políticas que você pode aceitar em que é necessário que os pacotes que você usa sejam assinados. Isso permite que você confie em um autor de pacote, desde que ele seja assinado por autor ou confie em um pacote se ele pertencer a um usuário ou conta específica que seja o repositório assinado por NuGet.org.

Para configurar as políticas de confiança [do cliente, consulte a documentação a seguir](../consume-packages/installing-signed-packages.md).

### <a name="lock-files"></a>Bloquear arquivos

**📦 Consumidor do pacote**

Arquivos de bloqueio armazenam o hash do conteúdo do pacote. Se o hash de conteúdo de um pacote que você deseja instalar corresponder ao arquivo de bloqueio, ele garantirá a capacidade de repetição do pacote.

Para habilitar arquivos de bloqueio, [consulte a documentação a seguir](../consume-packages/package-references-in-project-files.md#locking-dependencies).

## <a name="monitor-your-supply-chain"></a>Monitorar sua cadeia de suprimentos

### <a name="github-secret-scanning"></a>Verificação de segredos do GitHub

**📦🖊 Autor do pacote**

O GitHub verifica repositórios de chaves de API do NuGet para impedir usos fraudulentos de segredos que foram confirmados acidentalmente. 

Para saber mais sobre a verificação de segredo, consulte [sobre a verificação de segredo](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning).

### <a name="author-package-signing"></a>Criar assinatura de pacote

**📦🖊 Autor do pacote**

A [assinatura de autor](../reference/signed-packages-reference.md) permite que um autor de pacote carimbasse sua identidade em um pacote e para que um consumidor Verifique se ele foi fornecido por você. Isso protege você contra a violação de conteúdo e serve como uma única fonte de verdade sobre a origem do pacote e a autenticidade do pacote. Quando combinado com as políticas de confiança do cliente, você pode verificar se um pacote é proveniente de um autor específico.

Para criar um pacote de assinatura, consulte [assinar um pacote](../create-packages/sign-a-package.md).

### <a name="two-factor-authentication-2fa"></a>Autenticação de Two-Factor (2FA)

**📦🖊 Autor do pacote**

A habilitação da autenticação de dois fatores (2FA) pode adicionar uma camada extra de segurança ao [fazer logon em sua conta do GitHub](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) ou no [repositório de pacotes públicos do NuGet.org](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa). É recomendável que você habilite a autenticação de dois fatores para proteger sua conta.

### <a name="package-id-prefix-reservation"></a>Reserva de prefixo da ID do pacote 

**📦🖊 Autor do pacote**

Para proteger a identidade de seus pacotes, você pode reservar um prefixo de ID de pacote com seu respectivo namespace para associar um proprietário correspondente se o prefixo de ID do pacote cair corretamente nos [critérios especificados](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria). 

Para saber mais sobre como reservar prefixos de ID, consulte [reserva de prefixo de ID de pacote](../nuget-org/id-prefix-reservation.md).

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a>Preterindo e deslistando um pacote vulnerável

**📦🖊 Autor do pacote**

Para proteger o ecossistema do pacote .NET quando estiver ciente de uma vulnerabilidade em um pacote que você criou, faça o melhor para reprovar e deslistar o pacote para que ele fique oculto dos usuários que procuram por pacotes. Se você estiver consumindo um pacote que foi preterido e não listado, evite usar o pacote.

Para saber como substituir e deslistar um pacote, consulte a documentação a seguir sobre como [substituir](../nuget-org/deprecate-packages.md) e [deslistar pacotes](../nuget-org/policies/deleting-packages.md#unlisting-a-package).

## <a name="summary"></a>Resumo

Sua cadeia de suprimentos de software é qualquer coisa que vá ou afete seu código. Embora as comprometeções de cadeia de fornecimento sejam reais e crescendo em popularidade, elas ainda são raras; Portanto, a coisa mais importante que você pode fazer é proteger sua cadeia **de fornecimento, conhecendo suas dependências, gerenciando suas dependências** e **monitorando sua cadeia de suprimentos.**

Você aprendeu sobre vários métodos que o NuGet e o [GitHub](/learn/modules/maintain-secure-repository-github/) fornecem que estão disponíveis hoje para serem mais eficazes na exibição, no gerenciamento e no monitoramento da sua cadeia de fornecedores.

Para obter mais informações sobre como proteger o software do mundo, consulte [o estado do relatório de segurança do Octoverse 2020](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf).
