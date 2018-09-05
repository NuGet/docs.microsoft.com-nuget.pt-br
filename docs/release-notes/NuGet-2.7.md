---
title: Notas de versão 2.7 do NuGet
description: Notas de versão do NuGet 2.7, incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 97d3e5f0238fd6947a54e5eb3229b89b6746f18c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550959"
---
# <a name="nuget-27-release-notes"></a>Notas de versão 2.7 do NuGet

[NuGet 2.6.1 para WebMatrix Release Notes](../release-notes/nuget-2.6.1-for-webmatrix.md) | [notas de versão do NuGet 2.7.1](../release-notes/nuget-2.7.1.md)

NuGet 2.7 foi lançado em 22 de agosto de 2013.

## <a name="acknowledgements"></a>Confirmações

Gostaríamos de agradecer os seguintes colaboradores externos por suas contribuições significativas para NuGet 2.7:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Mostra a url de licença quando listando pacotes e detalhamento é detalhado.
2. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -adicione o atributo developmentDependency para `packages.config` e usá-lo no comando de pacote para incluir apenas os pacotes de tempo de execução
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Evite a chave duplicada de propriedades no comando de pacote nuget.exe.
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -Aumentar tamanho do cache de máquina para 200.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -caixa de diálogo do NuGet corrigir mostrando as atualizações na guia errada
    - Correção Project.TargetFramework pode ser nula em GerenteDoProjeto
    - [#3248](http://nuget.codeplex.com/workitem/3248) -corrigir SharedPackageRepository FindPackage/FindPackagesById falhará em packageId inexistente
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -habilitar o suporte para o projeto Nomad
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -falha de comando de envio de correção com exit código 0 quando o arquivo não existe.
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -corrigir o bug com o comando Add-BindingRedirect quando um projeto referencia um projeto de banco de dados.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -correção de bug de nuget.pack análise curinga no atributo 'exclude' incorretamente.
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) -correção de bug `NuGet.targets` não passa $ (plataforma) para nuget.exe ao restaurar os pacotes.
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -correção de bug no comando de pacote nuget.exe que permitiria que a adição de arquivos com o mesmo nome mas com maiusculas e minúsculas diferentes, eventualmente fazendo com que a exceção "Item já existe".
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) -propriedade da versão de adicionar a classe NetPortableProfile.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -corrigir bugs de NullReferenceException se requireApiKey = true, mas o cabeçalho X-NUGET-APIKEY não estiver presente
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) -NuGet.Build corrige destinos de arquivo para que ele funcione corretamente no MonoDevelop
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - Melhorar o desempenho do comando de restauração, aumentando a paralelização

## <a name="notable-features-in-the-release"></a>Recursos importantes da versão

### <a name="package-restore-by-default-with-implicit-consent"></a>Restauração de pacote por padrão (com consentimento implícito)

Apresenta uma nova abordagem para restauração de pacote NuGet 2.7 e também supera um grande obstáculo: consentimento de restauração de pacote agora é ativado por padrão! A combinação da nova abordagem e o consentimento implícito drasticamente simplificará os cenários de restauração de pacote.

#### <a name="implicit-consent"></a>Consentimento implícito

Com o NuGet versões 2.0, 2.1, 2.2, 2.5 e 2.6, usuários necessários para permitir explicitamente o NuGet Baixe pacotes ausentes durante a compilação. Se esse consentimento não tinha sido explicitamente fornecido, e soluções que tinham habilitado a restauração de pacote não será compilar até que o usuário tive dado consentimento.

Começando com o NuGet 2.7, consentimento de restauração de pacote está ativado por padrão, permitindo aos usuários explicitamente *recusar* da restauração de pacote, se desejado, usando a caixa de seleção nas configurações do NuGet no Visual Studio. Essa alteração em consentimento implícito afeta NuGet nos seguintes ambientes:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* Utilitário de linha de comando NuGet.exe

