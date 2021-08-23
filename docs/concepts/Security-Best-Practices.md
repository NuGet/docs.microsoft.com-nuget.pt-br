---
title: Práticas recomendadas para uma cadeia de fornecimento de software segura
description: Práticas recomendadas para proteger sua cadeia de fornecimento de software usando NuGet & GitHub.
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: 4575d4779ed90150cec667489c85875b7fb87a8d
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726971"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a>Práticas recomendadas para uma cadeia de fornecimento de software segura

O código-fonte aberto está em todos os lugares. Ele está em muitas bases de código proprietárias e projetos de comunidade. Para organizações e indivíduos, a pergunta hoje não é se você está ou não usando código-fonte aberto, mas qual código-fonte aberto você está usando e quanto.

Se você não estiver ciente do que está em sua cadeia de fornecimento de software, uma vulnerabilidade upstream em uma de suas dependências poderá ser fatal, tornando você e seus clientes vulneráveis a um possível comprometimento. Neste documento, nos aprofundaremos no que significa o termo "cadeia de fornecedores de software", por que isso importa e como você pode ajudar a proteger a cadeia de fornecedores do projeto com as práticas recomendadas.

![O Estado do Octoverso 2020 – Código Aberto](media/opensource-percent.png)

## <a name="dependencies"></a>Dependências 

O termo cadeia de fornecimento de software é usado para se referir a tudo o que entra em seu software e de onde ele vem. São as dependências e as propriedades de suas dependências das que sua cadeia de fornecimento de software depende. Uma dependência é o que seu software precisa executar. Pode ser código, binários ou outros componentes e de onde eles vêm, como um repositório ou gerenciador de pacotes.

Ele inclui quem escreveu o código, quando ele foi contribuído, como ele foi revisado quanto a problemas de segurança, vulnerabilidades conhecidas, versões com suporte, informações de licença e qualquer coisa que toque nele em qualquer ponto do processo.

Sua cadeia de fornecedores também abrange outras partes da sua pilha além de um único aplicativo, como os scripts de build e empacotamento ou o software que executa a infraestrutura de que seu aplicativo depende.

## <a name="vulnerabilities"></a>Vulnerabilidades

Atualmente, as dependências de software são pervasivas. É muito comum que seus projetos usem centenas de dependências de código aberto para a funcionalidade que você não precisa escrever por conta própria. Isso pode significar que a maioria do seu aplicativo consiste em código que você não escreveu. 

![O Estado do Octoverso 2020 – Dependências](media/dependencies.png)

Possíveis vulnerabilidades em suas dependências de terceiros ou de código aberto são dependências presumidas que você não pode controlar tão fortemente quanto o código que você escreve, o que pode criar possíveis riscos de segurança em sua cadeia de fornecedores.

Se uma dessas dependências tiver uma vulnerabilidade, provavelmente você também terá uma vulnerabilidade. Isso pode ser perigoso, pois uma de suas dependências pode mudar sem que você saiba. Mesmo que uma vulnerabilidade exista em uma dependência hoje, mas não seja explorável, ela poderá ser explorada no futuro. 

Ser capaz de aproveitar o trabalho de milhares de desenvolvedores de software livre e autores de biblioteca significa que milhares de pessoas com ética podem contribuir efetivamente diretamente para seu código de produção. Seu produto, por meio de sua cadeia de fornecedores de software, é afetado por vulnerabilidades sem-pate, erros de engano ou até mesmo ataques mal-intencionados contra dependências.

## <a name="supply-chain-compromises"></a>Comprometimentos da cadeia de fornecedores

A definição tradicional de uma cadeia de fornecedores vem da fabricação; é a cadeia de processos necessários para fazer e fornecer algo. Inclui planejamento, fornecimento de materiais, fabricação e varejo. Uma cadeia de fornecimento de software é semelhante, exceto que, em vez de materiais, é código. Em vez de fabricação, é desenvolvimento. Em vez de resvasar o ore do chão, o código é origem de fornecedores, comerciais ou de software livre e, em geral, o código de software livre vem de repositórios. A adição de código de um repositório significa que seu produto assume uma dependência desse código.

Um exemplo de ataque de cadeia de fornecimento de software ocorre quando um código mal-intencionado é adicionado intencionalmente a uma dependência, usando a cadeia de fornecimento dessa dependência para distribuir o código para suas vítima. Ataques de cadeia de fornecedores são reais. Há muitos métodos para atacar uma cadeia de fornecedores, desde inserir diretamente código mal-intencionado como um novo colaborador, assumir a conta de um colaborador sem que outras pessoas percebam ou até mesmo comprometer uma chave de assinatura para distribuir software que não faz parte oficialmente da dependência.

Um ataque de cadeia de fornecedores de software raramente é a meta final, em vez disso, é o início de uma oportunidade para um invasor inserir malware ou fornecer um backdoor para acesso futuro.

