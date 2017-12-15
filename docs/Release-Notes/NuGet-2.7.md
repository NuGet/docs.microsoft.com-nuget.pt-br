---
title: "Notas de versão do NuGet 2.7 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba2edaad-4795-47a0-a572-d0e1716bd540
description: "Notas de versão do NuGet 2.7 incluindo correções de bugs, problemas conhecidos, recursos adicionados e DCRs."
keywords: "Notas de versão 2.7 NuGet, correções de bugs, problemas conhecidos, adicionaram recursos, DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 502cb5e68f905e9ad8f4003bb0690d3e676f6bb7
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-27-release-notes"></a>Notas de versão 2.7 do NuGet

[NuGet 2.6.1 para notas de versão do WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 notas de versão](../release-notes/nuget-2.7.1.md)

2.7 NuGet foi lançado em 22 de agosto de 2013.

## <a name="acknowledgements"></a>Confirmações

Gostaríamos de agradecer seguintes colaboradores externos por suas contribuições significativas para o NuGet 2.7:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Mostre o url de licença ao listar pacotes e detalhamento é detalhado.
1. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -adicionar o atributo developmentDependency `packages.config` e usá-lo no comando de pacote para incluir apenas os pacotes de tempo de execução
1. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Evite a chave duplicada de propriedades no comando de pacote de nuget.exe.
1. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -Aumentar tamanho de cache de máquina para 200.
1. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -corrigir NuGet diálogo mostrando as atualizações na guia errada
    - Correção Project.TargetFramework pode ser nulo em GerenteDoProjeto
    - [#3248](http://nuget.codeplex.com/workitem/3248) -corrigir SharedPackageRepository FindPackage/FindPackagesById falhará em packageId inexistente
1. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -habilitar o suporte para o projeto Nomad
1. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [&#3252;](http://nuget.codeplex.com/workitem/3252) -falha de comando de envio de correção com exit código 0 quando o arquivo não existe.
1. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -correção de bugs com o comando Add-BindingRedirect quando um projeto faz referência a um projeto de banco de dados.
1. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -correção de bug de nuget.pack análise curinga no atributo 'exclude' incorretamente.
1. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
    - [#3307](http://nuget.codeplex.com/workitem/3307) -correção de bug `NuGet.targets` não passa $(Platform) nuget.exe durante a restauração de pacotes.
1. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
    - [#3294](http://nuget.codeplex.com/workitem/3294) -correção de bug no comando de pacote de nuget.exe que poderia permitir a adição de arquivos com o mesmo nome mas com maiusculas e minúsculas diferentes, causando eventualmente exceção "Item já existe".
1. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
    - [#2990](http://nuget.codeplex.com/workitem/2990) -propriedade de versão de adicionar a classe NetPortableProfile.
1. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
    - [#3460](https://nuget.codeplex.com/workitem/3460) -correção de bug NullReferenceException se requireApiKey = true, mas o cabeçalho X-NUGET-APIKEY não estiver presente
1. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
    - [#3278](https://nuget.codeplex.com/workitem/3278) -NuGet.Build corrige destinos de arquivo para que ele funciona corretamente em MonoDevelop
1. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
    - Melhorar o desempenho do comando de restauração, aumentando a paralelização

## <a name="notable-features-in-the-release"></a>Recursos importantes da versão

### <a name="package-restore-by-default-with-implicit-consent"></a>Restauração do pacote por padrão (com consentimento implícito)

2.7 NuGet apresenta uma nova abordagem para restauração do pacote e também supera um grande desafio: consentimento de restauração do pacote está ativada por padrão! A combinação da nova abordagem e o consentimento implícito drasticamente simplificará os cenários de restauração de pacote.

#### <a name="implicit-consent"></a>Consentimento implícito

Com as versões 2.0, 2.1, 2.2, 2.5 e 2.6 do NuGet, os usuários necessários para permitir explicitamente o NuGet Baixe pacotes ausentes durante a compilação. Se esse consentimento não tivesse sido explicitamente fornecido, e soluções que tinham habilitado a restauração do pacote não conseguirá criar até que o usuário tinha recebeu o consentimento.

A partir do NuGet 2.7, consentimento de restauração do pacote está ativado por padrão, permitindo aos usuários explicitamente *recusar* de restauração do pacote, se desejado, usando a caixa de seleção nas configurações do NuGet no Visual Studio. Essa alteração de consentimento implícito afeta NuGet nos seguintes ambientes:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* Utilitário de linha de comando NuGet.exe

#### <a name="automatic-package-restore-in-visual-studio"></a>Restauração automática de pacotes no Visual Studio

A partir do NuGet 2.7, NuGet baixará automaticamente os pacotes ausentes durante a compilação do Visual Studio, mesmo se a restauração do pacote ainda não foi explicitamente habilitada para a solução. Este pacote restauração automática ocorre no Visual Studio quando você criar um projeto ou solução, mas antes de MSBuild é invocado. Isso resulta em alguns benefícios significativos:

1. Nenhuma outra precisa usar o gesto de "Habilitar a restauração de pacotes NuGet" em sua solução
1. Projetos não precisam ser modificada e o NuGet não fazer alterações ao seu projeto para garantir a restauração do pacote está habilitada
1. Todos os pacotes do NuGet, incluindo aqueles que incluídos importações do MSBuild para arquivos props/destinos, serão restaurados *antes de* MSBuild é invocado, garantindo que os props/destinos reconhecidos adequadamente durante a compilação

Para usar a restauração automática de pacotes no Visual Studio, você só precisará executar uma (ação em):

1. Não marcar seu `packages` pasta

Há várias maneiras para omitir o `packages` pasta do controle de origem. Para obter mais informações, consulte o [pacotes e controle de origem](../consume-packages/packages-and-source-control.md) tópico.

Enquanto todos os usuários são implicitamente aceitado o consentimento a restauração automática de pacotes, você pode facilmente recusá-lo através das configurações do Gerenciador de pacotes no Visual Studio.

![Configurações do Gerenciador de pacote](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Restauração do pacote simplificado na linha de comando

2.7 NuGet apresenta um novo recurso para nuget.exe:`nuget.exe restore`

Este novo comando de restauração permite que você facilmente restaurar todos os pacotes para uma solução com um único comando, aceitando um arquivo de solução ou a pasta como um argumento. Além disso, esse argumento é implícita quando há apenas uma única solução na pasta atual. Isso significa que todos os procedimentos de trabalho de uma pasta que contém um arquivo de solução única (MySolution.sln):

1. restauração de NuGet.exe MySolution.sln
1. restauração de NuGet.exe.
1. restauração de NuGet.exe

O comando de restauração irá abrir o arquivo de solução e localizar todos os projetos na solução. A partir daí, ele encontrará os `packages.config` arquivos para cada um dos projetos e restaurar todos os pacotes encontrados. Também restaura os pacotes de solução de nível, localizada no `.nuget\packages.config` arquivo. Para obter mais informações sobre o novo comando de restauração podem ser encontradas na [referência de linha de comando](../tools/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>O novo fluxo de trabalho de restauração do pacote

Estamos felizes sobre essas alterações para a restauração de pacotes, como ela introduz um novo fluxo de trabalho. Se você deseja omitir os pacotes do controle de origem você simplesmente não confirmar o `packages` pasta. Os usuários do Visual Studio que abrir em Compile a solução verá os pacotes automaticamente restaurados. Para compilações de linha de comando, basta invocar `nuget.exe restore` antes de chamar `msbuild`. Você não precisará Lembre-se de usar o gesto de "Habilitar a restauração de pacotes NuGet" em sua solução e que não precisamos modificar seus projetos para alterar a compilação. E isso também resulta em uma experiência mais aprimorada para pacotes que incluem importações do MSBuild, especialmente para importações adicionadas por meio do recurso de recente do NuGet para [importar automaticamente props/destinos arquivos](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) da pasta \build.

Além do trabalho que fizemos sozinhos, estamos também trabalhando com alguns parceiros importantes para refinar essa nova abordagem. Não temos concretas cronogramas para qualquer uma dessas ainda, mas cada parceiro é como felizes, já que estamos sobre a nova abordagem.

* Serviço do Team Foundation - estão trabalhando para integrar a chamada para `nuget.exe restore` padrão criar cenários.
* Windows Azure Web Sites - estão trabalhando para permitir que você enviar por push o seu projeto no Azure e ter `nuget.exe restore` chamado antes de seu site da web é criado.
* TeamCity - eles estão atualizando seu plug-in do instalador do NuGet para TeamCity 8. x
* AppHarbor - estão trabalhando para permitir que você enviar por push o seu repositório para AppHarbor e `nuget.exe restore` antes que sua solução de compilação.

Com cada um dos parceiros acima, devem usar sua própria cópia do nuget.exe e você não precisa realizar nuget.exe em sua solução.

#### <a name="known-issues"></a>Problemas conhecidos

Havia dois problemas conhecidos com a restauração de nuget.exe com a versão 2.7 inicial, mas eles foram corrigidos em 9/6/2013 com uma atualização para o [NuGet.CommandLine pacote](http://www.nuget.org/packages/NuGet.CommandLine/).  Essa atualização também está disponível no [página de download do NuGet 2.7](https://nuget.codeplex.com/releases/view/107605) no CodePlex.  Executando `nuget.exe update -self` será atualizada para a versão mais recente.

Foram fixos:

1. [Nova restauração do pacote não funciona em Mono ao usar arquivos SLN](https://nuget.codeplex.com/workitem/3596)
1. [Nova restauração do pacote não funciona com projetos Wix](https://nuget.codeplex.com/workitem/3598)

Também há um problema conhecido com o novo fluxo de trabalho de restauração do pacote no qual [restauração automática de pacotes não funciona para projetos em uma pasta de solução](https://nuget.codeplex.com/workitem/3625). Esse problema foi corrigido no NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Erros/avisos de compilação de redirecionamento do projeto e atualização

Muitas vezes depois de redirecionamento ou atualizar seu projeto, você achar que alguns pacotes do NuGet não estão funcionando corretamente. Infelizmente, não há nenhuma indicação de que isso e, em seguida, não há nenhuma orientação sobre como endereçá-lo. Com o NuGet 2.7, agora usamos alguns eventos do Visual Studio para reconhecer quando tiver sido redirecionado ou atualizado o seu projeto de forma que afeta seus pacotes do NuGet instaladas.

Se é possível detectar se qualquer um dos seus pacotes foram afetados pelo redirecionamento ou atualização, podemos produzirá erros de compilação imediata para informá-lo. Além de erro de compilação imediata, podemos também mantêm uma `requireReinstallation="true"` sinalizador no seu `packages.config` arquivo para todos os pacotes que foram afetados pelo redirecionamento e cada subsequentes de compilação no Visual Studio gerará avisos de compilação para esses pacotes.

Embora o NuGet não é possível executar a ação automática para reinstala os pacotes afetados, esperamos que essa indicação e aviso vai guiá-ajuda você descobrir quando precisar reinstala os pacotes. Também estamos trabalhando em [documentação de diretrizes de reinstalação do pacote](../consume-packages/reinstalling-and-updating-packages.md) que essas mensagens de erro direcioná-lo para.

### <a name="nuget-configuration-defaults"></a>Padrões de configuração do NuGet

Muitas empresas estão usando o NuGet internamente, mas tiveram um tempo de disco rígido orientando seus desenvolvedores para usar origens do pacote interno em vez de nuget.org. 2.7 NuGet apresenta um recurso de padrões de configuração que permite que os padrões de todo o computador deve ser especificado para:

1. Fontes de pacote habilitado
1. Fontes de pacote registrado, mas desabilitado
1. A origem de envio de nuget.exe padrão

Cada um deles agora pode ser configurada em um arquivo localizado em `%ProgramData%\NuGet\NuGetDefaults.Config`. Se esse arquivo de configuração especifica origens do pacote, a origem do pacote nuget.org padrão não será registrada automaticamente e os `NuGetDefaults.Config` será registrado.

Embora não seja necessário para usar esse recurso, esperamos que as empresas implantem `NuGetDefaults.Config` arquivos usando a diretiva de grupo.

*Observe que esse recurso nunca fará com que uma origem do pacote a ser removido das configurações do NuGet do desenvolvedor. Isso significa que se o desenvolvedor já tiver usado o NuGet e, portanto, a origem do pacote nuget.org registrado, ele não será removido após a criação de um `NuGetDefaults.Config` arquivo.*

Consulte [padrões de configuração NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) para obter mais informações sobre esse recurso.

### <a name="renaming-the-default-package-source"></a>Renomear a origem do pacote padrão

NuGet sempre registrou uma origem de pacote padrão chamada "NuGet oficial origem do pacote" que aponta para nuget.org. Esse nome é detalhado e também não especificar onde ele foi realmente apontando. Para resolver esses dois problemas, nós já renomeou esta origem de pacote para simplesmente "nuget.org" na interface de usuário. A URL de origem do pacote também foi alterada para incluir o "www". group. Depois de usar NuGet 2.7, seu "NuGet oficial origem do pacote existente" será atualizada automaticamente para "nuget.org" como seu nome e "https://www.nuget.org/api/v2/" como a URL.

### <a name="performance-improvements"></a>Melhorias de desempenho

Fizemos alguma melhoria no desempenho em 2.7 que produzirá o espaço de memória menor, menor uso de disco e a instalação de pacote mais rápida. Também fizemos consultas mais inteligentes feeds baseado em OData que reduza a carga geral.

### <a name="new-extensibility-apis"></a>Novas APIs de extensibilidade

Adicionamos algumas novas APIs para nossos serviços de extensibilidade para preencher a lacuna de funcionalidades ausentes nas versões anteriores.

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

Esse recurso foi contribuição de [Adam Ralph](https://twitter.com/adamralph) e permite que os autores de pacote declarar dependências que só foram usadas no desenvolvimento de tempo e não exigem que as dependências do pacote. Adicionando um `developmentDependency="true"` a um pacote no atributo `packages.config`, `nuget.exe pack` não incluirá esse pacote como uma dependência.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Removeu o suporte para Visual Studio 2010 Express para Windows Phone

O novo modelo de restauração do pacote do 2.7 é implementado por um novo VSPackage que é diferente do NuGet VSPackage principal. Devido a um problema técnico, esse novo VSPackage não funciona corretamente no *Visual Studio 2010 Express para Windows Phone* SKU compartilham a mesma base de código com os outros suporte para SKUs do Visual Studio. Portanto, a partir do NuGet 2.7, podemos está cancelando suporte *Visual Studio 2010 Express para Windows Phone* da extensão de publicado. Suporte para *Visual Studio 2010 Express para Web* ainda está incluído na extensão primária publicado na Galeria de extensão do Visual Studio.

Como estamos não souber como muitos desenvolvedores ainda estejam usando o NuGet nessa versão/edição do Visual Studio, estamos publicando uma extensão do Visual Studio separada especificamente para esses usuários e publicá-lo no CodePlex (em vez da Galeria de extensões do Visual Studio) . Não pretendemos continuam a manter essa extensão, mas se isso afeta informe-nos preenchendo um problema no CodePlex.

Para baixar o NuGet Package Manager (para Visual Studio 2010 Express para Windows Phone), visite o [NuGet 2.7 Downloads](https://nuget.codeplex.com/releases/view/107605) página.

### <a name="bug-fixes"></a>Correções de Bug

Além desses recursos, esta versão do NuGet também inclui muitas correções de bugs. Não havia 97 questões total na versão. Para obter uma lista completa de trabalho itens corrigidos no NuGet 2.7, por favor, exibição de [NuGet Issue Tracker para esta versão](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