#### <a name="automatic-package-restore-in-visual-studio"></a>Restauração automática de pacotes no Visual Studio

Começando com o NuGet 2.7, o NuGet baixará automaticamente os pacotes ausentes durante o build no Visual Studio, mesmo que a restauração de pacote ainda não foi habilitada explicitamente para a solução. Essa restauração automática do pacote acontece no Visual Studio quando você compila um projeto ou solução, mas antes que o MSBuild é chamado. Isso resulta em alguns benefícios significativos:

1. Nenhuma outra precisar usar o gesto "Habilitar a restauração do pacote NuGet" em sua solução
1. Projetos não precisam ser modificados e NuGet não fará alterações ao seu projeto para garantir que a restauração de pacote está habilitada
1. Todos os pacotes do NuGet, incluindo aqueles que são incluídas as importações do MSBuild para arquivos de propriedades/destinos serão restaurados *antes de* MSBuild é chamado, garantindo a essas propriedades/destinos são reconhecidos corretamente durante a compilação

Para usar a restauração automática do pacote no Visual Studio, você só precisa executar uma (ação em):

1. Não fazer check-in seu `packages` pasta

Há várias maneiras para omitir o `packages` pasta do controle de origem. Para obter mais informações, consulte o [pacotes e controle do código-fonte](../consume-packages/packages-and-source-control.md) tópico.

Embora todos os usuários são implicitamente aceitado o consentimento de restauração automática do pacote, você pode facilmente recusá-lo através das configurações do Gerenciador de pacotes no Visual Studio.