![O estado do Octoverso 2020 – Ciclo de vida de vulnerabilidade](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a>Software sem compatibilidade

O uso de open-source hoje é significativo e não deve ficar lento em breve. Considerando que não vamos parar de usar software livre, a ameaça à segurança da cadeia de fornecedores é um software sem compatibilidade. Sabendo disso, como você pode lidar com o risco de uma dependência do seu projeto ter uma vulnerabilidade?

- **Saber o que está em seu ambiente.** Isso requer a descoberta de suas dependências e dependências transitivas para entender os riscos dessas dependências, como vulnerabilidades ou restrições de licenciamento.
- **Gerencie suas dependências.** Quando uma nova vulnerabilidade de segurança é descoberta, você deve determinar se foi afetado e, em caso afirmado, atualizar para a versão mais recente e o patch de segurança disponíveis. Isso é especialmente importante para revisar as alterações que introduzem novas dependências ou auditam regularmente as dependências mais antigas.
- **Monitore sua cadeia de fornecedores.** Isso ocorre auditando os controles que você tem em mãos para gerenciar suas dependências. Isso ajudará você a impor condições mais restritivas a serem atendidas para suas dependências.

![O estado do Octoverso 2020 – Consultorias](media/advisories.png)

Abordaremos várias ferramentas e técnicas que NuGet e GitHub, que você pode usar hoje para resolver possíveis riscos dentro do seu projeto. 

## <a name="knowing-what-is-in-your-environment"></a>Saber o que está em seu ambiente

### <a name="nuget-dependency-graph"></a>NuGet de dependência

**📦 Consumidor do Pacote**

Você pode exibir suas NuGet dependências em seu projeto observando diretamente o respectivo arquivo de projeto.

Normalmente, isso é encontrado em um dos dois locais:

-   [`packages.config`](../reference/packages-config.md) – localizado na raiz do projeto.
-   [`<PackageReference>`](../consume-packages/package-references-in-project-files.md) – Localizado no arquivo de projeto. 

Dependendo do método usado para gerenciar suas dependências do NuGet, você também pode usar o [](/visualstudio/ide/solutions-and-projects-in-visual-studio#solution-explorer) Visual Studio para exibir suas dependências diretamente no Gerenciador de Soluções ou [NuGet Gerenciador de Pacotes](../consume-packages/install-use-packages-visual-studio.md).

Para ambientes da CLI, você pode usar o comando para listar as dependências do projeto [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) ou da solução. 

Para obter mais informações sobre como gerenciar NuGet dependências, [consulte a documentação a seguir.](../consume-packages/overview-and-workflow.md)

### <a name="github-dependency-graph"></a>Grafo de dependência do GitHub 

**📦 Pacotes de | 📦🖊 Autor do pacote**

Você pode usar GitHub de dependência do usuário para ver os pacotes dos que seu projeto depende e os repositórios que dependem dele. Isso pode ajudá-lo a ver todas as vulnerabilidades detectadas em suas dependências.

Para obter mais informações sobre GitHub dependências do repositório, [consulte a documentação a seguir.](https://github.co/dependency-graph)

### <a name="dependency-versions"></a>Versões de dependência

**📦 Pacotes de | 📦🖊 Autor do pacote**

Para garantir uma cadeia de fornecimento segura de dependências, você deve garantir que todas as suas dependências & ferramentas sejam atualizadas regularmente para a versão estável mais recente, pois geralmente incluirão a funcionalidade mais recente e os patches de segurança para vulnerabilidades conhecidas. Suas dependências podem incluir o código de que você depende, binários consumidos, ferramentas que você usa e outros componentes. Isso pode incluir:

-   [Visual Studio](https://visualstudio.microsoft.com/downloads/)
-   [Runtime de & SDK do .NET](https://dotnet.microsoft.com/download)
-   [NuGet](https://www.nuget.org/downloads)
-   [Pacotes NuGet](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a>Gerenciar suas dependências

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a>NuGet dependências preterida e vulneráveis

**📦 Pacotes de | 📦🖊 Autor do pacote**

Você pode usar a [CLI do dotnet](/dotnet/core/tools/dotnet-list-package) para listar as dependências preterida ou vulneráveis conhecidas que você pode ter dentro de seu projeto ou solução. Você pode usar o comando `dotnet list package --deprecated` ou para fornecer uma lista de quaisquer `dotnet list package --vulnerable` preterências ou vulnerabilidades conhecidas.

### <a name="github-vulnerable-dependencies"></a>GitHub dependências vulneráveis

**📦 Pacotes de | 📦🖊 Autor do pacote**

Se o projeto estiver hospedado no GitHub, você poderá aproveitar a Segurança do [GitHub](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) para encontrar vulnerabilidades e erros de segurança em seu projeto e o Dependabot os corrigirá abrindo uma solicitação de pull em sua base de código. 

Capturar dependências vulneráveis antes que elas sejam introduzidas é uma meta do [movimento "Shift Left".](https://en.wikipedia.org/wiki/Shift-left_testing) Poder ter informações sobre suas dependências, como sua licença, dependências transitivas e a idade das dependências, ajuda você a fazer exatamente isso.

Para obter mais informações sobre os alertas do Dependabot & atualizações de segurança, [consulte a documentação a seguir.](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies)

### <a name="nuget-feeds"></a>NuGet feeds

**📦 Consumidor do Pacote**

Ao usar vários feeds de & privados NuGet, um pacote pode ser baixado de qualquer um dos feeds. Para garantir que seu build seja previsível e seguro contra ataques conhecidos, como a Confusão de [Dependência,](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610)saber de quais feeds específicos seus pacotes estão vindo é uma melhor prática. Você pode usar um único feed ou feed privado com recursos de upstreaming para proteção.

Para obter mais informações para proteger seus feeds de pacote, consulte 3 Maneiras de atenuar o risco [ao usar feeds de pacotes privados.](https://azure.microsoft.com/resources/3-ways-to-mitigate-risk-using-private-package-feeds/)

### <a name="client-trust-policies"></a>Políticas de confiança do cliente

**📦 Consumidor do Pacote**

Há políticas nas quais você pode optar por exigir que os pacotes que você usa sejam assinados. Isso permite que você confie em um autor do pacote, desde que ele seja assinado pelo autor ou confie em um pacote se ele for de propriedade de um usuário ou conta específico que seja um repositório assinado por NuGet.org.

Para configurar políticas de confiança do cliente, [consulte a documentação a seguir.](../consume-packages/installing-signed-packages.md)

### <a name="lock-files"></a>Bloquear arquivos

**📦 Consumidor do Pacote**

Os arquivos de bloqueio armazenam o hash do conteúdo do pacote. Se o hash de conteúdo de um pacote que você deseja instalar corresponde ao arquivo de bloqueio, isso garantirá a capacidade de repetição do pacote.

Para habilitar arquivos de bloqueio, [consulte a documentação a seguir.](../consume-packages/package-references-in-project-files.md#locking-dependencies)

## <a name="monitor-your-supply-chain"></a>Monitorar sua cadeia de fornecedores

### <a name="github-secret-scanning"></a>Verificação de segredos do GitHub

**📦🖊 Autor do pacote**

GitHub verifica repositórios para NuGet de API para evitar usos fraudulentos de segredos que foram acidentalmente comprometidos. 

Para saber mais sobre a verificação de segredo, consulte [Sobre a verificação de segredo.](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning)

### <a name="author-package-signing"></a>Assinatura de pacote de autor

**📦🖊 Autor do pacote**

[A assinatura de](../reference/signed-packages-reference.md) autor permite que um autor do pacote carimbar sua identidade em um pacote e para que um consumidor verifique se ela veio de você. Isso protege contra a adulteração de conteúdo e serve como uma única fonte de verdade sobre a origem do pacote e a autenticidade do pacote. Quando combinado com políticas de confiança do cliente, você pode verificar se um pacote veio de um autor específico.

Para assinar um pacote, consulte [Assinar um pacote](../create-packages/sign-a-package.md).

### <a name="two-factor-authentication-2fa"></a>Two-Factor autenticação (2FA)

**📦🖊 Autor do pacote**

A habilitação da 2FA (autenticação de dois fatores) pode adicionar uma camada extra de segurança ao fazer logon em sua conta [GitHub](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) ou no repositório de pacotes [públicos NuGet.org](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa). É recomendável habilitar a autenticação de dois fatores para proteger sua conta.

### <a name="package-id-prefix-reservation"></a>Reserva de prefixo da ID do pacote 

**📦🖊 Autor do pacote**

Para proteger a identidade de seus pacotes, você pode reservar um prefixo de ID do pacote com seu respectivo namespace para associar um proprietário correspondente se o prefixo de ID do pacote se enquadra corretamente nos [critérios especificados.](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) 

Para saber mais sobre como reservar prefixos de ID, consulte [Reserva de prefixo de ID do pacote](../nuget-org/id-prefix-reservation.md).

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a>Preterindo e deslistando um pacote vulnerável

**📦🖊 Autor do pacote**

Para proteger o ecossistema de pacotes .NET quando você estiver ciente de uma vulnerabilidade em um pacote que você tenha sido autor, faça o possível para preteri-lo e desalocar o pacote para que ele fique oculto dos usuários que pesquisam pacotes. Se você estiver consumindo um pacote que foi preterido e não está na lista, evite usar o pacote.

Para saber como preteri-lo e desalocar um pacote, consulte a documentação a seguir sobre como [preteri-los](../nuget-org/deprecate-packages.md) e não [listar pacotes](../nuget-org/policies/deleting-packages.md#unlisting-a-package).

## <a name="summary"></a>Resumo

Sua cadeia de fornecimento de software é qualquer coisa que entra ou afeta seu código. Embora os comprometimentos da cadeia de fornecedores sejam reais e crescentes em popularidade, eles ainda são raros; portanto, a coisa mais importante que você pode fazer é proteger sua cadeia de fornecedores ciente de suas **dependências,** gerenciar suas dependências e **monitorar sua cadeia de fornecedores.**

Você aprendeu sobre vários métodos que NuGet e [GitHub](/learn/modules/maintain-secure-repository-github/) que estão disponíveis para você hoje para ser mais eficaz na exibição, no gerenciamento e no monitoramento da cadeia de fornecedores.

Para obter mais informações sobre como proteger o software do mundo, consulte [The State of the Octoverse 2020 Security Report](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf).
