---
title: Notas de Versão do NuGet 4.0 RTM
description: Notas de versão do NuGet 4.0 RTM incluindo problemas conhecidos, correções de bugs, recursos adicionados e DCRs.
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c3ec5c20e5175edd315de20ca98c7a106c51809e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776278"
---
# <a name="nuget-40-rtm-release-notes"></a>Notas de Versão do NuGet 4.0 RTM

O [Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) vem com o NuGet 4.0, que adiciona suporte para o .NET Core, tem várias correções de qualidade e melhora o desempenho. Esta versão também proporciona várias melhorias, como suporte para PackageReference, comandos do NuGet como destinos do MSBuild, restauração do pacote em segundo plano e muito mais.

## <a name="known-issues"></a>Problemas conhecidos

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a>Talvez a restauração do NuGet falhe quando você tem vários projetos referenciando outro projeto em uma solução

#### <a name="issue"></a>Problema

Talvez a restauração do NuGet não funcionará se, em uma solução, você tiver referências do projeto no mesmo projeto com maiúsculas e minúsculas diferentes ou com diferentes caminhos relativos. [NuGet#4574](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a>Solução alternativa

Corrija as maiúsculas ou caminhos relativos para que eles sejam os mesmos para todas as referências do projeto.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Ao usar o Console do Gerenciador de Pacotes, talvez a tecla 'Enter' não funcione

#### <a name="issue"></a>Problema

Às vezes, a tecla enter não funciona no Console do Gerenciador de Pacotes. Se isso ocorrer, confira o progresso na correção e forneça informações úteis adicionais sobre as etapas de reprodução. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Solução alternativa

Reinicie o Visual Studio e abra o PMC antes de abrir a solução. Como alternativa, experimente excluir o `project.lock.json` e restaurá-lo novamente.

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>Em projetos .NET Core, talvez você acabe em loop de restauração infinito ao usar um pacote que contém um assembly com uma assinatura inválida

#### <a name="issue"></a>Problema

Às vezes, quando você usa um pacote que contém um assembly com uma assinatura inválida ou quando a versão do pacote é definida com o ticker 'DateTime', isso faz com que a restauração automática de pacotes seja executada em loop infinito. [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>Solução alternativa

No momento, não há uma solução alternativa para esse problema.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Você não consegue exibir, adicionar ou atualizar o DotNetCLITools usando o Gerenciador de Pacotes NuGet

#### <a name="issue"></a>Problema

O Gerenciador de Pacotes do NuGet não exibe nem permite a adição/atualização de DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Solução alternativa

O DotNetCLIToolReferences deve ser editado manualmente no arquivo de projeto.

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a>Haverá falha na restauração do NuGet quando você definir a propriedade PackageId para projetos

#### <a name="issue"></a>Problema

Para projetos .NET Core, a restauração do NuGet no Visual Studio não respeita a propriedade PackageId de projetos. [NuGet#4586](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a>Solução alternativa

Execute a restauração usando a linha de comando.

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a>Quando seu projeto não tiver a pasta 'obj', poderá haver falha na restauração do pacote

#### <a name="issue"></a>Problema

O Visual Studio não restaura PackageReferences quando a pasta 'obj' foi excluída do Visual Studio. [NuGet#4528](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a>Solução alternativa

Crie a pasta 'obj' manualmente e a restauração deverá funcionar.

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a>Pode haver falha na atualização manual dos pacotes usando o pacote de atualização no console

#### <a name="issue"></a>Problema

O uso manual do pacote de atualização no console funciona somente uma vez para projetos PackageReferences que acabaram de ser convertidos. [NuGet#4431](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a>Solução alternativa

No momento, não há uma solução alternativa para esse problema.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto

#### <a name="issue"></a>Problema

Redirecionar a versão da estrutura de destino pode levar a um IntelliSense incompleto no Visual Studio. Isso acontece quando você está usando PackageReferences como o formato do gerenciador de pacotes. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Solução alternativa

Faça uma restauração manual.

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a>O msbuild /t:restore falha quando um projeto que define como destino o .NET461 referencia outro projeto que define como destino o .NETStandard

#### <a name="issue"></a>Problema

O msbuild /t:restore falha quando um projeto baseado em PackageReferenece que define como destino o .NET461 referencia outro projeto baseado em PackageReference que define como destino o .NETStandard.  [NuGet#4532](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a>Solução alternativa

No momento, não há uma solução alternativa para esse problema.

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>Problemas corrigidos no período de tempo do NuGet 4.0 RTM

[Notas de Versão do NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md) -Lista todos os problemas corrigidos para o NuGet 4.0 RC

### <a name="features"></a>Recursos

- Localizar cadeias de caracteres em NuGet.Core.sln – [#2041](https://github.com/NuGet/Home/issues/2041)

- O NuGet força o carregamento de projetos de aplicativo Web no modo LSL – [#4258](https://github.com/NuGet/Home/issues/4258)

- Suporte a AutoReferenced PackageReference para bloquear alterações de versão na interface do usuário para pacotes com “sdk instalado” – [#4044](https://github.com/NuGet/Home/issues/4044)

- Comunicar corretamente PackageSpec.Version para todas as dependências do projeto (PackageRef) – [#3902](https://github.com/NuGet/Home/issues/3902)

- suporte à remoção de referências em `.csproj` das linhas de comando – [#4101](https://github.com/NuGet/Home/issues/4101)

- Suporte à restauração de projetos de PackageReference (normal e xplat) e Lightweight Solution Load – [#4003](https://github.com/NuGet/Home/issues/4003)

- suporte à adição de referências em `.csproj` das linhas de comando – [#3751](https://github.com/NuGet/Home/issues/3751)

- Suporte de restauração do NuGet para Lightweight Solution Load para `packages.config` ou `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)

- Suporte para contentFiles no arquivo de destino gerado no nuget – [#3683](https://github.com/NuGet/Home/issues/3683)

- Estabelecer um IC Mono para validação do nuget.exe no Mac usando o MSBuild – [#3646](https://github.com/NuGet/Home/issues/3646)

- Retirar o NuGet de dependências do NuGet.Core v2 – [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>Bugs

- A restauração do NuGet no Visual Studio não respeita a propriedade PackageId de projetos – [#4586](https://github.com/NuGet/Home/issues/4586)

- Erro de NuGet ProjectSystemCache ao adicionar o pacote no pacote do vsix – [#4545](https://github.com/NuGet/Home/issues/4545)

- O pacote gera uma exceção se IncludeSource for usado em um projeto com várias TFMs – [#4536](https://github.com/NuGet/Home/issues/4536)

- Falha no VS 2017 RC3 ao usar a atualização do gerenciamento de pacotes de toda a solução – [#4474](https://github.com/NuGet/Home/issues/4474)

- Não é possível desinstalar o pacote recém-instalado – [#4435](https://github.com/NuGet/Home/issues/4435)

- Ao migrar para o PackageRef, soluções híbridas demonstram um comportamento estranho de restauração – [#4433](https://github.com/NuGet/Home/issues/4433)

- Compilar logo após iniciar a operação do NuGet (instalação, atualização, restauração) pode fazer com que o VS pare de responder – [#4420](https://github.com/NuGet/Home/issues/4420)

- Interface do usuário sem resposta – Deadlock ao inicializar NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)

- adicionar o comando ao pacote deverá adicionar a versão como atributo, em vez de elemento – [#4325](https://github.com/NuGet/Home/issues/4325)

- dotnet
  - dotnetcore Restore foo.sln – falha quando as configurações no SLN causam a duplicação de projetos (mas com configurações diferentes) no grafo de restauração – [#4316](https://github.com/NuGet/Home/issues/4316)

- Pacotes somente de conteúdo – [#3668](https://github.com/NuGet/Home/issues/3668)

- Por padrão, recuse a opção do seletor de formato de pacote – [#4468](https://github.com/NuGet/Home/issues/4468)

- Desempenho: o projeto CreateUAP_CSharp_VS.01.1.Create regrediu Duration_TotalElapsedTime 3.153,570 ms (149,1%). Linha de base 26129.02 – [#4452](https://github.com/NuGet/Home/issues/4452)

- Desempenho: a solução ManagedLangs_CS_DDRIT.0300.Rebuild regrediu Duration_TotalElapsedTime em 1,5 segundo. Linha de base 26105 – [#4441](https://github.com/NuGet/Home/issues/4441)

- A indicação falha em projetos multi-TFM – [#4419](https://github.com/NuGet/Home/issues/4419)

- Desempenho: a solução WebForms_DDRIT.1200.Close regrediu VM_ImagesInMemory_Total_devenv pela contagem de 3,000 (0,5%). Linha de base 26123.04 – [#4408](https://github.com/NuGet/Home/issues/4408)

- vsfeedback – Avisos de pacote durante o direcionamento para netcoreapp1.1 – [#4397](https://github.com/NuGet/Home/issues/4397)

- PathTooLongException ao tentar adicionar um pacote do NuGet ao aplicativo Web vazio do ASP.NET Core – [#4391](https://github.com/NuGet/Home/issues/4391)

- O pacote é executado com muita frequência – dotnet
  - dotnetcore pack falha com o erro “Há uma dependência circular no grafo de dependência de destino envolvendo o destino ‘Pack’” – [#4381](https://github.com/NuGet/Home/issues/4381)

- O pacote é executado com muita frequência – A geração de pacote do NuGet não inclui todas as configurações – [#4380](https://github.com/NuGet/Home/issues/4380)

- O nuget que adiciona NullReferenceException com packageref em projetos do C++ – [#4378](https://github.com/NuGet/Home/issues/4378)

- Acessibilidade: o narrator não narrar a caixa de seleção para escolher os projetos para instalar o pacote – [#4366](https://github.com/NuGet/Home/issues/4366)

- O NuGet VS17 esporadicamente falha ao se conectar com feeds VSO/VSTS – Bug do VS 365798 – [#4365](https://github.com/NuGet/Home/issues/4365)

- contentFiles são colocados no local incorreto se o PackagePath especificar o caminho como “contentFiles” – [#4348](https://github.com/NuGet/Home/issues/4348)

- O destino do pacote acrescenta a propriedade PackageVersion com VersionSuffix – [#4324](https://github.com/NuGet/Home/issues/4324)

- Especificar o caminho do pacote não funciona com o dotnet pack – [#4321](https://github.com/NuGet/Home/issues/4321)

- O NuGet produz diversos avisos sobre importações duplicadas durante a restauração – [#4304](https://github.com/NuGet/Home/issues/4304)

- A escolha da caixa de diálogo “Formato do Gerenciador de Pacotes do NuGet” é exibida incorretamente no tema escuro – [#4300](https://github.com/NuGet/Home/issues/4300)

- Falha do VS na restauração de build – [#4298](https://github.com/NuGet/Home/issues/4298)

- Deadlocks do Visual Studio se você adicionar TFM no targetframeworks, salvar e depois compilar. 10% do tempo – [#4295](https://github.com/NuGet/Home/issues/4295)

- nuget pack não produz a mensagem de êxito quando o empacotamento de um projeto é bem-sucedido – [#4294](https://github.com/NuGet/Home/issues/4294)

- PackTask falha porque System.IO.Compression 4.1 não foi encontrado – [#4290](https://github.com/NuGet/Home/issues/4290)

- O pacote é executado com muita frequência – PackTask falha com frequência com conflito de acesso de arquivo – [#4289](https://github.com/NuGet/Home/issues/4289)

- O NuGet abre a janela de saída durante a restauração de tela de fundo – [#4274](https://github.com/NuGet/Home/issues/4274)

- Eliminar ServiceProvider como padrão de codificação perigoso (o que pode fazer o sistema parar de responder) – [#4268](https://github.com/NuGet/Home/issues/4268)

- Perf/UIHang – Melhorar leituras de DownloadTimeoutStream – [#4266](https://github.com/NuGet/Home/issues/4266)

- Ocorre um deadklock no Visual Studio se você tentar fechar um projeto antes do NuGet concluir a restauração – [#4257](https://github.com/NuGet/Home/issues/4257)

- Problemas com PackTask e empacotamento `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)

- [vsfeedback] Não é possível resolver pacotes do nuget no novo projeto (é preciso reiniciar o visual studio) – [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] A lista suspensa “Version” que mostra as versões de pacote disponíveis se esforça para permanecer em sincronia com o pacote do nuGet selecionado... – [#4198](https://github.com/NuGet/Home/issues/4198)

- O Nuget.Client deve usar CPS JoinableTaskFactory ao interagir com o CPS para evitar deadlocks – [#4185](https://github.com/NuGet/Home/issues/4185)

- O NuGet 3.5.0 não desempacota `.targets` do pacote – [#4171](https://github.com/NuGet/Home/issues/4171)

- dotnet
  - dotnetcore pack não é compatível com o título no `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)

- Install-Package resulta em uma caixa de diálogo de erro no VS2017 RC – [#4127](https://github.com/NuGet/Home/issues/4127)

- A atualização de um pacote para o projeto do .net core parece não funcionar, pois a interface do usuário não obtém a atualização do CPS do indicado. - [#4035](https://github.com/NuGet/Home/issues/4035)

- Melhorar o aviso de referência não resolvida – [#3955](https://github.com/NuGet/Home/issues/3955)

- dotnet
  - Pacote de dotnetcore – ProjectReference perde informações de versão – [#3953](https://github.com/NuGet/Home/issues/3953)

- Criar o projeto de criação de aplicativos UWP e recompilar as regressões no tempo decorrido – [#3873](https://github.com/NuGet/Home/issues/3873)

- A mensagem de restauração bem-sucedida é exibida mesmo após um erro durante a restauração. - [#3799](https://github.com/NuGet/Home/issues/3799)

- Publicar novamente o Nuget.CommandLine 3.4.4 para Nuget.org – [#2931](https://github.com/NuGet/Home/issues/2931)

- Na Migração, os projetos mudam de `project.json` para `.csproj` ---falha de restauração – [#4297](https://github.com/NuGet/Home/issues/4297)

- Falha de restauração no Projeto de teste xunit recém-criado – [#4296](https://github.com/NuGet/Home/issues/4296)

- Projetos do Core podem parar de responder, travando a interface do usuário ao abrir – [#4269](https://github.com/NuGet/Home/issues/4269)

- corrigir o arquivo de destino para tarefas de build – [#4267](https://github.com/NuGet/Home/issues/4267)

- A lista de erros tem um erro após a solução de build que descarrega o projeto referenciado – [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057: o destino “_GenerateRestoreGraphProjectEntry” não existe no projeto. - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback: a interface do usuário de gerenciador do nuget para a solução falha ao selecionar todos os projetos – [#4191](https://github.com/NuGet/Home/issues/4191)

- O msbuildpath do nuget.exe falha quando há uma barra à direita – [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback: a restauração do NuGet fornece vários avisos de referência de projeto para o projeto LinqToTwitter – [#4156](https://github.com/NuGet/Home/issues/4156)

- O pacote de `.csproj` não inclui o atributo minClientVersion – [#4135](https://github.com/NuGet/Home/issues/4135)

- Atraso do fornecimento de NuGet.Build.Tasks.Pack.dll quando conectado ao VS2017 (d15rel 26014.00) – [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback: falha na restauração de um projeto do VS 2015 gerado com CMake 3.7.1 – [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback: erros de restauração podem obscurecer mensagens de erro mais completas que poderiam ser mostradas pelo build – [#4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] Erro ao restaurar pacotes do NuGet para o projeto de site: o valor não pode ser nulo. - [#4092](https://github.com/NuGet/Home/issues/4092)

- A migração gera “Exceção de referência do objeto” em NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker – [#4067](https://github.com/NuGet/Home/issues/4067)

- dotnet
  - dotnetcore pack deve empacotar as ferramentas com as versões para as quais o pacote foi compilado – [#4063](https://github.com/NuGet/Home/issues/4063)

- Restauração do nova tela de fundo grava milissegundos na barra de status quando a restauração leva segundos – [#4036](https://github.com/NuGet/Home/issues/4036)

- Erro de digitação na falha ao resolver todas as referências do projeto – [#4018](https://github.com/NuGet/Home/issues/4018)

- Habilitar fluxos de trabalho PCM em cenários de referência do pacote – [#4016](https://github.com/NuGet/Home/issues/4016)

- Não é possível localizar os pacotes instalados na interface do usuário do gerenciador de pacotes – [#4015](https://github.com/NuGet/Home/issues/4015)

- dotnet
  - dotnetcore pack falha quando PackagePath está vazio – [#3993](https://github.com/NuGet/Home/issues/3993)

- Falha ao restaurar a tarefa em um cenário com vários usuários – [#3897](https://github.com/NuGet/Home/issues/3897)

- Não é possível alterar o tipo de Conteúdo ao usar a Tarefa de Pacote do NuGet para o empacotamento – [#3895](https://github.com/NuGet/Home/issues/3895)

- A cópia padrão do ContentFiles está incorreta para MsBuild /t:pack – [#3894](https://github.com/NuGet/Home/issues/3894)

- A restauração do pacote de instalação duplica os logs da mensagem de restauração de pacotes – [#3785](https://github.com/NuGet/Home/issues/3785)

- Remover as grades de proteção – A restauração da seção “runtimes” deve se aplicar somente ao projeto atual – [#3768](https://github.com/NuGet/Home/issues/3768)

- A tarefa do pacote coloca arquivos de conteúdo tanto em 'content/' quanto em 'contentFiles/' – [#3718](https://github.com/NuGet/Home/issues/3718)

- dotnet
  - dotnetcore pack3 realiza divisão de marca extra – [#3701](https://github.com/NuGet/Home/issues/3701)

- dotnet
  - dotnetcore pack: empacotar projetos com referências de pacote resulta em aviso de importação duplicada – [#3665](https://github.com/NuGet/Home/issues/3665)

- O log de restauração no VS nem sempre é exibido – [#3633](https://github.com/NuGet/Home/issues/3633)

- Texto de ajuda de locais de NuGet locais ainda menciona cache de pacotes – [#3592](https://github.com/NuGet/Home/issues/3592)

- O Restore3 associa PackageReferences a TargetFrameworks. - [#3504](https://github.com/NuGet/Home/issues/3504)

- O Nuget escolhe uma versão inesperada do MSBuild no VS "15" Preview 4 dev. prompt de comando – [#3408](https://github.com/NuGet/Home/issues/3408)

- Gravar arquivos de objetos/destinos em caso de restauração com falha – [#3399](https://github.com/NuGet/Home/issues/3399)

- O NuGet não respeita as mesma correções de compatibilidade durante a restauração que o MSBuild ao ser executado no prompt de comando do VS 15 – [#3387](https://github.com/NuGet/Home/issues/3387)

- Habilitar novamente o PackFromProjectWithDevelopmentDependencySet para VS15 – [#3272](https://github.com/NuGet/Home/issues/3272)

- Problemas do Blend com o NuGet – [#4043](https://github.com/NuGet/Home/issues/4043)

- Integrar 4.0.0.2067 em repositórios de CLI e SDK para fornecimento com o RC2 – [#4029](https://github.com/NuGet/Home/issues/4029)

- O VS para de responder ao Criar novo aplicativo de Console Core, Fechar a solução, Abrir a solução e Fechar a solução – [#4008](https://github.com/NuGet/Home/issues/4008)

- O sistema para de responder ao abrir o projeto em d15prerel.25916.01 – [#3982](https://github.com/NuGet/Home/issues/3982)

- Corrigir a mensagem doc/help de locais do dotnet/nuget.exe – [#3919](https://github.com/NuGet/Home/issues/3919)

- Inspecionar PackTask em busca de problemas com espaço em branco à direita ou à esquerda – [#3906](https://github.com/NuGet/Home/issues/3906)

- dotnet
  - dotnetcore pack empacota do obj, não do bin – [#3880](https://github.com/NuGet/Home/issues/3880)

- dotnet
  - dotnetcore pack sempre parece definir ProjectReference para 1.0.0 – [#3874](https://github.com/NuGet/Home/issues/3874)

- dotnet
  - dotnetcore pack falha com referências de projeto e <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)

- LockRecursionException em ProjectSystemCache.TryGetProjectNameByShortName – [#3861](https://github.com/NuGet/Home/issues/3861)

- Cortar espaços em branco de propriedades do MSBuild – [#3819](https://github.com/NuGet/Home/issues/3819)

- Consolide os dois eventos de projeto acionados no carregamento do projeto – [#3759](https://github.com/NuGet/Home/issues/3759)

- Bibliotecas de P2P no arquivo `project.assets.json` tem uma Versão incorreta – [#3748](https://github.com/NuGet/Home/issues/3748)

- Falha na restauração devido ao feed sem resposta e ao pacote indisponível – [#3672](https://github.com/NuGet/Home/issues/3672)

- O nuget.exe pode ficar sem responder devido a uma grande quantidade de saídas de erro do MSBuild – [#3572](https://github.com/NuGet/Home/issues/3572)

- A restauração no build falha para o Blend na primeira vez e é bem-sucedida na segunda (cenário de VS corrigido) – [#2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>DCRs

- migrar vsix de vsix v2 para v3 – [#4196](https://github.com/NuGet/Home/issues/4196)

- O NuGet deve ter um mecanismo para obter o caminho para o arquivo de bloqueio no MSBuild – [#3351](https://github.com/NuGet/Home/issues/3351)

- Adicionar ativos de build à verificação de compatibilidade de TFM e ao arquivo de ativos – [#3296](https://github.com/NuGet/Home/issues/3296)

- Definir um novo “Pacote” ProjectCapability nos destinos de Pacote para habilitar funcionalidades relacionadas a Pacotes – [#4146](https://github.com/NuGet/Home/issues/4146)

- Executar o pacote como um destino pós-build condicionado na propriedade "GeneratePackageOnBuild" do MSBuild – [#4145](https://github.com/NuGet/Home/issues/4145)

- Use a propriedade RestoreProjectStyle do NuGet para criar um projeto específico do NuGet – [#4134](https://github.com/NuGet/Home/issues/4134)

- Adaptar a restauração para alteração de referências transitivas do projeto – [#4076](https://github.com/NuGet/Home/issues/4076)

- Adicionar propriedades do NuGet ao arquivo de destino para projetos não UWP – [#4030](https://github.com/NuGet/Home/issues/4030)

- Suporte a UWP TargetPlatformVersion – [#3923](https://github.com/NuGet/Home/issues/3923)

- Comunicar metadados de referência de projeto no sistema de projeto do NuGet – [#3922](https://github.com/NuGet/Home/issues/3922)

- Adicionar interface do usuário ao modo de empacotamento – [#3921](https://github.com/NuGet/Home/issues/3921)

- `.csproj` herdado precisa de NugetTargetMoniker e RuntimeIdentifiers definidos no projeto/destinos – [#3854](https://github.com/NuGet/Home/issues/3854)

- O pacote de instalação pode se sobrepor a recuperação automática – [#3836](https://github.com/NuGet/Home/issues/3836)

- O menu de contexto QueryStatus não aparece quando o VSPackage não está carregado – [#3835](https://github.com/NuGet/Home/issues/3835)

- Restauração de Solução e Restauração de Build ainda mostram caixas de diálogo – [#3789](https://github.com/NuGet/Home/issues/3789)

- Isolar a versão VSSDK no build da solução NuGet.Clients – [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>Links para problemas do GitHub corrigidos no RTM
[Lista de problemas 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[Lista de problemas 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[Lista de problemas 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[Lista de problemas 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[Lista de problemas 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