![Configurações do Gerenciador de pacotes](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Restauração de pacote simplificada da linha de comando

NuGet 2.7 introduz um novo recurso para nuget.exe: `nuget.exe restore`

Este novo comando de restauração permite que você facilmente restaurar todos os pacotes para uma solução com um único comando, aceitando um arquivo de solução ou pasta como um argumento. Além disso, esse argumento é inferido quando há apenas uma única solução na pasta atual. Isso significa que todos os seguintes trabalhar em uma pasta que contém um arquivo de solução única (MySolution.sln):

1. restauração de NuGet.exe MySolution.sln
1. restauração de NuGet.exe.
1. restauração de NuGet.exe

O comando Restore abrirá o arquivo de solução e localizar todos os projetos na solução. A partir daí, ele encontrará o `packages.config` arquivos para cada um dos projetos e restaurar todos os pacotes encontrados. Ele também restaura os pacotes de nível da solução localizada no `.nuget\packages.config` arquivo. Para obter mais informações sobre o novo comando de restauração podem ser encontradas na [referência de linha de comando](../tools/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>O novo fluxo de trabalho de restauração de pacote

Estamos empolgados com essas alterações para o pacote de restauração, pois ela introduz um novo fluxo de trabalho. Se você deseja omitir seus pacotes do controle do código-fonte você simplesmente não confirmar o `packages` pasta. Os usuários do Visual Studio que abrir em criar a solução verá os pacotes restaurados automaticamente. Para compilações de linha de comando, simplesmente invocar `nuget.exe restore` antes de invocar `msbuild`. Você não precisa se lembrar de usar o gesto de "Habilitar a restauração do pacote NuGet" em sua solução, e não precisamos modificar seus projetos para alterar a compilação. E isso também resulta em uma experiência muito aprimorada para pacotes que incluem as importações do MSBuild, especialmente para importações adicionadas por meio do recurso recente do NuGet para [importação automaticamente propriedades/destinos arquivos](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) da pasta \build.

Além do trabalho que fizemos sozinhos, também estamos trabalhando com alguns parceiros importantes para aprimorar essa nova abordagem. Ainda não temos cronogramas concretas para qualquer um deles, mas cada parceiro é tão empolgado quantos nós sobre a nova abordagem.

* Team Foundation Service - estão trabalhando para integrar a chamada para `nuget.exe restore` padrão compilar cenários.
* Sites do Azure do Windows - eles estão trabalhando para permitir que você enviar por push o seu projeto para o Azure e tenha `nuget.exe restore` chamado antes que seu site da web é criado.
* TeamCity – eles estão atualizando seu plug-in do instalador do NuGet para TeamCity 8.x
* AppHarbor - estão trabalhando para permitir que você enviar por push o seu repositório para AppHarbor e ter `nuget.exe restore` chamado antes de sua solução é a compilação.

Com cada um dos parceiros acima, devem usar sua própria cópia do nuget.exe e você não precisará realizar nuget.exe em sua solução.

#### <a name="known-issues"></a>Problemas Conhecidos

Havia dois problemas conhecidos com a restauração nuget.exe da versão 2.7 inicial, mas eles foram corrigidos em 6/9/2013 com uma atualização para o [CommandLine pacote](http://www.nuget.org/packages/NuGet.CommandLine/).  Essa atualização também está disponível na [página de download do NuGet 2.7](https://nuget.codeplex.com/releases/view/107605) no CodePlex.  Executando `nuget.exe update -self` será atualizada para a versão mais recente.

Foram fixos:

1. [Nova restauração do pacote não funciona no Mono, ao usar arquivos SLN](https://nuget.codeplex.com/workitem/3596)
1. [Nova restauração do pacote não funciona com projetos Wix](https://nuget.codeplex.com/workitem/3598)

Também há um problema conhecido com o novo fluxo de trabalho de restauração de pacote no qual [restauração automática do pacote não funciona para projetos em uma pasta de solução](https://nuget.codeplex.com/workitem/3625). Esse problema foi corrigido no NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Erros/avisos de compilação de redirecionamento do projeto e atualização

Muitas vezes após o redirecionamento ou upgrade de seu projeto, você achar que alguns pacotes do NuGet não estão funcionando corretamente. Infelizmente, não há nenhuma indicação de que isso e, em seguida, não há nenhuma orientação sobre como endereçá-lo. Com o NuGet 2.7, agora podemos usar alguns eventos do Visual Studio reconheça quando você tiver redirecionados ou atualizou o seu projeto de forma que afeta seus pacotes NuGet instalados.

Se detectarmos que qualquer um dos seus pacotes foram afetados pelo redirecionamento ou upgrade, podemos irá produzir erros de compilação de imediato para informá-lo. O erro de build de imediato, além de também mantemos um `requireReinstallation="true"` sinalizador em seu `packages.config` arquivo para todos os pacotes que foram afetados pelo redirecionamento e cada subsequentes de compilação no Visual Studio irá gerar avisos de build para esses pacotes.

Embora o NuGet não pode executar a ação automática para reinstalar os pacotes afetados, esperamos que essa indicação e aviso vai guiá-ajuda você descobrir quando você precisa reinstalar pacotes. Também estamos trabalhando na [documentação de diretrizes de reinstalação do pacote](../consume-packages/reinstalling-and-updating-packages.md) que essas mensagens de erro direcionará você para.

### <a name="nuget-configuration-defaults"></a>Padrões de configuração do NuGet

Muitas empresas estão usando o NuGet internamente, mas tiveram dificuldade para orientar seus desenvolvedores para usar origens do pacote interno em vez do nuget.org. NuGet 2.7 apresenta um recurso de padrões de configuração que permite que os padrões de todo o computador deve ser especificado para:

1. Origens de pacote habilitado
1. Origens de pacote registrado, mas desabilitado
1. Origem de push padrão nuget.exe

Cada um deles agora pode ser configurada dentro de um arquivo localizado em `%ProgramData%\NuGet\NuGetDefaults.Config`. Se esse arquivo de configuração especifica a origens de pacote, a origem do pacote nuget.org padrão não será registrada automaticamente e aqueles em `NuGetDefaults.Config` será registrado.

Embora não seja necessário usar esse recurso, esperamos que as empresas implantem `NuGetDefaults.Config` arquivos usando a diretiva de grupo.

*Observe que esse recurso nunca fará com que uma origem de pacote a ser removido das configurações do NuGet do desenvolvedor. Isso significa que se o desenvolvedor já tiver usado o NuGet e, portanto, tem a origem do pacote nuget.org registrado, ele não será removido após a criação de um `NuGetDefaults.Config` arquivo.*

Ver [padrões de configuração do NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) para obter mais informações sobre esse recurso.

### <a name="renaming-the-default-package-source"></a>Renomeando a origem do pacote padrão

O NuGet sempre tiver registrado uma origem de pacote padrão chamada "Oficial origem do pacote NuGet" que aponta para o nuget.org. Esse nome foi detalhado e ele também não especificar onde ele estava realmente apontando. Para resolver esses dois problemas, mudamos o nome desta origem do pacote para simplesmente "nuget.org" na interface do usuário. A URL para a origem do pacote também foi alterada para incluir o "www". group. Depois de usar o NuGet 2.7, seu "NuGet oficial origem do pacote existente" será automaticamente atualizada para "nuget.org" como seu nome e "<https://www.nuget.org/api/v2/>" como sua URL.

### <a name="performance-improvements"></a>Melhorias de desempenho

Fizemos uma melhora de desempenho no 2.7 que produzirá o volume de memória menor, menos uso de disco e instalações mais rápidas do pacote. Também fizemos consultas mais inteligentes feeds baseado em OData que reduzirá a carga geral.

### <a name="new-extensibility-apis"></a>Novas APIs de extensibilidade

Adicionamos algumas novas APIs para nossos serviços de extensibilidade para preencher a lacuna das funcionalidades ausentes nas versões anteriores.

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

### <a name="development-only-dependencies"></a>Dependências de desenvolvimento

Esse recurso foi contribuição [Adam Ralph](https://twitter.com/adamralph) e permite que os autores de pacote declarar as dependências que foram usadas apenas no desenvolvimento de tempo e não exigem as dependências do pacote. Adicionando um `developmentDependency="true"` atributo a um pacote no `packages.config`, `nuget.exe pack` não incluirão mais esse pacote como uma dependência.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Removemos o suporte para o Visual Studio 2010 Express para Windows Phone

O novo modelo de restauração de pacote no 2.7 é implementado por um novo VSPackage que é diferente do NuGet VSPackage principal. Devido a um problema técnico, esse novo VSPackage não funciona corretamente na *Visual Studio 2010 Express para Windows Phone* SKU como podemos compartilhar a mesma base de código com os outros há suporte para SKUs do Visual Studio. Portanto, começando com o NuGet 2.7, podemos está descartando o suporte para *Visual Studio 2010 Express para Windows Phone* da extensão publicada. Suporte para *Visual Studio 2010 Express para Web* ainda está incluída na extensão do primário publicado na Galeria de extensão do Visual Studio.

Como estamos não sabe quantos desenvolvedores ainda estiver usando o NuGet nessa versão/edição do Visual Studio, estamos publicando uma extensão separada do Visual Studio especificamente para os usuários e publicá-lo no CodePlex (em vez de galeria de extensão do Visual Studio) . Não planejamos continuar a manter essa extensão, mas se isso afeta você, fale conosco através do preenchimento de um problema no CodePlex.

Para baixar o NuGet Package Manager (para Visual Studio 2010 Express para Windows Phone), visite o [Downloads do NuGet 2.7](https://nuget.codeplex.com/releases/view/107605) página.

### <a name="bug-fixes"></a>Correções de Bug

Além desses recursos, esta versão do NuGet também inclui muitas correções de bugs. Havia 97 total de problemas abordados na versão. Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.7, por favor, modo de exibição de [rastreador de problemas do NuGet para esta versão](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
