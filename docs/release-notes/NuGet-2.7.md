---
title: Notas de versão do NuGet 2,7
description: Notas de versão do NuGet 2,7 incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f26ac80046ec321ce5bdbf2bac23c0e1939cd69a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317077"
---
# <a name="nuget-27-release-notes"></a>Notas de versão do NuGet 2,7

[NuGet 2.6.1 para notas de versão](../release-notes/nuget-2.6.1-for-webmatrix.md) | do WebMatrix notas de[versão do NuGet 2.7.1](../release-notes/nuget-2.7.1.md)

O NuGet 2,7 foi lançado em 22 de agosto de 2013.

## <a name="acknowledgements"></a>Confirmações

Gostaríamos de agradecer aos seguintes colaboradores externos por suas contribuições significativas para o NuGet 2,7:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Mostrar URL de licença ao listar pacotes e detalhes é detalhado.
2. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -adicionar o atributo developmentDependency `packages.config` ao e usá-lo no comando de pacote para incluir apenas pacotes de tempo de execução
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Evite a chave de propriedades duplicadas no comando NuGet. exe Pack.
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -aumentar o tamanho do cache da máquina para 200.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - caixa de diálogo [#3217](http://nuget.codeplex.com/workitem/3217) corrigir o NuGet mostrando as atualizações na guia incorreta
    - Fix Project. TargetFramework pode ser nulo no projectmanager
    - [#3248](http://nuget.codeplex.com/workitem/3248) -Fix SharedPackageRepository FindPackage/FindPackagesById falhará em PackageID não existente
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -habilita o suporte para o projeto Nomad
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -falha de comando de envio de correção com exit código 0 quando o arquivo não existe.
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -corrigir o bug com o comando Add-BindingRedirect quando um projeto faz referência a um projeto de banco de dados.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -corrigir o bug do curinga de análise do NuGet. Pack no atributo ' Exclude ' de forma incorreta.
10. [Justin Prezado](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [](http://nuget.codeplex.com/workitem/3307) o bug `NuGet.targets` de #3307 correção não passa $ (plataforma) para NuGet. exe durante a restauração de pacotes.
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -corrija o bug no comando de pacote NuGet. exe, que permitiria adicionar arquivos com o mesmo nome, mas com maiúsculas e minúsculas, eventualmente fazendo com que a exceção "o item já exista".
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) -adicionar a Propriedade Version à classe NetPortableProfile.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -corrigir o bug NullReferenceException se requireApiKey = true, mas o cabeçalho X-NUGET-APIKEY não estiver presente
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) -corrige o arquivo de destino NuGet. Build para que funcione corretamente no MonoDevelop
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - Melhorar o desempenho do comando de restauração aumentando a paralelização

## <a name="notable-features-in-the-release"></a>Recursos notáveis na versão

### <a name="package-restore-by-default-with-implicit-consent"></a>Restauração de pacote por padrão (com consentimento implícito)

O NuGet 2,7 apresenta uma nova abordagem para a restauração do pacote e também supera um grande obstáculo: O consentimento de restauração de pacote agora está ativado por padrão! A combinação da nova abordagem e do consentimento implícito simplificará drasticamente os cenários de restauração de pacote.

#### <a name="implicit-consent"></a>Consentimento implícito

Com as versões 2,0, 2,1, 2,2, 2,5 e 2,6 do NuGet, os usuários precisavam permitir explicitamente que o NuGet baixe pacotes ausentes durante a compilação. Se esse consentimento não tiver sido explicitamente fornecido, as soluções que tinham a restauração de pacote habilitada falhariam ao serem compiladas até que o usuário tivesse concedido o consentimento.

A partir do NuGet 2,7, o consentimento de restauração de pacote é ativado por padrão,  ao mesmo tempo que permite que os usuários recusem explicitamente a restauração do pacote, se desejado, usando a caixa de seleção nas configurações do NuGet no Visual Studio. Essa alteração para o consentimento implícito afeta o NuGet nos seguintes ambientes:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* Utilitário de linha de comando NuGet. exe

#### <a name="automatic-package-restore-in-visual-studio"></a>Restauração automática de pacote no Visual Studio

A partir do NuGet 2,7, o NuGet baixará automaticamente os pacotes ausentes durante a compilação no Visual Studio, mesmo que a restauração do pacote não tenha sido explicitamente habilitada para a solução. Essa restauração automática de pacote ocorre no Visual Studio quando você cria um projeto ou a solução, mas antes de o MSBuild ser invocado. Isso gera alguns benefícios significativos:

1. Não é necessário usar o gesto "Habilitar restauração de pacote NuGet" em sua solução
1. Os projetos não precisam ser modificados e o NuGet não fará alterações no projeto para garantir que a restauração do pacote esteja habilitada
1. Todos os pacotes NuGet, incluindo aqueles que incluíram importações do MSBuild para arquivos props/targets, serão restaurados antes que o MSBuild seja invocado, garantindo *que* essas props/destinos sejam reconhecidas corretamente durante a compilação

Para usar a restauração automática de pacote no Visual Studio, você só precisa tomar uma ação (em):

1. Não faça check- `packages` in de sua pasta

Há várias maneiras de omitir a `packages` pasta do controle do código-fonte. Para obter mais informações, consulte o tópico [pacotes e controle do código-fonte](../consume-packages/packages-and-source-control.md) .

Embora todos os usuários sejam implicitamente optados pelo consentimento automático de restauração de pacote, você pode facilmente recusar as configurações do Gerenciador de pacotes no Visual Studio.

![Configurações do Gerenciador de pacotes](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Restauração simplificada de pacote da linha de comando

O NuGet 2,7 apresenta um novo recurso para NuGet. exe:`nuget.exe restore`

Esse novo comando Restore permite que você restaure facilmente todos os pacotes para uma solução com um único comando, aceitando um arquivo de solução ou uma pasta como um argumento. Além disso, esse argumento é implícito quando há apenas uma única solução na pasta atual. Isso significa que todos os trabalhos a seguir são de uma pasta que contém um único arquivo de solução (MySolution. sln):

1. NuGet. exe restaurar MySolution. sln
1. restauração do NuGet. exe.
1. restauração do NuGet. exe

O comando Restore abrirá o arquivo de solução e localizará todos os projetos dentro da solução. A partir daí, ele encontrará `packages.config` os arquivos para cada um dos projetos e restaurará todos os pacotes encontrados. Ele também restaura os `.nuget\packages.config` pacotes no nível da solução encontrados no arquivo. Mais informações sobre o novo comando Restore podem ser encontradas na [referência de linha de comando](../reference/cli-reference/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>O novo fluxo de trabalho de restauração de pacote

Estamos empolgados com essas alterações na restauração do pacote, pois ele introduz um novo fluxo de trabalho. Se você quiser omitir seus pacotes do controle do código-fonte, simplesmente `packages` não confirme a pasta. Os usuários do Visual Studio que abrirem e criarem a solução verão os pacotes restaurados automaticamente. Para compilações de linha de comando, `nuget.exe restore` basta invocar `msbuild`antes de invocar. Você não precisa mais se lembrar de usar o gesto "Habilitar restauração de pacote NuGet" em sua solução e não precisaremos mais modificar seus projetos para alterar a compilação. E isso também produz uma experiência muito melhorada para pacotes que incluem importações do MSBuild, especialmente para importações adicionadas por meio do recurso recente do NuGet para [importar automaticamente arquivos props/targets](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) da pasta \Build.

Além do trabalho que fizemos por si só, também estamos trabalhando com alguns parceiros importantes para arredondar essa nova abordagem. Ainda não temos cronogramas concretos para nenhum deles, mas cada um deles está tão empolgado quanto estamos sobre a nova abordagem.

* Team Foundation Service-eles estão trabalhando para integrar a chamada para `nuget.exe restore` nos cenários de compilação padrão.
* Sites do Windows Azure-eles estão trabalhando para permitir que você envie por push seu projeto para o `nuget.exe restore` Azure e que tenha sido chamado antes que seu site seja criado.
* TeamCity-eles estão atualizando seu plug-in do NuGet Installer para o TeamCity 8. x
* AppHarbor-eles estão trabalhando para permitir que você envie por push seu repositório para AppHarbor `nuget.exe restore` e tenha chamado antes de sua solução ser compilada.

Com cada um dos parceiros acima, eles usariam sua própria cópia do NuGet. exe e você não precisaria carregar o NuGet. exe em sua solução.

#### <a name="known-issues"></a>Problemas Conhecidos

Havia dois problemas conhecidos com o NuGet. exe Restore com a versão inicial 2,7, mas eles foram corrigidos em 9/6/2013 com uma atualização para o [pacote NuGet. CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/).  Essa atualização também está disponível na [página de download do NuGet 2,7](https://nuget.codeplex.com/releases/view/107605) no CodePlex.  A `nuget.exe update -self` execução será atualizada para a versão mais recente.

Os corrigidos foram:

1. [A nova restauração de pacote não funciona no mono ao usar o arquivo SLN](https://nuget.codeplex.com/workitem/3596)
1. [A nova restauração do pacote não funciona com projetos do WiX](https://nuget.codeplex.com/workitem/3598)

Também há um problema conhecido com o novo fluxo de trabalho de restauração de pacote no qual a [restauração automática de pacote não funciona para projetos em uma pasta de solução](https://nuget.codeplex.com/workitem/3625). Esse problema foi corrigido no NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Redirecionamento de projeto e atualização de erros/avisos de compilação

Muitas vezes depois de redirecionar ou atualizar seu projeto, você descobre que alguns pacotes NuGet não estão funcionando corretamente. Infelizmente, não há nenhuma indicação disso e, em seguida, não há nenhuma orientação sobre como solucioná-lo. Com o NuGet 2,7, agora usamos alguns eventos do Visual Studio para reconhecer quando você redirecionava ou atualizou seu projeto de forma que afete seus pacotes NuGet instalados.

Se detectarmos que qualquer um dos seus pacotes foi afetado pela redirecionamento ou atualização, geraremos erros de Build imediatos para que você saiba. Além do erro de compilação imediata, também persistemos um `requireReinstallation="true"` sinalizador em seu `packages.config` arquivo para todos os pacotes que foram afetados pelo redirecionamento, e cada compilação subsequente no Visual Studio gerará avisos de compilação para esses pacotes.

Embora o NuGet não possa tomar a ação automática para reinstalar os pacotes afetados, esperamos que essa indicação e aviso sejam orientados a descobrir quando você precisa reinstalar os pacotes. Também estamos trabalhando na [documentação de diretrizes](../consume-packages/reinstalling-and-updating-packages.md) de reinstalação de pacotes para as quais essas mensagens de erro o direcionam.

### <a name="nuget-configuration-defaults"></a>Padrões de configuração do NuGet

Muitas empresas estão usando o NuGet internamente, mas teve um tempo rígido que orienta seus desenvolvedores a usar fontes de pacote internas em vez de nuget.org. O NuGet 2,7 apresenta um recurso de padrões de configuração que permite que os padrões de todo o computador sejam especificados para:

1. Fontes de pacote habilitadas
1. Fontes de pacote registradas, mas desabilitadas
1. A origem de push NuGet. exe padrão

Cada um deles agora pode ser configurado em um arquivo localizado em `%ProgramData%\NuGet\NuGetDefaults.Config`. Se esse arquivo de configuração especificar as origens do pacote, a origem do pacote NuGet.org padrão não será registrada automaticamente, e `NuGetDefaults.Config` aquelas em serão registradas em seu lugar.

Embora não seja necessário usar esse recurso, esperamos que as empresas implantem `NuGetDefaults.Config` arquivos usando política de grupo.

*Observe que esse recurso nunca fará com que uma origem do pacote seja removida das configurações do NuGet de um desenvolvedor. Isso significa que, se o desenvolvedor já tiver usado o NuGet e, portanto, tiver a origem do pacote NuGet.org registrada, ele não `NuGetDefaults.Config` será removido após a criação de um arquivo.*

Consulte [padrões de configuração do NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) para obter mais informações sobre esse recurso.

### <a name="renaming-the-default-package-source"></a>Renomeando a origem do pacote padrão

O NuGet sempre registrou uma origem de pacote padrão chamada "origem do pacote oficial do NuGet" que aponta para nuget.org. Esse nome era detalhado e também não especificou onde ele estava realmente apontando. Para resolver esses dois problemas, renomeamos essa origem do pacote para simplesmente "nuget.org" na interface do usuário. A URL para a origem do pacote também foi alterada para incluir o "www". group. Depois de usar o NuGet 2,7, a "origem do pacote oficial do NuGet" existente será automaticamente atualizada para "NuGet.org" como seu<https://www.nuget.org/api/v2/>nome e "" como sua URL.

### <a name="performance-improvements"></a>Melhorias de desempenho

Fizemos alguma melhoria de desempenho em 2,7, o que produzirá menor volume de memória, menos uso de disco e instalação de pacote mais rápida. Também fizemos consultas mais inteligentes para feeds baseados em OData, o que reduzirá a carga geral.

### <a name="new-extensibility-apis"></a>Novas APIs de extensibilidade

Adicionamos algumas novas APIs aos nossos serviços de extensibilidade para preencher a lacuna de funcionalidades ausentes em versões anteriores.

#### <a name="ivspackageinstallerservices"></a>IVsPackageInstallerServices

    ```cs
    // Checks if a NuGet package with the specified Id and version is installed in the specified project.
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    // Get the list of NuGet packages installed in the specified project.
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
    ```

#### <a name="ivspackageinstaller"></a>IVsPackageInstaller

    ```cs
    // Installs one or more packages that exist on disk in a folder defined in the registry.
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    // Installs one or more packages that are embedded in a Visual Studio Extension Package.
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);
    ```

### <a name="development-only-dependencies"></a>Dependências somente de desenvolvimento

Esse recurso foi contribuído pelo [Adam Ralph](https://twitter.com/adamralph) e permite que os autores de pacotes declaram dependências que eram usadas apenas no momento do desenvolvimento e não exigem dependências de pacote. Ao adicionar um `developmentDependency="true"` atributo a um pacote no `packages.config`, `nuget.exe pack` o não incluirá mais esse pacote como uma dependência.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Removido o suporte para o Visual Studio 2010 Express para Windows Phone

O novo modelo de restauração de pacote no 2,7 é implementado por um novo VSPackage que é diferente do VSPackage principal do NuGet. Devido a um problema técnico, esse novo VSPackage não funciona corretamente no *visual studio 2010 Express para Windows Phone* SKU, pois compartilhamos a mesma base de código com outros SKUs do Visual Studio com suporte. Portanto, a partir do NuGet 2,7, estamos descartando o suporte para o *Visual Studio 2010 Express para Windows Phone* da extensão publicada. O suporte para o *visual studio 2010 Express para Web* ainda está incluído na extensão primária publicada na Galeria de extensões do Visual Studio.

Como não temos certeza de quantos desenvolvedores ainda estão usando o NuGet nessa versão/edição do Visual Studio, estamos publicando uma extensão separada do Visual Studio especificamente para esses usuários e publicando-o no CodePlex (em vez da Galeria de extensões do Visual Studio) . Não planejamos continuar a manter essa extensão, mas se isso afetar, informe-nos ao arquivar um problema no CodePlex.

Para baixar o Gerenciador de pacotes NuGet (para Visual Studio 2010 Express para Windows Phone), visite a página de [downloads do nuget 2,7](https://nuget.codeplex.com/releases/view/107605) .

### <a name="bug-fixes"></a>Correções de Bug

Além desses recursos, esta versão do NuGet também inclui muitas outras correções de bugs. Havia 97 problemas totais abordados na versão. Para obter uma lista completa de itens de trabalho corrigidos no NuGet 2,7, consulte o rastreador de [problemas do NuGet para esta versão](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
